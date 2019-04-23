---
title: Referenzarchitektur für das Desktophosting
description: Architekturleitfaden zum Erstellen einer desktophostinglösung mit RDS und Azure.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 11/02/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1bac5dd3-8430-46ee-8bef-10cc4b7cc437
author: lizap
manager: dongill
ms.openlocfilehash: 6f235fd89c34c00601c802f4ea71e440af630169
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890241"
---
# <a name="desktop-hosting-reference-architecture"></a>Referenzarchitektur für das Desktophosting

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Artikel werden eine Sammlung von architekturbausteinen für mehrinstanzenfähig, erstellen Sie mithilfe von Remote Desktop Services (RDS) und Microsoft Azure-Computern gehostete Windows-Desktop und die Anwendung Dienste, bei denen rufen wir "desktop gehostet wird." Sie können dieser architekturverweis verwenden, äußerst sichere, skalierbare und zuverlässige desktophostinglösungen für kleine und mittelgroße Unternehmen mit 5 bis 5000 Benutzern zu erstellen.    
  
Die primäre Zielgruppe für diese Referenzarchitektur sind Hostinganbieter, die möchten, nutzen Sie Microsoft Azure Infrastructure Services zum Übermitteln von desktophostingdienste und Subscriber Access Licenses, (SALs) mit mehreren Mandanten über das [ Microsoft Service Provider Licensing Agreement](https://www.microsoft.com/hosting/en/us/licensing/splabenefits.aspx) (SPLA) Programm. End-Benutzer, die zum Erstellen und Verwalten von desktop hosting-Lösungen in Microsoft Azure Infrastructure Services für ihren eigenen Mitarbeitern verwendet werden soll, eine zweite Zielgruppe für diese Referenzarchitektur sind [RDS-Benutzer-CALs erweiterten Rechte über Software Assurance](https://download.microsoft.com/download/6/B/A/6BA3215A-C8B5-4AD1-AA8E-6C93606A4CFB/Windows_Server_2012_R2_Remote_Desktop_Services_Licensing_Datasheet.pdf) (SA).   
  
Zum Übermitteln von einem desktophosting-hosting-Lösungen die SA-Kunden und Partner, nutzen Sie die Windows Server für Windows-Benutzern eine Anwendungsoberfläche zu bieten, die Geschäftskunden und Heimanwendern vertraut ist. Erstellt auf der Grundlage von Windows 10, Windows Server 2016 bietet, vertraute Anwendungen und Benutzer auftreten.    
  
Der Umfang dieses Dokuments ist auf:   
  
* Architektonische Anleitung für einen Desktop, Dienst hostet. Ausführliche Informationen, z.B. Bereitstellungsverfahren, Leistungs- und kapazitätsplanung wird in separaten Dokumenten erläutert. Weitere allgemeine Informationen zu Azure-Infrastrukturdiensten, finden Sie unter [Microsoft Azure Virtual Machines](https://azure.microsoft.com/documentation/services/virtual-machines/).   
  
* Sitzungsbasierte Desktops, RemoteApp-Anwendungen und Server-basierten persönliche Desktops, die Windows Server 2016 Remote Desktop Session Host (RD Session Host) verwenden. Windows Client-basierten virtuellen Desktopinfrastrukturen entwickelt werden nicht behandelt werden, da es keine Service Provider License Agreement (SPLA) für Windows-Clientbetriebssysteme ist. Windows Server-basierten virtuellen Desktopinfrastrukturen entwickelt sind unter der SPLA zulässig, und Windows Client-basierten virtuellen Desktopinfrastrukturen entwickelt werden auf dedizierter Hardware mit Endkunden Lizenzen in bestimmten Szenarien zulässig. Client-basierten virtuellen Desktopinfrastrukturen entwickelt sind jedoch außerhalb des Bereichs für dieses Dokument.   
  
* Microsoft-Produkte und Funktionen, die in erster Linie für Windows Server 2016 und Microsoft Azure-Infrastrukturdiensten.   
  
* Hosten von Diensten für Mandanten, die einer Größe von 5 bis 5000 Benutzer eine Remotedesktopverbindung.   Für größere Mandanten müssen Sie möglicherweise so ändern Sie diese Architektur, um eine angemessene Leistung bereitzustellen. Der Server-Manager-RDS-grafischen Benutzeroberfläche (GUI) wird nicht für Bereitstellungen mehr als 500 Benutzern empfohlen. PowerShell wird empfohlen, für die Verwaltung von RDS-Bereitstellungen, zwischen 500 und 5000 Benutzer.   
  
* Der minimale Satz von Komponenten und Diensten für einen Desktop Hostingdienst erforderlich sind. Es gibt viele optionale Komponenten und Dienste, die hinzugefügt werden können, um einen Desktop, dem Dienst zu verbessern, aber Hierbei handelt es sich außerhalb des Bereichs für dieses Dokument.    
  
Nach der Lektüre dieses Dokuments sollte der Leser verstehen:   
- Die Bausteine, die erforderlich sind, um eine sichere, zuverlässige, mehrinstanzenfähige desktophostinglösung basierend auf Microsoft Azure-Diensten bereitstellen.  
- Der Zweck jeder Baustein und deren Zusammenwirken.  
  
Es gibt mehrere Möglichkeiten zum Erstellen einer desktophostinglösung basierend auf dieser Architektur. Diese Architektur wird die Integration und Verbesserungen in Azure mit Windows Server 2016 beschrieben. Andere Bereitstellungsoptionen stehen zur Verfügung, mit der [Desktop Referenzarchitekturhandbuch](https://go.microsoft.com/fwlink/p/?LinkId=517389) für Windows Server 2012 R2.    
  
Die folgenden Themen werden behandelt:  
- [Logische Architektur der Desktop hosten](Desktop-hosting-logical-architecture.md)  
- [Verstehen Sie die RDS-Rollen](Understanding-RDS-roles.md)
- [Verstehen der desktophosting-Umgebung](Understanding-the-desktop-hosting-environment.md)  
- [Azure-Dienste und Überlegungen zum desktophosting](Azure-services-and-considerations-for-desktop-hosting.md)
  
 


