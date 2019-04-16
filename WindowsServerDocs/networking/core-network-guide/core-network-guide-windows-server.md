---
title: Netzwerkhandbuch für Windows Server
description: Dieses Thema enthält eine Übersicht über das Kernnetzwerkhandbuch, wodurch Sie zum Planen und Bereitstellen der Kernkomponenten für eine einwandfreie Verwendung des Netzwerks und eine neue Active Directory-Domäne in einer neuen Gesamtstruktur mit Windows Server2016 erforderlich
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.date: ''
ms.assetid: 9b3ef3eb-4246-4e0e-8bf1-53224ca5f2f9
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 63e4cf8c5bf56ef5131e835163a5fcb5dfd98b55
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="core-network-guide-for-windows-server"></a>Netzwerkhandbuch für Windows Server

>Gilt für: Windows Server, Windows Server 2016

Dieses Thema enthält eine Übersicht über das Core Network Guide for Windows Server&reg; 2016 und enthält die folgenden Abschnitte.  
  
-   [Einführung in die Windows Server-Hauptnetzwerk](#bkmk_intro)  
  
-   [Netzwerkhandbuch für Windows Server](#bkmk_core)  
  
## <a name="bkmk_intro"></a>Einführung in die Windows Server-Hauptnetzwerk

Ein Hauptnetzwerk ist eine Sammlung von Netzwerkhardware, Geräten und Software, die die grundlegenden Dienste für Ihre Organisation Informationstechnologie (IT) muss.

Ein Windows Server-Hauptnetzwerk bietet Ihnen zahlreiche Vorteile, z. b.

- Kern-Protokolle für Netzwerkkonnektivität zwischen Computern und anderen (TCP/IP, Transmission Control Protocol/Internet Protocol) kompatible Geräte. TCP/IP ist eine Suite von Standardprotokollen für die Verbindung von Computern und Netzwerken erstellen. TCP/IP ist eine Netzwerkprotokollsoftware, die von Microsoft bereitgestellten&reg; Windows&reg; Betriebssysteme, die implementiert und unterstützt die TCP/IP-Protokoll Suite.

- Dynamic Host Configuration Protocol (DHCP) Server automatische IP-Adressierung. Die manuelle Konfiguration von IP-Adressen auf allen Computern in Ihrem Netzwerk ist zeitaufwändig und weniger flexibel als die dynamische Bereitstellung von Computern und anderen Geräten mit IP-Adressleases vom DHCP-Server.

- Domain Name System (DNS) Name Resolution-Diensts. Mit DNS können Benutzer, Computer, Anwendungen und Dienste die IP-Adressen von Computern und Geräten im Netzwerk zu suchen, mit dem vollqualifizierten Domänennamen des Computers oder Geräts.

- Eine Gesamtstruktur, also eine oder mehrere Active Directory-Domänen, die gleichen Klassen- und Attributdefinitionen (Schema), Standort und Replikationsinformationen (Konfiguration) und gesamtstrukturweite Suchfunktionen (globaler Katalog) gemeinsam nutzen.

- Eine Gesamtstruktur-Stammdomäne, die erste Domäne wird, die in einer neuen Gesamtstruktur erstellt werden. Die Organisations-Admins und Schema-Admins-Gruppen, die gesamtstrukturweite Administratorgruppen handelt, befinden sich in der Gesamtstruktur-Stammdomäne. Darüber hinaus ist eine Gesamtstruktur-Stammdomäne, wie bei anderen Domänen eine Sammlung von Computer-, Benutzer- und Gruppenobjekten, die vom Administrator in Active Directory-Domänendienste (AD DS) definiert sind. Diese Objekte verwenden eine gemeinsame Verzeichnis Verzeichnisdatenbank und gemeinsame Sicherheitsrichtlinien. Sie können auch sicherheitsbeziehungen mit anderen Domänen freigeben, wenn Sie Domänen hinzufügen, wenn Ihre Organisation wächst. Der Verzeichnisdienst speichert Verzeichnisdaten auch und kann autorisierten Computern, Anwendungen und Benutzer auf die Daten zugreifen.

- Eine Benutzer- und Datenbank. Der Verzeichnisdienst stellt eine zentralisierte Benutzerkontendatenbank, mit dem Sie zum Erstellen von Benutzer- und Computerkonten für Personen und Computer, die autorisiert sind, eine Verbindung zu Ihrem Netzwerk und den Zugriff auf das Netzwerk Ressourcen, z.B. Anwendungen, Datenbanken, freigegebene Dateien und Ordner und Drucker.

Ein Hauptnetzwerk können Sie das Netzwerk zu skalieren, wie Ihr Unternehmen wächst und IT-Anforderungen ändern. Mit einem Hauptnetzwerk können Sie beispielsweise Domänen, IP-Subnetze, RAS-Dienste, Drahtlosdienste und andere Features und Serverrollen, die von Windows Server2016 bereitgestellten hinzufügen.

## <a name="bkmk_core"></a>Netzwerkhandbuch für Windows Server

Windows Server2016 Core Network Guide enthält Anweisungen zum Planen und Bereitstellen der Kernkomponenten für eine einwandfreie Verwendung des Netzwerks und eine neue Active Directory erforderlich&reg; Domäne in einer neuen Gesamtstruktur. Mithilfe dieses Handbuchs können Sie Computer, die mit den folgenden Windows Server-Komponenten bereitstellen:

- Die Active Directory-Domänendienste (AD DS)-Serverrolle

- Der Domain Name System (DNS)-Serverrolle

- Das Dynamic Host Configuration-Protokoll (DHCP)-Serverrolle

- Der Rollendienst Netzwerkrichtlinienserver (Network Policy Server, NPS) der Serverrolle Netzwerkrichtlinien- und Zugriffsdienste

- Die Serverrolle Webserver (IIS)

- Transmission Control Protocol/Internet Protocol Version 4 (TCP/IP) Verbindungen auf einzelnen Servern

Dieses Handbuch ist am folgenden Speicherort verfügbar.

- Die [Haupt-Netzwerkhandbuch](../core-network-guide/Core-Network-Guide.md) in der technischen Bibliothek zu Windows Server2016.
  


