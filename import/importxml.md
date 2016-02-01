---
title: XML-Schemata
weight: 20
---

# OPUS Import-XML

Um Metadaten in OPUS4 zu importieren, ist es notwendig, diese auf OPUS-Import-XML zu mappen.  Dieses Format wird im Folgenden dokumentiert.



## Hinweise zu Datenstruktur und -syntax

Im OPUS4-Import-Format entspricht **`opusDocument`** einem Metadatensatz und wird durch Elemente, Unterelemente und Attribute strukturiert.
Das Format wird in der Schemadatei **$BASEDIR/opus4/scripts/import/opus_import.xsd** definiert. Die Reihenfolge der Elemente innerhalb 
von **`opusDocument`** ist bindend.  Attribute spezifizieren die Eigenschaften von Dokumenten und sind immer einem bestimmten Element
zugeordnet.  Die Reihenfolge der Attribute innerhalb eines Elements ist nicht bindend.  Eckige Klammern dienen lediglich der Verständlichkeit
und sind nicht Teil des Formats.


### Kardinalität

Es wird bei den Elementen und Unterelementen zwischen obligatorisch und optional unterschieden.  Darüber hinaus sind einige (Unter)Elemente
(unbegrenzt) wiederholbar.

<p class="info" markdown="1">
  Obligatorisch, nicht wiederholbar ...............: 1  
  Obligatorisch, wiederholbar .......................: 1..n  
  Optional, nicht wiederholbar ......................: 0..1  
  Optional, wiederholbar ..............................: 0..n  
</p>


## Referenzbeschreibung von OPUS-Import-XML

### **1 OPUS-Dokument**

+ Bezeichner: **`opusDocument`**
+ Attribut: obligatorisch: *`oldId`* (beliebiger Inhalt)
  + Dient aussschließlich beim Import für die Referenzierung des Ausgangsdatensatzes.
+ Attribut: optional: *`docId`*  (nur Zahlen)
  + Dient ausschließlich beim Import zur Instanziierung eines bestehenden OPUS4-Dokuments.
+ Attribut: obligatorisch: *`language="[dreistelliger Sprachcode]"`*
  + Es gilt der Standard [ISO 639-2][lc-lang].
+ Attribut: obligatorisch: *`type="[ein OPUS4-Dokumenttyp]"`*
+ Attribut: optional: *`pageFirst`* (beliebiger Inhalt)
+ Attribut: optional: *`pageLast`* (beliebiger Inhalt)
+ Attribut: optional: *`pageNumber`* (beliebiger Inhalt)
+ Attribut: optional: *`edition`* (beliebiger Inhalt)
+ Attribut: optional: *`volume`* (beliebiger Inhalt)
+ Attribut: optional: *`issue`* (beliebiger Inhalt)
+ Attribut: optional: *`publisherName`* (beliebiger Inhalt)
+ Attribut: optional: *`publisherPlace`* (beliebiger Inhalt)
+ Attribut: optional: *`creatingCorporation`* (beliebiger Inhalt)
+ Attribut: optional: *`contributingCorporation`* (beliebiger Inhalt)
+ Attribut: optional: *`belongsToBibliography`* (true, false)
+ Attribut: obligatorisch: *`serverState`* (audited, published, restricted, inprogress, unpublished)
+ Kardinalität: 1

+ Beschreibung des Inhalts: Das Element OPUS-Document beinhaltet den Metadatensatz
  zu einem gesamten Dokument.   Die Attribute *`language`*, *`type`*, *`oldId`* und
  *`serverState`* sind obligatorisch.  Mit dem Attribut *`serverState`* wird festgelegt,
  welchen [Dokumentstatus]() das Dokument nach dem Import in OPUS4 hat.  Das Attribut
  *`docId`* bezieht sich auf eine OPUS4-Dokument-ID.  Es kann genutzt werden, um einen
  bereits bestehendes Dokument in OPUS4 [zu aktualisieren]().  Die Attribute *`oldId`*
  und *`docId`* werden nicht als Werte importiert und an das neu aufgebaute OPUS4-Dokument
  gehängt, sondern dienen lediglich der Referenzierung (z.B. im Import-Logfile).



#### **1.1  (Haupt)Titel**

+ Bezeichnung: **`titlesMain`**
+ Kardinalität: 1

+ Beschreibung des Inhalts: Der Titel ist der Name des Dokuments.  (Hauptsachtitel).


##### **1.1.1 (Haupt)Titel**

