---
title: Fork
weight: 20
---

An dieser Stelle kann **Git** und seine Möglichkeiten nicht in allen Einzelheiten erklärt werden. Dafür gibt es im
Internet eine vielzahl von Tutorial und anderen Ressourcen, einschließlich der Hilfe von GitHub selbst. Hier sollen
nur ein paar Stichpunkte zu möglichen Anwendungsfällen im Rahmen von OPUS 4 angesprochen werden.

# Fork

Auf GitHub kann man einen Fork eines Repositories anlegen. Wenn zum Beispiel Anpassungen an der OPUS 4 Applikation
vornehmen möchte kann man einen Fork von [opus4/application](https://github.com/opus4/application) anlegen und hat
dann seine eigene Kopie des Repositories.

Änderungen, die im eigenen Repository vorgenommen werden, können als Pull Request an das ursprüngliche Repository
zurückgegeben werden.

# Pull Requests

Wenn auf GitHub ein Fork eines Repositories angelegt wurde können Änderungen von dort als Pull Request an das
ursprüngliche Repository zurückgegeben werden. Genauere Informationen dazu finden sich in der Hilfe von GitHub.
Im Rahmen der OPUS 4 Entwicklung sind folgende Punkte wichtig.

* Ein Pull Request sollte sich genau auf ein Feature oder einen Bugfix beziehen. In anderen Worten die Änderungen in
einem Pull Request sollten möglichst klein sein und einen klaren Zweck haben.

* Die Sourcen sollten auf dem neuesten Stand sein, so daß der Pull Request automatisch übernommen werden kann. Das
heißt wenn sich nach dem Fork der ursprünglich Source Code verändert hat sollten diese Änderungen vor dem Erstellen
des Pull Requests übernommen werden.

* Pull Requests sollten idealerweise nur einen einzigen Commit enthalten. Bei größeren Änderungen können mehrere
Commits Sinn machen. Jeder Commit sollte eine in sich abgeschlossene Änderung enthalten. Während der Entwicklung ist
es sinnvoll häufig und früh Commits durchzuführen. Später sollten diese Commits aber vor einem Pull Request bereinigt
werden.

Im folgenden Beispiel gibt es drei Commits:

{% highlight text %}
Commit 1 - Neue Funktion
Commit 2 - Bugfix in der neuen Funktion
Commit 3 - Zusätzliche Dokumentation im Code
{% endhighlight %}

Zuerst wurde einen neue Funktion eingebaut. Dann wurde ein Fehler gefunden und korrigiert. Zum Schluß wurde noch die
Dokumentation im Code ergänzt. Bevor ein Pull Request angelegt wird sollten diese drei Commits zusammengefasst werden,
so daß nur noch ein Commit für die neue Funktion übrig bleibt. Git bietet Funktionen dafür.

TODO git merging commits

