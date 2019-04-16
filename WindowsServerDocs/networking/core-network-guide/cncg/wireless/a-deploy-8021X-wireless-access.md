---
title: Bereitstellen der Kennwort-basierte 802.1X-authentifizierten drahtlosen Zugriff
description: In diesem Thema ist Teil des Windows Server 2016 Networking Guide "Deploy Password-Based 802.1 X Authenticated Wireless Access"
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: ff06ba23-9c0f-49ec-8f7b-611cf8d73a1b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0ded8a273a9ad464b44fa7245db58d0fd05f06a2
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="deploy-password-based-8021x-authenticated-wireless-access"></a>Bereitstellen von Password\-basierte 802.1X-authentifizierten drahtlosen Zugriff

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dies ist ein Begleithandbuch zum Windows Server&reg; 2016 Core Network Guide. Das Handbuch zum Hauptnetzwerk bietet Anweisungen zum Planen und die erforderlichen Komponenten für eine einwandfreie Verwendung des Netzwerks und eine neue Active Directory® Domäne in einer neuen Gesamtstruktur bereitstellen.

Dieses Handbuch wird erläutert, wie für die Erstellung eines Hauptnetzwerks mithilfe von Anleitungen zum Bereitstellen von Institute of Electrical und Electronics Engineers \(IEEE\) 802.1X\-authentifizierten IEEE 802.11-Drahtloszugriff mit Protected Extensible Authentication Protocol – Microsoft Challenge Handshake Authentication Protocol Version 2 \ (PEAP\-MS\-CHAP v2\).

Da PEAP\-MS\-CHAP v2 erforderlich ist, dass Benutzer während der Authentifizierung ein Zertifikat, anstatt Password\ basierende Anmeldeinformationen angeben, ist es in der Regel einfacher und kostengünstiger als EAP\-TLS oder PEAP\-TLS bereitstellen.

>[!NOTE]
>In diesem Handbuch wird IEEE 802.1 X Authenticated Wireless Access mit PEAP\-MS\-CHAP v2 "wireless Access" und "WLAN-Zugriffs" abgekürzt.

## <a name="about-this-guide"></a>Informationen zum Handbuch
Dieses Handbuch, in Kombination mit den erforderlichen Handbüchern erläutert, enthält Anweisungen dazu, wie Sie die folgende WLAN-Infrastruktur bereitstellen.  

- Eine oder mehrere 802.1X\-fähigen 802.11 drahtlose Zugriff Punkte \(APs\).

- Active Directory-Domänendienste \(AD DS\)-Benutzer und -Computer.

- Die Gruppenrichtlinienverwaltung.

- Ein oder mehrere Netzwerkrichtlinienserver \(NPS\)-Server.

- Serverzertifikate für Computer, auf dem NPS ausgeführt wird.

- Drahtlose Clientcomputer, auf denen Windows ausgeführt wird&reg; 10, Windows 8.1 oder Windows 8.

### <a name="dependencies-for-this-guide"></a>Abhängigkeiten für diese Anleitung

Um authentifizierten WLAN mit diesem Handbuch erfolgreich bereitzustellen, müssen Sie eine Netzwerk und Domäne-Umgebung mit allen über die erforderlichen Technologien bereitgestellt verfügen. Außerdem benötigen Sie Serverzertifikate für Ihre authentifizierenden NPS-Server bereitgestellt.

Die folgenden Abschnitte enthalten Links zu Dokumentationen, die beschreibt, wie diese Technologien bereitgestellt.

#### <a name="network-and-domain-environment-dependencies"></a>Netzwerk- und Umgebung Abhängigkeiten

Dieses Handbuch richtet sich an Netzwerk- und Systemadministratoren, die die Anweisungen in der Windows Server 2016 befolgt haben **Kernnetzwerkhandbuch** ein Hauptnetzwerk bereitstellen oder für Benutzer, die zuvor die Core-Technologien enthalten im Kernnetzwerk durchführen, einschließlich der AD DS bereitgestellt haben Domain Name System \(DNS\), Dynamic Host Configuration-Protokoll \(DHCP\), TCP/IP, NPS und Windows Internet Name Service \(WINS\).  

Das Handbuch zum Hauptnetzwerk finden Sie unter den folgenden Speicherorten:

- Die Windows Server 2016 [Kernnetzwerkhandbuch](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide) ist in der technischen Bibliothek zu Windows Server 2016 verfügbar. 

