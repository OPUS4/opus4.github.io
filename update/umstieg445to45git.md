---
title: Manuell 4.4.5 to 4.5
---

<p class="note">
Version 4.5 wurde noch nicht veröffentlicht. Diese Anleitung hier dient dazu OPUS 4 Instanzen der Version 4.4.5 manuell
auf eine Instanz umzustellen, die vom Master Branch von GitHub aufgesetzt wurde. Dieser Branch wird sich bis zum Release
von 4.5 weiterentwicklen und dann bis zur nächsten Version (4.5.1) eingefroren.
</p>

# Manuelles Update von 4.4.5 auf 4.5 mit Git

Der OPUS 4.5 Release wird am Anfang nur durch ein Tagging auf GitHub durchgeführt werden. Der entsprechende Tarball wird
später nachgereicht werden. Um die neue Version vorher nutzen zu können, kann das Update manuell durchgeführt und dabei
gleich auf Git umgestiegen werden.

OPUS 4.4.5 und 4.5 sind weitestgehend kompatibel, was das manuelle Update vereinfacht. Die Dokumententypen haben sich
nicht geändert und das Datenbankschema ist das gleiche.

Für einen manuellen Umstieg empfiehlt es sich eine neue Instanz mit Git aufzusetzen und dann die lokalen Anpassungen aus
der Verzeichnissen der 4.4.5 Installation in die neue Instanz zu übertragen. In den meisten Fällen sollte dies nicht
komplizierter sein, als die üblichen Nacharbeiten bei einem OPUS 4 Update.

Die Anleitung für die [Installation]({{ site.baseurl }}/installation/installation.html) hilft dabei die neue Instanz
mit Git aufzusetzen. Der Setup Prozess ist dann ein anderer. Es wird davon ausgegangen, daß bereits eine Datenbank und
ein Solr-Core existiert.

<p class="warning">
Zum Testen empfiehlt es sich die Datenbank zu duplizieren und einen neuen Solr-Core anzulegen, um die produktive Instanz
nicht zu gefährden.
</p>

Das folgende sind Hinweise zu den wichtigsten Dateien und Verzeichnisse, die von der alten Instanz auf die Neue
übertragen werden müssen. In den Beispielen wird angenommen, daß die alte OPUS 4.4.5 Instanz im Verzeichnis
```opus445``` installiert ist und die neue in ```opus45```.

## Anpassungen übertragen

Um zu ermitteln welche Dateien in der alten Instanz angepasst wurden kann den OPUS 4.4.5 Tarball in ein anderes
Verzeichnis entpacken (opus445-ref) und dann mit dem ```diff``` Kommando einen Vergleich durchführen.

{% highlight bash %}
$ diff -rq opus445-ref opus445
{% endhighlight %}

Es macht Sinn dabei die Workspace Verzeichnisse zu ignorieren.

{% highlight bash %}
$ diff -rq --exclude=workspace opus445-ref opus445
{% endhighlight %}

### Dokumententypen

Die Dokumententypen haben sich von 4.4.5 auf 4.5 nicht verändert. Die Dateien der neuen Instanz können einfach durch die
alten Dateien ersetzt werden. Die Dateien liegen in ```application/configs/doctypes```.

Um das Übertragen zu vereinfachen kann ein Werkzeug wie ```meld``` eingesetzt werden. ***Meld*** ist ein grafisches
Werkzeug um Dateien oder Verzeichnisse miteinander zu synchronisieren. Zum Beispiel lassen sich so die Dateien für
die Dokumententypen vergleichen und abgleichen.

{% highlight bash %}
$ meld opus445/opus4/application/configs/doctypes opus45/application/configs/doctypes
{% endhighlight %}

Es ist auch für das Abgleichen der Konfigurationsdateien nützlich.

{% highlight bash %}
meld config.ini.template config.ini
{% endhighlight %}

***Meld*** ist nur ein mögliches Werkzeug von vielen für den Abgleich von Unterschieden zwischen Dateien.

### Templates für Dokumententypen

Wie bei den Dokumententypen auch können die neuen Dateien einfach durch die alten ersetzt werden. Die Dateien liegen in
```application/configs/doctypes_templates```.

### Konfiguration

Die Konfigurationsdatei, ```config.ini```, kann komplett übernommen werden, sollte aber mit der neuen Templatedatei,
 ```config.ini.template```, abgeglichen werden.

### Übersetzungen

Die Dateien aus den ```language_custom``` Verzeichnissen können einfach in die neue Instanz kopiert werden.

### Layout

Viele Instanzen verwenden ein separates Verzeichnis für das eigenen Layout. Das war in der Vergangenheit die Empfehlung
der Anleitung für OPUS 4. Mit Git macht es mehr Sinn das eigentliche ```opus4``` Layout anzupassen. Die Änderungen an
den Layoutdateien sollten also in das Defaultlayout der neuen Instanz übertragen werden. Wenn dann später in der
Entwicklung Änderungen an den Layoutdateien vorgenommen werden, können diese automatisch übernommen werden bzw.
Konflikte können mit Git und den üblichen Werkzeugen aufgelöst werdne. Für die meisten Updates wird es nicht notwendig
sein manuell einzugreifen.

## Weitere Hinweise

OPUS 4.5 befindet sich noch in der Entwicklung und die Anleitungen für die Arbeit mit Git werden noch verfeinert.

Wenn man eine funktionierendes Repository mit Git aufgesetzt hat macht es Sinn die lokalen Anpassungen mit in die lokale
Git Versionierung aufzunehmen. Zum einen lassen sich dann mit *clone* Kopien der angepassten Instanz anlegen, zum
anderen kann Git dann besser mit Konflikten zwischen lokalen und GitHub Dateien umgehen. Unter Umständen macht es lokal
Sinn die ```.gitignore``` Dateien anzupassen, um Dateien zu versionieren, bei der Entwicklung nicht berücksichtigt
werden sollten.

Beim Erstellen des Tarball wurden einige Dateien und Verzeichnisse gefiltert. Wenn OPUS 4 direkt aus dem Git Repository
bezogen wird, findet diese Filterung nicht statt und es tauchen lokal z.B. auch einige Dokumententypen auf, die sonst
nur für Tests während der Entwicklung gedacht sind. Diese können lokal gelöscht werden. Langfristig wird nach Wegen
gesucht diese Dateien auszulagern, so daß mit Git installierte Instanzen möglichst wenig nachbearbeitet werden müssen.



