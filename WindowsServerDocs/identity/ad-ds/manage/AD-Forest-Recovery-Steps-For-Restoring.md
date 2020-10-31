---
title: 'AD-Gesamtstruktur Wiederherstellung: Schritte zum Wiederherstellen der Gesamtstruktur'
ms.author: daveba
author: iainfoulds
manager: daveba
ms.date: 08/09/2018
ms.topic: article
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.openlocfilehash: fcddc2d0f9f9bc755d20700c756450f2d0ff46cc
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "93070792"
---
# <a name="ad-forest-recovery---steps-for-restoring-the-forest"></a>AD-Gesamtstruktur Wiederherstellung: Schritte zum Wiederherstellen der Gesamtstruktur

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Dieser Abschnitt enthält eine Übersicht über den empfohlenen Pfad für die Wiederherstellung einer Gesamtstruktur. Die Schritte zur Wiederherstellung der Gesamtstruktur werden später ausführlich beschrieben.

In der folgenden Liste sind die Wiederherstellungsschritte auf hoher Ebene zusammengefasst:

1. [Identifizieren des Problems](AD-Forest-Recovery-Identify-the-Problem.md)

   Arbeiten Sie daran, und Microsoft-Support, um den Umfang des Problems und mögliche Ursachen zu ermitteln und mögliche Abhilfemaßnahmen für alle Beteiligten zu evaluieren. In vielen Fällen sollte die Gesamtstruktur Wiederherstellung die letzte Option sein.

2. [Entscheiden, wie die Gesamtstruktur wieder hergestellt werden soll](AD-Forest-Recovery-Determine-how-to-Recover.md)

   Nachdem Sie festgestellt haben, dass die Wiederherstellung der Gesamtstruktur erforderlich ist, führen Sie die vorbereitenden Schritte für die Vorbereitung aus: bestimmen Sie die aktuelle Gesamtstruktur, ermitteln Sie die Funktionen, die von den einzelnen Domänen Controllern ausgeführt werden, und legen Sie fest, welcher Domänen Controller für jede Domäne wieder hergestellt werden soll.

3. [Anfängliche Wiederherstellung ausführen](AD-Forest-Recovery-Perform-initial-recovery.md)

   Stellen Sie in Isolation einen DC für jede Domäne wieder her, bereinigen Sie Sie, und verbinden Sie die Domänen erneut. Zurücksetzen privilegierter Konten und Beheben von Problemen, die in dieser Phase durch Sicherheitsverletzungen verursacht werden.

4. [Erneutes Bereitstellen der restlichen DCS](AD-Forest-Recovery-Restore-Additional-DCs.md)

   Stellen Sie die Gesamtstruktur erneut bereit, um den Status vor dem Fehler wiederherzustellen. Dieser Schritt muss an Ihren speziellen Entwurf und Ihre Anforderungen angepasst werden. Das Klonen von virtualisierten Domänen Controllern kann dazu beitragen, diesen Prozess zu beschleunigen.

5. [Bereinigung](AD-Forest-Recovery-Cleanup.md)

   Nachdem die Funktionalität wieder hergestellt wurde, konfigurieren Sie die Namensauflösung nach Bedarf neu, und Sie erhalten LOB-Anwendungen.

Die Schritte in diesem Handbuch dienen dazu, die Möglichkeit zu minimieren, dass gefährliche Daten in die wiederhergestellte Gesamtstruktur wieder eingeführt werden. Sie müssen diese Schritte ggf. so ändern, dass folgende Faktoren berücksichtigt werden:

- Skalierbarkeit
- Remote Verwaltbarkeit
- Geschwindigkeit der Wiederherstellung
