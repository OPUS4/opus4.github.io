---
title: Datenbank
weight: 40
---

# MySQL Datenbank

## Installation

Unter Ubuntu kann MySQL mit folgendem Kommando installiert werden. Für OPUS wird mindestens die Version 5.1
vorausgesetzt.

{% highlight bash %}
sudo apt-get install mysql-server
{% endhighlight %}


## Datenbank für OPUS 4 erstellen

OPUS 4 verwendet MySQL (TODO Version). Um die Datenbank für OPUS 4 zu erstellen logged man sich als MySQL Root Nutzer
ein.

{% highlight sql %}
create database opusdb default character set = utf8 default collate = utf8_general_ci;
{% endhighlight %}

Der *opus4admin* Nutzer wird verwendet um die Datenbank zu initialisieren.

{% highlight sql %}
create user 'opus4admin'@'localhost' identified by '<passwd>';
grant all privileges on opusdb.* to 'opus4admin'@'localhost';
{% endhighlight %}

Die Webapplikation verwendet den normalen *opus4* Nutzer, um lesend und schreibend auf die Datenbank zuzugreifen.

{% highlight sql %}
create user 'opus4'@'localhost' identified by '<passwd>';
grant select,insert,update,delete on opusdb.* to 'opus4'@'localhost';
{% endhighlight %}

