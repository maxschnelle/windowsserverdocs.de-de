---
title: 'Anmerkungen zu dieser Version: Wichtige Probleme in Windows Server 2016'
description: Nachfolgend sind wichtige Probleme aufgeführt, für die eine Problemumgehung erforderlich ist, um einen Absturz, das Aufhängen des Systems, einen Installationsfehler oder Datenverlust zu verhindern.
ms.prod: windows-server
ms.date: 11/13/2018
ms.technology: server-general
ms.topic: article
ms.assetid: 134aab85-664f-4d44-87ef-9e5fd389071f
author: jaimeo
ms.author: jaimeo
ms.openlocfilehash: 8ceff837c2b85466f5583eed03f39e73f32fd4a4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80826383"
---
# <a name="release-notes-important-issues-in-windows-server-2016"></a>Versionshinweise: Wichtige Probleme in Windows Server 2016

>Gilt für: Windows Server 2016

In diesen Versionshinweisen sind die wichtigsten Probleme des Windows Server 2016-Betriebssystems zusammengefasst, und du erfährst, wie sich diese Probleme gegebenenfalls umgehen lassen. Informationen zu standardmäßigen Änderungen, neuen Features und Fixes in diesem Release finden Sie unter [Neues in Windows Server 2016](whats-new-in-windows-server-2016.md) und in den Ankündigungen der zuständigen Featureteams. Sofern es nicht anders angegeben ist, gelten alle aufgeführten Probleme für alle Editionen und Installationsoptionen von Windows Server 2016.

Dieses Dokument wird ständig aktualisiert. Wenn kritische Probleme ermittelt werden, die eine Problemumgehung erfordern, werden diese genauso wie neue Problemumgehungen und Fixes hinzugefügt, sobald sie verfügbar sind.

## <a name="express-updates-available-starting-in-november-2018-new"></a>Expressupdates ab November 2018 verfügbar (NEU)

Ab dem Update im November 2018 (Update-Dienstag) werden von Windows wieder [Expressupdates](express-updates.md) für Windows Server 2016 veröffentlicht. Benutzern von WSUS und Configuration Manager werden wieder zwei Pakete für das Windows Server 2016-Update angezeigt: ein vollständiges Update und ein Expressupdate. Wenn du in deinen Serverumgebungen die Expressoption verwenden möchtest, vergewissere dich, dass auf dem Server seit November 2017 (KB 4048953) ein vollständiges Update ausgeführt wurde, um sicherzustellen, dass das Expressupdate ordnungsgemäß installiert wird. Bei Servern, die seit dem 11B-Update von 2017 (KB 4048953) nicht mehr aktualisiert wurden, treten beim Versuch, das Expressupdate anzuwenden, wiederholt Fehler auf, die Bandbreite und CPU-Ressourcen in einer Endlosschleife beanspruchen. Beende in diesem Fall das Pushen des Expressupdates, und pushe stattdessen ein aktuelles vollständiges Update, um die Fehlerschleife zu beenden.

## <a name="server-core-installation-option"></a>Server Core-Installationsoption

[comment]: # (ID: 370; Übermittler: amason; Status: abgemeldet)

Wenn Sie Windows Server 2016 installieren, indem Sie die Option „Server Core-Installation“ verwenden, wird der Druckspooler installiert und standardmäßig gestartet, auch wenn die Druckserverrolle nicht installiert ist.

Legen Sie den Druckspooler nach dem ersten Start auf „Deaktiviert“ fest, um dies zu vermeiden.

## <a name="containers"></a>Container

