---
title: Mit Git
weight: 10
---

# Installation mit Git

<p class="note">
Die Anleitung bezieht sich auf die aktuelle Entwicklungsversion. Für den Release von 4.5 wird es noch kleine
Änderungen geben, da dann die zu verwendende Version im Master *branch* liegt bzw. durch Tags markiert ist.
</p>

Die Installation mit Git wird empfohlen, da auf diese Weise Bug Fixes und andere Updates schneller und leichter in die
Instanz übernommen werden können.

## Git clone

Um mit Git eine neue OPUS 4 Instanz einzurichten muss zuerst eine lokale Kopie angelegt werden.

{% highlight bash %}
$ git clone https://github.com/opus4/application opus4
$ cd opus4
{% endhighlight %}

Das lokale Repository ist eine vollständige Kopie. Das heißt die bisherigen Änderungen und Branches sind ebenfalls
lokal verfügbar.

Die aktuelle Entwicklungsversion befindet sich momentan nicht im Branch *solrupdate* und nicht im *master*. Zu diesem
Branch kann man mit folgendem Kommando wechseln.

{% highlight bash %}
$ git checkout solrupdate
{% endhighlight %}

## Composer installieren

Für die weitere Installation wird [Composer](https://getcomposer.org) benötigt. Falls Composer bereits installiert ist,
kann dieser Schritt übersprungen werden. Andernfalls kann folgendes Skript verwendet werden.

**TODO** still changing

{% highlight bash %}
$ bin/install-composer.sh .
{% endhighlight %}

Dadurch wird `composer.phar` in das aktuelle Verzeichnis (`opus4`) installiert. Anschließend werden automatisch die
notwendigen Abhängigkeiten heruntergeladen und im ```vendor``` Verzeichnis abgelegt.

## Abhängigkeiten installieren

Die Abhängigkeiten werden mit Composer installiert. Dazu muss man in das Verzeichnis wechseln und `composer install`
aufrufen. Dieser Schritt ist nur notwendig wenn Composer nicht mit Hilfe des Installationsskriptes im ```bin```
Verzeichnis installiert wurde (siehe oben).

{% highlight bash %}
$ composer install
bzw.
$ php composer.phar install
{% endhighlight %}

Nun werden automatisch die notwendigen Pakete heruntergeladen und im `vendor` Verzeichnis der Instanz installiert.

### Datenbank Schema verlinken

Momentan ist es noch notwendig das Datenbank Schema, das Teil des OPUS 4 Frameworks ist, manuell zu verlinken.
Ausgehend vom Basisverzeichnis der OPUS 4 Instanz kann man das mit folgenden Kommandos machen.

{% highlight bash %}
$ cd db
$ ln -sv ../vendor/opus4-repo/framework/db/schema schema
{% endhighlight %}

## Einrichten

Zum Einrichten der Instanz kann jetzt das Setup Skript aufgerufen werden. <span style="color: red">Das Skript ist noch
noch an 4.5 angepasst. Daher muss OPUS 4 momentan manuell angerichtet werden.</span>

[Manuelles Einrichten von OPUS 4]({{ site.baseurl }}/installation/setup.html)