+ Bezeichnung: **`titleMain`**
+ Attribut: obligatorisch: *`language="[dreistelliger Sprachcode]"`*
  + Es gilt der Standard [ISO 639-2][lc-lang].
+ Kardinalität: 1..n

+ Beschreibung des Inhalts: Es ist möglich, mehrere Titel in verschiedenen Sprachen
  anzugeben, allerdings nur genau einen Titel pro Sprache.
+ Beispiel:
  {% highlight xml %}
<titlesMain>
   <titleMain language="deu">Beispieltitel deutsch</titleMain>
   <titleMain language="eng">example main title english</titleMain>
</titlesMain>
  {% endhighlight %}



#### **1.2  Weitere Titel**

+ Bezeichnung: **`titles`**
+ Kardinalität: 0..1

+ Beschreibung des Inhalts: In diesem Element können Untertitel, übergeordnete Titel 
  und übersetzte Titel des Dokuments angegeben werden.


##### **1.2.1 Weiterer Titel**

+ Bezeichnung: **`title`**
+ Attribut: obligatorisch: *`type`* (sub, parent, additional)
+ Attribut: obligatorisch: *`language="[dreistelliger Sprachcode]"`*
  + Es gilt der Standard [ISO 639-2][lc-lang].
+ Kardinalität: 1..n

+ Beschreibung des Inhalts: Es ist möglich, weitere Titel in verschiedenen Sprachen
  anzugeben, allerdings nur genau einen Titel pro Typ und Sprache.
+ Beispiel:
  {% highlight xml %}
<titles>
   <title type="sub" language="deu" >Beispieluntertitel deutsch</title>
   <title type="sub" language="eng">example subtitle english</title>
</titles>
  {% endhighlight %}



#### **1.3  Abstracts**

+ Bezeichnung: **`abstracts`**
+ Kardinalität: 0..1

+ Beschreibung des Inhalts: In diesem Element können Abstracts zum Dokument angegeben werden.


##### **1.3.1 Abstract**

+ Bezeichnung: **`abstract`**
+ Attribut: obligatorisch: *`language="[dreistelliger Sprachcode]"`*
  + Es gilt der Standard [ISO 639-2][lc-lang].
+ Kardinalität: 1..n

+ Beschreibung des Inhalts: Es ist möglich, mehrere Abstracts in verschiedenen Sprachen
  anzugeben, allerdings nur genau einen Abstract pro Sprache.
+ Beispiel:
  {% highlight xml %}
<abstracts>
   <abstract language="deu">Beispielabstract deutsch</abstract>
   <abstract language="eng">example abstract english</abstract>
</abstracts>
  {% endhighlight %}



#### **1.4  Personen**

+ Bezeichnung: **`persons`**
+ Kardinalität: 0..1

+ Beschreibung des Inhalts: Es ist möglich, mehrere Personen anzugeben. 
  Die Rollen sind wiederholbar (z.B. "author").


##### **1.4.1 Person**

+ Bezeichnung: **`person`**
+ Attribut: obligatorisch: *`role`* (advisor, author, contributor, editor, referee, translator, submitter)
+ Attribut: obligatorisch: *`firstName`* (beliebiger Inhalt)
+ Attribut: obligatorisch: *`lastName`* (beliebiger Inhalt)
+ Attribut: optional: *`academicTitle`* (beliebiger Inhalt)
+ Attribut: optional: *`email`* (beliebiger Inhalt)
+ Attribut: optional: *`allowEmailContact`* (true, false)
+ Attribut: optional: *`placeOfBirth`* (beliebiger Inhalt)
+ Attribut: optional: *`dateOfBirth`* ([ISO 8601][w3-date])

+ Kardinalität: 1..n

+ Beispiel:
  {% highlight xml %}
<persons>
   <person role="author"
           firstName="John"
           lastName="Doe"
           academicTitle="Dr."
           email="doe@example.org"
           allowsEmailContact="true"
           placeOfBirth="San Francisco"
           dateOfBirth="1968-07-24"/>
   <person role="editor"
           firstName="Jane"
           lastName="Doe"/>
</persons>
  {% endhighlight %}



#### **1.5  Schlagwörter**

+ Bezeichnung: **`keywords`**
+ Kardinalität: 0..1

+ Beschreibung des Inhalts: In diesem Element können Schlagwörter zum Dokument angegeben werden.


##### **1.5.1 Schlagwort**

