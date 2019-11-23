---
title: Kernkomponenten
description: Dieses Handbuch enthält Anweisungen zum Planen und Bereitstellen der Kernkomponenten, die für ein voll funktionsfähiges Netzwerk und eine neue Active Directory Domäne in einer neuen Gesamtstruktur mit Windows Server 2016 erforderlich sind.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: b3cd60f7-d380-4712-9a78-0a8f551e1121
ms.author: pashort
author: shortpatti
ms.openlocfilehash: cae789974c3f2b4f83c9120558d77dbe27f4190a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356414"
---
# <a name="core-network-components"></a>Kernkomponenten

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Dieses Handbuch enthält Anweisungen zum Planen und Bereitstellen der Kernkomponenten, die für ein voll funktionsfähiges Netzwerk und eine neue Active Directory Domäne in einer neuen Gesamtstruktur erforderlich sind.

> [!NOTE]
> Dieses Handbuch kann im Microsoft Word-Format aus der TechNet Gallery heruntergeladen werden. Weitere Informationen finden Sie im [Handbuch zum Hauptnetzwerk für Windows Server 2016](https://gallery.technet.microsoft.com/Core-Network-Guide-for-9da2e683).

Dieses Handbuch enthält die folgenden Abschnitte:

- [Informationen zur Anleitung](#BKMK_about)

- [Übersicht über das Kern Netzwerk](#BKMK_overview)

- [Zentrale Netzwerkplanung](#BKMK_planning)

- [Kern Netzwerk Bereitstellung](#BKMK_deployment)

- [Weitere technische Ressourcen](#BKMK_resources)

- [Fügt A durch E ein.](#BKMK_appendix)

## <a name="BKMK_about"></a>Informationen zu diesem Leitfaden
Dieses Handbuch ist für Netzwerk- und Systemadministratoren konzipiert, die ein neues Netzwerk installieren, oder die ein domänenbasiertes Netzwerk erstellen möchten, das ein aus Arbeitsgruppen bestehendes Netzwerk ersetzen soll. Das in diesem Handbuch erläuterte Bereitstellungsszenario ist vor allem hilfreich, wenn Sie bereits absehen können, dass Ihrem Netzwerk zukünftig weitere Dienste und Features hinzugefügt werden müssen.

Es wird empfohlen, Entwurfs- und Bereitstellungsanleitungen für jede der in diesem Bereitstellungsszenario verwendete Technologie zu lesen, um Hilfestellungen bei der Entscheidung zu erhalten, ob dieses Handbuch die benötigten Dienste und Konfigurationen erläutert.

Ein Hauptnetzwerk ist eine Sammlung von Netzwerkhardware, Geräten und Software, die die grundlegenden Dienste für die Anforderungen der Informationstechnologie (IT) Ihres Unternehmens bereitstellt.

Ein Windows Server-Hauptnetzwerk bietet Ihnen zahlreiche Vorteile, wie zum Beispiel:

-   Kern-Protokolle für Netzwerkkonnektivität zwischen Computern und anderen TCP/IP-kompatiblen Geräten. TCP/IP ist eine Suite von Standardprotokollen für die Verbindung von Computern und die Erstellung von Netzwerken. TCP/IP ist eine Netzwerkprotokoll Software, die mit Microsoft Windows-Betriebssystemen bereitgestellt wird, die die TCP/IP-Protokoll Suite implementieren und unterstützen.

-   Automatische Zuweisung von IP-Adressen mithilfe von DHCP (Dynamic Host Configuration Protocol) zu Computern und anderen Geräten, die als DHCP-Clients konfiguriert wurden. Die manuelle Konfiguration von IP-Adressen auf allen Computern in Ihrem Netzwerk ist zeitaufwändig und weniger flexibel als die dynamische Bereitstellung von IP-Adresskonfigurationen für Computer und andere Geräte durch einen DHCP-Server.

-   DNS-Namensauflösungsdienst (Domain Name System). Mit DNS können Benutzer, Computer, Anwendungen und Dienste die IP-Adressen von Computern und Geräten im Netzwerk mithilfe des vollqualifizierten Domänennamens (Fully Qualified Domain Name, FQDN) des Computers oder Geräts finden.

-   Eine Gesamtstruktur, bei der es sich um eine oder mehrere Active Directory-Domänen handelt, die gemeinsame Klassen- und Attributdefinitionen (Schema), Site- und Replikationsinformationen (Konfiguration) und gesamtstrukturweite Suchfunktionen (globaler Katalog) verwenden.

-   Eine Gesamtstruktur-Stammdomäne, bei der es sich um die erste der in der neuen Gesamtstruktur erstellten Domäne handelt. Die Gruppen Organisations-Admins und Schema-Admins, bei denen es sich um gesamtstrukturweite Administratorgruppen handelt, befinden sich in der Stammdomäne der Gesamtstruktur. Darüber hinaus ist eine Stammdomäne der Gesamtstruktur wie andere Domänen eine Gruppe von Computer-, Benutzer- und Gruppenobjekten, die vom Administrator in Active Directory-Domänendiensten (Active Directory Domain Services, AD DS) definiert werden. Diese Objekte verwenden mit anderen Domänen eine gemeinsame Verzeichnisdatenbank und gemeinsame Sicherheitsrichtlinien. Sie können auch Sicherheitsbeziehungen mit anderen Domänen gemeinsam verwenden, wenn Sie beim Wachsen Ihres Unternehmens Domänen hinzufügen. Der Verzeichnisdienst speichert auch Verzeichnisdaten und gestattet autorisierten Computern, Anwendungen und Benutzern auf die Daten zuzugreifen.

-   Eine Datenbank für Benutzer- und Computerkonten. Der Verzeichnisdienst stellt eine zentralisierte Benutzerkontendatenbank bereit. Diese ermöglicht die Erstellung von Benutzer- und Computerkonten für Personen und Computer, die berechtigt sind, eine Verbindung mit Ihrem Netzwerk herzustellen und auf die Netzwerkressourcen (beispielsweise Anwendungen, Datenbanken, freigegebene Dateien und Ordner sowie Drucker) zuzugreifen.

Ein Hauptnetzwerk ermöglicht außerdem eine Größenanpassung Ihres Netzwerks, wenn Ihr Unternehmen wächst und sich die IT-Anforderungen ändern. Mit einem Kern Netzwerk können Sie beispielsweise Domänen, IP-Subnetze, RAS-Dienste, drahtlose Dienste und andere Features und Server Rollen hinzufügen, die von Windows Server 2016 bereitgestellt werden.

### <a name="network-hardware-requirements"></a>Anforderungen an die Netzwerkhardware
Damit Sie erfolgreich ein Hauptnetzwerk bereitstellen können, müssen Sie unter anderem folgende Netzwerkhardware bereitstellen:

-   Kabelgestütztes Ethernet-, Fast Ethernet- oder Gigabyte Ethernet

-   Einen Hub, einen Schicht 2- oder Schicht 3-Switch oder ein anderes Gerät, das Netzwerkdatenverkehr zwischen Computern und Geräten weiterleitet.

-   Computer die den Mindesthardwareanforderungen für die jeweiligen Client- und Serverbetriebssysteme entsprechen.

## <a name="what-this-guide-does-not-provide"></a>Nicht in diesem Handbuch enthaltene Informationen
Dieses Handbuch enthält keine Anleitungen für folgende Bereitstellungen:

-   Netzwerkhardware wie Kabel, Router, Switches und Hubs

-   Zusätzliche Netzwerkressourcen wie Drucker und Dateiserver

-   Internetkonnektivität

-   Remotezugriff

-   Drahtloser Zugriff

-   Bereitstellung von Clientcomputern

> [!NOTE]
> Computer mit Windows-Client Betriebssystemen werden standardmäßig für den Empfang von IP-Adressleases vom DHCP-Server konfiguriert. Daher ist keine weitere DHCP- oder IPv4-Konfiguration (Internetprotokoll, Version 4) für Clientcomputer erforderlich.

## <a name="technology-overviews"></a>Technologieübersicht
Die folgenden Abschnitte bieten eine kurze Übersicht über die erforderlichen Technologien, die für die Erstellung eines Hauptnetzwerks bereitgestellt werden.

### <a name="active-directory-domain-services"></a>Active Directory Domain Services
Ein Verzeichnis ist eine hierarchische Struktur zum Speichern von Informationen zu Objekten im Netzwerk, wie Benutzer und Computer. Ein Verzeichnisdienst, wie z. b. AD DS, stellt die Methoden zum Speichern von Verzeichnis Daten und zum Bereitstellen dieser Daten für Netzwerk Benutzer und Administratoren bereit. AD DS speichert beispielsweise Informationen über Benutzerkonten, einschließlich Namen, e-Mail-Adressen, Kenn Wörter und Telefonnummern, und ermöglicht anderen autorisierten Benutzern im gleichen Netzwerk den Zugriff auf diese Informationen.

### <a name="dns"></a>DNS
DNS ist ein Namensauflösungsprotokoll für TCP/IP-Netzwerke, z. B. für das Internet oder ein Unternehmensnetzwerk. Ein DNS-Server dient als Host für Informationen, die es Clientcomputern und Diensten ermöglichen, leicht erkennbare, alphanumerische DNS-Namen in die IP-Adressen aufzulösen, die von den Computern zur Kommunikation untereinander verwendet werden.

### <a name="dhcp"></a>DHCP
DHCP ist ein IP-Standard für die Vereinfachung der Verwaltung der Host-IP-Konfiguration. Der DHCP-Standard ermöglicht DHCP-Servern die Verwaltung der dynamischen Zuweisung von IP-Adressen und sonstiger zugehöriger Konfigurationsdetails für DHCP-fähige Clients im Netzwerk.

DHCP ermöglicht die Verwendung eines DHCP-Servers für die dynamische Zuweisung einer IP-Adresse zu einem Computer oder einem anderen Gerät wie etwa zu einem Drucker im lokalen Netzwerk. Jeder Computer in einem TCP/IP-Netzwerk muss über eine eindeutige IP-Adresse verfügen. Zudem muss die zugehörige Subnetzmaske sowohl den Hostcomputer als auch das Subnetz angeben, an das der Computer angeschlossen ist. Durch die Verwendung von DHCP können Sie sicherstellen, dass alle als DHCP-Clients konfigurierten Computer eine für die Netzwerkadresse und das Subnetz geeignete IP-Adresse erhalten. Und durch die Verwendung von DHCP-Optionen wie Standardgateway und DNS-Server können Sie DHCP-Clients automatisch die Informationen bereitstellen, die diese benötigen, um in Ihrem Netzwerk ordnungsgemäß zu funktionieren.

In TCP/IP-basierten Netzwerken verringert DHCP die Komplexität und den Umfang von Verwaltungsaufgaben bei der Neukonfiguration von Computern.

### <a name="tcpip"></a>TCP/IP
TCP/IP in Windows Server 2016 lautet wie folgt:

-   Eine Netzwerksoftware auf der Grundlage von Netzwerkprotokollen, die dem Industriestandard entsprechen.

-   Ein routingfähiges Unternehmensnetzwerkprotokoll, das die Verbindung Ihres Windows-Computers sowohl mit LAN- als auch mit WAN-Umgebungen unterstützt.

-   Kerntechnologien und Hilfsprogramme für die Verbindung Ihres Windows-Computers mit anderen Systemen zum Austausch von Daten.

-   Eine Grundlage für den Zugriff auf globale Internetdienste wie WWW- und FTP-Server.

-   Ein zuverlässiges, skalierbares und plattformübergreifendes Client-/Server-Framework

TCP/IP stellt grundlegende TCP/IP-Hilfsprogramme bereit, mit deren Hilfe Windows-Computer Verbindungen mit anderen Microsoft- und Nicht-Microsoft-Systemen herstellen und Informationen austauschen können, beispielsweise:

-    Windows Server 2016

-   Windows 10

-    Windows Server 2012 R2

-   Windows 8.1

-    Windows Server 2012

-   Windows 8

-    Windows Server 2008 R2

-    Windows 7

-    WindowsServer 2008

-   Windows Vista

-   Internethosts

-   Apple Macintosh-Systeme

-   IBM-Mainframes

-   UNIX-und Linux-Systeme

-   Open VMS-Systeme

-   Netzwerk bereite Drucker

-   Tablets und Mobiltelefone mit kabelgebundener Ethernet-oder drahtlos 802,11-Technologie

## <a name="BKMK_overview"></a>Übersicht über das Kern Netzwerk
Die folgende Illustration veranschaulicht die Topologie des Windows Server-Hauptnetzwerks.

![Windows Server Core-Netzwerktopologie](../media/Core-Network-Guide/cng16_overview.jpg)

> [!NOTE]
> In diesem Handbuch finden Sie zudem Anweisungen zum Hinzufügen von optionalen Netzwerkrichtlinienservern (Network Policy Server, NPS) und Webservern (IIS) zur Netzwerktopologie als Grundlage für sichere Netzwerkzugriffslösungen wie verkabelte oder kabellose 802.1X-Bereitstellungen, die Sie mithilfe der Begleithandbücher zum Hauptnetzwerk implementieren können. Weitere Informationen finden Sie unter [Bereitstellen von optionalen Features für die Netzwerkzugriffsauthentifizierung und Webdienste](#BKMK_optionalfeatures).

### <a name="core-network-components"></a>Komponenten des Hauptnetzwerks
Das Hauptnetzwerk umfasst die folgenden Komponenten:

##### <a name="router"></a>Router
Dieses Bereitstellungshandbuch enthält Anleitungen für die Bereitstellung eines Hauptnetzwerks mit zwei Subnetzen, die von einem Router mit aktivierter DHCP-Weiterleitung getrennt werden. Sie können jedoch in Abhängigkeit von Ihren Anforderungen und Ressourcen auch einen Schicht 2-Switch, einen Schicht 3-Switch oder einen Hub bereitstellen. Wenn Sie einen Switch bereitstellen, muss dieser zu DHCP-Weiterleitung in der Lage sein, und Sie müssen jedem Subnetz einen DHCP-Server hinzufügen. Wenn Sie einen Hub bereitstellen, stellen Sie ein einzelnes Subnetz bereit und benötigen keine DHCP-Weiterleitung oder einen zweiten Bereich auf Ihrem DHCP-Server.

##### <a name="static-tcpip-configurations"></a>Konfiguration von statischem TCP/IP
Die Server in dieser Bereitstellung sind mit statischen IPv4-Adressen konfiguriert. Clientcomputer werden standardmäßig für den Empfang von IP-Adressleases vom DHCP-Server konfiguriert.

##### <a name="active-directory-domain-services-global-catalog-and-dns-server-dc1"></a>Globaler Katalog der Active Directory-Domänendienste und DNS-Server DC1
Sowohl Active Directory Domain Services (AD DS) als auch Domain Name System (DNS) werden auf diesem Server mit dem Namen DC1 installiert, der für alle Computer und Geräte im Netzwerk Verzeichnis-und Namensauflösungsdienste bereitstellt.

##### <a name="dhcp-server-dhcp1"></a>DHCP-Server DHCP1
Der DHCP-Server (mit dem Namen DHCP1) wird mit einem Bereich konfiguriert, der IP-Adressleases für Computer im lokalen Subnetz bereitstellt. Der DHCP-Server kann auch mit zusätzlichen Bereichen konfiguriert werden, um IP-Adressleases für Computer in anderen Subnetzen bereitzustellen, wenn die DHCP-Weiterleitung auf Routern konfiguriert ist.

##### <a name="client-computers"></a>Clientcomputer
Computer mit Windows-Client Betriebssystemen werden standardmäßig als DHCP-Clients konfiguriert, die IP-Adressen und DHCP-Optionen automatisch vom DHCP-Server abrufen.

## <a name="BKMK_planning"></a>Zentrale Netzwerkplanung
Bevor Sie ein Hauptnetzwerk bereitstellen, müssen Sie die folgenden Aufgaben ausführen:

-   [Planen von Subnetzen](#bkmk_NetFndtn_Pln_Subnt)

-   [Planen der grundlegenden Konfiguration aller Server](#bkmk_NetFndtn_Pln_AllSrvrs)

-   [Planen der Bereitstellung von DC1](#bkmk_NetFndtn_Pln_AD-DNS-01)

-   [Planen des Domänen Zugriffs](#bkmk_NetFndtn_Pln_DomAccess)

-   [Planen der Bereitstellung von DHCP1](#bkmk_NetFndtn_Pln_DHCP-01)

Die folgenden Abschnitte enthalten weitere Details zu jedem dieser Themen.

> [!NOTE]
> Unterstützung bei der Planung der-Bereitstellung finden Sie auch im [Anhang E-Core-Vorbereitungs Blatt für die Netzwerkplanung](#BKMK_E).

### <a name="bkmk_NetFndtn_Pln_Subnt"></a>Planen von Subnetzen
In TCP/IP-Netzwerken werden Router verwendet, um Hardware und Software zu verbinden, die auf verschiedenen physischen Netzwerksegmenten, Subnetze genannt, verwendet werden. Router werden auch verwendet, um IP-Pakete zwischen den einzelnen Subnetzen weiterzuleiten. Ermitteln Sie das physische Layout Ihres Netzwerks, einschließlich der Anzahl der benötigten Router und Subnetze, bevor Sie mit den Anleitungen in diesem Handbuch fortfahren.

Damit Sie die Server in Ihrem Netzwerk mit statischen IP-Adressen konfigurieren können, müssen Sie darüber hinaus den IP-Adressbereich festlegen, den Sie für das Subnetz verwenden möchten, in dem sich die Server Ihres Hauptnetzwerks befinden. In diesem Handbuch werden die privaten IP-Adressbereiche 10.0.0.1-10.0.0.254 und 10.0.1.1-10.0.1.254 als Beispiele verwendet, Sie können jedoch jeden bevorzugten privaten IP-Adressbereich verwenden.

> [!IMPORTANT]
> Nachdem Sie die IP-Adressbereiche ausgewählt haben, die Sie für die einzelnen Subnetze verwenden möchten, konfigurieren Sie Ihre Router mit einer IP-Adresse aus dem IP-Adressbereich, der in dem Subnetz verwendet wird, in dem der Router installiert ist. Wenn Ihr Router beispielsweise standardmäßig mit der IP-Adresse 192.168.1.1 konfiguriert wird, Sie den Router jedoch in einem Subnetz mit dem IP-Adressbereich 10.0.0.0/24 installieren, müssen Sie den Router neu konfigurieren, sodass er eine IP-Adresse aus dem IP-Adressbereich 10.0.0.0/24 verwendet.

Die folgenden erkannten privaten IP-Adressbereiche werden von Internetkommentaranforderungen (Request for Comments, RFC) 1918 festgelegt:

-   10.0.0.0-10.255.255.255

-   172.16.0.0-172.31.255.255

-   192.168.0.0-192.168.255.255

Wenn Sie die in RFC 1918 festgelegten privaten IP-Adressbereiche verwenden, können Sie keine direkte Verbindung mit dem Internet unter Verwendung einer privaten IP-Adresse herstellen, da Anforderungen an diese Adressen oder von diesen Adressen automatisch von den Routern der Internetdienstanbieter zurückgewiesen werden. Um zu einem späteren Zeitpunkt eine Internetverbindung zu Ihrem Hauptnetzwerk herzustellen, müssen Sie einen Vertrag mit einem Internetdienstanbieter abschließen, um eine öffentliche IP-Adresse zu erhalten.

> [!IMPORTANT]
> Wenn Sie private IP-Adressen verwenden, müssen Sie einen Proxy- oder NAT-Server (Network Address Translation, Netzwerkadressübersetzung) verwenden, um die privaten IP-Adressbereiche in Ihrem lokalen Netzwerk in eine öffentliche IP-Adresse zu konvertieren, die im Internet weitergeleitet werden kann. Die meisten Router bieten NAT-Dienste. Es sollte daher nicht schwierig sein, einen NAT-fähigen Router zu finden.

Weitere Informationen finden Sie unter [Planen der Bereitstellung von DHCP1](#bkmk_NetFndtn_Pln_DHCP-01).

### <a name="bkmk_NetFndtn_Pln_AllSrvrs"></a>Planen der grundlegenden Konfiguration aller Server
Für jeden Server im Hauptnetzwerk müssen Sie den Computer umbenennen und eine statische IPv4-Adresse sowie andere TCP/IP-Eigenschaften für den Computer zuweisen und konfigurieren.

#### <a name="planning-naming-conventions-for-computers-and-devices"></a>Planen von Namenskonventionen für Computer und Geräte
Aus Konsistenzgründen sollten Sie in Ihrem Netzwerk konsistente Namen für Server, Drucker und sonstige Geräte verwenden. Computernamen können verwendet werden, damit Benutzer und Administratoren den Zweck und den Standort eines Servers, Druckers oder sonstigen Geräts einfacher feststellen können. Wenn Sie z. b. über drei DNS-Server verfügen, eine in San Francisco, eine in Los Angeles und eine in Chicago, können Sie die Benennungs Konvention- *Server Funktion*-*Location*-*Number*verwenden:

-   DNS-DEN-01. Dieser Name steht für den DNS-Server in Denver, Colorado. Wenn in Denver weitere DNS-Server hinzukommen, kann der numerische Wert des Namens erhöht werden, beispielsweise DNS-DEN-02 und DNS-DEN-03.

-   DNS-SPAS-01. Dieser Name steht für den DNS-Server in South Pasadena, Kalifornien.

-   DNS-ORL-01. Dieser Name steht für den DNS-Server in Orlando, Florida.

Die in diesem Handbuch verwendete Benennungskonvention für Server ist sehr einfach: Der Name setzt sich aus der primären Serverfunktion und einer Nummer zusammen. Der Domänencontroller heißt beispielsweise DC1 und der DHCP-Server DHCP1.

Es wird empfohlen, vor der Installation des Hauptnetzwerks mithilfe dieses Handbuchs eine Benennungskonvention auszuwählen.

#### <a name="planning-static-ip-addresses"></a>Planen von statischen IP-Adressen
Bevor Sie jeden Computer mit einer statischen IP-Adresse konfigurieren, müssen Sie Ihre Subnetz- und IP-Adressbereiche planen. Darüber hinaus müssen Sie die IP-Adressen Ihrer DNS-Server festlegen. Wenn Sie einen Router installieren möchten, der Zugriff auf andere Netzwerke wie weitere Subnetze oder das Internet bereitstellt, müssen Sie für die Konfiguration der statischen IP-Adresse die IP-Adresse des Routers kennen, diese wird auch als Standardgateway bezeichnet.

Die folgende Tabelle enthält Beispielwerte für die Konfiguration einer statischen IP-Adresse.

|Konfigurationselemente|Beispielwerte|
|-----------------------|------------------|
|IP-Adresse|10.0.0.2|
|Subnetzmaske|255.255.255.0|
|Standardgateway (IP-Adresse des Routers)|10.0.0.1|
|Bevorzugter DNS-Server|10.0.0.2|

> [!NOTE]
> Wenn Sie mehrere DNS-Server bereitstellen möchten, können Sie auch die IP-Adresse des alternativen DNS-Servers planen.

### <a name="bkmk_NetFndtn_Pln_AD-DNS-01"></a>Planen der Bereitstellung von DC1
Im folgenden finden Sie die wichtigsten Planungsschritte vor der Installation von Active Directory Domain Services (AD DS) und DNS auf DC1.

#### <a name="planning-the-name-of-the-forest-root-domain"></a>Planen des Namens der Stammdomäne der Gesamtstruktur
Der erste Schritt im AD DS Entwurfsprozess besteht darin, die Anzahl der Gesamtstrukturen zu ermitteln, die in Ihrer Organisation erforderlich sind. Eine Gesamtstruktur ist der AD DS Container der obersten Ebene und besteht aus einer oder mehreren Domänen, die über ein gemeinsames Schema und einen globalen Katalog verfügen. Ein Unternehmen kann mehrere Gesamtstrukturen besitzen. Für die meisten Unternehmen ist eine einzelne Gesamtstruktur jedoch vorzuziehen und am einfachsten zu verwalten.

Wenn Sie in ihrem Unternehmen den ersten Domänencontroller erstellen, erstellen Sie die erste Domäne (auch als Stammdomäne der Gesamtstruktur bezeichnet) und die erste Gesamtstruktur. Bevor Sie jedoch diesen Schritt mithilfe dieser Anleitungen ausführen, müssen Sie den geeignetsten Domänennamen für Ihr Unternehmen ermitteln. In den meisten Fällen wird der Name des Unternehmens als Domänenname verwendet, und meistens ist dieser Domänenname registriert. Wenn Sie externe internetbasierte Webserver bereitstellen möchten, um Ihren Kunden oder Partnern Informationen und Dienste bereitzustellen, wählen Sie einen Domänennamen aus, der nicht bereits verwendet wird, und registrieren Sie den Domänennamen, sodass Ihr Unternehmen diesen Namen besitzt.

#### <a name="planning-the-forest-functional-level"></a>Planen der Gesamtstrukturfunktionsebene
Beim Installieren von AD DS müssen Sie die Gesamtstruktur Funktionsebene auswählen, die Sie verwenden möchten. Die Domänen-und Gesamtstruktur Funktionalität, die in Windows Server 2003 Active Directory eingeführt wurde, bietet eine Möglichkeit zum Aktivieren von Domänen-oder Gesamtstruktur weiten Active Directory Features in Ihrer Netzwerkumgebung. Je nach Netzwerkumgebung sind verschiedene Ebenen der Domänen- und Gesamtstrukturfunktionalität verfügbar.

Mit der Gesamtstrukturfunktionalität werden Features für alle Domänen in der Gesamtstruktur aktiviert. Die folgenden Gesamtstrukturfunktionsebenen sind verfügbar:

-    Windows Server 2008. Diese Gesamtstruktur Funktionsebene unterstützt nur Domänen Controller, auf denen Windows Server 2008 und höhere Versionen des Windows Server-Betriebssystems ausgeführt werden.

-    Windows Server 2008 R2. Diese Gesamtstruktur Funktionsebene unterstützt Windows Server 2008 R2-Domänen Controller und Domänen Controller, auf denen spätere Versionen des Windows Server-Betriebssystems ausgeführt werden.

-    Windows Server 2012. Diese Gesamtstruktur Funktionsebene unterstützt Windows Server 2012-Domänen Controller und Domänen Controller, auf denen spätere Versionen des Windows Server-Betriebssystems ausgeführt werden.

-    Windows Server 2012 R2. Diese Gesamtstruktur Funktionsebene unterstützt Windows Server 2012 R2-Domänen Controller und Domänen Controller, auf denen spätere Versionen des Windows Server-Betriebssystems ausgeführt werden.

-    Windows Server 2016. Diese Gesamtstruktur Funktionsebene unterstützt nur Windows Server 2016-Domänen Controller und Domänen Controller, auf denen spätere Versionen des Windows Server-Betriebssystems ausgeführt werden.

Wenn Sie eine neue Domäne in einer neuen Gesamtstruktur bereitstellen und auf allen Ihren Domänen Controllern Windows Server 2016 ausgeführt wird, empfiehlt es sich, während der AD DS Installation AD DS mit der Gesamtstruktur Funktionsebene Windows Server 2016 zu konfigurieren.

> [!IMPORTANT]
> Nachdem Sie die Gesamtstrukturfunktionsebene heraufgestuft haben, können Domänencontroller unter früheren Betriebssystemen nicht mehr in der Gesamtstruktur verwendet werden. Wenn Sie z. b. die Gesamtstruktur Funktionsebene auf Windows Server 2016 erhöhen, können Domänen Controller unter Windows Server 2012 R2 oder Windows Server 2008 nicht der Gesamtstruktur hinzugefügt werden.

Beispiel Konfigurationselemente für AD DS werden in der folgenden Tabelle bereitgestellt.

|Konfigurationselemente:|Beispielwerte:|
|------------------------|-------------------|
|Vollständiger DNS-Name|Beispiele:<br /><br />-Corp.contoso.com<br />-example.com|
|Gesamtstrukturfunktionsebene|-Windows Server 2008 <br />-Windows Server 2008 R2 <br />-Windows Server 2012 <br />-Windows Server 2012 R2 <br />-Windows Server 2016|
|Speicherort des AD DS-Datenbankordners|E:\konfigurations\\<br /><br />Oder übernehmen Sie den Standardspeicherort.|
|Speicherort des AD DS-Protokolldateiordners|E:\konfigurations\\<br /><br />Oder übernehmen Sie den Standardspeicherort.|
|Speicherort des AD DS-SYSVOL-Ordners|E:\konfigurations\\<br /><br />Oder übernehmen Sie den Standardspeicherort.|
|Administratorkennwort für den Verzeichnisdienst-Wiederherstellungsmodus|**J\*p2leO4 $ F**|
|Name der Antwortdatei (optional)|**AD-DS_AnswerFile**|

#### <a name="planning-dns-zones"></a>Planen von DNS-Zonen
Bei primären Active Directory-integrierten DNS-Servern wird bei der Installation der DNS-Serverrolle standardmäßig eine Forward-Lookupzone erstellt. Eine Forward-Lookupzone ermöglicht es Computern und Geräten, die IP-Adresse anderer Computer oder Geräte auf der Grundlage ihres DNS-Namens abzufragen. Zusätzlich zu einer Forward-Lookupzone sollten Sie eine DNS-Reverse-Lookupzone erstellen. Mithilfe einer DNS-Reverse-Lookupabfrage kann ein Computer oder ein Gerät den Namen eines anderen Computers oder Geräts anhand seiner IP-Adresse ermitteln. Die Bereitstellung einer Reverse-Lookupzone verbessert üblicherweise die DNS-Leistung und führt zu wesentlich erfolgreicheren DNS-Abfragen.

Wenn Sie eine Reverse-Lookupzone erstellen, wird die Domäne %%amp;quot;in-addr.arpa%%amp;quot; im DNS konfiguriert. Diese ist in den DNS-Standards definiert und im Internet-DNS-Namespace reserviert, um auf praktische und zuverlässige Weise Rückwärtsabfragen zu ermöglichen. Zur Erstellung eines Reverse-Namespace werden untergeordnete Domänen innerhalb der Domäne in-addr.arpa gebildet, für die eine umgekehrte Sortierung der Zahlen für IP-Adressen in punktierter Dezimalschreibweise verwendet wird.

Die Domäne in-addr. arpa gilt für alle TCP/IP-Netzwerke, die auf der IPv4-Adressierung (Internet Protocol Version 4) basieren. Der Assistent zum Erstellen neuer Zonen setzt automatisch voraus, dass Sie diese Domäne verwenden, wenn Sie eine neue Reverse-Lookupzone erstellen.

Während der Ausführung des Assistenten zum Erstellen neuer Zonen werden die folgenden Auswahlen empfohlen:

|Konfigurationselemente|Beispielwerte|
|-----------------------|------------------|
|Zonentyp|**Primäre Zone** und **Zone in Active Directory speichern** sind ausgewählt.|
|Active Directory-Zonenreplikationsbereich|**An alle DNS-Server in dieser Domäne**|
|Assistentenseite für den Namen der ersten Reverse-Lookupzone|**IPv4-Reverse-Lookupzone**|
|Assistentenseite für den Namen der zweiten Reverse-Lookupzone|Netzwerk-ID = 10.0.0.|
|Dynamische Updates|**Nur sichere dynamische Updates zulassen**|

### <a name="bkmk_NetFndtn_Pln_DomAccess"></a>Planen des Domänen Zugriffs
Wenn Sie sich bei der Domäne anmelden möchten, muss es sich bei dem Computer um einen Domänen Mitglieds Computer handeln, und das Benutzerkonto muss vor dem Anmeldeversuch in AD DS erstellt werden.

> [!NOTE]
> Einzelcomputer unter Windows verfügen über eine Datenbank mit Konten für lokale Benutzer und Gruppen, die als SAM-Benutzerkontendatenbank (Security Accounts Manager, Sicherheitskontenverwaltung) bezeichnet wird. Wenn Sie auf dem lokalen Computer ein Benutzerkonto in der SAM-Datenbank erstellen, können Sie sich beim lokalen Computer, nicht jedoch bei einer Domäne anmelden. Domänenbenutzerkonten werden mit der Microsoft Management Console (MMC) unter Active Directory-Benutzer und Computer auf einem Domänencontroller, nicht mit lokalen Benutzern und Gruppen auf dem lokalen Computer erstellt.

Nach der ersten erfolgreichen Anmeldung mit den Domänenanmeldeinformationen bleiben die Anmeldeeinstellungen erhalten, solange der Computer nicht aus der Domäne entfernt wird oder die Anmeldeeinstellungen manuell geändert werden.

Führen Sie die folgenden Schritte aus, bevor Sie sich bei der Domäne anmelden:

-   Erstellen Sie in Active Directory-Benutzer und -Computer Benutzerkonten. Jeder Benutzer muss in Active Directory-Benutzer und -Computer ein AD DS-Benutzerkonto besitzen. Weitere Informationen finden Sie unter [Erstellen eines Benutzerkontos in %%amp;quot;Active Directory-Benutzer und -Computer%%amp;quot;](#BKMK_createUA).

-   Stellen Sie sicher, dass die richtige IP-Adresskonfiguration verwendet wird. Damit der Computer einer Domäne hinzugefügt werden kann, muss er über eine IP-Adresse verfügen. In dieser Anleitung werden Server mit statischen IP-Adressen konfiguriert, und Clientcomputer empfangen IP-Adressleases vom DHCP-Server. Daher muss der DHCP-Server bereitgestellt werden, bevor der Domäne Clients hinzugefügt werden. Weitere Informationen finden Sie unter [Bereitstellen von DHCP1](#BKMK_deployDHCP01).

-   Fügen Sie den Computer der Domäne hinzu. Alle Computer, die Netzwerkressourcen bereitstellen oder auf diese zugreifen, müssen der Domäne hinzugefügt werden. Weitere Informationen finden Sie unter [Hinzufügen von Servercomputern zur Domäne und Anmelden](#BKMK_joinlogserver) und [Hinzufügen von Clientcomputern zur Domäne und Anmelden](#BKMK_joinlogclients).

### <a name="bkmk_NetFndtn_Pln_DHCP-01"></a>Planen der Bereitstellung von DHCP1
Im Anschluss finden Sie die wichtigsten Planungsschritte vor der Installation der Serverrolle DHCP auf DHCP1.

#### <a name="planning-dhcp-servers-and-dhcp-forwarding"></a>Planen von DHCP-Servern und DHCP-Weiterleitung
Da DHCP-Meldungen Broadcastmeldungen sind, werden diese von Routern nicht zwischen Subnetzen weitergeleitet. Wenn Sie mehrere Subnetze besitzen und für jedes Subnetz DHCP-Dienste bereitstellen möchten, müssen Sie folgendermaßen vorgehen:

-   Installieren Sie einen DHCP-Server in jedem Subnetz.

-   Konfigurieren Sie Router, um DHCP-Broadcastmeldungen zwischen Subnetzen weiterzuleiten, und konfigurieren Sie mehrere Bereiche auf dem DHCP-Server, einen Bereich pro Subnetz.

In den meisten Fällen ist die Konfiguration von Routern für die Weiterleitung von DHCP-Broadcastmeldungen kosteneffektiver als die Bereitstellung eines DHCP-Servers in jedem physischen Segment des Netzwerks.

#### <a name="planning-ip-address-ranges"></a>Planen von IP-Adressbereichen
Jedes Subnetz muss seinen eigenen eindeutigen IP-Adressbereich besitzen. Diese Bereiche werden auf einem DHCP-Server durch Bereiche dargestellt.

Ein Bereich ist eine administrative Gruppierung von IP-Adressen für Computer in einem Subnetz, die den DHCP-Dienst verwenden. Der Administrator erstellt zunächst einen Bereich für jedes physische Subnetz und verwendet diesen dann, um die von den Clients verwendeten Parameter zu definieren.

Ein Bereich weist folgende Eigenschaften auf:

-   Einen IP-Adressbereich, von dem Adressen ein- oder ausgeschlossen werden, die für DHCP-Dienst-Leaseangebote verwendet werden.

-   Eine Subnetzmaske, die das Subnetzpräfix für eine angegebene IP-Adresse bestimmt.

-   Ein bei seiner Erstellung zugewiesener Bereichsname.

-   Leasedauerwerte, die DHCP-Clients zugewiesen werden, die dynamisch zugeordnete IP-Adressen empfangen.

-   Beliebige DHCP-Bereichsoptionen, die für die Zuordnung zu DHCP-Clients konfiguriert wurden, z. B. IP-Adresse des DNS-Servers und IP-Adresse des Routers/Standardgateways.

-   Reservierungen werden optional verwendet, um sicherzustellen, dass ein DHCP-Client immer die gleiche IP-Adresse empfängt.

Listen Sie vor der Bereitstellung Ihrer Server die Subnetze und den IP-Adressbereich auf, den Sie für jedes Subnetz verwenden möchten.

#### <a name="planning-subnet-masks"></a>Planen von Subnetzmasken
Netzwerk-IDs und Host-IDs innerhalb einer IP-Adresse werden mithilfe einer Subnetzmaske unterschieden. Jede Subnetzmaske ist eine 32-Bit-Zahl, die aufeinander folgende Bitgruppen von Einsen (1) verwendet, um die Netzwerk-ID zu kennzeichnen und Nullen (0), um die Host-ID-Abschnitte der IP-Adresse zu kennzeichnen.

Beispielsweise ist die Subnetzmaske, die normalerweise mit der IP-Adresse 131.107.16.200 verwendet wird, die folgende 32-Bit-Binärzahl:

```
11111111 11111111 00000000 00000000
```

Diese Subnetzmasken-Nummer ist 16 1-Bit gefolgt von 16 Null Bits und gibt an, dass die Bereiche Netzwerk-ID und Host-ID dieser IP-Adresse eine Länge von 16 Bit haben. Normalerweise wird diese Subnetzmaske in punktierter Dezimalschreibweise als 255.255.0.0. angezeigt.

In der folgenden Tabelle werden Subnetzmasken für die Internetadressklassen angezeigt.

|Adressklasse|Bits für die Subnetzmaske|Subnetzmaske|
|-----------------|------------------------|---------------|
|Klasse A|11111111 00000000 00000000 00000000|255.0.0.0|
|Klasse B|11111111 11111111 00000000 00000000|255.255.0.0|
|Klasse C|11111111 11111111 11111111 00000000|255.255.255.0|

Wenn Sie einen Bereich in DHCP erstellen und den IP-Adressbereich für den Bereich eingeben, stellt DHCP diese Standard-Subnetzmaskenwerte bereit. In der Regel sind Standard-Subnetzmaskenwerte für die meisten Netzwerke ohne spezielle Anforderungen sowie für Netzwerke, bei denen jedes IP-Netzwerksegment einem physischen Netzwerk entspricht, akzeptabel.

In einigen Fällen können Sie angepasste Subnetzmasken für die Implementierung von IP-Subnetzen verwenden. Mit IP-Subnetzen können Sie den Abschnitt der Standard-Host-ID einer IP-Adresse zur Festlegung von Subnetzen unterteilen, bei denen es sich um Unterabschnitte der ursprünglichen klassenbasierten Netzwerk-ID handelt.

Wenn Sie die Länge der Subnetzmaske anpassen, können Sie die Anzahl der Bits reduzieren, die für die tatsächliche Host-ID verwendet wird.

Zur Vermeidung von Adressierungs- und Routingproblemen sollten Sie sicherstellen, dass alle TCP/IP-Computer in einem Netzwerksegment die gleiche Subnetzmaske verwenden, und dass jeder Computer und jedes Gerät eine eindeutige IP-Adresse besitzt.

#### <a name="planning-exclusion-ranges"></a>Planen von Ausschlussbereichen
Wenn Sie auf einem DHCP-Server einen Bereich erstellen, geben Sie einen IP-Adressbereich an, der alle IP-Adressen enthält, die der DHCP-Server an DHCP-Clients wie Computer und andere Geräte leasen darf. Wenn Sie anschließend einige Server und andere Geräte mit statischen IP-Adressen aus dem IP-Adressbereich manuell konfigurieren, den der DHCP-Server verwendet, können Sie versehentlich einen IP-Adresskonflikt verursachen, wenn Sie und der DHCP-Server verschiedenen Geräten eine IP-Adresse zuweisen.

Um dieses Problem zu beheben, können Sie einen Ausschlussbereich für den DHCP-Bereich erstellen. Ein Ausschluss Bereich ist ein zusammenhängender Bereich von IP-Adressen innerhalb des IP-Adress Bereichs des Bereichs, der vom DHCP-Server nicht verwendet werden darf. Wenn Sie einen Ausschlussbereich erstellen, weist der DHCP-Server keine Adressen aus diesem Bereich zu, sodass Sie diese Adressen manuell zuweisen können, ohne einen IP-Adresskonflikt zu verursachen.

Sie können IP-Adressen von der Verteilung durch den DHCP-Server ausschließen, indem Sie einen Ausschlussbereich für jeden Bereich erstellen. Sie sollten Ausschlüsse für alle Geräte erstellen, die mit einer statischen IP-Adresse konfiguriert sind. Die ausgeschlossenen Adressen sollten alle IP-Adressen enthalten, die Sie manuell anderen Servern, Nicht-DHCP-Clients, Arbeitsstationen ohne Datenträger oder Routing- und Remotezugriff- und PPP-Clients zugewiesen haben.

Es wird empfohlen, den Ausschlussbereich mit zusätzlichen Adressen zu konfigurieren, um für späteres Wachsen des Netzwerks vorbereitet zu sein. In der folgenden Tabelle finden Sie einen Beispiel Ausschluss Bereich für einen Bereich mit dem IP-Adressbereich 10.0.0.1-10.0.0.254 und einer Subnetzmaske von 255.255.255.0.

|Konfigurationselemente|Beispielwerte|
|-----------------------|------------------|
|Start-IP-Adresse des Ausschlussbereichs|10.0.0.1|
|End-IP-Adresse des Ausschlussbereichs|10.0.0.25|

#### <a name="planning-tcpip-static-configuration"></a>Planen einer statischen TCP/IP-Konfiguration
Einige Geräte wie Router, DHCP-Server und DNS-Server müssen mit einer statischen IP-Adresse konfiguriert werden. Möglicherweise haben Sie auch weitere Geräte wie Drucker, für die Sie sicherstellen möchten, dass sie immer die gleiche IP-Adresse besitzen. Listen Sie die Geräte für jedes Subnetz auf, die Sie statisch konfigurieren möchten, und planen Sie dann den Ausschlussbereich, den Sie auf dem DHCP-Server verwenden möchten, um sicherzustellen, dass der DHCP-Server nicht die IP-Adresse eines statisch konfigurierten Geräts least. Ein Ausschlussbereich ist eine begrenzte Abfolge von IP-Adressen innerhalb eines Bereichs, der von der Verarbeitung durch den DHCP-Dienst ausgeschlossen wird. Ausschlussbereiche stellen sicher, dass die Adressen in diesen Bereichen vom Server nicht für DHCP-Clients im Netzwerk bereitgestellt werden.

Wenn der IP-Adressbereich eines Subnetzes beispielsweise 192.168.0.1 bis 192.168.0.254 ist, und Sie zehn Geräte besitzen, die Sie mit einer statischen IP-Adresse konfigurieren möchten, können Sie einen Ausschlussbereich für den Bereich 192.168.0.*x* festlegen, der zehn oder mehr IP-Adressen enthält: 192.168.0.1 bis 192.168.0.15.

In diesem Beispiel werden zehn der ausgeschlossenen IP-Adressen verwendet, um Server und andere Geräte mit statischen IP-Adressen zu konfigurieren, und fünf weitere IP-Adressen bleiben für die Konfiguration neuer Geräte verfügbar, die zukünftig hinzugefügt werden können. Mit diesem Ausschlussbereich verfügt der DHCP-Server noch über einen Adresspool von 192.168.0.16 bis 192.168.0.254.

Weitere Beispiel Konfigurationselemente für AD DS und DNS finden Sie in der folgenden Tabelle.

|Konfigurationselemente|Beispielwerte|
|-----------------------|------------------|
|Bindungen für die Netzwerkverbindung|Ethernet|
|DNS-Servereinstellungen|DC1.corp.contoso.com|
|Bevorzugte IP-Adresse des DNS-Servers|10.0.0.2|
|Werte für das Dialogfeld %%amp;quot;Bereich hinzufügen%%amp;quot;<br /><br />1. Bereichs Name<br />2. Start-IP-Adresse<br />3. IP-Endadresse<br />4. Subnetzmaske<br />5. Standard Gateway (optional)<br />6. Leasedauer|1. primäres Subnetz<br />2.10.0.0.1<br />3.10.0.0.254<br />4.255.255.255.0<br />5.10.0.0.1<br />6.8 Tage|
|Betriebsmodus des IPv6-DHCP-Servers|Nicht aktiviert|

## <a name="BKMK_deployment"></a>Kern Netzwerk Bereitstellung
Führen Sie die folgenden grundlegenden Schritte aus, um ein Hauptnetzwerk bereitzustellen:

1.  [Konfigurieren aller Server](#BKMK_configuringAll)

2.  [Bereitstellen von DC1](#BKMK_deployADDNS01)

3.  [Hinzufügen von Server Computern zur Domäne und anmelden](#BKMK_joinlogserver)

4.  [Bereitstellen von DHCP1](#BKMK_deployDHCP01)

5.  [Hinzufügen von Client Computern zur Domäne und anmelden](#BKMK_joinlogclients)

6.  [Bereitstellen optionaler Features für die Netzwerk Zugriffs Authentifizierung und Webdienste](#BKMK_optionalfeatures)

> [!NOTE]
> -   Entsprechende Befehle von Windows PowerShell werden für die meisten Verfahren in diesem Handbuch bereitgestellt. Ersetzen Sie vor dem Ausführen dieser Cmdlets in Windows PowerShell die Beispielwerte durch Werte, die Ihre Netzwerkbereitstellung geeignet sind. Zudem müssen Sie jedes Cmdlet in Windows PowerShell in einer eigenen Zeile eingeben. In diesem Handbuch möglicherweise einzelne Cmdlets in mehreren Zeilen angezeigt, was auf Formatierungsbeschränkungen und die Anzeige des Dokuments durch den Browser oder eine andere Anwendung zurückzuführen ist.
> -   Die Verfahren in diesem Handbuch beinhalten keine Anleitungen für die Fälle, in denen das Dialogfeld **Benutzerkontensteuerung** geöffnet wird, um die Zustimmung zum Fortfahren abzufragen. Klicken Sie auf **Weiter**, wenn das Dialogfeld während der Ausführung der Verfahren in dieser Anleitung geöffnet wird und als Folge der ausgeführten Aktionen geöffnet wurde.

### <a name="BKMK_configuringAll"></a>Konfigurieren aller Server
Bevor Sie andere Technologien wie Active Directory-Domänendienste oder DHCP installieren, müssen Sie die folgenden Elemente konfigurieren.

-   [Umbenennen des Computers](#BKMK_rename)

-   [Konfigurieren einer statischen IP-Adresse](#BKMK_ip)

Sie können die folgenden Abschnitte verwenden, um diese Schritte auf jedem Server auszuführen.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um diese Verfahren ausführen zu können.

#### <a name="BKMK_rename"></a>Umbenennen des Computers
Mithilfe des in diesem Abschnitt beschriebenen Verfahrens können Sie den Namen eines Computers ändern. Die Umbenennung des Computers ist in Situationen nützlich, in denen das Betriebssystem automatisch einen Computernamen erstellt, den Sie nicht verwenden möchten.

> [!NOTE]
> Um dieses Verfahren mithilfe von Windows PowerShell durchzuführen, öffnen Sie PowerShell, und geben Sie die folgenden Cmdlets jeweils in eigene Zeilen ein, und drücken Sie dann die Eingabetaste. Anstelle von *Computername* müssen Sie den Namen eingeben, den Sie verwenden möchten.
>
> `Rename-Computer`*Computername*
>
> `Restart-Computer`

###### <a name="to-rename-computers-running-windows-server-2016-windows-server-2012-r2-and-windows-server-2012"></a>So benennen Sie Computer unter Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 um

1.  Klicken Sie im Server-Manager auf **Lokaler Server**. Die **Eigenschaften** des Computers werden im Detailbereich angezeigt.

2.  Klicken Sie in den **Eigenschaften** unter **Computername** auf den vorhandenen Computernamen. Das Dialogfeld **Systemeigenschaften** wird geöffnet. Klicken Sie auf **Ändern**. Das Dialogfeld **Ändern des Computernamens bzw. der Domäne** wird geöffnet.

3.  Geben Sie im Dialogfeld **Ändern des Computernamens bzw. der Domäne** unter **Computername** einen neuen Namen für den Computer ein. Wenn Sie dem Computer beispielsweise den Namen DC1 geben möchten, geben Sie **DC1** ein.

4.  Klicken Sie zweimal auf **OK** , und klicken Sie dann auf **Schließen**. Wenn Sie den Computer sofort neu starten möchten, um die Namensänderung abzuschließen, klicken Sie auf **Jetzt neu starten**. Andernfalls klicken Sie auf **Später neu starten**.

> [!NOTE]
> Informationen zum Umbenennen von Computern, auf denen andere Microsoft-Betriebssysteme ausgeführt werden, finden Sie unter [Anhang A: Umbenennen von Computern](#BKMK_A).

#### <a name="BKMK_ip"></a>Konfigurieren einer statischen IP-Adresse
Mithilfe der Verfahren in diesem Thema können Sie die IPv4-Eigenschaften (Internet Protocol Version 4) einer Netzwerkverbindung mit einer statischen IP-Adresse für Computer unter Windows Server 2016 konfigurieren.

> [!NOTE]
> Um dieses Verfahren mithilfe von Windows PowerShell durchzuführen, öffnen Sie PowerShell, und geben Sie die folgenden Cmdlets jeweils in eigene Zeilen ein, und drücken Sie dann die Eingabetaste. Anstelle der Schnittstellennamen und IP-Adressen in diesem Beispiel müssen Sie die Werte angeben, mit denen Sie Ihren Computer konfigurieren möchten.
>
> `New-NetIPAddress -IPAddress 10.0.0.2 -InterfaceAlias "Ethernet" -DefaultGateway 10.0.0.1 -AddressFamily IPv4 -PrefixLength 24`
>
> `Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 127.0.0.1`

###### <a name="to-configure-a-static-ip-address-on-computers-running-windows-server-2016-windows-server-2012-r2-and-windows-server-2012"></a>So konfigurieren Sie eine statische IP-Adresse auf Computern, auf denen Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 ausgeführt wird

1.  Klicken Sie in der Taskleiste mit der rechten Maustaste auf das Netzwerksymbol, und klicken Sie dann auf **Netzwerk- und Freigabecenter öffnen**.

2.  Klicken Sie im **Netzwerk-und Freigabe Center**auf **Adapter Einstellungen ändern**. Im Ordner **Netzwerkverbindungen** werden die verfügbaren Netzwerkverbindungen angezeigt.

3.  Klicken Sie in **Netzwerkverbindungen** mit der rechten Maustaste auf die zu konfigurierende Verbindung, und klicken Sie dann auf **Eigenschaften**. Das Dialogfeld **Eigenschaften** der Netzwerkverbindung wird geöffnet.

4.  Wählen Sie im Dialogfeld **Eigenschaften** unter **Diese Verbindung verwendet folgende Elemente** die Option **Internetprotokoll Version 4 (TCP/IPv4)** aus, und klicken Sie dann auf **Eigenschaften**. Das Dialogfeld **Eigenschaften von Internetprotokoll Version 4 (TCP/IPv4)** wird geöffnet.

5.  Klicken Sie in **Eigenschaften von Internetprotokoll Version 4 (TCP/IPv4)** auf der Registerkarte **Allgemein** auf **Folgende IP-Adresse verwenden**. Geben Sie in **IP-Adresse** die IP-Adresse ein, die Sie verwenden möchten.

6.  Drücken Sie die Tabulatortaste, um mit dem Cursor in das Feld **Subnetzmaske** zu wechseln. Es wird automatisch ein Standardwert für die Subnetzmaske eingefügt. Übernehmen Sie entweder die Standardsubnetzmaske, oder geben Sie die gewünschte Subnetzmaske ein.

7.  Geben Sie im Feld **Standardgateway** die IP-Adresse des Standardgateways ein.

    > [!NOTE]
    > Für **Standardgateway** müssen Sie die IP-Adresse angeben, die Sie in der LAN-Schnittstelle Ihres Routers verwenden. Wenn Ihr Router beispielsweise mit einem WAN wie dem Internet sowie mit Ihrem LAN verbunden ist, konfigurieren Sie die LAN-Schnittstelle mit der IP-Adresse, die Sie dann als **Standardgateway** angeben. Ein weiteres Beispiel: Wenn Ihr Router mit zwei LANs verbunden ist und LAN A den Adressbereich 10.0.0.0/24 und LAN B den Adressbereich 192.168.0.0/24 verwendet, konfigurieren Sie die IP-Adresse des Routers von LAN A mit einer Adresse aus diesem Adressbereich, z. B. 10.0.0.1. Konfigurieren Sie zudem im DHCP-Bereich für diesen Adressbereich das **Standardgateway** mit der IP-Adresse 10.0.0.1. Konfigurieren Sie für LAN B die LAN-B-Routerschnittstelle mit einer Adresse aus diesem Adressbereich, z. B. 192.168.0.1, und konfigurieren Sie dann den LAN-B-Bereich 192.168.0.0/24 mit dem Wert 192.168.0.1 für das **Standardgateway**.

8.  Geben Sie im Feld **Bevorzugter DNS-Server** die IP-Adresse des DNS-Servers ein. Wenn Sie den lokalen Computer als bevorzugten DNS-Server verwenden möchten, geben Sie die IP-Adresse des lokalen Computers ein.

9. Geben Sie gegebenenfalls im Feld **Alternativer DNS-Server** die IP-Adresse des alternativen DNS-Servers ein. Wenn Sie den lokalen Computer als alternativen DNS-Server verwenden möchten, geben Sie die IP-Adresse des lokalen Computers ein.

10. Klicken Sie auf **OK** und dann auf **Schließen**.

> [!NOTE]
> Informationen zum Konfigurieren einer statischen IP-Adresse auf Computern, auf denen andere Microsoft-Betriebssysteme ausgeführt werden, finden Sie in [Anhang B: Konfigurieren statischer IP-Adressen](#BKMK_B).

#### <a name="BKMK_deployADDNS01"></a>Bereitstellen von DC1
Zum Bereitstellen von DC1, bei dem es sich um den Computer mit Active Directory Domain Services (AD DS) und DNS handelt, müssen Sie diese Schritte in der folgenden Reihenfolge ausführen:

-   Führen Sie die Schritte im Abschnitt [Konfigurieren aller Server](#BKMK_configuringAll) aus.

-   [Installieren von AD DS und DNS für eine neue Gesamtstruktur](#BKMK_installAD-DNS)

-   [Erstellen eines Benutzerkontos in Active Directory Benutzern und Computern](#BKMK_createUA)

-   [Gruppenmitgliedschaft zuweisen](#BKMK_assigngroup)

-   [Konfigurieren einer DNS-Reverse-Lookupzone](#BKMK_reverse)

**Administratorrechte**

Wenn Sie ein kleines Netzwerk installieren und der einzige Administrator für dieses Netzwerk sind, sollten Sie für sich selbst ein Benutzerkonto erstellen und dieses Benutzerkonto sowohl der Gruppe Organisations-Admins als auch Domänen-Admins als Mitglied hinzufügen. Auf diese Weise ist es einfacher, als Administrator für alle Netzwerkressourcen zu fungieren. Es wird außerdem empfohlen, sich mit diesem Konto nur zur Ausführung von Verwaltungsaufgaben anzumelden und zur Ausführung von nicht im Zusammenhang mit IT stehenden Aufgaben ein separates Benutzerkonto zu erstellen.

Wenn Sie über eine größere Organisation mit mehreren Administratoren verfügen, lesen Sie AD DS Dokumentation, um die beste Gruppenmitgliedschaft für die Mitarbeiter der Organisation zu ermitteln.

**Unterschiede zwischen Domänen Benutzerkonten und Benutzerkonten auf dem lokalen Computer**

Einer der Vorteile einer domänenbasierten Infrastruktur ist der, dass Sie nicht auf jedem Computer in der Domäne Benutzerkonten erstellen müssen. Dies gilt sowohl für Clientcomputer als auch für Server.

Daher sollten Sie nicht auf jedem Computer in der Domäne Benutzerkonten erstellen. Erstellen Sie alle Benutzerkonten in Active Directory-Benutzer und -Computer, und verwenden Sie die obigen Verfahren, um die Gruppenmitgliedschaft zuzuweisen. Standardmäßig sind alle Benutzerkonten Mitglied der Gruppe Domänenbenutzer.

Alle Mitglieder der Gruppe %%amp;quot;Domänenbenutzer%%amp;quot; können sich nach dem Hinzufügen zur Domäne bei allen Clientcomputern anmelden.

Sie können Benutzerkonten so konfigurieren, dass Sie die Tage und Uhrzeiten angeben können, zu denen sich der Benutzer bei einem Computer anmelden darf. Sie können auch festlegen, welche Computer jeder Benutzer verwenden darf. Um diese Einstellungen zu konfigurieren, öffnen Sie Active Directory-Benutzer und -Computer, und doppelklicken Sie auf das zu konfigurierende Konto. Klicken Sie in den **Eigenschaften** des Benutzerkontos auf die Registerkarte **Konto**, und klicken Sie dann auf **Anmeldezeiten** oder auf **Anmelden an**.

#### <a name="BKMK_installAD-DNS"></a>Installieren von AD DS und DNS für eine neue Gesamtstruktur

Sie können eines der folgenden Verfahren verwenden, um Active Directory Domain Services (AD DS) und DNS zu installieren und eine neue Domäne in einer neuen Gesamtstruktur zu erstellen. 

Das erste Verfahren enthält Anweisungen zum Ausführen dieser Aktionen mithilfe von Windows PowerShell, während das zweite Verfahren zeigt, wie Sie AD DS und DNS mithilfe von Server-Manager installieren.

>[!IMPORTANT]
>Nachdem Sie die Schritte in diesem Verfahren abgeschlossen haben, wird der Computer automatisch neu gestartet.

**Installieren von AD DS und DNS mithilfe von Windows PowerShell**

Sie können die folgenden Befehle verwenden, um AD DS und DNS zu installieren und zu konfigurieren. Sie müssen den Domänen Namen in diesem Beispiel durch den Wert ersetzen, den Sie für Ihre Domäne verwenden möchten.

>[!NOTE]
>Weitere Informationen zu diesen Windows PowerShell-Befehlen finden Sie in den folgenden Referenz Themen.
>- [Install-Windows Feature](https://docs.microsoft.com/powershell/module/servermanager/install-windowsfeature?view=win10-ps)
>- [Install-addsforest](https://docs.microsoft.com/powershell/module/addsdeployment/install-addsforest?view=win10-ps)

Sie müssen mindestens Mitglied der Gruppe **Administratoren** sein, damit Sie dieses Verfahren ausführen können.

- Führen Sie Windows PowerShell als Administrator aus, geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:  

`Install-WindowsFeature AD-Domain-Services -IncludeManagementTools`

Nachdem die Installation erfolgreich abgeschlossen wurde, wird die folgende Meldung in Windows PowerShell angezeigt.


    Success Restart Needed  Exit Code   Feature Result
    ------- --------------  ---------   --------------
    True    No              Success     {Active Directory Domain Services, Group P...


- Geben Sie in Windows PowerShell den folgenden Befehl ein, und ersetzen Sie dabei den Text **Corp.contoso.com** durch Ihren Domänen Namen, und drücken Sie dann die EINGABETASTE:

````
Install-ADDSForest -DomainName "corp.contoso.com"
````

- Während des Installations-und Konfigurations Vorgangs, der oben im Windows PowerShell-Fenster angezeigt wird, wird die folgende Eingabeaufforderung angezeigt. Geben Sie anschließend ein Kennwort ein, und drücken Sie dann die EINGABETASTE.

    **SafeModeAdministratorPassword**

- Nachdem Sie ein Kennwort eingegeben und die EINGABETASTE gedrückt haben, wird die folgende Bestätigungsaufforderung angezeigt. Geben Sie dasselbe Kennwort ein, und drücken Sie die EINGABETASTE.

    **Bestätigen Sie SafeModeAdministratorPassword:**

- Wenn die folgende Eingabeaufforderung angezeigt wird, geben Sie den Buchstaben **Y** ein und drücken dann die EINGABETASTE.


~~~
The target server will be configured as a domain controller and restarted when this operation is complete.
Do you want to continue with this operation?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"):
~~~

- Wenn Sie möchten, können Sie die Warnmeldungen lesen, die während der normalen, erfolgreichen Installation von AD DS und DNS angezeigt werden. Diese Nachrichten sind normal und keine Anzeichen für Installationsfehler.

- Nachdem die Installation erfolgreich abgeschlossen wurde, wird eine Meldung mit dem Hinweis angezeigt, dass Sie im Begriff sind, sich vom Computer abzumelden, damit der Computer neu gestartet werden kann. Wenn Sie auf **Schließen**klicken, werden Sie sofort vom Computer abgemeldet, und der Computer wird neu gestartet. Wenn Sie nicht auf " **Schließen**" klicken, wird der Computer nach einem Standard Zeitraum neu gestartet.

- Nachdem der Server neu gestartet wurde, können Sie die erfolgreiche Installation von Active Directory Domain Services und DNS überprüfen. Öffnen Sie Windows PowerShell, geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE.

````
Get-WindowsFeature
````

Die Ergebnisse dieses Befehls werden in Windows PowerShell angezeigt und sollten den Ergebnissen in der folgenden Abbildung ähneln. Bei installierten Technologien enthalten die eckigen Klammern links neben dem Technologie Namen das Zeichen **X**, und der Wert **Installationsstatus** ist **installiert**.

![Ergebnisse des Befehls "Get-Windows Feature"](../media/Core-Network-Guide/server-roles-installed.jpg)

**Installieren von AD DS und DNS mithilfe Server-Manager**

1.  Klicken Sie auf DC1 unter **Server-Manager** auf **Verwalten** und dann auf **Rollen und Features hinzufügen**. Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet.

2.  Klicken Sie auf der Seite **Vorbemerkungen** auf **Weiter**.

    > [!NOTE]
    > Die Seite **Vorbemerkungen** im Assistenten zum Hinzufügen von Rollen und Features wird nicht angezeigt, wenn Sie bei einer früheren Ausführung des Assistenten die Option **Seite standardmäßig überspringen** ausgewählt haben.

3.  Wählen Sie unter **Installationstyp auswählen** die Option **Rollenbasierte oder featurebasierte Installation** aus, und klicken Sie dann auf **Weiter**.

4.  Stellen Sie sicher, dass unter **Zielserver auswählen** die Option **Einen Server aus dem Serverpool auswählen** aktiviert ist. Wählen Sie unter **Serverpool** den lokalen Computer aus. Klicken Sie auf **Weiter**.

5.  Klicken Sie im Dialogfeld **Serverrollen auswählen** unter **Rollen** auf **Active Directory-Domänendienste**. Klicken Sie unter **Sollen für Active Directory-Domänendienste erforderliche Features hinzugefügt werden?** auf **Features hinzufügen**. Klicken Sie auf **Weiter**.

6.  Klicken Sie unter **Features auswählen** auf **Weiter**, überprüfen Sie unter **Active Directory-Domänendienste** die angegebenen Informationen, und klicken Sie dann auf **Weiter**.

7.  Klicken Sie unter **Installationsauswahl bestätigen** auf **Installieren**. Auf der Seite %%amp;quot;Installationsstatus%%amp;quot; wird der Status während der Installation angezeigt. Klicken Sie nach Abschluss der Installation in den Meldungsdetails auf **Server zu einem Domänencontroller heraufstufen**. Der Konfigurations-Assistent für die Active Directory-Domänendienste wird geöffnet.

8.  Wählen Sie unter **Bereitstellungskonfiguration** die Option **Gesamtstruktur hinzufügen** aus. Geben Sie unter **Name der Stammdomäne** den vollqualifizierten Domänennamen (FQDN) für die Domäne ein. Wenn der vollqualifizierte Domänenname beispielsweise %%amp;quot;corp.contoso.com%%amp;quot; lautet, geben Sie **corp.contoso.com** ein. Klicken Sie auf **Weiter**.

9. Wählen Sie in **Domänencontrolleroptionen** unter **Funktionsebene der neuen Gesamtstruktur und der Stammdomäne auswählen** die gewünschte Funktionsebene der Gesamtstruktur und der Domäne aus. Vergewissern Sie sich, dass unter **Domänencontrollerfunktionen angeben** die Optionen **DNS-Server (Domain Name System)** und **Globaler Katalog** aktiviert sind. Geben Sie unter **Kennwort** und **Kennwort bestätigen** das gewünschte Kennwort für den Verzeichnisdienst-Wiederherstellungsmodus (Directory Services Restore Mode, DSRM) ein. Klicken Sie auf **Weiter**.

10. Klicken Sie unter **DNS-Optionen** auf **Weiter**.

11. Überprüfen Sie unter **Weitere Optionen** den der Domäne zugewiesenen NetBIOS-Namen, und ändern Sie ihn nur bei Bedarf. Klicken Sie auf **Weiter**.

12. Führen Sie in **Pfade** unter **Geben Sie den Speicherort der AD DS-Datenbank, der Protokolldateien und den Ort von SYSVOL an** einen der folgenden Schritte aus:

    -   Übernehmen Sie die Standardwerte.

    -   Geben Sie Speicherorte für **Datenbankordner**, **Ordner für Protokolldateien** und **Ordner %%amp;quot;SYSVOL%%amp;quot;** ein.

13. Klicken Sie auf **Weiter**.

14. Überprüfen Sie unter **Optionen prüfen** Ihre Auswahl.

15. Wenn Sie Einstellungen in ein Windows PowerShell-Skript exportieren möchten, klicken Sie auf **Skript anzeigen**. Das Skript wird in Editor geöffnet, und Sie können es am gewünschten Speicherort speichern. Klicken Sie auf **Weiter**. Unter **Voraussetzungsüberprüfung** wird Ihre Auswahl überprüft. Klicken Sie nach Abschluss der Überprüfung auf **Installieren**. Wenn Sie von Windows dazu aufgefordert werden, klicken Sie auf **Schließen**. Der Server wird neu gestartet, um die Installation von AD DS und DNS abzuschließen.

16. Um die erfolgreiche Installation zu überprüfen, können Sie die Server-Manager Konsole anzeigen, nachdem der Server neu gestartet wurde. Im linken Bereich sollten sowohl AD DS als auch DNS angezeigt werden, wie z. b. die markierten Elemente in der Abbildung unten.

![AD DS und DNS in Server-Manager](../media/Core-Network-Guide/server-roles-installed-sm.jpg)

##### <a name="BKMK_createUA"></a>Erstellen eines Benutzerkontos in Active Directory Benutzern und Computern
Mithilfe dieses Verfahrens können Sie unter Active Directory-Benutzer und -Computer in der Microsoft Management Console (MMC) ein neues Domänenbenutzerkonto erstellen.

Sie müssen mindestens Mitglied der Gruppe **Domänen-Admins** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.

> [!NOTE]
> Um dieses Verfahren mithilfe von Windows PowerShell durchzuführen, öffnen Sie PowerShell, und geben Sie das folgende Cmdlet in eine eigene Zeile ein, und drücken Sie dann die Eingabetaste. Anstelle des Benutzerkontonamens in diesem Beispiel müssen Sie den Wert angeben, den Sie verwenden möchten.
>
> `New-ADUser -SamAccountName User1 -AccountPassword (read-host "Set user password" -assecurestring) -name "User1" -enabled $true -PasswordNeverExpires $true -ChangePasswordAtLogon $false`
>
> Geben Sie nach dem Drücken der Eingabetaste das Kennwort für das Benutzerkonto ein. Das Konto wird erstellt und standardmäßig Mitglied der Gruppe %%amp;quot;Domänenbenutzer%%amp;quot;.
>
> Mit dem folgenden Cmdlet können Sie dem neuen Benutzerkonto weitere Gruppenmitgliedschaften zuweisen. Im folgenden Beispiel wird den Gruppen %%amp;quot;Domänen-Admins%%amp;quot; und %%amp;quot;Organisations-Admins%%amp;quot; der Benutzer %%amp;quot;Benutzer1%%amp;quot; hinzugefügt. Ändern Sie vor dem Ausführen dieses Befehls den Benutzerkontonamen, den Domänennamen und die Gruppen entsprechend Ihren Anforderungen.
>
> `Add-ADPrincipalGroupMembership -Identity "CN=User1,CN=Users,DC=corp,DC=contoso,DC=com" -MemberOf "CN=Enterprise Admins,CN=Users,DC=corp,DC=contoso,DC=com","CN=Domain Admins,CN=Users,DC=corp,DC=contoso,DC=com"`

###### <a name="to-create-a-user-account"></a>So erstellen Sie ein Benutzerkonto

1.  Klicken Sie auf DC1 unter Server-Manager auf **Tools** und dann auf **Active Directory-Benutzer und -Computer**. Das MMC-Snap-In %%amp;quot;Active Directory-Benutzer und -Computer%%amp;quot; wird geöffnet. Klicken Sie auf den Knoten für Ihre Domäne, wenn diese noch nicht ausgewählt ist. Wenn Ihre Domäne beispielsweise %%amp;quot;corp.contoso.com%%amp;quot; heißt, klicken Sie auf **corp.contoso.com**.

2.  Klicken Sie im Detailbereich mit der rechten Maustaste auf den Ordner, in dem Sie das Benutzerkonto erstellen möchten.

    **Was?**

    -   Active Directory Benutzer und Computer/*Domänen Knoten*/*Ordners*

3.  Zeigen Sie auf **Neu**, und klicken Sie dann auf **Benutzer**. Das Dialogfeld **Neues Objekt-Benutzer** wird geöffnet.

4.  Geben Sie unter **Vorname** den Vornamen des Benutzers ein.

5.  Geben Sie unter **Initialen** die Initialen des Benutzers ein.

6.  Geben Sie unter **Nachname** den Nachnamen des Benutzers ein.

7.  Ändern Sie **Vollständiger Name**, um Initialen hinzuzufügen oder die Reihenfolge des Vor- und Nachnamen umzukehren.

8.  Geben Sie im Feld **Benutzeranmeldename** den Benutzeranmeldenamen ein. Klicken Sie auf **Weiter**.

9. Geben Sie im Dialogfeld **Neues Objekt - Benutzer** unter **Kennwort** und **Kennwort bestätigen** das Benutzerkennwort ein, und wählen Sie die entsprechenden Kennwortoptionen aus.

10. Klicken Sie auf **Weiter**, überprüfen Sie die Einstellungen des neuen Benutzerkontos, und klicken Sie auf **Fertig stellen**.

##### <a name="BKMK_assigngroup"></a>Gruppenmitgliedschaft zuweisen
Mithilfe dieses Verfahrens können Sie einen Benutzer, einen Computer oder eine Gruppe zu einer Gruppe unter Active Directory-Benutzer und -Computer in der Microsoft Management Console (MMC) hinzufügen.

Für dieses Verfahren müssen Sie mindestens Mitglied der Gruppe **Domänen-Admins** oder einer gleichwertigen Gruppe sein.

###### <a name="to-assign-group-membership"></a>So weisen Sie eine Gruppenmitgliedschaft zu

1.  Klicken Sie auf DC1 unter Server-Manager auf **Tools** und dann auf **Active Directory-Benutzer und -Computer**. Das MMC-Snap-In %%amp;quot;Active Directory-Benutzer und -Computer%%amp;quot; wird geöffnet. Klicken Sie auf den Knoten für Ihre Domäne, wenn diese noch nicht ausgewählt ist. Wenn Ihre Domäne beispielsweise %%amp;quot;corp.contoso.com%%amp;quot; heißt, klicken Sie auf **corp.contoso.com**.

2.  Doppelklicken Sie im Detailbereich auf den Ordner mit der Gruppe, der ein Mitglied hinzugefügt werden soll.

    Position

    -   **Active Directory von Benutzern und Computern**/*Domänen Knoten*/*Ordner, der die Gruppe enthält*

3.  Klicken Sie im Detailbereich mit der rechten Maustaste auf das Objekt, das Sie einer Gruppe hinzufügen möchten, z. B. einen Benutzer oder einen Computer, und klicken Sie dann auf **Eigenschaften**. Das Dialogfeld **Eigenschaften** des-Objekts wird geöffnet. Klicken Sie auf die Registerkarte **Mitglied von**.

4.  Klicken Sie auf der Registerkarte **Mitglied von** auf **Hinzufügen**.

5.  Geben Sie im Feld **Geben Sie die zu verwendenden Objektnamen ein** den Namen der Gruppe ein, der Sie dieses Objekt hinzufügen möchten, und klicken Sie dann auf **OK**.

6.  Wenn Sie anderen Benutzern, Gruppen oder Computern die Mitgliedschaft in der Gruppe zuzuweisen möchten, wiederholen Sie die Schritte 4 und 5 dieses Verfahrens.

##### <a name="BKMK_reverse"></a>Konfigurieren einer DNS-Reverse-Lookupzone
Mithilfe dieses Verfahrens können Sie eine Reverse-Lookupzone im Domain Name System (DNS) konfigurieren.

Sie müssen mindestens Mitglied der Gruppe **Domänen-Admins** sein, damit Sie dieses Verfahren ausführen können.

> [!NOTE]
> -   Für mittelgroße und große Organisationen empfiehlt es sich, die Gruppe DnsAdmins in Active Directory Benutzer und Computern zu konfigurieren und zu verwenden. Weitere Informationen finden Sie unter [Weitere technische Ressourcen](#BKMK_resources).
> -   Um dieses Verfahren mithilfe von Windows PowerShell durchzuführen, öffnen Sie PowerShell, und geben Sie das folgende Cmdlet in eine eigene Zeile ein, und drücken Sie dann die Eingabetaste. Anstelle der DNS-Reverse-Lookupzone und der Zonendateinamen in diesem Beispiel müssen Sie die Werte angeben, die Sie verwenden möchten. Kehren Sie die Netzwerk-ID für den Namen der Reverse-Lookupzone um. Wenn die Netzwerk-ID z. b. 192.168.0 lautet, erstellen Sie den Reverse-lookupzonennamen **0.168.192.in-addr. arpa**.
>
> `Add-DnsServerPrimaryZone 0.0.10.in-addr.arpa -ZoneFile 0.0.10.in-addr.arpa.dns`

###### <a name="to-configure-a-dns-reverse-lookup-zone"></a>So konfigurieren Sie eine DNS-Reverse-Lookupzone

1.  Klicken Sie auf DC1 unter Server-Manager auf **Tools** und dann auf **DNS**. Das DNS-Snap-In der MMC wird geöffnet.

2.  Doppelklicken Sie unter DNS auf den Servernamen, um die Struktur zu erweitern, wenn dies noch nicht geschehen ist. Wenn der Name des DNS-Servers beispielsweise DC1 lautet, doppelklicken Sie auf **DC1**.

3.  Wählen Sie **Reverse-Lookupzonen** aus, klicken Sie mit der rechten Maustaste auf **Reverse-Lookupzonen**, und klicken Sie auf **Neue Zone**. Der Assistent zum Erstellen neuer Zonen wird geöffnet.

4.  Klicken Sie auf der Seite **Willkommen** auf **Weiter**.

5.  Wählen Sie unter **Zonentyp** die Option **Primäre Zone** aus.

6.  Wenn Ihr DNS-Server ein beschreibbarer Domänencontroller ist, stellen Sie sicher, dass **Zone in Active Directory speichern** ausgewählt ist. Klicken Sie auf **Weiter**.

7.  Wählen Sie unter **Active Directory-Zonenreplikationsbereich** die Option **Auf allen DNS-Servern, die auf Domänencontrollern in dieser Domäne ausgeführt werden** aus, es sei denn, Sie haben einen bestimmten Grund, eine andere Option auszuwählen. Klicken Sie auf **Weiter**.

8.  Wählen Sie auf der ersten Seite **Name der Reverse-Lookupzone** die Option **IPv4 Reverse-Lookupzone** aus. Klicken Sie auf **Weiter**.

9. Führen Sie auf der zweiten Seite **Name der Reverse-Lookupzone** einen der folgenden Schritte aus:

    -   Geben Sie im Feld **Netzwerk-ID** die Netzwerk-ID Ihres IP-Adressbereichs ein. Wenn der IP-Adressbereich beispielsweise die Adressen von 10.0.0.1 bis 10.0.0.254 enthält, geben Sie **10.0.0** ein.

    -   In **Name der Reverse-Lookupzone** wird der Name Ihrer IPv4 Reverse-Lookupzone automatisch hinzugefügt. Klicken Sie auf **Weiter**.

10. Wählen Sie unter **Dynamisches Update** den Typ der dynamischen Updates aus, die Sie zulassen möchten. Klicken Sie auf **Weiter**.

11. Überprüfen Sie auf der Seite **Fertigstellen des Assistenten** Ihre Auswahl, und klicken Sie auf **Fertig stellen**.

#### <a name="BKMK_joinlogserver"></a>Hinzufügen von Server Computern zur Domäne und anmelden
Nachdem Sie Active Directory Domain Services (AD DS) installiert und ein oder mehrere Benutzerkonten erstellt haben, die über Berechtigungen zum Hinzufügen eines Computers zur Domäne verfügen, können Sie der Domäne Kern Netzwerkserver hinzufügen und sich bei den Servern anmelden, um zusätzliche Technologien, wie z. b. DHCP (Dynamic Host Configuration Protocol).

Führen Sie auf allen Servern, die Sie bereitstellen, mit Ausnahme des Servers, auf dem AD DS ausgeführt wird, die folgenden Schritte aus:

1.  Führen Sie die unter [Konfigurieren aller Server](#BKMK_configuringAll) erläuterten Verfahren aus.

2.  Verwenden Sie die Anleitungen in den folgenden beiden Verfahren, um Ihre Server der Domäne hinzuzufügen und sich bei den Servern anzumelden, sodass Sie weitere Bereitstellungsaufgaben auszuführen können:

> [!NOTE]
> Um dieses Verfahren mithilfe von Windows PowerShell durchzuführen, öffnen Sie PowerShell, geben Sie das folgende Cmdlet ein, und drücken Sie dann die Eingabetaste. Anstelle des Domänennamens müssen Sie den Namen eingeben, den Sie verwenden möchten.
>
> `Add-Computer -DomainName corp.contoso.com`
>
> Wenn Sie dazu aufgefordert werden, geben Sie den Benutzernamen und das Kennwort für ein Konto ein, das über die Berechtigung zum Hinzufügen eines Computers zur Domäne verfügt. Um den Computer neu zu starten, geben Sie den folgenden Befehl ein, und drücken Sie die Eingabetaste.
>
> `Restart-Computer`

###### <a name="to-join-computers-running--windows-server-2016--windows-server-2012-r2--and--windows-server-2012--to-the-domain"></a>So fügen Sie Computer, auf denen Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 ausgeführt wird, der Domäne hinzu

1.  Klicken Sie im Server-Manager auf **Lokaler Server**. Klicken Sie im Detailbereich auf **ARBEITSGRUPPE**. Das Dialogfeld **Systemeigenschaften** wird geöffnet.

2.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf **Ändern**. Das Dialogfeld **Ändern des Computernamens bzw. der Domäne** wird geöffnet.

3.  Klicken Sie im Dialogfeld **Computername** unter **Mitglied von** auf **Domäne**, und geben Sie den Namen der Domäne ein, der der Computer hinzugefügt werden soll. Wenn Ihre Domäne beispielsweise %%amp;quot;corp.contoso.com%%amp;quot; heißt, geben Sie **corp.contoso.com** ein.

4.  Klicken Sie auf **OK**. Das Dialogfeld **Windows-Sicherheit** wird geöffnet.

5.  Geben Sie im Dialogfeld **Ändern des Computernamens bzw. der Domäne** im Feld **Benutzername** den Benutzernamen und im Feld **Kennwort** das Kennwort ein, und klicken Sie auf **OK**. Das Dialogfeld **Ändern des Computernamens bzw. der Domäne** wird geöffnet, und Sie werden bei der Domäne begrüßt. Klicken Sie auf **OK**.

6.  Im Dialogfeld **Ändern des Computernamens bzw. der Domäne** wird eine Meldung angezeigt, dass der Computer neu gestartet werden muss, damit die Änderungen wirksam werden. Klicken Sie auf **OK**.

7.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf der Registerkarte **Computername** auf **Schließen**. Das Dialogfeld **Microsoft Windows** wird geöffnet und zeigt erneut die Meldung an, dass der Computer neu gestartet werden muss, damit die Änderungen wirksam werden. Klicken Sie auf **Jetzt neu starten**.

> [!NOTE]
> Informationen zum Hinzufügen von Computern, auf denen andere Microsoft-Betriebssysteme ausgeführt werden, zur Domäne finden Sie unter [Anhang C: Verknüpfen von Computern mit der Domäne](#BKMK_C).

###### <a name="to-log-on-to-the-domain-using-computers-running-windows-server-2016"></a>So melden Sie sich bei der Domäne mit Computern an, auf denen Windows Server 2016 ausgeführt wird

1.  Melden Sie den Computer ab, oder starten Sie ihn neu.

2.  Drücken Sie STRG+ALT+ENTF. Der Anmeldebildschirm wird angezeigt.

3.  Klicken Sie in der unteren linken Ecke auf **anderer Benutzer**.

4.  Geben Sie unter **Benutzername**Ihren Benutzernamen ein.

5.  Geben Sie im Feld **Kennwort** das Domänenkennwort ein, und klicken Sie auf den Pfeil, oder drücken Sie die EINGABETASTE.

> [!NOTE]
> Informationen zum Anmelden bei der Domäne mithilfe von Computern, auf denen andere Microsoft-Betriebssysteme ausgeführt werden, finden Sie unter [Anhang D-Anmelden bei der Domäne](#BKMK_D).

#### <a name="BKMK_deployDHCP01"></a>Bereitstellen von DHCP1
Bevor Sie diese Komponente des Hauptnetzwerks bereitstellen können, müssen Sie folgende Schritte ausführen:

-   Führen Sie die Schritte im Abschnitt [Konfigurieren aller Server](#BKMK_configuringAll) aus.

-   Führen Sie die Schritte im Abschnitt [Hinzufügen von Servercomputern zur Domäne und Anmelden](#BKMK_joinlogserver) aus.

Führen Sie die folgenden Schritte in der angegebenen Reihenfolge aus, um DHCP1 bereitzustellen. Dabei handelt es sich um den Computer, auf dem die Serverrolle DHCP ausgeführt wird.

-   [Installieren des Dynamic Host Configuration-Protokolls (DHCP)](#BKMK_installDHCP)

-   [Erstellen und Aktivieren eines neuen DHCP-Bereichs](#BKMK_newscopeDHCP)

> [!NOTE]
> Um diese Verfahren mithilfe von Windows PowerShell durchzuführen, öffnen Sie PowerShell, und geben Sie die folgenden Cmdlets jeweils in eigene Zeilen ein, und drücken Sie dann die Eingabetaste. Anstelle von Bereichsname, Anfangs- und Endbereich der IP-Adressen, Subnetzmaske und anderen Werten in diesem Beispiel müssen Sie die Werte eingeben, die Sie verwenden möchten.
>
> `Install-WindowsFeature DHCP -IncludeManagementTools`
>
> `Add-DhcpServerv4Scope -name "Corpnet" -StartRange 10.0.0.1 -EndRange 10.0.0.254 -SubnetMask 255.255.255.0 -State Active`
>
> `Add-DhcpServerv4ExclusionRange -ScopeID 10.0.0.0 -StartRange 10.0.0.1 -EndRange 10.0.0.15`
>
> `Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.0.1 -ScopeID 10.0.0.0 -ComputerName DHCP1.corp.contoso.com`
>
> `Add-DhcpServerv4Scope -name "Corpnet2" -StartRange 10.0.1.1 -EndRange 10.0.1.254 -SubnetMask 255.255.255.0 -State Active`
>
> `Add-DhcpServerv4ExclusionRange -ScopeID 10.0.1.0 -StartRange 10.0.1.1 -EndRange 10.0.1.15`
>
> `Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.1.1 -ScopeID 10.0.1.0 -ComputerName DHCP1.corp.contoso.com`
>
> `Set-DhcpServerv4OptionValue -DnsDomain corp.contoso.com -DnsServer 10.0.0.2`
>
> `Add-DhcpServerInDC -DnsName DHCP1.corp.contoso.com`

##### <a name="BKMK_installDHCP"></a>Installieren des Dynamic Host Configuration-Protokolls (DHCP)
Mithilfe dieses Verfahrens können Sie die Rolle DHCP-Server unter Verwendung des Assistenten zum Hinzufügen von Rollen und Features installieren und konfigurieren.

Sie müssen mindestens Mitglied der Gruppe **Domänen-Admins** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.

###### <a name="to-install-dhcp"></a>So installieren Sie DHCP

1.  Klicken Sie auf DHCP1 unter Server-Manager auf **Verwalten** und dann auf **Rollen und Features hinzufügen**. Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet.

2.  Klicken Sie auf der Seite **Vorbemerkungen** auf **Weiter**.

    > [!NOTE]
    > Die Seite **Vorbemerkungen** im Assistenten zum Hinzufügen von Rollen und Features wird nicht angezeigt, wenn Sie bei einer früheren Ausführung des Assistenten die Option **Seite standardmäßig überspringen** ausgewählt haben.

3.  Wählen Sie unter **Installationstyp auswählen** die Option **Rollenbasierte oder featurebasierte Installation** aus, und klicken Sie dann auf **Weiter**.

4.  Stellen Sie sicher, dass unter **Zielserver auswählen** die Option **Einen Server aus dem Serverpool auswählen** aktiviert ist. Wählen Sie unter **Serverpool** den lokalen Computer aus. Klicken Sie auf **Weiter**.

5.  Wählen Sie unter **Server Rollen auswählen**unter **Rollen**die Option **DHCP-Server**aus. Klicken Sie unter **Sollen für DHCP-Server erforderliche Features hinzugefügt werden?** auf **Features hinzufügen**. Klicken Sie auf **Weiter**.

6.  Klicken Sie unter **Features auswählen** auf **Weiter**, überprüfen Sie unter **DHCP-Server** die angegebenen Informationen, und klicken Sie dann auf **Weiter**.

7.  Klicken Sie unter **Installationsauswahl bestätigen** auf **Zielserver bei Bedarf automatisch neu starten**. Wenn Sie aufgefordert werden, die Auswahl zu bestätigen, klicken Sie auf **Ja** und dann auf **Installieren**. Auf der Seite **Installationsfortschritt** wird während des Installationsvorgangs der Status angezeigt. Wenn der Prozess abgeschlossen ist, wird die Meldung "Konfiguration erforderlich. Die Installation auf *Computername*war erfolgreich "wird angezeigt, wobei *Computername* der Name des Computers ist, auf dem der DHCP-Server installiert wurde. Klicken Sie im Meldungsfenster auf **DHCP-Konfiguration abschließen**. Der DHCP-Konfigurations-Assistent nach der Installation wird geöffnet. Klicken Sie auf **Weiter**.

8.  Geben Sie unter **Autorisierung** die Anmeldeinformationen an, die beim Autorisieren des DHCP-Servers in Active Directory-Domänendienste verwendet werden sollen, und klicken Sie dann auf **Commit ausführen**. Klicken Sie nach Abschluss der Autorisierung auf **Schließen**.

##### <a name="BKMK_newscopeDHCP"></a>Erstellen und Aktivieren eines neuen DHCP-Bereichs
Mithilfe dieses Verfahrens können Sie unter Verwendung des DHCP-Snap-Ins der Microsoft Management Console (MMC) einen neuen DHCP-Bereich zu erstellen. Nach dem Abschluss des Verfahrens ist der Bereich aktiviert und der erstellte Ausschlussbereich verhindert, dass der DHCP-Server die IP-Adressen least, die Sie für die statische Konfiguration Ihrer Server und anderer Geräte verwenden, die eine statische IP-Adresse benötigen.

Sie müssen mindestens Mitglied der Gruppe **DHCP-Administratoren** oder einer entsprechenden Gruppe sein, um diese Verfahren ausführen zu können.

###### <a name="to-create-and-activate-a-new-dhcp-scope"></a>So erstellen und aktivieren Sie einen neuen DHCP-Bereich

1.  Klicken Sie auf DHCP1 unter Server-Manager auf **Tools** und dann auf **DHCP**. Das DHCP-Snap-In der MMC wird geöffnet.

2.  Erweitern Sie in **DHCP**den Servernamen. Wenn der Name des DHCP-Servers z. b. DHCP1.Corp.contoso.com lautet, klicken Sie auf den Pfeil nach unten neben **DHCP1.Corp.contoso.com**.

3.  Klicken Sie unterhalb des Server namens mit der rechten Maustaste auf **IPv4**, und klicken Sie dann auf **neuer Bereich**. Der Bereichserstellungs-Assistent wird geöffnet.

4.  Klicken Sie auf der Seite **Willkommen** auf **Weiter**.

5.  Geben Sie im Dialogfeld **Bereichsname** unter **Name** einen Namen für den Bereich ein. Geben Sie beispielsweise **Subnetz 1** ein.

6.  Geben Sie im Feld **Beschreibung** eine Beschreibung für den neuen Bereich ein, und klicken Sie auf **Weiter**.

7.  Führen Sie unter **IP-Adressbereich** eine der folgenden Aktionen aus:

    1.  Geben Sie im Feld **Start-IP-Adresse** die erste IP-Adresse des Bereichs ein. Geben Sie beispielsweise **10.0.0.1** ein.

    2.  Geben Sie im Feld **End-IP-Adresse** die letzte IP-Adresse des Bereichs ein. Geben Sie z. b. **10.0.0.254**ein. Die Werte für **Länge** und **Subnetzmaske** werden auf der Grundlage der unter **Start-IP-Adresse** eingegebenen IP-Adresse automatisch eingegeben.

    3.  Ändern Sie die Werte für **Länge** oder **Subnetzmaske** gegebenenfalls entsprechend Ihres Adressierungsschemas.

    4.  Klicken Sie auf **Weiter**.

8.  Führen Sie unter **Ausschlüsse hinzufügen** eine der folgenden Aktionen aus:

    1.  Geben Sie im Feld **Start-IP-Adresse** die erste IP-Adresse des Ausschlussbereichs ein. Geben Sie beispielsweise **10.0.0.1** ein.

    2.  Geben Sie im Feld **End-IP-Adresse** die letzte IP-Adresse des Ausschlussbereichs ein, beispielsweise **10.0.0.15**.

9. Klicken Sie auf **Hinzufügen** und dann auf **Weiter**.

10. Ändern Sie unter **Leasedauer** die Standardwerte für **Tage**, **Stunden**, und **Minuten** entsprechend den Anforderungen Ihres Netzwerks, und klicken Sie auf **Weiter**.

11. Wählen Sie unter **DHCP-Optionen konfigurieren** die Option **Ja, diese Optionen jetzt konfigurieren** aus, und klicken Sie auf **Weiter**.

12. Führen Sie unter **Router (Standardgateway)** eine der folgenden Aktionen aus:

    -   Wenn sich in Ihrem Netzwerk keine Router befinden, klicken Sie auf **Weiter**.

    -   Geben Sie im Feld **IP-Adresse** die IP-Adresse des Routers oder Standardgateways ein. Geben Sie beispielsweise **10.0.0.1** ein. Klicken Sie auf **Hinzufügen** und dann auf **Weiter**.

13. Gehen Sie unter **Domänenname und DNS-Server** folgendermaßen vor:

    1.  Geben Sie im Feld **Übergeordnete Domäne** den Namen der von den Clients zur Namensauflösung verwendeten DNS-Domäne ein. Geben Sie beispielsweise **corp.contoso.com** ein.

    2.  Geben Sie im Feld **Servername** den Namen des von den Clients zur Namensauflösung verwendeten DNS-Computers ein. Geben Sie beispielsweise **DC1** ein.

    3.  Klicken Sie auf **Auflösen**. Die IP-Adresse des DNS-Servers wird dem Feld **IP-Adresse** hinzugefügt. Klicken Sie auf **Hinzufügen**, warten Sie, bis die Überprüfung der IP-Adresse des DNS-Servers abgeschlossen ist, und klicken Sie auf **Weiter**.

14. Da sich in Ihrem Netzwerk keine WINS-Server befinden, klicken Sie unter **WINS-Server** auf **Weiter**.

15. Wählen Sie unter **Bereich aktivieren** die Option **Ja, diesen Bereich jetzt aktivieren** aus.

16. Klicken Sie auf **Weiter**und dann auf **Fertig stellen**.

> [!IMPORTANT]
> Wenn Sie neue Bereiche für weitere Subnetze erstellen möchten, wiederholen Sie dieses Verfahren. Verwenden Sie für jedes Subnetz, das Sie bereitstellen möchten, einen anderen IP-Adressbereich, und stellen Sie sicher, dass die Weiterleitung von DHCP-Meldungen auf allen Routern aktiviert ist, die in andere Subnetze führen.

### <a name="BKMK_joinlogclients"></a>Hinzufügen von Client Computern zur Domäne und anmelden

> [!NOTE]
> Um dieses Verfahren mithilfe von Windows PowerShell durchzuführen, öffnen Sie PowerShell, geben Sie das folgende Cmdlet ein, und drücken Sie dann die Eingabetaste. Anstelle des Domänennamens müssen Sie den Namen eingeben, den Sie verwenden möchten.
>
> `Add-Computer -DomainName corp.contoso.com`
>
> Wenn Sie dazu aufgefordert werden, geben Sie den Benutzernamen und das Kennwort für ein Konto ein, das über die Berechtigung zum Hinzufügen eines Computers zur Domäne verfügt. Um den Computer neu zu starten, geben Sie den folgenden Befehl ein, und drücken Sie die Eingabetaste.
>
> `Restart-Computer`

##### <a name="to-join-computers-running-windows-10-to-the-domain"></a>So fügen Sie Computer mit Windows 10 der Domäne hinzu

1.  Melden Sie sich bei dem Computer mit dem lokalen Administratorkonto an.

2.  Geben Sie in **Web und Windows durchsuchen** **System**ein. Klicken Sie in den Suchergebnissen auf **System (Systemsteuerung)** . Das Dialogfeld **System** wird geöffnet.

3.  Klicken Sie unter **System**auf **Erweiterte System Einstellungen**. Das Dialogfeld **Systemeigenschaften** wird geöffnet. Klicken Sie auf die Registerkarte **Computer Name** .

4.  Klicken Sie unter **Computer Name**auf **ändern**. Das Dialogfeld **Ändern des Computernamens bzw. der Domäne** wird geöffnet.

5.  Klicken Sie in **Computer Namen-bzw. Domänen Änderungen** unter **Mitglied von**auf **Domäne**, und geben Sie dann den Namen der Domäne ein, der Sie beitreten möchten. Wenn Ihre Domäne beispielsweise %%amp;quot;corp.contoso.com%%amp;quot; heißt, geben Sie **corp.contoso.com** ein.

6.  Klicken Sie auf **OK**. Das Dialogfeld **Windows-Sicherheit** wird geöffnet.

7.  Geben Sie im Dialogfeld **Ändern des Computernamens bzw. der Domäne** im Feld **Benutzername** den Benutzernamen und im Feld **Kennwort** das Kennwort ein, und klicken Sie auf **OK**. Das Dialogfeld **Ändern des Computernamens bzw. der Domäne** wird geöffnet, und Sie werden bei der Domäne begrüßt. Klicken Sie auf **OK**.

8.  Im Dialogfeld **Ändern des Computernamens bzw. der Domäne** wird eine Meldung angezeigt, dass der Computer neu gestartet werden muss, damit die Änderungen wirksam werden. Klicken Sie auf **OK**.

9. Klicken Sie im Dialogfeld **Systemeigenschaften** auf der Registerkarte **Computername** auf **Schließen**. Das Dialogfeld **Microsoft Windows** wird geöffnet und zeigt erneut die Meldung an, dass der Computer neu gestartet werden muss, damit die Änderungen wirksam werden. Klicken Sie auf **Jetzt neu starten**.

##### <a name="to-join-computers-running-windows-81-to-the-domain"></a>So fügen Sie Computer mit Windows 8.1 der Domäne hinzu

1.  Melden Sie sich bei dem Computer mit dem lokalen Administratorkonto an.

2.  Klicken Sie mit der rechten Maustaste auf **Start**und dann auf **System**. Das Dialogfeld **System** wird geöffnet.

3.  Klicken Sie unter **System**auf **Erweiterte System Einstellungen**. Das Dialogfeld **Systemeigenschaften** wird geöffnet. Klicken Sie auf die Registerkarte **Computer Name** .

4.  Klicken Sie unter **Computer Name**auf **ändern**. Das Dialogfeld **Ändern des Computernamens bzw. der Domäne** wird geöffnet.

5.  Klicken Sie in **Computer Namen-bzw. Domänen Änderungen** unter **Mitglied von**auf **Domäne**, und geben Sie dann den Namen der Domäne ein, der Sie beitreten möchten. Wenn Ihre Domäne beispielsweise %%amp;quot;corp.contoso.com%%amp;quot; heißt, geben Sie **corp.contoso.com** ein.

6.  Klicken Sie auf **OK**. Das Dialogfeld **Windows-Sicherheit** wird geöffnet.

7.  Geben Sie im Dialogfeld **Ändern des Computernamens bzw. der Domäne** im Feld **Benutzername** den Benutzernamen und im Feld **Kennwort** das Kennwort ein, und klicken Sie auf **OK**. Das Dialogfeld **Ändern des Computernamens bzw. der Domäne** wird geöffnet, und Sie werden bei der Domäne begrüßt. Klicken Sie auf **OK**.

8.  Im Dialogfeld **Ändern des Computernamens bzw. der Domäne** wird eine Meldung angezeigt, dass der Computer neu gestartet werden muss, damit die Änderungen wirksam werden. Klicken Sie auf **OK**.

9. Klicken Sie im Dialogfeld **Systemeigenschaften** auf der Registerkarte **Computername** auf **Schließen**. Das Dialogfeld **Microsoft Windows** wird geöffnet und zeigt erneut die Meldung an, dass der Computer neu gestartet werden muss, damit die Änderungen wirksam werden. Klicken Sie auf **Jetzt neu starten**.

##### <a name="to-log-on-to-the-domain-using-computers-running-windows-10"></a>So melden Sie sich bei der Domäne mithilfe von Windows 10-Computern an

1.  Melden Sie den Computer ab, oder starten Sie ihn neu.

2.  Drücken Sie STRG+ALT+ENTF. Der Anmeldebildschirm wird angezeigt.

3.  Klicken Sie in der unteren linken Ecke auf **anderer Benutzer**.

4.  Geben Sie im Feld **Benutzername** Ihre Domäne und Ihren Benutzernamen im Format *Domäne\Benutzer* ein. Um sich beispielsweise bei der Domäne %%amp;quot;corp.contoso.com%%amp;quot; mit dem Konto **Benutzer-01** anzumelden, geben Sie **CORP\Benutzer-01** ein.

5.  Geben Sie im Feld **Kennwort** das Domänenkennwort ein, und klicken Sie auf den Pfeil, oder drücken Sie die EINGABETASTE.

### <a name="BKMK_optionalfeatures"></a>Bereitstellen optionaler Features für die Netzwerk Zugriffs Authentifizierung und Webdienste
Wenn Sie Netzwerk Zugriffs Server wie drahtlos Zugriffspunkte oder VPN-Server bereitstellen möchten, sollten Sie nach der Installation des Kern Netzwerks sowohl einen NPS als auch einen Webserver bereitstellen. Bei Bereitstellung von Netzwerkzugriff wird empfohlen, sichere, zertifikatbasierte Authentifizierungsmethoden zu verwenden. Mithilfe von NPS können Sie Netzwerkzugriffsrichtlinien verwalten und sichere Authentifizierungsmethoden bereitstellen. Sie können einen Webserver verwenden, um die Zertifikatsperrliste der Zertifizierungsstelle zu veröffentlichen, die Zertifikate für die sichere Authentifizierung bereitstellt.

> [!NOTE]
> Mithilfe der Begleithandbücher zum Hauptnetzwerk können Sie Serverzertifikate und andere zusätzliche Features bereitstellen. Weitere Informationen finden Sie unter [Weitere technische Ressourcen](#BKMK_resources).

In der folgenden Abbildung wird die Windows Server Core-Netzwerktopologie mit hinzugefügten NPS und Webservern veranschaulicht.

![Windows Server Core-Netzwerktopologie mit hinzugefügten NPS und Webservern](../media/Core-Network-Guide/cng16_overview_2.jpg)

Die folgenden Abschnitte enthalten Informationen zum Hinzufügen von NPS- und Webserver zum Netzwerk.

-   [Bereitstellen von NPS1](#BKMK_deployNPS1)

-   [Bereitstellen von WEB1](#BKMK_IIS)

#### <a name="BKMK_deployNPS1"></a>Bereitstellen von NPS1
Der Netzwerkrichtlinienserver (Network Policy Server, NPS) wird als vorbereitende Maßnahme zur Bereitstellung anderer Netzwerktechnologien installiert, beispielsweise VPN-Server (Virtual Private Network), Drahtloszugriffspunkte und 802.1X-Authentifizierungsswitches.

Mit dem Netzwerk Richtlinien Server (Network Policy Server, NPS) können Sie Netzwerk Richtlinien mithilfe der folgenden Features zentral konfigurieren und verwalten: Remote Authentication Dial-in User Service (RADIUS)-Server und RADIUS-Proxy.

NPS ist eine optionale Komponente eines Hauptnetzwerks, Sie sollten NPS jedoch installieren, wenn eine der folgenden Voraussetzungen zutrifft:

-   Sie planen die Erweiterung Ihres Netzwerks auf RAS-Server, die mit dem RADIUS-Protokoll kompatibel sind, z. b. einen Computer mit Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 und Routing-und RAS-Dienst, Terminal Dienste-Gateway oder Remotedesktop Gateway.


-   Sie planen die Bereitstellung der 802.1 x-Authentifizierung für Kabel-oder drahtlos Zugriff.

Bevor Sie diesen Rollen Dienst bereitstellen, müssen Sie die folgenden Schritte auf dem Computer ausführen, den Sie als NPS konfigurieren.

-   Führen Sie die Schritte im Abschnitt [Konfigurieren aller Server](#BKMK_configuringAll) aus.

-   Führen Sie die Schritte im Abschnitt [Hinzufügen von Servercomputern zur Domäne und Anmelden](#BKMK_joinlogserver) aus.

Während der Bereitstellung von NPS1, bei dem es sich um den Computer handelt, auf dem der Rollendienst %%amp;quot;Netzwerkrichtlinienserver%%amp;quot; (Network Policy Server, NPS) der Serverrolle %%amp;quot;Netzwerkrichtlinien- und Zugriffsdienste%%amp;quot; ausgeführt wird, müssen Sie folgende Schritte ausführen:

-   [Planen der Bereitstellung von NPS1](#bkmk_NetFndtn_Pln_NPS-01)

-   [Netzwerk Richtlinien Server (NPS) installieren](#BKMK_installNPS)

-   [Registrieren des NPS in der Standard Domäne](#BKMK_registerNPS)

> [!NOTE]
> Dieses Handbuch enthält Anweisungen zum Bereitstellen von NPS auf einem eigenständigen Server oder virtuellen Computer mit dem Namen NPS1.  Ein weiteres empfohlenes Bereitstellungs Modell ist die Installation von NPS auf einem Domänen Controller. Wenn Sie NPS bevorzugen, anstatt auf einem eigenständigen Server auf einem Domänen Controller zu installieren, installieren Sie NPS auf DC1.

##### <a name="bkmk_NetFndtn_Pln_NPS-01"></a>Planen der Bereitstellung von NPS1
Wenn Sie nach der Bereitstellung Ihres Hauptnetzwerks Netzwerkzugriffsserver bereitstellen möchten, beispielsweise drahtlose Zugriffspunkte oder VPN-Server, sollten Sie NPS bereitstellen.

Wenn Sie NPS als RADIUS-Server (Remote Authentication Dial-In User Service) verwenden, führt NPS die Authentifizierung und Autorisierung für Verbindungsanforderungen über Ihre Netzwerkzugriffsserver aus. NPS ermöglicht darüber hinaus eine zentrale Konfiguration und Verwaltung von Netzwerkrichtlinien, die festlegen, wer auf das Netzwerk zugreifen kann, wie auf das Netzwerk zugegriffen werden kann, und wann auf das Netzwerk zugegriffen werden kann.

Im Anschluss finden Sie die wichtigsten Planungsschritte vor der Installation von NPS.

- Planen der Benutzerkontendatenbank. Wenn Sie den Server, auf dem NPS ausgeführt wird, einer Active Directory Domäne hinzufügen, führt NPS standardmäßig die Authentifizierung und Autorisierung mithilfe der AD DS Benutzerkonten Datenbank aus. In einigen Fällen, beispielsweise in großen Netzwerken, die NPS als RADIUS-Proxy für die Weiterleitung von Verbindungsanforderungen an andere RADIUS-Server weiterleiten, können Sie NPS auch auf Computern installieren, die keine Domänenmitglieder sind.

- Planen der RADIUS-Kontoführung. NPS ermöglicht die Protokollierung von Ressourcenerfassungsdaten in einer SQL Server-Datenbank oder in einer Textdatei auf dem lokalen Computer. Wenn Sie SQL Server-Protokollierung verwenden möchten, planen Sie die Installation und Konfiguration Ihres Servers, auf dem SQL Server ausgeführt wird.

##### <a name="BKMK_installNPS"></a>Netzwerk Richtlinien Server (NPS) installieren
Mithilfe dieses Verfahrens können Sie den Netzwerk Richtlinien Server (Network Policy Server, NPS) mithilfe des Assistenten zum Hinzufügen von Rollen und Features installieren. NPS ist ein Rollendienst der Serverrolle Netzwerkrichtlinien- und Zugriffsdienste.

> [!NOTE]
> Standardmäßig überwacht NPS RADIUS-Datenverkehr auf den Ports 1812, 1813, 1645 und 1646 für alle installierten Netzwerkadapter. Wenn die Windows-Firewall mit erweiterter Sicherheit bei der Installation von NPS aktiviert ist, werden während des Installationsvorgangs automatisch Firewallausnahmen für diese Ports für die Internet Protokollversion 6 \(IPv6-\) und IPv4-Verkehr erstellt. Wenn Ihre Netzwerk Zugriffs Server für das Senden von RADIUS-Datenverkehr über andere Ports als diese Standardeinstellungen konfiguriert sind, entfernen Sie die Ausnahmen, die bei der NPS-Installation unter Windows-Firewall mit erweiterter Sicherheit erstellt wurden, und erstellen Sie Ausnahmen für die Ports, die Sie für RADIUS-Datenverkehr.

**Administrator Anmelde Informationen**

Zur Ausführung dieses Verfahrens müssen Sie ein Mitglied der Gruppe **Domänen-Admins** sein.

> [!NOTE]
> Um dieses Verfahren mithilfe von Windows PowerShell durchzuführen, öffnen Sie PowerShell, geben Sie Folgendes ein, und drücken Sie dann die Eingabetaste.
>
> `Install-WindowsFeature NPAS -IncludeManagementTools`

###### <a name="to-install-nps"></a>So installieren Sie NPS

1.  Klicken Sie auf NPS1 unter Server-Manager auf **Verwalten** und dann auf **Rollen und Features hinzufügen**. Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet.

2.  Klicken Sie auf der Seite **Vorbemerkungen** auf **Weiter**.

    > [!NOTE]
    > Die Seite **Vorbemerkungen** im Assistenten zum Hinzufügen von Rollen und Features wird nicht angezeigt, wenn Sie bei einer früheren Ausführung des Assistenten die Option **Seite standardmäßig überspringen** ausgewählt haben.

3.  Wählen Sie unter **Installationstyp auswählen** die Option **Rollenbasierte oder featurebasierte Installation** aus, und klicken Sie dann auf **Weiter**.

4.  Stellen Sie sicher, dass unter **Zielserver auswählen** die Option **Einen Server aus dem Serverpool auswählen** aktiviert ist. Wählen Sie unter **Serverpool** den lokalen Computer aus. Klicken Sie auf **Weiter**.

5.  Wählen Sie unter **Server Rollen auswählen**unter **Rollen**die Option **Netzwerk Richtlinien-und Zugriffs Dienste**aus. Es wird ein Dialogfeld geöffnet, in dem Sie gefragt werden, ob für Netzwerk Richtlinien-und Zugriffs Dienste erforderliche Features hinzugefügt werden sollen. Klicken Sie auf **Features hinzufügen**und dann auf **Weiter**.

6.  Klicken Sie unter **Features auswählen** auf **Weiter**, überprüfen Sie unter **Netzwerkrichtlinien- und Zugriffsdienste** die angegebenen Informationen, und klicken Sie dann auf **Weiter**.

7.  Klicken Sie unter **Rollendienste auswählen** auf **Netzwerkrichtlinienserver**.  Klicken Sie unter **Sollen für Netzwerkrichtlinienserver erforderliche Features hinzugefügt werden?** auf **Features hinzufügen**. Klicken Sie auf **Weiter**.

8.  Klicken Sie unter **Installationsauswahl bestätigen** auf **Zielserver bei Bedarf automatisch neu starten**. Wenn Sie aufgefordert werden, die Auswahl zu bestätigen, klicken Sie auf **Ja** und dann auf **Installieren**. Auf der Seite %%amp;quot;Installationsstatus%%amp;quot; wird der Status während der Installation angezeigt. Wenn der Vorgang abgeschlossen ist, wird die Meldung "Installation erfolgreich auf *Computername*" angezeigt, wobei *Computername* der Name des Computers ist, auf dem Sie den Netzwerk Richtlinien Server installiert haben. Klicken Sie auf **Schließen**.

##### <a name="BKMK_registerNPS"></a>Registrieren des NPS in der Standard Domäne
Mit diesem Verfahren können Sie einen NPS in der Domäne registrieren, in der der Server ein Domänen Mitglied ist.

NPSS muss in Active Directory registriert werden, damit Sie über die Berechtigung zum Lesen der Einwähleigenschaften von Benutzerkonten während des Autorisierungs Vorgangs verfügen. Beim Registrieren eines NPS wird der Server der Gruppe " **RAS-und IAS-Server** " in Active Directory hinzugefügt.

**Administrator Anmelde Informationen**

Zur Ausführung dieses Verfahrens müssen Sie ein Mitglied der Gruppe **Domänen-Admins** sein.

> [!NOTE]
> Um dieses Verfahren mithilfe von Network Shell (Netsh)-Befehlen in Windows PowerShell auszuführen, öffnen Sie PowerShell, geben Sie Folgendes ein, und drücken Sie dann die EINGABETASTE.
>
> `netsh nps add registeredserver domain=corp.contoso.com server=NPS1.corp.contoso.com`

###### <a name="to-register-an-nps-in-its-default-domain"></a>So registrieren Sie einen NPS in seiner Standard Domäne

1.  Klicken Sie auf NPS1 unter Server-Manager auf %%amp;quot;Extras%%amp;quot; und dann auf **Netzwerkrichtlinienserver**. Das MMC-Snap-In %%amp;quot;Netzwerkrichtlinienserver%%amp;quot; wird geöffnet.

2.  Klicken Sie mit der rechten Maustaste auf **NPS (Lokal)** , und klicken Sie dann auf **Server in Active Directory registrieren**. Das Dialogfeld **Netzwerkrichtlinienserver** wird geöffnet.

3.  Klicken Sie im Dialogfeld **Netzwerkrichtlinienserver** auf **OK**, und klicken Sie erneut auf **OK**.

Weitere Informationen zum Netzwerk Richtlinien Server finden Sie unter [Netzwerk Richtlinien Server (Network Policy Server, NPS)](../technologies/nps/nps-top.md).

#### <a name="BKMK_IIS"></a>Bereitstellen von WEB1

Die Rolle "Webserver (IIS)" in Windows Server 2016 bietet eine sichere, einfach zu verwaltende, modulare und erweiterbare Plattform für das zuverlässige Hosting von Websites, Diensten und Anwendungen. Mit Internetinformationsdienste (IIS) können Sie Informationen für Benutzer im Internet, in einem Intranet oder in einem Extranet freigeben. IIS ist eine einheitliche Webplattform, die IIS, ASP.net, FTP-Dienste, PHP und Windows Communication Foundation (WCF) integriert.

Mit der Server Rolle "Webserver (IIS)" können Sie nicht nur eine CRL für den Zugriff durch Domänen Mitglieds Computer veröffentlichen, sondern auch mehrere Websites, Webanwendungen und FTP-Sites einrichten und verwalten. IIS bietet außerdem die folgenden Vorteile:

-   Maximale Websicherheit durch einen reduzierten Serverspeicherbedarf und automatischer Anwendungsisolation

-   Einfaches Bereitstellen und Ausführen von ASP.NET, klassischem ASP und PHP-Webanwendungen auf demselben Server

-   Anwendungsisolation durch standardmäßiges Zuteilen einer eindeutigen Identität und Sandbox-Konfiguration zu Arbeitsprozessen zur weiteren Reduzierung von Sicherheitsrisiken

-   Einfaches Hinzufügen, Entfernen und sogar Ersetzen von integrierten IIS-Komponenten durch benutzerdefinierte, an Kundenanforderungen angepasste Module

-   Beschleunigte Websites durch integriertes dynamisches Zwischenspeichern und erweiterte Komprimierung

Zum Bereitstellen von WEB1 (des Computers, auf dem die Serverrolle %%amp;quot;Webserver (IIS)%%amp;quot; ausgeführt wird) müssen folgende Schritte ausgeführt werden:

-   Führen Sie die Schritte im Abschnitt [Konfigurieren aller Server](#BKMK_configuringAll) aus.

-   Führen Sie die Schritte im Abschnitt [Hinzufügen von Servercomputern zur Domäne und Anmelden](#BKMK_joinlogserver) aus.

-   [Installieren der Server Rolle "Webserver (IIS)"](#BKMK_install_IIS)

##### <a name="BKMK_install_IIS"></a>Installieren der Server Rolle "Webserver (IIS)"
Sie müssen Mitglied der Gruppe **Administratoren** sein, um diesen Vorgang auszuführen.

> [!NOTE]
> Um dieses Verfahren mithilfe von Windows PowerShell durchzuführen, öffnen Sie PowerShell, geben Sie Folgendes ein, und drücken Sie dann die Eingabetaste.
>
> `Install-WindowsFeature Web-Server -IncludeManagementTools`

1.  Klicken Sie im **Server-Manager** auf **Verwalten** und dann auf **Rollen und Features hinzufügen**. Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet.

2.  Klicken Sie auf der Seite **Vorbemerkungen** auf **Weiter**.

    > [!NOTE]
    > Die Seite **Vorbemerkungen** im Assistenten zum Hinzufügen von Rollen und Features wird nicht angezeigt, wenn Sie bei einer früheren Ausführung des Assistenten die Option **Seite standardmäßig überspringen** ausgewählt haben.

3.  Klicken Sie auf der Seite **Installationstyp auswählen** auf **weiter**.

4.  Vergewissern Sie sich auf der Seite **Zielserver auswählen** , dass der lokale Computer ausgewählt ist, und klicken Sie dann auf **weiter**.

5.  Scrollen Sie auf der Seite **Server Rollen auswählen** zu, und wählen Sie **Webserver (IIS)** aus. Das Dialogfeld **Features hinzufügen, die für den Webserver (IIS) erforderlich sind, wird** geöffnet. Klicken Sie auf **Features hinzufügen**und dann auf **Weiter**.

6.  Klicken Sie auf **Weiter**, bis Sie alle Standardeinstellungen für Webserver akzeptiert haben, und klicken Sie dann auf **Installieren**.

7.  Stellen Sie sicher, dass alle Installationen erfolgreich waren, und klicken Sie dann auf **Schließen**.

## <a name="BKMK_resources"></a>Weitere technische Ressourcen
Weitere Informationen zu den Technologien in diesem Handbuch finden Sie in den folgenden Ressourcen:

 Ressourcen für die technische Bibliothek von Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012

-   [Neues in Active Directory Domain Services (AD DS) unter Windows Server 2016](https://technet.microsoft.com/library/mt163897.aspx)

-   [Active Directory Domain Services Übersicht](https://technet.microsoft.com/library/hh831484.aspx) unter https://technet.microsoft.com/library/hh831484.aspx.

-   [Übersicht über Domain Name System (DNS)](https://technet.microsoft.com/library/hh831667.aspx) unter https://technet.microsoft.com/library/hh831667.aspx.

-   [Implementieren der Rolle "DNS-Administratoren"](https://technet.microsoft.com/library/cc756152(WS.10).aspx)

-   [Übersicht über das Dynamic Host Configuration-Protokoll (DHCP)](https://technet.microsoft.com/library/hh831825.aspx) unter https://technet.microsoft.com/library/hh831825.aspx.

-   [Übersicht über Netzwerk Richtlinien-und Zugriffs Dienste](https://technet.microsoft.com/library/hh831683.aspx) unter https://technet.microsoft.com/library/hh831683.aspx.

-   [Übersicht über Webserver (IIS)](https://technet.microsoft.com/library/hh831725.aspx) unter https://technet.microsoft.com/library/hh831725.aspx.

## <a name="BKMK_appendix"></a>Fügt A durch E ein.
Die folgenden Abschnitte enthalten zusätzliche Konfigurationsinformationen für Computer, auf denen andere Betriebssysteme als Windows Server 2016, Windows 10, Windows Server 2012 und Windows 8 ausgeführt werden. Außerdem wird ein Arbeitsblatt für die netzwerkvorbereitung bereitgestellt, um Sie bei der Bereitstellung zu unterstützen.

1.  [Anhang A: Umbenennen von Computern](#BKMK_A)

2.  [Anhang B: Konfigurieren statischer IP-Adressen](#BKMK_B)

3.  [Anhang C: Hinzufügen von Computern zur Domäne](#BKMK_C)

4.  [Anhang D: Anmelden bei der Domäne](#BKMK_D)

5.  [Anhang E-zentrales Netzwerk Planungs Vorbereitungs Blatt](#BKMK_E)

## <a name="BKMK_A"></a>Anhang A: Umbenennen von Computern
Mithilfe der Verfahren in diesem Abschnitt können Sie Computern, auf denen Windows Server 2008 R2, Windows 7, Windows Server 2008 und Windows Vista ausgeführt wird, einen anderen Computernamen bereitstellen.

-   [Windows Server 2008 R2 und Windows 7](#bkmk_NetFndtn_Pln_rename_R2)

-   [Windows Server 2008 und Windows Vista](#bkmk_NetFndtn_Pln_Renam08)

### <a name="bkmk_NetFndtn_Pln_rename_R2"></a>Windows Server 2008 R2 und Windows 7
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um diese Verfahren ausführen zu können.

##### <a name="to-rename-computers-running-windows-server-2008-r2-and-windows-7"></a>So benennen Sie Computer unter Windows Server 2008 R2 und Windows 7 um

1.  Klicken Sie auf **Start**und mit der rechten Maustaste auf **Computer**und klicken Sie dann auf **Eigenschaften**. Das Dialogfeld **System** wird geöffnet.

2.  Klicken Sie unter **Einstellungen für Computernamen, Domäne und Arbeitsgruppe** auf **Einstellungen ändern**. Das Dialogfeld **Systemeigenschaften** wird geöffnet.

    > [!NOTE]
    > Auf Computern mit Windows 7 wird vor dem Öffnen des Dialog Felds **System Eigenschaften** das Dialogfeld **Benutzerkontensteuerung** geöffnet, in dem die Berechtigung zum Fortfahren angefordert wird. Klicken Sie auf **Weiter**, um fortzufahren.

3.  Klicken Sie auf **Ändern**. Das Dialogfeld **Ändern des Computernamens bzw. der Domäne** wird geöffnet.

4.  Geben Sie im Feld **Computername** einen Namen für den Computer ein. Wenn Sie dem Computer beispielsweise den Namen DC1 geben möchten, geben Sie **DC1** ein.

5.  Klicken Sie zweimal auf **OK** und dann auf **Schließen**. Klicken Sie dann auf **Jetzt neu starten**, um den Computer neu zu starten.

### <a name="bkmk_NetFndtn_Pln_Renam08"></a>Windows Server 2008 und Windows Vista
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um diese Verfahren ausführen zu können.

##### <a name="to-rename-computers-running-windows-server-2008-and-windows-vista"></a>So benennen Sie Computer unter Windows Server 2008 und Windows Vista um

1.  Klicken Sie auf **Start**und mit der rechten Maustaste auf **Computer**und klicken Sie dann auf **Eigenschaften**. Das Dialogfeld **System** wird geöffnet.

2.  Klicken Sie unter **Einstellungen für Computernamen, Domäne und Arbeitsgruppe** auf **Einstellungen ändern**. Das Dialogfeld **Systemeigenschaften** wird geöffnet.

    > [!NOTE]
    > Auf Computern, auf denen Windows Vista ausgeführt wird, wird vor dem Öffnen des Dialog Felds **System Eigenschaften** das Dialogfeld **Benutzerkontensteuerung** geöffnet, das die Berechtigung zum Fortfahren anfordert. Klicken Sie auf **Weiter**, um fortzufahren.

3.  Klicken Sie auf **Ändern**. Das Dialogfeld **Ändern des Computernamens bzw. der Domäne** wird geöffnet.

4.  Geben Sie im Feld **Computername** einen Namen für den Computer ein. Wenn Sie dem Computer beispielsweise den Namen DC1 geben möchten, geben Sie **DC1** ein.

5.  Klicken Sie zweimal auf **OK** und dann auf **Schließen**. Klicken Sie dann auf **Jetzt neu starten**, um den Computer neu zu starten.

## <a name="BKMK_B"></a>Anhang B: Konfigurieren statischer IP-Adressen
In diesem Thema werden Verfahren zur Konfiguration von statischen IP-Adressen auf Computern unter den folgenden Betriebssystemen erläutert:

-   [Windows Server 2008 R2](#bkmk_R2Cng_WS08R2IP)

-   [Windows Server 2008](#bkmk_NetFndtn_Pln_CfgStatic08)

### <a name="bkmk_R2Cng_WS08R2IP"></a>Windows Server 2008 R2
Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.

##### <a name="to-configure-a-static-ip-address-on-a-computer-running-windows-server-2008-r2"></a>So konfigurieren Sie eine statische IP-Adresse auf einem Computer unter Windows Server 2008 R2

1.  Klicken Sie auf **Start** und dann auf **Systemsteuerung**.

2.  Klicken Sie in der Systemsteuerung auf**Netzwerk und Internet**. **Netzwerk und Internet** wird geöffnet.

    Klicken Sie in **Netzwerk und Internet** auf **Netzwerk- und Freigabecenter**. **Netzwerk- und Freigabecenter** wird geöffnet.

3.  Klicken Sie in **Netzwerk- und Freigabecenter** auf **Adaptereinstellungen ändern**. **Netzwerkverbindungen** wird geöffnet.

4.  Klicken Sie in **Netzwerkverbindungen** mit der rechten Maustaste auf die zu konfigurierende Netzwerkverbindung, und klicken Sie dann auf **Eigenschaften**.

5.  Wählen Sie unter **Eigenschaften von LAN-Verbindung** in **Diese Verbindung verwendet folgende Elemente** **Internetprotokoll Version 4 (TCP/IPv4)** aus, und klicken Sie dann auf **Eigenschaften**. Das Dialogfeld **Eigenschaften von Internetprotokoll Version 4 (TCP/IPv4)** wird geöffnet.

6.  Klicken Sie in **Eigenschaften von Internetprotokoll Version 4 (TCP/IPv4)** auf der Registerkarte **Allgemein** auf **Folgende IP-Adresse verwenden**. Geben Sie in **IP-Adresse** die IP-Adresse ein, die Sie verwenden möchten.

7.  Drücken Sie die Tabulatortaste, um mit dem Cursor in das Feld **Subnetzmaske** zu wechseln. Es wird automatisch ein Standardwert für die Subnetzmaske eingefügt. Übernehmen Sie entweder die Standardsubnetzmaske, oder geben Sie die gewünschte Subnetzmaske ein.

8.  Geben Sie im Feld **Standardgateway** die IP-Adresse des Standardgateways ein.

9. Geben Sie im Feld **Bevorzugter DNS-Server** die IP-Adresse des DNS-Servers ein. Wenn Sie den lokalen Computer als bevorzugten DNS-Server verwenden möchten, geben Sie die IP-Adresse des lokalen Computers ein.

10. Geben Sie gegebenenfalls im Feld **Alternativer DNS-Server** die IP-Adresse des alternativen DNS-Servers ein. Wenn Sie den lokalen Computer als alternativen DNS-Server verwenden möchten, geben Sie die IP-Adresse des lokalen Computers ein.

11. Klicken Sie auf **OK** und dann auf **Schließen**.

### <a name="bkmk_NetFndtn_Pln_CfgStatic08"></a>Windows Server 2008
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um diese Verfahren ausführen zu können.

##### <a name="to-configure-a-static-ip-address-on-a-computer-running-windows-server-2008"></a>So konfigurieren Sie eine statische IP-Adresse auf einem Computer unter Windows Server 2008

1.  Klicken Sie auf **Start** und dann auf **Systemsteuerung**.

2.  Stellen Sie sicher, dass in der Systemsteuerungdie **Klassische Ansicht** ausgewählt ist, und doppelklicken Sie auf **Netzwerk- und Freigabecenter**.

3.  Klicken Sie im **Netzwerk- und Freigabecenter** unter **Aufgaben** auf **Netzwerkverbindungen verwalten**.

4.  Klicken Sie in **Netzwerkverbindungen** mit der rechten Maustaste auf die zu konfigurierende Netzwerkverbindung, und klicken Sie dann auf **Eigenschaften**.

5.  Wählen Sie unter **Eigenschaften von LAN-Verbindung** in **Diese Verbindung verwendet folgende Elemente** **Internetprotokoll Version 4 (TCP/IPv4)** aus, und klicken Sie dann auf **Eigenschaften**. Das Dialogfeld **Eigenschaften von Internetprotokoll Version 4 (TCP/IPv4)** wird geöffnet.

6.  Klicken Sie in **Eigenschaften von Internetprotokoll Version 4 (TCP/IPv4)** auf der Registerkarte **Allgemein** auf **Folgende IP-Adresse verwenden**. Geben Sie in **IP-Adresse** die IP-Adresse ein, die Sie verwenden möchten.

7.  Drücken Sie die Tabulatortaste, um mit dem Cursor in das Feld **Subnetzmaske** zu wechseln. Es wird automatisch ein Standardwert für die Subnetzmaske eingefügt. Übernehmen Sie entweder die Standardsubnetzmaske, oder geben Sie die gewünschte Subnetzmaske ein.

8.  Geben Sie im Feld **Standardgateway** die IP-Adresse des Standardgateways ein.

9. Geben Sie im Feld **Bevorzugter DNS-Server** die IP-Adresse des DNS-Servers ein. Wenn Sie den lokalen Computer als bevorzugten DNS-Server verwenden möchten, geben Sie die IP-Adresse des lokalen Computers ein.

10. Geben Sie gegebenenfalls im Feld **Alternativer DNS-Server** die IP-Adresse des alternativen DNS-Servers ein. Wenn Sie den lokalen Computer als alternativen DNS-Server verwenden möchten, geben Sie die IP-Adresse des lokalen Computers ein.

11. Klicken Sie auf **OK** und dann auf **Schließen**.

## <a name="BKMK_C"></a>Anhang C: Hinzufügen von Computern zur Domäne
Mit diesen Verfahren können Sie Computern, auf denen Windows Server 2008 R2, Windows 7, Windows Server 2008 und Windows Vista ausgeführt wird, der Domäne beitreten.

-   [Windows Server 2008 R2 und Windows 7](#BKMK_c1)

-   [Windows Server 2008 und Windows Vista](#BKMK_c2)

> [!IMPORTANT]
> Um einen Computer zu einer Domäne hinzufügen zu können, müssen Sie bei dem Computer mit dem lokalen Konto Administrator angemeldet sein. Wenn Sie mit einem Benutzerkonto angemeldet sind, das nicht über administrative Anmeldeinformationen für den lokalen Computer verfügt, müssen Sie die Anmeldeinformationen für das lokale Konto Administrator angeben, wenn Sie den Computer zu der Domäne hinzufügen. Außerdem müssen Sie über ein Benutzerkonto in der Domäne verfügen, der Sie den Computer hinzufügen möchten. Während der Hinzufügung des Computers zu der Domäne werden Sie zur Angabe der Anmeldeinformationen für Ihr Domänenkonto aufgefordert (Benutzername und Kennwort).

### <a name="BKMK_c1"></a>Windows Server 2008 R2 und Windows 7
Sie müssen mindestens Mitglied der Gruppe **Domänen-Benutzer** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.

##### <a name="to-join-computers-running-windows-server-2008-r2-and-windows-7-to-the-domain"></a>So fügen Sie Computer, auf denen Windows Server 2008 R2 und Windows 7 ausgeführt wird, der Domäne hinzu

1.  Melden Sie sich bei dem Computer mit dem lokalen Administratorkonto an.

2.  Klicken Sie auf **Start**und mit der rechten Maustaste auf **Computer**und klicken Sie dann auf **Eigenschaften**. Das Dialogfeld **System** wird geöffnet.

3.  Klicken Sie unter **Einstellungen für Computernamen, Domäne und Arbeitsgruppe** auf **Einstellungen ändern**. Das Dialogfeld **Systemeigenschaften** wird geöffnet.

    > [!NOTE]
    > Auf Computern mit Windows 7 wird vor dem Öffnen des Dialog Felds **System Eigenschaften** das Dialogfeld **Benutzerkontensteuerung** geöffnet, in dem die Berechtigung zum Fortfahren angefordert wird. Klicken Sie auf **Weiter**, um fortzufahren.

4.  Klicken Sie auf **Ändern**. Das Dialogfeld **Ändern des Computernamens bzw. der Domäne** wird geöffnet.

5.  Wählen Sie im Dialogfeld **Computername** unter **Mitglied von** die Option **Domäne** aus, und geben Sie den Namen der Domäne ein, der der Computer hinzugefügt werden soll. Wenn Ihre Domäne beispielsweise %%amp;quot;corp.contoso.com%%amp;quot; heißt, geben Sie **corp.contoso.com** ein.

6.  Klicken Sie auf **OK**. Das Dialogfeld **Windows-Sicherheit** wird geöffnet.

7.  Geben Sie im Dialogfeld **Ändern des Computernamens bzw. der Domäne** im Feld **Benutzername** den Benutzernamen und im Feld **Kennwort** das Kennwort ein, und klicken Sie auf **OK**. Das Dialogfeld **Ändern des Computernamens bzw. der Domäne** wird geöffnet, und Sie werden bei der Domäne begrüßt. Klicken Sie auf **OK**.

8.  Im Dialogfeld **Ändern des Computernamens bzw. der Domäne** wird eine Meldung angezeigt, dass der Computer neu gestartet werden muss, damit die Änderungen wirksam werden. Klicken Sie auf **OK**.

9. Klicken Sie im Dialogfeld **Systemeigenschaften** auf der Registerkarte **Computername** auf **Schließen**. Das Dialogfeld **Microsoft Windows** wird geöffnet und zeigt erneut die Meldung an, dass der Computer neu gestartet werden muss, damit die Änderungen wirksam werden. Klicken Sie auf **Jetzt neu starten**.

### <a name="BKMK_c2"></a>Windows Server 2008 und Windows Vista
Sie müssen mindestens Mitglied der Gruppe **Domänen-Benutzer** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.

##### <a name="to-join-computers-running-windows-server-2008-and-windows-vista-to-the-domain"></a>So fügen Sie Computer, auf denen Windows Server 2008 und Windows Vista ausgeführt wird, der Domäne hinzu

1.  Melden Sie sich bei dem Computer mit dem lokalen Administratorkonto an.

2.  Klicken Sie auf **Start**und mit der rechten Maustaste auf **Computer**und klicken Sie dann auf **Eigenschaften**. Das Dialogfeld **System** wird geöffnet.

3.  Klicken Sie unter **Einstellungen für Computernamen, Domäne und Arbeitsgruppe** auf **Einstellungen ändern**. Das Dialogfeld **Systemeigenschaften** wird geöffnet.

4.  Klicken Sie auf **Ändern**. Das Dialogfeld **Ändern des Computernamens bzw. der Domäne** wird geöffnet.

5.  Wählen Sie im Dialogfeld **Computername** unter **Mitglied von** die Option **Domäne** aus, und geben Sie den Namen der Domäne ein, der der Computer hinzugefügt werden soll. Wenn Ihre Domäne beispielsweise %%amp;quot;corp.contoso.com%%amp;quot; heißt, geben Sie **corp.contoso.com** ein.

6.  Klicken Sie auf **OK**. Das Dialogfeld **Windows-Sicherheit** wird geöffnet.

7.  Geben Sie im Dialogfeld **Ändern des Computernamens bzw. der Domäne** im Feld **Benutzername** den Benutzernamen und im Feld **Kennwort** das Kennwort ein, und klicken Sie auf **OK**. Das Dialogfeld **Ändern des Computernamens bzw. der Domäne** wird geöffnet, und Sie werden bei der Domäne begrüßt. Klicken Sie auf **OK**.

8.  Im Dialogfeld **Ändern des Computernamens bzw. der Domäne** wird eine Meldung angezeigt, dass der Computer neu gestartet werden muss, damit die Änderungen wirksam werden. Klicken Sie auf **OK**.

9. Klicken Sie im Dialogfeld **Systemeigenschaften** auf der Registerkarte **Computername** auf **Schließen**. Das Dialogfeld **Microsoft Windows** wird geöffnet und zeigt erneut die Meldung an, dass der Computer neu gestartet werden muss, damit die Änderungen wirksam werden. Klicken Sie auf **Jetzt neu starten**.

## <a name="BKMK_D"></a>Anhang D: Anmelden bei der Domäne
Mithilfe dieser Verfahren können Sie sich bei der Domäne mithilfe von Computern anmelden, auf denen Windows Server 2008 R2, Windows 7, Windows Server 2008 und Windows Vista ausgeführt wird.

-   [Windows Server 2008 R2 und Windows 7](#BKMK_d1)

-   [Windows Server 2008 und Windows Vista](#BKMK_d2)

### <a name="BKMK_d1"></a>Windows Server 2008 R2 und Windows 7
Sie müssen mindestens Mitglied der Gruppe **Domänen-Benutzer** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.

##### <a name="log-on-to-the-domain-using-computers-running-windows-server-2008-r2-and-windows-7"></a>Anmelden bei der Domäne mithilfe von Computern, auf denen Windows Server 2008 R2 und Windows 7 ausgeführt wird

1.  Melden Sie den Computer ab, oder starten Sie ihn neu.

2.  Drücken Sie STRG+ALT+ENTF. Der Anmeldebildschirm wird angezeigt.

3.  Klicken Sie auf **Benutzer wechseln** und dann auf **Anderer Benutzer**.

4.  Geben Sie im Feld **Benutzername** Ihre Domäne und Ihren Benutzernamen im Format *Domäne\Benutzer* ein. Um sich beispielsweise bei der Domäne %%amp;quot;corp.contoso.com%%amp;quot; mit dem Konto **Benutzer-01** anzumelden, geben Sie **CORP\Benutzer-01** ein.

5.  Geben Sie im Feld **Kennwort** das Domänenkennwort ein, und klicken Sie auf den Pfeil, oder drücken Sie die EINGABETASTE.

### <a name="BKMK_d2"></a>Windows Server 2008 und Windows Vista
Sie müssen mindestens Mitglied der Gruppe **Domänen-Benutzer** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.

##### <a name="log-on-to-the-domain-using-computers-running-windows-server-2008-and-windows-vista"></a>Anmelden bei der Domäne mithilfe von Computern, auf denen Windows Server 2008 und Windows Vista ausgeführt wird

1.  Melden Sie den Computer ab, oder starten Sie ihn neu.

2.  Drücken Sie STRG+ALT+ENTF. Der Anmeldebildschirm wird angezeigt.

3.  Klicken Sie auf **Benutzer wechseln** und dann auf **Anderer Benutzer**.

4.  Geben Sie im Feld **Benutzername** Ihre Domäne und Ihren Benutzernamen im Format *Domäne\Benutzer* ein. Um sich beispielsweise bei der Domäne %%amp;quot;corp.contoso.com%%amp;quot; mit dem Konto **Benutzer-01** anzumelden, geben Sie **CORP\Benutzer-01** ein.

5.  Geben Sie im Feld **Kennwort** das Domänenkennwort ein, und klicken Sie auf den Pfeil, oder drücken Sie die EINGABETASTE.

## <a name="BKMK_E"></a>Anhang E-zentrales Netzwerk Planungs Vorbereitungs Blatt
Sie können dieses Vorbereitungsblatt für die Netzwerkplanung verwenden, um die für die Installation eines Hauptnetzwerks erforderlichen Informationen zu erfassen. Dieses Thema enthält Tabellen, die die einzelnen Konfigurationselemente für jeden Server enthalten, für den Sie während des Installations- oder Konfigurationsprozess Informationen oder bestimmte Werte angeben müssen. Für jedes Konfigurationselement werden Beispielwerte angegeben.

Für die Planung und Nachverfolgung enthält jede Tabelle Leerzellen, in die Sie die für Ihre Bereitstellung verwendeten Werte eingeben können. Wenn Sie in diesen Tabellen sicherheitsspezifische Werte erfassen, sollten Sie die Daten an einem sicheren Ort aufbewahren.

Über die folgenden Links wechseln Sie zu den Abschnitten in diesem Thema, in denen Konfigurationselemente und Beispielwerte für die in dieser Anleitung erläuterten Bereitstellungsverfahren bereitgestellt werden.

1.  [Installieren von Active Directory Domain Services und DNS](#BKMK_FndtnPrep_InstallAD)

    -   [Konfigurieren einer DNS-Reverse-Lookupzone](#BKMK_FndtnPrep_DNSRevrsLook)

2.  [Installieren von DHCP](#BKMK_FndtnPrep_InstallDHCP)

    -   [Erstellen eines Ausschluss Bereichs in DHCP](#BKMK_FndtnPrep_DHCP_Exclusn)

    -   [Erstellen eines neuen DHCP-Bereichs](#bkmk_NetFndtn_Pln_DHCP_NewScope)

3.  [Installieren des Netzwerk Richtlinien Servers (optional)](#BKMK_FndtnPrep_InstallNPS)

### <a name="BKMK_FndtnPrep_InstallAD"></a>Installieren von Active Directory Domain Services und DNS
In den Tabellen in diesem Abschnitt sind die Konfigurationselemente für die Vorinstallation und die Installation von Active Directory Domain Services (AD DS) und DNS aufgeführt.

##### <a name="pre-installation-configuration-items-for-ad-ds-and-dns"></a>Konfigurationselemente für AD DS und DNS vor der Installation
Die folgenden Tabellen enthalten Konfigurationselemente für die Vorbereitung der Installation, wie in [Konfigurieren aller Server](#BKMK_configuringAll) erläutert:

-   [Konfigurieren einer statischen IP-Adresse](#BKMK_ip)

|Konfigurationselemente|Beispielwerte|Werte|
|-----------------------|------------------|----------|
|IP-Adresse|10.0.0.2||
|Subnetzmaske|255.255.255.0||
|Standardgateway|10.0.0.1||
|Bevorzugter DNS-Server|127.0.0.1||
|Alternativer DNS-Server|10.0.0.15||

-   [Umbenennen des Computers](#BKMK_rename)

|Konfigurationselement|Beispielwert|Wert|
|----------------------|-----------------|---------|
|Computername|DC1||

##### <a name="ad-ds-and-dns-installation-configuration-items"></a>Konfigurationselemente für AD DS und DNS-Installation
Konfigurationselemente für das Bereitstellungsverfahren für das Windows Server-Hauptnetzwerk[Installieren von AD DS und DNS für eine neue Gesamtstruktur](#BKMK_installAD-DNS):

|Konfigurationselemente|Beispielwerte|Werte|
|-----------------------|------------------|----------|
|Vollständiger DNS-Name|corp.contoso.com||
|Gesamtstrukturfunktionsebene|Windows Server 2003||
|Speicherort des AD DS-Datenbankordners|E:\konfigurations\\<br /><br />Oder übernehmen Sie den Standardspeicherort.||
|Speicherort des AD DS-Protokolldateiordners|E:\konfigurations\\<br /><br />Oder übernehmen Sie den Standardspeicherort.||
|Speicherort des AD DS-SYSVOL-Ordners|E:\konfigurations\\<br /><br />Oder übernehmen Sie den Standardspeicherort.||
|Administratorkennwort für den Verzeichnisdienst-Wiederherstellungsmodus|J*p2leO4$F||
|Name der Antwortdatei (optional)|AD-DS_AnswerFile||

#### <a name="BKMK_FndtnPrep_DNSRevrsLook"></a>Konfigurieren einer DNS-Reverse-Lookupzone

|Konfigurationselemente|Beispielwerte|Werte|
|-----------------------|------------------|----------|
|Zonentyp:|-Primäre Zone<br />-Sekundäre Zone<br />-Stub-Zone||
|Zonentyp<br /><br />**Speichern Sie die Zone in Active Directory**|-Ausgewählt<br />-Nicht ausgewählt||
|Active Directory-Zonenreplikationsbereich|-Auf alle DNS-Server in dieser Gesamtstruktur<br />-Auf alle DNS-Server in dieser Domäne<br />-Auf alle Domänen Controller in dieser Domäne<br />-Zu allen Domänen Controllern, die im Gültigkeitsbereich dieser Verzeichnis Partition angegeben sind||
|Name der Reverse-Lookupzone<br /><br />(IP-Typ)|-IPv4-Reverse-Lookupzone<br />-IPv6-Reverse-Lookupzone||
|Name der Reverse-Lookupzone<br /><br />(Netzwerk-ID)|10.0.0||

### <a name="BKMK_FndtnPrep_InstallDHCP"></a>Installieren von DHCP
Die Tabellen in diesem Abschnitt enthalten Konfigurationselemente für die Installationsvorbereitung und die Installation von DHCP.

##### <a name="pre-installation-configuration-items-for-dhcp"></a>Konfigurationselemente für die Vorbereitung der Installation von DHCP
Die folgenden Tabellen enthalten Konfigurationselemente für die Vorbereitung der Installation, wie in [Konfigurieren aller Server](#BKMK_configuringAll) erläutert:

-   [Konfigurieren einer statischen IP-Adresse](#BKMK_ip)

|Konfigurationselemente|Beispielwerte|Werte|
|-----------------------|------------------|----------|
|IP-Adresse|10.0.0.3||
|Subnetzmaske|255.255.255.0||
|Standardgateway|10.0.0.1||
|Bevorzugter DNS-Server|10.0.0.2||
|Alternativer DNS-Server|10.0.0.15||

-   [Umbenennen des Computers](#BKMK_rename)

|Konfigurationselement|Beispielwert|Wert|
|----------------------|-----------------|---------|
|Computername|DHCP1||

##### <a name="dhcp-installation-configuration-items"></a>Konfigurationselemene für die DHCP-Installation
Konfigurationselemente für das Bereitstellungsverfahren für das Windows Server-Hauptnetzwerk[Installieren von Dynamic Host Configuration-Protokoll (DHCP)](#BKMK_installDHCP):

|Konfigurationselemente|Beispielwerte|Werte|
|-----------------------|------------------|----------|
|Bindungen für die Netzwerkverbindung|Ethernet||
|DNS-Servereinstellungen|DC1||
|Bevorzugte IP-Adresse des DNS-Servers|10.0.0.2||
|IP-Adresse des alternativen DNS-Servers|10.0.0.15||
|Bereichsname|Corp1||
|Start-IP-Adresse|10.0.0.1||
|End-IP-Adresse|10.0.0.254||
|Subnetzmaske|255.255.255.0||
|Standardgateway (optional)|10.0.0.1||
|Leasedauer|8 Tage||
|Betriebsmodus des IPv6-DHCP-Servers|Nicht aktiviert||

#### <a name="BKMK_FndtnPrep_DHCP_Exclusn"></a>Erstellen eines Ausschluss Bereichs in DHCP
Konfigurationselemente zum Erstellen eines Ausschlussbereichs beim Erstellen eines Bereichs in DHCP.

|Konfigurationselemente|Beispielwerte|Werte|
|-----------------------|------------------|----------|
|Bereichsname|Corp1||
|Beschreibung des Bereichs|Subnetz 1 der Zentrale||
|Start-IP-Adresse des Ausschlussbereichs|10.0.0.1||
|End-IP-Adresse des Ausschlussbereichs|10.0.0.15||

#### <a name="bkmk_NetFndtn_Pln_DHCP_NewScope"></a>Erstellen eines neuen DHCP-Bereichs
Konfigurationselemente für das Bereitstellungsverfahren für das Windows Server-Hauptnetzwerk[Erstellen und Aktivieren eines neuen DHCP-Bereichs](#BKMK_newscopeDHCP):

|Konfigurationselemente|Beispielwerte|Werte|
|-----------------------|------------------|----------|
|Name des neuen Bereichs|Corp2||
|Beschreibung des Bereichs|Hauptbüro-Subnetz 2||
|(IP-Adressbereich)<br /><br />Start-IP-Adresse|10.0.1.1||
|(IP-Adressbereich)<br /><br />IP-Endadresse|10.0.1.254||
|Länge|8||
|Subnetzmaske|255.255.255.0||
|Start-IP-Adresse (Ausschlussbereich)|10.0.1.1||
|End-IP-Adresse des Ausschlussbereichs|10.0.1.15||
|Leasedauer<br /><br />Days<br /><br />Stunden<br /><br />Minuten|-8<br />-   0<br />-   0||
|Router (Standardgateway)<br /><br />IP-Adresse|10.0.1.1||
|Übergeordnete DNS-Domäne|corp.contoso.com||
|DNS-Server<br /><br />IP-Adresse|10.0.0.2||

### <a name="BKMK_FndtnPrep_InstallNPS"></a>Installieren des Netzwerk Richtlinien Servers (optional)
Die Tabellen in diesem Abschnitt enthalten Konfigurationselemente für die Installationsvorbereitung und die Installation von NPS.

##### <a name="pre-installation-configuration-items"></a>Konfigurationselemene für die Installationsvorbereitung
Die folgende Tabelle enthält Konfigurationselemente für die Vorbereitung der Installation, wie in [Konfigurieren aller Server](#BKMK_configuringAll) erläutert:

-   [Konfigurieren einer statischen IP-Adresse](#BKMK_ip)

|Konfigurationselemente|Beispielwerte|Werte|
|-----------------------|------------------|----------|
|IP-Adresse|10.0.0.4||
|Subnetzmaske|255.255.255.0||
|Standardgateway|10.0.0.1||
|Bevorzugter DNS-Server|10.0.0.2||
|Alternativer DNS-Server|10.0.0.15||

-   [Umbenennen des Computers](#BKMK_rename)

|Konfigurationselement|Beispielwert|Wert|
|----------------------|-----------------|---------|
|Computername|NPS1||

##### <a name="network-policy-server-installation-configuration-items"></a>Konfigurationselemente für die Installation des Netzwerkrichtlinienservers
Konfigurationselemente für die NPS-Bereitstellungs Prozeduren des Windows Server Core-Netzwerks [installieren den Netzwerk Richtlinien Server (NPS)](#BKMK_installNPS) und [registrieren den NPS in der Standard Domäne](#BKMK_registerNPS).

-   Für die Installation und Registrierung von NPS sind keine weiteren Konfigurationselemente erforderlich.

