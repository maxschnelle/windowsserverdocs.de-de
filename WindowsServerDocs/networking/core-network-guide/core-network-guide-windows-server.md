---
title: Netzwerk-Anleitung für Windows Server Core
description: Dieses Thema enthält eine Übersicht über das Handbuch zum Hauptnetzwerk, mit dem Sie die Kernkomponenten, die für ein voll funktionsfähiges Netzwerk erforderlich sind, und eine neue Active Directory Domäne in einer neuen Gesamtstruktur mit Windows Server 2016 planen und bereitstellen können.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.date: ''
ms.assetid: 9b3ef3eb-4246-4e0e-8bf1-53224ca5f2f9
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 52f8b9e1446b5b3f3b1e7060cc737204771d1eae
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356066"
---
# <a name="core-network-guidance-for-windows-server"></a>Netzwerk-Anleitung für Windows Server Core

>Gilt für: Windows Server, Windows Server 2016

Dieses Thema enthält eine Übersicht über die grundlegenden Netzwerk Anleitungen für Windows Server @ no__t-0 2016 und enthält die folgenden Abschnitte.  
  
-   [Einführung in das Windows Server Core-Netzwerk](#bkmk_intro)  
  
-   [Handbuch zum Hauptnetzwerk für Windows Server](#bkmk_core)  
  
## <a name="bkmk_intro"></a>Einführung in das Windows Server Core-Netzwerk

Ein Hauptnetzwerk ist eine Sammlung von Netzwerkhardware, Geräten und Software, die die grundlegenden Dienste für die Anforderungen der Informationstechnologie (IT) Ihres Unternehmens bereitstellt.

Ein Windows Server-Hauptnetzwerk bietet Ihnen zahlreiche Vorteile, wie zum Beispiel:

- Kern-Protokolle für Netzwerkkonnektivität zwischen Computern und anderen TCP/IP-kompatiblen Geräten. TCP/IP ist eine Suite von Standardprotokollen für die Verbindung von Computern und die Erstellung von Netzwerken. TCP/IP ist eine Netzwerkprotokoll Software, die mit Microsoft @ no__t-0 Windows @ no__t-1-Betriebssystemen bereitgestellt wird, die die TCP/IP-Protokoll Suite implementieren und unterstützen.

- Automatische IP-Adressierung des DHCP-Servers (Dynamic Host Configuration Protocol). Die manuelle Konfiguration von IP-Adressen auf allen Computern in Ihrem Netzwerk ist zeitaufwändig und weniger flexibel als die dynamische Bereitstellung von IP-Adressleases für Computer und andere Geräte durch einen DHCP-Server.

- DNS-Namensauflösungsdienst (Domain Name System). Mit DNS können Benutzer, Computer, Anwendungen und Dienste die IP-Adressen von Computern und Geräten im Netzwerk mithilfe des vollqualifizierten Domänennamens (Fully Qualified Domain Name, FQDN) des Computers oder Geräts finden.

- Eine Gesamtstruktur, bei der es sich um eine oder mehrere Active Directory-Domänen handelt, die gemeinsame Klassen- und Attributdefinitionen (Schema), Site- und Replikationsinformationen (Konfiguration) und gesamtstrukturweite Suchfunktionen (globaler Katalog) verwenden.

- Eine Gesamtstruktur-Stammdomäne, bei der es sich um die erste der in der neuen Gesamtstruktur erstellten Domäne handelt. Die Gruppen Organisations-Admins und Schema-Admins, bei denen es sich um gesamtstrukturweite Administratorgruppen handelt, befinden sich in der Stammdomäne der Gesamtstruktur. Darüber hinaus ist eine Stammdomäne der Gesamtstruktur wie andere Domänen eine Gruppe von Computer-, Benutzer- und Gruppenobjekten, die vom Administrator in Active Directory-Domänendiensten (Active Directory Domain Services, AD DS) definiert werden. Diese Objekte verwenden mit anderen Domänen eine gemeinsame Verzeichnisdatenbank und gemeinsame Sicherheitsrichtlinien. Sie können auch Sicherheitsbeziehungen mit anderen Domänen gemeinsam verwenden, wenn Sie beim Wachsen Ihres Unternehmens Domänen hinzufügen. Der Verzeichnisdienst speichert auch Verzeichnisdaten und gestattet autorisierten Computern, Anwendungen und Benutzern auf die Daten zuzugreifen.

- Eine Datenbank für Benutzer- und Computerkonten. Der Verzeichnisdienst stellt eine zentralisierte Benutzerkontendatenbank bereit. Diese ermöglicht die Erstellung von Benutzer- und Computerkonten für Personen und Computer, die berechtigt sind, eine Verbindung mit Ihrem Netzwerk herzustellen und auf die Netzwerkressourcen (beispielsweise Anwendungen, Datenbanken, freigegebene Dateien und Ordner sowie Drucker) zuzugreifen.

Ein Hauptnetzwerk ermöglicht außerdem eine Größenanpassung Ihres Netzwerks, wenn Ihr Unternehmen wächst und sich die IT-Anforderungen ändern. Mit einem Kern Netzwerk können Sie beispielsweise Domänen, IP-Subnetze, RAS-Dienste, drahtlose Dienste und andere Features und Server Rollen hinzufügen, die von Windows Server 2016 bereitgestellt werden.

## <a name="bkmk_core"></a>Handbuch zum Hauptnetzwerk für Windows Server

Im Windows Server 2016-Kern Netzwerk Handbuch finden Sie Anweisungen zum Planen und Bereitstellen der Kernkomponenten, die für ein voll funktionsfähiges Netzwerk und eine neue Active Directory @ no__t-0-Domäne in einer neuen Gesamtstruktur erforderlich sind. Mithilfe dieses Handbuchs können Sie Computer bereitstellen, die mit folgenden Windows-Serverkomponenten konfiguriert wurden:

- AD DS-Serverrolle (Active Directory Domain Services, Active Directory-Domänendienste)

- DNS-Serverrolle (Domain Name System)

- DHCP-Serverrolle (Dynamic Host Configuration-Protokoll)

- NPS-Rollendienst (Network Policy Server, Netzwerkrichtlinienserver) der Serverrolle Netzwerkrichtlinien- und Zugriffsdienste

- Serverrolle %%amp;quot;Webserver (IIS)%%amp;quot;

- TCP/IP v4-Verbindungen (Transmission Control Protocol/Internet Protocol Version 4) mit einzelnen Servern

Dieses Handbuch ist unter folgendem Speicherort verfügbar.

- Das [Handbuch](../core-network-guide/Core-Network-Guide.md) zum Hauptnetzwerk in der technischen Bibliothek zu Windows Server 2016.
  


