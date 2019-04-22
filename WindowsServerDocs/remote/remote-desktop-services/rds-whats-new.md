---
title: Neuigkeiten in Remote Desktop Services
description: Enthält eine Beschreibung der neuen Features von RDS in Windows Server 2016.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: chrimo
ms.date: 10/11/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 04d52dff-e61b-4633-9908-be8600abc2ba
author: ChristianMontoya
manager: scottman
ms.openlocfilehash: ad13fdce251c1f84bac725e9f1ee266c6aae5e13
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816311"
---
# <a name="whats-new-in-remote-desktop-services"></a>Neuigkeiten in Remote Desktop Services

Remote Desktop Services (RDS) basiert auf Windows Server 2016 ist eine Virtualisierungsplattform, die eine Vielzahl von Kundenszenarien aktivieren. Verbesserungen in der gesamten RDS-Lösung umfasst das Pensum dem Remotedesktop-Team und anderen Partnern Technologie bei Microsoft. Die folgenden Szenarios und Technologien sind neu oder wurden in Windows Server 2016 verbessert.

Achten Sie auch darauf unserer Sitzung von der Ignite 2016 ausprobieren: [Nutzen von RDS-Verbesserungen in Windows Server 2016](https://channel9.msdn.com/Events/Ignite/2016/BRK3098). In diesem Video werden das Produktteam für alle neuen und verbesserten Features in Remote Desktop Services, einschließlich der Unterstützung für vGPU. 

## <a name="app-compatibility---windows-server-2016-and-windows-10"></a>Anwendungskompatibilität – WindowsServer 2016 und Windows 10
Basiert auf derselben Grundlage von Windows 10 und hat Windows Server 2016 nicht nur die gleiche Aussehen und Verhalten, das Sie erwarten, dass aus einem Desktop, jedoch können auch viele der gleichen Anwendungen ausführen. Kopplung von Windows Server 2016 mit den Grafikfunktionen (siehe unten) erhalten Sie eine Umgebung für alle Benutzer, um produktiv zu sein. 

## <a name="azure-sql-database---the-new-database-for-your-highly-available-environment"></a>Azure SQL-Datenbank – die neue Datenbank für Ihre hoch verfügbare Umgebung
Der Remotedesktop-Verbindungsbroker kann alle der Informationen (z. B. Verbindungsstatus und Benutzer/Host-Zuordnungen) in einer freigegebenen SQL-Datenbank, z. B. Azure SQL-Datenbank zu speichern. Ganzen Sie der SQL Server AlwaysOn-Verfügbarkeitsgruppe Bereitstellung manuell den, ziehen Sie die Verbindungszeichenfolge für Azure SQL-Datenbank, und starten Sie die unter Verwendung der hoch verfügbaren Umgebung.

Weitere Informationen: [Verwenden von Azure SQL-Datenbank für Ihre Remotedesktop-Verbindungsbroker-Umgebung hohe Verfügbarkeit](https://blogs.technet.microsoft.com/enterprisemobility/2016/05/03/new-windows-server-2016-capability-use-azure-sql-db-for-your-remote-desktop-connection-broker-high-availability-environment/)

## <a name="graphics---solving-graphics-needs-across-various-scenarios"></a>Grafik - Graphics-Anforderungen für verschiedene Szenarien lösen
Dank der Hyper-V diskrete Gerätezuordnung können Sie jetzt die GPUs auf einem Hostcomputer direkt an einen virtuellen Computer zur Nutzung durch ihre Anwendungen, die GPU-erfordern zuordnen. In RemoteFX vGPU, einschließlich der Unterstützung für die OpenGL 4.4, OpenCL 1.1, 4 k-Auflösung und Windows Server-Computer wurden ebenfalls Verbesserungen vorgenommen.

Weitere Informationen: [Diskrete Gerätezuordnung](https://blogs.technet.microsoft.com/virtualization/2015/11/)

## <a name="rd-connection-broker---improved-connection-handling-during-logon-storms"></a>Remotedesktop-Verbindungsbroker - verbesserte Verbindung, die während der Anmeldung "Stürme" bieten behandeln
Mit verbesserte Behandlung ist der Remotedesktop-Verbindungsbroker jetzt mehr als 10.000 gleichzeitige anmeldeanforderungen, manchmal angezeigt, während "Anmeldung"Stürme "bieten" verarbeiten können. Die verbesserte RD Connection Broker macht auch die Wartung der Bereitstellung, da Sie mehrere kann einfacher Server schnell wieder in der Umgebung hinzufügen.

Weitere Informationen: [Verbesserte Leistung für Remote Desktop Connection Broker](https://blogs.technet.microsoft.com/enterprisemobility/2015/12/15/improved-remote-desktop-connection-broker-performance-with-windows-server-2016-and-windows-server-2012-r2-hotfix-kb3091411/)

## <a name="rdp-10---new-capabilities-built-into-the-protocol"></a>RDP 10 – neue Funktionen für das Protokoll
RDP-10 verwendet jetzt den Codec 264/AVC-444 für sowohl Video als auch Text entsprechend optimieren. In dieser Version wird die Pen-Remoting ebenfalls unterstützt. Mit diesen Funktionen werden Ihre remote-Sitzungen, können Sie sogar noch mehr, wie eine lokale Sitzung starten.  

Weitere Informationen: [RDP 10 AVC/H.264-Verbesserungen in Windows 10 und Windows Server 2016](https://blogs.technet.microsoft.com/enterprisemobility/2016/01/11/remote-desktop-protocol-rdp-10-avch-264-improvements-in-windows-10-and-windows-server-2016-technical-preview/)

## <a name="personal-session-desktops---providing-individual-desktops-to-any-end-user"></a>Persönliche sitzungsdesktops – Bereitstellen von einzelnen Desktops zu durch Endbenutzer
Persönliche sitzungsdesktops ist eine neue Möglichkeit, Ihre eigenen persönlichen Desktop, die für Sie in der Cloud gehostet wird. Administratorrechte und dedizierten Sitzung Hosts entfernt ist die Komplexität von Hostingumgebungen, in dem Benutzer den Desktop, wie sie verwalten möchten, ihre eigenen.

Weitere Informationen: [Persönliche Sitzungsdesktops](rds-personal-session-desktops.md)
