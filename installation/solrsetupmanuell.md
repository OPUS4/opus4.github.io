---
title: Solr manuell einrichten
group: navigation
---

# Solr für OPUS 4 manuell einrichten

Die folgende Anleitung beschreibt wie Solr 4.10.4 manuell für OPUS 4 eingerichtet werden kann. Als System wird
Ubuntu 14.0.4 verwendet. Die Schritte sollten für andere Linux Distributionen ähnlich sein.


## Solr 4.9.1 herunterladen

{% highlight bash %}
solr-4.10.4.tgz
{% endhighlight %}

 Auspacken

{% highlight bash %}
tar xvfz solr-4.10.4.tgz
{% endhighlight %}


## Konfigurationsdateien holen

Die Konfigurations Dateien liegen auf GitHub im Repository `opus4/search`. Sie können mit git clone heruntergeladen
werden.

{% highlight bash %}
git clone https://github.com/opus4/search
{% endhighlight %}

Die Konfigurationsdateien müssen im Augenblick unter Umständen für die Solr Version angepasst werden. Für Solr 4.9.1
muss luceneVersionMatch hinzugefügt werden (Siehe unten). Bei Solr 4.10.4 hat sich noch mehr geändert. (TODO neue
Konfigurationsdateien anlegen)

## Verzeichnisse vorbereiten

{% highlight bash %}
cd solr-4.10.4

cp -R example opus4

cd opus4/multicore

// Beispielverzeichnisse entfernen
rm -rf core0 core1 exampledocs
{% endhighlight %}

## Konfigurationsdateien ablegen

Entweder in

multicore/opus/conf

Dabei ist "opus" der Name des Cores. Für jeden Core muss dann ein solches Verzeichnis angelegt werden.

{% highlight xml %}
...
<core name="opus" instanceDir="opus" config="solrconfig.xml" schema="schema.xml" />
...
{% endhighlight %}

### Konfigurationsdateien für mehrere Cores verwenden

Alternativ, wenn man mehrere Cores mit der selben Konfiguration betreiben möchte kann man die Dateien als configSet
ablegen.

{% highlight bash %}

mkdir -p configsets/opus/conf

{% endhighlight %}

Die beiden Konfigurationdateien `schema.xml` und `solrconfig.xml` in dieses neue Verzeichnis kopieren.

In der Datei `solr.xml` den Core wie folgt eintragen.

{% highlight xml %}
...
<core name="opus" instanceDir="opus" configSet="opus4" />
...
{% endhighlight %}

Die Verzeichnissstruktur innerhalb von `multicore` ist dann wie folgt:

{% highlight bash %}
multicore/
|-solr.xml
|-configsets/
  |-opus4/
    |- conf/
       |- schema.xml
       |- solrconfig.xml
{% endhighlight %}

## solrconfig.xml anpassen

In der Datei `solrconfig.xml` muss zur Zeit (für Solr 4.9.1) noch folgender Eintrag hinzugefügt werden:

{% highlight xml %}

<luceneMatchVersion>4.9.1</luceneMatchVersion>

{% endhighlight %}

Das kann gleich am Anfang innerhalb von `<config>` gemacht werden.



## Port ändern

Normalerweise läuft Solr auf Port 8983. Wenn auf einem System mehrere Solr Instanzen laufen sollen ist es notwendig den
Port zu ändern. Dafür muss man die Datei `etc/jetty.xml` editieren. Dort findet sich eine Connector Konfiguration wie
folgende in der der Port geändert werden kann.

{% highlight xml %}
<Call name="addConnector">
    <Arg>
        <New class="org.eclipse.jetty.server.bio.SocketConnector">
            <Set name="host"><SystemProperty name="jetty.host" /></Set>
            <Set name="port"><SystemProperty name="jetty.port" default="8985"/></Set>
            <Set name="maxIdleTime">50000</Set>
            <Set name="lowResourceMaxIdleTime">1500</Set>
            <Set name="statsOn">false</Set>
        </New>
    </Arg>
</Call>
{% endhighlight %}

## Solr starten

Da wir die neue Instanz im Verzeichnis `multicore` konfiguriert haben muss sie mit folgendem Kommando gestartet werden.

{% highlight bash %}
java -Dsolr.solr.home=multicore -jar start.jar
{% endhighlight %}

## Extraktion von Volltexten einrichten

## Solr in separaten User Account installieren

## Startup Skript für Solr einrichten