[comment]: # (ID: 371; Übermittler: taylorb; Status: abgemeldet)
- Installiere vor der Verwendung von Containern das [Bereitstellungsstapel-Update für Windows 10 Version 1607: 23. August 2016](https://support.microsoft.com/kb/3176936) oder spätere Updates, die verfügbar sind. Andernfalls können verschiedene Probleme (unter anderem beim Erstellen, Starten oder Ausführen von Containern) sowie Fehler wie der folgende auftreten: „CreateProcess failed in Win32: The RPC server is unavailable“, Fehler bei CreateProcess in Win32: Der RPC-Server ist nicht verfügbar.

[comment]: # (ID: 373; Übermittler: plang; Status: abgemeldet)
- Der NanoServerPackage OneGet-Anbieter funktioniert nicht in Windows-Containern. Um dieses Problem zu umgehen, verwenden Sie Find-NanoServerPackage und Save-NanoServerPackage auf einem anderen Computer (nicht auf einem Container), um das benötigte Paket herunterzuladen. Anschließend kopieren Sie die Pakete in den Container und installieren sie.

## <a name="device-guard"></a>Device Guard

[comment]: # (ID: 369; Übermittler: nirb; Status: abgemeldet)
Beachten Sie bei Verwendung von virtualisierungsbasiertem Schutz der Codeintegrität oder abgeschirmten virtuellen Computern (die virtualisierungsbasierten Schutz der Codeintegrität verwenden), dass diese Technologien mit einigen Geräten und Anwendungen u. U. nicht kompatibel sind. Solche Konfigurationen sollten Sie vor der Aktivierung der Features in Produktionssystemen in Ihrem Labor testen. Andernfalls kann es zu unerwarteten Datenverlusten oder Abbruchfehlern kommen.

## <a name="microsoft-exchange"></a>Microsoft Exchange

[comment]: # (ID: 375; Übermittler: wgries; Status: abgemeldet)
Wenn Sie versuchen, Microsoft Exchange 2016 CU3 unter Windows Server 2016 auszuführen, treten im IIS-Hostprozess „W3WP.exe“ Fehler auf. Dieses Problem kann derzeit nicht vermieden werden. Sie sollten die Bereitstellung von Exchange 2016 CU3 unter Windows Server 2016 verschieben, bis ein Update zur Behebung dieses Problems verfügbar ist.

## <a name="remote-server-administration-tools-rsat"></a>Remoteserver-Verwaltungstools (RSAT)

[comment]: # (ID: 374; Übermittler: ryanpu; Status: abgemeldet)
Wenn du eine Version von Windows 10 verwendest, die älter als Windows 10 Anniversary Update ist, Hyper-V sowie virtuelle Computer mit aktiviertem Trusted Platform Module (einschließlich abgeschirmter virtueller Computer) verwendest und anschließend die für Windows Server 2016 bereitgestellte Version von RSAT installierst, tritt beim Versuch, diese virtuellen Computer zu starten, ein Fehler auf.

Führen Sie für den Clientcomputer ein Upgrade auf Windows 10 Anniversary Update (oder höher) durch, bevor Sie RSAT installieren, um dies zu vermeiden. Wenn dies bereits aufgetreten ist, deinstallieren Sie RSAT, führen Sie ein Upgrade für den Client auf Window 10 Anniversary Update durch, und installieren Sie RSAT anschließend erneut.

## <a name="shielded-virtual-machines"></a>Abgeschirmte VMs

[comment]: # (ID: 369; Übermittler: nirb; Status: abgemeldet)  
- Stellen Sie sicher, dass Sie alle verfügbaren Updates installiert haben, bevor Sie abgeschirmte virtuelle Computer in der Produktion bereitstellen.

- Beachten Sie bei Verwendung von virtualisierungsbasiertem Schutz der Codeintegrität oder abgeschirmten virtuellen Computern (die virtualisierungsbasierten Schutz der Codeintegrität verwenden), dass diese Technologien mit einigen Geräten und Anwendungen u. U. nicht kompatibel sind. Solche Konfigurationen sollten Sie vor der Aktivierung der Features in Produktionssystemen in Ihrem Labor testen. Andernfalls kann es zu unerwarteten Datenverlusten oder Abbruchfehlern kommen.

## <a name="start-menu"></a>Startmenü

[comment]: # (ID: 372; Übermittler: samli; Status: abgemeldet)
Dieses Problem betrifft Windows Server 2016, installiert mit der Option „Server mit Desktopdarstellung“.

Wenn du Anwendungen installierst, die Verknüpfungselemente in einem Ordner im **Startmenü** hinzufügen, funktionieren die Verknüpfungen erst, nachdem du dich abgemeldet und wieder angemeldet hast.

Wechseln Sie zurück zum Haupthub von [Windows Server 2016](Windows-Server-2016.md).

## <a name="storport-performance"></a>StorPort-Leistung

Einige Systeme besitzen unter einer neuen Installation von Windows Server 2016 möglicherweise eine geringere Speicherleistung als unter Windows Server 2012 R2.  Bei der Entwicklung von Windows Server 2016 wurde eine Reihe von Änderungen zur Verbesserung der Sicherheit und Zuverlässigkeit der Plattform vorgenommen. Einige Änderungen wie etwa die standardmäßige Aktivierung von Windows Defender führen zu längeren E/A-Pfaden, was die E/A-Leistung bei bestimmten Workloads und Mustern beeinträchtigen kann. Microsoft rät davon ab, Windows Defender zu deaktivieren, da es sich dabei um eine wichtige Schutzebene für Ihre Systeme handelt.  

## <a name="copyright"></a>Copyright

Dieses Dokument wird ohne Gewähr zur Verfügung gestellt. Die in diesem Dokument enthaltenen Informationen und Ansichten, einschließlich URLs und andere Verweise auf Internetwebsites, können ohne vorherige Ankündigung geändert werden.  

Dieses Dokument stellt Ihnen keinerlei Rechte am geistigen Eigentum eines beliebigen Microsoft-Produkts zur Verfügung. Dieses Dokument darf für interne Referenzzwecke kopiert und verwendet werden.  

&copy; 2016 Microsoft Corporation. Alle Rechte vorbehalten.  

Microsoft, Active Directory, Hyper-V, Windows, und Windows Server sind entweder eingetragene Marken oder Marken der Microsoft Corporation in den USA und/oder anderen Ländern oder Regionen.  

Dieses Produkt enthält Grafikfiltersoftware; diese Software basiert zum Teil auf der Arbeit der Independent JPEG Group.  

1.0