+ Bezeichnung: **`keyword`**
+ Attribut: obligatorisch: *`type`* (swd, uncontrolled)
+ Attribut: obligatorisch: *`language="[dreistelliger Sprachcode]"`*
  + Es gilt der Standard [ISO 639-2][lc-lang].
+ Kardinalität: 1..n

+ Beschreibung des Inhalts: Es ist möglich, mehrere Schlagwörter anzugeben.
+ Beispiel:
  {% highlight xml %}
<keywords>
   <keyword type="swd" language="deu">Berlin</keyword>
   <keyword type="uncontrolled" language="deu">Projektgruppe 1</keyword>
   <keyword type="uncontrolled" language="eng">project group 1</keyword>
</keywords>
  {% endhighlight %}



#### **1.6  DNB-Institutionen (Verbreitende Stelle(n))**

+ Bezeichnung: **`dnbInstitutions`**
+ Kardinalität: 0..1

+ Beschreibung des Inhalts: Verbreitende Stelle der Hochschulschrift
  (muss im Administrationsbereich von OPUS4 [angelegt]() werden)


##### **1.6.1 DNB-Institution**

+ Bezeichnung: **`dnbInstitution`**
+ Attribut: obligatorisch: *`id`* (nur Zahlen)
+ Attribut: obligatorisch: *`role`* (publisher, grantor)
+ Kardinalität: 1..n

+ Beschreibung des Inhalts: Voraussetzung ist, dass die verbreitende(n) Stelle(n) 
  bereits in OPUS4 angelegt wurden (siehe oben).
+ Beispiel:
  {% highlight xml %}
<dnbInstitutions>
  <dnbInstitution id="1" role="grantor"/>
  <dnbInstitution id="4" role="publisher"/>
</dnbInstitutions>
  {% endhighlight %}

<p class="warning" markdown="1">
Es muss darauf geachtet werden, dass in diesem Element nur IDs mit Rollen eingetragen
werden, über die die entsprechende verbreitende Stelle in OPUS4 verfügt.  Wenn z.B.
eine DNB-Institution referenziert wird, für die nur `is_grantor` (und nicht `is_publisher` ) 
gesetzt ist, und im Import-XML im Attribut *`role`* der Wert "publisher" eingetragen wird, 
dann wirft der Import eine Fehlermeldung aus und der betreffende Datensatz wird nicht
importiert. 
</p>



#### **1.7  Datumsangaben**

+ Bezeichnung: **`dates`**
+ Kardinalität: 1

+ Beschreibung des Inhalts: Es ist möglich, verschiedene Datumsangaben einzutragen,
  jedoch mindestens ein Datum des Typs "completed" oder "published" .


##### **1.7.1 Datum**

+ Bezeichnung: **`date`**
+ Attribut: obligatorisch: *`type`* (completed, published, thesisAccepted)
+ Attribut: optional: *`monthDay`* ([ISO 8601][w3-date])
+ Attribut: obligatorisch: *`year`* ([ISO 8601][w3-date])
+ Kardinalität: 1..n

+ Beschreibung des Inhalts: Es kann maximal ein Datum pro Typ eingetragen werden.
  Sollte das Element **`date`** dennoch mehrfach mit dem gleichen Typ eingetragen 
  werden, dann wird nur das erste importiert und die anderen werden ignoriert.
+ Beispiel:
  {% highlight xml %}
<dates>
  <date type="completed" monthDay="--05-31" year="2011"/>
  <date type="published" year="2009"/>
  <date type="thesisAccepted" year="2010"/>
</dates>
  {% endhighlight %}



#### **1.8  Identifikatoren**

+ Bezeichnung: **`identifiers`**
+ Kardinalität: 0..1

+ Beschreibung des Inhalts: Es ist möglich, verschiedene Identifikatoren für das
  Dokument einzutragen (z.B. ISBN oder ISSN).


##### **1.8.1 Identifikator**

+ Bezeichnung: **`identifier`**
+ Attribut: obligatorisch: *`type`* (doi, handle, urn, std-doi, url, cris-link, 
  splash-url, isbn, issn, opus3-id, opac-id, uuid, serial, pmid, arxiv)
+ Kardinalität: 1..n

+ Beschreibung des Inhalts: Es ist prinzipiell möglich, mehrere Identifikatoren
  eines Typs anzugeben.
+ Beispiel:
  {% highlight xml %}
<identifiers>
  <identifier type="isbn">978-3-86680-192-9</identifier>
  <identifier type="doi">10.1000/182</identifier>
