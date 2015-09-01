---
title: Mit Git
---

# Updates mit Git

In den meisten Fällen ist es sinnvoll Updates und andere Änderungen zuerst in einer Testinstanz zu prüfen, bevor die
Produktivinstanz aktualisiert wird. Mit Git gibt es dafür eine Reihe von Möglichkeiten.

Nehmen wir an eine OPUS 4 Instanz wurde mit Git installiert und eingerichtet. Diese Instanz ist im produktiven Einsatz.
Im folgenden wird sie **Prod** genannt.

Es wird angenommen das **Prod** im Verzeichnis `/var/local/opus4/opus4-prod` installiert wurde.

## Testinstanz anlegen

Damit Änderungen in **Prod** nicht sofort Live für alle Nutzer sichtbar sind, insbesondere, wenn etwas schief geht oder
länger dauert, sollte man vorher alles in einer Testinstanz prüfen. Dazu kann ein Clone von **Prod** angelegt werden.

{% highlight bash %}
$ cd /var/local/opus4
$ git clone opus4-prod opus4-test
{% endhighlight %}

Durch dieses Kommando wird das gesamte Git Repository kopiert. Dateien, die nicht unter Versionskontrolle sind, werden
nicht übertragen. Das könnten z.B. lokale Konfigurationsdateien wie `config.ini` sein.

<p class="warning">Lokale Konfigurationsdateien können natürlich auch mit Git versioniert werden. Man muss dann aber
unbedingt aufpassen, daß später bei einem *Push* diese Dateien nicht letztendlich mit auf GitHub landen, insbesondere
wenn sie Passwörter enthalten sollten. Das betrifft aber eigentlich nur Instanzen, die sich an der Entwicklung von
OPUS 4 beteiligen wollen und daher auch Dateien zurück zu GitHub übertragen.</p>

Die Testinstanz kann jetzt mit Datenbank, Suchindex und URL eingerichtet werden. Ob dabei die Informationen der **Prod**
Instanz verwendet werden oder nicht hängt von verschiedenen Faktoren ab. Es kann nützlich sein, die echten Daten in der
Testinstanz zu sehen, aber dann muss aufgepasst werden, daß diese Daten nicht versehentlich verändert werden.

Das neue Repository merkt sich, wo die Dateien her gekommen sind.

{% highlight bash %}
$ git remote -v
{% endhighlight %}

In unserm Beispiel würde die Ausgabe so aussehen.

{% highlight bash %}
origin	/var/local/opus4/opus4-prod (fetch)
origin	/var/local/opus4/opus4-prod (push)
{% endhighlight %}

## Dateien ändern/hinzufügen

In der Instanz **Test** können nur Änderungen an Dateien vorgenommen werden, z.B. am Layout oder den Dokumenttypen. Mit
`git status` bekommt man angezeigt welche Dateien lokal verändert wurden. Am Anfang sollte die Ausgabe so aussehen.

{% highlight bash %}
On branch master
Your branch is up-to-date with 'origin/master'.

nothing to commit, working directory clean
{% endhighlight %}

Zur Zeit könnte der verwendete Branch evtl. **solrupdate** anstelle von **master** sein.

Als lokale Änderung könnte zum Beispiel eine Übersetzung angepasst werden. **TODO** Details

Mit `status` wird diese neue Datei aufgelistet.

{% highlight bash %}
$ git status
{% endhighlight %}

Mit dem `add` Kommando kann die Datei zum nächsten Commit hinzugefügt werden.

{% highlight bash %}
$ git add <Datei|Verzeichnis>
{% endhighlight %}

Mit `commit` wird die neue Datei dann in die Versionskontrolle aufgenommen.

{% highlight bash %}
$ git commit -m "Übersetzung für Institut angepasst."
{% endhighlight %}

Mit `status` kann der aktuelle Zustand des Repositories für die **Test** Instanz wieder angezeigt werdne.

{% highlight bash %}
$ git status
{% endhighlight %}

Die **Test** Instanz ist jetzt einen Commit weiter als die Produktivinstanz.

{% highlight bash %}
On branch solrupdate
Your branch is ahead of 'origin/solrupdate' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working directory clean
{% endhighlight %}

## Änderungen übertragen

Wenn die Änderungen in der **Test** Instanz geprüft wurden können sie in die Produktivinstanz übertragen werden. Dafür
wird in Git normalerweise das `push` Kommando verwendet. In unserem Fall ist das **Prod** Repository aber nicht **bare**
(TODO verlink Erläuterungen). Das heißt ein Push wird von Git normalerweise abgelehnt. Eine Installationsvariante mit
**bare** Repository wird später besprochen.

Um die Änderungen jetzt von der **Test** in die **Prod** Instanz übertragen zu können fügen wir die Testinstanz als
Remote zu Produktivinstanz hinzu.

{% highlight bash %}
$ cd /var/local/opus4/opus45-prod
$ git remote add test ../opus45-test
{% endhighlight %}

Nun können die Änderungen mit `pull` anstelle von `push` übertragen werden. Im Verzeichnis der **Prod** Instanz wird
folgendes Kommando ausgeführt.

{% highlight bash %}
$ git pull test master
{% endhighlight %}

Dadurch wird die gerade in der Testinstanz angelegte Datei in die Produktivinstanz übertragen.


