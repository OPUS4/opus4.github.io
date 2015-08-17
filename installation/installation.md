---
title: Mit Git
---

# Installation mit Git

Die Installation mit Git wird empfohlen, da auf diese Weise Bug Fixes und andere Updates schneller und leichter in die
Instanz übernommen werden können.

## Git clone

Um mit Git eine neue OPUS 4 Instanz einzurichten muss zuerst eine lokale Kopie angelegt werden.

{% highlight bash %}
$ git clone https://github.com/opus4/application opus4
{% endhighlight %}

## Abhängigkeiten installieren

Die Abhängigkeiten werden mit Composer installiert. Dazu muss man in das Verzeichnis wechseln und `composer install`
aufrufen.

{% highlight bash %}
$ cd opus4
$ composer install
{% endhighlight %}

Nun werden automatisch die notwendigen Pakete heruntergeladen und im `vendor` Verzeichnis der Instanz installiert.

## Einrichten

Zum Einrichten der Instanz kann jetzt das Setup Skript aufgerufen werden.
