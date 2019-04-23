---
title: Bereitstellung des kennwortbasierten authentifizierten 802.1X-Funkzugriffs
description: Dieses Thema ist Teil des Windows Server 2016-Networking Guide "Deploy Password-Based 802.1 X Authenticated Wireless Access"
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: ff06ba23-9c0f-49ec-8f7b-611cf8d73a1b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f34580f4a0fd92c6f059d19d09a6926fc2775960
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840011"
---
# <a name="deploy-password-based-8021x-authenticated-wireless-access"></a>Bereitstellen von Kennwort\-basierten drahtlosen Zugriff mit 802.1X-Authentifizierung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dies ist ein Begleithandbuch zum Windows Server&reg; 2016 Core Network Guide. Das Handbuch zum-Hauptnetzwerk enthält Anweisungen zum Planen und die erforderlichen Komponenten für ein voll funktionsfähiges Netzwerk und eine neue Active-Domäne in einer neuen Gesamtstruktur bereitstellen.

Dieses Handbuch erläutert die Erstellung eines Hauptnetzwerks mithilfe von Anleitungen zum Bereitstellen von Institute of Electrical and Electronics Engineers \(IEEE\) 802.1 X\-authentifizierten IEEE 802.11 drahtlosen Zugriff mit Protected Extensible Authentication Protocol – Microsoft Challenge Handshake Authentication Protocol Version 2 \(PEAP\-MS\-CHAP-v2\).

Da PEAP\-MS\-CHAP v2 erfordert, dass Benutzer das Kennwort eingeben\-basierend Anmeldeinformationen, anstatt ein Zertifikat während der Authentifizierung, es ist in der Regel einfacher und kostengünstiger als EAPBereitstellen\-TLS oder PEAP\-TLS.

>[!NOTE]
>In diesem Handbuch IEEE 802.1 X Authenticated Wireless Access mit PEAP\-MS\-CHAP-v2 abgekürzt wird als "drahtlosen Zugriff" und "WLAN-Zugriff."

## <a name="about-this-guide"></a>Informationen zur Anleitung
Dieses Handbuch, in Kombination mit den erforderlichen Leitfäden, die unten beschriebenen enthält Anweisungen dazu, wie Sie die folgende WLAN-Infrastruktur bereitstellen.  

- Eine oder mehrere 802.1 X\-802.11 Drahtloszugriffspunkte \(APs\).

- Active Directory-Domänendienste \(AD DS\) -Benutzer und-Computer.

- Gruppenrichtlinienverwaltung

- Eine oder mehrere Netzwerkrichtlinienserver \(NPS\) Server.

- Serverzertifikate für Computer, auf denen NPS ausgeführt wird

- Drahtlose Windows-Clientcomputern&reg; 10, Windows 8.1 oder Windows 8.

### <a name="dependencies-for-this-guide"></a>Abhängigkeiten in diesem Handbuch

Zur erfolgreichen Bereitstellung authentifizierte drahtlose mit diesem Handbuch müssen Sie eine Umgebung zum Netzwerk und die Domäne mit allen erforderlichen Technologien bereitgestellt verfügen. Sie müssen auch Serverzertifikate, die bereitgestellt werden, um Ihre Authentifizierung NPSs verfügen.

Die folgenden Abschnitte enthalten Links zu Dokumentationen, das zeigt, wie diese Technologien bereitgestellt.

#### <a name="network-and-domain-environment-dependencies"></a>Netzwerk und die Domäne Umgebung-Abhängigkeiten

Dieses Handbuch richtet sich für die Netzwerk- und Systemadministratoren, die die Anweisungen in Windows Server 2016 ausgeführt haben **Core Network Guide** ein Hauptnetzwerk bereitstellen oder für diejenigen, die zuvor die kerntechnologien bereitgestellt haben in dem Kernnetzwerk möglich, einschließlich der AD DS, Domain Name System enthaltenen \(DNS\), Dynamic Host Configuration Protocol \(DHCP\), TCP\/IP, NPS und Windows Internet Name Service \(WINS\).  

Das Handbuch zum Hauptnetzwerk ist unter den folgenden Links verfügbar:

- Windows Server 2016 [Core Network Guide](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide) ist in der technischen Bibliothek zu Windows Server 2016 verfügbar. 