- Die [Handbuch zum Hauptnetzwerk](https://gallery.technet.microsoft.com/Core-Network-Guide-for-9da2e683) steht auch in Word-Format im TechNet-Galerie unter [https://gallery.technet.microsoft.com/Core-Network-Guide-for-9da2e683](https://gallery.technet.microsoft.com/Core-Network-Guide-for-9da2e683).

#### <a name="server-certificate-dependencies"></a>Server-Zertifikat-Abhängigkeiten
Es gibt zwei verfügbare Optionen beim Registrieren von Authentication-Server mit Serverzertifikaten für die Verwendung mit 802.1X-Authentifizierung - eigene public Key-Infrastruktur mithilfe von Active Directory Certificate Services \(AD CS\) bereitstellen oder verwenden Sie Zertifikate, die von einer öffentlichen Zertifizierungsstelle registriert sind \(CA\).

##### <a name="ad-cs"></a>AD CS
Netzwerk- und Systemadministratoren, die Bereitstellung des authentifizierten WLAN müssen gehen Sie wie in der Windows Server 2016 Core Network Companion Guide **Bereitstellen von Serverzertifikaten für 802.1 X verkabelte oder kabellose 802.1X-Bereitstellungen**. Dieses Handbuch wird erläutert, wie bereitstellen und Verwenden von AD CS, damit Serverzertifikate für Computer, auf dem NPS ausgeführt wird.

Dieses Handbuch ist am folgenden Speicherort verfügbar.

- Windows Server 2016 Core Network Companion Guide [Bereitstellen von Serverzertifikaten für 802.1 X kabelgebundenen und drahtlosen Bereitstellungen](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments?f=255&MSPPError=-2147217396) im HTML-Format in der technischen Bibliothek. 

##### <a name="public-ca"></a>Öffentliche Zertifizierungsstelle
Sie können Zertifikate von einer öffentlichen Zertifizierungsstelle wie VeriSign, erwerben, dass Clientcomputer bereits vertrauen. 

Ein Clientcomputer vertraut eine Zertifizierungsstelle, wenn das Zertifikat im Zertifikatspeicher vertrauenswürdiger Stammzertifizierungsstellen installiert ist. Standardmäßig verfügen Windows-Computern mehrere öffentliche Zertifizierungsstellenzertifikate deren Speicher vertrauenswürdiger Stammzertifizierungsstellen-Zertifikat installiert.  

Es wird empfohlen, dass Sie die Entwurfs- und Bereitstellungshandbücher für jede der Technologien überprüfen, die in diesem Bereitstellungsszenario verwendet werden. Diese Handbücher hilft Ihnen festzustellen, ob dieses Bereitstellungsszenario bereitstellt, die Dienste und Konfigurationen, die Sie für das Netzwerk Ihrer Organisation benötigen.

### <a name="requirements"></a>Anforderungen
Im folgenden sind die Anforderungen für die Bereitstellung einer Infrastruktur für drahtlosen Zugriff mithilfe der in diesem Handbuch dokumentierten Szenario:

- Vor dem Bereitstellen dieses Szenario, müssen Sie zuerst 802.1X\ erwerben-fähigen Drahtloszugriffspunkten Funkverbindung an den entsprechenden Stellen an Ihrem Standort bereitstellen. Im Planungsabschnitt dieses Handbuchs hilft bei der Bestimmung der Features, die die Zugriffspunkte unterstützen müssen.

- Active Directory-Domänendienste \(AD DS\) ist installiert, wie die anderen erforderlichen Netzwerk-Technologien sind gemäß der Anleitung in Windows Server 2016 Core Network Guide.  

- AD CS wird bereitgestellt, und Serverzertifikate mit NPS-Servern registriert sind. Diese Zertifikate sind erforderlich, wenn Sie die PEAP\-MS\-CHAP v2 Certificate\-basierten Authentifizierungsmethoden bereitstellen, die in diesem Handbuch verwendet wird.

- Ein Mitglied Ihrer Organisation ist vertraut mit den IEEE 802.11-Standards, die unterstützt werden, indem Sie Ihre drahtlosen Zugriffspunkte und die Drahtlosnetzwerk-Adapter, die an den Clientcomputern und Geräten in Ihrem Netzwerk installiert sind. Eine Person in Ihrer Organisation ist z. B. mit Funkübertragung, 802.11 drahtlose Authentifizierung vertraut \ (WPA2 oder WPA\), und zwar \(AES or TKIP\).

## <a name="what-this-guide-does-not-provide"></a>Was dieses Handbuch bietet keine  
Im folgenden sind einige Elemente, die dieser Anleitung nicht bereitstellt:

### <a name="comprehensive-guidance-for-selecting-8021x-capable-wireless-access-points"></a>Umfassende Anleitungen zum Auswählen von 802.1X\-fähigen Drahtloszugriffspunkten

Da viele zwischen Marken und Modelle von 802.1X\ Unterschiede-Drahtloszugriffspunkt, dieses Handbuch bietet keine ausführlichen Informationen zu:  

- Bestimmen, welche Marken und Modelle von drahtlosen Zugriffspunkt am besten geeignet ist, die für Ihren Anforderungen geeignet sind.

- Die physische Bereitstellung von drahtlosen Zugriffspunkten in Ihrem Netzwerk.

- Erweiterte drahtlosen Zugriffspunkt-Konfiguration, z. B. für drahtlose virtuelle lokale Netzwerke \(VLANs\).

- Anweisungen zum drahtlosen Zugriffspunkt Vendor\-spezifische Attribute in NPS konfigurieren.

Darüber hinaus Terminologie und den Namen für die Einstellung zwischen drahtlosen Zugriffspunkt Marken und Modelle variieren und passt sich nicht auf die generische Einstellungsnamen, die in dieser Anleitung verwendet werden. Drahtlose Zugriffspunkt Details, zur Konfiguration müssen Sie die Produktdokumentation vom Hersteller des Ihre drahtlosen Zugriffspunkte überprüfen.

### <a name="instructions-for-deploying-nps-server-certificates"></a>Anweisungen zum Bereitstellen von NPS-Serverzertifikate
  
Es gibt zwei Alternativen für die Bereitstellung von NPS-Serverzertifikate. Dieses Handbuch bietet keine umfassende Anleitungen, können Sie ermitteln, welche Alternative Ihren Anforderungen am besten erfüllt. Im Allgemeinen sind jedoch die Optionen ab:

- Erwerben Zertifikate von einer öffentlichen Zertifizierungsstelle, z. B. VeriSign, die bereits von Windows-basierten Clients als vertrauenswürdig eingestuft werden. Diese Option ist für kleinere Netzwerke in der Regel empfohlen.

- Bereitstellen einer Public Key-Infrastruktur \(PKI\) in Ihrem Netzwerk mit AD CS. Dies wird empfohlen, für die meisten Netzwerke und die Anweisungen zum Bereitstellen von Serverzertifikaten mit AD CS stehen im oben erwähnten-Bereitstellungshandbuch.

### <a name="nps-network-policies-and-other-nps-settings"></a>NPS-Netzwerkrichtlinien und andere NPS-Einstellungen

Mit Ausnahme der Konfigurationseinstellungen vorgenommen werden, beim Ausführen der **konfigurieren 802.1 X** Assistent, wie in diesem Handbuch dokumentiert, dieses Handbuch bietet keine ausführliche Informationen zur manuellen Konfiguration von NPS-Bedingungen, Einschränkungen oder andere NPS-Einstellungen.

### <a name="dhcp"></a>DHCP

Diese Anleitung bietet keine Informationen zum Entwerfen oder DHCP-Subnetze für WLANs bereitstellen.

## <a name="technology-overviews"></a>Technologieübersichten
Folgendes sind Technologieübersichten für die Bereitstellung von drahtlosen Zugriff:

### <a name="ieee-8021x"></a>IEEE 802.1 X
Der IEEE 802.1X-Standard definiert die Steuerung des Zugriffs Port\-basierten Netzwerk, die verwendet wird, um authentifizierten Netzwerkzugriff auf Ethernet-Netzwerke bereitzustellen. Diese Port\-basierte Netzwerkzugriffsteuerung verwendet die physischen Merkmale der switched-LAN-Infrastruktur mit einem LAN-Anschluss verbundene Geräte zu authentifizieren. Zugriff auf den Port kann verweigert werden, wenn der Authentifizierungsvorgang fehlschlägt. Obwohl dieser Standard für verkabelte Ethernet-Netzwerke entwickelt wurde, wurde es und für 802.11-Drahtlos-LANs.

### <a name="8021x-capable-wireless-access-points-aps"></a>802.1X\-drahtloser Zugriffspunkte \(APs\)
Dieses Szenario erfordert die Bereitstellung von einem oder mehreren 802.1X\-Drahtloszugriffspunkt, die mit dem Remote Authentication Dial\-In User Service \(RADIUS\)-Protokoll kompatibel sind.

802.1 X und RADIUS\ kompatible Zugriffspunkte in der RADIUS-Infrastruktur mit einem RADIUS-Server, z. B. einem NPS-Server bereitgestellt werden aufgerufen, *RADIUS-Clients*.

### <a name="wireless-clients"></a>Drahtlose clients
Dieses Handbuch enthält umfassende Konfigurationsdetails für Domäne\ Mitglieder der Gruppe Zugriff mit 802.1X-Authentifizierung bereitstellen, die mit drahtlosen Clientcomputern unter Windows 10, Windows 8.1 und Windows 8 mit dem Netzwerk verbinden. Computer müssen der Domäne angehören, um authentifizierten Zugriff erfolgreich hergestellt.

>[!NOTE]
>Sie können auch Computer, auf denen Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 als drahtlose Clients ausgeführt werden.

### <a name="support-for-ieee-80211-standards"></a>Unterstützung für IEEE 802.11-Standards
Unterstützte Betriebssysteme für Windows und Windows Server bieten integrierten Unterstützung für 802.11-Drahtlosnetzwerke. In diesen Betriebssystemen wird Sie als eine drahtlose Verbindung im Netzwerk- und Freigabecenter ein installierte 802.11 drahtlose Netzwerkadapter angezeigt. 

Zwar integrierten Unterstützung für 802.11-Drahtlosnetzwerke, hängen die drahtlosen Komponenten von Windows die folgenden:

- Die Funktionen des drahtlosen Netzwerkadapters. Der wireless LAN oder Sicherheitsstandards, die Sie benötigen, muss der installierten Drahtlosnetzwerkadapter unterstützen. Wenn der funknetzwerkadapter Wi\-Fi Protected Access \(WPA\) nicht unterstützt, können nicht Sie z. B. aktivieren oder WPA Sicherheitsoptionen konfigurieren.

- Die Funktionen der Treiber für den Drahtlosnetzwerkadapter. Um Optionen für drahtloses Netzwerk konfigurieren können, muss der Treiber für den Adapter unterstützen die Berichterstattung für alle seine Funktionen für Windows. Stellen Sie sicher, dass der Treiber für den WLAN-Adapter für die Funktionen des Betriebssystems geschrieben wird. Stellen Sie außerdem sicher, dass der Treiber die aktuelle Version von Microsoft Update oder die Website der Hersteller der drahtlosen Netzwerkadapters überprüfen ist.

Die folgende Tabelle zeigt die Übertragungsrate und die Frequenzen für allgemeine drahtlosen IEEE 802.11-Standards.

|Standards|Frequenzen|Übertragung Bitraten|Verwendung|
|-------------|---------------|--------------------------|---------|  
|802.11|Industrielle S\-Band-wissenschaftliche und medizinische \(ISM\) Frequenzbereich \ (2.4 auf 2.5 GHz\)|2 Megabit pro Sekunde \(Mbps\)|Veraltet. Selten verwendet.|  
|802. 11 b|S\-Band-ISM|11 MBit/s|Häufig verwendet.|  
|802. 11a|C#-Band-ISM \ (5,725 zu 5.875 GHz\)|54 MBit/s|Nicht häufig verwendet, die Kosten und begrenzter Bereich.|  
|802. 11 g|S\-Band-ISM|54 MBit/s|Häufig verwendet. 802. 11 g-Geräte sind kompatibel mit 802. 11 b Geräte.|  
|802. 11n \2.4 und 5.0 GHz|C#-Band- und S\-Band-ISM|250 MBit/s|Geräte basierend auf der registrierungseintragswert Ratifizierung IEEE 802. 11n standard ist, seit August 2007 verfügbar. Viele 802. 11n Geräte sind kompatibel mit 802. 11a, b und g-Geräte.|
|802. 11ac |5 GHz |6,93 Gbit/s |802. 11ac, vom IEEE 2014 genehmigt ist skalierbar und schneller als 802. 11n und Zugriffspunkte und drahtlose Clients, in denen Unterstützung bereitgestellt wird.|

### <a name="wireless-network-security-methods"></a>Sicherheitsmethoden für Drahtlosnetzwerke
**Wireless-Netzwerk-Sicherheitsmethoden** ist eine informelle Gruppierung von drahtlosen Authentifizierung \ (auch als wireless Sicherheit\ bezeichnet) und wireless-Verschlüsselung. WLAN-Authentifizierung und Verschlüsselung sind paarweise um zu verhindern, dass nicht autorisierte Benutzer Zugriff auf das drahtlose Netzwerk, und schützen drahtlose Übertragungen verwendet werden. 

Wenn Sie drahtlos-Sicherheitseinstellungen in der drahtlosen Netzwerk Richtlinien von der Gruppenrichtlinie konfigurieren, stehen mehrere Kombinationen aus. Allerdings nur die WPA2\ Enterprise, WPA\ Enterprise, und Öffnen mit 802.1 X-Authentifizierungsstandards werden unterstützt für 802.1 X Authenticated wireless Bereitstellungen.

>[!NOTE]
>Während der Konfiguration der Wireless Network Policies, wählen Sie **WPA2\ Enterprise**, **WPA\ Enterprise**, oder **offen bei 802.1 X** Zugang zu den EAP-Einstellungen, die für 802.1 X drahtlosbereitstellungen authentifiziert erforderlich sind.  

#### <a name="wireless-authentication"></a>WLAN-Authentifizierung
Es wird empfohlen, dass die Verwendung von drahtlosen Authentifizierungsstandards für 802.1 X drahtlosbereitstellungen authentifiziert.  

**Wi\-Fi Protected Access – Enterprise \(WPA\-Enterprise\)** WPA ist ein vorläufige Standard, der von der WLAN-Alliance zur Einhaltung des Protokolls für drahtlose 802.11-Sicherheit entwickelt. Die WPA-Protokoll wurde in Reaktion auf eine Reihe von schweren Fehlern im Sicherheitsentwurf entwickelt, die im vorherigen Wired Equivalent Privacy \(WEP\) Protokoll ermittelt wurden.

WPA\ Enterprise bietet verbesserten Sicherheit gegenüber WEP werden durch:  

1. Eine Authentifizierung erforderlich ist, die 802.1X-Authentifizierung X EAP-Framework als Teil der Infrastruktur verwendet, die zentralisierte gegenseitige Authentifizierung und die dynamische Verwaltung der Schlüssel wird sichergestellt  

2. Verbessern die Integrität überprüfen Wert \(ICV\) mit einer Überprüfung der Integrität \(MIC\) zum Schutz der Header und der Nutzlast  

3. Implementieren einen Framezähler um Replay-Angriffe zu verhindern.  

**Wi\-Fi Protected Access 2 – Enterprise \(WPA2\-Enterprise\)** wie die WPA\-Enterprise standard, WPA2\-Enterprise verwendet, die 802.1 X und EAP-Framework. WPA2\ Enterprise bietet stärkeren Datenschutz für mehrere Benutzer und große verwaltete Netzwerke. WPA2\ Unternehmen ist eine stabile Protokoll, das entworfen wurde, um zu verhindern, dass nicht autorisierte Netzwerkzugriff durch die Überprüfung von Benutzern im Netzwerk über einen Authentifizierungsserver.  

#### <a name="wireless-security-encryption"></a>Wireless-Verschlüsselung
Schutz-Verschlüsselung wird verwendet, um die drahtlosen Übertragungen zu schützen, die zwischen dem drahtlosen Client und dem drahtlosen Zugriffspunkt gesendet werden. Wireless-Verschlüsselung wird in Verbindung mit der ausgewählten Netzwerkauthentifizierungsmethode für Sicherheit verwendet. Computer unter Windows 10, Windows 8.1 und Windows 8 Unterstützung standardmäßig zwei Verschlüsselungsstandards:

1. **Temporal Key Integrity Protocol** \(TKIP\) ist eine ältere Verschlüsselungsprotokoll, das ursprünglich Bereitstellen sicherer drahtlose Verschlüsselung als durch das kaum Wired Equivalent Privacy \(WEP\)-Protokoll bereitgestellt wurde. TKIP wurde entwickelt, vom IEEE 802. 11i Gruppe sowie die Wi\-Fi Alliance WEP ersetzen, ohne dass die ältere Hardware zu ersetzen. TKIP ist eine Suite von Algorithmen, die die WEP-Nutzlast kapselt und ermöglicht Benutzern älteren WLAN-Geräte Upgrade auf TKIP ohne Austausch von Hardware. Wie bei WEP verwendet TKIP die RC4-Verschlüsselungsalgorithmus Stream als basiert. Das neue Protokoll, verschlüsselt jedoch jedes mit einem eindeutigen Schlüssel und die Schlüssel sind sehr viel sicherer als die WEP. Obwohl TKIP eignet sich für ein Upgrade von Sicherheit bei älteren Geräten, die entwickelt wurden, nur WEP verwenden, nicht alle Sicherheitsprobleme WLANs näher, und in den meisten Fällen ist nicht aussagekräftig ist, um sensible Behörden oder Übertragungen von Unternehmensdaten zu schützen.  

2. **Advanced Encryption Standard** \(AES\) ist die bevorzugte Verschlüsselungsprotokoll für die Verschlüsselung von Daten für Unternehmen und Behörden. AES bietet eine höhere Sicherheitsstufe drahtlose Übertragung als TKIP oder WEP. Im Gegensatz zu TKIP und WEP erfordert AES drahtlose Hardware, die den AES-Standard unterstützt. AES ist ein Schlüssel Symmetric\ Verschlüsselungsstandard, die drei Blockchiffren AES\-128, AES\ 192 und AES\-256 verwendet.

In Windows Server 2016 stehen die folgenden AES\-basierten drahtlosen Verschlüsselungsmethoden für die Konfiguration im Drahtlosprofil Eigenschaften bei der Auswahl einer Authentifizierungsmethode des WPA2\-Unternehmen, die empfohlen wird.

1. **AES\-CCMP**. Counter-Modus Cipher Block Chaining Message Authentication Code Protocol \(CCMP\) implementiert die 802. 11i eignet sich für höhere sicherheitsverschlüsselung als die WEP und 128-Bit-AES-Verschlüsselung-Schlüssel verwendet.
2. **AES\ GCMP**. \(GCMP\) Galois Counter Mode-Protokoll wird durch 802. 11ac unterstützt, ist effizienter als AES\ CCMP und bietet eine bessere Leistung für drahtlose Clients. GCMP verwendet 256-Bit-AES-Verschlüsselungsschlüssel.

> [!IMPORTANT]
> Wired Equivalent Privacy wurde \(WEP\) den ursprünglichen Schutz standard, der zur Verschlüsselung des Netzwerkverkehrs verwendet wurde. Sie sollten nicht WEP in Ihrem Netzwerk bereitstellen, da bekannten Sicherheitsrisiken bei dieser veralteten Sicherheit vorhanden sind.

### <a name="active-directory-doman-services-ad-ds"></a>Active Directory Domain Services-\(AD DS\)
AD DS wird eine verteilte Datenbank, die gespeichert und verwaltet Informationen zu Netzwerkressourcen und anwendungsspezifische Daten aus Directory\-fähigen Anwendungen bereitgestellt. Administratoren können AD DS verwenden, um die Elemente eines Netzwerks, z. B. Benutzer, Computer und anderen Geräten in einer hierarchischen Containerstruktur zu organisieren. Hierarchische Struktur umfasst die Active Directory-Gesamtstruktur, Domänen in der Gesamtstruktur und Organisationseinheiten \(OUs\) in jeder Domäne. Ein Server mit AD DS wird aufgerufen, eine *Domänencontroller*.  

AD DS enthält die Benutzerkonten, Computerkonten und Eigenschaften, die von IEEE 802.1 X und PEAP\-MS\-CHAP v2 erforderlich sind, um Benutzeranmeldeinformationen zu authentifizieren und Autorisierung für drahtlose Verbindungen auszuwerten.

### <a name="active-directory-users-and-computers"></a>Active Directory-Benutzer und-Computer
Active Directory-Benutzer und-Computer ist eine Komponente von AD DS mit Konten, die physischen Entitäten, z. B. einem Computer, einer Person oder einer Sicherheitsgruppe darstellen. Ein *Sicherheitsgruppe* ist eine Sammlung von Benutzer- oder Computerkonten, die Administratoren als einzelne Einheit verwaltet werden können. Benutzer- und Computerkonten, die einer bestimmten Gruppe angehören, werden als bezeichnet *Gruppenmitglieder*.  

### <a name="group-policy-management"></a>Die Gruppenrichtlinien-Verwaltungskonsole
Die Gruppenrichtlinien-Verwaltungskonsole können Directory\-basierte Änderungs- und konfigurationsverwaltung von Benutzer- und Einstellungen, einschließlich Informationen zu Sicherheit und Benutzer. Sie können eine Gruppenrichtlinie verwenden, um Konfigurationen für Gruppen von Benutzern und Computern zu definieren. Mit der Gruppenrichtlinie können Sie Einstellungen für die Registrierungseinträge, Sicherheit, für die Softwareinstallation, Skripts, ordnerumleitung, Remoteinstallationsdienste und Internet Explorer-Wartung angeben. Die Gruppenrichtlinie, die Einstellungen, die Sie erstellen in einer Gruppenrichtlinie enthaltenen \(GPO\)-Objekt. Durch Zuordnen eines Gruppenrichtlinienobjekts mit ausgewählten Active Directory-System-Container – Standorten, Domänen und Organisationseinheiten – Sie können die Einstellungen des Gruppenrichtlinienobjekts für die Benutzer und Computer in diesen Active Directory-Containern anwenden. Um Gruppenrichtlinien-Objekte in einem Unternehmen zu verwalten, können Sie den Gruppenrichtlinienverwaltungs-Editor Microsoft Management Console \(MMC\) verwenden.  

Dieses Handbuch enthält ausführliche Anweisungen zum Angeben von Einstellungen in den Drahtlosnetzwerkrichtlinien \ (IEEE 802.11\) Erweiterung der Gruppenrichtlinien-Verwaltungskonsole. Das Drahtlosnetzwerk \ (IEEE 802.11\) Richtlinien konfigurieren Domäne\-Member-Clientcomputer mit der erforderlichen Konnektivität und drahtlose Einstellungen für 802.1 X-Drahtloszugriff.

### <a name="server-certificates"></a>Serverzertifikate
Dieses Bereitstellungsszenario sind Serverzertifikate für alle NPS-Server, die 802.1X-Authentifizierung erforderlich.  

Ein Serverzertifikat ist ein digitales Dokument, das häufig für die Authentifizierung und zum Sichern von Informationen in offenen Netzwerken verwendet wird. Ein Zertifikat bindet einen öffentlichen Schlüssel sicher an die Person, die den entsprechenden privaten Schlüssel enthält. Zertifikate werden von der ausstellenden Zertifizierungsstelle digital signiert, und sie können für einen Benutzer, einen Computer oder einen Dienst ausgestellt werden.  

Eine Zertifizierungsstelle \(CA\) ist eine Entität, die verantwortlich für das Einrichten und bestätigen der Authentizität öffentlicher Schlüssel für Antragsteller \ (normalerweise Benutzern oder Computer\) oder anderen Zertifizierungsstellen. Aktivitäten einer Zertifizierungsstelle umfassen das Binden öffentlicher Schlüssel an distinguished Names über signierte Zertifikate, Verwalten von Zertifikatsseriennummern und Sperren von Zertifikaten.  

Active Directory-Zertifikatdienste \(AD CS\) ist eine Serverrolle, die Zertifikate als Netzwerk-Zertifizierungsstelle ausstellt. Eine AD CS-Infrastruktur, auch bekannt als Zertifikat eine *public Key-Infrastruktur \(PKI\)*, stehen anpassbare Dienste zum Ausstellen und Verwalten von Zertifikaten für die Organisation.

### <a name="eap-peap-and-peap-ms-chap-v2"></a>EAP und PEAP PEAP\-MS\-CHAP v2
Extensible Authentication Protocol-\(EAP\) erweitert Point\-zu-Punkt-Protokoll \(PPP\) in eigener Regie zusätzliche Authentifizierungsmethoden, bei denen Anmeldeinformationen und Informationen mit tauscht Länge ausgetauscht. Mit EAP-Authentifizierung sowohl im Netzwerk zugreifen, Client und der Authentifikator \ (z. B. die NPS-Server\) muss unterstützen den gleichen EAP-Typ für die erfolgreiche Authentifizierung erfolgen kann. Windows Server 2016 umfasst eine EAP-Infrastruktur, unterstützt zwei EAP-Typen und die Möglichkeit, EAP-Nachrichten an den NPS-Server zu übergeben. Unter Verwendung von EAP unterstützen Sie zusätzliche Authentifizierungsschemas, bekannt als *EAP-Typen*. Die EAP-Typen, die durch Windows Server 2016 unterstützt werden:  

- Transport Layer Security \(TLS\)

- Microsoft Challenge Handshake Authentication Protocol Version 2 \ (MS\ CHAP v2\)

>[!IMPORTANT]
>Sichere EAP-Typen \ (z. B. solche, die auf Certificates\ basieren) bieten einen besseren Schutz gegen Brute\-Force-Angriffe, Verzeichnisangriffe und Kennwort Schutzfunktion als Password\-basierte Authentifizierungsprotokolle \ (z. B. Version 1\ CHAP oder MS\ CHAP).

Geschützte EAP-\(PEAP\) verwendet TLS, um einen verschlüsselten Kanal zwischen einem authentifizierten PEAP-Client, z. B. einem drahtlosen Computer und einem PEAP-Authentifikator, z. B. einem NPS-Server oder andere RADIUS-Server zu erstellen. PEAP gibt keine Authentifizierungsmethode an, aber es bietet zusätzliche Sicherheit für andere EAP-Authentifizierungsprotokolle \ (z. B. EAP\-MS\-CHAP v2\) kann, die über die TLS verschlüsselten Kanal von PEAP arbeiten. PEAP wird als Authentifizierungsmethode für den von Zugriffsclients verwendet, die mit dem Netzwerk über die folgenden Arten von Network Access Server \(NASs\) verbinden:

- 802.1X\-fähigen Drahtloszugriffspunkten

- 802.1X\-fähigen Switches authentifizieren

- Netzwerk-Computer unter Windows Server 2016 und der RAS-Dienst \(RAS\), die als virtuelle Private konfiguriert sind \(VPN\) Server, DirectAccess-Server oder beides

- Computer unter Windows Server 2016 und Remote Desktop Services

PEAP\-MS\-CHAP v2 ist einfacher als EAP\-TLS bereitstellen, da die Benutzerauthentifizierung ausgeführt wird, mithilfe von Password\ basierende Anmeldeinformationen \ (Benutzername und Password\) anstelle von Zertifikaten oder Smartcards. Nur NPS oder andere RADIUS-Server müssen über ein Zertifikat verfügen. NPS-Serverzertifikats wird von der NPS-Server während der Authentifizierung verwendet, um seine Identität gegenüber PEAP-Clients nach.

Dieses Handbuch enthält Anweisungen zum Konfigurieren der drahtlose Clients und der NPS-server\(s\) PEAP\-MS\-CHAP v2 für Zugriff mit 802.1X-Authentifizierung verwenden.

### <a name="network-policy-server"></a>Der Netzwerkrichtlinienserver
Network Policy Server \(NPS\) können Sie zentral konfigurieren und verwalten Netzwerkrichtlinien mithilfe von Remote Authentication Dial\-In User Service \(RADIUS\) Server und RADIUS-Proxy. NPS ist erforderlich, wenn Sie den drahtlosen Zugriff mit 802.1X-Authentifizierung bereitstellen.

Wenn Sie Ihre 802.1 X drahtlose Zugriffspunkte als RADIUS-Clients in NPS konfigurieren, werden die NPS verbindungsanforderungen von APs verarbeitet. Während der Verarbeitung der Verbindung-Anforderung führt NPS Authentifizierung und Autorisierung. Authentifizierung bestimmt, ob der Client gültige Anmeldeinformationen verfügt. Wenn der NPS erfolgreich den anfordernden Client authentifiziert, bestimmt NPS, ob der Client für den angeforderten Verbindungsaufbau autorisiert ist, und entweder zulässt oder verweigert Verbindung. Dies ist wie folgt ausführlicher erläutert:

#### <a name="authentication"></a>Authentifizierung

Erfolgreicher gegenseitige PEAP\-MS\-CHAP v2-Authentifizierung verfügt über zwei Hauptkomponenten:

1.  Der Client authentifiziert den NPS-Server.  Während dieser Phase der gegenseitige Authentifizierung sendet der NPS-Server das Serverzertifikat auf dem Clientcomputer, sodass der Client des NPS-Servers mit dem Zertifikat Identität kann. Um die NPS-Server erfolgreich zu authentifizieren, muss der Clientcomputer der Zertifizierungsstelle vertrauen, die NPS-Serverzertifikat ausgestellt hat. Der Client vertraut diese Zertifizierungsstelle, wenn das Zertifizierungsstellenzertifikat im Zertifikatspeicher vertrauenswürdige Stammzertifizierungsstellen auf dem Clientcomputer vorhanden ist.

    Wenn Sie eine eigene private Zertifizierungsstelle bereitstellen, wird das Zertifikat der Zertifizierungsstelle automatisch im Zertifikatspeicher vertrauenswürdige Stammzertifizierungsstellen für den aktuellen Benutzer und für den lokalen Computer installiert, der Gruppenrichtlinie auf dem Client Domänenmitgliedscomputer aktualisiert wird. Wenn Sie Zertifikate von einer öffentlichen Zertifizierungsstelle bereitstellen möchten, stellen Sie sicher, dass das öffentliche Zertifikat der Zertifizierungsstelle bereits in den Zertifikatspeicher für vertrauenswürdige Stammzertifizierungsstellen ist.  

2.  Der NPS-Server authentifiziert den Benutzer. Nach der erfolgreichen Authentifizierung des Clients den NPS-Server, sendet der Client die Anmeldeinformationen des Benutzers Password\-basierte an den Netzwerkrichtlinienserver, der Anmeldeinformationen des Benutzers in Active Directory-Domänendiensten \(AD DS\) der Benutzerkonten-Datenbank dient.

Wenn die Anmeldeinformationen gültig sind und die Authentifizierung erfolgreich ist, beginnt der NPS-Server die Autorisierung-Phase der Verarbeitung der verbindungsanforderung. Wenn die Anmeldeinformationen nicht gültig sind, und schlägt die Authentifizierung fehl, NPS sendet eine Nachricht Zugriff ablehnen und die die verbindungsanforderung wurde abgelehnt.  

#### <a name="authorization"></a>Autorisierung

Der Server mit NPS führt die Autorisierung wie folgt:  

1. NPS überprüft die Einschränkungen in der Benutzer oder Computer Dial\-Eigenschaften des Benutzerkontos in AD DS. Alle Benutzer- und Computerkonto in Active Directory-Benutzer und -Computer enthält mehrere Eigenschaften, einschließlich finden Sie auf der **Dial\ in** Registerkarte. Auf dieser Registerkarte im **Netzwerkzugriffsberechtigungen**, wenn der Wert **Zugriff zulassen**, den Benutzer oder Computer ist berechtigt, eine Verbindung mit dem Netzwerk herstellen. Wenn der Wert **Verweigern des Zugriffs**, den Benutzer oder Computer ist nicht berechtigt, eine Verbindung mit dem Netzwerk herstellen. Wenn der Wert **steuern den Zugriff über die NPS-Netzwerkrichtlinien**, NPS wertet die konfigurierten Netzwerkrichtlinien, um festzustellen, ob der Benutzer oder Computer autorisiert ist, eine Verbindung mit dem Netzwerk herstellen. 

2. NPS verarbeitet die Netzwerkrichtlinien, um eine Richtlinie zu finden, die verbindungsanforderung entspricht. Wenn eine übereinstimmende Richtlinie gefunden wird, NPS entweder gewährt oder verweigert die Verbindung entsprechend der Konfiguration dieser Richtlinie.  

Wenn Authentifizierung und Autorisierung erfolgreich sind, und übereinstimmende Netzwerkrichtlinie Zugriff gewährt, NPS gewährt Zugriff auf das Netzwerk und den Benutzer und Computer können, eine Verbindung mit Netzwerkressourcen, die für die sie über Berechtigungen verfügen.  

>[!NOTE]
>Zum drahtlosen Zugriff bereitstellen, müssen Sie die NPS-Richtlinien konfigurieren. Dieses Handbuch enthält Anweisungen zum Verwenden der **konfigurieren 802.1 X** auf dem Netzwerkrichtlinienserver, um NPS-Richtlinien für drahtlosen Zugriff 802.1X-authentifizierten zu erstellen.  

### <a name="bootstrap-profiles"></a>Bootstrap-Profile
In 802.1X\-authentifizierte drahtlose Netzwerke drahtlose Clients müssen Anmeldeinformationen Sicherheit, die vom RADIUS-Server authentifiziert werden, um eine Verbindung mit dem Netzwerk herstellen. Für geschütztes EAP \[PEAP\]\-Microsoft Challenge Handshake Authentication Protocol Version 2 \[MS\-CHAP v2\], die Anmeldeinformationen sind eine Kombination aus Benutzername und Kennwort. Für EAP\-Transport Layer Security \[TLS\] oder PEAP\-TLS, die Anmeldeinformationen sind Zertifikate, z. B. Benutzer- und Clientzertifikate oder Smartcards.

Wenn eine Verbindung mit einem Netzwerk herstellen, der zum Ausführen von PEAP\-MS\-CHAP v2, PEAP\-TLS oder EAP\-TLS-Authentifizierung konfiguriert ist, wird standardmäßig, müssen Windows-Drahtlosclients auch ein Computerzertifikat überprüfen, die vom RADIUS-Server gesendet wird. Das Zertifikat, das vom RADIUS-Server, für jede Sitzung gesendet wird wird häufig als ein Serverzertifikat bezeichnet.

Wie bereits erwähnt, Sie können Ihre RADIUS-Server ihre Serverzertifikat auszustellen auf zwei Arten: von einer kommerziellen Zertifizierungsstelle \ (z. B. VeriSign, Inc., \), oder von einer privaten Zertifizierungsstelle, die Sie in Ihrem Netzwerk bereitstellen. Wenn der RADIUS-Server ein Computerzertifikat, die von einer kommerziellen Zertifizierungsstelle ausgestellt wurde, die bereits ein Stammzertifikat im Speicher vertrauenswürdiger Stammzertifizierungsstellen-Zertifikatspeicher des Clients installiert sendet, kann dann der Drahtlosclient überprüfen Computerzertifikat des RADIUS-Servers, unabhängig davon, ob der Drahtlosclient Active Directory-Domäne verknüpft ist. In diesem Fall der Drahtlosclient mit dem Drahtlosnetzwerk herstellen kann und Sie können den Computer der Domäne beitreten.

>[!NOTE]
>Das Verhalten der Client das Serverzertifikat kann deaktiviert werden, aber Deaktivieren der Überprüfung des Serverzertifikats wird in produktionsumgebungen nicht empfohlen.

Wireless bootstrap-Profile sind temporäre Profile, die in einer Weise drahtlosen Client-Benutzer zur Verbindung mit dem 802.1X\ können konfiguriert werden-authentifizierte Drahtlosnetzwerk, bevor der Computer der Domäne, And\ angehört / haben bzw. bevor der Benutzer erfolgreich mit der Domäne angemeldet hat mit einem bestimmten drahtlose Computer zum ersten Mal.  In diesem Abschnitt werden zusammengefasst, welches Problem festgestellt wird, wenn Sie versuchen, zum Hinzufügen eines drahtlosen Computers zur Domäne oder für einen Benutzer mit einem Domäne\ verbundene drahtlose Computer zum ersten Mal an der Domäne anmelden.

Für Bereitstellungen, in dem der Benutzer oder IT-Administrator kann nicht physisch Verbinden von Computern mit dem Ethernet-Netzwerk mit der Domäne beitritt, und der Computer verfügt nicht über die erforderlichen ausstellende, ZS-Zertifikat installiert Stamm seine **vertrauenswürdige Stammzertifizierungsstellen** Zertifikatspeicher, können Sie die drahtlose Clients konfigurieren, mit einem Profil temporäre drahtlose Verbindung mit dem Namen einer *Bootstrapping Profil* , eine Verbindung mit dem Drahtlosnetzwerk herstellen.

Ein *Bootstrapping Profil* nicht mehr erforderlich, das Computerzertifikat des RADIUS-Servers zu überprüfen. Diese temporäre Konfiguration ermöglicht drahtlosen Benutzern das Hinzufügen des Computers zur Domäne, mit der die Zeit für das Drahtlosnetzwerk \ (IEEE 802.11\)-Richtlinien werden angewendet und die entsprechenden Stamm-CA-Zertifikat wird automatisch auf dem Computer installiert.

Wenn eine Gruppenrichtlinie angewendet wird, werden ein oder mehrere drahtlose Verbindung-Profile, die die Anforderung für die gegenseitige Authentifizierung erzwingen auf dem Computer angewendet. Das bootstrap-Profil ist nicht mehr erforderlich und wird entfernt. Nach dem Hinzufügen des Computers zur Domäne und den Computer neu starten, kann der Benutzer eine drahtlose Verbindung verwenden, an der Domäne anmelden.

Eine Übersicht über den drahtlosen Zugriff Bereitstellungsprozess diesen Technologien finden Sie unter [drahtlosen Zugriff Bereitstellungsübersicht](b-wireless-access-deploy-overview.md).
