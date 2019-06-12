---
title: Always On-VPN-Technologie-Übersicht
description: 'Diese Seite umschreib eine kurze Übersicht über die Always On-VPN-Technologien mit Links zu ausführlichen Dokumente. '
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: 65a575b24ea3c70ad7eedd95fe287d955ccaeea6
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749674"
---
# <a name="always-on-vpn-technology-overview"></a>Übersicht über die Always On-VPN-Technologie

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorherige:** Erfahren Sie mehr über die Always On-VPN-Verbesserungen](always-on-vpn-enhancements.md)
- [**nächster:** Erfahren Sie mehr über die erweiterten Funktionen von Always On-VPN-](deploy/always-on-vpn-adv-options.md)

Für diese Bereitstellung müssen Sie installieren neuen RAS-Server, auf der Windows Server 2016 ausgeführt wird, sowie einige Ihrer vorhandenen Infrastruktur für die Bereitstellung zu ändern.

Die folgende Abbildung zeigt die Infrastruktur, die zur Always On-VPN-Bereitstellung erforderlich ist.

![Always On-VPN-Infrastruktur](../../../media/Always-On-Vpn/Ao-Vpn-Overview.jpg)

Der Verbindungsprozess, die in dieser Abbildung dargestellt umfasst die folgenden Schritte aus:

1. Mit öffentlichen DNS-Server führt der Windows 10-VPN-Client eine Namensabfrage für die Auflösung der IP-Adresse des VPN-Gateways an.

2. Verwenden die IP-Adresse, die vom DNS zurückgegeben wurden, sendet der VPN-Client eine verbindungsanforderung an das VPN-Gateway an.

3. Das VPN-Gateway ist ebenfalls als Remote Authentication Dial-in User Service (RADIUS)-Client konfiguriert. der VPN-RADIUS-Client sendet die verbindungsanforderung an die Organisation/Unternehmenskonten NPS-Server für die anforderungsverarbeitung für die Verbindung an.

4. Der NPS-Server verarbeitet die verbindungsanforderung, die evtl. eine Autorisierung und Authentifizierung, und bestimmt, ob Sie zulassen oder Verweigern der verbindungsanforderung.

5. Der NPS-Server leitet eine Access-Accept oder den Zugriff verweigern-Antwort an das VPN-Gateway weiter.

6. Die Verbindung initiiert oder beendet wird anhand der Antwort, die der VPN-Server von der NPS-Server zu empfangen.

Weitere Informationen zu den einzelnen Infrastrukturkomponenten, die in der Abbildung oben dargestellt finden Sie unter den folgenden Abschnitten.

>[!NOTE]
>Wenn Sie bereits einige dieser Technologien in Ihrem Netzwerk bereitgestellt haben, können die Anweisungen in diesem Leitfaden zur Bereitstellung Sie zusätzliche Konfigurationsschritte der Technologien für diesen bereitstellungszweck ausführen.

## <a name="domain-name-system-dns"></a>Domain Name System (DNS)

Interne und externe Domain Name System (DNS)-Zonen sind erforderlich, die davon aus, dass die interne Zone eine delegierte untergeordnete Domäne von der externen Zone (z. B. "corp.contoso.com" und "contoso.com").

Erfahren Sie mehr über [Domain Name System (DNS)](../../../../networking/dns/dns-top.md) oder [Core Network Guide](../../../../networking/core-network-guide/core-network-guide.md).

>[!NOTE]
>Andere DNS-entwirft, z. B. Split-Brain-DNS (mit dem gleichen Domänennamen intern und extern in separaten DNS-Zonen) oder unabhängig vom stagingstatus internen und externe Domänen (z. B. "contoso.Local" und "contoso.com") sind ebenfalls möglich. Weitere Informationen zum Bereitstellen von Split-Brain-DNS finden Sie unter [verwenden DNS-Richtlinien für die DNS-Bereitstellung Split-Brain](../../../../networking/dns/deploy/split-brain-DNS-deployment.md).

## <a name="firewalls"></a>Firewalls

Stellen Sie sicher, dass Ihre Firewalls den Datenverkehr zu ermöglichen, der für sowohl VPN- und RADIUS-Kommunikation zum ordnungsgemäßen erforderlich ist.

