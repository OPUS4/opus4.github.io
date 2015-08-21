---
title: Update
weight: 70
---

Mit dem Umstieg auf Git und Composer ändert sich das Updateverfahren.

## Versehentliche Updates verhindern

Mit `git pull` kann man die eigene Instanz auf den neuesten Stand bringen.

{% highlight bash %}
$ git remote -v
origin	https://github.com/OPUS4/application.git (fetch)
origin	https://github.com/OPUS4/application.git (push)
{% endhighlight %}

Damit das nicht ausversehen passiert kann man die Verbindung zum GitHub Repository kappen indem man den Remote Eintrag
dafür entfernt.

{% highlight bash %}
$ git remote rm origin
{% endhighlight %}

Das Kommando `git remote -v` sollte jetzt nichts mehr ausgeben. Um dann später ein Pull durchführen zu können kann die
 Remote Adresse wieder hinzugefügt werden.

 {% highlight bash %}
 $ git remote add origin https://github.com/OPUS4/application.git
 {% endhighlight %}
