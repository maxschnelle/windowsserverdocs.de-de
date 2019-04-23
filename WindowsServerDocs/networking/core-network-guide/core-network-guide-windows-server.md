---
title: Netzwerk-Anleitung für Windows Server Core
description: Dieses Thema enthält eine Übersicht über das Handbuch zum Hauptnetzwerk, wodurch Sie zum Planen und Bereitstellen der Kernkomponenten erforderlich sind, für eine voll funktionsfähige Netzwerks und eine neue Active Directory-Domäne in eine neue Gesamtstruktur mit Windows Server 2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.date: ''
ms.assetid: 9b3ef3eb-4246-4e0e-8bf1-53224ca5f2f9
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a905fd0c11237edd3a408998f8f71aa25a054328
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847901"
---
# <a name="core-network-guidance-for-windows-server"></a>Netzwerk-Anleitung für Windows Server Core

>Gilt für: Windows Server, Windows Server 2016

Dieses Thema enthält eine Übersicht über die Core-Netzwerk-Anleitung für Windows Server&reg; 2016 und enthält die folgenden Abschnitte.  
  
-   [Einführung in die Windows Server-Hauptnetzwerk](#bkmk_intro)  
  
-   [Kernnetzwerkhandbuch für WindowsServer](#bkmk_core)  
  
## <a name="bkmk_intro"></a>Einführung in die Windows Server-Hauptnetzwerk

Ein Hauptnetzwerk ist eine Sammlung von Netzwerkhardware, Geräten und Software, die die grundlegenden Dienste für die Anforderungen der Informationstechnologie (IT) Ihres Unternehmens bereitstellt.

Ein Windows Server-Hauptnetzwerk bietet Ihnen zahlreiche Vorteile, wie zum Beispiel:

- Kern-Protokolle für Netzwerkkonnektivität zwischen Computern und anderen TCP/IP-kompatiblen Geräten. TCP/IP ist eine Suite von Standardprotokollen für die Verbindung von Computern und die Erstellung von Netzwerken. TCP/IP ist eine Netzwerkprotokollsoftware, die von Microsoft bereitgestellten&reg; Windows&reg; Suite für Betriebssysteme, die implementiert und unterstützt die TCP/IP-Protokoll.

- Automatische IP-Adressierung des DHCP-Servers (Dynamic Host Configuration Protocol). Die manuelle Konfiguration von IP-Adressen auf allen Computern in Ihrem Netzwerk ist zeitaufwändig und weniger flexibel als die dynamische Bereitstellung von IP-Adressleases für Computer und andere Geräte durch einen DHCP-Server.

- DNS-Namensauflösungsdienst (Domain Name System). Mit DNS können Benutzer, Computer, Anwendungen und Dienste die IP-Adressen von Computern und Geräten im Netzwerk mithilfe des vollqualifizierten Domänennamens (Fully Qualified Domain Name, FQDN) des Computers oder Geräts finden.

- Eine Gesamtstruktur, bei der es sich um eine oder mehrere Active Directory-Domänen handelt, die gemeinsame Klassen- und Attributdefinitionen (Schema), Site- und Replikationsinformationen (Konfiguration) und gesamtstrukturweite Suchfunktionen (globaler Katalog) verwenden.

- Eine Gesamtstruktur-Stammdomäne, bei der es sich um die erste der in der neuen Gesamtstruktur erstellten Domäne handelt. Die Gruppen Organisations-Admins und Schema-Admins, bei denen es sich um gesamtstrukturweite Administratorgruppen handelt, befinden sich in der Stammdomäne der Gesamtstruktur. Darüber hinaus ist eine Stammdomäne der Gesamtstruktur wie andere Domänen eine Gruppe von Computer-, Benutzer- und Gruppenobjekten, die vom Administrator in Active Directory-Domänendiensten (Active Directory Domain Services, AD DS) definiert werden. Diese Objekte verwenden mit anderen Domänen eine gemeinsame Verzeichnisdatenbank und gemeinsame Sicherheitsrichtlinien. Sie können auch Sicherheitsbeziehungen mit anderen Domänen gemeinsam verwenden, wenn Sie beim Wachsen Ihres Unternehmens Domänen hinzufügen. Der Verzeichnisdienst speichert auch Verzeichnisdaten und gestattet autorisierten Computern, Anwendungen und Benutzern auf die Daten zuzugreifen.

- Eine Datenbank für Benutzer- und Computerkonten. Der Verzeichnisdienst stellt eine zentralisierte Benutzerkontendatenbank bereit. Diese ermöglicht die Erstellung von Benutzer- und Computerkonten für Personen und Computer, die berechtigt sind, eine Verbindung mit Ihrem Netzwerk herzustellen und auf die Netzwerkressourcen (beispielsweise Anwendungen, Datenbanken, freigegebene Dateien und Ordner sowie Drucker) zuzugreifen.

Ein Hauptnetzwerk ermöglicht außerdem eine Größenanpassung Ihres Netzwerks, wenn Ihr Unternehmen wächst und sich die IT-Anforderungen ändern. Mit einem Hauptnetzwerk können Sie beispielsweise Domänen, IP-Subnetze, RAS-Dienste, Drahtlosdienste und weitere Features und Serverrollen, die von Windows Server 2016 bereitgestellte hinzufügen.

## <a name="bkmk_core"></a>Kernnetzwerkhandbuch für WindowsServer

Windows Server 2016 Core Network Guide enthält Anweisungen zum Planen und Bereitstellen der Kernkomponenten erforderlich, die für eine voll funktionsfähige Netzwerks und einer neuen Active Directory sind&reg; Domäne in einer neuen Gesamtstruktur. Mithilfe dieses Handbuchs können Sie Computer bereitstellen, die mit folgenden Windows-Serverkomponenten konfiguriert wurden:

- AD DS-Serverrolle (Active Directory Domain Services, Active Directory-Domänendienste)

- DNS-Serverrolle (Domain Name System)

- DHCP-Serverrolle (Dynamic Host Configuration-Protokoll)

- NPS-Rollendienst (Network Policy Server, Netzwerkrichtlinienserver) der Serverrolle Netzwerkrichtlinien- und Zugriffsdienste

- Serverrolle %%amp;quot;Webserver (IIS)%%amp;quot;

- TCP/IP v4-Verbindungen (Transmission Control Protocol/Internet Protocol Version 4) mit einzelnen Servern

Dieses Handbuch ist an folgendem Speicherort verfügbar.

- Die [Core Network Guide](../core-network-guide/Core-Network-Guide.md) in der technischen Bibliothek für Windows Server 2016.
  