Weitere Informationen finden Sie unter [Konfigurieren von Firewalls für RADIUS-Verkehr](../../../../networking/technologies/nps/nps-firewalls-configure.md).

## <a name="remote-access-as-a-ras-gateway-vpn-server"></a>Remotezugriff als RAS-Gateway-VPN-Server

In Windows Server 2016 ausführen auch als Router und RAS-Server die Remotezugriffs-Serverrolle soll; aus diesem Grund unterstützt ein breites Spektrum an Funktionen. Für diese Anleitung für die Bereitstellung, die Sie benötigen nur einer kleinen Teilmenge dieser Funktionen: Unterstützung für IKEv2-VPN-Verbindungen und LAN-routing.

IKEv2 befindet es sich um ein VPN-Tunneling-Protokoll in die Internet Engineering Task Force-Anforderung für Kommentare 7296 beschrieben. Der wichtigste Vorteil von IKEv2 ist, dass es sich um Unterbrechungen in die zugrunde liegende Netzwerkverbindung toleriert. Z. B. wenn die Verbindung vorübergehend unterbrochen wird, oder wenn ein Benutzer einen Clientcomputer aus einem Netzwerk zu einem anderen bewegt, IKEv2 automatisch wiederherstellt, die VPN-Verbindung, wenn die Verbindung wiederhergestellt ist – alles ohne Eingreifen des Benutzers.

Mithilfe von RAS-Gateway können Sie VPN-Verbindungen, die Endbenutzern zu ermöglichen, mit dem Remotezugriff, Netzwerk und Ressourcen Ihrer Organisation bereitstellen. Eine dauerhafte Verbindung zwischen Clients und das Netzwerk Ihrer Organisation Bereitstellen von Always On-VPN-verwaltet werden, wenn der Remotecomputer mit dem Internet verbunden sind. Mit RAS-Gateway können Sie eine Standort-zu-Standort-VPN-Verbindung zwischen zwei Servern an verschiedenen Standorten, z. B. zwischen Ihrem primären Büro und einer Zweigstelle, auch (Network Address Translation, NAT) verwenden, sodass Benutzer innerhalb des Netzwerks auf externe zugreifen können Ressourcen, z. B. das Internet. RAS-Gateway unterstützt auch Border Gateway Protocol (BGP), mit der dynamischen routing-Dienste bereitstellt, wenn Ihre Remotestandorten auch Edge-Gateways verfügen, die Unterstützung von BGP.

Sie können Remote Access Service (RAS)-Gateways mithilfe von Windows PowerShell-Befehle und die Remote Access Microsoft Management Console (MMC) verwalten.

## <a name="network-policy-server-nps"></a>Netzwerkrichtlinienserver (Network Policy Server, NPS)

NPS ermöglicht Ihnen das Erstellen und Erzwingen von unternehmensweiten Netzwerkadressen-Zugriffsrichtlinien für die Anforderung von Verbindungsauthentifizierung und Autorisierung. Wenn Sie NPS als Server Remote Authentication Dial-in User Service (RADIUS) verwenden, konfigurieren Sie Netzwerkzugriffsserver, z. B. VPN-Servern als RADIUS-Clients in NPS.

Sie können auch Netzwerkrichtlinien konfigurieren, mit denen NPS Verbindungsanforderungen autorisiert, und Sie können die RADIUS-Kontoführung so konfigurieren, dass NPS Kontoführungsinformationen in Protokolldateien auf der lokalen Festplatte oder in einer Microsoft SQL Server-Datenbank protokolliert.

Weitere Informationen finden Sie unter [(Network Policy Server, NPS)](../../../../networking/technologies/nps/nps-top.md).

## <a name="active-directory-certificate-services"></a>Active Directory-Zertifikatdienste

Der Server der Zertifizierungsstelle (Certification Authority, CA) ist eine Zertifizierungsstelle, die Active Directory Certificate Services ausgeführt wird. Die VPN-Konfiguration erfordert eine Active Directory-basierten public Key-Infrastruktur (PKI).

