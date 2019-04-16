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
ms.localizationpriority: medium
ms.openlocfilehash: 5a25a9152298a38ad77a377a87b71917ee586947
ms.sourcegitcommit: 23e0a68e21985d709e029e7771d3c52d6815bcb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/13/2018
ms.locfileid: "6507713"
---
# Anmerkungen zu dieser Version: Wichtige Probleme in Windows Server 2016

>Gilt für: Windows Server 2016

In diesen Anmerkungen zur Version sind die wichtigsten Probleme im Betriebssystem Windows Server&reg; 2016 zusammengefasst, und Sie erfahren, wie Sie diese Probleme gegebenenfalls umgehen können. Informationen zu standardmäßigen Änderungen, neuen Features und Fixes in diesem Release finden Sie unter [Neues in Windows Server 2016](what-s-new-in-windows-server-2016.md) und in den Ankündigungen der zuständigen Featureteams. Sofern es nicht anders angegeben ist, gelten alle aufgeführten Probleme für alle Editionen und Installationsoptionen von Windows Server 2016.  

Dieses Dokument wird ständig aktualisiert. Wenn kritische Probleme ermittelt werden, die eine Problemumgehung erfordern, werden diese genauso wie neue Problemumgehungen und Fixes hinzugefügt, sobald sie verfügbar sind.  

## Express-Updates verfügbar im November 2018 (neu)

Beginnend mit dem November 2018 "Update-Dienstag" aktualisieren, Windows wird erneut veröffentlichen [Express-Updates](express-updates.md) für Windows Server 2016. Wenn Sie WSUS und System Center Configuration Manager (SCCM) verwenden wieder sehen Sie zwei Pakete für die Windows Server 2016-Update: eine vollständige Aktualisierung und ein Express-Update. Wenn Sie für Ihre Server-Umgebungen Express verwenden möchten, müssen Sie bestätigen, dass der Server eine vollständige Aktualisierung seit November 2017 (KB-4048953) um sicherzustellen, dass die Express-Update ordnungsgemäß installiert getroffen hat. Wenn Sie eine Express-Update auf einem Server, die seit dem 2017 11-Update (KB-4048953) aktualisiert wurde noch nicht versuchen, sehen Sie wiederholter Fehler, die die Bandbreite und CPU-Ressourcen in einer Endlosschleife nutzen. Wenn Sie in diesem Szenario erhalten, beenden Sie die Express-Update weggeschoben und stattdessen push inzwischen eine vollständige Aktualisierung die Fehler Schleife zu beenden.  

## Server Core-Installationsoption
[comment]: # (ID: 370; Absender: Amason; Status: signiert deaktiviert)  
Wenn Sie Windows Server 2016 installieren, indem Sie die Option „Server Core-Installation“ verwenden, wird der Druckspooler installiert und standardmäßig gestartet, auch wenn die Druckserverrolle nicht installiert ist.

Legen Sie den Druckspooler nach dem ersten Start auf „Deaktiviert“ fest, um dies zu vermeiden.


## Container  

