---
title: Voraussetzungen
weight: 5
---

# Voraussetzungen

Vor der Installation und den Betrieb von OPUS 4 muss das System einige Grundvoraussetzungen erfüllen.

* [Apache 2]({{ site.baseurl }}/installation/apache.html)
* MySQL (mindestens Version 5.1)
* PHP 5.5 (oder neuer)
* Git

OPUS 4 funktioniert im allgemeinen auch mit älteren PHP Versionen ab 5.3 (mit "Multibyte-String"-Unterstützung). Es
wird aber empfohlen eine möglichst aktuelle Version von PHP zu verwenden, die immer noch gewartet und mit
Sicherheitsupdates versorgt wird.

## Zusätzliche Komponenten

* [Solr](http://lucene.apache.org/solr) 5.2.1
* Java Runtime

## PHP Pakete installieren

In Ubuntu können die notwendige PHP Pakete mit folgendem Kommando installiert werden.

{% highlight bash %}
sudo apt-get install
{% endhighlight %}

Das Kommando muss mit folgenden Paketen aufgerufen werden.

php5 |
php5-cli |
php5-common |
php5-curl |
php5-dev |
php5-gd |
php5-mcrypt |
php5-mysql |
php5-uuid |
php5-xsl |
php-log |
libapache2-mod-php5 |

{% highlight bash %}
$ sudo apt-get install php5
{% endhighlight %}

<p class="warning" markdown="1">
Damit OPUS 4 fehlerfrei funktioniert, muss der Parameter
[allow_url_fopen](http://php.net/manual/en/filesystem.configuration.php) in der
[php.ini](http://php.net/manual/en/configuration.file.php) auf "1" gesetzt, also eingeschaltet sein. Das
ist in aktuellen PHP Versionen normalerweise der Fall.
</p>

## Git installieren

{% highlight bash %}
$ sudo apt-get install git
{% endhighlight %}