Organisationen können AD CS verwenden, um Sicherheit zu verbessern, indem Sie die Identität einer Person, Geräts oder des Diensts an einen entsprechenden öffentlichen Schlüssel binden. AD CS umfasst auch Funktionen, die Ihnen ermöglichen, die Registrierung von Zertifikaten und Zertifikatsperrlisten in einer Vielzahl von skalierbaren Umgebungen verwalten. Weitere Informationen finden Sie unter [Active Directory Certificate Services Overview](https://technet.microsoft.com/library/hh831740.aspx) und [Public Key-Infrastruktur-Entwurfsrichtlinien](https://social.technet.microsoft.com/wiki/contents/articles/2901.public-key-infrastructure-design-guidance.aspx).

Während der Durchführung der Bereitstellung konfigurieren Sie die folgenden Zertifikatvorlagen auf der Zertifizierungsstelle.

- Die Zertifikatvorlage für die Benutzerauthentifizierung

- Die Zertifikatvorlage für die VPN-Server-Authentifizierung

- Die Zertifikatvorlage für die NPS-Server-Authentifizierung

### <a name="certificate-templates"></a>Zertifikatvorlagen

Zertifikatvorlagen können die Aufgabe der Verwaltung von einer Zertifizierungsstelle (CA) können Sie zum Ausstellen von Zertifikaten, die vorkonfiguriert sind, für die ausgewählten Vorgänge erheblich vereinfachen. Das Zertifikatvorlagen-MMC-Snap-in können die folgenden Aufgaben ausführen.

- Zeigen Sie Eigenschaften für jede Zertifikatvorlage.

- Kopieren und Ändern von Zertifikatvorlagen.

- Steuern, welche Benutzer und Computer können Vorlagen lesen und Registrieren von Zertifikaten.

- Aufgaben Sie andere administrative im Zusammenhang mit Zertifikatvorlagen.

Zertifikatvorlagen sind ein wesentlicher Bestandteil einer Unternehmenszertifizierungsstelle (CA). Sie sind ein wichtiges Element der Zertifikatsrichtlinie für eine Umgebung, die den Satz von Regeln und Formate für die Registrierung von Zertifikaten, Verwendung und Verwaltung ist.

Weitere Informationen finden Sie unter [Zertifikatvorlagen](https://technet.microsoft.com/library/cc730705.aspx).

### <a name="digital-server-certificates"></a>Digitale Serverzertifikate

Dieser Leitfaden zur Bereitstellung enthält Anweisungen für die Verwendung von Active Directory-Zertifikatdienste (AD CS) sowohl registrieren und automatisch registrieren von Zertifikaten für RAS und NPS-Infrastruktur-Servern. AD CS ermöglichen Ihnen eine public Key-Infrastruktur (PKI) zu erstellen und Bereitstellen von Kryptografie mit öffentlichem Schlüssel, digitale Zertifikate und digitale Signatur-Funktionen für Ihre Organisation.

Wenn Sie digital Serverzertifikate für die Authentifizierung zwischen Computern in Ihrem Netzwerk verwenden, geben Sie die Zertifikate:

1. Datenvertraulichkeit durch Verschlüsselung.

2. Integrität durch digitale Signaturen.

3. Authentifizierung durch Zuordnung von Zertifikatschlüsseln mit einem Computer, Benutzer oder Gerät Konten in einem Computernetzwerk.

Weitere Informationen finden Sie unter [AD CS-Schritt-für-Schritt-Handbuch: Bereitstellung der PKI-Hierarchie mit zwei Ebenen](https://social.technet.microsoft.com/wiki/contents/articles/15037.ad-cs-step-by-step-guide-two-tier-pki-hierarchy-deployment.aspx).

## <a name="active-directory-domain-services-ad-ds"></a>Active Directory-Domänendienste (AD DS)

Mit AD DS wird eine verteilte Datenbank bereitgestellt, in der Informationen zu Netzwerkressourcen und anwendungsspezifische Daten aus AD-fähigen Anwendungen gespeichert und verwaltet werden. Administratoren können AD DS verwenden, um die Elemente eines Netzwerks (z. B. Benutzer, Computer und andere Geräte) in einer hierarchischen Struktur aus Einschlussbeziehungen zu organisieren. Diese hierarchische Struktur umfasst die Active Directory-Gesamtstruktur, Domänen in der Gesamtstruktur sowie die Organisationseinheiten in den einzelnen Domänen. Ein Server, auf dem AD DS ausgeführt wird, wird als Domänencontroller bezeichnet.

AD DS enthält die Benutzerkonten, Computerkonten und Eigenschaften, die von PEAP Protected Extensible Authentication Protocol () zum Authentifizieren der Anmeldeinformationen des Benutzers und zum Auswerten der Autorisierung für Anforderungen von VPN-Verbindungen erforderlich sind. Weitere Informationen zum Bereitstellen von AD DS finden Sie unter Windows Server 2016 [Core Network Guide](../../../../networking/core-network-guide/Core-Network-Guide.md).

Während der Ausführung der Schritte in dieser Bereitstellung konfigurieren Sie die folgenden Elemente auf dem Domänencontroller.

- Aktivieren der automatischen Registrierung von Zertifikaten in der Gruppenrichtlinie für Computer und Benutzer

- Erstellen der VPN-Benutzergruppe

- Erstellen Sie die VPN-Server-Gruppe

- Der NPS-Servers-Gruppe erstellen

### <a name="active-directory-users-and-computers"></a>Active Directory-Benutzer und-Computer

Active Directory-Benutzer und-Computer ist eine Komponente von AD DS mit Konten, die physische Entitäten, z. B. ein Computer, eine Person oder einer Sicherheitsgruppe darzustellen. Eine Sicherheitsgruppe ist eine Sammlung von Benutzer- oder Computerkonten, die Administratoren als einzelne Einheit verwaltet werden können. Benutzer- und Computerkonten, die einer bestimmten Gruppe angehören, werden als Gruppenmitglieder bezeichnet.

Benutzerkonten in Active Directory-Benutzer und-Computer haben DFÜ-Eigenschaften, die NPS während des Autorisierungsprozesses - ausgewertet wird, es sei denn, die **Netzwerk Zugriffsberechtigung** des Benutzerkontos-Eigenschaftensatz auf **Steuerelement Zugriff über die Netzwerkrichtlinie für NPS**. Dies ist die Standardeinstellung für alle Benutzerkonten. In einigen Fällen kann jedoch mit dieser Einstellung eine andere Konfiguration aufweisen, die den Benutzer eine Verbindung herstellen über ein VPN blockiert. Zum Schutz vor dieser Möglichkeit können Sie die NPS-Server zum Ignorieren von Einwähleigenschaften des Kontos konfigurieren.

Weitere Informationen finden Sie unter [NPS konfigurieren, um Einwähleigenschaften des Benutzerkontos ignorieren](../../../../networking/technologies/nps/nps-np-configure.md#configure-nps-to-ignore-user-account-dial-in-properties).

### <a name="group-policy-management"></a>Gruppenrichtlinienverwaltung

Die Gruppenrichtlinien-Verwaltungskonsole können verzeichnisbasierte Änderungs- und konfigurationsverwaltung von Benutzer- und computereinstellungen, einschließlich Informationen zu Sicherheit und Benutzer. Sie verwenden Gruppenrichtlinien, um Konfigurationen für Gruppen von Benutzern und Computern zu definieren.

Mit der Gruppenrichtlinie können Sie Einstellungen für die Registrierungseinträge, Sicherheit, Softwareinstallation, Skripts, ordnerumleitung, Remoteinstallationsdienste und Internet Explorer-Wartung angeben. Die gruppenrichtlinieneinstellungen, die Sie erstellen, sind in ein Gruppenrichtlinienobjekt (GPO) enthalten. Durch Verknüpfen eines Gruppenrichtlinienobjekts mit ausgewählten Active Directory-System-Container, Sites, Domänen und Organisationseinheiten: Sie können die Einstellungen des Gruppenrichtlinienobjekts anwenden, um die Benutzer und Computer in dieser Active Directory-Container. Zum Verwalten der Gruppenrichtlinienobjekte in einem Unternehmen können Sie die Group Policy Management Editor Microsoft Management Console (MMC) verwenden.

## <a name="windows-10-vpn-clients"></a>Windows 10-VPN-Clients

Zusätzlich zu den Serverkomponenten stellen Sie sicher, dass die Clientcomputer, die Sie konfigurieren, um das VPN verwenden Windows 10 Anniversary Update (Version 1607) ausgeführt werden. Die Windows 10-VPN-Clients müssen in Active Directory-Domäne eingebunden sein.


Der Windows 10-VPN-Client ist hochgradig konfigurierbar und bietet viele Optionen. Um die bestimmten Funktionen veranschaulichen, die dieses Szenario verwendet, identifiziert die Tabelle 1 VPN-Funktionskategorien und spezifischen Konfigurationen, die diese Bereitstellung verweist. Sie konfigurieren die einzelnen Einstellungen für diese Funktionen mithilfe der VPNv2-Konfigurationsdienstanbieter (CSP) weiter unten in dieser Bereitstellung. 

Tabelle 1: VPN-Features und Konfigurationen, die in dieser Bereitstellung erläutert

| VPN-Funktion     |     Szenario-Bereitstellungskonfiguration         |
|-----------------|-----------------------------------------------|
| Verbindungstyp |                 Native IKEv2                  |
|     Routing     |                Split-tunneling                |
| Namensauflösung |  Liste der Domänennameninformationen und DNS-suffix  |
|   Auslösen    |    Erkennung von Always On und vertrauenswürdiges Netzwerk    |
| Authentifizierung  | PEAP-TLS mit TPM-geschützten Benutzerzertifikate |

>[!NOTE]
>PEAP-TLS und TPM sind "Protected Extensible Authentication Protocol mit die Transport Layer Security" und "Trusted Platform Module".

### <a name="vpnv2-csp-nodes"></a>VPNv2 CSP-Knoten

In dieser Bereitstellung verwenden Sie den Knoten "profileXML" VPNv2 CSP, um das VPN-Profil zu erstellen, das für Windows 10-Clientcomputer bereitgestellt wird. Configuration Service Providers (CSPs) sind die Schnittstellen, die verschiedene Funktionen innerhalb des Windows-Clients verfügbar zu machen. CSPs funktioniert vom Konzept her ähnlich wie Gruppenrichtlinien funktionieren. Jeder CSP verfügt über Knoten mit der Konfiguration, die einzelne Einstellungen darstellen. Z. B. Einstellungen für Gruppenrichtlinien, können Sie auch CSP-Einstellungen, Registrierungsschlüssel, Dateien, Berechtigungen und So weiter verknüpfen. Ähnlich wie Sie den Gruppenrichtlinienverwaltungs-Editor verwenden, um Gruppenrichtlinienobjekte (GPOs) zu konfigurieren, konfigurieren Sie CSP-Knoten mithilfe einer verwaltungslösung mobiler Geräte (MDM) wie z.B. Microsoft Intune. MDM-Produkte wie z.B. Intune bieten eine benutzerfreundliche Konfigurationsoption, mit dem CSP im Betriebssystem konfiguriert.

![Verwaltung von Geräten zu CSP-Konfiguration](../../../media/Always-On-Vpn/Vpn-Mdm.jpg)

Sie können keine jedoch einige Knoten CSP direkt über eine Benutzeroberfläche (UI) wie der Intune-Verwaltungskonsole konfigurieren. In diesen Fällen müssen Sie die Open Mobile Alliance Uniform Resource Identifier (OMA-URI)-Einstellungen konfigurieren manuell. Sie konfigurieren die OMA-URIs, über das OMA-Device-Management-Protokoll (OMA-DM), einer universellen-Management-Spezifikation, die meisten modernen Apple, Android und Windows-Geräte unterstützen. Solange sie die OMA-DM-Spezifikation entsprechen, sollten alle MDM-Produkte mit diesen Betriebssystemen auf die gleiche Weise interagieren.

Windows 10 bietet viele CSPs, aber diese Bereitstellung konzentriert sich auf die VPNv2 CSP Konfigurieren des VPN-Clients. VPNv2 CSP ermöglicht die Konfiguration der einzelnen VPN-Profil-Einstellungen in Windows 10 über eine eindeutige CSP-Knoten. Ebenfalls im VPNv2 CSP enthalten einen Knoten namens ist *"profileXML"* , können Sie alle Einstellungen konfigurieren in einem Knoten statt einzeln. Weitere Informationen zu "profileXML" finden Sie im Abschnitt "" profileXML "Übersicht" weiter unten in dieser Bereitstellung. Weitere Informationen zu jedem Knoten VPNv2 CSP finden Sie unter den [VPNv2 CSP](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-csp).

## <a name="next-steps"></a>Nächste Schritte

- [Erfahren Sie mehr über die erweiterte Always On-VPN-Funktionen](deploy/always-on-vpn-adv-options.md)

- [Planen der Always On-VPN-Bereitstellung](deploy/always-on-vpn-deploy-deployment.md)

## <a name="related-topics"></a>Verwandte Themen

- [Die Unterstützung der Microsoft-Serversoftware für Microsoft Azure-Computern](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines): Dieser Artikel beschreibt die Unterstützungsrichtlinie für Microsoft-Serversoftware in der Microsoft Azure-VM-Umgebung (Infrastructure-as-a-Service) ausgeführt.

- [Remotezugriff](../../Remote-Access.md): Dieses Thema enthält eine Übersicht über die Remotezugriffs-Serverrolle in Windows Server 2016.

- [Technische Anleitung für Windows 10-VPN-](https://docs.microsoft.com/windows/access-protection/vpn/vpn-guide): Dieses Handbuch führt Sie durch die Entscheidungen, dass Sie für Windows 10-Clients in Ihrem Unternehmen VPN-Lösung und zur Konfiguration der Bereitstellung machen werden. Dieses Handbuch verweist auf die VPNv2 Configuration Service Provider (CSP) und bietet mobile geräteverwaltung (MDM) mit Microsoft Intune und der VPN-Profil-Vorlage für Windows 10 Anweisungen.

- [Core Network Guide](../../../../networking/core-network-guide/Core-Network-Guide.md): Dieses Handbuch enthält Anweisungen zum Planen und Bereitstellen der Hauptkomponenten, die für ein voll funktionsfähiges Netzwerk und eine neue Active Directory-Domäne in einer neuen Gesamtstruktur erforderlich sind.

- [Domain Name System (DNS)](../../../../networking/dns/dns-top.md): Dieses Thema enthält eine Übersicht über die des Domain Name Systems (DNS). In Windows Server 2016 ist DNS für eine Serverrolle, die Sie installieren können, mithilfe von Server-Manager oder Windows PowerShell-Befehlen. Wenn Sie eine neue Active Directory-Gesamtstruktur und Domäne installieren, wird DNS automatisch in Active Directory als globalen Katalog Server für die Gesamtstruktur und Domäne installiert.

- [Active Directory-Zertifikatdienste – Übersicht über die](https://technet.microsoft.com/library/hh831740.aspx): Dieses Dokument enthält eine Übersicht über Active Directory-Zertifikatdienste (AD CS) in Windows Server® 2012. AD CS ist die Serverrolle, die es Ihnen ermöglicht, eine Public Key Infrastructure (PKI) zu erstellen und Verschlüsselung für öffentliche Schlüssel, digitale Zertifikate und Funktionen für digitale Signaturen in Ihrer Organisation bereitzustellen.

- [Leitfaden zum Design der Public Key-Infrastruktur](https://social.technet.microsoft.com/wiki/contents/articles/2901.public-key-infrastructure-design-guidance.aspx):  Dieses Wiki enthält Anleitungen zum Entwerfen von Public Key-Infrastrukturen (PKIs). Bevor Sie eine PKI und Zertifizierung Zertifizierungsstelle (CA)-Hierarchie konfigurieren, sollten Sie von Ihrer Organisation Security-Richtlinie und zertifikatverwaltung Practice Statement, (CPS) kennen.

- [AD CS-Schritt-für-Schritt-Anleitung: Bereitstellung der PKI-Hierarchie mit zwei Ebenen](https://social.technet.microsoft.com/wiki/contents/articles/15037.ad-cs-step-by-step-guide-two-tier-pki-hierarchy-deployment.aspx): Diese schrittweise Anleitung beschreibt die Schritte zum Einrichten einer grundlegenden Konfigurations von Active Directory®-Zertifikatdienste (AD CS) in einer Lab-Umgebung erforderlich sind. AD CS in Windows Server® 2008 R2 bietet anpassbare Dienste zum Erstellen und Verwalten von public Key-Zertifikate, die in Softwaresicherheitssystemen mit Technologien für öffentliche Schlüssel verwendet.

- [Netzwerkrichtlinienserver (NPS)](../../../../networking/technologies/nps/nps-top.md): Dieses Thema enthält eine Übersicht über Network Policy Server unter Windows Server 2016. Mit einem Netzwerkrichtlinienserver (Network Policy Server, NPS) können Sie organisationsweite Netzwerkzugriffsrichtlinien für die Authentifizierung und Autorisierung von Verbindungsanforderungen erstellen und erzwingen.
