---
title: Metadaten importieren
weight: 40
---

# Metadaten importieren



## Vorbereitungen

Wenn der Import nicht für eine leere Instanz ausgeführt wird, sondern 
sich schon Dokumente in der Instanz befinden, sollte vor dem Import 
**unbedingt ein Backup der Datenbank** vorgenommen werden.



## Import

Das Import-Skript wird wie folgt aufgerufen:

{% highlight bash %}
$ $BASEDIR/opus4/scripts/import/MetadataImporter.php <import_file> [<reject_log_file>]
{% endhighlight %}

Bedeutung der Parameter:

+ (mandatory) `<import_file>` 
  + Ablageort der zu importierenden XML-Datei
+ (optional) `<reject_log_file>` 
  + Ablageort der Reject-Datei 
  + Dort werden die *`oldId`* der zu importierenden Dokumente notiert, die nicht 
    erfolgreich importiert werden konnten.

Entfällt der zweite Parameter, dann wird eine Datei **reject.log** im aktuellen
Arbeitsverzeichnis angelegt.  Bitte generell beachten, dass die Datei bei jedem
Durchlauf neu angelegt wird (wird also innerhalb mehrerer Durchläufe der Name
nicht geändert, dann wird die Datei überschrieben).

Die Logausgabe erfolgt aktuell auf die Console.  Bei einem erfolgreichen Import 
(hier am Beispiel des Dokuments mit der *`oldId`* "123") sieht das wie folgt aus:

{% highlight bash %}
$ ./MetadataImporter.php /somepath/test_import.xml

$ Loading XML file '/somepath/test_import.xml' ...
$ ... OK
$ Validate XML file '/somepath/test_import.xml' ...
$ ... OK
$ Start processing of record #123 ...
$ ... OK
$ Import finished successfully. 1 documents were imported.
{% endhighlight %}

Der Import via OPUS-Import-XML kann auch dazu genutzt werden, um Metadaten zu bereits 
in OPUS4 vorhandenen Dokumenten zu aktualisieren.  Der Ablauf ist identisch zum oben 
beschriebenen Import, allerdings muss beachtet werden, dass der neue Datensatz

+ im Attribut *`docId`* die ID des OPUS4-Dokuments enthält,
+ alle gewünschten Metadaten enthält, die in OPUS4 zu dem Dokument gespeichert werden 
  sollen, nicht nur zusätzliche oder zu ändernde (es findet kein "merge" statt, sondern 
  ein "delete" und "insert").

Bereits angehängte Dateien des Dokuments bleiben von dem Update unberührt.



## Fehlerbehandlung

Ein gescheiterter Import erzeugt hingegen folgende Ausgabe (wieder am Beispiel des 
Dokuments mit der *`oldId`* "123"):

{% highlight bash %}
$ ./MetadataImporter.php /somepath/test_import_invalid_enrichmentkey.xml

$ Loading XML file '/somepath/test_import_invalid_enrichmentkey.xml' ...
$ ... OK
$ Validate XML file '/somepath/test_import_invalid_enrichmentkey.xml' ...
$ ... OK
$ Start processing of record #123 ...
$ Error while processing document #123: enrichment key
UnregisteredEnrichmentKey does not exist: No Opus_Db_EnrichmentKeys with
id UnregisteredEnrichmentKey in database.
$ ... SKIPPED
$ Import finished. 0 documents were imported. 1 documents were skipped.
{% endhighlight %}

In diesem Fall wird die *`oldId`* des betroffenen Dokuments / der betroffenen Dokumente in die Datei 
**reject.log** geschrieben.  Es gibt verschiedene Fehlerursachen; die gängigsten sind im Folgenden 
anhand von Beispielen aufgeführt. 



### Übersicht über mögliche Fehlermeldungen


#### **Strukturelle Fehler**

##### **Nicht wohlgeformtes XML**
{% highlight bash %}
$ .../MetadataImporter.php test_import_badformed.xml

$ Loading XML file 'test_import_badformed.xml' ...
$ ... ERROR: Cannot load XML document test_import_badformed.xml: 
make sure it is well-formed.
{% endhighlight %}

##### **Nicht schemavalides XML**
{% highlight bash %}
$ ./MetadataImporter.php test_import_schemainvalid.xml

$ Loading XML file 'test_import_schemainvalid.xml' ...
$ ... OK
$ Validate XML file 'test_import_schemainvalid.xml' ...
$ ... ERROR: XML document test_import_schemainvalid.xml is not valid:
on line 11 (Error 1868): Element 'titleMain': The attribute 'language'
is required but missing.
{% endhighlight %}

##### **Markup im Elementinhalt ohne [CDATA][wiki-cdata]**
{% highlight bash %}
$ ./MetadataImporter.php test_import_invalid_missing_cdata.xml

