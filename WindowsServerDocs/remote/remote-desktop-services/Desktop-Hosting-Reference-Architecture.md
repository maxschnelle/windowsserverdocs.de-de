---
title: Referenzarchitektur für das Desktophosting
description: Architekturleitfaden für die Erstellung einer Desktophostinglösung mit RDS und Azure
ms.author: elizapo
ms.date: 11/02/2016
ms.topic: article
ms.assetid: 1bac5dd3-8430-46ee-8bef-10cc4b7cc437
author: lizap
manager: dongill
ms.openlocfilehash: 7cd57a6df788ab1730332522b3682feeb398fb60
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87989736"
---
# <a name="desktop-hosting-reference-architecture"></a>Referenzarchitektur für das Desktophosting

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

In diesem Artikel wird eine Reihe von Architekturbausteinen für die Verwendung von Remotedesktopdienste (Remote Desktop Services, RDS) und Microsoft Azure Virtual Machines zur Erstellung mehrinstanzenfähiger, gehosteter Windows-Desktop- und -Anwendungsdienste definiert (sogenanntes „Desktophosting“). Diese Architekturreferenz ermöglicht die Erstellung äußerst sicherer, skalierbarer und zuverlässiger Desktophostinglösungen für kleine und mittelgroße Organisationen mit fünf bis 5.000 Benutzern.

Die primäre Zielgruppe dieser Referenzarchitektur sind Hostinganbieter, die die Microsoft Azure-Infrastrukturdienste nutzen möchten, um Desktophostingdienste und Abonnentenzugriffslizenzen (Subscriber Access Licenses, SALs) auf mehreren Mandanten über das [Microsoft SPLA-Programm](https://www.microsoft.com/hosting/en/us/licensing/splabenefits.aspx) (Service Provider Licensing Agreement) anzubieten. Eine weitere Zielgruppe dieser Referenzarchitektur sind Endkunden, die in Microsoft Azure-Infrastrukturdiensten unter Verwendung von [RDS-Benutzer-CALs mit erweiterten Rechten durch Software Assurance](https://download.microsoft.com/download/6/B/A/6BA3215A-C8B5-4AD1-AA8E-6C93606A4CFB/Windows_Server_2012_R2_Remote_Desktop_Services_Licensing_Datasheet.pdf) (SA) Desktophostinglösungen für ihre eigenen Mitarbeiter erstellen und verwalten möchten.

Zur Bereitstellung einer Desktophostinglösung nutzen Hostingpartner und SA-Kunden Windows Server, um Windows-Benutzern eine vertraute Anwendungsoberfläche zu bieten. Windows Server 2016 basiert auf Windows 10 und zeichnet sich durch gewohnte Anwendungsunterstützung und Benutzerfreundlichkeit aus.

Der Umfang dieses Dokuments ist auf Folgendes beschränkt:

* Architekturleitfaden für einen Desktophostingdienst. Details wie Bereitstellungsverfahren, Leistung und Kapazitätsplanung werden in separaten Dokumenten behandelt. Allgemeinere Informationen zu Azure-Infrastrukturdiensten findest du in der [Dokumentation zu virtuellen Computern](https://azure.microsoft.com/documentation/services/virtual-machines/).

* Sitzungsbasierte Desktops, RemoteApp-Anwendungen und serverbasierte persönliche Desktops, die den Remotedesktop-Sitzungshost (RD-Sitzungshost) von Windows Server 2016 verwenden. Windows-clientbasierte virtuelle Desktopinfrastrukturen werden hier nicht behandelt, da für Windows-Clientbetriebssysteme kein Dienstanbieter-Lizenzvertrag (Service Provider License Agreement, SPLA) zur Verfügung steht. Windows Server-basierte virtuelle Desktopinfrastrukturen sind unter dem SPLA zulässig; Windows-clientbasierte virtuelle Desktopinfrastrukturen sind in bestimmten Szenarien auf dedizierter Hardware mit Endkundenlizenzen zulässig. Clientbasierte virtuelle Desktopinfrastrukturen werden in diesem Dokument jedoch nicht behandelt.

* Produkte und Features von Microsoft, in erster Linie Windows Server 2016 und Microsoft Azure-Infrastrukturdienste.

* Desktophostingdienste für Mandanten mit fünf bis 5.000 Benutzern.   Für größere Mandanten muss diese Architektur ggf. angepasst werden, um eine angemessene Leistung zu erzielen. Die RDS-GUI (Graphical User Interface, grafische Benutzeroberfläche) von Server Manager ist für Bereitstellungen mit mehr als 500 Benutzern nicht empfehlenswert. Für die Verwaltung von RDS-Bereitstellungen mit 500 bis 5.000 Benutzern wird PowerShell empfohlen.

* Mindestens erforderliche Komponenten und Dienste für einen Desktophostingdienst. Ein Desktophostingdienst kann mit zahlreichen optionalen Komponenten und Diensten erweitert werden, diese sind jedoch nicht Gegenstand dieses Dokuments.

In diesem Dokument wird Folgendes behandelt:
- Die erforderlichen Bausteine für die Erstellung einer sicheren, zuverlässigen und mehrinstanzenfähigen Desktophostinglösung auf der Grundlage von Microsoft Azure-Diensten
- Der Zweck der einzelnen Bausteine und deren Zusammenwirken

Für die Erstellung einer auf dieser Architektur basierenden Desktophostinglösung gibt es verschiedene Möglichkeiten. Diese Architektur gibt einen Überblick über die Integration sowie über Verbesserungen in Azure mit Windows Server 2016. Weitere Bereitstellungsoptionen stehen im [Handbuch zur Referenzarchitektur für das Desktophosting](https://go.microsoft.com/fwlink/p/?LinkId=517389) für Windows Server 2012 R2 zur Verfügung.

Die folgenden Themen werden behandelt:
- [Desktophosting: Logische Architektur](Desktop-hosting-logical-architecture.md)
- [Grundlegendes zu den RDS-Rollen](./desktop-hosting-service.md)
- [Grundlegendes zur Desktophostingumgebung](Understanding-the-desktop-hosting-environment.md)
- [Azure-Dienste und Überlegungen zum Desktophosting](Azure-services-and-considerations-for-desktop-hosting.md)