[comment]: # (ID: 371; Absender: Taylorb; Status: signiert deaktiviert)  
- Installieren Sie vor der Verwendung von Containern das [Bereitstellungsstapel-Update für Windows 10 Version 1607: 23. August 2016](https://support.microsoft.com/en-us/kb/3176936) oder spätere Updates, die verfügbar sind. Andernfalls kann eine Reihe von Problemen auftreten, einschließlich Fehlern beim Erstellen, Starten oder Ausführen von Containern, sowie Fehler ähnlich dem folgenden: „CreateProcess failed in Win32: The RPC server is unavailable“ (Fehler bei CreateProcess in Win32: Der RPC-Server ist nicht verfügbar).

[comment]: # (ID: 373; Absender: Plang; Status: signiert deaktiviert)  
- Der NanoServerPackage OneGet-Anbieter funktioniert nicht in Windows-Containern. Um dieses Problem zu umgehen, verwenden Sie Find-NanoServerPackage und Save-NanoServerPackage auf einem anderen Computer (nicht auf einem Container), um das benötigte Paket herunterzuladen. Anschließend kopieren Sie die Pakete in den Container und installieren sie.

## Device Guard
[comment]: # (ID: 369; Absender: Nirb; Status: signiert deaktiviert)
Beachten Sie bei Verwendung von virtualisierungsbasiertem Schutz der Codeintegrität oder abgeschirmten virtuellen Computern (die virtualisierungsbasierten Schutz der Codeintegrität verwenden), dass diese Technologien mit einigen Geräten und Anwendungen u.U. nicht kompatibel sind. Solche Konfigurationen sollten Sie vor der Aktivierung der Features in Produktionssystemen in Ihrem Labor testen. Andernfalls kann es zu unerwarteten Datenverlusten oder Abbruchfehlern kommen.

## Microsoft Exchange
[comment]: # (ID: 375; Absender: Wgries; Status: signiert deaktiviert)
Wenn Sie versuchen, Microsoft Exchange 2016 CU3 unter Windows Server 2016 auszuführen, treten im IIS-Hostprozess „W3WP.exe“ Fehler auf. Dieses Problem kann derzeit nicht vermieden werden. Sie sollten die Bereitstellung von Exchange 2016 CU3 unter Windows Server2016 verschieben, bis ein Update zur Behebung dieses Problems verfügbar ist.

## Remoteserver-Verwaltungstools (RSAT)
[comment]: # (ID: 374; Absender: Ryanpu; Status: signiert deaktiviert)
Wenn Sie eine Version von Windows 10 ausführen, die älter als Windows 10 Anniversary Update ist, und Hyper-V- sowie virtuelle Computer mit aktiviertem Trusted Platform Module (einschließlich abgeschirmter virtueller Computer) verwenden und anschließend die für Windows Server 2016 bereitgestellte Version von RSAT installieren, tritt bei Versuchen, diese virtuellen Computer (VMs) zu starten, ein Fehler auf.

Führen Sie für den Clientcomputer ein Upgrade auf Windows 10 Anniversary Update (oder höher) durch, bevor Sie RSAT installieren, um dies zu vermeiden. Wenn dies bereits aufgetreten ist, deinstallieren Sie RSAT, führen Sie ein Upgrade für den Client auf Windows 10 Anniversary Update durch, und installieren Sie RSAT anschließend erneut.


## Abgeschirmte virtuelle Computer
[comment]: # (ID: 369; Absender: Nirb; Status: signiert deaktiviert)  
- Stellen Sie sicher, dass Sie alle verfügbaren Updates installiert haben, bevor Sie abgeschirmte virtuelle Computer in der Produktion bereitstellen.

- Beachten Sie bei Verwendung von virtualisierungsbasiertem Schutz der Codeintegrität oder abgeschirmten virtuellen Computern (die virtualisierungsbasierten Schutz der Codeintegrität verwenden), dass diese Technologien mit einigen Geräten und Anwendungen u.U. nicht kompatibel sind. Solche Konfigurationen sollten Sie vor der Aktivierung der Features in Produktionssystemen in Ihrem Labor testen. Andernfalls kann es zu unerwarteten Datenverlusten oder Abbruchfehlern kommen.


## Startmenü
[comment]: # (ID: 372; Absender: Samli; Status: signiert deaktiviert)
Dieses Problem betrifft Windows Server 2016, installiert mit der Option „Server mit Desktopdarstellung“.

Wenn Sie Anwendungen installieren, die Verknüpfungselemente in einem Ordner im Startmenü hinzufügen, funktionieren die Verknüpfungen erst, nachdem Sie sich abgemeldet und erneut angemeldet haben.



Wechseln Sie zurück zum Haupthub von [Windows Server 2016](Windows-Server-2016.md).

## Storport-Leistung
Im Vergleich zu Windows Server 2012 R2 weisen einige Systeme möglicherweise eine verringerte Speicherleistung auf, wenn eine neue Installation von Windows Server 2016 ausgeführt wird.Bei der Entwicklung von Windows Server2016 wurde eine Reihe von Änderungen zur Verbesserung der Sicherheit und Zuverlässigkeit der Plattform vorgenommen. Einige Änderungen, wie die standardmäßige Aktivierung von Windows Defender, bewirken längere E/A-Pfade, wodurch die E/A-Leistung bei bestimmten Workloads und Arbeitsmustern reduziert werden kann. Microsoft empfiehlt nicht, Windows Defender deaktivieren, da es sich um eine wichtige Schutzebene für Ihre Systeme handelt.  

## Copyright  
Dieses Dokument wird ohne Gewähr zur Verfügung gestellt. Die in diesem Dokument enthaltenen Informationen und Ansichten, einschließlich URLs und andere Verweise auf Internetwebsites, können ohne vorherige Ankündigung geändert werden.  

Dieses Dokument stellt Ihnen keinerlei Rechte am geistigen Eigentum eines beliebigen Microsoft-Produkts zur Verfügung. Dieses Dokument darf für interne Referenzzwecke kopiert und verwendet werden.  

&copy;2016 Microsoft Corporation. Alle Rechte vorbehalten.  

Microsoft, Active Directory, Hyper-V, Windows, und Windows Server sind entweder eingetragene Marken oder Marken der MicrosoftCorporation in den USA und/oder anderen Ländern oder Regionen.  

Dieses Produkt enthält Grafikfiltersoftware; diese Software basiert zum Teil auf der Arbeit der Independent JPEG Group.  


1.0  