$ Loading XML file 'test_import_invalid_missing_cdata.xml' ...
$ ... OK
$ Validate XML file 'test_import_invalid_missing_cdata.xml' ...
$ ... ERROR: XML document test_import_invalid_missing_cdata.xml is not valid:
on line 68 (Error 1842): Element 'enrichment': Element content is not allowed, 
because the content type is a simple type definition.
{% endhighlight %}


#### **Inhaltliche Fehler**

##### **Ungültiger Bezeichner `<enrichment key="...">`**
{% highlight bash %}
$ ./MetadataImporter.php test_import_invalid_enrichmentkey.xml

$ Loading XML file 'test_import_invalid_enrichmentkey.xml' ...
$ ... OK
$ Validate XML file 'test_import_invalid_enrichmentkey.xml' ...
$ ... OK
$ Start processing of record #00 ...
$ Error while processing document #00: enrichment key
UnregisteredEnrichmentKey does not exist: No Opus_Db_EnrichmentKeys with
id UnregisteredEnrichmentKey in database.
$ ... SKIPPED
$ Import finished. 0 documents were imported. 1 documents were skipped.
{% endhighlight %}

##### **Ungültiger Bezeichner `<collection id="...">`**
{% highlight bash %}
$ ./MetadataImporter.php test_import_invalid_collectionid.xml

$ Loading XML file 'test_import_invalid_collectionid.xml' ...
$ ... OK
$ Validate XML file 'test_import_invalid_collectionid.xml' ...
$ ... OK
$ Start processing of record #00 ...
$ Error while processing document #00: collection id 12345678 does not
exist: No Opus_Db_Collections with id 12345678 in database.
$ ... SKIPPED
$ Import finished. 0 documents were imported. 1 documents were skipped.
{% endhighlight %}

##### **Ungültiger Bezeichner `<dnbInstitution id="...">`**
{% highlight bash %}
$ ./MetadataImporter.php test_import_invalid_dnbinstitution.xml

$ Loading XML file 'test_import_invalid_dnbinstitution.xml' ...
$ ... OK
$ Validate XML file 'test_import_invalid_dnbinstitution.xml' ...
$ ... OK
$ Start processing of record #00 ...
$ Error while processing document #00: dnbInstitution id 3 does not
exist: No Opus_Db_DnbInstitutes with id 3 in database.
$ ... SKIPPED
$ Import finished. 0 documents were imported. 1 documents were skipped.
{% endhighlight %}

##### **Ungültiger Bezeichner `<dnbInstitution role="...">`**
{% highlight bash %}
$ ./MetadataImporter.php test_import_invalid_dnbinstitutionrole.xml

$ Loading XML file 'test_import_invalid_dnbinstitutionrole.xml' ...
$ ... OK
$ Validate XML file 'test_import_invalid_dnbinstitutionrole.xml' ...
$ ... OK
$ Start processing of record #00 ...
$ Error while processing document #00: given role publisher is not
allowed for dnbInstitution id 1
$ ... SKIPPED
$ Import finished. 0 documents were imported. 1 documents were skipped.
{% endhighlight %}

##### **Ungültiger Bezeichner `<licence id="...">`**
{% highlight bash %}
$ ./MetadataImporter.php test_import_invalid_licenceid.xml

$ Loading XML file 'test_import_invalid_licenceid.xml' ...
$ ... OK
$ Validate XML file 'test_import_invalid_licenceid.xml' ...
$ ... OK
$ Start processing of record #00 ...
$ Error while processing document #00: licence id 999 does not exist: No
Opus_Db_DocumentLicences with id 999 in database.
$ ... SKIPPED
$ Import finished. 0 documents were imported. 1 documents were skipped.
{% endhighlight %}

##### **Ungültiger Bezeichner `<seriesItem id="...">`**
{% highlight bash %}
$ ./MetadataImporter.php test_import_invalid_seriesid.xml

$ Loading XML file 'test_import_invalid_seriesid.xml' ...
$ ... OK
$ Validate XML file 'test_import_invalid_seriesid.xml' ...
$ ... OK
$ Start processing of record #00 ...
$ Error while processing document #00: series id 123456789 does not
exist: No Opus_Db_Series with id 123456789 in database.
$ ... SKIPPED
$ Import finished. 0 documents were imported. 1 documents were skipped.
{% endhighlight %}


#### **Inhaltliche Fehler beim Update eines vorhandenen Dokuments**

##### **Es gibt kein Dokument mit dem angegebenen Attribut _`docId`_**
{% highlight bash %}
$ ./MetadataImporter.php test_import_invalid_docid.xml

$ Loading XML file 'test_import_invalid_docid.xml' ...
$ ... OK
$ Validate XML file 'test_import_invalid_docid.xml' ...
$ ... OK
$ Start processing of record #00 ...
$ Could not load document #987654321 from database: No Opus_Db_Documents
with id 987654321 in database.
$ ... SKIPPED
$ Import finished. 0 documents were imported. 1 documents were skipped.
{% endhighlight %}



[wiki-cdata]: http://de.wikipedia.org/wiki/CDATA
