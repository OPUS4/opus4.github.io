---
title: Roadmap
weight: 10
---

# Roadmap

<p class="info">
GitHub bietet die Möglichkeit Milestones für Projekte zu verwalten. Wir werden in Zukunft dazu übergehen die geplanten,
großen Punkte der Entwicklung dort zu erfassen. Das ist aber noch nicht passiert. Die eigentliche Ticket-Verwaltung
findet vorerst weiterhin in einem JIRA-System beim KOBV statt.
</p>

## OPUS 4.5

Geplant für **September 2015**

Der nächste Release wird OPUS 4.5. Ursprünglich war dieser Release als 4.4.6 geplant, aber es haben sich so viele
Änderungen bei der Installation und für zukunftige Updates ergeben, daß es Sinn gemacht hat die Versionsnummer zu
ändern.

  * [Was ist neu in OPUS 4.5?]({{ site.baseurl }}/opus45.html)

Momentan sind wir dabei das Update von Solr 1.4.1 auf Solr 5.2.1 zu testen und arbeiten noch an den Installations-
und Updateskripten. Bis zum Release wird auch noch die Online-Dokumentation weiter ausgebaut.

## OPUS 4.6

Geplant für **Dezember 2015**

Nachdem Umstieg auf Git, Composer und ein Aufräumen von OPUS in 4.5 können wir uns hoffentlich wieder voll auf neue
Features für OPUS 4.6 konzentrieren. Geplant sind unter anderem folgende Punkte, die ursprünglich für 4.5 vorgesehen
waren.

* Verbessertes Personenmanagement
  * Suche nach Autoren ID
  * Publikationslisten basierend auf Autoren ID
  * Deduplizierung von vorhandenen Autoren
* Vereinfachte Sortierung von Schriftenreihen
* Bugfixes

Insbesondere die Deduplizierung der vorhanden Autoren bzw. Personen ist komplex. Sie ist notwendig, um in existierenden
Instanzen zu ermitteln welche Autoren für die einzelnen Dokumente wirklich identisch sind. Im bisherigen Datenmodell
von OPUS 4 wird nicht erfasst, ob der *Thomas Müller* für ein Dokument die selbe Person ist wie der *Thomas Müller* für
ein anderes Dokument.