</identifiers>
  {% endhighlight %}



#### **1.9  Bemerkungen**

+ Bezeichnung: **`notes`**
+ Kardinalität: 0..1

+ Beschreibung des Inhalts: An dieser Stelle können Bemerkungen bzw.
  Notizen angegeben werden.


##### **1.9.1 Bemerkung**

+ Bezeichnung: **`note`**
+ Attribut: obligatorisch: *`visibility`* (private, public)
+ Kardinalität: 1..n

+ Beschreibung des Inhalts: Es können mehrere Bemerkungen bzw.
  Notizen angegeben werden und zwar mit der Sichtbarkeit 
  intern ("private") oder öffentlich ("public").
+ Beispiel:
  {% highlight xml %}
<notes>
   <note visibility="private">Dokument muss noch geprüft werden.</note>
   <note visibility="public">Parallel erschienen als Druckausgabe</note>
</notes>
  {% endhighlight %}



#### **1.10 Sammlungen (Collections)**

+ Bezeichnung: **`collections`**
+ Kardinalität: 0..1

+ Beschreibung des Inhalts: An dieser Stelle können Sammlungen angegeben werden.

##### **1.10.1 Sammlung**

+ Bezeichnung: **`collection`**
+ Attribut: obligatorisch: *`id`* (nur Zahlen)
+ Kardinalität: 1..n

+ Beschreibung des Inhalts: Voraussetzung ist, dass die Sammlung(en) bereits
  in OPUS4 angelegt wurden.  An dieser Stelle wird daher nur die ID eingetragen.
+ Beispiel:
  {% highlight xml %}
<collections>
   <collection id="234"/>
</collections>
  {% endhighlight %}


#### **1.11 Schriftenreihen**

+ Bezeichnung: **`series`**
+ Kardinalität: 0..1

+ Beschreibung des Inhalts: An dieser Stelle können Schriftenreihen angegeben werden.


##### **1.11.1 Schriftenreihe**

+ Bezeichnung: **`seriesItem`**
+ Attribut: obligatorisch: *`id`* (nur Zahlen)
+ Attribut: obligatorisch: *`number`* (beliebiger Inhalt)
+ Kardinalität: 1..n

+ Beschreibung des Inhalts: Voraussetzung ist, dass die Schriftenreihe(n) bereits 
  in OPUS4 angelegt wurde(n).  Das Attribut *`number`* bezieht sich auf die Bandnummer.
+ Beispiel:
  {% highlight xml %}
<series>
   <seriesItem id="2" number="2005/2006, III"/>
</series>
  {% endhighlight %}



#### **1.12 Benutzerdefinierte Felder (Enrichments)**

+ Bezeichnung: **`enrichments`**
+ Kardinalität: 0..1

+ Beschreibung des Inhalts: An dieser Stelle können benutzerdefinierte Felder angegeben werden.


##### **1.12.1 Benutzerdefiniertes Feld**

+ Bezeichnung: **`enrichment`**
+ Attribut: obligatorisch: *`key`* (die Bezeichnung)
+ Kardinalität: 1..n

+ Beschreibung des Inhalts: Voraussetzung ist, dass die benutzerdefinierten Felder 
  bereits in OPUS4 angelegt wurden.  An dieser Stelle wird daher der *`key`* und 
  der Inhalt bzw. Wert des benutzerdefinierten Feldes eingetragen.
+ Beispiel:
  {% highlight xml %}
<enrichments>
   <enrichment key="validtestkey">xyz</enrichment>
</enrichments>
  {% endhighlight %}



#### **1.13 Lizenzen**

+ Bezeichnung: **`licences`**
+ Kardinalität: 0..1

+ Beschreibung des Inhalts: An dieser Stelle können Lizenzen angegeben werden.


##### **1.13.1 Lizenz**

+ Bezeichnung: **`licence`**
+ Attribut: obligatorisch: *`id`* (nur Zahlen)
+ Kardinalität: 1..n

+ Beschreibung des Inhalts: Voraussetzung ist, dass die Lizenz bereits in OPUS4 
  angelegt wurde.  An dieser Stelle wird daher nur die ID der gewünschten Lizenz 
  eingetragen.
+ Beispiel:
  {% highlight xml %}
<licences><licence id="5"/></licences>
  {% endhighlight %}


[lc-lang]: http://www.loc.gov/standards/iso639-2/langhome.html
[w3-date]: http://www.w3.org/TR/xmlschema-2/#date

