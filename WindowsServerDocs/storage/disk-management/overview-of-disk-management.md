---
title: 'Datenträgerverwaltung: Übersicht'
description: Die Datenträgerverwaltung ist ein Systemhilfsprogramm unter Windows, mit dem du erweiterte Speicheraufgaben ausführen kannst, wie z.B. die Initialisierung eines neuen Laufwerks, die Erweiterung von Volumes, das Schrumpfen von Partitionen und das Ändern von Laufwerksbuchstaben.
ms.date: 06/07/2019
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: a3885ae6b09ad431fd1ea5e4c593e02c7bb274d9
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2019
ms.locfileid: "66812548"
---
# <a name="overview-of-disk-management"></a>Datenträgerverwaltung: Übersicht

> **Gilt für:** Windows 10, Windows 8.1, Windows 7, Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die Datenträgerverwaltung ist ein Systemhilfsprogramm unter Windows, mit dem du erweiterte Speicheraufgaben ausführen kannst. Die Datenträgerverwaltung ist u.a. für folgende Aufgaben geeignet:

- Informationen zum Einrichten eines neuen Laufwerks findest du unter [Initialisieren neuer Datenträger](initialize-new-disks.md).
- Wie du ein Volume in einen Speicherplatz hinein erweiterst, der nicht bereits Teil eines Volumes auf demselben Laufwerk ist, erfährst du unter [Erweitern eines Basisvolumes](extend-a-basic-volume.md).
- Wie du eine Partition so verkleinerst, dass du eine benachbarte Partition erweitern kannst, erfährst du unter [Verkleinern eines Basisvolumes](shrink-a-basic-volume.md).
- Wie du einen Laufwerkbuchstaben änderst oder einen neuen Laufwerkbuchstaben zuweist, erfährst du unter [Ändern eines Laufwerkbuchstabens](change-a-drive-letter.md).

![Datenträgerverwaltung mit einem typischen Laufwerk mit drei Partitionen – einer 499-MB-Systempartition, einem größeren C-Laufwerk für Windows und einer weiteren 499-MB-Partition für die Wiederherstellung.](media/disk-management.png)

> [!TIP]
>  Wenn du beim Befolgen dieser Verfahren eine Fehlermeldung erhältst oder etwas nicht funktioniert, wirf einen Blick in das Thema [Datenträgerverwaltung: Problembehandlung](troubleshooting-disk-management.md). Wenn dies nicht hilft – keine Panik! In der [Microsoft-Community](https://answers.microsoft.com/en-us/windows) stehen jede Menge Informationen zur Verfügung. Durchsuche am besten den Abschnitt [Dateien, Ordner und Onlinespeicher](https://answers.microsoft.com/en-us/windows/forum/windows_10-files?sort=lastreplydate&dir=desc&tab=All&status=all&mod=&modAge=&advFil=&postedAfter=&postedBefore=&threadType=all&isFilterExpanded=true&tm=1514405359639). Solltest du danach immer noch Hilfe benötigen, kannst du dort eine Frage stellen, die dann von Microsoft oder von anderen Mitgliedern der Community beantwortet wird. Wir freuen uns auch über Feedback zu Verbesserungsmöglichkeiten bei diesen Themen. Beantworte einfach die Frage *Ist diese Seite hilfreich?* , und hinterlasse dort oder in den öffentlichen Kommentaren am Ende dieses Themas einen Kommentar.

Die folgenden gängigen Aufgaben möchtest du vielleicht erledigen, aber hierfür werden andere Tools in Windows verwendet:

- Wie du Speicherplatz freigibst, erfährst du unter [Freigeben von Speicherplatz unter Windows 10](https://support.microsoft.com/help/12425/windows-10-free-up-drive-space).
- Wie du deine Laufwerke defragmentierst, erfährst du unter [Defragmentieren des Windows 10-PCs](https://support.microsoft.com/help/4026701/windows-defragment-your-windows-10-pc).
- Wie du mehrere Festplatten in einem Pool ähnlich einem RAID zusammenfasst, erfährst du unter [Speicherplätze unter Windows 10](https://support.microsoft.com/help/12438/windows-10-storage-spaces).

## <a name="about-those-extra-recovery-partitions"></a>Informationen zu diesen zusätzlichen Wiederherstellungspartitionen

Falls du neugierig bist (wir haben deine Kommentare gelesen!): Windows umfasst typischerweise drei Partitionen auf deinem Hauptlaufwerk (normalerweise das C:-Laufwerk):

![Datenträger 0 mit drei Partitionen – eine EFI-Systempartition, die Windows-Partition und eine Wiederherstellungspartition](media/windows-partitions.png)

- **EFI-Systempartition**: Sie wird bei modernen PCs zum Starten (Booten) des PCs und des Betriebssystems verwendet.
- **Windows-Betriebssystemlaufwerk (C:)** : Hier ist Windows installiert ist, und in der Regel speicherst du dort deine übrigen Apps und Dateien.
- **Wiederherstellungspartition**: Hier werden spezielle Tools gespeichert, die dir bei der Wiederherstellung von Windows helfen, falls Probleme beim Starten oder andere schwerwiegende Probleme auftreten.

Wenn die Datenträgerverwaltung die EFI-Systempartition und die Wiederherstellungspartition als 100% frei anzeigt, lügt sie. Diese Partitionen enthalten in der Regel viele wirklich wichtige Dateien, die dein PC benötigt, um ordnungsgemäß zu funktionieren. Du solltest sie einfach in Ruhe ihre Arbeit erledigen lassen, damit sie deinen PC starten und dir helfen, Probleme zu beheben.

## <a name="see-also"></a>Weitere Informationen

- [Verwalten von Datenträgern](manage-disks.md)
- [Verwalten von Basisvolumes](manage-basic-volumes.md)
- [Datenträgerverwaltung: Problembehandlung](troubleshooting-disk-management.md)
- [Wiederherstellungsoptionen unter Windows 10](https://support.microsoft.com/help/12415/windows-10-recovery-options)
- [Suchen nach fehlenden Dateien nach dem Upgrade auf Windows 10](https://support.microsoft.com/help/12386/windows-10-find-lost-files-after-update)
- [Sichern und Wiederherstellen in Windows 10](https://support.microsoft.com/help/17143/windows-10-back-up-your-files)
- [Erstellen eines Wiederherstellungslaufwerks](https://support.microsoft.com/help/4026852/windows-create-a-recovery-drive)
- [Erstellen eines Systemwiederherstellungspunkts](https://support.microsoft.com/help/4027538/windows-create-a-system-restore-point)
- [Suchen des BitLocker-Wiederherstellungsschlüssels](https://support.microsoft.com/help/4026181/windows-find-my-bitlocker-recovery-key)
