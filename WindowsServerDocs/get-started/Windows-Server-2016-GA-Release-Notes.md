---
title: 'Anmerkungen zu dieser Version: Wichtige Probleme in Windows Server 2016'
description: Nachfolgend sind wichtige Probleme aufgeführt, für die eine Problemumgehung erforderlich ist, um einen Absturz, das Aufhängen des Systems, einen Installationsfehler oder Datenverlust zu verhindern.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 11/13/2018
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 134aab85-664f-4d44-87ef-9e5fd389071f
author: jaimeo
ms.author: jaimeo
ms.openlocfilehash: dec1ec184a147ef4fae64e9cc4384c0b6e4510b6
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749540"
---
# <a name="release-notes-important-issues-in-windows-server-2016"></a>Versionshinweise: Wichtige Probleme in WindowsServer 2016

>Gilt für: Windows Server 2016

Diese Anmerkungen zur Version fassen zusammen, die wichtigsten Probleme in das Betriebssystem Windows Server 2016, einschließlich der Möglichkeiten zum Umgehen der Probleme, sofern bekannt. Informationen zu standardmäßigen Änderungen, neuen Features und Fixes in diesem Release finden Sie unter [Neues in Windows Server 2016](whats-new-in-windows-server-2016.md) und in den Ankündigungen der zuständigen Featureteams. Sofern es nicht anders angegeben ist, gelten alle aufgeführten Probleme für alle Editionen und Installationsoptionen von Windows Server 2016.

Dieses Dokument wird ständig aktualisiert. Wenn kritische Probleme ermittelt werden, die eine Problemumgehung erfordern, werden diese genauso wie neue Problemumgehungen und Fixes hinzugefügt, sobald sie verfügbar sind.

## <a name="express-updates-available-starting-in-november-2018-new"></a>Express-Updates ab, die im November 2018 (neu)

Ab dem November 2018 "Tuesday aktualisieren"-Update, Windows erneut veröffentlichen [-Express-Updates](express-updates.md) für Windows Server 2016. Wenn Sie WSUS und System Center Configuration Manager (SCCM) verwenden, sehen Sie erneut zwei Pakete für das Windows Server 2016-Update: ein vollständiges Update und ein Express-Update. Wenn Sie Express für Ihre Umgebung Server verwenden möchten, müssen Sie sicherstellen, dass der Server eine vollständige Aktualisierung seit November 2017 (KB-4048953) um sicherzustellen, dass das Express-Update installiert wurde ordnungsgemäß angewendet wurde. Wenn Sie eine Express-Updates auf einem Server, die seit dem Update für 2017-11 (KB-4048953 versuchen) nicht aktualisiert wurde, sehen Sie wiederholte Fehler, die von Bandbreite und CPU-Ressourcen in eine Endlosschleife zu nutzen. Wenn Sie in diesem Szenario erhalten haben, beenden Sie die Übertragung des Express-Updates, und übertragen Sie eine aktuelle vollständige Aktualisierung zum Beenden der Schleife Fehler.

## <a name="server-core-installation-option"></a>Server Core-Installationsoption

[comment]: # (ID: 370; Übermittler: Amason; Status: hat genehmigt)

Wenn Sie Windows Server 2016 installieren, indem Sie die Option „Server Core-Installation“ verwenden, wird der Druckspooler installiert und standardmäßig gestartet, auch wenn die Druckserverrolle nicht installiert ist.

Legen Sie den Druckspooler nach dem ersten Start auf „Deaktiviert“ fest, um dies zu vermeiden.

## <a name="containers"></a>Container

