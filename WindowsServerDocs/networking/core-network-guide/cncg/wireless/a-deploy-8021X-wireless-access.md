---
title: Bereitstellung des kennwortbasierten authentifizierten 802.1X-Funkzugriffs
description: Dieses Thema ist Teil des Windows Server 2016-Netzwerk Handbuchs "Bereitstellen von Kenn Wort basiertem 802.1 x authentifizierten drahtlosen Zugriff".
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: ff06ba23-9c0f-49ec-8f7b-611cf8d73a1b
ms.author: lizross
author: eross-msft
ms.openlocfilehash: a03d9d1b0532c846e8514ca904d38ea825baf4d4
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318128"
---
# <a name="deploy-password-based-8021x-authenticated-wireless-access"></a>Bereitstellen von Kenn Wort\-basiertem drahtlos Zugriff mit 802.1 x-Authentifizierung

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Dies ist ein Begleit Handbuch zum Windows Server&reg; 2016-Kern Netzwerk Handbuch. Das Handbuch zum Hauptnetzwerk enthält Anweisungen zum Planen und Bereitstellen der Komponenten, die für ein voll funktionsfähiges Netzwerk und eine neue Active Directory® Domäne in einer neuen Gesamtstruktur erforderlich sind.

In diesem Handbuch wird erläutert, wie Sie auf einem Kern Netzwerk aufbauen, indem Sie Anweisungen zum Bereitstellen von Technikern von Elektro-und Elektronik Technikern \(IEEE\) 802.1 x\-authentifizierten IEEE 802,11-drahtlos Zugriff mit dem geschützten Extensible Authentication Protocol – Microsoft Challenge Handshake Authentication Protocol Version 2 \(PAP\-MS\-CHAP v2\)bereitstellen.

Da der PEAP-\-MS\-CHAP v2 erfordert, dass Benutzer während des Authentifizierungs Vorgangs auf Kenn Wort\-basierende Anmelde Informationen anstelle eines Zertifikats anwenden, ist es in der Regel einfacher und kostengünstiger, als EAP\-TLS oder PEAP\-TLS.

>[!NOTE]
>In diesem Handbuch wird der von IEEE 802.1 x authentifizierte drahtlos Zugriff mit dem Peer-\-MS\-CHAP v2 als "drahtloser Zugriff" und "WLAN-Zugriff" abgekürzt.

## <a name="about-this-guide"></a>Informationen zur Anleitung
Diese Anleitung enthält in Kombination mit den unten beschriebenen Voraussetzungen Anweisungen zum Bereitstellen der folgenden WiFi-Zugriffs Infrastruktur.  

- Mindestens ein 802.1 x\-802,11 fähige drahtlos Zugriffspunkte \(APS\).

- Active Directory Domain Services \(AD DS\) Benutzer und Computer.

- Gruppenrichtlinienverwaltung

- Ein oder mehrere Netzwerk Richtlinien Server \(NPS-\) Server.

- Serverzertifikate für Computer, auf denen NPS ausgeführt wird

- Drahtlose Client Computer, auf denen Windows&reg; 10, Windows 8.1 oder Windows 8 ausgeführt wird.

### <a name="dependencies-for-this-guide"></a>Abhängigkeiten für dieses Handbuch

Um mit diesem Handbuch authentifizierte drahtlos Bereitstellungen erfolgreich bereitzustellen, müssen Sie über eine Netzwerk-und Domänen Umgebung mit allen erforderlichen Technologien verfügen. Außerdem müssen Sie für Ihre authentifizier enden NPSS Server Zertifikate bereitgestellt haben.

In den folgenden Abschnitten finden Sie Links zu Dokumentationen, die Ihnen zeigen, wie diese Technologien bereitgestellt werden.

#### <a name="network-and-domain-environment-dependencies"></a>Abhängigkeiten von Netzwerk-und Domänen Umgebungen

Dieses Handbuch richtet sich an Netzwerk-und Systemadministratoren, die die Anweisungen im Windows Server 2016- **Kern Netzwerk Handbuch** zum Bereitstellen eines Kern Netzwerks befolgt haben, oder für diejenigen, die zuvor die Kerntechnologien im Kern Netzwerk bereitgestellt haben, einschließlich AD DS, Domain Name System \(DNS\), Dynamic Host Configuration-Protokoll \(DHCP-\), TCP\/IP, NPS und Windows Internet Name Service \(WINS\)  

Das Handbuch zum Hauptnetzwerk ist an den folgenden Orten verfügbar:

- Das Windows Server 2016- [Kern Netzwerk Handbuch](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide) ist in der technischen Bibliothek für Windows Server 2016 verfügbar. 

