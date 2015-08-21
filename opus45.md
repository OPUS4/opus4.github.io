---
title: OPUS 4.5
---

# Was ist neu in OPUS 4.5

OPUS 4.5 sollte eigentlich die Version 4.4.6 bekommen und nur kleinere Probleme beheben. Im Laufe der Zeit hat sich
dann aber gezeigt, daß dies ein sehr wichtiger Release ist bei dem sich viel für die weitere Entwicklung von OPUS
verändert. Was bedeutet das?

Die Entwicklung von OPUS 4 ist zu GitHub migriert. Es war vorher ein Open Source Projekt. Der Source Code war immer auf
den Subversion Repositorien am ZIB frei zugänglich. Diese Repositorien sind auch weiterhin zugänglich werden aber nicht
mehr weiter gepflegt.  Die Dateien wurden mit Ihrer Vergangenheit in neue Git Repositorien auf GitHub verschoben.

Mit Version 4. 5 ändert sich die empfohlene Methode zur Installation von OPUS. Statt des Tarballs wird empfohlen mit Git
einen Clone von OPUS 4 anzulegen. Die Clone Operation ersetzt im Prinzip das Herunterladen und Auspacken des Tarballs.
Was ist der Vorteil?

Ein Git Clone ist selbst ein Git Repository und weiß woher der Code kommt. Wenn es Änderungen im ursprünglichen
Repository (origin) gibt können diese mit einfachen Kommando übernommen werden.

Das heißt, daß Bug Fixes und Verbesserungen sofort zur Verfügung gestellt werden und übernommen werden können. Die
Entscheidung, ob man die eigene Instanz sofort aktualisieren möchte oder lieber auf den nächsten Release wartet kann
jede Institution selbst treffen.

Vorerst wird es weiterhin den Tarball geben. Er wird ein oder zweimal im Jahr auf den neuesten Stand gebracht werden.
