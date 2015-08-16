---
title: Installation
group: navigation
weight: 40
---

# Installation

Die Installationsanleitung geht von einem Ubuntu 14 LTS System aus. Diese Distribution wird zur Zeit in der Entwicklung
und im Hosting beim KOBV verwendet.

Es wird davon ausgegangen, daß Git installiert ist und grundlegende Kenntnisse vorhanden sind.

# Installation mit Git

Um mit Git eine neue OPUS 4 Instanz einzurichten muss zuerst eine lokale Kopie angelegt werden.

{% highlight bash %}
$ git clone https://github.com/opus4/application opus4
{% endhighlight %}

# Abhängigkeiten installieren

{% highlight bash %}
$ cd opus4
$ composer install
{% endhighlight %}

# Einrichten

Zum Einrichten der Instanz kann jetzt das Setup Skript aufgerufen werden.
