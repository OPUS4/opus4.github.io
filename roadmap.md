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

Momentan sind wir dabei das Update von Solr 1.4.1 auf Solr 5.3.1 zu testen und noch einige Bugs zu beheben.

  * [Was ist neu in OPUS 4.5?]({{ site.baseurl }}/opus45.html)

Wenn OPUS 4.5 stabil läuft wird auf GitHub ein Tag angelegt werden und die weitere Entwicklung wird auf einem anderen
Branch stattfinden. Mit den Anleitungen, die hier zu finden sind wird es dann möglich sein OPUS direkt mit Git manuell
einzurichten. Das wird der offizielle Release sein.

Anschließend werden an den Installations- und Updateskripten weiterarbeiten, die es ermöglichen eine alte OPUS Instanz
auf den Stand von 4.5 zu bringen. Außerdem wird die Online-Dokumentation weiter ausgebaut werden.

Für alte Instanzen in der Version 4.4.5 wird es eine einfache Anleitung geben, um manuell auf eine mit Git installierte
Version 4.5 von OPUS zu wechseln. Die Installation mit Git wird aufgrund der besseren Updatemöglichkeiten für die
Zukunft empfohlen, um Zeit und Ressourcen bei der Entwicklung und beim Betrieb von OPUS 4 Repositorien zu sparen.

## Weitere Entwicklung

Nach dem Release von 4.5 wird die Entwicklung in verschiedenen Branches auf GitHub fortgesetzt werden. Diese Branches
werden in erste Linie **MASTER**, **EARLY** und konkrete Versionsnummern wie **4.6** sein.

Der **MASTER** Branch wird in der Regel auf dem Stand von festgelegten Versionsnummern bleiben bis die nächste Version
freigegeben wird, beginnend mit Version 4.5. Kritische Bugfixes werden in diesen Branch bei Bedarf aufgenommen werden.
Dieser Branch ist für Produktivsysteme gedacht. Er wird aktualisiert, wenn genügend Änderungen für eine neue Version
zusammengekommen sind.

Der **EARLY** Branch (Name kann sich noch ändern) wird alle neu entwickelten Funktionen enthalten, sofern sie keine
Änderungen an der Datenbank oder am Index erfordern. Das heißt alles was fertig ist und durch ein einfaches Update mit
Git übernommen werden kann. Eine Instanz kann auf diesem Branch betrieben werden, wenn immer die neuesten Funktionen
genutzt werden sollen.

Die Branches mit konkreten Versionsnummern sind dazu da Änderungen zu sammeln, die ein komplexeres Update erfordern,
z.B. das Ausführen von Skripten, um das Datenbankschema zu aktualisieren oder Änderungen am Solr Index vorzunehmen.
Diese Änderungen werden in größeren Abständen mit großen Versionnummern, wie **4.6**, veröffentlicht werden.