[comment]: # (ID: 371; Übermittler: Taylorb; Status: hat genehmigt)
- Bevor Sie Container verwenden, installieren Sie [Bereitstellungsstapel-Update für Windows 10 Version 1607: 23. August 2016](https://support.microsoft.com/en-us/kb/3176936) oder spätere Updates, die verfügbar sind. Andernfalls, eine Reihe von Problemen auftreten, einschließlich Fehlern beim Erstellen, starten oder Ausführen von Containern und ähnliche Fehler wie "Fehler bei der CreateProcess in Win32: Der RPC-Server ist nicht verfügbar."

[comment]: # (ID: 373; Übermittler: Plang; Status: hat genehmigt)
- Der NanoServerPackage OneGet-Anbieter funktioniert nicht in Windows-Containern. Um dieses Problem zu umgehen, verwenden Sie Find-NanoServerPackage und Save-NanoServerPackage auf einem anderen Computer (nicht auf einem Container), um das benötigte Paket herunterzuladen. Anschließend kopieren Sie die Pakete in den Container und installieren sie.

## <a name="device-guard"></a>Device Guard

[comment]: # (ID: 369; Übermittler: Nirb; Status: hat genehmigt)
Beachten Sie bei Verwendung von virtualisierungsbasiertem Schutz der Codeintegrität oder abgeschirmten virtuellen Computern (die virtualisierungsbasierten Schutz der Codeintegrität verwenden), dass diese Technologien mit einigen Geräten und Anwendungen u. U. nicht kompatibel sind. Solche Konfigurationen sollten Sie vor der Aktivierung der Features in Produktionssystemen in Ihrem Labor testen. Andernfalls kann es zu unerwarteten Datenverlusten oder Abbruchfehlern kommen.

## <a name="microsoft-exchange"></a>Microsoft Exchange

[comment]: # (ID: 375; Übermittler: Wgries; Status: hat genehmigt)
Wenn Sie versuchen, Microsoft Exchange 2016 CU3 unter Windows Server 2016 auszuführen, treten im IIS-Hostprozess „W3WP.exe“ Fehler auf. Dieses Problem kann derzeit nicht vermieden werden. Sie sollten die Bereitstellung von Exchange 2016 CU3 unter Windows Server 2016 verschieben, bis ein Update zur Behebung dieses Problems verfügbar ist.

## <a name="remote-server-administration-tools-rsat"></a>Remoteserver-Verwaltungstools (RSAT)

[comment]: # (ID: 374; Übermittler: Ryanpu; Status: hat genehmigt)
Wenn Sie eine Version von Windows 10, die älter sind als das Anniversary-Update ausführen und Hyper-V und virtuellen Computern mit einer aktivierten virtuellen Trusted Platform Module (einschließlich geschützten virtueller Maschinen) verwenden und installieren Sie dann auf die Version der bereitgestellten Remoteserver-Verwaltungstools für Windows Server 2016 fehl Versuche, diese virtuellen Computer zu starten.

Führen Sie für den Clientcomputer ein Upgrade auf Windows 10 Anniversary Update (oder höher) durch, bevor Sie RSAT installieren, um dies zu vermeiden. Wenn dies bereits aufgetreten ist, deinstallieren Sie RSAT, führen Sie ein Upgrade für den Client auf Window 10 Anniversary Update durch, und installieren Sie RSAT anschließend erneut.

## <a name="shielded-virtual-machines"></a>Abgeschirmte VMs

[comment]: # (ID: 369; Übermittler: Nirb; Status: hat genehmigt)  
- Stellen Sie sicher, dass Sie alle verfügbaren Updates installiert haben, bevor Sie abgeschirmte virtuelle Computer in der Produktion bereitstellen.

- Beachten Sie bei Verwendung von virtualisierungsbasiertem Schutz der Codeintegrität oder abgeschirmten virtuellen Computern (die virtualisierungsbasierten Schutz der Codeintegrität verwenden), dass diese Technologien mit einigen Geräten und Anwendungen u. U. nicht kompatibel sind. Solche Konfigurationen sollten Sie vor der Aktivierung der Features in Produktionssystemen in Ihrem Labor testen. Andernfalls kann es zu unerwarteten Datenverlusten oder Abbruchfehlern kommen.

## <a name="start-menu"></a>Startmenü

[comment]: # (ID: 372; Übermittler: Samli; Status: hat genehmigt)
Dieses Problem betrifft Windows Server 2016, installiert mit der Option „Server mit Desktopdarstellung“.

Wenn Sie Anwendungen installieren, die der Verknüpfungselemente in einem Ordner hinzufügen der **starten** im Menü die Verknüpfungen funktioniert erst, nachdem Sie sich abmelden und dann erneut an erneut.

Wechseln Sie zurück zum Haupthub von [Windows Server 2016](Windows-Server-2016.md).

## <a name="storport-performance"></a>Storport-Leistung

Im Vergleich zu Windows Server 2012 R2 weisen einige Systeme möglicherweise eine verringerte Speicherleistung auf, wenn eine neue Installation von Windows Server 2016 ausgeführt wird.  Bei der Entwicklung von Windows Server 2016 wurde eine Reihe von Änderungen zur Verbesserung der Sicherheit und Zuverlässigkeit der Plattform vorgenommen. Einige Änderungen, wie die standardmäßige Aktivierung von Windows Defender, bewirken längere E/A-Pfade, wodurch die E/A-Leistung bei bestimmten Workloads und Arbeitsmustern reduziert werden kann. Microsoft empfiehlt nicht, Windows Defender deaktivieren, da es sich um eine wichtige Schutzebene für Ihre Systeme handelt.  

## <a name="copyright"></a>Copyright

Dieses Dokument wird ohne Gewähr zur Verfügung gestellt. Die in diesem Dokument enthaltenen Informationen und Ansichten, einschließlich URLs und andere Verweise auf Internetwebsites, können ohne vorherige Ankündigung geändert werden.  

Dieses Dokument stellt Ihnen keinerlei Rechte am geistigen Eigentum eines beliebigen Microsoft-Produkts zur Verfügung. Dieses Dokument darf für interne Zwecke kopiert und verwendet werden.  

&copy;2016 Microsoft Corporation. Alle Rechte vorbehalten.  

Microsoft, Active Directory, Hyper-V, Windows, und Windows Server sind entweder eingetragene Marken oder Marken der Microsoft Corporation in den USA und/oder anderen Ländern oder Regionen.  

Dieses Produkt enthält Grafikfiltersoftware; diese Software basiert zum Teil auf der Arbeit der Independent JPEG Group.  

1.0
