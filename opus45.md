---
title: OPUS 4.5
weight: 20
---

# OPUS 4.5

<p class="info">
OPUS 4.5 sollte eigentlich die Version 4.4.6 bekommen und nur kleinere Probleme beheben. Durch die Migration zu GitHub
und die Einführung von Composer ergeben sich aber große Veränderungen bei der Installation und zukünftigen Updates. Die
größere Versionsnummer soll deutlich ausdrücken wie wichtig dieser Release ist.
</p>

## Was ist neu in OPUS 4.5

Version 4.5 enthält einige kleinere Bugfixes unter anderem um Anforderungen des DINI-Zertifikats zu erfüllen, sowie
kleinere Verbesserungen in der Administration. Die Liste der Tickets wird in der CHANGES Datei für den Release zu
finden sein.

Die wichtigsten Änderungen haben damit zu tun wie die OPUS 4 Entwicklung abläuft, wie Installationen und Updates in
Zukunft funktionieren. Es wird weiterhin einen Tarball geben, aber die empfohlene Methode der Installation ändert sich
mit Version 4.5.

### Entwicklung

Durch die Migration zu [GitHub](https://github.com/opus4) ist die Entwicklung von OPUS 4 noch offener geworden.
Als Open Source Projekt war der Source Code von OPUS 4 immer frei zugänglich in
den [Subversion](https://svn.zib.de/opus4dev)
Repositorien am [ZIB](http://www.zib.de). Diese bleiben auch weiterhin zugänglich, werden aber nicht mehr weiter
gepflegt. Die Entwicklung findet jetzt auf GitHub statt.

Auf GitHub stehen mehr Werkzeuge zur Verfügung, die unter anderem die Zusammenarbeit mit externen Entwicklern und
anderen Institutionen, die sich an der Entwicklung beteiligen wollen, wesentlich vereinfachen.

Für OPUS 4.5 wurde bereits zwei Projekte mit externen Entwicklern auf GitHub durchgeführt. Zum einen eine Verbesserung
bei der Navigation von Suchergebnissen, die durch das [BSZ](https://www.bsz-bw.de) finanziert wurde, zum anderen der
Umstieg von Solr 1.4.1 auf Solr 5.2.1 den der [KOBV](https://www.kobv.de) in Auftrag gegeben hat.

### Installation und Updates

Mit Version 4.5 ändert sich die empfohlene Methode zur Installation von OPUS. Statt des Tarballs wird empfohlen mit
[Git](https://git-scm.com/) einen Clone vom OPUS 4 Repository anzulegen. Die Clone Operation ersetzt im Prinzip das
Herunterladen und Auspacken des Tarballs. Eine detailierte Beschreibung findet sich in der
[Installationanleitung]({{ site.baseurl }}/installation/installation.html). Was ist der Vorteil?

Ein Git Clone ist selbst ein Git Repository, das weiß woher die Dateien gekommen sind. Wenn es Änderungen im
ursprünglichen
Repository (origin) gibt können diese mit einfachen Kommandos übernommen werden. Das heißt Bugfixes und Verbesserungen
können sofort nach ihrer Fertigstellung in lokale Instanzen übernommen werden. Im Idealfall durch ein einfaches kurzes
Kommando. Es muss nicht mehr auf den nächsten Release mit einem neuen Tarball gewartet werden.

Vorerst wird es weiterhin den Tarball geben. Er wird aber höchstens ein oder zweimal im Jahr auf den neuesten Stand
gebracht werden, insbesondere z.B. dann, wenn sich die Schema für die Datenbank oder den Suchindex verändern.

OPUS 4 Instanzen sind in der Regel keine Software die einfach installiert und dann konfiguriert wird. Die meisten
Instanzen werden an die Bedürfnisse der jeweiligen Institution angepasst und dabei werden Dateien von OPUS verändert.
Das heißt im Prinzip wird ein Branch angelegt, eine Version von OPUS 4 die nicht mehr vollständig mit dem Original
übereinstimmt. Das macht Updates schwierig. Für solche Situationen ist Git bestens geeignet. Sollte es Konflikte
zwischen lokalen Änderungen und einer neuen Version geben werden diese von Git erkannt und können mit geeigneten
Werkzeugen aufgelöst werden.

Wir werden versuchen die notwendigen Schritte hier auf diesen Seiten ausführlich zu erläutern, um den Einstieg so
einfach wie möglich zu machen.

<p class="note">
OPUS 4.5 wird voraussichtlich ein Pflichtupdate werden. Das heißt es wird keine Updatemöglichkeit von vorhergehenden
Version, wie z.B. 4.4.2,  zu Versionen nach 4.5 geben. Um 4.6 zu installieren, muss zuerst zu 4.5 gewechselt werden.
</p>

### Composer

In Zunkunft wird [Composer](https://getcomposer.org) eingesetzt werden, um die Abhängigkeiten von OPUS 4 zu verwalten.
Notwendige Softwarebibliotheken wie z.B. das ZendFramework werden in einer Konfigurationsdatei aufgelistet und können
dann durch Composer installiert und aktualisiert werden. Dadurch vereinfachen sich die Installations- und Updateskripte.
Das OPUS 4 Framework, die Verbindung zur Datenbank und zum Suchindex, ist mit Version 4.5 ein eigenständiges Composer
Paket geworden, so daß es ebenfalls als Abhängigkeit von Composer heruntergeladen und aktualisiert werden kann. Die
Pakete werden auf [Packagist.org](https://packagist.org) gehostet. Die OPUS Pakete finden sich dort unter
[opus4-repo](https://packagist.org/packages/opus4-repo).

### Migration

Der Code für die Migration von OPUS 3 wurde aus der normalen OPUS 4 Release entfernt und in ein eigenes
Repository [migration](https://github.com/opus4/migration) auf GitHub verschoben. Die Migration wird in Zukunft eine
optionale Komponente sein, die bei Bedarf installiert werden kann.

## Zusammenfassung

Mit OPUS 4.5 wird sich die Entwicklung wesentlich verändern, sie  wird vorallem effizienter werden. Weniger Zeit wird
in Updateskripte fließen, mehr in neue Features und andere Verbesserungen. Für Institutionen deren Instanzen gehostet
werden wird sich nichts ändern. Die Veränderungen werden im Hosting passieren.

