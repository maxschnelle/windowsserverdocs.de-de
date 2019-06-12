---
title: 'Datenträgerverwaltung: Übersicht'
description: Die Datenträgerverwaltung ist ein Systemprogramm in Windows, die Ihnen ermöglicht, erweiterte Storage-Aufgaben, z. B. ein neues Laufwerk zu initialisieren, Erweitern von Volumes, Verkleinern von Partitionen und Ändern von Laufwerkbuchstaben auszuführen.
ms.date: 06/07/2019
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: a3885ae6b09ad431fd1ea5e4c593e02c7bb274d9
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812548"
---
# <a name="overview-of-disk-management"></a>Datenträgerverwaltung: Übersicht

> **Gilt für:** Windows 10, Windows 8.1, Windows 7, WindowsServer (Halbjährlicher Kanal), WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012

Die Datenträgerverwaltung ist ein Systemprogramm in Windows, die Sie erweiterte Aufgaben ausführen können. Hier sind einige Dinge, die die Datenträgerverwaltung für geeignet ist:

- Um ein neues Laufwerk einrichten zu können, finden Sie unter [initialisieren ein neues Laufwerk](initialize-new-disks.md).
- Zum Erweitern eines Volumes in den Speicherplatz, der nicht bereits Teil eines Volumes auf dem gleichen Laufwerk ist, finden Sie unter [Erweitern eines Basisvolumes](extend-a-basic-volume.md).
- Verkleinern Sie eine Partition, in der Regel, damit Sie eine Partition benachbarte erweitern können, finden Sie unter [Verkleinern eines Basisvolumes](shrink-a-basic-volume.md).
- Um einen Laufwerkbuchstaben zu ändern oder einen neuen Laufwerkbuchstaben zuweisen, finden Sie unter [ändern Sie einen Laufwerkbuchstaben](change-a-drive-letter.md).

![Ein typisches Laufwerk mit drei Partitionen – eine Systempartition 499 MB, ein größeres C-Laufwerk für Windows und einer anderen 499 MB-Partition für die Wiederherstellung mit Datenträger-Verwaltung](media/disk-management.png)

> [!TIP]
>  Wenn Sie eine Fehlermeldung erhalten oder etwas nicht möglich, wenn diese Verfahren befolgen, nehmen Sie einen Blick die [Datenträgerverwaltung: Problembehandlung](troubleshooting-disk-management.md) Thema. Wenn dies nicht helfen – keine Panik! Auf eine Fülle von Informationen ist die [Microsoft-Community](https://answers.microsoft.com/en-us/windows) site – suchen Sie die [Dateien, Ordner und Speicher](https://answers.microsoft.com/en-us/windows/forum/windows_10-files?sort=lastreplydate&dir=desc&tab=All&status=all&mod=&modAge=&advFil=&postedAfter=&postedBefore=&threadType=all&isFilterExpanded=true&tm=1514405359639) aus, und wenn Sie weitere Hilfe benötigen, senden, gibt es eine Frage und von Microsoft oder anderen Mitgliedern der der Community versucht, die helfen. Wenn Sie Feedback zum Verbessern der in diesen Themen haben, wir würden uns über Ihre anregungen! Beantworten Sie einfach die *ist diese Seite hilfreich?* Eingabeaufforderung ein, und lassen Sie alle Kommentare, dort oder aber in der öffentlichen Kommentare Thread am Ende dieses Themas.

Hier sind einige allgemeinen Aufgaben, die Sie tun möchten, können jedoch, die anderen Tools in Windows verwenden:

- Zum Freigeben von Speicherplatz finden Sie unter [Speicherplatz auf Laufwerk in Windows 10-](https://support.microsoft.com/help/12425/windows-10-free-up-drive-space).
- Um Ihre Laufwerke defragmentieren möchten, finden Sie unter [Ihres Windows 10-PCs zu defragmentieren](https://support.microsoft.com/help/4026701/windows-defragment-your-windows-10-pc).
- Mehrere Festplatten und pool zusammen, wie ein RAID, finden Sie unter [Speicherplätze](https://support.microsoft.com/help/12438/windows-10-storage-spaces).

## <a name="about-those-extra-recovery-partitions"></a>Informationen zu diesen zusätzlichen Wiederherstellungspartitionen

Für den Fall, dass Sie wissen (Wir haben Ihre Kommentare lesen!), umfasst Windows in der Regel drei Partitionen auf dem Haupt-Laufwerk (normalerweise C:\ Laufwerk):

![Datenträger 0 mit drei Partitionen – eine EFI-Systempartition, die Windows-Partition und einer Wiederherstellungspartition](media/windows-partitions.png)

- **EFI-Systempartition** – wird von modernen PCs zum (start) verwendet Ihr PC und ein Betriebssystem.
- **Windows-Betriebssystemlaufwerk (c)** – Dies ist, auf dem Windows installiert ist, und in der Regel fügen Sie den Rest Ihrer apps und Dateien hinzu.
- **Wiederherstellungspartition** – Dies ist, in denen spezielle Tools gespeichert sind, können Sie die Windows wiederherstellen, falls es Probleme beim Starten oder andere ernsthafte Probleme ausgeführt wird.

Obwohl Datenträgerverwaltung die EFI-Systempartition und die Wiederherstellungspartition als 100 % frei anzeigen kann, ist es zurück. Diese Partitionen sind in der Regel ziemlich voller wirklich wichtigen Dateien, die Ihr PC benötigt wird, ordnungsgemäß funktioniert. Es wird empfohlen, lassen Sie sie allein dazu ihre Arbeit, starten Ihren PC, und so können Sie die Probleme zu beheben.

## <a name="see-also"></a>Siehe auch

- [Verwalten von Datenträgern](manage-disks.md)
- [Verwalten von Basisvolumes](manage-basic-volumes.md)
- [Datenträgerverwaltung: Problembehandlung](troubleshooting-disk-management.md)
- [Wiederherstellungsoptionen im Windows 10](https://support.microsoft.com/help/12415/windows-10-recovery-options)
- [Suchen nach verlorenen Dateien nach der Aktualisierung auf Windows 10](https://support.microsoft.com/help/12386/windows-10-find-lost-files-after-update)
- [Sichern und Wiederherstellen von Dateien](https://support.microsoft.com/help/17143/windows-10-back-up-your-files)
- [Erstellen Sie ein Wiederherstellungslaufwerk](https://support.microsoft.com/help/4026852/windows-create-a-recovery-drive)
- [Erstellen eines Systemwiederherstellungspunkts](https://support.microsoft.com/help/4027538/windows-create-a-system-restore-point)
- [Suchen Sie die BitLocker-Wiederherstellungsschlüssel](https://support.microsoft.com/help/4026181/windows-find-my-bitlocker-recovery-key)