- Das [Handbuch](https://gallery.technet.microsoft.com/Core-Network-Guide-for-9da2e683) zum Hauptnetzwerk ist auch im Word-Format in der TechNet Gallery unter [https://gallery.technet.microsoft.com/Core-Network-Guide-for-9da2e683](https://gallery.technet.microsoft.com/Core-Network-Guide-for-9da2e683)verfügbar.

#### <a name="server-certificate-dependencies"></a>Server Zertifikat Abhängigkeiten
Es gibt zwei Optionen für die Registrierung von Authentifizierungs Servern bei Server Zertifikaten für die Verwendung mit der 802.1 x-Authentifizierung: Stellen Sie Ihre eigene Public Key-Infrastruktur mithilfe von Active Directory-Zertifikat Diensten \(AD CS\) bereit, oder verwenden Sie Server Zertifikate, die von einer öffentlichen Zertifizierungsstelle \(ca\)angemeldet sind.

##### <a name="ad-cs"></a>AD CS
Netzwerk-und Systemadministratoren, die authentifizierte drahtlos Bereitstellungen bereitstellen, müssen die Anweisungen im Windows Server 2016 Core Network-Begleit Handbuch befolgen **und Server Zertifikate für drahtlose und drahtlose 802.1 x-bereit Stellungen**bereitstellen. In diesem Handbuch wird erläutert, wie Sie AD CS für die automatische Registrierung von Server Zertifikaten für Computer mit NPS bereitstellen und verwenden.

Dieses Handbuch ist unter folgendem Speicherort verfügbar.

- Im Windows Server 2016 Core Network-Begleit Handbuch werden [Server Zertifikate für drahtlose und drahtlose 802.1 x-bereit Stellungen](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments?f=255&MSPPError=-2147217396) im HTML-Format in der technischen Bibliothek bereitgestellt. 

##### <a name="public-ca"></a>Öffentliche Zertifizierungsstelle
Sie können Server Zertifikate von einer öffentlichen Zertifizierungsstelle, z. b. VeriSign, erwerben, der Client Computer bereits Vertrauen. 

Ein Client Computer vertraut einer Zertifizierungsstelle, wenn das Zertifizierungsstellen Zertifikat im Zertifikat Speicher für vertrauenswürdige Stamm Zertifizierungsstellen installiert ist. Standardmäßig verfügen Computer, auf denen Windows ausgeführt wird, über mehrere öffentliche Zertifizierungsstellen Zertifikate im Zertifikat Speicher vertrauenswürdiger Stamm Zertifizierungsstellen.  

Sie sollten die Entwurfs- und Bereitstellungshandbücher für jede der Technologien einsehen, die in diesem Bereitstellungsszenario verwendet werden. Diese Handbücher können Ihnen helfen, zu bestimmen, ob dieses Bereitstellungsszenario die Dienste und Konfigurationen bietet, die Sie zur Organisation des Netzwerks benötigen.

### <a name="requirements"></a>Voraussetzungen
Im folgenden finden Sie die Anforderungen für die Bereitstellung einer drahtlos Zugriffs Infrastruktur mithilfe des Szenarios, das in diesem Handbuch dokumentiert ist:

- Vor der Bereitstellung dieses Szenarios müssen Sie zunächst 802.1 x\-fähigen drahtlosen Zugriffs Punkten erwerben, um an den gewünschten Orten an Ihrem Standort eine drahtlose Abdeckung bereitzustellen. Der Planungsabschnitt dieses Handbuchs unterstützt Sie bei der Ermittlung der Features, die von ihren APS unterstützt werden müssen.

- Active Directory Domain Services \(AD DS\) installiert ist, wie die anderen erforderlichen Netzwerktechnologien, gemäß den Anweisungen im Windows Server 2016-Kern Netzwerk Handbuch.  

- AD CS wird bereitgestellt, und Server Zertifikate werden bei NPSS registriert. Diese Zertifikate sind erforderlich, wenn Sie die in diesem Handbuch verwendete Authentifizierungsmethode\-MS\-CHAP v2-Zertifikat\-basierten Authentifizierungsmethode bereitstellen.

- Ein Mitglied Ihrer Organisation ist mit den IEEE 802,11-Standards vertraut, die von ihren drahtlos Zugriffs Punkten und den drahtlos Netzwerkadaptern unterstützt werden, die auf den Client Computern und Geräten in Ihrem Netzwerk installiert sind. Beispielsweise ist eine Person in Ihrer Organisation mit Radio Frequency Types, 802,11 Wireless Authentication \(WPA2-oder WPA-\)und Chiffren \(AES-oder TKIP-\)vertraut.

## <a name="what-this-guide-does-not-provide"></a>Nicht in diesem Handbuch enthaltene Informationen  
Im folgenden finden Sie einige Elemente, die in diesem Handbuch nicht enthalten sind:

### <a name="comprehensive-guidance-for-selecting-8021x-capable-wireless-access-points"></a>Umfassende Richtlinien für die Auswahl von 802.1 x\-fähigen drahtlosen Zugriffs Punkten

Da viele Unterschiede zwischen Marken und Modellen von 802.1 x\-fähigen drahtlos Zugriffs Punkten bestehen, bietet dieses Handbuch keine detaillierten Informationen zu folgenden Punkten:  

- Die Bestimmung, welche Marke oder welches drahtlos Zugriffspunkt am besten für Ihre Anforderungen geeignet ist.

- Die physische Bereitstellung von drahtlos Zugriffs Punkten in Ihrem Netzwerk.

- Erweiterte drahtlose AP-Konfiguration, z. b. für drahtlose virtuelle lokale Netzwerke \(VLANs\).

- Anweisungen zum Konfigurieren eines drahtlosen AP-Anbieters\-bestimmten Attributen in NPS.

Außerdem variieren die Terminologie und die Namen für Einstellungen zwischen drahtlosen AP-Marken und-Modellen und stimmen möglicherweise nicht mit den in diesem Handbuch verwendeten generischen Einstellungs Namen identisch. Informationen zur Konfiguration von drahtlos Zugriffs Punkten finden Sie in der Produktdokumentation des Herstellers Ihrer drahtlos Zugriffspunkte.

### <a name="instructions-for-deploying-nps-certificates"></a>Anweisungen zum Bereitstellen von NPS-Zertifikaten
  
Es gibt zwei Alternativen für die Bereitstellung von NPS-Zertifikaten. Dieses Handbuch enthält keine umfassenden Anleitungen, mit denen Sie ermitteln können, welche Alternative Ihren Anforderungen am besten entspricht. Im Allgemeinen werden jedoch die folgenden Optionen angezeigt:

- Erwerben von Zertifikaten von einer öffentlichen Zertifizierungsstelle, z. b. VeriSign, die bereits von Windows\-basierten Clients als vertrauenswürdig eingestuft werden. Diese Option wird in der Regel für kleinere Netzwerke empfohlen.

- Bereitstellen einer Public Key-Infrastruktur \(PKI-\) in Ihrem Netzwerk mithilfe von AD CS. Dies wird für die meisten Netzwerke empfohlen, und die Anweisungen zum Bereitstellen von Server Zertifikaten mit AD CS finden Sie im zuvor erwähnten Bereitstellungs Handbuch.

### <a name="nps-network-policies-and-other-nps-settings"></a>NPS-Netzwerk Richtlinien und andere NPS-Einstellungen

Mit Ausnahme der Konfigurationseinstellungen, die bei der Ausführung des Assistenten zum **Konfigurieren von 802.1 x** vorgenommen werden (wie in diesem Handbuch beschrieben), bietet dieses Handbuch keine detaillierten Informationen zum manuellen Konfigurieren von NPS-Bedingungen, Einschränkungen oder anderen NPS-Einstellungen.

### <a name="dhcp"></a>DHCP

Dieses Bereitstellungs Handbuch enthält keine Informationen zum Entwerfen oder Bereitstellen von DHCP-Subnetzen für drahtlose LANs.

## <a name="technology-overviews"></a>Technologieübersicht
Im folgenden finden Sie Technologie Übersichten für die Bereitstellung von drahtlos Zugriff:

### <a name="ieee-8021x"></a>IEEE 802.1X
Der IEEE 802.1 x-Standard definiert die Port\-basierten Netzwerk Zugriffs Steuerung, die verwendet wird, um authentifizierten Netzwerk Zugriff auf Ethernet-Netzwerke bereitzustellen. Dieser Port\-basierten Netzwerk Zugriffs Steuerung verwendet die physischen Merkmale der umschten LAN-Infrastruktur, um Geräte zu authentifizieren, die mit einem LAN-Anschluss verbunden sind. Der Zugriff auf den Port kann verweigert werden, wenn der Authentifizierungsvorgang fehlschlägt. Obwohl dieser Standard für verkabelte Ethernet-Netzwerke entwickelt wurde, wurde er für die Verwendung auf 802,11 Wireless LANs angepasst.

### <a name="8021x-capable-wireless-access-points-aps"></a>802.1 x\-fähige drahtlos Zugriffspunkte \(APS\)
Dieses Szenario erfordert die Bereitstellung mindestens einer 802.1 x\-fähigen drahtlos Zugriffspunkte, die mit dem Remote Authentication Dial\-in User Service \(RADIUS\)-Protokoll kompatibel sind.

802.1 x-und RADIUS-\-konforme APS werden bei der Bereitstellung in einer RADIUS-Infrastruktur mit einem RADIUS-Server wie z. b. einem NPS als *RADIUS-Clients*bezeichnet.

### <a name="wireless-clients"></a>Drahtlose Clients
Dieses Handbuch enthält umfassende Konfigurationsdetails zum Bereitstellen von 802.1 x-authentifizierten Zugriff für Domänen\-Mitglieds Benutzer, die eine Verbindung mit dem Netzwerk mit drahtlosen Client Computern unter Windows 10, Windows 8.1 und Windows 8 herstellen. Computer müssen der Domäne hinzugefügt werden, um erfolgreich authentifizierten Zugriff zu gewährleisten.

>[!NOTE]
>Sie können auch Computer verwenden, auf denen Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 als drahtlose Clients ausgeführt werden.

### <a name="support-for-ieee-80211-standards"></a>Unterstützung für IEEE 802,11-Standards
Unterstützte Windows-und Windows Server-Betriebssysteme bieten integrierte\-zur Unterstützung von Drahtlos Netzwerken in 802,11. In diesen Betriebssystemen wird ein installierter drahtloser Netzwerkadapter mit 802,11 als drahtlose Netzwerkverbindung im Netzwerk-und Freigabe Center angezeigt. 

Obwohl es\-zur Unterstützung von Drahtlos Netzwerken in 802,11 gibt, sind die drahtlosen Komponenten von Windows von folgenden Komponenten abhängig:

- Die Funktionen des drahtlos Netzwerkadapters. Der installierte drahtlose Netzwerkadapter muss die von Ihnen benötigten drahtlosen LAN-oder drahtlos Sicherheitsstandards unterstützen. Wenn der Drahtlos Netzwerkadapter z. b. keinen Wi\-Fi-geschützten Zugriff \(WPA\)unterstützt, können Sie WPA-Sicherheitsoptionen nicht aktivieren oder konfigurieren.

- Die Funktionen des Drahtlos Netzwerkadapter-Treibers. Damit Sie drahtlos Netzwerkoptionen konfigurieren können, muss der Treiber für den Drahtlos Netzwerkadapter die Berichterstellung aller Funktionen von Windows unterstützen. Vergewissern Sie sich, dass der Treiber für den Drahtlos Netzwerkadapter für die Funktionen Ihres Betriebssystems geschrieben wurde. Stellen Sie außerdem sicher, dass der Treiber die aktuellste Version ist, indem Sie Microsoft Update oder die Website des Anbieters des drahtlos Netzwerkadapters überprüfen.

In der folgenden Tabelle sind die Übertragungsraten und Häufigkeits Raten für gängige IEEE 802,11-drahtlos Standards aufgeführt.

|Standards|Eigen|Bitübertragungs Raten|Verwendung|
|-------------|---------------|--------------------------|---------|  
|802,11|S\-Band Industrie, wissenschaftlich und medizinisch \(ISM\) Frequenzbereich \(2,4 bis 2,5 GHz\)|2 meits pro Sekunde \(Mbit/s\)|Veraltet. Nicht häufig verwendet.|  
|802.11 b|S\--Band-ISM|11 Mbit/s|Häufig verwendet.|  
|802.11 a|C\--Band-ISM \(5,725 bis 5,875 GHz\)|54 Mbit/s|Nicht häufig aufgrund von Kosten und begrenztem Bereich verwendet.|  
|802.11 g|S\--Band-ISM|54 Mbit/s|Häufig verwendet. 802.11 g-Geräte sind kompatibel mit 802.11 b-Geräten.|  
|802.11 n \ 2,4 und 5,0 GHz|C\--und S\--Band-ISM|250 Mbit/s|Geräte, die auf dem Pre\--Standard für die Ratifizierung der Norm IEEE 802.11 n basieren, wurden im August 2007 verfügbar Viele 802.11 n-Geräte sind kompatibel mit den Geräten 802.11 a, b und g.|
|802.11ac |5 GHz |6,93 Gbit/s |802.11 AC, von IEEE in 2014 genehmigt, ist skalierbarer und schneller als 802.11 n und wird bereitgestellt, wo von APS und drahtlosen Clients diese unterstützt werden.|

### <a name="wireless-network-security-methods"></a>Sicherheitsmethoden für drahtlose Netzwerke
Bei **drahtlosen Netzwerk Sicherheitsmethoden** handelt es sich um eine informelle Gruppierung von drahtlos Authentifizierung \(manchmal auch als drahtlose Sicherheits\) und drahtlose Sicherheits Verschlüsselung bezeichnet. Drahtlose Authentifizierung und Verschlüsselung werden paarweise verwendet, um zu verhindern, dass nicht autorisierte Benutzer auf das Drahtlos Netzwerk zugreifen und drahtlose Übertragungen geschützt werden. 

Wenn Sie die drahtlos Sicherheitseinstellungen in den Drahtlos Netzwerk Richtlinien von Gruppenrichtlinie konfigurieren, können Sie mehrere Kombinationen auswählen. Allerdings werden nur die Authentifizierungs Standards WPA2\-Enterprise, WPA\-Enterprise und Open with 802.1 x für authentifizierte 802.1 x-drahtlos Bereitstellungen unterstützt.

>[!NOTE]
>Beim Konfigurieren von Drahtlos Netzwerk Richtlinien müssen Sie **WPA2\-Enterprise**, **WPA\-Enterprise**oder **Open with 802.1 x** auswählen, um Zugriff auf die EAP-Einstellungen zu erhalten, die für die Bereitstellung von bereit Stellungen mit 802.1 x-Authentifizierung erforderlich sind.  

#### <a name="wireless-authentication"></a>Drahtlose Authentifizierung
In diesem Handbuch wird die Verwendung der folgenden drahtlosen Authentifizierungs Standards für drahtlos Bereitstellungen mit 802.1 x-Authentifizierung empfohlen.  

**Wi\-Fi Protected Access – Enterprise \(WPA\-Enterprise\)** WPA ist ein zwischen Standard, der von der WiFi-Allianz entwickelt wurde, um das 802,11-drahtlos Sicherheitsprotokoll einzuhalten. Das WPA-Protokoll wurde als Reaktion auf eine Reihe schwerwiegender Fehler entwickelt, die in der vorhergehenden Datenschutz \(WEP-\) Protokolls erkannt wurden.

WPA\-Enterprise bietet verbesserte Sicherheit gegenüber WEP durch:  

1. Erfordert eine Authentifizierung, bei der das 802.1 x EAP-Framework als Teil der Infrastruktur verwendet wird, das die zentralisierte gegenseitige Authentifizierung und dynamische Schlüsselverwaltung gewährleistet  

2. Verbessern des Werts der Integritäts Überprüfung \(ICV-\) mit einer Nachrichten Integritäts Überprüfung \(MIC-\), um den Header und die Nutzlast zu schützen  

3. Implementieren eines Frame Zählers, um Wiedergabe Angriffe abzuraten  

**Wi\-Fi Protected Access 2 – Enterprise \(WPA2\-Enterprise\)** Wie der WPA\-Enterprise Standard verwendet WPA2\-Enterprise das 802.1 x-und das EAP-Framework. WPA2\-Enterprise bietet stärkeren Datenschutz für mehrere Benutzer und große verwaltete Netzwerke. WPA2\-Enterprise ist ein stabiles Protokoll, das dazu dient, unbefugten Netzwerk Zugriff zu verhindern, indem Netzwerk Benutzer über einen Authentifizierungsserver überprüft werden.  

#### <a name="wireless-security-encryption"></a>Drahtlose Sicherheits Verschlüsselung
Die drahtlose Sicherheits Verschlüsselung wird verwendet, um die drahtlos Übertragungen zu schützen, die zwischen dem drahtlosen Client und dem drahtlos Zugriffspunkt gesendet werden. Die Verschlüsselung der drahtlos Sicherheit wird in Verbindung mit der ausgewählten Authentifizierungsmethode für die Netzwerksicherheit verwendet. Standardmäßig unterstützen Computer, auf denen Windows 10, Windows 8.1 und Windows 8 ausgeführt wird, zwei Verschlüsselungsstandards:

1. Das **Temporale Schlüssel Integritäts Protokoll** \(TKIP\) ist ein älteres Verschlüsselungsprotokoll, das ursprünglich so entworfen wurde, dass es eine sicherere drahtlose Verschlüsselung bietet, als die von der inhärenten \(WEP\)-Protokoll gleichwertige Datenschutz. TKIP wurde von der Taskgruppe IEEE 802.11 i und der Wi\-fi-Allianz entworfen, um WEP zu ersetzen, ohne dass Legacy Hardware ersetzt werden muss. TKIP ist eine Suite von Algorithmen, die die WEP-Nutzlast kapselt und es Benutzern von Legacy-WiFi-Geräten ermöglicht, ein Upgrade auf TKIP auszuführen, ohne Hardware zu ersetzen. Wie WEP verwendet TKIP den RC4-Stream-Verschlüsselungsalgorithmus als Grundlage. Das neue Protokoll verschlüsselt jedoch jedes Datenpaket mit einem eindeutigen Verschlüsselungsschlüssel, und die Schlüssel sind wesentlich stärker als die von WEP. TKIP eignet sich zwar zum Aktualisieren der Sicherheit auf älteren Geräten, die ausschließlich für WEP konzipiert waren, aber nicht alle Sicherheitsprobleme, auf die drahtlose LANs gerichtet sind, und in den meisten Fällen ist es nicht ausreichend robust, sensible Behörden oder Unternehmensdaten zu schützen. Übertragungen.  

2. **Advanced Encryption Standard** \(AES\) ist das bevorzugte Verschlüsselungsprotokoll für die Verschlüsselung von kommerziellen und behördlichen Daten. AES bietet ein höheres Maß an drahtlos Übertragungssicherheit als TKIP oder WEP. Im Gegensatz zu TKIP und WEP erfordert AES drahtlose Hardware, die den AES-Standard unterstützt. AES ist ein symmetrischer\-Schlüssel Verschlüsselungsstandard, der drei Blockchiffren, AES\-128, AES\-192 und AES\-256 verwendet.

In Windows Server 2016 sind die folgenden AES\-basierten drahtlos Verschlüsselungsmethoden für die Konfiguration in den Eigenschaften von drahtlos Profilen verfügbar, wenn Sie eine Authentifizierungsmethode von WPA2\-Enterprise auswählen. Dies wird empfohlen.

1. **AES-\-CCMP**. Im Leistungsmodus-Verschlüsselungs Block Verkettung Nachrichtenauthentifizierungscode Protokoll \(CCMP\) implementiert den 802.11 i-Standard und ist für eine höhere Sicherheits Verschlüsselung als von WEP vorgesehen und verwendet 128-Bit-AES-Verschlüsselungsschlüssel.
2. **AES-\-gcmp**. Der "Galois Counter Mode"-Protokoll \(gcmp-\) der von 802.11 AC unterstützt wird, ist effizienter als AES\-CCMP und bietet eine bessere Leistung für drahtlose Clients. Gcmp verwendet 256-Bit-AES-Verschlüsselungsschlüssel.

> [!IMPORTANT]
> Datenschutz bei der Datenschutz \(WEP\) war der ursprüngliche Standard Sicherheitsstandard, der zum Verschlüsseln von Netzwerk Datenverkehr verwendet wurde. Sie sollten WEP nicht in Ihrem Netzwerk bereitstellen, da es in dieser veralteten Form der Sicherheit wohl\-bekannten Sicherheitsrisiken gibt.

### <a name="active-directorydoman-services-adds"></a>Active Directory domAD DS \(\)
In AD DS wird eine verteilte Datenbank bereitgestellt, in der Informationen zu Netzwerkressourcen und Anwendungs\-spezifischen Daten aus Verzeichnis\-aktivierten Anwendungen gespeichert und verwaltet werden. Administratoren können AD DS verwenden, um die Elemente eines Netzwerks (z. B. Benutzer, Computer und andere Geräte) in einer hierarchischen Struktur aus Einschlussbeziehungen zu organisieren. Die hierarchische Containment-Struktur umfasst die Active Directory Gesamtstruktur, Domänen in der Gesamtstruktur und Organisationseinheiten \(OUs\) in jeder Domäne. Ein Server, auf dem AD DS ausgeführt wird, wird als *Domänen Controller*bezeichnet.  

AD DS enthält die Benutzerkonten, Computer Konten und Konto Eigenschaften, die für IEEE 802.1 x und PEAP\-MS\-CHAP v2 erforderlich sind, um die Benutzer Anmelde Informationen zu authentifizieren und die Autorisierung für drahtlose Verbindungen auszuwerten.

### <a name="active-directory-users-and-computers"></a>Active Directory-Benutzer und -Computer
Active Directory Benutzer und Computer ist eine Komponente von AD DS, die Konten enthält, die physische Entitäten darstellen, z. b. einen Computer, eine Person oder eine Sicherheitsgruppe. Bei einer *Sicherheitsgruppe* handelt es sich um eine Sammlung von Benutzer-oder Computer Konten, die von Administratoren als einzelne Einheit verwaltet werden können. Benutzer-und Computer Konten, die einer bestimmten Gruppe angehören, werden als *Gruppenmitglieder*bezeichnet.  

### <a name="group-policy-management"></a>Gruppenrichtlinienverwaltung
Gruppenrichtlinie Management ermöglicht die Verzeichnis\-basierte Änderungs-und Konfigurations Verwaltung von Benutzer-und Computereinstellungen, einschließlich Sicherheits-und Benutzerinformationen. Mit Gruppenrichtlinie können Sie Konfigurationen für Gruppen von Benutzern und Computern definieren. Mit Gruppenrichtlinie können Sie Einstellungen für Registrierungseinträge, Sicherheit, Software Installation, Skripts, Ordner Umleitung, Remoteinstallations Dienste und Internet Explorer-Wartung angeben. Die Gruppenrichtlinie Einstellungen, die Sie erstellen, sind in einem Gruppenrichtlinie Objekt \(GPO-\)enthalten. Durch Zuordnen eines Gruppenrichtlinien Objekts zu ausgewählten Active Directory System Containern – Websites, Domänen und Organisationseinheiten – können Sie die Einstellungen des GPO auf die Benutzer und Computer in diesen Active Directory Containern anwenden. Zum Verwalten von Gruppenrichtlinie Objekten in einem Unternehmen können Sie die Gruppenrichtlinienverwaltungs-Editor Microsoft Management Console \(MMC-\)verwenden.  

Dieses Handbuch enthält ausführliche Anweisungen zum Angeben von Einstellungen im Drahtlos Netzwerk \(IEEE 802,11\) Richtlinien Erweiterung der Gruppenrichtlinie Verwaltung. Das Drahtlos Netzwerk \(IEEE 802,11\)-Richtlinien konfiguriert Domänen\-Mitglieds-drahtlos Client Computer mit den erforderlichen Konnektivitätseinstellungen und drahtlos Einstellungen für den drahtlos Zugriff mit 802.1 x-Authentifizierung.

### <a name="server-certificates"></a>Serverzertifikate
Dieses Bereitstellungs Szenario erfordert Server Zertifikate für jeden NPS, der die 802.1 x-Authentifizierung ausführt.  

Ein Serverzertifikat ist ein digitales Dokument, das häufig für die Authentifizierung und zum Sichern von Informationen in offenen Netzwerken verwendet wird. Ein Zertifikat verbindet einen öffentlichen Schlüssel sicher mit der Entität, die den entsprechenden privaten Schlüssel besitzt. Zertifikate werden von der ausstellenden Zertifizierungsstelle digital signiert und können für einen Benutzer, einen Computer oder einen Dienst ausgestellt werden.  

Eine Zertifizierungsstelle \(Zertifizierungsstelle\) ist eine Entität, die für die Einrichtung und bürgung von öffentlichen Schlüsseln zuständig ist, die zu Subjekten \(in der Regel Benutzer oder Computer\) oder anderen Zertifizierungsstellen gehören. Die Aktivitäten einer Zertifizierungsstelle können das Binden öffentlicher Schlüssel an Distinguished Names über signierte Zertifikate, das Verwalten von Zertifikat Seriennummern und das Sperren von Zertifikaten einschließen.  

Active Directory Zertifikat Dienste \(AD CS\) ist eine Server Rolle, die Zertifikate als Netzwerk Zertifizierungsstelle ausgibt. Eine AD CS-Zertifikat Infrastruktur, die auch als *Public Key-Infrastruktur \(PKI\)* bezeichnet wird, bietet anpassbare Dienste zum Ausstellen und Verwalten von Zertifikaten für das Unternehmen.

### <a name="eap-peap-and-peap-ms-chap-v2"></a>EAP, PEAP und PEAP\-MS\-CHAP v2
Das Extensible Authentication-Protokoll \(EAP-\) erweitert Punkt-\-auf\-Punkt Protokoll \(PPP\), indem zusätzliche Authentifizierungsmethoden zugelassen werden, die Anmelde Informationen und Informationsaustausch beliebiger Längen verwenden. Bei der EAP-Authentifizierung müssen der Netzwerk Zugriffs Client und der Authentifikator \(z. b. der NPS-\) denselben EAP-Typ unterstützen, damit eine erfolgreiche Authentifizierung erfolgen kann. Windows Server 2016 umfasst eine EAP-Infrastruktur, unterstützt zwei EAP-Typen sowie die Möglichkeit, EAP-Nachrichten an NPSS zu übergeben. Durch die Verwendung von EAP können Sie zusätzliche Authentifizierungs Schemas unterstützen, die als *EAP-Typen*bezeichnet werden. Folgende EAP-Typen werden von Windows Server 2016 unterstützt:  

- Transport Layer Security \(TLS-\)

- Microsoft Challenge Handshake Authentication-Protokollversion 2 \(MS\-CHAP v2\)

>[!IMPORTANT]
>Starke EAP-Typen \(z. b. solche, die auf Zertifikaten basieren,\) eine bessere Sicherheit vor Brute-\--Force-Angriffen, Wörterbuchangriffen und Kenn Wörtern mit Kenn Wörtern als auf Kenn Wörtern\-basierten Authentifizierungs Protokollen \(wie z. b. CHAP oder MS\-CHAP Version 1\).

Geschützter EAP-\(PEAP\) verwendet TLS zum Erstellen eines verschlüsselten Kanals zwischen einem authentifizier enden PEAP-Client, z. b. einem drahtlos Computer, und einem PEAP-Authentifikator, wie z. b. einem NPS-oder einem anderen RADIUS-Server. PEAP gibt keine Authentifizierungsmethode an, bietet jedoch zusätzliche Sicherheit für andere EAP-Authentifizierungsprotokolle \(z. b. EAP\-MS\-CHAP v2\), die über den von PEAP bereitgestellten TLS-verschlüsselten Kanal betrieben werden können. Die Zugriffsmethode für Clients, die über die folgenden Arten von Netzwerk Zugriffs Servern eine Verbindung mit dem Netzwerk Ihres Unternehmens herstellen, wird als Authentifizierungsmethode für den Zugriff auf Clients verwendet, die \(nass\):

- 802.1 x\-fähige drahtlos Zugriffspunkte

- 802.1 x\-fähige authentifizier Ende Switches

- Computer, auf denen Windows Server 2016 und der RAS-Dienst ausgeführt werden, \(RAS-\), die als virtuelles privates Netzwerk \(VPN\) Server, DirectAccess-Server oder beides konfiguriert sind.

- Computer, auf denen Windows Server 2016 und Remotedesktopdienste ausgeführt werden

PEAP\-MS\-CHAP v2 ist einfacher bereitzustellen als EAP\-TLS, da die Benutzerauthentifizierung mithilfe von Kennwort-\-basierten Anmelde Informationen \(Benutzername und Kennwort\)anstelle von Zertifikaten oder Smartcards ausgeführt wird. Es sind nur NPS-oder andere RADIUS-Server erforderlich, um ein Zertifikat zu erhalten. Das NPS-Zertifikat wird vom NPS während des Authentifizierungsprozesses verwendet, um seine Identität bei den Peer-Clients nachzuweisen.

Dieses Handbuch enthält Anweisungen zum Konfigurieren Ihrer drahtlosen Clients und ihrer NPS-\(s\) für die Verwendung von PAP\-MS\-CHAP v2 für authentifizierten 802.1 x-Zugriff.

### <a name="network-policy-server"></a>Netzwerkrichtlinienserver
Der Netzwerk Richtlinien Server \(NPS-\) ermöglicht das zentrale konfigurieren und Verwalten von Netzwerk Richtlinien mithilfe der Remote-Authentifizierungs\-in Benutzer Dienst \(RADIUS\) Server und RADIUS-Proxy. NPS ist erforderlich, wenn Sie den drahtlosen 802.1 x-Zugriff bereitstellen.

Wenn Sie Ihre 802.1 x-drahtlos Zugriffspunkte als RADIUS-Clients in NPS konfigurieren, verarbeitet NPS die von den APS gesendeten Verbindungsanforderungen. Während der Verarbeitung von Verbindungsanforderungen führt NPS die Authentifizierung und Autorisierung aus. Die Authentifizierung bestimmt, ob der Client gültige Anmelde Informationen angegeben hat. Wenn die NPS den anfordernden Client erfolgreich authentifiziert hat, ermittelt NPS, ob der Client autorisiert ist, die angeforderte Verbindung herzustellen, und die Verbindung wird entweder zugelassen oder verweigert. Dies wird im folgenden ausführlicher erläutert:

#### <a name="authentication"></a>Authentifizierung

Erfolgreiche gegenseitige Peer-\-MS\-CHAP v2-Authentifizierung besteht aus zwei Hauptteilen:

1.  Der Client authentifiziert den NPS.  In dieser Phase der gegenseitigen Authentifizierung sendet das NPS sein Serverzertifikat an den Client Computer, damit der Client die Identität des NPS mit dem Zertifikat überprüfen kann. Zum erfolgreichen Authentifizieren des NPS muss der Client Computer der Zertifizierungsstelle vertrauen, die das NPS-Zertifikat ausgestellt hat. Der Client vertraut dieser Zertifizierungsstelle, wenn das Zertifikat der Zertifizierungsstelle im Zertifikat Speicher für vertrauenswürdige Stamm Zertifizierungsstellen auf dem Client Computer vorhanden ist.

    Wenn Sie eine eigene private Zertifizierungsstelle bereitstellen, wird das Zertifizierungsstellen Zertifikat automatisch im Zertifikat Speicher Vertrauenswürdige Stamm Zertifizierungsstellen für den aktuellen Benutzer und für den lokalen Computer installiert, wenn Gruppenrichtlinie auf dem Domänen Mitglieds-Client Computer aktualisiert wird. Wenn Sie Server Zertifikate von einer öffentlichen Zertifizierungsstelle bereitstellen möchten, stellen Sie sicher, dass das Zertifikat der öffentlichen Zertifizierungsstelle bereits im Zertifikat Speicher Vertrauenswürdige Stamm Zertifizierungsstellen vorhanden ist.  

2.  Der Benutzer authentifiziert den Benutzer. Nachdem der Client die NPS erfolgreich authentifiziert hat, sendet der Client das Kennwort des Benutzers\-basierten Anmelde Informationen an den NPS, der die Anmelde Informationen des Benutzers für die Benutzerkonten Datenbank in Active Directory Dom\(-AD DS\)überprüft.

Wenn die Anmelde Informationen gültig sind und die Authentifizierung erfolgreich ist, startet die NPS die Autorisierungs Phase der Verarbeitung der Verbindungsanforderung. Wenn die Anmelde Informationen ungültig sind und die Authentifizierung fehlschlägt, sendet NPS eine Zugriffs Ablehnungs Meldung, und die Verbindungsanforderung wird verweigert.  

#### <a name="authorization"></a>Autorisierung

Der Server mit NPS führt wie folgt eine Autorisierung aus:  

1. NPS überprüft, ob die Benutzer-oder Computer Konto-\-in den Eigenschaften in AD DS. Jedes Benutzer-und Computer Konto in Active Directory Benutzer und Computer umfasst mehrere Eigenschaften, einschließlich derjenigen, die auf der Registerkarte " **Dial\-in** " gefunden werden. Wenn auf dieser Registerkarte unter **Netzwerk Zugriffsberechtigung**der Wert **Zugriff zulassen**angezeigt wird, ist der Benutzer oder Computer autorisiert, eine Verbindung mit dem Netzwerk herzustellen. Wenn der Wert " **Zugriff verweigern**" lautet, ist der Benutzer oder Computer nicht autorisiert, eine Verbindung mit dem Netzwerk herzustellen. Wenn der Wert **Zugriffs Steuerung über NPS-Netzwerk Richtlinie**lautet, wertet NPS die konfigurierten Netzwerk Richtlinien aus, um zu bestimmen, ob der Benutzer oder Computer autorisiert ist, eine Verbindung mit dem Netzwerk herzustellen. 

2. NPS verarbeitet dann seine Netzwerk Richtlinien, um eine Richtlinie zu suchen, die mit der Verbindungsanforderung übereinstimmt. Wenn eine abgleichsrichtlinie gefunden wird, wird die Verbindung von NPS basierend auf der Konfiguration der Richtlinie entweder erteilt oder verweigert.  

Wenn Authentifizierung und Autorisierung erfolgreich sind und die entsprechende Netzwerk Richtlinie Zugriff gewährt, gewährt NPS Zugriff auf das Netzwerk, und der Benutzer und der Computer können eine Verbindung mit Netzwerkressourcen herstellen, für die Sie über Berechtigungen verfügen.  

>[!NOTE]
>Zum Bereitstellen von drahtlos Zugriff müssen Sie NPS-Richtlinien konfigurieren. Dieses Handbuch enthält Anweisungen für die Verwendung des **Assistenten zum Konfigurieren von 802.1 x** in NPS zum Erstellen von NPS-Richtlinien für den drahtlos Zugriff mit 802.1 x-Authentifizierung.  

### <a name="bootstrap-profiles"></a>Bootstrap-profile
In 802.1 x\-authentifizierten Drahtlos Netzwerken müssen drahtlose Clients Sicherheits Anmelde Informationen bereitstellen, die von einem RADIUS-Server authentifiziert werden, um eine Verbindung mit dem Netzwerk herzustellen. Für geschützte EAP-\[PEAP-\]\-Microsoft Challenge Handshake Authentication-Protokollversion 2 \[MS\-CHAP v2\]sind die Sicherheits Anmelde Informationen ein Benutzername und ein Kennwort. Bei EAP\-Transport Layer Security \[TLS\] oder PEAP\-TLS sind die Sicherheits Anmelde Informationen Zertifikate, z. b. Client Benutzer-und Computer Zertifikate oder Smartcards.

Beim Herstellen einer Verbindung mit einem Netzwerk, das für die Durchführung von PEAP-\-MS\-CHAP v2, PEAP\-TLS oder EAP\-TLS-Authentifizierung konfiguriert ist, müssen die drahtlosen Windows-Clients standardmäßig auch ein Computer Zertifikat überprüfen, das vom RADIUS-Server gesendet wird. Das Computer Zertifikat, das vom RADIUS-Server für jede Authentifizierungs Sitzung gesendet wird, wird häufig als Serverzertifikat bezeichnet.

Wie bereits erwähnt, können Sie Ihre RADIUS-Server auf zwei Arten für Ihr Serverzertifikat ausgeben: von einer kommerziellen Zertifizierungsstelle \(z. b. VeriSign, Inc.,\)oder von einer privaten Zertifizierungsstelle, die Sie in Ihrem Netzwerk bereitstellen. Wenn der RADIUS-Server ein Computer Zertifikat sendet, das von einer kommerziellen Zertifizierungsstelle ausgestellt wurde, für die bereits ein Stamm Zertifikat im Zertifikat Speicher der vertrauenswürdigen Stamm Zertifizierungsstellen des Clients installiert wurde, kann der drahtlose Client die des RADIUS-Servers überprüfen. Computer Zertifikat, unabhängig davon, ob der drahtlose Client der Active Directory Domäne beigetreten ist. In diesem Fall kann der drahtlose Client eine Verbindung mit dem Drahtlos Netzwerk herstellen, und dann können Sie den Computer der Domäne hinzufügen.

>[!NOTE]
>Das Verhalten, das erfordert, dass der Client das Serverzertifikat überprüft, kann deaktiviert werden, aber die Deaktivierung der Serverzertifikat Überprüfung wird in Produktionsumgebungen nicht empfohlen.

Drahtlos Boots Trap Profile sind temporäre Profile, die so konfiguriert werden, dass Benutzer von drahtlosen Clients eine Verbindung mit dem 802.1 x\-authentifizierten Drahtlos Netzwerk herstellen können, bevor der Computer der Domäne hinzugefügt wird, und\/oder bevor der Benutzer sich zum ersten Mal erfolgreich bei der Domäne angemeldet hat.  In diesem Abschnitt wird das Problem zusammengefasst, das beim Versuch aufgetreten ist, einen drahtlosen Computer der Domäne hinzuzufügen, oder wenn ein Benutzer zum ersten Mal eine Domäne\-verknüpften drahtlos Computers verwendet, um sich bei der Domäne anzumelden.

Bei bereit Stellungen, bei denen der Benutzer oder IT-Administrator einen Computer nicht physisch mit dem verkabelten Ethernet-Netzwerk verbinden kann, um den Computer der Domäne hinzuzufügen, und auf dem Computer nicht das erforderliche ausstellende Stamm Zertifizierungsstellen-Zertifikat im Zertifikat Speicher der **vertrauenswürdigen Stamm Zertifizierungs** stellen installiert ist, können Sie drahtlose Clients mit einem temporären drahtlos Verbindungsprofil ( *Bootstrap-Profil*) konfigurieren, um

Ein *Bootstrap-Profil* entfernt die Anforderung, das Computer Zertifikat des RADIUS-Servers zu validieren. Diese temporäre Konfiguration ermöglicht dem drahtlosen Benutzer das Hinzufügen des Computers zur Domäne. zu diesem Zeitpunkt werden das Drahtlos Netzwerk \(IEEE 802,11\)-Richtlinien angewendet, und das entsprechende Zertifikat der Stamm Zertifizierungsstelle wird automatisch auf dem Computer installiert.

Wenn Gruppenrichtlinie angewendet wird, werden ein oder mehrere drahtlos Verbindungsprofile, die die Anforderung für die gegenseitige Authentifizierung erzwingen, auf den Computer angewendet. Das Bootstrap-Profil ist nicht mehr erforderlich und wird entfernt. Nachdem Sie den Computer der Domäne hinzufügen und den Computer neu gestartet haben, kann sich der Benutzer mit einer drahtlos Verbindung bei der Domäne anmelden.

Eine Übersicht über den Bereitstellungs Prozess für drahtlos Zugriffe mithilfe dieser Technologien finden Sie unter [Übersicht über die Bereitstellung von drahtlos Zugriff](b-wireless-access-deploy-overview.md).