- Die [Core Network Guide](https://gallery.technet.microsoft.com/Core-Network-Guide-for-9da2e683) ist auch verfügbar im Word-Format im TechNet-Katalog auf [ https://gallery.technet.microsoft.com/Core-Network-Guide-for-9da2e683 ](https://gallery.technet.microsoft.com/Core-Network-Guide-for-9da2e683).

#### <a name="server-certificate-dependencies"></a>Server-Zertifikat-Abhängigkeiten
Es gibt zwei Optionen zur Verfügung, für die Registrierung Authentication-Server mit Serverzertifikate für die Verwendung mit 802.1X-Authentifizierung – deploy eigene public Key-Infrastruktur mithilfe von Active Directory Certificate Services \(AD CS\) oder Verwenden Sie Serverzertifikate, die von einer öffentlichen Zertifizierungsstelle registriert sind \(Zertifizierungsstelle\).

##### <a name="ad-cs"></a>AD CS
Netzwerk- und Systemadministratoren, die authentifizierte drahtlose Bereitstellung gelten die Anweisungen in der Windows Server 2016 Core Network Companion Guide **Bereitstellen von Serverzertifikaten für 802.1 X verkabelte oder kabellose 802.1X-Bereitstellungen**. Dieses Handbuch wird erläutert, wie zum Bereitstellen und Verwenden von AD CS auf Server-Zertifikate automatisch registrieren auf Computern, auf dem NPS ausgeführt wird.

Dieses Handbuch ist an folgendem Speicherort verfügbar.

- Windows Server 2016 Core Network Companion Guide [Bereitstellen von Serverzertifikaten für 802.1 X verkabelte und drahtlose Bereitstellungen](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments?f=255&MSPPError=-2147217396) im HTML-Format in der technischen Bibliothek. 

##### <a name="public-ca"></a>Öffentliche Zertifizierungsstelle
Serverzertifikate von einer öffentlichen Zertifizierungsstelle an, wie z. B. VeriSign, können Sie, dass die Clientcomputer bereits vertrauen erwerben. 

Ein Clientcomputer vertraut eine Zertifizierungsstelle, wenn das CA-Zertifikat im Zertifikatspeicher vertrauenswürdige Stammzertifizierungsstellen installiert ist. Standardmäßig verfügen die Computer mit Windows mehrere öffentliche Zertifizierungsstellenzertifikate installiert deren vertrauenswürdige Stammzertifizierungsstellen-Zertifikat zu speichern.  

Sie sollten die Entwurfs- und Bereitstellungshandbücher für jede der Technologien einsehen, die in diesem Bereitstellungsszenario verwendet werden. Diese Handbücher können Ihnen helfen, zu bestimmen, ob dieses Bereitstellungsszenario die Dienste und Konfigurationen bietet, die Sie zur Organisation des Netzwerks benötigen.

### <a name="requirements"></a>Anforderungen
Es folgen die Anforderungen für die Bereitstellung einer Infrastruktur für drahtlosen Zugriff mithilfe eines Szenarios in diesem Handbuch dokumentiert:

- Vor der Bereitstellung dieses Szenarios, müssen Sie zuerst 802.1 X erwerben\-funkzugriffspunkte, drahtlose Konnektivität am gewünschten Standort an Ihrem Standort zu gewährleisten. Im Planungsabschnitt dieses Handbuchs hilft bei der Bestimmung der Features, die die Zugriffspunkte unterstützen müssen.

- Active Directory-Domänendienste \(AD DS\) installiert ist, da die anderen erforderlichen Netzwerk-Technologien sind gemäß der Anleitung in der Windows Server 2016 Core Network Guide.  

- AD CS bereitgestellt wird, und Serverzertifikate, NPSs registriert sind. Diese Zertifikate sind erforderlich, wenn Sie die PEAP bereitstellen\-MS\-CHAP-v2-Zertifikat\-basierend Authentifizierungsmethode, die in diesem Handbuch verwendet wird.

- Ein Mitglied Ihrer Organisation ist vertraut, mit den IEEE 802.11-Standards, die unterstützt werden, indem Sie Ihre drahtlosen Zugriffspunkte und dem drahtlosen Netzwerkadaptern, die in der Client-Computern und Geräten in Ihrem Netzwerk installiert sind. Beispielsweise ist eine Person in Ihrer Organisation mit Radio Frequency, Funkübertragung Typen 802.11 drahtlose Authentifizierung vertraut \(WPA2 oder WPA\), und Verschlüsselungen \(AES oder TKIP\).

## <a name="what-this-guide-does-not-provide"></a>Nicht in diesem Handbuch enthaltene Informationen  
Es folgen einige Elemente, die dieser Anleitung nicht bietet:

### <a name="comprehensive-guidance-for-selecting-8021x-capable-wireless-access-points"></a>Ausführliche Anleitungen für die Auswahl von 802.1 X\-funkzugriffspunkte

Da viele zwischen Marken und Modelle von 802.1 X Unterschiede\-fähigen Drahtloszugriffspunkten, dieses Handbuch bietet keine detaillierte Informationen zu:  

- Bestimmen, welche Marke oder Ihr Modell der Drahtloszugriffspunkt am besten geeignet ist, die an Ihre Anforderungen geeignet ist.

- Die physische Bereitstellung von drahtlosen Zugriffspunkten in Ihrem Netzwerk.

- In einem erweiterten drahtlosen AP-Konfiguration, z. B. für drahtlose virtuelle lokale Netzwerke \(VLANs\).

- Anweisungen zum Konfigurieren der Hersteller\-bestimmte Attribute auf dem Netzwerkrichtlinienserver.

Darüber hinaus Terminologie und Namen für die Einstellungen zwischen dem drahtlosen AP-Marken und Modelle variieren und entsprechen möglicherweise nicht die generische Einstellungsnamen, die in diesem Handbuch verwendet werden. Drahtlose AP Details zur Konfiguration müssen Sie die Produktdokumentation des Herstellers der Ihre drahtlosen Zugriffspunkte überprüfen.

### <a name="instructions-for-deploying-nps-certificates"></a>Anweisungen zum Bereitstellen von NPS-Zertifikate
  
Es gibt zwei Möglichkeiten zum Bereitstellen von NPS-Zertifikaten. Dieses Handbuch bietet keine umfassende Anleitungen, die Ihnen helfen zu bestimmen, welche Alternative Ihren Anforderungen am besten erfüllt. Im Allgemeinen sind jedoch die Optionen, die auftreten:

- Erwerben Zertifikate von einer öffentlichen Zertifizierungsstelle an, wie z. B. VeriSign, sind bereits vertrauen von Windows\-basierten Clients. Diese Option ist für kleinere Netzwerke in der Regel empfohlen.

- Bereitstellen einer Public Key-Infrastruktur \(PKI\) in Ihrem Netzwerk mithilfe von AD CS. Dies wird empfohlen, für die meisten Netzwerke, und die Anweisungen zum Bereitstellen von Serverzertifikaten mit AD CS finden Sie im zuvor erwähnten Deployment Guide.

### <a name="nps-network-policies-and-other-nps-settings"></a>Richtlinien für NPS-Netzwerke und andere NPS-Einstellungen

Mit Ausnahme der Konfigurationseinstellungen vorgenommen werden, wenn Sie ausführen, die **konfigurieren 802.1 X** -Assistenten wie in diesem Handbuch dokumentiert, dieses Handbuch bietet keine detaillierte Informationen zum manuellen Konfigurieren von NPS-Bedingungen, Einschränkungen oder andere NPS Einstellungen.

### <a name="dhcp"></a>DHCP

In diesem Bereitstellungshandbuch bietet keine Informationen zu entwerfen oder DHCP-Subnetze für drahtlose LANs bereitgestellt.

## <a name="technology-overviews"></a>Technologieübersicht
Technologieübersicht für die Bereitstellung von drahtlosen Zugriff "folgen":

### <a name="ieee-8021x"></a>IEEE 802.1X
Der Standard IEEE 802.1 X definiert, den Port\--basierte Netzwerk-Zugriffssteuerung, die verwendet wird, einen authentifizierten Netzwerkzugriff auf Ethernet-Netzwerke ermöglichen. Dieser Port\-basierend Netzwerkzugriffssteuerung verwendet die physischen Merkmale der switched-LAN-Infrastruktur zum Authentifizieren von Geräten, die mit einem LAN-Anschluss verbunden. Der Zugriff auf den Port kann verweigert werden, wenn der Authentifizierungsvorgang fehlschlägt. Obwohl dieser Standard für verdrahtete Ethernetnetzwerke entwickelt wurde, war es für die Verwendung für drahtlose 802.11-LANs angepasst.

### <a name="8021x-capable-wireless-access-points-aps"></a>802.1 X\-funkzugriffspunkte \(APs\)
Dieses Szenario erfordert die Bereitstellung eine oder mehrere 802.1X-fähige\-fähigen Drahtloszugriffspunkten, die mit dem Remote Authentication Dial kompatibel sind\-In User Service \(RADIUS\) Protokoll.

802.1 X und RADIUS-\-kompatibel APs, bei der Bereitstellung in einer RADIUS-Infrastruktur mit einem RADIUS-Server wie z. B. einem NPS heißen *RADIUS-Clients*.

### <a name="wireless-clients"></a>Drahtlose clients
Dieses Handbuch bietet umfassende Konfigurationsdetails für Domäne Zugriff mit 802.1X-Authentifizierung bereitstellen\-Member-Benutzer, die mit dem drahtlosen Client-Computern, die unter Windows 10, Windows 8.1 und Windows 8 mit dem Netzwerk verbinden. Computer müssen mit der Domäne angehören, damit authentifizierten Zugriff erfolgreich herstellen.

>[!NOTE]
>Sie können auch Computer, auf denen Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 als drahtlose Clients ausgeführt werden.

### <a name="support-for-ieee-80211-standards"></a>Unterstützung für IEEE 802.11-Standards
Unterstützt Windows und Windows Server-Betriebssysteme bieten erstellt\-in der Unterstützung für 802.11 drahtlose Netzwerke. In diesen Betriebssystemen wird Sie einer installierten 802.11 Drahtlosnetzwerkadapter als eine drahtlose Netzwerkverbindung im Netzwerk- und Freigabecenter angezeigt. 

Obwohl es basiert\-in der Unterstützung für drahtlose 802.11-Netzwerke, die drahtlosen Komponenten von Windows sind, hängt von folgenden:

- Die Funktionen des drahtlosen Netzwerkadapters. Die w-LAN oder Standards für Sicherheit bei drahtlosen Verbindungen, die erforderlich sind, muss der installierten Drahtlosnetzwerkadapter unterstützen. Angenommen, der Drahtlosnetzwerkadapter WLAN nicht unterstützt\--Fi Protected Access \(WPA\), Sie können nicht aktiviert oder WPA-Sicherheitsoptionen konfigurieren.

- Die Funktionen der Treiber des drahtlosen Netzwerkadapters. Damit Sie so konfigurieren Sie Optionen für drahtlose Netzwerke können, muss der Treiber für den Drahtlosnetzwerkadapter unterstützen die berichterstellung für alle seine Funktionen zu Windows. Stellen Sie sicher, dass der Treiber für Ihre drahtlosen Netzwerkadapter für die Funktionen des Betriebssystems geschrieben wird. Stellen Sie außerdem sicher, dass der Treiber die aktuelle Version ist, anhand von Microsoft Update oder die Website des Herstellers, drahtlose Netzwerkadapter.

Die folgende Tabelle zeigt die Übertragungsraten und die Häufigkeit von allgemeinen drahtlosen IEEE 802.11-Standards.

|Standards|Frequenzen|Übertragung von Bitraten|Verwendung|
|-------------|---------------|--------------------------|---------|  
|802.11|S\--Band-Industrie, Wissenschaft und Medical \(ISM\) Frequenzbereich \(2.4, 2.5 GHz\)|2 Mbit / s \(Mbit/s\)|Veraltet. Nicht häufig verwendet wird.|  
|802.11b|S\---Band-ISM|11 Mbit/s|Häufig verwendet.|  
|802.11a|C\---Band-ISM \(5,725 zu 5.875 GHz\)|54 Mbit/s|Aufgrund der Kosten und Mühen sparen begrenzten Bereich verwendet nicht häufig.|  
|802.11g|S\---Band-ISM|54 Mbit/s|Häufig verwendet. 802. 11 g-Geräte sind kompatibel mit 802. 11 b Geräte.|  
|802. 11n \2.4 und 5.0 GHz|C\--Band- und S\---Band-ISM|250 Mbit/s|Geräte auf Grundlage des präproduktionsclients\-Ratifizierung IEEE 802. 11n standard wurde im August 2007 verfügbar. Viele 802. 11n Geräte sind kompatibel mit 802. 11a, b und g-Geräte.|
|802.11ac |5 GHz |6,93 Gbit/s |802. 11ac, vom IEEE im Jahr 2014 genehmigt ist, Skalierbarkeit und schneller als die 802. 11n und bereitgestellt wird, in denen APs und drahtlosen Clients ihn unterstützen.|

### <a name="wireless-network-security-methods"></a>Drahtlosnetzwerk-Sicherheitsmethoden
**Wireless-Netzwerks Sicherheitsmethoden** ist eine informelle Gruppierung der Drahtlosauthentifizierung \(manchmal als drahtlose Sicherheit bezeichnet\) und wireless-sicherheitsverschlüsselung. Drahtlose Authentifizierung und Verschlüsselung werden paarweise drahtlose Übertragungen zu schützen und um zu verhindern, dass nicht autorisierte Benutzer Zugriff auf das drahtlose Netzwerk verwendet werden. 

Wenn Sie drahtlos-Sicherheitseinstellungen in der drahtlosen Netzwerk Richtlinien von der Gruppenrichtlinie konfigurieren, stehen mehrere Kombinationen zur Auswahl. Allerdings nur die WPA2\-Enterprise, WPA\-Enterprise und Öffnen mit 802.1 X Authentifizierungsstandards für 802.1 X authentifizierte drahtlose Bereitstellungen unterstützt werden.

>[!NOTE]
>Beim Konfigurieren der Wireless Network Policies, Sie müssen auswählen, **WPA2\-Enterprise**, **WPA\-Enterprise**, oder **offen bei 802.1 X** in Reihenfolge für den Zugriff auf die EAP-Einstellungen, die für 802.1 X benötigt werden authentifizierte drahtlose Bereitstellungen.  

#### <a name="wireless-authentication"></a>Drahtlose Authentifizierung
Dieses Handbuch empfiehlt, dass die Verwendung der folgenden Drahtlosauthentifizierung Standards für 802.1X-authentifizierte drahtlose Bereitstellungen authentifiziert.  

**WLAN\--Fi Protected Access – Enterprise \(WPA\-Enterprise\)**  WPA ist eine vorläufige Norm, die die WiFi-Alliance zur Einhaltung des Protokolls 802.11 drahtlose Sicherheit entwickelt. Die WPA-Protokoll wurde entwickelt, als Reaktion auf eine Anzahl von schweren Fehlern, die in der vorherigen Wired Equivalent Privacy ermittelt wurden \(WEP\) Protokoll.

WPA\-Enterprise bietet verbesserte Sicherheit für WEP durch:  

1. Eine Authentifizierung erforderlich, die 802.1X-Authentifizierung X EAP-Framework als Teil der Infrastruktur verwendet, die zentralisierte gegenseitige Authentifizierung und dynamischer schlüsselverwaltung gewährleistet  

2. Erweitern die Integrität überprüfen Wert \(ICV\) mit einem Message Integrity Check \(MIC\), um die Header und Nutzlast zu schützen  

3. Implementieren einen Framezähler, um Replay-Angriffe zu verhindern.  

**WLAN\-Fi Protected Access 2 – Enterprise \(WPA2\-Enterprise\)**  wie WPA\-WPA2-Enterprise Standard\-Unternehmen verwendet werden, die 802.1 X und EAP-Framework. WPA2\-Enterprise bietet eine stärkere Schutz von Daten für mehrere Benutzer und große verwaltete Netzwerke. WPA2\-Enterprise ist eine stabile Protokoll, die entwickelt wird, um nicht autorisierten Netzwerkzugriff zu verhindern, indem Sie Benutzer über einen Authentication-Server im Netzwerk überprüfen.  

#### <a name="wireless-security-encryption"></a>Sicherheit bei drahtlosen Verbindungen Verschlüsselung
Sicherheit bei drahtlosen Verbindungen-Verschlüsselung wird verwendet, um die drahtlosen Übertragungen zu schützen, die zwischen dem drahtlosen Client und dem drahtlosen AP gesendet werden. Sicherheit bei drahtlosen Verbindungen Verschlüsselung wird in Verbindung mit der ausgewählten Netzwerkauthentifizierungsmethode für Sicherheit verwendet. Standardmäßig von Computern unter Windows 10, Windows 8.1 und Windows 8 unterstützt zwei Verschlüsselungsstandards:

1. **Temporal Key Integrity Protocol** \(TKIP\) ist ein ältere Verschlüsselungsprotokoll, das Bereitstellen sicherer drahtlose Verschlüsselung als die von der Natur aus unsicher, Wired Equivalent Privacy bereitgestellten wurde ursprünglich entworfen wurde \(WEP\) Protokoll. TKIP wurde entwickelt, durch die IEEE 802. 11i task-Gruppe und die Wi\-Fi-Allianz WEP zu ersetzen, ohne dass die Ersetzung des ältere Hardware. TKIP ist eine Sammlung von Algorithmen, die die WEP-Nutzlast kapselt, und ermöglicht Benutzern von Altgeräten WiFi auf TKIP zu aktualisieren, ohne den Austausch von Hardware. Wie bei WEP verwendet TKIP den Verschlüsselungsalgorithmus RC4 Stream als Grundlage. Das neue Protokoll, jedoch jedem Datenpaket verschlüsselt, mit einem eindeutigen Schlüssel und die Schlüssel sind wesentlich sicherer als die von WEP. TKIP ist, zwar nützlich für die Aktualisierung der Sicherheit bei älteren Geräten, die entwickelt wurden, verwenden Sie nur WEP es befasst sich alle Sicherheitsprobleme in drahtlosen LANs nicht, und in den meisten Fällen nicht aussagekräftig ist, um vertrauliche Government "oder" Unternehmensdaten zu schützen Übertragungen.  

2. **Advanced Encryption Standard** \(AES\) ist das bevorzugte Verschlüsselungsprotokoll für die Verschlüsselung von Daten von Unternehmen und Behörden. AES bietet eine höhere Sicherheit bei der drahtlosen Übertragung als entweder TKIP oder WEP. Im Gegensatz zu TKIP und WEP erfordert AES drahtlose Hardware, die den AES-Standard unterstützt. AES ist ein symmetrischer\-Schlüsselverschlüsselung standard, der drei Blockchiffren, AES verwendet\-128, AES\-192 und AES\-256.

In Windows Server 2016 die folgenden AES\-drahtlose Verschlüsselung auf Basis von Methoden sind für die Konfiguration im Drahtlosprofil Eigenschaften verfügbar, bei der Auswahl einer Authentifizierungsmethode von WPA2\-Enterprise, was empfohlen wird.

1. **AES\-CCMP**. Leistungsindikator-Modus Cipher Block Chaining Message Authentication Code Protocol \(CCMP\) implementiert die 802. 11i-standard ist für das höher als die WEP-sicherheitsverschlüsselung und 128-Bit-AES-Verschlüsselungsschlüsseln verwendet.
2. **AES\-GCMP**. Galois Counter Mode-Protokoll \(GCMP\) wird durch 802. 11ac unterstützt, ist effizienter als AES\-CCMP und bietet eine bessere Leistung bei drahtlosen Clients. GCMP verwendet 256-Bit-AES-Verschlüsselungsschlüsseln.

> [!IMPORTANT]
> Wired Equivalent Privacy \(WEP\) wurde von der ursprünglichen Standard Sicherheit bei drahtlosen Verbindungen, die zur Verschlüsselung des Netzwerkverkehrs verwendet wurde. Sie sollten nicht WEP in Ihrem Netzwerk bereitstellen, da es auch gibt\-bekannte Schwachstellen dieser veralteten Art von Sicherheit.

### <a name="active-directorydoman-services-adds"></a>Active Directory-Domänendienste \(AD DS\)
AD DS bietet eine verteilte Datenbank, die Informationen zu Netzwerkressourcen und die Anwendung gespeichert und verwaltet\-bestimmte Daten aus dem Verzeichnis\-Anwendungen aktiviert. Administratoren können AD DS verwenden, um die Elemente eines Netzwerks (z. B. Benutzer, Computer und andere Geräte) in einer hierarchischen Struktur aus Einschlussbeziehungen zu organisieren. Diese hierarchische Struktur umfasst die Active Directory-Gesamtstruktur, Domänen in der Gesamtstruktur sowie die Organisationseinheiten \(Organisationseinheiten\) in jeder Domäne. Ein Server mit AD DS wird aufgerufen, eine *Domänencontroller*.  

AD DS enthält die Benutzerkonten, Computerkonten und Eigenschaften, die durch IEEE 802.1 X und PEAP erforderlich sind\-MS\-CHAP-v2 zum Authentifizieren der Anmeldeinformationen des Benutzers und Autorisierung für drahtlose Verbindungen zu bewerten.

### <a name="active-directory-users-and-computers"></a>Active Directory-Benutzer und-Computer
Active Directory-Benutzer und-Computer ist eine Komponente von AD DS mit Konten, die physische Entitäten, z. B. ein Computer, eine Person oder einer Sicherheitsgruppe darzustellen. Ein *Sicherheitsgruppe* ist eine Sammlung von Benutzer- oder Computerkonten, die Administratoren als einzelne Einheit verwaltet werden können. Benutzer- und Computerkonten, die einer bestimmten Gruppe angehören, werden als bezeichnet *Gruppenmitglieder*.  

### <a name="group-policy-management"></a>Gruppenrichtlinienverwaltung
Der Gruppenrichtlinienverwaltung ermöglicht Directory\-Änderungs- und Verwaltung von Benutzer- und computereinstellungen, einschließlich Informationen zu Sicherheit und Benutzer. Sie verwenden Gruppenrichtlinien, um Konfigurationen für Gruppen von Benutzern und Computern zu definieren. Mit der Gruppenrichtlinie können Sie Einstellungen für die Registrierungseinträge, Sicherheit, Softwareinstallation, Skripts, ordnerumleitung, Remoteinstallationsdienste und Internet Explorer-Wartung angeben. Die gruppenrichtlinieneinstellungen, die Sie erstellen, befinden sich in einem Group Policy Object \(GPO\). Durch Verknüpfen eines Gruppenrichtlinienobjekts mit ausgewählten Active Directory-System-Container, Sites, Domänen und Organisationseinheiten: Sie können die Einstellungen des Gruppenrichtlinienobjekts anwenden, um die Benutzer und Computer in dieser Active Directory-Container. Zum Verwalten der Gruppenrichtlinienobjekte in einem Unternehmen können Sie die Gruppenrichtlinienverwaltungs-Editor-Microsoft Management Console \(MMC\).  

Dieses Handbuch enthält ausführliche Anweisungen zum Angeben von Einstellungen im Funknetzwerk \(IEEE 802.11\) richtlinienerweiterung der Gruppenrichtlinien-Verwaltungskonsole. Das Drahtlosnetzwerk \(IEEE 802.11\) Domäne zum Konfigurieren von Richtlinien\-Member Drahtlosclientcomputer mit der Konnektivität und drahtlose Einstellungen für 802.1 X-Drahtloszugriff.

### <a name="server-certificates"></a>Serverzertifikate
Dieses Bereitstellungsszenario sind Serverzertifikate für jeden NPS, die 802.1X-Authentifizierung erforderlich.  

Ein Serverzertifikat ist ein digitales Dokument, das häufig zur Authentifizierung und zum sicheren Informationen in offenen Netzwerken verwendet wird. Ein Zertifikat verbindet einen öffentlichen Schlüssel sicher mit der Entität, die den entsprechenden privaten Schlüssel besitzt. Zertifikate werden von der ausstellenden Zertifizierungsstelle digital signiert, und sie können für einen Benutzer, einen Computer oder einen Dienst ausgestellt werden.  

Eine Zertifizierungsstelle \(Zertifizierungsstelle\) ist eine Entität verantwortlich für das Einrichten und zum Bestätigen der Authentizität öffentlicher Schlüssel, die zu den Themen gehören \(normalerweise Benutzern oder Computern\) oder anderen Zertifizierungsstellen. Aktivitäten von einer Zertifizierungsstelle umfassen das Binden von öffentlichen Schlüssel an distinguished Names über signierte Zertifikate, die Verwaltung von Seriennummern von Zertifikaten und Sperren von Zertifikaten.  

Active Directory-Zertifikatdienste \(AD CS\) ist eine Serverrolle, die Zertifikate als netzwerkzertifizierungsstelle ausstellt. Eine AD CS-Infrastruktur, auch bekannt als Zertifikat eine *public Key-Infrastruktur \(PKI\)*, anpassbare Dienste zum Ausstellen und Verwalten von Zertifikaten für das Unternehmen bietet.

### <a name="eap-peap-and-peap-ms-chap-v2"></a>EAP, PEAP und PEAP\-MS\-CHAP-v2
Extensible Authentication-Protokoll \(EAP\) Punkt erweitert\-zu\-Point-Protokoll \(PPP\) , Weitere Authentifizierungsmethoden, die Anmeldeinformationen und Informationen mit zulässt zufälliger Länge ausgetauscht. Mit EAP-Authentifizierung, sowohl im Netzwerk zugreifen, Client und dem Authentifikator \(wie z. B. den NPS\) muss den gleichen EAP-Typ für eine erfolgreiche Authentifizierung erfolgen unterstützen. Windows Server 2016 schließt eine EAP-Infrastruktur, unterstützt zwei EAP-Typen und die Möglichkeit, EAP-Nachrichten, NPSs übergeben. Unter Verwendung von EAP unterstützen Sie zusätzliche Authentifizierungsschemen, bekannt als *EAP-Typen*. Die EAP-Typen, die durch Windows Server 2016 unterstützt werden:  

- Transport Layer Security \(TLS\)

- Microsoft Challenge Handshake Authentication Protocol Version 2 \(MS\-CHAP-v2\)

>[!IMPORTANT]
>Sichere EAP-Typen \(wie jene, die auf Zertifikate basieren\) bieten einen besseren Schutz gegen Brute\-Erzwingen von Angriffen, Wörterbuchangriffen und das Kennwort erraten Angriffe als Kennwort\-basierend Authentifizierungsprotokolle \(wie CHAP oder MS\-CHAP, Version 1\).

Geschütztes EAP \(PEAP\) verwendet TLS, um einen verschlüsselten Kanal zwischen einem authentifizierenden PEAP-Client, z. B. einen Drahtloscomputer und PEAP-Authentifizierer, z. B. einem NPS oder andere RADIUS-Server zu erstellen. PEAP gibt keine Authentifizierungsmethode, aber es bietet zusätzliche Sicherheit für andere Authentifizierungsprotokolle EAP \(wie EAP\-MS\-CHAP-v2\) arbeiten können über den verschlüsselten TLS-Kanal durch den PEAP bereitgestellt. PEAP dient als Authentifizierungsmethode für Access-Clients, die mit dem Unternehmensnetzwerk über die folgenden Typen von Netzwerkzugriffsservern verbinden \(NAS\):

- 802.1 X\-funkzugriffspunkte

- 802.1 X\-kann authentifizierenden Switches

- Computer unter Windows Server 2016 und den RAS-Dienst \(RAS\) , der als virtuelles privates Netzwerk konfiguriert sind \(VPN\) -Server, DirectAccess-Server oder beides

- Computer unter Windows Server 2016 und Remote Desktop Services

PEAP\-MS\-CHAP v2 ist einfacher, als EAP bereitzustellen\-TLS da Benutzerauthentifizierung ausgeführt wird, indem Sie Kennwort\-basierende Anmeldeinformationen \(des Benutzernamens und Kennworts\), anstelle von Zertifikaten oder Smartcards. Nur NPS oder andere RADIUS-Server sind erforderlich, um ein Zertifikat zu erhalten. Der NPS-Zertifikat wird von den NPS während der Authentifizierung verwendet, seine Identität gegenüber PEAP-Clients nach.

Dieses Handbuch enthält Anweisungen zum Konfigurieren von Ihrem drahtlosen Clients und den NPS\(s\) mit PEAP\-MS\-CHAP-v2 für 802.1 X authentifizierter Zugriff.

### <a name="network-policy-server"></a>Netzwerkrichtlinienserver
Netzwerkrichtlinienserver \(NPS\) können Sie zentral konfigurieren und Verwalten von Richtlinien für Netzwerke mit Remote Authentication Dial\-In User Service \(RADIUS\) Server- und RADIUS-Proxy. NPS ist erforderlich, wenn Sie den drahtlosen Zugriff mit 802.1X-Authentifizierung bereitstellen.

Wenn Sie Ihre 802.1 X drahtlose Zugriffspunkte als RADIUS-Clients in NPS konfigurieren, verarbeitet NPS verbindungsanforderungen von APs gesendet werden. Während der anforderungsverarbeitung für Verbindung führt NPS, Authentifizierung und Autorisierung. Die Authentifizierung bestimmt, ob der Client gültige Anmeldeinformationen verfügt. Wenn der NPS den anfordernden Client erfolgreich authentifiziert hat, bestimmt NPS, ob der Client autorisiert ist, um die angeforderten Verbindung herzustellen, und entweder zulässt oder verweigert Sie die Verbindung. Dies wird wie folgt ausführlicher erläutert:

#### <a name="authentication"></a>Authentifizierung

Erfolgreiche gegenseitige PEAP\-MS\-CHAP-v2-Authentifizierung besteht aus zwei Hauptkomponenten:

1.  Der Client authentifiziert den NPS.  Während dieser Phase der gegenseitigen Authentifizierung sendet der NPS das Serverzertifikat auf dem Clientcomputer an, damit der Client NPSs-Identität mit dem Zertifikat überprüfen kann. Um den NPS erfolgreich authentifizieren zu können, muss der Client-Computer der Zertifizierungsstelle vertrauen, die das NPS-Zertifikat ausgestellt hat. Der Client vertraut diese Zertifizierungsstelle aus, wenn der ZS-Zertifikat im Zertifikatspeicher vertrauenswürdige Stammzertifizierungsstellen auf dem Clientcomputer vorhanden ist.

    Wenn Sie Ihre eigenen private Zertifizierungsstelle bereitstellen, wird das ZS-Zertifikat automatisch im Zertifikatspeicher vertrauenswürdige Stammzertifizierungsstellen für den aktuellen Benutzer und für den lokalen Computer installiert, wenn Gruppenrichtlinien, auf dem Client Domänenmitgliedscomputer aktualisiert wird. Wenn Sie Serverzertifikate von einer öffentlichen Zertifizierungsstelle bereitstellen möchten, stellen Sie sicher, dass das öffentliche Zertifikat der Zertifizierungsstelle bereits im Zertifikatspeicher vertrauenswürdiger Stammzertifizierungsstellen stammen.  

2.  Der NPS authentifiziert den Benutzer. Nachdem der Client den NPS erfolgreich authentifiziert hat, wird der Client sendet das Kennwort des Benutzers\-basierende Anmeldeinformationen an den NPS, der überprüft, die Anmeldeinformationen des Benutzers für die Benutzerdatenbank für die Konten in Active Directory-Domänendienste ob \(AD DS\).

Wenn die Anmeldeinformationen gültig sind und die Authentifizierung erfolgreich ist, beginnt der NPS der Autorisierungsphase der anforderungsverarbeitung Verbindung an. Wenn die Anmeldeinformationen ungültig sind und schlägt die Authentifizierung fehl, NPS sendet eine Nachricht zum Ablehnen von Zugriff und die verbindungsanforderung wird verweigert.  

#### <a name="authorization"></a>Autorisierung

Der Server mit NPS führt die Autorisierung wie folgt:  

1. NPS überprüft, ob Einschränkungen in der Benutzer oder Computer Konto Drehknopf\-in Eigenschaften in AD DS. Alle Benutzer- und Computerkonto in Active Directory-Benutzer und-Computer umfasst mehrere Eigenschaften, einschließlich finden Sie auf die **Dial\-in** Registerkarte. Auf dieser Registerkarte im **Netzwerk Zugriffsberechtigung**, wenn der Wert ist **zulassen des Zugriffs**, ist der Benutzer oder Computer autorisiert, eine Verbindung mit dem Netzwerk herstellen. Wenn der Wert ist **Verweigern des Zugriffs**, den Benutzer oder Computer ist nicht autorisiert, eine Verbindung mit dem Netzwerk herstellen. Wenn der Wert ist **steuern den Zugriff über die Netzwerkrichtlinie für NPS**, NPS ausgewertet wird, die konfigurierten Netzwerkrichtlinien, um zu bestimmen, ob der Benutzer oder Computer autorisiert ist, eine Verbindung mit dem Netzwerk herstellen. 

2. NPS verarbeitet dann die Netzwerkrichtlinien, um eine Richtlinie zu finden, die die verbindungsanforderung entspricht. Wenn eine passende Richtlinie gefunden wird, NPS gewährt oder verweigert die Verbindung aufgrund von Konfiguration, der Richtlinie.  

Wenn Authentifizierung und Autorisierung erfolgreich sind, und die entsprechenden Netzwerkrichtlinie Zugriff gewährt, NPS erhalten Sie Zugriff auf das Netzwerk, und Benutzer und Computer können auf Netzwerkressourcen, die für die sie Berechtigungen haben eine Verbindung herstellen.  

>[!NOTE]
>Zum drahtlosen Zugriff bereitstellen, müssen Sie die NPS-Richtlinien konfigurieren. Dieses Handbuch enthält Anweisungen zur Verwendung der **konfigurieren 802.1 X-Assistenten** in NPS, um NPS-Richtlinien für drahtlosen Zugriff 802.1X-authentifizierte zu erstellen.  

### <a name="bootstrap-profiles"></a>Bootstrap-Profile
802.1 X\-authentifizierte drahtlose Netzwerke, drahtlose Clients müssen die Sicherheitsanmeldeinformationen, die von einem RADIUS-Server authentifiziert werden, um mit dem Netzwerk verbinden angeben. Für geschütztes EAP \[PEAP\]\-Microsoft Challenge Handshake Authentication Protocol Version 2 \[MS\-CHAP-v2\], die Anmeldeinformationen sind, einen Benutzernamen und Kennwort. Für EAP\-Transport Layer Security \[TLS\] oder PEAP\-TLS, die Anmeldeinformationen sind Zertifikate, z. B. Benutzer- und Client-Zertifikaten oder Smartcards.

Um eine Verbindung mit einem Netzwerk herstellt, der zum Durchführen von PEAP konfiguriert ist\-MS\-CHAPv2 PEAP\-TLS oder EAP\-standardmäßig Windows drahtlosen Clients müssen außerdem ein Computerzertifikat, das Überprüfen der TLS-Authentifizierung gesendet vom RADIUS-Server. Das Zertifikat des Computers, das für jede authentifizierungssitzung vom RADIUS-Server gesendet wird, wird häufig als ein Serverzertifikat bezeichnet.

Wie bereits erwähnt, können Sie ausgeben RADIUS-Server ihr Serverzertifikat in eine von zwei Arten: von einer kommerziellen Zertifizierungsstelle \(wie z. B. VeriSign, Inc.,\), oder von einer privaten Zertifizierungsstelle, die Sie in Ihrem Netzwerk bereitstellen. Wenn der RADIUS-Server ein Computerzertifikat, die von einer kommerziellen Zertifizierungsstelle ausgestellt wurde, die bereits ein Stammzertifikat im vertrauenswürdigen Stammzertifizierungsstellen-Zertifikatspeicher des Clients installiert sendet, kann dann der drahtlose Client die RADIUS-Server überprüfen Computerzertifikat, unabhängig davon, ob der drahtlose Client Active Directory-Domäne verknüpft ist. In diesem Fall der drahtlose Client mit dem drahtlosen Netzwerk herstellen kann, und klicken Sie dann können Sie den Computer der Domäne hinzufügen.

>[!NOTE]
>Das Verhalten, dass der Client zum Überprüfen des Serverzertifikats kann deaktiviert werden, aber das Deaktivieren der Überprüfung des Serverzertifikats wird nicht in produktionsumgebungen empfohlen.

Bootstrap-Drahtlosprofil sind temporäre Profile, die in so, dass Benutzer der drahtlosen Clients zur Verbindung mit dem 802.1 X aktivieren konfiguriert sind\-drahtloses Netzwerk authentifiziert, bevor der Computer mit der Domäne angehört und\/oder vor der Benutzer wurde erfolgreich in die Domäne angemeldet mithilfe von einem bestimmten drahtlosen Computer zum ersten Mal.  Dieser Abschnitt fasst zusammen, welches Problem gefunden wird, wenn Sie versuchen, einen Drahtloscomputer mit der Domäne oder für einen Benutzer mit einer Domäne beizutreten\-verknüpften Drahtloscomputer zum ersten Mal mit der Domäne anmelden.

Für Bereitstellungen, in dem der Benutzer oder IT-Administrator einen Computer physisch mit dem Beitritt zur Domäne Ethernet-Netzwerk verbinden kann nicht aus, und der Computer verfügt nicht über die erforderlichen ausstellende, ZS-Zertifikat installiert, die im Stamm der  **Vertrauenswürdige Stammzertifizierungsstellen** Zertifikatspeicher, können Sie drahtlose Clients mit einem Profil temporäre drahtlose Verbindung mit dem Namen konfigurieren eine *Bootstrapping Profil*, eine Verbindung mit dem drahtlosen Netzwerk herstellen.

Ein *Bootstrapping Profil* entfällt die Anforderung zum Überprüfen der RADIUS-Server Computerzertifikats. Diese temporäre Konfiguration mit der drahtlose Benutzer fügen Sie den Computer der Domäne, die zu diesem Zeitpunkt für das Drahtlosnetzwerk \(IEEE 802.11\) Richtlinien werden angewendet, und die entsprechenden Stamm-CA-Zertifikat wird automatisch installiert, auf die Computer, auf.

Wenn die Gruppenrichtlinie angewendet wird, werden ein oder mehrere drahtlose Verbindung-Profile, die die Anforderung für die gegenseitige Authentifizierung erzwingen auf dem Computer angewendet. Das bootstrap-Profil ist nicht mehr erforderlich und wird entfernt. Nach dem Hinzufügen des Computers zur Domäne und Neustart des Computers, können der Benutzer eine drahtlose Verbindung Sie mit der Domäne anmelden.

Einen Überblick über den drahtlosen Zugriff Bereitstellungsprozess, die mit diesen Technologien finden Sie unter [Wireless Access-Bereitstellungsübersicht](b-wireless-access-deploy-overview.md).
