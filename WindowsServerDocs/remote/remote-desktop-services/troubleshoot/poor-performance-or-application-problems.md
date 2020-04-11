---
title: Eingeschränkte Leistung oder Anwendungsprobleme während der Remotedesktopverbindung
description: Beheben von eingeschränkter Leistung oder Anwendungsproblemen während der Remotedesktopverbindung.
ms.reviewer: rklemen
ms.topic: troubleshooting
author: kaushika-msft
manager: dcscontentpm
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 91ced9e729966ee9c46e76d01d7ccbec9a510f5b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857223"
---
# <a name="poor-performance-or-application-problems-during-remote-desktop-connection"></a>Eingeschränkte Leistung oder Anwendungsprobleme während der Remotedesktopverbindung

In diesem Artikel werden verschiedene häufige Probleme behandelt, die bei Benutzern auftreten können, wenn sie Remotedesktopfunktionen verwenden.

### <a name="intermittent-problems-with-new-microsoft-azure-virtual-machines"></a>Gelegentlich auftretende Probleme bei virtuellen Microsoft Azure-Computern

Dieses Problem betrifft virtuelle Computer, die vor Kurzem bereitgestellt wurden. Nachdem der Benutzer eine Verbindung mit dem virtuellen Computer hergestellt hat, lädt die Remotedesktopsitzung nicht alle Einstellungen des Benutzers ordnungsgemäß.

Um dieses Problem zu umgehen, trennen Sie die Verbindung mit dem virtuellen Computer, warten Sie mindestens 20 Minuten lang, und stellen Sie dann wieder eine Verbindung her.

Um dieses Problem zu lösen, wenden Sie die folgenden Updates nach Eignung auf die virtuellen Computer an:

  - Windows 10 und Windows Server 2016: KB 4343884, [30. August 2018 – KB4343884 (Betriebssystembuild 14393.2457)](https://support.microsoft.com/help/4343884/windows-10-update-kb4343884)
  - Windows Server 2012 R2: KB 4343891, [30. August 2018 – KB4343891 (Vorschau des monatlichen Rollups)](https://support.microsoft.com/help/4343891/windows-81-update-kb4343891)

### <a name="video-playback-issues-on-windows-10-version-1709"></a>Probleme mit der Videowiedergabe unter Windows 10, Version 1709

Dieses Problem tritt auf, wenn Benutzer Verbindungen mit Remotecomputern herstellen, die Windows 10, Version 1709, ausführen. Wenn diese Benutzer ein Video mithilfe des VMR9-Codecs (Video Mixing Renderer 9) wiedergeben, zeigt der Player nur ein schwarzes Fenster an.

Dies ist ein bekanntes Problem in Windows 10, Version 1709. Das Problem tritt unter Windows 10, Version 1703, nicht auf.

### <a name="desktop-sharing-issues-on-windows-10"></a>Probleme mit der Desktopfreigabe unter Windows 10

Dieses Problem tritt auf, wenn der Benutzer ein schreibgeschütztes Benutzerprofil (und eine zugeordnete Registrierungsstruktur) besitzt, wie etwa in einem Kioskszenario. Wenn ein solcher Benutzer eine Verbindung mit einem Remotecomputer unter Windows 10, Version 1803, herstellt, kann er seinen Desktop nicht freigeben.

Um dieses Problem zu beheben, wenden Sie das Windows 10-Update 4340917, [24. Juli 2018 – KB4340917 (Betriebssystembuild 17134.191)](https://support.microsoft.com/help/4340917/windows-10-update-kb4340917) an.

### <a name="performance-issues-when-mixing-versions-of-windows-10-if-nla-is-disabled"></a>Leistung bei der gemischten Verwendung von Windows 10-Versionen, wenn NLA deaktiviert ist

Dieses Problem tritt auf, wenn NLA deaktiviert ist und Remotedesktop-Clientcomputer, auf denen Windows 10 ausgeführt wird, Verbindungen mit Remotedesktops herstellen, auf denen andere Versionen von Windows 10 ausgeführt werden. Benutzer von Remotedesktopclients auf Computern, auf denen Windows 10, Version 1709 oder früher, ausgeführt wird, erfahren eine Beeinträchtigung der Leistung bei Verbindungen mit Remotedesktops, auf denen Windows 10, Version 1803 oder höher, ausgeführt wird.

Dies tritt auf, weil bei deaktivierter NLA die älteren Clientcomputer ein langsameres Protokoll für Verbindungen mit Windows 10, Version 1803 oder höher, verwenden.

Um dieses Problem zu beheben, wenden Sie KB 4340917, [24. Juli 2018 — KB4340917 (Betriebssystembuild 17134.191)](https://support.microsoft.com/help/4340917/windows-10-update-kb4340917) an.

### <a name="black-screen-issue"></a>Problem mit schwarzem Bildschirm

Dieses Problem tritt in Windows 8.0, Windows 8.1, Windows 10 RTM und Windows Server 2012 R2 auf. Ein Benutzer startet mehrere Anwendungen auf einem Remotedesktop und trennt anschließend die Verbindung. In regelmäßigen Abständen stellt der Benutzer die Verbindung mit dem Remotedesktop wieder her, um mit den Anwendungen zu interagieren, und trennt die Verbindung dann wieder. An einem bestimmten Punkt zeigt die Remotedesktopsitzung beim Wiederherstellen der Verbindung nur einen schwarzen Bildschirm an. Damit die Sitzung wieder korrekt dargestellt wird, muss der Benutzer die Sitzung entweder über die Konsole des Remotecomputers oder die RDSH-Serverkonsole beenden und die Anwendungen seiner Sitzung beenden.

Um dieses Problem zu beheben, wenden Sie die folgenden Updates nach Eignung an:

  - Windows 8 und Windows Server 2012 KB4103719, [17. Mai 2018 – KB4103719 (Vorschau der monatlichen Zusammenfassung)](https://support.microsoft.com/help/4103719/windows-server-2012-update-kb4103719)
  - Windows 8.1 und Windows Server 2012 R2: KB4103724, [17 Mai 2018 – KB4103724 (Vorschau des monatlichen Rollups)](https://support.microsoft.com/help/4103724/windows-81-update-kb4103724) und KB 4284863, [21. Juni 2018 – KB4284863 (Vorschau des monatlichen Rollups)](https://support.microsoft.com/help/4284863/windows-81-update-kb4284863)
  - Windows 10: Behoben in KB4284860, [12. Juni 2018 – KB4284860 (Betriebssystembuild 10240.17889)](https://support.microsoft.com/help/4284860/windows-10-update-kb4284860)
