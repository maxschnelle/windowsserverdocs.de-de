---
title: Always On VPN-Technologieübersicht
description: 'Diese Seite Provies eine kurze Übersicht über die Always On VPN-Technologien mit Links zu ausführlichen Dokumenten. '
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: fd3f7c6ca8555e270aabf04bbee6800ed284080c
ms.sourcegitcommit: 4147e092d77d9458696e6686bccefe3788c90508
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2019
ms.locfileid: "9031324"
---
# Übersicht über die Technologie von Always On VPN
>Gilt für: WindowsServer (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows 10

& #171;  [ **Vorherige:** erfahren Sie mehr über die Always On VPN-Erweiterungen](always-on-vpn-enhancements.md)<br>
& #187;  [ **Weiter:** erfahren Sie mehr über die erweiterten Funktionen von Always On VPN](deploy/always-on-vpn-adv-options.md)

Für diese Bereitstellung müssen Sie installieren neuen RAS-Server, auf der Windows Server 2016 ausgeführt wird, sowie einige Ihrer vorhandenen Infrastruktur für die Bereitstellung ändern.

Die folgende Abbildung zeigt die Infrastruktur, die erforderlich sind, um die Always On VPN bereitstellen.

![Always On VPN-Infrastruktur](../../../media/Always-On-Vpn/Ao-Vpn-Overview.jpg)

Der Verbindungsprozess in der folgenden Abbildung dargestellt umfasst die folgenden Schritte aus:

1. Öffentliche DNS-Server mit der Windows 10-VPN-Client wird eine Auflösung Namensabfrage für IP-Adresse des VPN-Gateway führt.

2. Verwenden die IP-Adresse, die vom DNS zurückgegeben, sendet der VPN-Client eine Anforderung der Verbindung mit dem VPN-Gateway.

3. Das VPN-Gateway wird auch als eine Remote Authentication Dial-In User Service \(RADIUS\) konfiguriert Client; der VPN-RADIUS-Client sendet Anforderung der Verbindung an die Organisation/Unternehmens NPS-Servers für verbindungsverarbeitung-Anforderung.

4. NPS-Servers verarbeitet die Anforderung der Verbindung, einschließlich der Durchführung der Autorisierung und Authentifizierung, und legt fest, ob gewähren oder Verweigern der Anforderung der Verbindung.

5. NPS-Servers leitet eine Access-Accept oder verweigern Sie den Zugriff Antwort an das VPN-Gateway.

6. Die Verbindung initiiert oder beendet wird basierend auf der Antwort, die der VPN-Server von NPS-Servers zu erhalten.

Weitere Informationen zu jeder Infrastrukturkomponente, die in der Abbildung oben dargestellt finden Sie unter den folgenden Abschnitten.

>[!NOTE]
>Wenn Sie bereits einige dieser Technologien, die in Ihrem Netzwerk bereitgestellt haben, können Sie die Anweisungen in dieser bereitstellungsanleitung verwenden, zusätzliche Konfigurationsschritte über die Technologien für diesen Zweck Bereitstellung durchführen.

## Domain Name System (DNS)

Interne und externe Domain Name System (DNS)-Zonen erforderlich ist, sind die wird davon ausgegangen, dass die interne Zone eine delegierte Unterdomäne der externen Zone (z. B. "corp.contoso.com" und "contoso.com") ist.

Hier erfahren Sie mehr über [Domain Name System (DNS)](../../../../networking/dns/dns-top.md) oder [Handbuch zum Kernnetzwerk](../../../../networking/core-network-guide/core-network-guide.md).




>[!NOTE] 
>Andere DNS-designs, z. B. Split Brain-DNS (mit dem gleichen Domänennamen intern und extern in separaten DNS-Zonen) oder unabhängige interne und externe Domänen (z. B. contoso.local und "contoso.com") sind ebenfalls möglich. Weitere Informationen zum Bereitstellen von Split Brain-DNS finden Sie unter [Verwendung von DNS-Richtlinien für Split /-Brain DNS-Bereitstellung](../../../../networking/dns/deploy/split-brain-DNS-deployment.md).

## Firewalls

Stellen Sie sicher, dass Ihre Firewalls den Datenverkehr, der für die VPN- sowohl RADIUS-Kommunikation zulassen ordnungsgemäß erforderlich ist.

Weitere Informationen finden Sie unter [Konfigurieren von Firewalls für RADIUS-Datenverkehr](../../../../networking/technologies/nps/nps-firewalls-configure.md).

## Remote Access als VPN-Server RAS-Gateway

In Windows Server 2016 dient die Remote Access-Serverrolle zum sowie sowohl einen Router und RAS-Server ausführen. aus diesem Grund wird eine Breite Palette von Features unterstützt. In diesem Handbuch Bereitstellung, die Sie benötigen nur einer kleinen Teilmenge dieser Features: Unterstützung für IKEv2-VPN-Verbindungen und LAN-routing.

IKEv2 ist ein VPN-Tunneling-Protokoll im Internet Engineering Task Force anfordern für Kommentare 7296 beschrieben. Der wichtigste Vorteil von IKEv2 ist, dass es Unterbrechung der zugrunde liegenden Netzwerkverbindung verträglich. Beispielsweise, wenn die Verbindung vorübergehend nicht mehr auffindbar ist oder wenn ein Benutzer ein Client-PC von einem Netzwerk in ein anderes bewegt, IKEv2 automatisch wiederherstellt, die VPN-Verbindung, wenn die Verbindung wiederhergestellt ist – ohne Eingreifen des Benutzers.

Mit RAS-Gateway, können Sie die VPN-Verbindungen zum Bereitstellen von Endbenutzern mit remote-Zugriff auf das Netzwerk und Ressourcen Ihres Unternehmens bereitstellen. Always On VPN bereitstellen erhält eine dauerhafte Verbindung zwischen Clients und dem Netzwerk Ihres Unternehmens, wenn remote-Computern mit dem Internet verbunden sind. Mit RAS-Gateway können Sie eine Standort-zu-Standort-VPN-Verbindung zwischen zwei Servern an verschiedenen Standorten, z. B. zwischen Ihrem primären Büro und einer Zweigstelle auch Network Address Translation \(NAT\) verwenden, damit Benutzer innerhalb des Netzwerks externe zugreifen können Ressourcen, z. B. das Internet. Außerdem unterstützt RAS-Gateway Border Gateway Protocol (BGP), die dynamische Routingdienste bereitstellt, bei die remote-Standorten auch Edge-Gateways, die BGP unterstützen.

Sie können Remote Access Service (RAS)-Gateways mithilfe von Windows PowerShell-Befehle und der Remote Access Microsoft Management Console (MMC) verwalten.



## Netzwerkrichtlinienserver (Network Policy Server, NPS)

Sie können erstellen und erzwingen organisationsweite Netzwerkzugriffsrichtlinien für die Anforderungsauthentifizierung und Autorisierung. Wenn Sie NPS als Server Remote Authentication Dial-In User Service (RADIUS) verwenden, konfigurieren Sie Zugriff Netzwerkserver, z. B. VPN-Server als RADIUS-Clients in NPS.

Sie konfigurieren auch Netzwerkrichtlinien, die NPS verwendet, um verbindungsanforderungen zu autorisieren, und Sie können die RADIUS-Kontoführung konfigurieren, damit NPS Daten Protokolldateien auf der lokalen Festplatte oder in einer Microsoft SQL Server-Datenbank protokolliert.

Weitere Informationen finden Sie unter [(Network Policy Server, NPS)](../../../../networking/technologies/nps/nps-top.md).


## Active Directory-Zertifikatdienste

Der Zertifizierungsstelle (CA)-Server ist eine Zertifizierungsstelle, die Active Directory-Zertifikatdienste ausgeführt wird. Die VPN-Konfiguration erfordert eine Active Directory-basierte public Key-Infrastruktur (PKI).

Organisationen können AD CS verwenden, um die Sicherheit zu steigern, indem Sie die Identität einer Person, Gerät, oder Dienst zu einem entsprechenden öffentlichen Schlüssel binden. AD CS enthält auch Features, mit die Sie zur Registrierung von Zertifikaten und Sperren in einer Vielzahl von skalierbaren Umgebungen verwalten können. Weitere Informationen finden Sie unter [Active Directory Certificate Services-Übersicht](https://technet.microsoft.com/library/hh831740.aspx) und [Public Key-Infrastruktur-Designrichtlinien](https://social.technet.microsoft.com/wiki/contents/articles/2901.public-key-infrastructure-design-guidance.aspx).

Bei Abschluss der Bereitstellung konfigurieren Sie die folgenden Zertifikatvorlagen für die Zertifizierungsstelle.

-   Die Zertifikatvorlage für die Benutzerauthentifizierung

-   Die Zertifikatvorlage für die VPN-Server-Authentifizierung

-   Die Zertifikatvorlage für die Authentifizierung des NPS-Servers

### Zertifikatvorlagen

Zertifikatvorlagen können die Aufgabe der Verwaltung von einer Zertifizierungsstelle (CA) erheblich vereinfachen, indem Sie zum Ausstellen von Zertifikaten, die vorkonfiguriert sind für die ausgewählten Vorgänge zugelassen wird. Das Zertifikatvorlagen-MMC-Snap-in können Sie die folgenden Aufgaben ausführen.

-   Anzeigen von Eigenschaften für jede Zertifikatvorlage.

-   Kopieren und Bearbeiten von Zertifikatvorlagen.

-   Steuern, welche Benutzer und Computer Vorlagen lesen und Registrieren von Zertifikaten können.

-   Führen Sie andere Verwaltungsaufgaben im Zusammenhang mit Zertifikatvorlagen.

Zertifikatvorlagen sind ein wesentlicher Bestandteil von einer Unternehmens-Zertifizierungsstelle (CA). Sie sind ein wichtiger Bestandteil der Zertifikatrichtlinie für eine Umgebung, die den Satz von Regeln und Formate für die Registrierung von Zertifikaten, Verwendung und Verwaltung.

Weitere Informationen finden Sie unter [Zertifikatvorlagen](https://technet.microsoft.com/library/cc730705.aspx).

### Digitale Zertifikate

Dieses bereitstellungsanleitung enthält Anweisungen für die Verwendung von Active Directory-Zertifikatdienste (AD CS) registrieren sowohl für Remote Access und NPS-Infrastrukturserver Zertifikate automatisch registrieren. AD CS können Sie eine public Key-Infrastruktur (PKI) erstellen und Bereitstellen von Kryptografie mit öffentlichem Schlüssel, digitale Zertifikate und digitale Signatur, die Funktionen für Ihre Organisation.

Wenn Sie digitale Zertifikate für die Authentifizierung zwischen Computern in Ihrem Netzwerk verwenden, erhalten die Zertifikate:

1.  Vertraulichkeit durch die Verschlüsselung.

2.  Integrität durch digitale Signaturen.

3.  Authentifizierung durch einen Computer, Benutzer oder Geräte Konten auf einem Computernetzwerk Zertifikatschlüssel zuordnen.

Weitere Informationen finden Sie unter [AD CS-Schritt-für-Schritt-Anleitung: Bereitstellung von zwei Ebene PKI-Hierarchie](https://social.technet.microsoft.com/wiki/contents/articles/15037.ad-cs-step-by-step-guide-two-tier-pki-hierarchy-deployment.aspx).

## Active Directory-Domänendienste (AD DS)

AD DS bietet eine verteilte Datenbank, die speichert und Informationen zu Netzwerkressourcen und anwendungsspezifische Daten aus Verzeichnis-fähige Anwendung verwaltet. Administratoren können AD DS zum Organisieren von Elementen eines Netzwerks, z. B. Benutzern, Computern und anderen Geräten in einer hierarchischen Kapselung-Struktur. Die Kapselung hierarchischen Struktur enthält die Active Directory-Gesamtstruktur Domänen in der Gesamtstruktur und Organisationseinheiten (OEs) in jeder Domäne. Ein Server, der AD DS ausgeführt wird, wird einen Domänencontroller aufgerufen.

AD DS enthält die Benutzerkonten, Computerkonten und Eigenschaften von Benutzerkonten, die von PEAP Protected Extensible Authentication Protocol () erforderlich sind, um Benutzeranmeldeinformationen Authentifizierung und Autorisierung für VPN-verbindungsanforderungen auszuwerten. Informationen zum Bereitstellen von AD DS finden Sie in der Windows Server 2016- [Handbuch zum Kernnetzwerk](../../../../networking/core-network-guide/Core-Network-Guide.md).



Bei Abschluss der Schritte in dieser Bereitstellung konfigurieren Sie die folgenden Elemente auf dem Domänencontroller.

-   Aktivieren Sie die automatische Registrierung von Zertifikaten in "Gruppenrichtlinie" für Computer und Benutzer

-   Erstellen der VPN-Benutzergruppe

-   Erstellen Sie die Gruppe der VPN-Server

-   Erstellen Sie die Gruppe der NPS-Servern

### Active Directory-Benutzer und-Computer

Active Directory-Benutzer und-Computer ist eine Komponente von AD DS, die Konten enthält, die physische Einheiten, z. B. eines Computers, eine Person oder eine Sicherheitsgruppe darstellen. Eine Sicherheitsgruppe ist eine Sammlung von Benutzer- oder Computerkonten, die Administratoren als eine Einheit verwalten können. Benutzer- und Computerkonten, die zu einer bestimmten Gruppe gehören werden als Mitglieder der Gruppe bezeichnet.

Benutzerkonten in Active Directory-Benutzer und-Computer besitzen DFÜ-Eigenschaften, die während des Autorisierungsprozesses - NPS ausgewertet wird, es sei denn, die **Zugriffsberechtigung für die Netzwerk** -Eigenschaft des Benutzerkontos auf **Steuern des Zugriffs über NPS-Netzwerkrichtlinien festgelegt ist **. Dies ist die Standardeinstellung für alle Benutzerkonten. In einigen Fällen jedoch, diese Einstellung eine andere Konfiguration möglicherweise, die den Benutzer eine Verbindung herstellen über VPN blockiert. Um gegen diese Möglichkeit zu schützen, können Sie den Netzwerkrichtlinienserver um DFÜ-Eigenschaften des Kontos zu ignorieren konfigurieren.

Weitere Informationen finden Sie unter [Konfigurieren von NPS auf Benutzerkonto ignorieren DFÜ - Eigenschaften](../../../../networking/technologies/nps/nps-np-configure.md#configure-nps-to-ignore-user-account-dial-in-properties).



### Gruppenrichtlinienverwaltung

Die Gruppenrichtlinien-Verwaltungskonsole ermöglicht Directory-basierte und Verwaltung von Benutzer- und Einstellungen, einschließlich der Sicherheit und Informationen. Verwenden Sie Gruppenrichtlinien, um Konfigurationen für Gruppen von Benutzern und Computern zu definieren.

Mit "Gruppenrichtlinie" können Sie die Einstellungen für Registrierungseinträge, Sicherheit, Softwareinstallation, Skripts, ordnerumleitungen, remote-Installationsdienste und Internet Explorer-Wartung angeben. Die Gruppenrichtlinien-Einstellungen, die Sie erstellen, sind in ein Gruppenrichtlinienobjekt (GPO) enthalten. Durch das Zuordnen eines Gruppenrichtlinienobjekts mit ausgewählten Active Directory-systemcontainern – Sites, Domänen und Organisationseinheiten – können Sie die GPO-Einstellungen auf die Benutzer und Computer in diesen Active Directory-Containern anwenden. Um Gruppenrichtlinienobjekte in einem Unternehmen zu verwalten, können Sie die Group Policy Management Editor Microsoft Management Console (MMC) verwenden.


## Windows 10-VPN-Clients

Zusätzlich zu den Server-Komponenten stellen Sie sicher, dass die Client-Computer, die Sie konfigurieren, um VPN verwenden Windows 10 Anniversary Update (version1607) ausgeführt werden. Die Windows 10-VPN-Clients müssen Domäne zu Ihrer Active Directory-Domäne angehören.


Der Windows 10-VPN-Client ist stark konfigurierbar und bietet viele Optionen. Um die spezifischen Features besser zu veranschaulichen, die dieses Szenario verwendet, identifiziert Tabelle 1 VPN-Feature verwendeten Kategorien und bestimmte Konfigurationen, die diese Bereitstellung verweist. Sie können die einzelnen Einstellungen für diese Features mithilfe der VPNv2-Konfigurationsdienstanbieter (CSP) wird später in dieser Bereitstellung konfigurieren. 

Tabelle1. VPN-Features und Konfigurationen, die in dieser Bereitstellung erläutert

| **VPN-Funktion** | **Szenario Bereitstellungskonfiguration**         |
|-----------------|-----------------------------------------------|
| Verbindungstyp | Systemeigene IKEv2                                  |
| Routing         | Split-tunneling                               |
| Auflösung von Namen | Domänennamen-Informationsliste und DNS-suffix   |
| Auslösen      | Always On und Trusted Network Detection       |
| Authentifizierung  | PEAP-TLS mit TPM geschützt Benutzerzertifikate |
---

>[!NOTE] 
>PEAP-TLS und TPM sind "Protected Extensible Authentication-Protokoll mit die Transport Layer Security" und "Trusted Platform Module".

### VPNv2-CSP-Knoten

In dieser Bereitstellung verwenden Sie den ProfileXML-VPNv2-CSP-Knoten, um das VPN-Profil erstellen, das auf Windows 10-Clientcomputern bereitgestellt wird. Konfigurationsdienstanbieter (CSPs) sind Schnittstellen, die verschiedene Management-Funktionen in der Windows-Client verfügbar zu machen. vom Konzept her CSPs Arbeit ähnelt der Funktionsweise von Gruppenrichtlinien. Jeder CSP hat Konfiguration-Knoten, die einzelne Einstellungen darstellen. Wie Gruppenrichtlinien, können Sie auch den CSP-Einstellungen für Registrierungsschlüssel, Dateien, Berechtigungen usw. verknüpfen. Ähnlich wie Sie den Gruppenrichtlinienverwaltungs-Editor verwenden, um Gruppenrichtlinienobjekte (GPOs) zu konfigurieren, konfigurieren Sie CSP-Knoten mit einer Lösung für mobile Device Management (MDM) wie Microsoft Intune. MDM-Produkte wie Intune bieten eine benutzerfreundliche Konfigurationsoption, die das CSP im Betriebssystem konfiguriert.

![Mobile Device Management CSP-Konfiguration](../../../media/Always-On-Vpn/Vpn-Mdm.jpg)

Sie können nicht jedoch einige CSP-Knoten direkt über eine Benutzeroberfläche (UI) wie der Intune-Admin-Konsole konfigurieren. In diesen Fällen müssen Sie die Open Mobile Alliance Uniform Resource Identifier (OMA-URI)-Einstellungen konfigurieren manuell. Sie konfigurieren OMA-URIs, mit dem OMA Device Management-Protokoll (OMA-DM), eine universelle Geräte-Management-Spezifikation, die meisten moderne Apple, Android und Windows-Geräten zu unterstützen. Solange die OMA-DM-Spezifikation beachtet werden, sollten alle MDM-Produkte mit folgenden Betriebssysteme auf die gleiche Weise interagieren.

Windows 10 bietet viele CSPs, aber diese Bereitstellung konzentriert auf dem VPNv2-CSP den VPN-Client zu konfigurieren. Dem VPNv2-CSP ermöglicht die Konfiguration der einzelnen VPN-Profil-Einstellungen in Windows 10 über eine eindeutige CSP-Knoten. Auch in dem VPNv2-CSP enthalten ist Knoten *ProfileXML*, das Ihnen ermöglicht, konfigurieren Sie alle Einstellungen in einem Knoten statt einzeln. Weitere Informationen zu ProfileXML finden Sie im Abschnitt "ProfileXML Übersicht" weiter unten in dieser Bereitstellung. Informationen zu jedem VPNv2-CSP-Knoten finden Sie unter dem [VPNv2-CSP](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-csp).



## Nächste Schritte

- [Erfahren Sie mehr über die erweiterten Funktionen von Always On VPN](deploy/always-on-vpn-adv-options.md)

- [Planen der Always On VPN-Bereitstellung](deploy/always-on-vpn-deploy-deployment.md)


---

## Verwandte Themen
- [Microsoft-Software für Microsoft Azure-VMs zu unterstützen](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines): Dieser Artikel beschreibt die Support-Richtlinie für die Ausführung von Microsoft-Server-Software in der Microsoft Azure-VM-Umgebung (Infrastructure-as-a-Service).

- [Remote Access](../../Remote-Access.md): Dieses Thema enthält eine Übersicht über die RAS-Server-Rolle in Windows Server 2016.

- [Windows 10 technische VPN-Anleitung](https://docs.microsoft.com/windows/access-protection/vpn/vpn-guide): Diese Anleitung führt Sie durch die Entscheidungen, die Sie machen für Windows 10-Clients in der Enterprise-VPN-Lösung und wie Sie Ihre Bereitstellung konfigurieren. Dieses Handbuch verweist auf den VPNv2-Konfigurationsdienstanbieter (CSP) und enthält Konfigurationsanweisungen für die Verwaltung mobiler Geräte (MDM) unter Verwendung von Microsoft Intune und der VPN-Profilvorlage für Windows 10.

- [Handbuch zum Kernnetzwerk](../../../../networking/core-network-guide/Core-Network-Guide.md): Dieses Handbuch enthält Anweisungen zum Planen und Bereitstellen der Kernkomponenten für eine voll funktionsfähige Netzwerk- und einer neuen Active Directory-Domäne in einer neuen Gesamtstruktur erforderlich.

- [Domain Name System (DNS)](../../../../networking/dns/dns-top.md): Dieses Thema enthält eine Übersicht der Systeme DNS (Domain Name). In Windows Server 2016 ist DNS eine Serverrolle, die Sie mithilfe von Server-Manager oder Windows PowerShell-Befehle installieren können. Wenn Sie eine neue Active Directory-Gesamtstruktur und Domäne installieren, wird automatisch DNS in Active Directory als globalen Katalog Server für die Gesamtstruktur und die Domäne installiert. 

- [Übersicht über Active Directory Zertifikat](https://technet.microsoft.com/library/hh831740.aspx): Dieses Dokument enthält eine Übersicht über Active Directory-Zertifikatdienste (AD CS) in Windows Server® 2012. AD CS ist die Server-Rolle mit dem Sie eine public Key-Infrastruktur (PKI) erstellen und Bereitstellen von Kryptografie mit öffentlichem Schlüssel, digitale Zertifikate und digitale Signatur, die Funktionen für Ihre Organisation.

- [Public Key-Infrastruktur-Designrichtlinien](https://social.technet.microsoft.com/wiki/contents/articles/2901.public-key-infrastructure-design-guidance.aspx): dieses Wiki enthält Richtlinien zum Entwerfen von Public Key-Infrastrukturen (PKI). Bevor Sie eine PKI und-Zertifizierung Zertifizierungsstelle (ZS) Hierarchie konfigurieren, sollten Sie im Hinblick auf Ihrer Organisation Security Policy und das Zertifikat Praxis Anweisung (CPS) sein.

- [AD CS-Schritt-für-Schritt-Anleitung: Bereitstellung von zwei Ebene PKI-Hierarchie](https://social.technet.microsoft.com/wiki/contents/articles/15037.ad-cs-step-by-step-guide-two-tier-pki-hierarchy-deployment.aspx): Dieser Artikel beschreibt die erforderlichen Schritte zum Einrichten einer grundlegenden Konfigurations der Active Directory®-Zertifikatsdienste (AD CS) in einer Lab-Umgebung. AD CS in Windows Server® 2008 R2 bereit anpassbare Dienste zum Erstellen und Verwalten von Zertifikaten in öffentlichen Schlüsseln zur beliebig.

- [Netzwerkrichtlinienserver (Network Policy Server, NPS)](../../../../networking/technologies/nps/nps-top.md): Dieses Thema enthält eine Übersicht über Network Policy Server in Windows Server 2016. Mit einem Netzwerkrichtlinienserver (Network Policy Server, NPS) können Sie organisationsweite Netzwerkzugriffsrichtlinien für die Authentifizierung und Autorisierung von Verbindungsanforderungen erstellen und erzwingen. 

---
