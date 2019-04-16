---
title: Handbuch zum Hauptnetzwerk
description: Dieses Handbuch enthält Anweisungen zum Planen und Bereitstellen der Kernkomponenten für eine einwandfreie Verwendung des Netzwerks und eine neue Active Directory-Domäne in einer neuen Gesamtstruktur mit Windows Server2016 erforderlich
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: b3cd60f7-d380-4712-9a78-0a8f551e1121
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 90390a7b975bc358fb96715d23fe542bc261220e
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="core-network-guide"></a>Handbuch zum Hauptnetzwerk

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Handbuch enthält Anweisungen zum Planen und Bereitstellen der Kernkomponenten für eine einwandfreie Verwendung des Netzwerks und eine neue Active Directory-Domäne in einer neuen Gesamtstruktur erforderlich.

> [!NOTE]
> Dieses Handbuch ist in Microsoft Word-Format in TechNet-Galerie heruntergeladen. Weitere Informationen finden Sie unter [Core Network Guide für Windows Server2016](https://gallery.technet.microsoft.com/Core-Network-Guide-for-9da2e683).

Dieses Handbuch enthält die folgenden Abschnitte.

- [Informationen zum Handbuch](#BKMK_about)

- [Hauptnetzwerk – Übersicht](#BKMK_overview)

- [Hauptnetzwerk – Planung](#BKMK_planning)

- [Hauptnetzwerk – Bereitstellung](#BKMK_deployment)

- [Zusätzliche technische Ressourcen](#BKMK_resources)

- [Anhänge A bis E](#BKMK_appendix)

## <a name="BKMK_about"></a>Informationen zum Handbuch
Dieses Handbuch richtet sich an Netzwerk- und Systemadministratoren, die ein neues Netzwerk installieren oder einen domänenbasierten Netzwerks um ein Netzwerk zu ersetzen, die aus Arbeitsgruppen bestehendes erstellen möchten. In diesem Handbuch Bereitstellungsszenario ist besonders nützlich, wenn Sie erwarten, dass weitere Dienste und Features mit dem Netzwerk in der Zukunft hinzufügen müssen.

Es wird empfohlen, dass Sie überprüfen des Entwurfs und für jede der Technologien in diesem Bereitstellungsszenario verwendet werden bereitstellungsanleitungen, um zu ermitteln, ob dieses Handbuch enthält die Dienste und Konfigurationen, die Sie benötigen.

Ein Hauptnetzwerk ist eine Sammlung von Netzwerkhardware, Geräten und Software, die die grundlegenden Dienste für Ihre Organisation Informationstechnologie (IT) muss.

Ein Windows Server-Hauptnetzwerk bietet Ihnen zahlreiche Vorteile, z. b.

-   Kern-Protokolle für Netzwerkkonnektivität zwischen Computern und anderen (TCP/IP, Transmission Control Protocol/Internet Protocol) kompatible Geräte. TCP/IP ist eine Suite von Standardprotokollen für die Verbindung von Computern und Netzwerken erstellen. TCP/IP ist eine Netzwerkprotokollsoftware mit Microsoft-Windows-Betriebssystemen bereitgestellt, die implementiert und die TCP/IP-Protokollsuite unterstützt.

-   Dynamic Host Configuration Protocol (DHCP) automatische IP-Adresszuweisung für Computer und andere Geräte, die als DHCP-Clients konfiguriert sind. Die manuelle Konfiguration von IP-Adressen auf allen Computern in Ihrem Netzwerk ist zeitaufwändig und weniger flexibel als die dynamische Bereitstellung von Computern und anderen Geräten mit IP-Adresskonfiguration ein DHCP-Server.

-   Domain Name System (DNS) Name Resolution-Diensts. Mit DNS können Benutzer, Computer, Anwendungen und Dienste die IP-Adressen von Computern und Geräten im Netzwerk zu suchen, mit dem vollqualifizierten Domänennamen des Computers oder Geräts.

-   Eine Gesamtstruktur, also eine oder mehrere Active Directory-Domänen, die gleichen Klassen- und Attributdefinitionen (Schema), Standort und Replikationsinformationen (Konfiguration) und gesamtstrukturweite Suchfunktionen (globaler Katalog) gemeinsam nutzen.

-   Eine Gesamtstruktur-Stammdomäne, die erste Domäne wird, die in einer neuen Gesamtstruktur erstellt werden. Die Organisations-Admins und Schema-Admins-Gruppen, die gesamtstrukturweite Administratorgruppen handelt, befinden sich in der Gesamtstruktur-Stammdomäne. Darüber hinaus ist eine Gesamtstruktur-Stammdomäne, wie bei anderen Domänen eine Sammlung von Computer-, Benutzer- und Gruppenobjekten, die vom Administrator in Active Directory-Domänendienste (AD DS) definiert sind. Diese Objekte verwenden eine gemeinsame Verzeichnis Verzeichnisdatenbank und gemeinsame Sicherheitsrichtlinien. Sie können auch sicherheitsbeziehungen mit anderen Domänen freigeben, wenn Sie Domänen hinzufügen, wenn Ihre Organisation wächst. Der Verzeichnisdienst speichert Verzeichnisdaten auch und kann autorisierten Computern, Anwendungen und Benutzer auf die Daten zugreifen.

-   Eine Benutzer- und Datenbank. Der Verzeichnisdienst stellt eine zentralisierte Benutzerkontendatenbank, mit dem Sie zum Erstellen von Benutzer- und Computerkonten für Personen und Computer, die autorisiert sind, eine Verbindung zu Ihrem Netzwerk und den Zugriff auf das Netzwerk Ressourcen, z.B. Anwendungen, Datenbanken, freigegebene Dateien und Ordner und Drucker.

Ein Hauptnetzwerk können Sie das Netzwerk zu skalieren, wie Ihr Unternehmen wächst und IT-Anforderungen ändern. Mit einem Hauptnetzwerk können Sie beispielsweise Domänen, IP-Subnetze, RAS-Dienste, Drahtlosdienste und andere Features und Serverrollen, die von Windows Server2016 bereitgestellten hinzufügen.

### <a name="network-hardware-requirements"></a>Anforderungen an die Netzwerkhardware
Um erfolgreich ein Hauptnetzwerk bereitstellen, müssen Sie die Netzwerkhardware, u. a. folgende bereitstellen:

-   Ethernet-, Fast Ethernet- oder Gigabyte Ethernet-Kabel

-   Ein Hub, Schicht-2 oder 3-Switch, Router oder anderen Geräten, die Funktion der Netzwerkdatenverkehr zwischen Computern und Geräten erfüllt.

-   Computer, die die mindesthardwareanforderungen für die jeweiligen Client und Server-Betriebssysteme erfüllen.

## <a name="what-this-guide-does-not-provide"></a>Was dieses Handbuch bietet keine
Dieses Handbuch bietet keine Anweisungen für folgende:

-   Netzwerkhardware wie Kabel, Router, Switches und Hubs

-   Zusätzliche Netzwerkressourcen wie Drucker und Dateiserver

-   Internetkonnektivität

-   Remotezugriff

-   Drahtlosen Zugriff

-   Bereitstellung von Clientcomputern

> [!NOTE]
> Computer mit Windows-Clientbetriebssysteme sind standardmäßig für den Empfang von IP-Adressleases vom DHCP-Server konfiguriert. Daher keine weitere DHCP- oder Internetprotokoll Version 4 (IPv4) ist die Konfiguration der Clientcomputer erforderlich.

## <a name="technology-overviews"></a>Technologieübersichten
Die folgenden Abschnitte enthalten eine kurze Übersicht über die erforderlichen Technologien, die zur Erstellung eines Hauptnetzwerks bereitgestellt werden.

### <a name="active-directory-domain-services"></a>Active Directory-Domänendienste
Ein Verzeichnis ist eine hierarchische Struktur, die Informationen zu Objekten im Netzwerk, z.B. Benutzer und -Computer gespeichert. Ein Verzeichnisdienst wie AD DS enthält die Methoden für die Speicherung von Verzeichnisdaten und diese Daten für Netzwerkbenutzer und Administratoren zur Verfügung stellen. Z.B. AD DS speichert Informationen über Benutzerkonten wie Namen, E-Mail-Adressen, Kennwörter und Telefonnummern und ermöglicht anderen autorisierten Benutzern im selben Netzwerk auf diese Informationen zuzugreifen.

### <a name="dns"></a>DNS
DNS ist ein Namensauflösungsprotokoll für TCP/IP-Netzwerke, z.B. dem Internet oder einem Unternehmensnetzwerk. Ein DNS-Server hostet die Informationen, die von Clientcomputern und leicht gelöst erkannt, alphanumerische DNS-Namen zu IP-Adressen, mit dem Computer miteinander kommunizieren.

### <a name="dhcp"></a>DHCP
DHCP ist ein IP-Standard für die Vereinfachung der Verwaltung der Host-IP-Konfiguration. Der DHCP-Standard bietet für die Verwendung von DHCP-Servern als eine Möglichkeit zum dynamischen Zuweisung von IP-Adressen und sonstiger zugehöriger Konfigurationsdetails für DHCP Clients im Netzwerk zu verwalten.

DHCP ermöglicht Ihnen die Verwendung ein DHCP-Servers dynamisch zuweisen einer IP-Adresse auf einem Computer oder einem anderen Gerät wie einen Drucker in Ihrem lokalen Netzwerk. Alle Computer in einem TCP/IP-Netzwerk benötigen eine eindeutige IP-Adresse, da die IP-Adresse und die zugehörige Subnetzmaske identifizieren, der Host-PC und das Subnetz, mit dem der Computer verbunden ist. Mithilfe von DHCP können Sie sicherstellen, dass alle Computer, die als DHCP-Clients konfiguriert sind, IP-Adresse erhalten, die für die Netzwerkadresse und das Subnetz geeignet ist, und Sie können mithilfe von DHCP-Optionen wie Standardgateway und DNS-Server automatisch DHCP-Clients bereitstellen, mit den Informationen, den sie benötigen in Ihrem Netzwerk ordnungsgemäß funktioniert.

TCP/IP-basierten Netzwerken verringert DHCP die Komplexität und den Umfang von Verwaltungsaufgaben, die bei der Neukonfiguration von Computern.

### <a name="tcpip"></a>TCP/IP
TCP/IP in Windows Server2016 ist Folgendes:

-   Eine Netzwerksoftware basierend auf Industriestandard-Netzwerkprotokolle.

-   Ein Routingfähiges Netzwerkprotokoll, die die Verbindung Ihres Windows-basierten Computers auf lokalen Netzwerks (LAN) und wide Area Network (WAN)-Umgebungen unterstützt.

-   Kerntechnologien und Hilfsprogramme für die Verbindung Ihres Windows-Computers mit anderen Systemen zum Austausch von Daten.

-   Eine Grundlage für den Zugriff auf globale Internetdienste, wie das World Wide Web und File Transfer Protocol (FTP).

-   Ein zuverlässiges, skalierbares und plattformübergreifendes Client-/Server-Framework.

TCP/IP bietet grundlegende TCP/IP-Dienstprogramme, mit denen Windows-basierten Computern eine Verbindung herstellen und Freigeben von Informationen mit anderen Microsoft- und Nicht-Microsoft-Systemen, einschließlich:

-    Windows Server 2016

-   Windows10

-    Windows Server2012 R2

-   Windows 8.1

-    Windows Server 2012

-   Windows 8

-    Windows Server2008 R2

-    Windows 7

-    Windows Server 2008

-   Windowsvista

-   Internet-Hosts

-   Apple Macintosh-Systeme

-   IBM mainframes

-   UNIX- und Linux-Systeme

-   Open VMS-Systeme

-   Netzwerkfähige Drucker

-   Tablets und Handys mit kabelgebundenen Ethernet oder drahtlose 802.11-Technologie aktiviert

## <a name="BKMK_overview"></a>Hauptnetzwerk – Übersicht
Die folgende Abbildungzeigt die Windows Server-Hauptnetzwerk Topologie.

![Windows Server Core-Netzwerktopologie](../media/Core-Network-Guide/cng16_overview.jpg)

> [!NOTE]
> Dieses Handbuch enthält auch Anweisungen zum Hinzufügen von optionalen (Network Policy Server, NPS) und den Webserver (IIS)-Servern zur Netzwerktopologie als Grundlage für sichere netzwerkzugriffslösungen wie 802.1 X verkabelte und kabellose 802.1X-Bereitstellungen, die Sie mithilfe der Begleithandbücher zum Core implementiert werden können. Weitere Informationen finden Sie unter [Bereitstellen von optionalen Features für die Netzwerkzugriffsauthentifizierung und Webdienste](#BKMK_optionalfeatures).

### <a name="core-network-components"></a>Komponenten des Hauptnetzwerks
Im folgenden werden die Komponenten eines Hauptnetzwerks.

##### <a name="router"></a>Router
Dieses Bereitstellungshandbuch enthält Anweisungen zum Bereitstellen eines Hauptnetzwerks mit zwei Subnetzen, getrennt durch einen Router, der DHCP-Weiterleitung aktiviert wurde. Sie können jedoch eine Schicht 2-Switch, einen Schicht 3-Switch oder einen Hub, je nach Ihren Anforderungen und Ressourcen bereitstellen. Wenn Sie einen Switch bereitstellen, muss der Switch der DHCP-Weiterleitung oder platzieren Sie einen DHCP-Server auf jedem Subnetz. Wenn Sie einen Hub bereitstellen, wird Sie ein einzelnes Subnetz bereitstellen und DHCP-Weiterleitung oder einen zweiten Bereich nicht auf dem DHCP-Server erforderlich.

##### <a name="static-tcpip-configurations"></a>Statische TCP/IP-Konfigurationen
Die Server in dieser Bereitstellung sind mit statischen IPv4-Adressen konfiguriert. Clientcomputer werden standardmäßig für den Empfang von IP-Adressleases vom DHCP-Server konfiguriert.

##### <a name="active-directory-domain-services-global-catalog-and-dns-server-dc1"></a>Globalen Katalog mit Active Directory-Domänendienste und DNS-Server DC1
Sowohl mit der Active Directory-Domänendienste (AD DS) und Domain Name System (DNS) auf dem Server, mit dem Namen DC1, und dadurch Verzeichnis installiert sind, und Namensauflösungsdienste für alle Computer und Geräte im Netzwerk.

##### <a name="dhcp-server-dhcp1"></a>DHCP-Server DHCP1
Der DHCP-Server, mit dem Namen DHCP1 ist mit einem Bereich konfiguriert, IP (Internet Protocol)-Adressleases für Computer im lokalen Subnetz bereitstellt. Der DHCP-Server kann auch konfiguriert werden, mit zusätzlichen Bereichen zu IP-Adressleases für Computer in anderen Subnetzen bereitzustellen, wenn DHCP-Weiterleitung auf Routern konfiguriert ist.

##### <a name="client-computers"></a>Clientcomputern
Computer mit Windows-Clientbetriebssysteme werden standardmäßig als DHCP-Clients konfiguriert die IP-Adressen und DHCP-Optionen automatisch vom DHCP-Server erhalten.

## <a name="BKMK_planning"></a>Hauptnetzwerk – Planung
Bevor Sie ein Hauptnetzwerk bereitstellen, müssen Sie die folgenden Elemente planen.

-   [Planen der Subnetze](#bkmk_NetFndtn_Pln_Subnt)

-   [Planen der Basiskonfiguration aller Server](#bkmk_NetFndtn_Pln_AllSrvrs)

-   [Planen der Bereitstellung von DC1](#bkmk_NetFndtn_Pln_AD-DNS-01)

-   [Planen des domänenzugriffs](#bkmk_NetFndtn_Pln_DomAccess)

-   [Planen der Bereitstellung von DHCP1](#bkmk_NetFndtn_Pln_DHCP-01)

Die folgenden Abschnitte enthalten weitere Detail für jedes dieser Elemente.

> [!NOTE]
> Bei der Planung Ihrer Bereitstellung auch finden Sie unter [AnhangE - Core die Planung eines Hauptnetzwerks](#BKMK_E).

### <a name="bkmk_NetFndtn_Pln_Subnt"></a>Planen der Subnetze
Im Netzwerk (TCP/IP, Transmission Control Protocol/Internet Protocol) Router verwendet, um die Hardware und Software, die auf verschiedenen physischen Netzwerksegmenten Subnetze genannt interconnect. Router werden auch verwendet, um IP-Pakete zwischen den einzelnen Subnetzen weiterzuleiten. Bestimmen Sie das physische Layout Ihres Netzwerks, einschließlich der Anzahl der Router und Subnetze, die Sie, die bevor Sie mit den Anweisungen in dieser Anleitung fortfahren benötigen.

Um die Server in Ihrem Netzwerk mit statischen IP-Adressen zu konfigurieren, müssen Sie darüber hinaus den IP-Adressbereich festlegen, den für das Subnetz verwenden, in denen Ihres Hauptnetzwerks befinden sollen. In diesem Handbuch werden die privaten IP-Adressbereiche 10.0.0.1 – 10.0.0.254 und 10.0.1.1 - 10.0.1.254 als Beispiel verwendet, jedoch können Sie alle privaten IP-Adressbereich, den Sie bevorzugen.

> [!IMPORTANT]
> Nachdem Sie die IP-Adressbereiche ausgewählt haben, die Sie für jedes Subnetz verwenden möchten, stellen Sie sicher, dass die IP-Adresse aus der gleichen IP-Adressbereich, die im Subnetz verwendet werden, auf dem der Router installiert ist, konfigurieren Sie Ihre Router. Beispielsweise müssen, wenn der Router ist standardmäßig mit der IP-Adresse 192.168.1.1 konfiguriert, aber Sie den Router in einem Subnetz mit einem IP-Adressbereich von 10.0.0.0/24 installieren, Sie den Router eine IP-Adresse aus dem 10.0.0.0/24 IP-Adressbereich verwenden neu konfigurieren.

Die folgenden erkannten privaten IP-Bereiche durch die Internet Request for Comments (RFC) 1918 angegeben werden:

-   10.0.0.0 - 10.255.255.255

-   172.16.0.0 - 172.31.255.255

-   192.168.0.0 - 192.168.255.255

Beim Sie die privaten IP-Adressbereiche gemäß RFC 1918 verwenden, verbinden Sie können nicht direkt mit dem Internet über eine private IP-Adresse, da Anforderungen an diese oder von diesen Adressen automatisch von Internet Service Provider (ISP) Router verworfen werden. Um die Internetkonnektivität des Hauptnetzwerks hinzufügen müssen später, Sie mit einem Internetdienstanbieter eine öffentliche IP-Adresse Vertrag.

> [!IMPORTANT]
> Wenn Sie private IP-Adressen verwenden, müssen Sie eine Art von Proxys oder Server Network Address Translation (NAT) verwenden, um die privaten IP-Adressbereiche in Ihrem lokalen Netzwerk in eine öffentliche IP-Adresse zu konvertieren, die im Internet weitergeleitet werden kann. Die meisten Router bieten NAT-Dienste so ziemlich einfach, wählen einen Router, der NAT-fähig ist sein soll.

Weitere Informationen finden Sie unter [Planen der Bereitstellung von DHCP1](#bkmk_NetFndtn_Pln_DHCP-01).

### <a name="bkmk_NetFndtn_Pln_AllSrvrs"></a>Planen der Basiskonfiguration aller Server
Für jeden Server im Kernnetzwerk durchführen müssen Sie Umbenennen des Computers und zuweisen und konfigurieren Sie eine statische IPv4-Adresse und andere TCP/IP-Eigenschaften für den Computer.

#### <a name="planning-naming-conventions-for-computers-and-devices"></a>Planen von Namenskonventionen für Computer und Geräte
Um die Konsistenz in Ihrem Netzwerk ist es sinnvoll, konsistente Namen für Server, Drucker und anderen Geräten verwenden. Computernamen können verwendet werden, damit Benutzer und Administratoren den Zweck und den Speicherort, von dem Server, Drucker oder ein anderes Gerät einfach identifizieren. Wenn beispielsweise Sie über drei DNS-Server, einen in San Francisco, Los Angeles und Chicago haben, können die Namenskonvention *Server-Funktion*-*Speicherort*-*Anzahl*:

-   DNS-DEN-01. Dieser Name steht für den DNS-Server in Denver, Colorado. Wenn in Denver, zusätzliche DNS-Server hinzugefügt werden, im Namen der numerische Wert erhöht werden, beispielsweise DNS-DEN-02 und DNS-DEN-03.

-   DNS-SPAS-01. Dieser Name steht für den DNS-Server in South Pasadena, Kalifornien.

-   DNS-ORL-01. Dieser Name steht für den DNS-Server in Orlando, Florida, USA.

Für diese Anleitung wird der Benennungskonvention für Server ist sehr einfach und besteht aus der primären Serverfunktion und eine Zahl. Beispielsweise der Domänencontroller ist mit dem Namen DC1, und der DHCP-Server wird mit dem Namen DHCP1.

Es wird empfohlen, dass Sie vor der Installation des Hauptnetzwerks mithilfe dieses Handbuchs eine Benennungskonvention auszuwählen.

#### <a name="planning-static-ip-addresses"></a>Planen von statischen IP-Adressen
Bevor Sie jeden Computer mit einer statischen IP-Adresse konfiguriert haben, müssen Sie Ihre Subnetz- und IP-Adressbereiche planen. Darüber hinaus müssen Sie die IP-Adressen Ihrer DNS-Server ermitteln. Wenn Sie einen Router installieren, der auf andere Netzwerke wie Weitere Subnetze oder das Internet zugreifen möchten, müssen Sie die IP-Adresse des Routers, auch bezeichnet als Standardgateway für statische IP-Adresskonfiguration kennen.

Die folgende Tabelle enthält Beispielwerte für die Konfiguration von statischen IP-Adresse.

|Konfigurationselemente|Beispielwerte|
|-----------------------|------------------|
|IP-Adresse|10.0.0.2|
|Subnetzmaske|255.255.255.0|
|Standardgateway (Router-IP-Adresse)|10.0.0.1|
|Bevorzugter DNS-Server|10.0.0.2|

> [!NOTE]
> Wenn Sie mehr als ein DNS-Server bereitstellen möchten, können Sie auch die alternativen DNS-Server-IP-Adresse planen.

### <a name="bkmk_NetFndtn_Pln_AD-DNS-01"></a>Planen der Bereitstellung von DC1
Folgendes sind die wichtigsten Planungsschritte vor der Installation von Active Directory-Domänendienste (AD DS) und DNS auf DC1.

#### <a name="planning-the-name-of-the-forest-root-domain"></a>Planen den Namen der Stammdomäne der Gesamtstruktur
Ein erster Schrittbeim Entwerfen der AD DS ist zu bestimmen, wie viele Gesamtstrukturen Ihre Organisation erforderlich ist. Eine Gesamtstruktur ist der AD DS-Container der obersten Ebene und besteht aus einer oder mehreren Domänen, die ein gemeinsames Schema und globalen Katalog gemeinsam nutzen. Eine Organisation kann mehrere Gesamtstrukturen besitzen, aber in den meisten Unternehmen ist ein Gesamtstruktur-Entwurf vorzuziehen und am einfachsten zu verwalten.

Wenn Sie den ersten Domänencontroller in Ihrer Organisation erstellen, erstellen Sie die erste Domäne (auch als Stammdomäne der Gesamtstruktur bezeichnet) und die erste Gesamtstruktur. Bevor Sie diesen Schrittmithilfe dieser Anleitung nutzen, jedoch müssen Sie den geeignetsten Domänennamen für Ihre Organisation bestimmen. In den meisten Fällen ist der Name des Unternehmens mit dem Namen der Domäne verwendet und in vielen Fällen ist dieser Domänenname registriert. Wenn Sie planen, Bereitstellen von externen Internet-basierten Webservern, um Informationen und Services für Ihre Kunden oder Partner, wählen einen Domänennamen, der noch nicht verwendet wird, und klicken Sie dann den Domänennamen registrieren, sodass es im Besitz der Organisation.

#### <a name="planning-the-forest-functional-level"></a>Planen der Gesamtstrukturfunktionsebene
Während der Installation von AD DS, müssen Sie die Gesamtstrukturfunktionsebene auswählen, die Sie verwenden möchten. In Windows Server2003 Active Directory eingeführte Domänen- und Funktionalität bietet ein Verfahren zum Aktivieren der Domäne oder Gesamtstruktur-Wide Active Directory-Features in Ihrer Netzwerkumgebung. Es sind verschiedene Ebenen der Domänen- und Gesamtstrukturfunktionalität verfügbar ist, abhängig von Ihrer Umgebung.

Gesamtstrukturfunktionalität werden Features für alle Domänen in der Gesamtstruktur aktiviert. Die folgenden Gesamtstrukturfunktionsebenen sind verfügbar:

-    Windows Server 2008. Diese Gesamtstrukturfunktionsebene unterstützt nur Domänencontroller, auf denen Windows Server2008 und höheren Versionen des Betriebssystems Windows Server ausgeführt werden.

-    Windows Server2008 R2. Diese Gesamtstrukturfunktionsebene unterstützt Windows Server2008 R2-Domänencontroller und Domänencontrollern, auf denen spätere Versionen des Betriebssystems Windows Server ausgeführt werden.

-    Windows Server 2012. Diese Gesamtstrukturfunktionsebene unterstützt Windows Server2012-Domänencontroller und Domänencontrollern, auf denen spätere Versionen des Betriebssystems Windows Server ausgeführt werden.

-    Windows Server2012 R2. Diese Gesamtstrukturfunktionsebene unterstützt Windows Server2012 R2-Domänencontroller und Domänencontrollern, auf denen spätere Versionen des Betriebssystems Windows Server ausgeführt werden.

-    Windows Server 2016. Diese Gesamtstrukturfunktionsebene unterstützt nur Windows Server2016-Domänencontroller und Domänencontrollern, auf denen spätere Versionen des Betriebssystems Windows Server ausgeführt werden.

Wenn Sie eine neue Domäne in einer neuen Gesamtstruktur bereitstellen, und alle Domänencontroller Windows Server2016 ausgeführt werden wird, empfiehlt es sich, dass Sie AD DS mit der Gesamtstrukturfunktionsebene Windows Server2016 während der AD DS-Installation konfigurieren.

> [!IMPORTANT]
> Nachdem die Gesamtstrukturfunktionsebene ausgelöst wurde, können Domänencontroller, auf denen ältere Betriebssysteme ausgeführt werden in der Gesamtstruktur verwendet werden. Wenn Sie die Gesamtstrukturfunktionsebene auf Windows Server2016 heraufstufen, können nicht z.B. Domänencontroller unter Windows Server2012 R2 oder Windows Server2008 in der Gesamtstruktur hinzugefügt werden.

Beispiel für Konfigurationselemente für die AD DS werden in der folgenden Tabelle bereitgestellt.

|Konfigurationselemente:|Beispielwerte:|
|------------------------|-------------------|
|Vollständiger DNS-name|Beispiele:<br /><br />-corp.contoso.com<br />-example.com|
|Funktionsebene der Gesamtstruktur|– Windows Server2008 <br />– Windows Server2008 R2 <br />– Windows Server2012 <br />– Windows Server2012 R2 <br />– Windows Server2016|
|Active Directory Domain Services-Datenbank-Ordner|E:\Configuration\\<br /><br />Oder übernehmen Sie den Standardspeicherort.|
|Active Directory Domain Services-Protokoll Dateien Speicherort des Ordners|E:\Configuration\\<br /><br />Oder übernehmen Sie den Standardspeicherort.|
|Active Directory Domain Services SYSVOL-Ordner|E:\Configuration\\<br /><br />Oder übernehmen Sie den Standardspeicherort|
|Directory Wiederherstellung Administratorkennwort|**J\ * p2leO4$ F**|
|Name der Antwortdatei (optional)|**AD-DS_AnswerFile**|

#### <a name="planning-dns-zones"></a>Planen der DNS-Zonen
Auf primären, Active Directory-integrierte DNS-Servern wird Forward-Lookupzone während der Installation der DNS-Serverrolle standardmäßig erstellt. Forward-Lookupzone ermöglicht es Computern und Geräten zum Abfragen von einem anderen Computer oder Geräte IP-Adresse, die basierend auf den DNS-Namen. Zusätzlich zu einer Forward-Lookupzone empfiehlt es sich, dass Sie eine DNS-Reverse-Lookupzone erstellen. Mithilfe einer DNS-kann Reverse-Lookup-Abfrage, einen Computer oder Gerät den Namen eines anderen Computers oder Geräts anhand seiner IP-Adresse ermitteln. Bereitstellen von Reverse-Lookupzone verbessert üblicherweise die DNS-Leistung und erfolgreicheren DNS-Abfragen.

Wenn Sie eine Reverse-Lookupzone erstellen, wird die in-addr.arpa-Domäne, die in den DNS-Standards definiert und im Internet-DNS-Namespace, um eine praktische und zuverlässige Weise Rückwärtsabfragen bieten reserviert, im DNS konfiguriert. Zum Erstellen von reverse-Namespace werden untergeordnete Domänen innerhalb der Domäne in-addr.arpa gebildet verwenden, die eine umgekehrte Sortierung der Zahlen in punktierter Dezimalschreibweise von IP-Adressen.

Die Domäne in-addr.arpa gilt, für alle TCP/IP-Netzwerke, die auf Internetprotokoll Version 4 (IPv4) basieren Adressierung. Der Assistent zum Erstellen neuer Zonen setzt automatisch voraus, dass Sie diese Domäne verwenden, wenn Sie eine neue Reverse-Lookupzone erstellen.

Während Sie den Assistenten ausführen, werden die folgenden Auswahlen empfohlen:

|Konfigurationselemente|Beispielwerte|
|-----------------------|------------------|
|Zonentyp|**Primäre Zone**, und **speichern Sie die Zone in Active Directory** aktiviert ist|
|Active Directory-Zonenreplikationsbereich|**Alle DNS-Server in dieser Domäne**|
|Seite der ersten Reverse-Lookupzone Name des Assistenten|**IPv4 Reverse-Lookupzone**|
|Seite der zweiten Reverse-Lookupzone Name des Assistenten|Netzwerk-ID = 10.0.0.|
|Dynamische Updates|**Nur sichere dynamische Updates zulassen**|

### <a name="bkmk_NetFndtn_Pln_DomAccess"></a>Planen des domänenzugriffs
Um mit der Domäne anmelden zu können, muss der Computer einen Domänenmitgliedscomputer sein und muss das Benutzerkonto in AD DS vor der Anmeldung erstellt werden.

> [!NOTE]
> Einzelne Computer, auf denen Windows ausgeführt werden, haben eine lokale Benutzer und Gruppen Konto Datenbank, die die Sicherheitskontenverwaltung (Security Accounts Manager, SAM)-Benutzerkontendatenbank aufgerufen wird. Wenn Sie ein Benutzerkonto auf dem lokalen Computer in der SAM-Datenbank erstellen, können auf dem lokalen Computer protokolliert, aber Sie können einer Domäne anmelden. Domänenbenutzerkonten werden mit dem Active Directory-Benutzer und Computer Microsoft Management Console (MMC) auf einem Domänencontroller nicht mit lokalen Benutzern und Gruppen auf dem lokalen Computer erstellt.

Nach der ersten erfolgreichen Anmeldung mit den Domänenanmeldeinformationen bleiben die anmeldeeinstellungen erhalten, es sei denn, der Computer aus der Domäne entfernt wird oder die anmeldeeinstellungen manuell geändert werden.

Vor dem Anmelden an der Domäne:

-   Erstellen von Benutzerkonten in Active Directory-Benutzer und -Computer. Jeder Benutzer muss ein Active Directory-Domänendienste-Benutzerkonto in Active Directory-Benutzer und -Computer besitzen. Weitere Informationen finden Sie unter [erstellen Sie ein Benutzerkonto in Active Directory-Benutzer und -Computer](#BKMK_createUA).

-   Stellen Sie die richtige IP-Adresskonfiguration sicher. Um einen Computer mit der Domäne beizutreten, muss der Computer eine IP-Adresse verfügen. In diesem Handbuch mit statischen IP-Adressen konfiguriert sind, und Clientcomputer empfangen IP-Adressleases vom DHCP-Server. Aus diesem Grund muss der DHCP-Server bereitgestellt werden, bevor Sie Clients mit der Domäne verknüpfen. Weitere Informationen finden Sie unter [Bereitstellen von DHCP1](#BKMK_deployDHCP01).

-   Der Computer der Domäne hinzufügen. Alle Computer, enthält oder Netzwerkressourcen zugreift, muss der Domäne angehören. Weitere Informationen finden Sie unter [Hinzufügen von Servercomputern zur Domäne und Anmelden](#BKMK_joinlogserver) und [Hinzufügen von Clientcomputern zur Domäne und Anmelden](#BKMK_joinlogclients).

### <a name="bkmk_NetFndtn_Pln_DHCP-01"></a>Planen der Bereitstellung von DHCP1
Folgendes sind die wichtigsten Planungsschritte vor der Installation der Serverrolle DHCP auf DHCP1.

#### <a name="planning-dhcp-servers-and-dhcp-forwarding"></a>Planen der DHCP-Server und DHCP-Weiterleitung
Da DHCP-Meldungen Broadcastmeldungen sind, werden sie nicht zwischen Subnetzen über Router weitergeleitet. Wenn Sie mehrere Subnetze besitzen und DHCP-Dienst für jedes Subnetz bereitstellen möchten, müssen Sie einen der folgenden Schritteausführen:

-   Installieren Sie in jedem Subnetz einen DHCP-Server

-   Konfigurieren Sie Router so, dass DHCP-Broadcastmeldungen in Subnetzen weiterzuleiten, und konfigurieren Sie mehrere Bereiche auf dem DHCP-Server, einen Bereich pro Subnetz.

In den meisten Fällen ist die Konfiguration von Routern für die Weiterleitung von DHCP-Broadcastmeldungen kosteneffektiver als Bereitstellen eines DHCP-Servers in jedem physischen Segment des Netzwerks.

#### <a name="planning-ip-address-ranges"></a>Planen der IP-Adressbereiche
Jedes Subnetz benötigen Sie einen eigenen eindeutigen IP-Adressbereich. Diese Bereiche werden auf einem DHCP-Server durch Bereiche dargestellt.

Ein Bereich ist eine administrative Gruppierung von IP-Adressen für Computer in einem Subnetz, die den DHCP-Dienst verwenden. Der Administrator erstellt zunächst einen Bereich für jedes physische Subnetz und verwendet dann den Bereich, um die von Clients verwendeten Parameter zu definieren.

Ein Bereich weist die folgenden Eigenschaften:

-   Ein IP-Adressbereich, aus der Adressen für die DHCP-Dienst-Leaseangebote verwendet ein- oder ausgeschlossen werden soll.

-   Eine Subnetzmaske, die das Subnetzpräfix für eine bestimmte IP-Adresse bestimmt.

-   Ein bei seiner Erstellung zugewiesener Bereichsname.

-   Leasedauerwerte, die DHCP-Clients zugewiesen werden, die dynamisch zugeordnete IP-Adressen zu erhalten.

-   Beliebige DHCP-Bereichsoptionen, der für die Zuordnung zu DHCP-Clients, z.B. IP-Adresse des DNS-Servers und Router/IP-Adresse des Standardgateways konfiguriert.

-   Reservierungen werden optional verwendet, um sicherzustellen, dass ein DHCP-Client immer die gleiche IP-Adresse erhält.

Führen Sie vor der Bereitstellung Ihrer Server die Subnetze und der IP-Adressbereich, die, den Sie für jedes Subnetz verwenden möchten.

#### <a name="planning-subnet-masks"></a>Planen von Subnetzmasken
Netzwerk-IDs und Host-IDs innerhalb einer IP-Adresse werden mithilfe einer Subnetzmaske unterschieden. Jede Subnetzmaske ist eine 32-Bit-Zahl mit aufeinander folgende Bitgruppen von Einsen (1) zu den Netzwerk-ID und Nullen (0), um die Teile des Host-ID einer IP-Adresse zu identifizieren.

Beispielsweise ist die Subnetzmaske, die in der Regel mit der IP-Adresse 131.107.16.200 verwendet die folgenden 32-Bit-Binärzahl:

```
11111111 11111111 00000000 00000000
```

Diese Subnetzmaske Subnetznummer handelt es sich 16 eine Bits gefolgt von 16-Bit 0 (null), gibt an, dass die Netzwerk-ID und Host-ID Abschnitte dieser IP-Adresse jeweils 16Bit lang sind. In der Regel wird diese Subnetzmaske in punktierter Dezimalschreibweise als 255.255.0.0 angezeigt.

In der folgende Tabelle werden Subnetzmasken für die Internetadressklassen angezeigt.

|Address-Klasse|Bits für die Subnetzmaske|Subnetzmaske|
|-----------------|------------------------|---------------|
|Klasse A|11111111 00000000 00000000 00000000|255.0.0.0|
|Klasse-B|11111111 11111111 00000000 00000000|255.255.0.0|
|Klasse-C|11111111 11111111 11111111 00000000|255.255.255.0|

Wenn Sie einen Bereich in DHCP erstellen und Sie den IP-Adressbereich für den Bereich eingeben, stellt DHCP diese Standard-subnetzmaskenwerte bereit. In der Regel sind Standard-subnetzmaskenwerte für die meisten Netzwerke ohne spezielle Anforderungen und, wobei jedes IP-Netzwerksegment einem physischen Netzwerk entspricht, akzeptabel.

In einigen Fällen können Sie angepasste Subnetzmasken IP-Subnetzen implementieren. Mit IP-Subnetzen, können Sie den Abschnittdes Standard Host-ID-Teils einer IP-Adresse Subnetze, an denen es sich es sich um Unterabschnitte der ursprünglichen klassenbasierten Netzwerk-ID handelt

Anpassen der Länge der Subnetzmaske, können Sie die Anzahl der Bits reduzieren, die für die tatsächliche Host-ID verwendet werden

Um Probleme mit der Adressierung und Routing zu verhindern, sollten Sie sicherstellen, dass alle TCP/IP-Computer in einem Netzwerksegment die gleiche Subnetzmaske verwenden und jedem Computer oder Gerät eine eindeutige IP-Adresse hat.

#### <a name="planning-exclusion-ranges"></a>Planen von Ausschlussbereichen
Wenn Sie einen Bereich auf einem DHCP-Server erstellen, geben Sie einen IP-Adressbereich, der alle IP-Adressen enthält, die der DHCP-Server DHCP-Clients, z.B. Computer und andere Geräte leasen darf. Wenn Sie fahren, und einige Server manuell konfigurieren und andere Geräte mit statischen IP-Adressen aus der gleichen IP-Adressbereich, den der DHCP-Server verwendet wird, können Sie versehentlich einen IP-Adressenkonflikt erstellen, in denen Sie und der DHCP-Server verfügen zugewiesen sowohl die IP-Adresse auf verschiedenen Geräten.

Um dieses Problem zu beheben, können Sie einen Ausschlussbereich für den DHCP-Bereich erstellen. Ein Ausschlussbereich handelt es sich um einen zusammenhängenden Bereich von IP-Adressen innerhalb des Bereichs IP-Adressbereich, die der DHCP-Server nicht verwenden darf. Wenn Sie einen Ausschlussbereich erstellen, weist der DHCP-Server nicht die Adressen in diesem Bereich zu, sodass Sie diese Adressen manuell zuweisen können, ohne einen IP-Adressenkonflikt erstellen.

Erstellen einen Ausschlussbereich für jeden Bereich können Sie IP-Adressen von der Verteilung der DHCP-Server ausschließen. Sie sollten Ausschlüsse für alle Geräte verwenden, die mit einer statischen IP-Adresse konfiguriert sind. Die ausgeschlossenen Adressen sollten alle IP-Adressen enthalten, die Sie manuell anderen Servern, Nicht-DHCP-Clients, Arbeitsstationen ohne Datenträger oder Routing- und Remotezugriff- und PPP-Clients zugewiesen.

Es wird empfohlen, dass Sie den Ausschlussbereich mit zusätzlichen Adressen für Wachstum des Netzwerks konfigurieren. Die folgende Tabelle enthält einen Beispiel Ausschlussbereich für einen Bereich mit einer IP-Adressbereich 10.0.0.1 – 10.0.0.254 und Subnetzmaske 255.255.255.0.

|Konfigurationselemente|Beispielwerte|
|-----------------------|------------------|
|Start-IP-Adresse des Ausschlussbereichs|10.0.0.1|
|End-IP-Adresse des Ausschlussbereichs|10.0.0.25|

#### <a name="planning-tcpip-static-configuration"></a>Planen von statischen TCP/IP-Konfiguration
Bestimmte Geräte wie Router, DHCP-Server und DNS-Server müssen mit einer statischen IP-Adresse konfiguriert werden. Darüber hinaus müssen Sie möglicherweise weitere Geräte wie Drucker, die Sie immer sicherstellen möchten die IP-Adresse verfügen. Listen Sie die Geräte, die Sie konfigurieren statisch für jedes Subnetz möchten, und klicken Sie dann planen Sie des Ausschlussbereichs ein, die Sie auf dem DHCP-Server verwenden, um sicherzustellen, dass der DHCP-Server nicht über die IP-Adresse eines statisch konfigurierten Geräts least möchten. Ein Ausschlussbereich ist eine begrenzte Abfolge von IP-Adressen innerhalb eines Bereichs, der vom DHCP-Dienstangebot ausgeschlossen. Ausschlussbereiche stellen sicher, die alle Adressen in diesen Bereichen für DHCP-Clients im Netzwerk nicht vom Server angeboten werden.

Wenn die IP-Adressbereich eines Subnetzes 192.168.0.1 über 192.168.0.254 ist und Sie zehn Geräte, die Sie mit einer statischen IP-Adresse konfigurieren möchten, können Sie z.B. einen Ausschlussbereich für den 192.168.0 erstellen. *x* Bereich, der zehn oder mehr IP-Adressen enthält: 192.168.0.1 über 192.168.0.15.

In diesem Beispiel zehn der ausgeschlossenen IP-Adressen mit dem Server und andere Geräte mit statischen IP-Adressen konfigurieren und fünf weitere IP-Adressen für die Konfiguration neuer Geräte, die Sie in der Zukunft hinzufügen möchten, möglicherweise verfügbar bleiben. Mit diesem Ausschlussbereich bleibt der DHCP-Server über einen Adresspool von 192.168.0.16 über 192.168.0.254.

In der folgenden Tabelle werden zusätzliche Beispiel Konfigurationselemente für die AD DS und DNS bereitgestellt.

|Konfigurationselemente|Beispielwerte|
|-----------------------|------------------|
|Bindungen für die Netzwerkverbindung|Ethernet|
|DNS-servereinstellungen|DC1.corp.contoso.com|
|IP-Adresse des bevorzugten DNS-Servers|10.0.0.2|
|Hinzufügen von Werten im Dialogfeld Bereich<br /><br />1. Bereichsname<br />2. IP-Startadresse<br />3. Endet IP-Adresse<br />4. Subnetzmaske<br />5. Standardgateway (optional)<br />6. Leasedauer|1. Primären Subnetz<br />2.  10.0.0.1<br />3.  10.0.0.254<br />4.  255.255.255.0<br />5.  10.0.0.1<br />6. 8Tage|
|Betriebsmodus des IPv6-DHCP-Servers|Nicht aktiviert.|

## <a name="BKMK_deployment"></a>Hauptnetzwerk – Bereitstellung
Zum Bereitstellen eines Hauptnetzwerks werden befolgt die grundlegenden Schritte:

1.  [Konfigurieren aller Server](#BKMK_configuringAll)

2.  [Bereitstellen von DC1](#BKMK_deployADDNS01)

3.  [Hinzufügen von Servercomputern zur Domäne und anmelden](#BKMK_joinlogserver)

4.  [Bereitstellen von DHCP1](#BKMK_deployDHCP01)

5.  [Hinzufügen von Clientcomputern zur Domäne und anmelden](#BKMK_joinlogclients)

6.  [Bereitstellen von optionalen Features für die Netzwerkzugriffsauthentifizierung und Webdienste](#BKMK_optionalfeatures)

> [!NOTE]
> -   Gleichwertige Windows PowerShell-Befehle werden für die meisten Verfahren in diesem Handbuch bereitgestellt. Vor dem Ausführen dieser Cmdlets in Windows PowerShell, ersetzen Sie Beispielwerte durch Werte, die für Ihre netzwerkbereitstellung geeignet sind. Darüber hinaus müssen Sie jedes Cmdlet in einer einzelnen Zeile in Windows PowerShell eingeben. In diesem Handbuch möglicherweise einzelne Cmdlets in mehreren Zeilen aufgrund von formatierungseinschränkungen auf, und die Anzeige des Dokuments durch den Browser oder eine andere Anwendung angezeigt.
> -   Die Verfahren in diesem Handbuch beinhalten keine Anweisungen für diese Fälle in der die **User Account Control** Dialogfeld geöffnet wird, um Ihre Zustimmung zum Fortfahren abzufragen. Wenn dieses Dialogfeld wird geöffnet, während Sie die Verfahren in diesem Handbuch durchgeführt werden, und wenn das Dialogfeld, als Antwort auf Ihre Aktionen geöffnet wurde auf **Weiter**.

### <a name="BKMK_configuringAll"></a>Konfigurieren aller Server
Vor der Installation von anderen Technologien wie Active Directory-Domänendienste oder DHCP, ist es wichtig, dass die folgenden Elemente konfigurieren.

-   [Umbenennen des Computers](#BKMK_rename)

-   [Konfigurieren einer statischen IP-Adresse](#BKMK_ip)

In den folgenden Abschnitten können Sie diese Aktionen für jeden Server ausführen.

Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um diese Schritteausführen.

#### <a name="BKMK_rename"></a>Umbenennen des Computers
Das Verfahren können in diesem Abschnittzum Ändern des Namens eines Computers. Die Umbenennung des Computers ist hilfreich für Situationen, in denen das Betriebssystem automatisch einen Computernamen erstellt hat, den Sie nicht verwenden möchten.

> [!NOTE]
> Führen Sie dieses Verfahren mithilfe von Windows PowerShell, öffnen Sie PowerShell und geben Sie die folgenden Cmdlets jeweils in eigene Zeilen, und drücken dann die EINGABETASTE. Sie müssen auch ersetzen *ComputerName* mit dem Namen, die Sie verwenden möchten.
>
> `Rename-Computer`*ComputerName*
>
> `Restart-Computer`

###### <a name="to-rename-computers-running-windows-server-2016-windows-server-2012-r2-and-windows-server-2012"></a>Zum Umbenennen von Computern unter Windows Server2016, Windows Server2012 R2 und Windows Server2012

1.  Klicken Sie im Server-Manager auf **lokalen Server**. Der Computer **Eigenschaften** werden im Detailbereich angezeigt.

2.  In **Eigenschaften**im **Computername**, klicken Sie auf den vorhandenen Computernamen. Die **Systemeigenschaften** Dialogfeld wird geöffnet. Klicken Sie auf **ändern**. Die **Computer bzw.-domänenänderungen** das Dialogfeld wird geöffnet.

3.  In der **Computer bzw.-domänenänderungen** Dialogfeld **Computername**, geben Sie einen neuen Namen für den Computer. Geben Sie beispielsweise, wenn Sie den Computer DC1 benennen möchten, **DC1**.

4.  Klicken Sie auf **OK** zweimal, und klicken Sie dann auf **schließen**. Wenn Sie den Computer sofort an die Namensänderung abzuschließen, klicken Sie auf neu starten möchten **jetzt neu starten**. Klicken Sie anderenfalls auf **später neu starten**.

> [!NOTE]
> Informationen zum Umbenennen von Computern, die andere Microsoft-Betriebssysteme ausgeführt werden, finden Sie unter [AnhangA – Umbenennen von Computern](#BKMK_A).

#### <a name="BKMK_ip"></a>Konfigurieren einer statischen IP-Adresse
Sie können die Verfahren in diesem Thema verwenden, so konfigurieren Sie das Internet Protocol Version 4 (IPv4) Eigenschaften einer Netzwerkverbindung mit einer statischen IP-Adresse für Computer mit Windows Server2016.

> [!NOTE]
> Führen Sie dieses Verfahren mithilfe von Windows PowerShell, öffnen Sie PowerShell und geben Sie die folgenden Cmdlets jeweils in eigene Zeilen, und drücken dann die EINGABETASTE. Sie müssen die Schnittstellennamen und IP-Adressen in diesem Beispiel wird auch durch Werte ersetzen, die Sie verwenden, um Ihren Computer konfigurieren möchten.
>
> `New-NetIPAddress -IPAddress 10.0.0.2 -InterfaceAlias "Ethernet" -DefaultGateway 10.0.0.1 -AddressFamily IPv4 -PrefixLength 24`
>
> `Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 127.0.0.1`

###### <a name="to-configure-a-static-ip-address-on-computers-running-windows-server-2016-windows-server-2012-r2-and-windows-server-2012"></a>So konfigurieren Sie eine statische IP-Adresse auf Computern unter Windows Server2016, Windows Server2012 R2 und Windows Server2012

1.  In der Taskleiste mit der rechten Maustaste des Netzwerksymbol, und klicken Sie dann auf **öffnen Netzwerk- und Freigabecenter**.

2.  In **Netzwerk- und Freigabecenter**, klicken Sie auf **adaptereinstellungen ändern**. Die **Netzwerkverbindungen** Ordner wird geöffnet und zeigt die verfügbaren Netzwerkverbindungen.

3.  In **Netzwerkverbindungen**, mit der rechten Maustaste der Verbindungs, die Sie konfigurieren möchten, und klicken Sie dann auf **Eigenschaften**. Die Netzwerkverbindung **Eigenschaften** Dialogfeld wird geöffnet.

4.  In einer Netzwerkverbindung **Eigenschaften** Dialogfeld **diese Verbindung verwendet folgende Elemente**Option **Internet Protocol Version 4 (TCP/IPv4)**, und klicken Sie dann auf **Eigenschaften**. Die **Eigenschaften von Internetprotokoll Version 4 (TCP/IPv4)** Dialogfeld wird geöffnet.

5.  In **Eigenschaften von Internetprotokoll Version 4 (TCP/IPv4)**auf die **allgemeine** auf **verwenden Sie die folgende IP-Adresse**. In **IP-Adresse**, geben Sie die IP-Adresse, die Sie verwenden möchten.

6.  Drücken Sie Tab, um den Cursor im **Subnetzmaske**. Ein Standardwert für die Subnetzmaske wird automatisch eingegeben. Entweder akzeptieren Sie die Standardsubnetzmaske, oder geben Sie die Subnetzmaske, die Sie verwenden möchten.

7.  In **Standardgateway**, geben Sie die IP-Adresse des Standardgateways.

    > [!NOTE]
    > Sie müssen konfigurieren, **Standardgateway** mit der gleichen IP-Adresse, die Sie auf der lokalen Netzwerks (LAN)-Schnittstelle des Routers verwenden. Wenn beispielsweise Sie einen Router, die auf ein wide Area Network (WAN) wie z.B. dem Internet sowie Ihrem LAN verbunden ist haben, konfigurieren die LAN-Schnittstelle mit der gleichen IP-Adresse, die Sie dann als angeben der **Standardgateway**. In einem weiteren Beispiel besitzen Sie einen Router, der mit zwei LANs verbunden ist, in dem LAN A Adresse Bereich 10.0.0.0/24 und LAN B verwendet die Adresse Bereich 192.168.0.0/24, konfigurieren Sie die IP-Adresse von LAN A Router mit einer Adresse aus diesem Adressbereich, z.B. 10.0.0.1. Darüber hinaus konfigurieren, in der DHCP-Bereich für diesen Adressbereich, **Standardgateway** mit der IP-Adresse 10.0.0.1. Konfigurieren Sie für das LAN B die LAN B-Routerschnittstelle mit einer Adresse aus diesem Adressbereich, z.B. 192.168.0.1, und konfigurieren Sie dann den LAN B Bereich 192.168.0.0/24 mit einem **Standardgateway** 192.168.0.1 Wert.

8.  In **Bevorzugter DNS-Server**, geben Sie die IP-Adresse Ihres DNS-Servers. Wenn Sie den lokalen Computer als bevorzugten DNS-Server verwenden möchten, geben Sie die IP-Adresse des lokalen Computers.

9. In **alternativer DNS-Server**, geben Sie die IP-Adresse des alternativen DNS-Servers, falls vorhanden. Wenn Sie den lokalen Computer als alternativen DNS-Server verwenden möchten, geben Sie die IP-Adresse des lokalen Computers.

10. Klicken Sie auf **OK**, und klicken Sie dann auf **schließen**.

> [!NOTE]
> Weitere Informationen zum Konfigurieren einer statischen IP-Adresse auf Computern, die andere Microsoft-Betriebssysteme ausgeführt werden, finden Sie unter [AnhangB - Konfigurieren von statischen IP-Adressen](#BKMK_B).

#### <a name="BKMK_deployADDNS01"></a>Bereitstellen von DC1
Um DC1 bereitzustellen, die der Computer ausgeführt wird Active Directory-Domänendienste (AD DS) und DNS müssen Sie diese Schrittein der folgenden Reihenfolge ausführen:

-   Führen Sie die Schritteim Abschnitt [Konfigurieren aller Server](#BKMK_configuringAll).

-   [Installieren von AD DS und DNS für eine neue Gesamtstruktur](#BKMK_installAD-DNS)

-   [Erstellen Sie ein Benutzerkonto in Active Directory-Benutzer und -Computer](#BKMK_createUA)

-   [Zuweisen einer Gruppenmitgliedschaft](#BKMK_assigngroup)

-   [Konfigurieren einer DNS-Reverse-Lookupzone](#BKMK_reverse)

**Administratorrechte**

Wenn Sie ein kleines Netzwerk installieren und der einzige für das Netzwerk Administrator, empfiehlt es sich, dass Sie ein Benutzerkonto für sich selbst erstellen und dann Ihr Benutzerkonto als Mitglied der Organisations-Admins und Domänen-Admins hinzufügen. Auf diese Weise können Sie als Administrator für alle Netzwerkressourcen zu fungieren erleichtern. Es wird auch empfohlen, dass Sie mit diesem Konto anmelden nur, wenn Sie administrative Aufgaben ausführen müssen und Aufgaben im Zusammenhang mit, dass Sie ein separates Benutzerkonto für die Ausführung von Nicht-IT erstellen.

Wenn Sie ein größeres Netzwerk mit mehreren Administratoren haben, finden Sie in AD DS-Dokumentation die beste Gruppenmitgliedschaft für Mitarbeiter des Unternehmens zu ermitteln.

**Unterschiede zwischen Domänenbenutzerkonten und Benutzerkonten auf dem lokalen Computer**

Einer der Vorteile einer domänenbasierten Infrastruktur ist, dass Sie nicht auf jedem Computer in der Domäne Benutzerkonten erstellen müssen. Dies gilt, ob der Computer ein Clientcomputer oder einem Server ist.

Aus diesem Grund sollten Sie nicht auf jedem Computer in der Domäne Benutzerkonten erstellen. Erstellen Sie alle Benutzerkonten in Active Directory-Benutzer und -Computer, und verwenden Sie die vorhergehenden Verfahren, um die Gruppenmitgliedschaft zuzuweisen. Standardmäßig werden alle Benutzerkonten Mitglied der Gruppe Domänen-Benutzer.

Alle Mitglieder der Gruppe Domänen-Benutzer können auf jedem Clientcomputer anmelden, nachdem er der Domäne angehört.

Sie können konfigurieren, Benutzerkonten, um festzulegen, die Tage und Uhrzeiten aus, die der Benutzer am Computer anmelden darf. Sie können auch festlegen, welche Computer jeder Benutzer verwenden darf. Um diese Einstellungen konfigurieren, öffnen Sie Active Directory-Benutzer und -Computer zu, suchen Sie das Benutzerkonto, das Sie konfigurieren möchten, und doppelklicken Sie auf das Konto. Das Benutzerkonto **Eigenschaften**, klicken Sie auf die **Konto** Registerkarte, und klicken Sie dann auf **Anmeldezeiten** oder **anmelden**.

#### <a name="BKMK_installAD-DNS"></a>Installieren von AD DS und DNS für eine neue Gesamtstruktur

Sie können eines der folgenden Verfahren zum Installieren von Active Directory-Domänendienste (AD DS) und DNS- und eine neue Domäne in einer neuen Gesamtstruktur erstellen. 

Das erste Verfahren bietet Anweisungen zum Ausführen dieser Aktionen mithilfe von Windows PowerShell, während das zweite Verfahren zum Installieren von AD DS und DNS mithilfe von Server-Manager zeigt.

>[!IMPORTANT]
>Klicken Sie nach dem Ausführen der Schrittein diesem Verfahren wird der Computer automatisch neu gestartet.

**Installieren von AD DS und DNS mit WindowsPowerShell**

Sie können die folgenden Befehle zum Installieren und Konfigurieren von AD DS und DNS. Sie müssen den Domänennamen in diesem Beispiel wird mit dem Wert ersetzen, die Sie für Ihre Domäne verwenden möchten.

>[!NOTE]
>Weitere Informationen zu diesen Windows PowerShell-Befehlen finden Sie unter den folgenden Themen.
>- [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/server-manager/install-windowsfeature)
>- [Install-ADDSForest](https://technet.microsoft.com/itpro/powershell/windows/adds/deployment/install-addsforest)

Mitgliedschaft in **Administratoren** ist mindestens erforderlich, um dieses Verfahren auszuführen.

- Führen Sie Windows PowerShell als Administrator aus, geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE:  

`Install-WindowsFeature AD-Domain-Services -IncludeManagementTools`

Wenn die Installation erfolgreich abgeschlossen wurde, wird in Windows PowerShell die folgende Meldung angezeigt.

    
    Success Restart Needed  Exit Code   Feature Result
    ------- --------------  ---------   --------------
    True    No              Success     {Active Directory Domain Services, Group P...
    

- In Windows PowerShell, geben Sie folgenden Befehl ein, ersetzen Sie den Text **corp.contoso.com** mit Ihren Domänennamen ein, und drücken Sie dann die EINGABETASTE:

````
Install-ADDSForest -DomainName "corp.contoso.com"
````

- Bei der Installation und Konfiguration, der oben in der Windows PowerShell-Fenster angezeigt wird, wird Sie die folgende Meldung angezeigt. Nachdem sie angezeigt wird, geben Sie ein Kennwort, und drücken Sie dann die EINGABETASTE.

    **SafeModeAdministratorPassword:**

- Nachdem Sie ein Kennwort eingeben, und drücken Sie die EINGABETASTE, wird die folgende Aufforderung zur Bestätigung angezeigt. Geben Sie dasselbe Kennwort ein, und drücken Sie dann die EINGABETASTE.

    **Bestätigen Sie SafeModeAdministratorPassword:**

- Wenn die folgende Meldung angezeigt wird, geben Sie den Buchstaben **Y** und drücken Sie dann die EINGABETASTE.

    
    Der Zielserver wird als Domänencontroller konfiguriert und neu gestartet, wenn dieser Vorgang abgeschlossen ist.
    Möchten Sie diesen Vorgang fortsetzen?
    [Y] Ja [A] keine [L] Nein, alle [S] anhalten Ja für alle [N] [?] Hilfe (Standardwert ist "Y"):
    
- Wenn Sie möchten, können Sie die Warnung Nachrichten lesen, die während der normalen, erfolgreiche Installation von AD DS und DNS-angezeigt werden. Diese Nachrichten sind normal und sind keine Hinweise auf Fehler bei der Installation.

- Nach der Installation erfolgreich ist, wird eine Meldung angezeigt, dass Sie sind dabei, die auf dem Computer angemeldet sein, damit der Computer neu gestartet werden kann. Wenn Sie auf **schließen**Sie den Computer sofort abgemeldet werden und der Computer wird neu gestartet. Wenn Sie nicht auf **schließen**, dem Neustart des Computers nach einem standardmäßigen Zeitraum.

- Nachdem der Server neu gestartet wird, können Sie die erfolgreiche Installation von Active Directory-Domänendienste und DNS-überprüfen. Öffnen Sie Windows PowerShell, geben Sie den folgenden Befehl, und drücken Sie die EINGABETASTE.

````
Get-WindowsFeature
````

Die Ergebnisse dieses Befehls werden in Windows PowerShell angezeigt, und sollte die Ergebnisse in der folgenden Abbildungähnelt. Für installierte-Technologien, enthalten die Klammern neben den Namen der Technologie der Zeichen **X**, und der Wert der **Installationsstatus** ist **installiert**.

![Ergebnisse des Befehls Get-WindowsFeature](../media/Core-Network-Guide/server-roles-installed.jpg)

**Installieren Sie AD DS und DNS-Server-Manager verwenden**

1.  Auf DC1 im **Server-Manager**, klicken Sie auf **verwalten**, und klicken Sie dann auf **Hinzufügen von Rollen und Features**. Das Hinzufügen von Rollen und Features-Assistent wird geöffnet.

2.  In **Vorbemerkungen**, klicken Sie auf **Weiter**.

    > [!NOTE]
    > Die **Vorbemerkungen** des Hinzufügen von Rollen und Features Assistenten nicht angezeigt wird, wenn Sie zuvor ausgewählt haben **diese Seite standardmäßig überspringen** beim Hinzufügen von Rollen und Features-Assistent ausgeführt wurde.

3.  In **Select Installation Type**, stellen Sie sicher, dass **rollenbasierte oder featurebasierte Installation** ausgewählt ist, und klicken Sie dann auf **Weiter**.

4.  In **Zielserver auswählen**, stellen Sie sicher, dass **wählen Sie einen Server aus dem Serverpool** ausgewählt ist. In **Serverpool**, stellen Sie sicher, dass der lokale Computer ausgewählt ist. Klicken Sie auf **Weiter**.

5.  In **Serverrollen auswählen**im **Rollen**, klicken Sie auf **Active Directory Domain Services**. In **Hinzufügen von Features, die für Active Directory-Domänendienste erforderlich sind**, klicken Sie auf **Features hinzufügen**. Klicken Sie auf **Weiter**.

6.  In **Features auswählen**, klicken Sie auf **Weiter**, und im **Active Directory Domain Services**, überprüfen Sie die Informationen, die bereitgestellt wird, und klicken Sie dann auf **Weiter**.

7.  In **Installationsauswahl bestätigen**, klicken Sie auf **installieren**. Der Installationsstatus wird Status während der Installation. Klicken Sie nach Abschluss des Vorgangs in den Meldungsdetails auf **Server zu einem Domänencontroller heraufstufen**. Mit dem Assistenten zum Konfiguration von Active Directory-Domänendiensten wird geöffnet.

8.  In **Bereitstellungskonfiguration**Option **Hinzufügen einer neuen Gesamtstruktur**. In **Stammdomänenname**, geben Sie den vollständig qualifizierten Domänennamen (FQDN) für Ihre Domäne. Geben Sie z.B. ist der FQDN corp.contoso.com, **corp.contoso.com**. Klicken Sie auf **Weiter**.

9. In **Domänencontrolleroptionen**im **Funktionsebene der neuen Gesamtstruktur und der Stammdomäne auswählen**, wählen Sie die Funktionsebene der Gesamtstruktur und die Domänenfunktionsebene auf, die Sie verwenden möchten. In **Domänencontrollerfunktionen angeben**, stellen Sie sicher, dass **Domain Name System (DNS) Server** und **globalen Katalog (GC)** ausgewählt sind. In **Kennwort** und **Kennwort bestätigen**, geben Sie das Directory Services-Wiederherstellungsmodus (DSRM) ein, die Sie verwenden möchten. Klicken Sie auf **Weiter**.

10. In **DNS-Optionen**, klicken Sie auf **Weiter**.

11. In **zusätzliche Optionen**, überprüfen Sie den NetBIOS-Namen, die der Domäne zugewiesen ist, und nur bei Bedarf zu ändern. Klicken Sie auf **Weiter**.

12. In **Pfade**im **Geben Sie den Speicherort des AD DS-Datenbank, Protokolldateien und SYSVOL**, führen Sie eine der folgenden Optionen:

    -   Die Standardwerte zu übernehmen.

    -   Geben Sie Speicherorte von Ordnern, die Sie verwenden möchten **Datenbankordner**, **Protokolldateiordner**, und **SYSVOL-Ordner**.

13. Klicken Sie auf **Weiter**.

14. In **Optionen prüfen**, überprüfen Sie Ihre Auswahl.

15. Wenn Sie die Einstellungen in Windows PowerShell-Skript exportieren möchten, klicken Sie auf **Skript anzeigen**. Das Skript in Editor geöffnet, und können Sie es speichern, um den Speicherort des Ordners, den Sie möchten. Klicken Sie auf **Weiter**. In **Voraussetzungsüberprüfung**, Ihre Auswahl überprüft. Wenn die Überprüfung abgeschlossen ist, klicken Sie auf **installieren**. Wenn Sie von Windows aufgefordert werden, klicken Sie auf **schließen**. Zum Abschließen der Installation von AD DS und DNS-Neustart des Servers.

16. Zeigen Sie zum Überprüfen der erfolgreichen Installation der Server-Manager-Konsole nach dem Neustart des Servers. AD DS- und DNS-sollte im linken Bereich, z.B. die markierten Artikel in der Abbildungunten angezeigt werden.

![AD DS und DNS in Server-Manager](../media/Core-Network-Guide/server-roles-installed-sm.jpg)

##### <a name="BKMK_createUA"></a>Erstellen Sie ein Benutzerkonto in Active Directory-Benutzer und -Computer
Dieses Verfahrens können Sie ein neues Domänenbenutzerkonto in Active Directory-Benutzer und Computer Microsoft Management Console (MMC) erstellen.

Mitgliedschaft in **Domänen-Admins**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren auszuführen.

> [!NOTE]
> Führen Sie dieses Verfahren mithilfe von Windows PowerShell, öffnen Sie PowerShell das folgende Cmdlet in einer Zeile eingeben und dann die EINGABETASTE. Außerdem müssen Sie den Kontonamen in diesem Beispiel wird mit dem Wert angeben, die Sie verwenden möchten.
>
> `New-ADUser -SamAccountName User1 -AccountPassword (read-host "Set user password" -assecurestring) -name "User1" -enabled $true -PasswordNeverExpires $true -ChangePasswordAtLogon $false`
>
> Nachdem Sie die EINGABETASTE, geben Sie das Kennwort für das Benutzerkonto ein. Das Konto wird erstellt und in der Standardeinstellung ist Mitglied der Gruppe der Gruppe Domänen-Benutzer gewährt.
>
> Mit dem folgenden Cmdlet können Sie das neue Benutzerkonto Weitere Gruppenmitgliedschaften zuweisen. Im folgenden Beispiel werden die Gruppen Domänen-Admins und Organisations-Admins "user1" hinzugefügt. Vergewissern Sie sich vor dem Ausführen dieses Befehls, dass Sie den Kontonamen, den Domänennamen und die Gruppen entsprechend Ihren Anforderungen ändern.
>
> `Add-ADPrincipalGroupMembership -Identity "CN=User1,CN=Users,DC=corp,DC=contoso,DC=com" -MemberOf "CN=Enterprise Admins,CN=Users,DC=corp,DC=contoso,DC=com","CN=Domain Admins,CN=Users,DC=corp,DC=contoso,DC=com"`

###### <a name="to-create-a-user-account"></a>Zum Erstellen eines Benutzerkontos

1.  Klicken Sie auf DC1 im Server-Manager auf **Tools**, und klicken Sie dann auf **Active Directory-Benutzer und -Computer**. Die Active Directory-Benutzer und -Computer in der MMC wird geöffnet. Wenn es nicht bereits ausgewählt ist, klicken Sie auf den Knoten für Ihre Domäne. Angenommen, Ihre Domäne corp.contoso.com, klicken Sie auf **corp.contoso.com**.

2.  Klicken Sie im Detailbereich auf den Ordner, in dem Sie ein Benutzerkonto hinzufügen möchten.

    **In welchen Bereichen?**

    -   Active Directory-Benutzer und -Computer /*Domänenknoten*/*Ordner*

3.  Zeigen Sie auf **neu**, und klicken Sie dann auf **Benutzer**. Die **neues Objekt – Benutzer** Dialogfeld wird geöffnet.

4.  In **Vorname**, geben Sie die Vornamen des Benutzers ein.

5.  In **Initialen**, geben Sie die Initialen des Benutzers.

6.  In **Nachname**, geben Sie die Nachnamen des Benutzers ein.

7.  Ändern Sie **vollständiger Name** um Initialen hinzuzufügen oder die Reihenfolge des vor- und Nachnamen umzukehren.

8.  In **Benutzeranmeldename**, geben Sie den Benutzeranmeldenamen ein. Klicken Sie auf **Weiter**.

9. In **neues Objekt – Benutzer**im **Kennwort** und **Kennwort bestätigen**, geben Sie das Kennwort des Benutzers ein, und wählen Sie dann die entsprechenden Kennwortoptionen aus.

10. Klicken Sie auf **Weiter**, überprüfen Sie die Einstellungen des neuen Benutzers, und klicken Sie dann auf **Fertig stellen**.

##### <a name="BKMK_assigngroup"></a>Zuweisen einer Gruppenmitgliedschaft
Dieses Verfahrens können Sie einem Benutzer, Computer oder einer Gruppe zu einer Gruppe in Active Directory-Benutzer und Computer Microsoft Management Console (MMC) hinzufügen.

Mitgliedschaft in **Domänen-Admins**, oder einer entsprechenden Gruppe die mindestvoraussetzung, um dieses Verfahren auszuführen.

###### <a name="to-assign-group-membership"></a>Gruppenmitgliedschaft zuweisen

1.  Klicken Sie auf DC1 im Server-Manager auf **Tools**, und klicken Sie dann auf **Active Directory-Benutzer und -Computer**. Die Active Directory-Benutzer und -Computer in der MMC wird geöffnet. Wenn es nicht bereits ausgewählt ist, klicken Sie auf den Knoten für Ihre Domäne. Angenommen, Ihre Domäne corp.contoso.com, klicken Sie auf **corp.contoso.com**.

2.  Doppelklicken Sie im Detailbereich auf den Ordner mit der Gruppe ein Mitglied hinzugefügt werden soll.

    In welchen Bereichen?

    -   **Active Directory-Benutzer und -Computer**/*Domänenknoten*/*Ordner, der die Gruppe enthält.*

3.  Klicken Sie im Detailbereich mit der Maustaste des Objekts, das Sie hinzufügen möchten zu einer Gruppe ein, z.B. einen Benutzer oder Computer, und klicken Sie dann auf **Eigenschaften**. Des Objekts **Eigenschaften** Dialogfeld wird geöffnet. Klicken Sie auf die **Mitglied** Registerkarte.

4.  Auf der **Mitglied** auf **hinzufügen**.

5.  In **Geben Sie die zu verwendenden Objektnamen ein**, geben Sie den Namen der Gruppe "Sie möchten das Objekt hinzuzufügen, und klicken Sie dann auf" **OK**.

6.  Mitgliedschaft in anderen Benutzer, Gruppen oder Computer zuweisen möchten, wiederholen Sie die Schritte4 und 5 dieses Verfahrens.

##### <a name="BKMK_reverse"></a>Konfigurieren einer DNS-Reverse-Lookupzone
Sie können dieses Verfahren verwenden, so konfigurieren Sie eine Reverse-Lookupzone im Domain Name System (DNS).

Mitgliedschaft in **Domänen-Admins** ist mindestens erforderlich, um dieses Verfahren auszuführen.

> [!NOTE]
> -   Für mittlere und große Unternehmen empfiehlt es sich, dass Sie konfigurieren und verwenden Sie die Gruppe DNSAdmins in Active Directory-Benutzer und -Computer. Weitere Informationen finden Sie unter [zusätzliche technische Ressourcen](#BKMK_resources)
> -   Führen Sie dieses Verfahren mithilfe von Windows PowerShell, öffnen Sie PowerShell das folgende Cmdlet in einer Zeile eingeben und dann die EINGABETASTE. Sie müssen auch die DNS-Reverse-Lookup und der Zonendateinamen Namen in diesem Beispiel ersetzen, die mit den Werten, die Sie verwenden möchten. Stellen Sie sicher, dass Sie die Netzwerk-ID für den Namen der reverse-Zone rückgängig machen. Beispielsweise ist die Netzwerk-ID 192.168.0, der Name der Reverse-Lookupzone erstellen **0.168.192.in-addr.arpa**.
>
> `Add-DnsServerPrimaryZone 0.0.10.in-addr.arpa -ZoneFile 0.0.10.in-addr.arpa.dns`

###### <a name="to-configure-a-dns-reverse-lookup-zone"></a>So konfigurieren Sie DNS-Reverse-Lookupzone

1.  Klicken Sie auf DC1 im Server-Manager auf **Tools**, und klicken Sie dann auf **DNS**. Der DNS-MMC geöffnet wird.

2.  Doppelklicken Sie in DNS Wenn dies nicht bereits geschehen ist, auf den Servernamen, um die Struktur zu erweitern. Wenn beispielsweise der DNS-Server-Namen DC1 lautet, doppelklicken Sie auf **DC1**.

3.  Wählen Sie **Reverse-Lookupzonen**, mit der rechten Maustaste **Reverse-Lookupzonen**, und klicken Sie dann auf **neue Zone**. Der Assistent zum Erstellen neuer Zonen wird geöffnet.

4.  In **Willkommen beim Assistenten zum Erstellen neuer Zonen**, klicken Sie auf **Weiter**.

5.  In **Zonentyp**Option **primäre Zone**.

6.  Wenn Ihr DNS-Server ein beschreibbarer Domänencontroller ist, stellen Sie sicher, dass **speichern Sie die Zone in Active Directory** ausgewählt ist. Klicken Sie auf **Weiter**.

7.  In **Active Directory-Zonenreplikationsbereich**Option **alle DNS-Server auf Domänencontrollern in dieser Domäne**, es sei denn, Sie einen bestimmten Grund haben, eine andere Option auszuwählen. Klicken Sie auf **Weiter**.

8.  Im ersten **Name der Reverse-Lookup** Seite **IPv4 Reverse-Lookupzone**. Klicken Sie auf **Weiter**.

9. In der zweiten **Name der Reverse-Lookup** eine der folgenden Optionen:

    -   In **Netzwerk-ID**, geben Sie die Netzwerk-ID Ihres IP-Adressbereichs. Geben Sie z.B. ist der IP-Adressbereich 10.0.0.1 über 10.0.0.254, **10.0.0**.

    -   In **Reverse-lookupzonennamen**, Ihrer IPv4 reverse-lookupzonennamen wird automatisch hinzugefügt. Klicken Sie auf **Weiter**.

10. In **dynamisches Update**, wählen Sie den Typ des dynamischen Updates, die Sie zulassen möchten. Klicken Sie auf **Weiter**.

11. In **Abschließen des Assistenten für neue Zone**, überprüfen Sie Ihre Auswahl, und klicken Sie dann auf **Fertig stellen**.

#### <a name="BKMK_joinlogserver"></a>Hinzufügen von Servercomputern zur Domäne und anmelden
Nachdem Sie die Active Directory-Domänendienste (AD DS) installiert und eine oder mehrere Benutzerkonten, die Berechtigung zum Hinzufügen eines Computers zur Domäne erstellt haben, können Sie Hauptnetzwerks zur Domäne und melden Sie sich bei den Servern hinzufügen, um weitere Technologien, wie z.B. Dynamic Host Configuration Protocol (DHCP) zu installieren.

Führen Sie auf allen Servern, die Sie bereitstellen, mit Ausnahme der Server mit AD DS folgende Schritteaus:

1.  Führen Sie die Verfahren im [Konfigurieren aller Server](#BKMK_configuringAll).

2.  Verwenden Sie die Anweisungen in den folgenden beiden Verfahren, um Ihre Server der Domäne hinzuzufügen und zu melden Sie sich bei den Servern, um weitere Bereitstellungsaufgaben auszuführen können:

> [!NOTE]
> Führen Sie dieses Verfahren mithilfe von Windows PowerShell, öffnen Sie PowerShell und geben Sie das folgende Cmdlet, und drücken dann die EINGABETASTE. Sie müssen auch den Domänennamen mit dem Namen ersetzen, die Sie verwenden möchten.
>
> `Add-Computer -DomainName corp.contoso.com`
>
> Wenn Sie dazu aufgefordert werden, geben Sie den Benutzernamen und das Kennwort für ein Konto, das über die Berechtigung zum Hinzufügen eines Computers zur Domäne verfügt. Um den Computer neu starten, geben Sie folgenden Befehl ein, und drücken Sie die EINGABETASTE.
>
> `Restart-Computer`

###### <a name="to-join-computers-running--windows-server-2016--windows-server-2012-r2--and--windows-server-2012--to-the-domain"></a>Auf Computern unter Windows Server2016, Windows Server2012 R2 und Windows Server2012 mit der Domäne beitreten

1.  Klicken Sie im Server-Manager auf **lokalen Server**. Klicken Sie im Detailbereich auf **Arbeitsgruppe**. Die **Systemeigenschaften** Dialogfeld wird geöffnet.

2.  In der **Systemeigenschaften** Dialogfeld, klicken Sie auf **ändern**. Die **Computer bzw.-domänenänderungen** das Dialogfeld wird geöffnet.

3.  In **Computername**im **Mitglied**, klicken Sie auf **Domäne**, und geben Sie den Namen der Domäne, die Sie hinzufügen möchten. Geben Sie z.B. ist der Domänenname corp.contoso.com, **corp.contoso.com**.

4.  Klicken Sie auf **OK**. Die **Windows-Sicherheit** Dialogfeld wird geöffnet.

5.  In **Computer bzw.-domänenänderungen**im **Benutzernamen**, geben Sie den Benutzernamen ein, und im **Kennwort**, geben Sie das Kennwort ein, und klicken Sie dann auf **OK**. Die **Computer bzw.-domänenänderungen** das Dialogfeld wird angezeigt, und Sie werden bei der Domänenbenutzers begrüßt. Klicken Sie auf **OK**.

6.  Die **Computer bzw.-domänenänderungen** das Dialogfeld zeigt einer Meldung angezeigt, dass Sie den Computer, um die Änderungen zu übernehmen neu gestartet werden müssen. Klicken Sie auf **OK**.

7.  Auf der **Systemeigenschaften** Dialogfeld auf die **Computername** auf **schließen**. Die **Microsoft Windows** Dialogfeld wird geöffnet und zeigt die Meldung, erneut an, dass Sie den Computer, um die Änderungen zu übernehmen neu gestartet werden müssen. Klicken Sie auf **jetzt neu starten**.

> [!NOTE]
> Informationen zum Hinzufügen von Computern, die andere Microsoft-Betriebssysteme an der Domäne ausgeführt werden, finden Sie unter [AnhangC – Hinzufügen von Computern zur Domäne](#BKMK_C).

###### <a name="to-log-on-to-the-domain-using-computers-running-windows-server-2016"></a>Anmelden bei der Domäne mit einem Computer unter Windows Server2016

1.  Melden Sie den Computer oder starten Sie den Computer neu.

2.  Drücken Sie STRG+ALT+ENTF. Der Anmeldebildschirm angezeigt wird.

3.  Klicken Sie in der unteren linken Ecke auf **anderer Benutzer**.

4.  In **Benutzernamen**, geben Sie Ihren Benutzernamen ein.

5.  In **Kennwort**, geben Sie das Domänenkennwort ein, und klicken Sie auf den Pfeil, oder drücken Sie die EINGABETASTE.

> [!NOTE]
> Weitere Informationen zur Anmeldung an der Domäne mit Computern, die andere Microsoft-Betriebssysteme ausgeführt werden, finden Sie unter [AnhangD – Anmelden bei der Domäne](#BKMK_D).

#### <a name="BKMK_deployDHCP01"></a>Bereitstellen von DHCP1
Bevor Sie diese Komponente des Hauptnetzwerks bereitstellen können, müssen Sie Folgendes tun:

-   Führen Sie die Schritteim Abschnitt [Konfigurieren aller Server](#BKMK_configuringAll).

-   Führen Sie die Schritteim Abschnitt [Hinzufügen von Servercomputern zur Domäne und Anmelden](#BKMK_joinlogserver).

Bereitstellen von DHCP1 des Computers Serverrolle Dynamic Host Configuration-Protokoll (DHCP) ausgeführt, müssen Sie diese Schrittein der folgenden Reihenfolge ausführen:

-   [Installieren von Dynamic Host Configuration-Protokoll (DHCP)](#BKMK_installDHCP)

-   [Erstellen Sie und aktivieren Sie einen neuen DHCP-Bereich](#BKMK_newscopeDHCP)

> [!NOTE]
> Öffnen Sie PowerShell zum Ausführen dieser Verfahren mithilfe von Windows PowerShell Geben Sie die folgenden Cmdlets jeweils in eigene Zeilen, und drücken Sie dann die EINGABETASTE. Sie müssen den Bereichsnamen, IP-Adresse Start- und Endbereich, Subnetzmaske und anderen Werten in diesem Beispiel auch mit den Werten ersetzen, die Sie verwenden möchten.
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

##### <a name="BKMK_installDHCP"></a>Installieren von Dynamic Host Configuration-Protokoll (DHCP)
Dieses Verfahren können Sie installieren und konfigurieren die DHCP-Serverrolle hinzufügen von Rollen und Features-Assistenten verwenden.

Mitgliedschaft in **Domänen-Admins**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren auszuführen.

###### <a name="to-install-dhcp"></a>So installieren Sie DHCP

1.  Klicken Sie auf DHCP1 unter Server-Manager auf **verwalten**, und klicken Sie dann auf **Hinzufügen von Rollen und Features**. Das Hinzufügen von Rollen und Features-Assistent wird geöffnet.

2.  In **Vorbemerkungen**, klicken Sie auf **Weiter**.

    > [!NOTE]
    > Die **Vorbemerkungen** des Hinzufügen von Rollen und Features Assistenten nicht angezeigt wird, wenn Sie zuvor ausgewählt haben **diese Seite standardmäßig überspringen** beim Hinzufügen von Rollen und Features-Assistent ausgeführt wurde.

3.  In **Select Installation Type**, stellen Sie sicher, dass **rollenbasierte oder featurebasierte Installation** ausgewählt ist, und klicken Sie dann auf **Weiter**.

4.  In **Zielserver auswählen**, stellen Sie sicher, dass **wählen Sie einen Server aus dem Serverpool** ausgewählt ist. In **Serverpool**, stellen Sie sicher, dass der lokale Computer ausgewählt ist. Klicken Sie auf **Weiter**.

5.  In **Serverrollen auswählen**im **Rollen**Option **DHCP-Server**. In **Hinzufügen von Features, die für DHCP-Server erforderlich sind**, klicken Sie auf **Features hinzufügen**. Klicken Sie auf **Weiter**.

6.  In **Features auswählen**, klicken Sie auf **Weiter**, und im **DHCP-Server**, überprüfen Sie die Informationen, die bereitgestellt wird, und klicken Sie dann auf **Weiter**.

7.  In **Installationsauswahl bestätigen**, klicken Sie auf **Zielserver bei Bedarf automatisch neu**. Wenn Sie aufgefordert werden, die Auswahl zu bestätigen, klicken Sie auf **Ja**, und klicken Sie dann auf **installieren**. Die **Installationsstatus** Seite zeigt den Status während der Installation. Wenn der Vorgang abgeschlossen ist, die Meldung "Konfiguration erforderlich. Die Installation war erfolgreich auf *ComputerName*"angezeigt wird, wobei *ComputerName* ist der Name des Computers, auf dem DHCP-Server installiert. Klicken Sie im Meldungsfenster auf **DHCP-Konfiguration abschließen**. Der DHCP-Post-Install nach der Konfigurations-Assistent wird geöffnet. Klicken Sie auf **Weiter**.

8.  In **Autorisierung**, geben Sie die Anmeldeinformationen, die Sie verwenden, um autorisieren Sie den DHCP-Server in Active Directory Domain Services, und klicken Sie dann auf möchten **übernehmen**. Klicken Sie nach Abschluss der Autorisierung auf **schließen**.

##### <a name="BKMK_newscopeDHCP"></a>Erstellen Sie und aktivieren Sie einen neuen DHCP-Bereich
Dieses Verfahrens können Sie einen neuen DHCP-Bereich mit der DHCP-Microsoft Management Console (MMC) erstellen. Wenn Sie das Verfahren abgeschlossen haben, der Bereich aktiviert und des Ausschlussbereichs ein, die Sie erstellen verhindert, dass des DHCP-Servers leasen, die IP-Adressen, die Sie verwenden, um statische Konfiguration Ihrer Server und andere Geräte, die eine statische IP-Adresse benötigen.

Mitgliedschaft in **DHCP-Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren auszuführen.

###### <a name="to-create-and-activate-a-new-dhcp-scope"></a>Erstellen und aktivieren einen neuen DHCP-Bereich

1.  Klicken Sie auf DHCP1 unter Server-Manager auf **Tools**, und klicken Sie dann auf **DHCP**. Die DHCP-MMC geöffnet wird.

2.  In **DHCP**, erweitern Sie den Namen des Servers. Z.B. den Namen des DHCP-Servers DHCP1.corp.contoso.com, klicken Sie auf den Pfeil nach unten neben **DHCP1.corp.contoso.com**.

3.  Unter den Namen des Servers mit der rechten Maustaste **IPv4**, und klicken Sie dann auf **neuen Bereich**. Die Bereichserstellungs-Assistent wird geöffnet.

4.  In **Willkommen beim Assistenten**, klicken Sie auf **Weiter**.

5.  In **Bereichsname**im **Namen**, geben Sie einen Namen für den Bereich. Geben Sie z.B. **Subnetz 1**.

6.  In **Beschreibung**, geben Sie eine Beschreibung für den neuen Bereich, und klicken Sie dann auf **Weiter**.

7.  In **IP-Adressbereich**, gehen Sie folgendermaßen vor:

    1.  In **Start-IP-Adresse**, geben Sie die IP-Adresse, die die erste IP-Adresse im Bereich ist. Geben Sie z.B. **10.0.0.1**.

    2.  In **End-IP-Adresse**, geben Sie die IP-Adresse, die die letzte IP-Adresse im Bereich ist. Geben Sie z.B. **10.0.0.254**. -Werte für **Länge** und **Subnetzmaske** werden automatisch eingegeben, basierend auf der IP-Adresse, die Sie eingegeben, für die haben **Start-IP-Adresse**.

    3.  Ändern Sie ggf. die Werte in **Länge** oder **Subnetzmaske**entsprechend Ihres Adressierungsschemas.

    4.  Klicken Sie auf **Weiter**.

8.  In **Ausschlüsse hinzufügen**, gehen Sie folgendermaßen vor:

    1.  In **Start-IP-Adresse**, geben Sie die IP-Adresse, die die erste IP-Adresse des Ausschlussbereichs. Geben Sie z.B. **10.0.0.1**.

    2.  In **End-IP-Adresse**, geben die IP-Adresse, die die letzte IP-Adresse des Ausschlussbereichs beispielsweise **10.0.0.15**.

9. Klicken Sie auf **hinzufügen**, und klicken Sie dann auf **Weiter**.

10. In **Leasedauer**, ändern Sie die Standardwerte für **Tage**, **Stunden**, und **Minuten**, entsprechend den Anforderungen für das Netzwerk, und klicken Sie dann auf **Weiter**.

11. In **DHCP-Optionen konfigurieren**Option **Ja, ich möchte diese Optionen jetzt konfigurieren**, und klicken Sie dann auf **Weiter**.

12. In **Router (Standardgateway)**, führen Sie eine der folgenden Optionen:

    -   Wenn der Router im Netzwerk nicht vorhanden sind, klicken Sie auf **Weiter**.

    -   In **IP-Adresse**, geben Sie die IP-Adresse des Routers oder Standardgateways. Geben Sie z.B. **10.0.0.1**. Klicken Sie auf **hinzufügen**, und klicken Sie dann auf **Weiter**.

13. In **Domänenname und DNS-Server**, gehen Sie folgendermaßen vor:

    1.  In **übergeordneten Domäne**, geben Sie den Namen der DNS-Domäne, die Clients für die Namensauflösung verwenden. Geben Sie z.B. **corp.contoso.com**.

    2.  In **Servername**, geben Sie den Namen des DNS-Computers, den Clients für die Namensauflösung verwenden. Geben Sie z.B. **DC1**.

    3.  Klicken Sie auf **beheben**. Die IP-Adresse des DNS-Servers wird im hinzugefügt **IP-Adresse**. Klicken Sie auf **hinzufügen**, warten Sie, bis der DNS-Server IP-Adressüberprüfung abgeschlossen, und klicken Sie dann auf **Weiter**.

14. In **WINS-Server**, da Sie nicht über WINS-Server in Ihrem Netzwerk verfügen klicken Sie auf **Weiter**.

15. In **Bereich aktivieren**Option **Ja, ich möchte diesen Bereich jetzt aktivieren**.

16. Klicken Sie auf **Weiter**, und klicken Sie dann auf **Fertig stellen**.

> [!IMPORTANT]
> Wiederholen Sie dieses Verfahren, um neue Bereiche für Weitere Subnetze zu erstellen. Verwenden Sie einen anderen Bereich der IP-Adresse für jedes Subnetz, das Sie planen, bereitstellen, und stellen Sie sicher, dass die Weiterleitung von DHCP-Meldung auf allen Routern aktiviert ist, die in andere Subnetze führen.

### <a name="BKMK_joinlogclients"></a>Hinzufügen von Clientcomputern zur Domäne und anmelden

> [!NOTE]
> Führen Sie dieses Verfahren mithilfe von Windows PowerShell, öffnen Sie PowerShell und geben Sie das folgende Cmdlet, und drücken dann die EINGABETASTE. Sie müssen auch den Domänennamen mit dem Namen ersetzen, die Sie verwenden möchten.
>
> `Add-Computer -DomainName corp.contoso.com`
>
> Wenn Sie dazu aufgefordert werden, geben Sie den Benutzernamen und das Kennwort für ein Konto, das über die Berechtigung zum Hinzufügen eines Computers zur Domäne verfügt. Um den Computer neu starten, geben Sie folgenden Befehl ein, und drücken Sie die EINGABETASTE.
>
> `Restart-Computer`

##### <a name="to-join-computers-running-windows-10-to-the-domain"></a>Auf Computern unter Windows10 mit der Domäne beitreten

1.  Melden Sie sich an den Computer mit dem lokalen Administratorkonto an.

2.  In **suchen im Web und Windows**, Typ **System**. Klicken Sie in den Suchergebnissen auf **System (Systemsteuerung)**. Die **System** Dialogfeld wird geöffnet.

3.  In **System**, klicken Sie auf **Erweiterte Systemeinstellungen**. Die **Systemeigenschaften** Dialogfeld wird geöffnet. Klicken Sie auf die **Computername** Registerkarte.

4.  In **Computername**, klicken Sie auf **ändern**. Die **Computer bzw.-domänenänderungen** das Dialogfeld wird geöffnet.

5.  In **Computer bzw.-domänenänderungen** im **Mitglied**, klicken Sie auf **Domäne**, und geben Sie den Namen der Domäne hinzugefügt werden soll. Geben Sie z.B. ist der Domänenname corp.contoso.com, **corp.contoso.com**.

6.  Klicken Sie auf **OK**. Die **Windows-Sicherheit** Dialogfeld wird geöffnet.

7.  In **Computer bzw.-domänenänderungen**im **Benutzernamen**, geben Sie den Benutzernamen ein, und im **Kennwort**, geben Sie das Kennwort ein, und klicken Sie dann auf **OK**. Die **Computer bzw.-domänenänderungen** das Dialogfeld wird angezeigt, und Sie werden bei der Domänenbenutzers begrüßt. Klicken Sie auf **OK**.

8.  Die **Computer bzw.-domänenänderungen** das Dialogfeld zeigt einer Meldung angezeigt, dass Sie den Computer, um die Änderungen zu übernehmen neu gestartet werden müssen. Klicken Sie auf **OK**.

9. Auf der **Systemeigenschaften** Dialogfeld auf die **Computername** auf **schließen**. Die **Microsoft Windows** Dialogfeld wird geöffnet und zeigt die Meldung, erneut an, dass Sie den Computer, um die Änderungen zu übernehmen neu gestartet werden müssen. Klicken Sie auf **jetzt neu starten**.

##### <a name="to-join-computers-running-windows-81-to-the-domain"></a>Auf Computern unter Windows8.1 mit der Domäne beitreten

1.  Melden Sie sich an den Computer mit dem lokalen Administratorkonto an.

2.  Mit der rechten Maustaste **starten**, und klicken Sie dann auf **System**. Die **System** Dialogfeld wird geöffnet.

3.  In **System**, klicken Sie auf **Erweiterte Systemeinstellungen**. Die **Systemeigenschaften** Dialogfeld wird geöffnet. Klicken Sie auf die **Computername** Registerkarte.

4.  In **Computername**, klicken Sie auf **ändern**. Die **Computer bzw.-domänenänderungen** das Dialogfeld wird geöffnet.

5.  In **Computer bzw.-domänenänderungen** im **Mitglied**, klicken Sie auf **Domäne**, und geben Sie den Namen der Domäne hinzugefügt werden soll. Geben Sie z.B. ist der Domänenname corp.contoso.com, **corp.contoso.com**.

6.  Klicken Sie auf **OK**. Die **Windows-Sicherheit** Dialogfeld wird geöffnet.

7.  In **Computer bzw.-domänenänderungen**im **Benutzernamen**, geben Sie den Benutzernamen ein, und im **Kennwort**, geben Sie das Kennwort ein, und klicken Sie dann auf **OK**. Die **Computer bzw.-domänenänderungen** das Dialogfeld wird angezeigt, und Sie werden bei der Domänenbenutzers begrüßt. Klicken Sie auf **OK**.

8.  Die **Computer bzw.-domänenänderungen** das Dialogfeld zeigt einer Meldung angezeigt, dass Sie den Computer, um die Änderungen zu übernehmen neu gestartet werden müssen. Klicken Sie auf **OK**.

9. Auf der **Systemeigenschaften** Dialogfeld auf die **Computername** auf **schließen**. Die **Microsoft Windows** Dialogfeld wird geöffnet und zeigt die Meldung, erneut an, dass Sie den Computer, um die Änderungen zu übernehmen neu gestartet werden müssen. Klicken Sie auf **jetzt neu starten**.

##### <a name="to-log-on-to-the-domain-using-computers-running-windows-10"></a>Anmelden bei der Domäne mit einem Computer unter Windows10

1.  Melden Sie den Computer oder starten Sie den Computer neu.

2.  Drücken Sie STRG+ALT+ENTF. Der Anmeldebildschirm angezeigt wird.

3.  Klicken Sie im unten links auf **anderer Benutzer**.

4.  In **Benutzernamen**, geben Sie Ihre Domäne und den Namen im Format *Domäne\Benutzer*. Z.B. zum Anmelden bei der Domäne corp.contoso.com mit einem Konto mit dem Namen **Benutzer-01**, Typ **corp\benutzer-01**.

5.  In **Kennwort**, geben Sie das Domänenkennwort ein, und klicken Sie auf den Pfeil, oder drücken Sie die EINGABETASTE.

### <a name="BKMK_optionalfeatures"></a>Bereitstellen von optionalen Features für die Netzwerkzugriffsauthentifizierung und Webdienste
Wenn Sie Netzwerkzugriffsserver, z.B. drahtlose Zugriffspunkte oder VPN-Server, nach der Installation Ihres Hauptnetzwerks Netzwerkzugriffsserver bereitstellen möchten, empfiehlt es sich, dass Sie einen NPS-Server und einen Webserver bereitstellen. Für die Bereitstellung von Netzwerkzugriff wird die Verwendung von sicheren zertifikatbasierte Authentifizierungsmethoden empfohlen. Sie können NPS verwenden, um Netzwerkzugriffsrichtlinien verwalten und sichere Authentifizierungsmethoden bereitstellen. Einen Webserver können so veröffentlichen Sie die Zertifikatsperrliste (CRL) von der Zertifizierungsstelle (CA), die Zertifikate für die sichere Authentifizierung bereitstellt.

> [!NOTE]
> Mithilfe der Begleithandbücher zum Hauptnetzwerk können Sie Serverzertifikate und andere zusätzliche Features bereitstellen. Weitere Informationen finden Sie unter [zusätzliche technische Ressourcen](#BKMK_resources).

Die folgende Abbildungzeigt die Windows Server-Hauptnetzwerk-Topologie mit NPS und Web-Servern hinzugefügt.

![Windows Server-Hauptnetzwerk Topologie mit hinzugefügte NPS und Web-Server](../media/Core-Network-Guide/cng16_overview_2.jpg)

Die folgenden Abschnitte enthalten Informationen zum Hinzufügen von NPS- und Webserver zum Netzwerk.

-   [Bereitstellung von NPS1](#BKMK_deployNPS1)

-   [Bereitstellen von WEB1](#BKMK_IIS)

#### <a name="BKMK_deployNPS1"></a>Bereitstellung von NPS1
Der Netzwerkrichtlinienserver (Network Policy Server, NPS)-Server wird als vorbereitende Maßnahme zur Bereitstellung anderer netzwerktechnologien, z.B. Server virtuelle private Netzwerke (VPN), Drahtloszugriffspunkte und 802.1X-Authentifizierungsswitches installiert.

Netzwerkrichtlinienserver (Network Policy Server, NPS) können Sie zentral konfigurieren und verwalten Netzwerkrichtlinien mithilfe der folgenden Funktionen: Remote Authentication Dial-in User Service (RADIUS)-Server und RADIUS-Proxy.

NPS ist eine optionale Komponente eines Hauptnetzwerks, aber Sie sollten NPS installieren, wenn eine der folgenden Aussagen zutrifft:

-   Sie planen die Erweiterung Ihres Netzwerks mit RAS-Server enthalten, die mit dem RADIUS-Protokoll, z.B. einem Computer unter Windows Server2016, Windows Server2012 R2, Windows Server2012, Windows Server2008 R2 oder Windows Server2008 und Routing- und RAS-Dienst, Terminaldienste-Gatewayserver oder dem Remotedesktopgateway kompatibel sind.


-   Sie planen, Bereitstellen von 802.1 X-Authentifizierung für kabelgebundenen oder drahtlosen Zugriff.

Vor dem Bereitstellen dieses rollendients, müssen Sie die folgenden Schritteauf dem Computer ausführen, die Sie als NPS-Server konfigurieren.

-   Führen Sie die Schritteim Abschnitt [Konfigurieren aller Server](#BKMK_configuringAll).

-   Führen Sie die Schritteim Abschnitt [Hinzufügen von Servercomputern zur Domäne und anmelden](#BKMK_joinlogserver)

Bereitstellung von NPS1 des Computers mit dem Rollendienst Netzwerkrichtlinienserver (Network Policy Server, NPS) der Serverrolle Netzwerkrichtlinien- und Zugriffsdienste, müssen Sie folgende Schritteausführen:

-   [Planen der Bereitstellung von NPS1](#bkmk_NetFndtn_Pln_NPS-01)

-   [Installieren von Netzwerkrichtlinienserver (NPS)](#BKMK_installNPS)

-   [Registrieren des NPS-Servers in der Standarddomäne](#BKMK_registerNPS)

> [!NOTE]
> Dieses Handbuch enthält Anweisungen für die Bereitstellung von NPS auf einem eigenständigen Server oder virtuellen Computer mit dem Namen NPS1.  Eine andere empfohlene Bereitstellungsmodell ist die Installation von NPS auf einem Domänencontroller. Wenn Sie lieber die Installation von NPS auf einem Domänencontroller nicht auf einem eigenständigen Server, installieren Sie NPS auf DC1.

##### <a name="bkmk_NetFndtn_Pln_NPS-01"></a>Planen der Bereitstellung von NPS1
Wenn Sie Netzwerkzugriffsserver, z.B. drahtlose Zugriffspunkte oder VPN-Server, nach der Bereitstellung Ihres Hauptnetzwerks Netzwerkzugriffsserver bereitstellen möchten, empfiehlt es sich, dass Sie NPS bereitstellen.

Wenn Sie NPS als Server Remote Authentication Dial-in User Service (RADIUS) verwenden, führt NPS Authentifizierung und Autorisierung für Verbindungsanforderungen über Ihre Netzwerkzugriffsserver aus. NPS ermöglicht darüber hinaus zentral konfigurieren und Verwalten von Netzwerkrichtlinien, die bestimmen, wer auf das Netzwerk zugreifen können, wie sie das Netzwerk zugreifen können, und wenn das Netzwerk zugegriffen werden kann.

Folgendes sind die wichtigsten Planungsschritte vor der Installation von NPS.

- Planen der Benutzerkontendatenbank. Wenn Sie den Server mit NPS zu einer Active Directory-Domäne beitreten, führt NPS standardmäßig Authentifizierung und Autorisierung mithilfe der AD DS-Benutzerkontendatenbank. In einigen Fällen können z.B. mit großen Netzwerken, die NPS als RADIUS-Proxy zu verwenden, um Verbindungsanforderungen an andere RADIUS-Server weitergeleitet Sie NPS auf einem Computer kein Domänenmitglied installieren möchten.

- Planen der RADIUS-Kontoführung. NPS ermöglicht Sie Ressourcenerfassungsdaten in eine SQL Server-Datenbank oder in einer Textdatei auf dem lokalen Computer anmelden. Wenn Sie SQL Server-Protokollierung verwenden möchten, Planen Sie die Installation und Konfiguration des Servers mit SQL Server.

##### <a name="BKMK_installNPS"></a>Installieren von Netzwerkrichtlinienserver (NPS)
Dieses Verfahrens können Sie Netzwerkrichtlinienserver (Network Policy Server, NPS) mithilfe des Hinzufügen von Rollen und Features-Assistenten installieren. NPS ist ein Rollendienst der Serverrolle Netzwerkrichtlinien- und Zugriffsdienste.

> [!NOTE]
> Standardmäßig überwacht NPS RADIUS-Datenverkehr auf den Ports 1812, 1813, 1645 und 1646 für alle installierten Netzwerkadapter. Wenn Windows-Firewall mit erweiterter Sicherheit bei der Installation von NPS aktiviert ist, werden die Firewallausnahmen für diese Ports während der Installation für Internetprotokoll Version 6 \(IPv6\) und IPv4-Datenverkehr automatisch erstellt. Wenn Ihre Netzwerkzugriffsserver für das Senden von RADIUS-Verkehr über andere Ports als die standardmäßigen konfiguriert sind, entfernen Sie die Ausnahmen in der Windows-Firewall mit erweiterter Sicherheit während der Installation von NPS erstellt, und erstellen Sie Ausnahmen für die Ports, die Sie für RADIUS-Datenverkehr verwenden.

**Administrative Anmeldeinformationen**

Um dieses Verfahren auszuführen, müssen Sie Mitglied der werden die **Domänen-Admins** Gruppe.

> [!NOTE]
> Führen Sie dieses Verfahren mithilfe von Windows PowerShell, öffnen Sie PowerShell und geben Sie Folgendes ein, und drücken dann die EINGABETASTE.
>
> `Install-WindowsFeature NPAS -IncludeManagementTools`

###### <a name="to-install-nps"></a>So installieren Sie NPS

1.  Klicken Sie auf NPS1 unter Server-Manager auf **verwalten**, und klicken Sie dann auf **Hinzufügen von Rollen und Features**. Das Hinzufügen von Rollen und Features-Assistent wird geöffnet.

2.  In **Vorbemerkungen**, klicken Sie auf **Weiter**.

    > [!NOTE]
    > Die **Vorbemerkungen** des Hinzufügen von Rollen und Features Assistenten nicht angezeigt wird, wenn Sie zuvor ausgewählt haben **diese Seite standardmäßig überspringen** beim Hinzufügen von Rollen und Features-Assistent ausgeführt wurde.

3.  In **Select Installation Type**, stellen Sie sicher, dass **rollenbasierte oder featurebasierte Installation** ausgewählt ist, und klicken Sie dann auf **Weiter**.

4.  In **Zielserver auswählen**, stellen Sie sicher, dass **wählen Sie einen Server aus dem Serverpool** ausgewählt ist. In **Serverpool**, stellen Sie sicher, dass der lokale Computer ausgewählt ist. Klicken Sie auf **Weiter**.

5.  In **Serverrollen auswählen**im **Rollen**Option **Netzwerkrichtlinien- und Zugriffsdienste**. Ein Dialogfeld gefragt werden, ob sie Features hinzufügen sollten, die für Netzwerkrichtlinien- und Zugriffsdienste erforderlich sind. Klicken Sie auf **Features hinzufügen**, und klicken Sie dann auf **Weiter**.

6.  In **Features auswählen**, klicken Sie auf **Weiter**, und im **Netzwerkrichtlinien- und Zugriffsdienste**, überprüfen Sie die Informationen, die bereitgestellt wird, und klicken Sie dann auf **Weiter**.

7.  In **Rollendienste auswählen**, klicken Sie auf **Netzwerkrichtlinienserver**.  In **Hinzufügen von Features, die für Netzwerkrichtlinienserver erforderlich sind**, klicken Sie auf **Features hinzufügen**. Klicken Sie auf **Weiter**.

8.  In **Installationsauswahl bestätigen**, klicken Sie auf **Zielserver bei Bedarf automatisch neu**. Wenn Sie aufgefordert werden, die Auswahl zu bestätigen, klicken Sie auf **Ja**, und klicken Sie dann auf **installieren**. Der Installationsstatus wird Status während der Installation. Wenn der Vorgang abgeschlossen ist, die Meldung "die Installation war erfolgreich auf *ComputerName*" angezeigt wird, wobei *ComputerName* ist der Name des Computers, auf dem Netzwerkrichtlinienserver installiert. Klicken Sie auf **schließen **.

##### <a name="BKMK_registerNPS"></a>Registrieren des NPS-Servers in der Standarddomäne
Dieses Verfahrens können Sie einen NPS-Server in der Domäne registrieren, in dem der Server Mitglied einer Domäne ist.

NPS-Server müssen in Active Directory registriert werden, damit sie die Berechtigung, die DFÜ-Eigenschaften von Benutzerkonten während des Autorisierungsprozesses zu lesen. Registrieren eines NPS-Servers den Server Fügt die **RAS- und IAS-Server** Gruppe in Active Directory.

**Administrative Anmeldeinformationen**

Um dieses Verfahren auszuführen, müssen Sie Mitglied der werden die **Domänen-Admins** Gruppe.

> [!NOTE]
> Um dieses Verfahren ausführen, indem Sie die Verwendung von Network Shell (Netsh)-Befehlen in Windows PowerShell, öffnen Sie PowerShell und geben Sie Folgendes ein, und drücken dann die EINGABETASTE.
>
> `netsh nps add registeredserver domain=corp.contoso.com server=NPS1.corp.contoso.com`

###### <a name="to-register-an-nps-server-in-its-default-domain"></a>So registrieren Sie einen NPS-Server in seiner Standarddomäne

1.  Klicken Sie auf NPS1 unter Server-Manager auf Extras, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Die Netzwerk-Gruppenrichtlinien-MMC wird geöffnet.

2.  Mit der rechten Maustaste **NPS (lokal)**, und klicken Sie dann auf **Server in Active Directory registrieren**. Die **Netzwerkrichtlinienserver** Dialogfeld wird geöffnet.

3.  In **Netzwerkrichtlinienserver**, klicken Sie auf **OK**, und klicken Sie dann auf **OK** erneut.

Weitere Informationen zu Network Policy Server, finden Sie unter [(Network Policy Server, NPS)](../technologies/nps/nps-top.md).

#### <a name="BKMK_IIS"></a>Bereitstellen von WEB1

Die Rolle "Webserver (IIS)" in Windows Server2016 bietet eine sichere, einfach zu verwaltende, modulare und erweiterbare Plattform für ein zuverlässiges Hosting von Websites, Diensten und Anwendungen. Mit Internet Information Services (IIS), können Sie Informationen gemeinsamen mit Benutzern im Internet, Intranet oder einem Extranet freigeben. IIS ist eine einheitliche Webplattform, die IIS, ASP.NET, FTP-Dienste, PHP und Windows Communication Foundation (WCF) integriert wird.

Zusätzlich zu, sodass Sie eine Zertifikatsperrliste für den Zugriff durch Domänenmitgliedscomputer zu veröffentlichen, kann die Serverrolle Webserver (IIS) für Sie einrichten und verwalten mehrere Websites, Webanwendungen und FTP-Sites. IIS bietet außerdem die folgenden Vorteile:

-   Maximale websicherheit durch einen reduzierten Fuß und automatischer Anwendungsisolation.

-   Einfaches Bereitstellen und Ausführen ASP.NET klassisches ASP und PHP-Webanwendungen auf demselben Server.

-   Anwendungsisolation durch seine Arbeitsprozesse eine eindeutige Identität und Sandbox-Konfiguration in der Standardeinstellung weiteren Reduzierung von Sicherheitsrisiken.

-   Leicht hinzufügen, entfernen und sogar Ersetzen von integrierten IIS-Komponenten durch benutzerdefinierte Module, Kundenanforderungen.

-   Beschleunigte Websites durch integriertes dynamisches Zwischenspeichern und erweiterte Komprimierung.

Zum Bereitstellen von WEB1 der Computer, auf der die Serverrolle Webserver (IIS) ausgeführt wird ist, müssen Sie die folgenden Schritteausführen:

-   Führen Sie die Schritteim Abschnitt [Konfigurieren aller Server](#BKMK_configuringAll).

-   Führen Sie die Schritteim Abschnitt [Hinzufügen von Servercomputern zur Domäne und anmelden](#BKMK_joinlogserver)

-   [Installieren der Serverrolle Webserver (IIS)](#BKMK_install_IIS)

##### <a name="BKMK_install_IIS"></a>Installieren der Serverrolle Webserver (IIS)
Um dieses Verfahren auszuführen, müssen Sie Mitglied der werden die **Administratoren** Gruppe.

> [!NOTE]
> Führen Sie dieses Verfahren mithilfe von Windows PowerShell, öffnen Sie PowerShell und geben Sie Folgendes ein, und drücken dann die EINGABETASTE.
>
> `Install-WindowsFeature Web-Server -IncludeManagementTools`

1.  In **Server-Manager**, klicken Sie auf **verwalten**, und klicken Sie dann auf **Hinzufügen von Rollen und Features**. Das Hinzufügen von Rollen und Features-Assistent wird geöffnet.

2.  In **Vorbemerkungen**, klicken Sie auf **Weiter**.

    > [!NOTE]
    > Die **Vorbemerkungen** des Hinzufügen von Rollen und Features Assistenten nicht angezeigt wird, wenn Sie zuvor ausgewählt haben **diese Seite standardmäßig überspringen** beim Hinzufügen von Rollen und Features-Assistent ausgeführt wurde.

3.  Auf der **Select Installation Type** auf **Weiter**.

4.  Auf der **Zielserver auswählen** Seite, stellen Sie sicher, dass der lokale Computer ausgewählt ist, und klicken Sie dann auf **Weiter**.

5.  Auf der **Serverrollen auswählen** Seite, führen Sie einen Bildlauf aus, und wählen Sie **Webserver (IIS)**. Die **Hinzufügen von Features, die für Webserver (IIS) erforderlich sind** Dialogfeld wird geöffnet. Klicken Sie auf **Features hinzufügen**, und klicken Sie dann auf **Weiter**.

6.  Klicken Sie auf **Weiter** bis Sie akzeptiert haben alle Standardeinstellungen Webserver, und klicken Sie dann auf **installieren**.

7.  Stellen Sie sicher, dass alle Installationen erfolgreich waren, und klicken Sie dann auf **schließen**.

## <a name="BKMK_resources"></a>Zusätzliche technische Ressourcen
Weitere Informationen zu den Technologien in diesem Handbuch finden Sie unter den folgenden Ressourcen:

 Windows Server 2016, Windows Server2012 R2 und Windows Server2012 technischen Bibliotheksressourcen

-   [Neues in Active Directory-Domänendienste (AD DS) in Windows Server2016](https://technet.microsoft.com/en-us/library/mt163897.aspx)

-   [Active Directory Übersicht über Domänendienste](https://technet.microsoft.com/library/hh831484.aspx) am https://technet.microsoft.com/library/hh831484.aspx.

-   [Domain Name System (DNS) – Übersicht](https://technet.microsoft.com/library/hh831667.aspx) am https://technet.microsoft.com/library/hh831667.aspx.

-   [Implementieren der DNS Admins-Rolle](https://technet.microsoft.com/library/cc756152(WS.10).aspx)

-   [Übersicht über die Dynamic Host Configuration Protocol (DHCP)](https://technet.microsoft.com/library/hh831825.aspx) am https://technet.microsoft.com/library/hh831825.aspx.

-   [Netzwerkrichtlinien- und Zugriffsdienste: Übersicht](https://technet.microsoft.com/library/hh831683.aspx) am https://technet.microsoft.com/library/hh831683.aspx.

-   [Übersicht über die Web Server (IIS)](https://technet.microsoft.com/library/hh831725.aspx) am https://technet.microsoft.com/library/hh831725.aspx.

## <a name="BKMK_appendix"></a>Anhänge A bis E
Die folgenden Abschnitte enthalten weitere Informationen zur Konfiguration für Computer, auf denen andere Betriebssysteme als Windows Server2016, Windows10, Windows Server2012 und Windows8 ausgeführt werden. Darüber hinaus wird ein netzwerkvorbereitungsblatt zur Unterstützung bei der Bereitstellung bereitgestellt.

1.  [AnhangA – Umbenennen von Computern](#BKMK_A)

2.  [AnhangB - Konfigurieren von statischen IP-Adressen](#BKMK_B)

3.  [AnhangC – Hinzufügen von Computern zur Domäne](#BKMK_C)

4.  [AnhangD – Anmelden bei der Domäne](#BKMK_D)

5.  [AnhangE – Vorbereitungsblatt für die Planung eines Hauptnetzwerks](#BKMK_E)

## <a name="BKMK_A"></a>AnhangA – Umbenennen von Computern
Die Verfahren können in diesem AbschnittSie Computern unter Windows Server2008 R2, Windows7, Windows Server2008 und Windows Vista mit einer neuen Computernamen zuweisen.

-   [Windows Server 2008 R2 und Windows 7](#bkmk_NetFndtn_Pln_rename_R2)

-   [Windows Server 2008 und windowsvista](#bkmk_NetFndtn_Pln_Renam08)

### <a name="bkmk_NetFndtn_Pln_rename_R2"></a>Windows Server2008 R2 und Windows7
Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um diese Schritteausführen.

##### <a name="to-rename-computers-running-windows-server-2008-r2-and-windows-7"></a>Zum Umbenennen von Computern unter Windows Server2008 R2 und Windows7

1.  Klicken Sie auf **starten**, mit der rechten Maustaste **Computer**, und klicken Sie dann auf **Eigenschaften**. Die **System** Dialogfeld wird geöffnet.

2.  In **Einstellungen für Computernamen, Domäne und Arbeitsgruppe**, klicken Sie auf **Einstellungsänderungen**. Die **Systemeigenschaften** Dialogfeld wird geöffnet.

    > [!NOTE]
    > Auf Computern Windows7 ausgeführt, bevor die **Systemeigenschaften** das Dialogfeld wird angezeigt, die **User Account Control** Dialogfeld öffnet, die Zustimmung zum Fortfahren abzufragen. Klicken Sie auf **Weiter** um den Vorgang fortzusetzen.

3.  Klicken Sie auf **ändern**. Die **Computer bzw.-domänenänderungen** das Dialogfeld wird geöffnet.

4.  In **Computername**, geben Sie den Namen für den Computer. Geben Sie beispielsweise, wenn Sie den Computer DC1 benennen möchten, **DC1**.

5.  Klicken Sie auf **OK** klicken Sie zweimal auf **schließen**, und klicken Sie dann auf **jetzt neu starten** den Computer neu starten.

### <a name="bkmk_NetFndtn_Pln_Renam08"></a>Windows Server 2008 und windowsvista
Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um diese Schritteausführen.

##### <a name="to-rename-computers-running-windows-server-2008-and-windows-vista"></a>Zum Umbenennen von Computern unter Windows Server2008 und Windows Vista

1.  Klicken Sie auf **starten**, mit der rechten Maustaste **Computer**, und klicken Sie dann auf **Eigenschaften**. Die **System** Dialogfeld wird geöffnet.

2.  In **Einstellungen für Computernamen, Domäne und Arbeitsgruppe**, klicken Sie auf **Einstellungsänderungen**. Die **Systemeigenschaften** Dialogfeld wird geöffnet.

    > [!NOTE]
    > Auf Computern unter Windows Vista ausgeführt, bevor die **Systemeigenschaften** das Dialogfeld wird angezeigt, die **User Account Control** Dialogfeld öffnet, die Zustimmung zum Fortfahren abzufragen. Klicken Sie auf **Weiter** um den Vorgang fortzusetzen.

3.  Klicken Sie auf **ändern**. Die **Computer bzw.-domänenänderungen** das Dialogfeld wird geöffnet.

4.  In **Computername**, geben Sie den Namen für den Computer. Geben Sie beispielsweise, wenn Sie den Computer DC1 benennen möchten, **DC1**.

5.  Klicken Sie auf **OK** klicken Sie zweimal auf **schließen**, und klicken Sie dann auf **jetzt neu starten** den Computer neu starten.

## <a name="BKMK_B"></a>AnhangB - Konfigurieren von statischen IP-Adressen
Dieses Thema enthält Verfahren zum Konfigurieren von statischen IP-Adressen auf Computern unter folgendem Betriebssystem erstellt:

-   [Windows Server2008 R2](#bkmk_R2Cng_WS08R2IP)

-   [Windows Server 2008](#bkmk_NetFndtn_Pln_CfgStatic08)

### <a name="bkmk_R2Cng_WS08R2IP"></a>Windows Server2008 R2
Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren auszuführen.

##### <a name="to-configure-a-static-ip-address-on-a-computer-running-windows-server-2008-r2"></a>So konfigurieren Sie eine statische IP-Adresse auf einem Computer unter Windows Server2008 R2

1.  Klicken Sie auf **starten**, und klicken Sie dann auf **Systemsteuerung**.

2.  In **Systemsteuerung**, klicken Sie auf **Netzwerk und Internet**. **Netzwerk und Internet** wird geöffnet.

    In **Netzwerk und Internet**, klicken Sie auf **Netzwerk- und Freigabecenter**. **Netzwerk- und Freigabecenter** wird geöffnet.

3.  In **Netzwerk- und Freigabecenter**, klicken Sie auf **adaptereinstellungen ändern**. **Netzwerkverbindungen** wird geöffnet.

4.  In **Netzwerkverbindungen**, mit der rechten Maustaste der Netzwerkverbindungs, die Sie konfigurieren möchten, und klicken Sie dann auf **Eigenschaften**.

5.  In **Eigenschaften von LAN-Verbindung**im **diese Verbindung verwendet folgende Elemente**Option **Internet Protocol Version 4 (TCP/IPv4)**, und klicken Sie dann auf **Eigenschaften**. Die **Eigenschaften von Internetprotokoll Version 4 (TCP/IPv4)** Dialogfeld wird geöffnet.

6.  In **Eigenschaften von Internetprotokoll Version 4 (TCP/IPv4)**auf die **allgemeine** auf **verwenden Sie die folgende IP-Adresse**. In **IP-Adresse**, geben Sie die IP-Adresse, die Sie verwenden möchten.

7.  Drücken Sie Tab, um den Cursor im **Subnetzmaske**. Ein Standardwert für die Subnetzmaske wird automatisch eingegeben. Entweder akzeptieren Sie die Standardsubnetzmaske, oder geben Sie die Subnetzmaske, die Sie verwenden möchten.

8.  In **Standardgateway**, geben Sie die IP-Adresse des Standardgateways.

9. In **Bevorzugter DNS-Server**, geben Sie die IP-Adresse Ihres DNS-Servers. Wenn Sie den lokalen Computer als bevorzugten DNS-Server verwenden möchten, geben Sie die IP-Adresse des lokalen Computers.

10. In **alternativer DNS-Server**, geben Sie die IP-Adresse des alternativen DNS-Servers, falls vorhanden. Wenn Sie den lokalen Computer als alternativen DNS-Server verwenden möchten, geben Sie die IP-Adresse des lokalen Computers.

11. Klicken Sie auf **OK**, und klicken Sie dann auf **schließen**.

### <a name="bkmk_NetFndtn_Pln_CfgStatic08"></a>Windows Server 2008
Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um diese Schritteausführen.

##### <a name="to-configure-a-static-ip-address-on-a-computer-running-windows-server-2008"></a>So konfigurieren Sie eine statische IP-Adresse auf einem Computer unter Windows Server2008

1.  Klicken Sie auf **starten**, und klicken Sie dann auf **Systemsteuerung**.

2.  In **Systemsteuerung**, überprüfen Sie, ob **Standardansicht** ausgewählt ist, und doppelklicken Sie dann auf **Netzwerk- und Freigabecenter**.

3.  In **Netzwerk- und Freigabecenter**im **Aufgaben**, klicken Sie auf **Netzwerkverbindungen verwalten**.

4.  In **Netzwerkverbindungen**, mit der rechten Maustaste der Netzwerkverbindungs, die Sie konfigurieren möchten, und klicken Sie dann auf **Eigenschaften**.

5.  In **Eigenschaften von LAN-Verbindung**im **diese Verbindung verwendet folgende Elemente**Option **Internet Protocol Version 4 (TCP/IPv4)**, und klicken Sie dann auf **Eigenschaften**. Die **Eigenschaften von Internetprotokoll Version 4 (TCP/IPv4)** Dialogfeld wird geöffnet.

6.  In **Eigenschaften von Internetprotokoll Version 4 (TCP/IPv4)**auf die **allgemeine** auf **verwenden Sie die folgende IP-Adresse**. In **IP-Adresse**, geben Sie die IP-Adresse, die Sie verwenden möchten.

7.  Drücken Sie Tab, um den Cursor im **Subnetzmaske**. Ein Standardwert für die Subnetzmaske wird automatisch eingegeben. Entweder akzeptieren Sie die Standardsubnetzmaske, oder geben Sie die Subnetzmaske, die Sie verwenden möchten.

8.  In **Standardgateway**, geben Sie die IP-Adresse des Standardgateways.

9. In **Bevorzugter DNS-Server**, geben Sie die IP-Adresse Ihres DNS-Servers. Wenn Sie den lokalen Computer als bevorzugten DNS-Server verwenden möchten, geben Sie die IP-Adresse des lokalen Computers.

10. In **alternativer DNS-Server**, geben Sie die IP-Adresse des alternativen DNS-Servers, falls vorhanden. Wenn Sie den lokalen Computer als alternativen DNS-Server verwenden möchten, geben Sie die IP-Adresse des lokalen Computers.

11. Klicken Sie auf **OK**, und klicken Sie dann auf **schließen**.

## <a name="BKMK_C"></a>AnhangC – Hinzufügen von Computern zur Domäne
Diese Verfahren können Sie Computer unter Windows Server2008 R2, Windows7, Windows Server2008 und Windows Vista mit der Domäne hinzugefügt werden.

-   [Windows Server 2008 R2 und Windows 7](#BKMK_c1)

-   [Windows Server 2008 und windowsvista](#BKMK_c2)

> [!IMPORTANT]
> Um einen Computer einer Domäne hinzugefügt haben, müssen Sie auf dem Computer mit dem lokalen Administratorkonto angemeldet werden, oder wenn Sie auf den Computer mit einem Benutzerkonto, die nicht lokalen Computer administrativen Anmeldeinformationen verfügen angemeldet sind, müssen Sie die Anmeldeinformationen für das lokale Administratorkonto angeben, bei der den Computer der Domäne hinzugefügt. Darüber hinaus müssen Sie ein Benutzerkonto in der Domäne haben Sie den Computer hinzufügen möchten. Bei der den Computer der Domäne beitritt werden Sie für Ihre Domänenanmeldeinformationen (Benutzername und Kennwort) aufgefordert.

### <a name="BKMK_c1"></a>Windows Server2008 R2 und Windows7
Mitgliedschaft in **Domänenbenutzer**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren auszuführen.

##### <a name="to-join-computers-running-windows-server-2008-r2-and-windows-7-to-the-domain"></a>Auf Computern unter Windows Server2008 R2 und Windows7 mit der Domäne beitreten

1.  Melden Sie sich an den Computer mit dem lokalen Administratorkonto an.

2.  Klicken Sie auf **starten**, mit der rechten Maustaste **Computer**, und klicken Sie dann auf **Eigenschaften**. Die **System** Dialogfeld wird geöffnet.

3.  In **Einstellungen für Computernamen, Domäne und Arbeitsgruppe**, klicken Sie auf **Einstellungsänderungen**. Die **Systemeigenschaften** Dialogfeld wird geöffnet.

    > [!NOTE]
    > Auf Computern Windows7 ausgeführt, bevor die **Systemeigenschaften** das Dialogfeld wird angezeigt, die **User Account Control** Dialogfeld öffnet, die Zustimmung zum Fortfahren abzufragen. Klicken Sie auf **Weiter** um den Vorgang fortzusetzen.

4.  Klicken Sie auf **ändern**. Die **Computer bzw.-domänenänderungen** das Dialogfeld wird geöffnet.

5.  In **Computername**im **Mitglied**Option **Domäne**, und geben Sie den Namen der Domäne hinzugefügt werden soll. Geben Sie z.B. ist der Domänenname corp.contoso.com, **corp.contoso.com**.

6.  Klicken Sie auf **OK**. Die **Windows-Sicherheit** Dialogfeld wird geöffnet.

7.  In **Computer bzw.-domänenänderungen**im **Benutzernamen**, geben Sie den Benutzernamen ein, und im **Kennwort**, geben Sie das Kennwort ein, und klicken Sie dann auf **OK**. Die **Computer bzw.-domänenänderungen** das Dialogfeld wird angezeigt, und Sie werden bei der Domänenbenutzers begrüßt. Klicken Sie auf **OK**.

8.  Die **Computer bzw.-domänenänderungen** das Dialogfeld zeigt einer Meldung angezeigt, dass Sie den Computer, um die Änderungen zu übernehmen neu gestartet werden müssen. Klicken Sie auf **OK**.

9. Auf der **Systemeigenschaften** Dialogfeld auf die **Computername** auf **schließen**. Die **Microsoft Windows** Dialogfeld wird geöffnet und zeigt die Meldung, erneut an, dass Sie den Computer, um die Änderungen zu übernehmen neu gestartet werden müssen. Klicken Sie auf **jetzt neu starten**.

### <a name="BKMK_c2"></a>Windows Server 2008 und windowsvista
Mitgliedschaft in **Domänenbenutzer**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren auszuführen.

##### <a name="to-join-computers-running-windows-server-2008-and-windows-vista-to-the-domain"></a>Auf Computern unter Windows Server2008 und Windows Vista mit der Domäne beitreten

1.  Melden Sie sich an den Computer mit dem lokalen Administratorkonto an.

2.  Klicken Sie auf **starten**, mit der rechten Maustaste **Computer**, und klicken Sie dann auf **Eigenschaften**. Die **System** Dialogfeld wird geöffnet.

3.  In **Einstellungen für Computernamen, Domäne und Arbeitsgruppe**, klicken Sie auf **Einstellungsänderungen**. Die **Systemeigenschaften** Dialogfeld wird geöffnet.

4.  Klicken Sie auf **ändern**. Die **Computer bzw.-domänenänderungen** das Dialogfeld wird geöffnet.

5.  In **Computername**im **Mitglied**Option **Domäne**, und geben Sie den Namen der Domäne hinzugefügt werden soll. Geben Sie z.B. ist der Domänenname corp.contoso.com, **corp.contoso.com**.

6.  Klicken Sie auf **OK**. Die **Windows-Sicherheit** Dialogfeld wird geöffnet.

7.  In **Computer bzw.-domänenänderungen**im **Benutzernamen**, geben Sie den Benutzernamen ein, und im **Kennwort**, geben Sie das Kennwort ein, und klicken Sie dann auf **OK**. Die **Computer bzw.-domänenänderungen** das Dialogfeld wird angezeigt, und Sie werden bei der Domänenbenutzers begrüßt. Klicken Sie auf **OK**.

8.  Die **Computer bzw.-domänenänderungen** das Dialogfeld zeigt einer Meldung angezeigt, dass Sie den Computer, um die Änderungen zu übernehmen neu gestartet werden müssen. Klicken Sie auf **OK**.

9. Auf der **Systemeigenschaften** Dialogfeld auf die **Computername** auf **schließen**. Die **Microsoft Windows** Dialogfeld wird geöffnet und zeigt die Meldung, erneut an, dass Sie den Computer, um die Änderungen zu übernehmen neu gestartet werden müssen. Klicken Sie auf **jetzt neu starten**.

## <a name="BKMK_D"></a>AnhangD – Anmelden bei der Domäne
Diese Verfahren können Sie mit der Domäne mit einem Computer unter Windows Server2008 R2, Windows7, Windows Server2008 und Windows Vista anmelden.

-   [Windows Server 2008 R2 und Windows 7](#BKMK_d1)

-   [Windows Server 2008 und windowsvista](#BKMK_d2)

### <a name="BKMK_d1"></a>Windows Server2008 R2 und Windows7
Mitgliedschaft in **Domänenbenutzer**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren auszuführen.

##### <a name="log-on-to-the-domain-using-computers-running-windows-server-2008-r2-and-windows-7"></a>Melden Sie sich bei der Domäne mit Computern unter Windows Server2008 R2 und Windows7

1.  Melden Sie den Computer oder starten Sie den Computer neu.

2.  Drücken Sie STRG+ALT+ENTF. Der Anmeldebildschirm angezeigt wird.

3.  Klicken Sie auf **Benutzer wechseln**, und klicken Sie dann auf **anderer Benutzer**.

4.  In **Benutzernamen**, geben Sie Ihre Domäne und den Namen im Format *Domäne\Benutzer*. Z.B. zum Anmelden bei der Domäne corp.contoso.com mit einem Konto mit dem Namen **Benutzer-01**, Typ **corp\benutzer-01**.

5.  In **Kennwort**, geben Sie das Domänenkennwort ein, und klicken Sie auf den Pfeil, oder drücken Sie die EINGABETASTE.

### <a name="BKMK_d2"></a>Windows Server 2008 und windowsvista
Mitgliedschaft in **Domänenbenutzer**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren auszuführen.

##### <a name="log-on-to-the-domain-using-computers-running-windows-server-2008-and-windows-vista"></a>Melden Sie sich bei der Domäne mit Computern unter Windows Server2008 und Windows Vista

1.  Melden Sie den Computer oder starten Sie den Computer neu.

2.  Drücken Sie STRG+ALT+ENTF. Der Anmeldebildschirm angezeigt wird.

3.  Klicken Sie auf **Benutzer wechseln**, und klicken Sie dann auf **anderer Benutzer**.

4.  In **Benutzernamen**, geben Sie Ihre Domäne und den Namen im Format *Domäne\Benutzer*. Z.B. zum Anmelden bei der Domäne corp.contoso.com mit einem Konto mit dem Namen **Benutzer-01**, Typ **corp\benutzer-01**.

5.  In **Kennwort**, geben Sie das Domänenkennwort ein, und klicken Sie auf den Pfeil, oder drücken Sie die EINGABETASTE.

## <a name="BKMK_E"></a>AnhangE – Vorbereitungsblatt für die Planung eines Hauptnetzwerks
Diese die Planung eines Hauptnetzwerks können Sie um zur Installation eines Hauptnetzwerks erforderlichen Informationen zu sammeln. Dieses Thema enthält Tabellen, die die einzelnen Konfigurationselemente für jeden Server enthalten, für die Sie Informationen oder bestimmte Werte während der Installation oder Konfiguration angeben müssen. Für jedes Konfigurationselement werden Beispielwerte bereitgestellt.

Für die Planung und Nachverfolgung, werden die Leerzeichen in jeder Tabelle dienen soll, geben Sie die Werte für Ihre Bereitstellung verwendeten bereitgestellt. Wenn Sie die Werte in diesen Tabellen anmelden, sollten Sie die Informationen an einem sicheren Ort speichern.

Die folgenden Links wechseln in den Abschnitten in diesem Thema, die Konfigurationselemente und Beispielwerte, die in diesem Handbuch dargestellten Bereitstellung zugeordnet sind.

1.  [Installieren von Active Directory-Domänendienste und DNS](#BKMK_FndtnPrep_InstallAD)

    -   [Konfigurieren einer DNS-Reverse-Lookupzone](#BKMK_FndtnPrep_DNSRevrsLook)

2.  [Installieren von DHCP](#BKMK_FndtnPrep_InstallDHCP)

    -   [Erstellen eines Ausschlussbereichs in DHCP](#BKMK_FndtnPrep_DHCP_Exclusn)

    -   [Erstellen eines neuen DHCP-Bereichs](#bkmk_NetFndtn_Pln_DHCP_NewScope)

3.  [Installieren von Netzwerkrichtlinienserver (optional)](#BKMK_FndtnPrep_InstallNPS)

### <a name="BKMK_FndtnPrep_InstallAD"></a>Installieren von Active Directory-Domänendienste und DNS
Die Tabellen in diesem Abschnittenthalten Konfigurationselemente für die Installationsvorbereitung und die Installation von Active Directory-Domänendienste (AD DS) und DNS.

##### <a name="pre-installation-configuration-items-for-ad-ds-and-dns"></a>Vor der Installation von Konfigurationselementen für AD DS und DNS
Die folgenden Tabellen Liste vor der Installation von Konfigurationselementen, siehe [Konfigurieren aller Server](#BKMK_configuringAll):

-   [Konfigurieren Sie eine statische IP-Adresse](#BKMK_ip)

|Konfigurationselemente|Beispielwerte|Werte|
|-----------------------|------------------|----------|
|IP-Adresse|10.0.0.2||
|Subnetzmaske|255.255.255.0||
|Standard-Gateway|10.0.0.1||
|Bevorzugter DNS-Server|127.0.0.1||
|Alternativer DNS-Server|10.0.0.15||

-   [Umbenennen des Computers](#BKMK_rename)

|Konfigurationselement|Beispiel für einen Wert|Wert|
|----------------------|-----------------|---------|
|Computername|DC1||

##### <a name="ad-ds-and-dns-installation-configuration-items"></a>AD DS und DNS-Installation von Konfigurationselementen
Konfigurationselemente für die Windows Server-Hauptnetzwerk Bereitstellungsverfahren [Installieren von AD DS und DNS für eine neue Gesamtstruktur](#BKMK_installAD-DNS):

|Konfigurationselemente|Beispielwerte|Werte|
|-----------------------|------------------|----------|
|Vollständiger DNS-name|corp.contoso.com||
|Funktionsebene der Gesamtstruktur|Windows Server 2003||
|Active Directory-Domänendienste-Datenbank-Ordner|E:\Configuration\\<br /><br />Oder übernehmen Sie den Standardspeicherort.||
|Active Directory-Domänendienste Ordnerspeicherort für Protokolldateien|E:\Configuration\\<br /><br />Oder übernehmen Sie den Standardspeicherort.||
|Active Directory Domain Services SYSVOL-Ordner|E:\Configuration\\<br /><br />Oder übernehmen Sie den Standardspeicherort||
|Directory wiederherstellen Administratorkennwort|J * p2leO4$ F||
|Name der Antwortdatei (optional)|AD-DS_AnswerFile||

#### <a name="BKMK_FndtnPrep_DNSRevrsLook"></a>Konfigurieren einer DNS-Reverse-Lookupzone

|Konfigurationselemente|Beispielwerte|Werte|
|-----------------------|------------------|----------|
|Typ:|-Primäre Zone<br />-Sekundäre Zone<br />-Stub Zone||
|Zonentyp<br /><br />**Speichern Sie die Zone in Active Directory**|– Aktiviert<br />– Nicht ausgewählt||
|Active Directory-Zonenreplikationsbereich|-Um alle DNS-Server in dieser Gesamtstruktur<br />-Um alle DNS-Server in dieser Domäne<br />-Auf alle Domänencontroller in dieser Domäne<br />– Auf allen Domänencontrollern, die im Bereich dieser Verzeichnispartition angegeben||
|Name der Reverse-Lookupzone<br /><br />(IP-Typ)|-IPv4 Reverse-Lookupzone<br />-IPv6 Reverse-Lookupzone||
|Name der Reverse-Lookupzone<br /><br />(Netzwerk-ID)|10.0.0||

### <a name="BKMK_FndtnPrep_InstallDHCP"></a>Installieren von DHCP
Die Tabellen in diesem Abschnittenthalten Konfigurationselemente für die Installationsvorbereitung und die Installation von DHCP.

##### <a name="pre-installation-configuration-items-for-dhcp"></a>Vor der Installation von Konfigurationselementen für DHCP
Die folgenden Tabellen Liste vor der Installation von Konfigurationselementen, siehe [Konfigurieren aller Server](#BKMK_configuringAll):

-   [Konfigurieren Sie eine statische IP-Adresse](#BKMK_ip)

|Konfigurationselemente|Beispielwerte|Werte|
|-----------------------|------------------|----------|
|IP-Adresse|10.0.0.3||
|Subnetzmaske|255.255.255.0||
|Standard-Gateway|10.0.0.1||
|Bevorzugter DNS-Server|10.0.0.2||
|Alternativer DNS-Server|10.0.0.15||

-   [Umbenennen des Computers](#BKMK_rename)

|Konfigurationselement|Beispiel für einen Wert|Wert|
|----------------------|-----------------|---------|
|Computername|DHCP1||

##### <a name="dhcp-installation-configuration-items"></a>DHCP-Installation von Konfigurationselementen
Konfigurationselemente für die Windows Server-Hauptnetzwerk Bereitstellungsverfahren [installieren Dynamic Host Configuration Protocol (DHCP)](#BKMK_installDHCP):

|Konfigurationselemente|Beispielwerte|Werte|
|-----------------------|------------------|----------|
|Bindungen für die Netzwerkverbindung|Ethernet||
|DNS-servereinstellungen|DC1||
|IP-Adresse des bevorzugten DNS-Servers|10.0.0.2||
|IP-Adresse des alternativen DNS-Servers|10.0.0.15||
|Bereichsname|Corp1||
|Start-IP-Adresse|10.0.0.1||
|End-IP-Adresse|10.0.0.254||
|Subnetzmaske|255.255.255.0||
|Standardgateway (optional)|10.0.0.1||
|Leasedauer|Acht Tage||
|Betriebsmodus des IPv6-DHCP-Servers|Nicht aktiviert.||

#### <a name="BKMK_FndtnPrep_DHCP_Exclusn"></a>Erstellen eines Ausschlussbereichs in DHCP
Konfigurationselemente ein Ausschlussbereichs beim Erstellen eines Bereichs in DHCP erstellen.

|Konfigurationselemente|Beispielwerte|Werte|
|-----------------------|------------------|----------|
|Bereichsname|Corp1||
|Beschreibung des Bereichs|Subnetz 1 der zentrale||
|Start IP-Adresse des Ausschlussbereichs|10.0.0.1||
|Ende IP-Adresse des Ausschlussbereichs|10.0.0.15||

#### <a name="bkmk_NetFndtn_Pln_DHCP_NewScope"></a>Erstellen eines neuen DHCP-Bereichs
Konfigurationselemente für die Windows Server-Hauptnetzwerk Bereitstellungsverfahren [erstellen und aktivieren Sie einen neuen DHCP-Bereich](#BKMK_newscopeDHCP):

|Konfigurationselemente|Beispielwerte|Werte|
|-----------------------|------------------|----------|
|Name des neuen Bereichs|Corp2||
|Beschreibung des Bereichs|Zentrale Subnetz 2||
|(IP-Adressbereich)<br /><br />Start-IP-Adresse|10.0.1.1||
|(IP-Adressbereich)<br /><br />End-IP-Adresse|10.0.1.254||
|Länge|8||
|Subnetzmaske|255.255.255.0||
|(Ausschlussbereich) Start-IP-Adresse|10.0.1.1||
|Ende IP-Adresse des Ausschlussbereichs|10.0.1.15||
|Leasedauer<br /><br />Tage<br /><br />Stunden<br /><br />Minuten|-   8<br />-   0<br />-   0||
|Router (Standardgateway)<br /><br />IP-Adresse|10.0.1.1||
|Übergeordnete DNS-Domäne|corp.contoso.com||
|DNS-Server<br /><br />IP-Adresse|10.0.0.2||

### <a name="BKMK_FndtnPrep_InstallNPS"></a>Installieren von Netzwerkrichtlinienserver (optional)
Die Tabellen in diesem Abschnittenthalten Konfigurationselemente für die Installationsvorbereitung und die Installation von NPS.

##### <a name="pre-installation-configuration-items"></a>Vor der Installation von Konfigurationselementen
Die folgenden drei Tabellen enthalten vor der Installation von Konfigurationselementen, wie unter [Konfigurieren aller Server](#BKMK_configuringAll):

-   [Konfigurieren Sie eine statische IP-Adresse](#BKMK_ip)

|Konfigurationselemente|Beispielwerte|Werte|
|-----------------------|------------------|----------|
|IP-Adresse|10.0.0.4||
|Subnetzmaske|255.255.255.0||
|Standard-Gateway|10.0.0.1||
|Bevorzugter DNS-Server|10.0.0.2||
|Alternativer DNS-Server|10.0.0.15||

-   [Umbenennen des Computers](#BKMK_rename)

|Konfigurationselement|Beispiel für einen Wert|Wert|
|----------------------|-----------------|---------|
|Computername|NPS1||

##### <a name="network-policy-server-installation-configuration-items"></a>Network Policy Server-Installation von Konfigurationselementen
Konfigurationselemente für die Windows Server Core NPS-Bereitstellungsverfahren [installieren Network Policy Server (NPS)](#BKMK_installNPS) und [Registrieren des NPS-Servers in der Standarddomäne](#BKMK_registerNPS).

-   Zum Installieren und die Registrierung von NPS sind keine weiteren Konfigurationselemente erforderlich.

