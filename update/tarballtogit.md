---
title: Umstieg auf Git
---

# Umstieg auf Git

Mit Git ist es wesentlich einfacher wichtige Bugfixes und neue Funktionen in die eigene OPUS 4 Instanz zu übernehmen.
Wie kann ein existierende Instanz, die mit einem Tarball installiert wurde auf Git umgestellt werden.

<p class="note" >
Die Dokumentation auf dieser Seite zur Umstellung einer existierenden OPUS 4 Instanz auf Git ist noch nicht fertig.
Wenn sie Vorschläge haben wie der Umstieg vereinfacht werden kann wenden Sie sich bitte an die Entwickler (TODO Link).
<br /><br />
Das folgende sind die aktuellen Ideen zum Umstieg. Die Anleitungen werden überarbeitet, wenn OPUS 4.5 fertig ist und
ein Umstieg an echten Instanzen getestet werden konnte.
</p>

Vermutlich wird es für existierende Instanzen am einfachsten sein noch einmal den Tarball zu verwenden, um auf die
Version 4.5 zu wechseln und diese dann mit Git zu verknüpfen.

# Vorbereitungen

Die lokale Instanz kann in ein Git Repository umgewandelt werden. Anschließend kann das GitHub Repository als Remote
hinzugefügt werden.

{% highlight bash %}
$ git init
$ git remote add origin https://github.com/opus4/application
$ git checkout -b opus-master
$ git pull origin master
{% endhighlight %}

An dieser Stelle kommt es danne evtl. zu Konflikten zwischen lokalen Dateien und der Version auf GitHub. Diese müssen
aufgelöst werden. Dazu kann `git mergetool` verwendet werden. Welches Tool dabei wirklich zum Einsatz kommt hängt davon
ab was auf dem System installiert ist. Das Kommando wird eine Liste mit Möglichkeiten ausgeben.

{% highlight bash %}
$ git mergetool
{% endhighlight %}

<p class="warning" markdown="1">
Der **master** Branch von `opus4/application` ist noch nicht bereit für die Installation einer OPUS 4 Instanz. Die
Entwicklung findet momemtan auf dem **solrupdate** Branch statt.
</p>
