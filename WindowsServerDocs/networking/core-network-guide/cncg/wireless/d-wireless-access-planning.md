---
title: Drahtlosen Zugriff Planung der Bereitstellung
description: In diesem Thema ist Teil des Windows Server 2016 Networking Guide "Deploy Password-Based 802.1 X Authenticated Wireless Access"
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 8c632d02-2270-4a82-8fc4-74ea3747f079
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a1aa7d9fa66c480988ec7e3a97447157bd3eab9c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="wireless-access-deployment-planning"></a>Drahtlosen Zugriff Planung der Bereitstellung

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Bevor Sie den drahtlosen Zugriff bereitstellen, müssen Sie Folgendes planen:

- Installation von Wireless Access zeigt \(APs\) in Ihrem Netzwerk

- Drahtlosen Client-Konfiguration und Zugriff

Die folgenden Abschnitte enthalten Detail zu diesen SchrittenPlanung.

## <a name="planning-wireless-ap-installations"></a>Planen der drahtlose Zugriffspunkt-Installationen
Wenn Sie Ihre WLAN-Zugriff-Lösung entwerfen, müssen Sie Folgendes tun:

1. Bestimmen Sie, welche Standards, Ihre drahtlosen Zugriffspunkte unterstützen müssen
2. Bestimmen Sie, die in allen Regionen, in dem Mobilfunkanbieter bereitgestellt werden sollen
3. Bestimmen Sie, in denen drahtlose Zugriffspunkte werden soll

Darüber hinaus müssen Sie planen ein Schema der IP-Adresse für Ihren drahtlosen Zugriffspunkts und Wireless-Clients. Finden Sie im Abschnitt **Planen der Konfiguration der drahtlosen Zugriffspunkts in NPS** unten für die-bezogene Informationen.

### <a name="verify-wireless-ap-support-for-standards"></a>Überprüfen der drahtlosen Zugriffspunkt Unterstützung von Standards
Für die Zwecke der Konsistenz und einfache Bereitstellung und Verwaltung von AP empfiehlt es sich, dass Sie drahtlose Zugriffspunkte derselben Marke und Modell bereitstellen.

Die Drahtloszugriffspunkte, die Sie bereitstellen müssen die folgenden Funktionen:

- **IEEE 802.1 X**

- **RADIUS-Authentifizierung**

- **WLAN-Authentifizierung und Verschlüsselung.** Aufgeführt in der Reihenfolge der größten bis am wenigsten bevorzugt:

    1.  WPA2\-Enterprise mit AES

    2.  WPA2\-Enterprise mit TKIP

    3.  WPA\-Enterprise mit AES

    4.  WPA\-Enterprise mit TKIP

>[!NOTE]
>Zum Bereitstellen von WPA2 müssen Sie verwenden, drahtlosen Netzwerkadaptern und drahtlosen Zugriffspunkten, die auch WPA2 unterstützen. Verwenden Sie andernfalls WPA\ Enterprise.

Zur Erhöhung der Sicherheit für das Netzwerk bereitstellen, müssen der drahtlose Zugriffspunkte darüber hinaus die folgenden Sicherheitsoptionen unterstützen:

- **DHCP-Filterung.** Der drahtlose Zugriffspunkt muss filtern Sie nach IP-Ports, um die Übertragung von DHCP-Broadcastmeldungen in diesen Fällen zu vermeiden, in dem der Drahtlosclient als DHCP-Server konfiguriert ist. Der drahtlose Zugriffspunkt muss den Client von IP-Pakete von UDP-Port 68 an das Netzwerk senden blockieren.

- **DNS filtern.** Der drahtlose Zugriffspunkt muss auf IP-Ports, um zu verhindern, dass einen Client als DNS-Server ausführen filtern. Der drahtlose Zugriffspunkt muss den Client sendet, dass die IP-Pakete von TCP- oder UDP-Port 53 mit dem Netzwerk blockieren.

- **Clientisolation** Wenn Ihrem drahtlosen Zugriffspunkt Client Isolation Funktionen bereitstellt, sollten Sie mögliche Address Resolution Protocol \(ARP\) spoofing-Angriffe zu verhindern, dass die Funktion aktivieren.

### <a name="identify-areas-of-coverage-for-wireless-users"></a>Ermittlung der Abdeckung für Mobiltelefone
Verwenden Sie Bauzeichnungen der einzelnen im Fertigungsbetrieb für jeden erstellen, um die Bereiche identifizieren, wo Sie die Funkverbindung bereitstellen möchten. Identifizieren Sie z.B. die entsprechenden Niederlassungen, Konferenzen Räume, Lobbys, Cafeterias oder Courtyards.

Geben Sie auf die Zeichnungen alle Geräte, die sich störend auf die drahtlose Signale, z.B. medizinischen Geräten, drahtlose Videokameras, kabellose Telefone, die in der 2.4 bis 2.5 GHz industrielle, wissenschaftliche und medizinische \(ISM\) Bereichen, ausgeführt werden und Bluetooth\-fähigen Geräten.

Markieren Sie in der Zeichnung Aspekte der erstellen, das drahtlose Signale stören kann; metallobjekten verwendet, bei der Erstellung eines Gebäudes können das Funksignal auswirken. Z.B. die folgenden allgemeinen Objekte können sich störend auf Verbreitung des Signals: Aufzüge Fernwärme und Air\ Verfassung Kanäle und konkrete Unterstützung Girders.

Weitere Informationen finden Sie in der AP-Hersteller Informationen zu Quellen, die drahtlosen Zugriffspunkt Funkübertragung Dämpfung verursachen können. Die meisten Zugriffspunkte bieten testen Software, die Sie für die Signalstärke, Fehlerrate und Datendurchsatz überprüfen verwenden können.

### <a name="determine-where-to-install-wireless-aps"></a>Bestimmen des Installationsorts für drahtlose Zugriffspunkte installieren
Suchen Sie auf der Bauzeichnungen genug zusammen Ihre drahtlosen Zugriffspunkte schließen, um ausreichend Funkverbindung jedoch weit auseinander zu ermöglichen, dass sie nicht gegenseitig beeinträchtigen.

Die erforderliche Abstand zwischen APs hängt von den Typ der Zugriffspunkt und AP-Antenne Aspekte des Gebäudes, die die blockieren Wireless-Signale und anderen Quellen Interferenzen. Sie können drahtlosen Zugriffspunkt Standorte markieren, damit jeder drahtlose Zugriffspunkt nicht mehr als 300 Fuß aus allen benachbarten drahtlosen Zugriffspunkt ist. Weitere Informationen finden Sie unter der drahtlosen Zugriffspunkt Dokumentation des Herstellers für AP-Spezifikationen und Richtlinien für die Platzierung.

Installieren Sie drahtlose Zugriffspunkte vorübergehend an den Speicherorten auf Ihrem Bauzeichnungen angegeben. Bestimmen Sie anhand eines Laptops mit einer 802.11-Drahtlosadapter und der Standort-Umfrage-Software, die häufig bereitgestellt werden, die mit Drahtlosadapter ausgestattet sind, klicken Sie dann die Signalstärke innerhalb eines Bereichs Abdeckung.

In allen Regionen, in denen Signalstärke gering ist, setzen Sie den Zugriffspunkt, verbessern die Signalstärke für die Reichweite, und installieren Sie zusätzliche drahtlose Zugriffspunkte, um die erforderlichen deckt, verschieben oder Entfernen von Quellen Signal Interferenzen.  

Aktualisieren Sie Ihre Bauzeichnungen, um die endgültige Position des alle drahtlosen Zugriffspunkten anzugeben. Müssen eine Karte mit genaue AP Platzierung hilft später bei der Problembehandlung für Operations oder wenn Sie ein Upgrade oder Zugriffspunkte ersetzen möchten.

### <a name="plan-wireless-ap-and-nps-radius-client-configuration"></a>Planen der drahtlosen Zugriffspunkt und Ihren NPS RADIUS-Client-Konfiguration
Sie können NPS verwenden, um drahtlose Zugriffspunkte einzeln oder in Gruppen zu konfigurieren.

Wenn Sie ein großes drahtloses Netzwerk, das viele Zugriffspunkte enthält bereitstellen, ist es sehr viel einfacher APs in Gruppen zu konfigurieren. Um die Zugriffspunkte als RADIUS-Client-Gruppen auf dem Netzwerkrichtlinienserver hinzuzufügen, müssen Sie die Zugriffspunkte mit diesen Eigenschaften konfigurieren.

- Die drahtlose Zugriffspunkte werden mit IP-Adressen aus dem IP-Adressbereich konfiguriert.

- Die drahtlose Zugriffspunkte werden alle mit den gleichen gemeinsamen geheimen Schlüssel konfiguriert.

### <a name="plan-the-use-of-peap-fast-reconnect"></a>Planen der Verwendung von PEAP schnelle Wiederherstellung der Verbindung
In einer 802.1 X-Infrastruktur sind drahtlose Zugriffspunkte als RADIUS-Clients, RADIUS-Server konfiguriert. Wenn PEAP schnelle Wiederherstellung der Verbindung bereitgestellt werden, ein drahtlosen Client, der zwischen zwei oder mehr Zugriffspunkten wechselt ist nicht erforderlich, mit jeder neue Zuordnung authentifiziert werden.

Schnelle PEAP-Wiederherstellung die Antwortzeit für die Authentifizierung zwischen Client und Authentifikator reduziert, da die Authentifizierung wird von den neuen Zugriffspunkt an den Netzwerkrichtlinienserver weitergeleitet wird, die ursprünglich Authentifizierung und Autorisierung für die Verbindung Clientanforderung ausgeführt.

Da die PEAP-Client und der NPS-Server, die beide verwenden die zuvor Transport Layer Security \(TLS\) Verbindungseigenschaften zwischengespeichert \ (diese Sammlung ist mit dem Namen der TLS-Handle\), der NPS-Server kann schnell feststellen, dass der Client für eine erneute Verbindung autorisiert ist.

>[!IMPORTANT]
>Für die schnelle verbindungswiederherstellung, um korrekt zu funktionieren, müssen die Zugriffspunkte als RADIUS-Clients, von dem gleichen NPS-Server konfiguriert werden.

Wenn der ursprüngliche NPS-Server nicht verfügbar ist oder der Client an den Zugriffspunkt verschoben wird, der als RADIUS-Client auf einen anderen RADIUS-Server konfiguriert ist, muss eine vollständige Authentifizierung zwischen dem Client und dem neuen Authentifikator erfolgen.

### <a name="wireless-ap-configuration"></a>Konfiguration von drahtlosen Zugriffspunkt
Die folgende Liste fasst die Elemente, die häufig auf 802.1X\ konfigurierten-Drahtloszugriffspunkt:

> [!NOTE]
> Die Namen der Elemente können je nach Marke und Modell variieren und sich erheblich von denen in der folgenden Liste werden können. Weitere Informationen finden Sie in der Dokumentation Ihres drahtlosen Zugriffspunkt Konfiguration fest-spezifische Detail.

- **Dienst festlegen Bezeichner \(SSID\)**. Dies ist der Name des Drahtlosnetzwerks \ (z.B. ExampleWlan\), und der Name, der für drahtlose Clients angekündigt wird. Um Verwirrung zu reduzieren, sollten die SSID, die Sie kündigen möchten die SSID, die durch keine drahtlosen Netzwerke übertragen wird, die innerhalb des Drahtlosnetzwerks Empfangsbereich sind nicht überein.

    Konfigurieren Sie in Fällen, in denen mehrere drahtlose Zugriffspunkte als Teil der im selben drahtlosen Netzwerk bereitgestellt werden jeden drahtlosen Zugriffspunkt mit derselben SSID. Konfigurieren Sie in Fällen, in denen mehrere drahtlose Zugriffspunkte als Teil der im selben drahtlosen Netzwerk bereitgestellt werden jeden drahtlosen Zugriffspunkt mit derselben SSID.  

    In Fällen, in denen Sie unterschiedliche Funknetzwerke entsprechend den geschäftlichen Anforderungen bereitstellen müssen, sollten Ihre drahtlosen Zugriffspunkts ein Netzwerk eine andere SSID als die SSID Ihrer anderen network\(s\) übertragen. Sie z.B., wenn Sie ein separates drahtloses Netzwerk für Ihre Mitarbeiter und Gäste benötigen, konnte konfigurieren Ihre drahtlosen Zugriffspunkte für das Unternehmensnetzwerk mit der SSID festgelegt, dass übertragen **ExampleWLAN**. Für das Gastbetriebssystem-Netzwerk kann anschließend jeder drahtlose Zugriffspunkt SSID übertragen festgelegt **GuestWLAN**. Auf diese Weise können Ihre Mitarbeiter und Gäste mit dem gewünschten Netzwerk ohne unnötige Verwirrung verbinden.  

    > [!TIP]  
    > Einige drahtlosen Zugriffspunkts haben die Möglichkeit, mehrere SSIDS um Multithread-Bereitstellungen gerecht zu übertragen. Drahtlosen Zugriffspunkts, die mehrere SSID übertragen können können Bereitstellung und Wartungsaufgaben Kosten reduzieren.  

- **Wireless-Authentifizierung und Verschlüsselung**.

    WLAN-Authentifizierung ist die Sicherheitsauthentifizierung, die verwendet wird, wenn der Drahtlosclient mit einem drahtlosen Zugriffspunkt verknüpft.  

    Wireless-Verschlüsselung wird die Sicherheit Verschlüsselungsverfahren, das mit der WLAN-Authentifizierung verwendet wird, um die Kommunikation zu schützen, die zwischen den drahtlosen Zugriffspunkt und Ihren drahtlosen Client gesendet werden.  

- **Wireless-AP-IP-Adresse \(static\)**. Konfigurieren Sie auf jeder drahtlose Zugriffspunkt eine eindeutige statische IP-Adresse. Das Subnetz einen DHCP-Server bedient wird, sicher, dass alle AP-IP-Adressen in einem Ausschlussbereich DHCP-fallen, so, dass der DHCP-Server nicht die IP-Adresse zu einem anderen Computer oder Gerät ausgestellt. Ausschlussbereiche im Verfahren "So erstellen und aktivieren einen neuen DHCP-Bereich" dokumentiert sind, der [Kernnetzwerkhandbuch](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide). Wenn Sie planen, Zugriffspunkte als RADIUS-Clients nach Gruppe in NPS konfigurieren, muss jeder Zugriffspunkt in der Gruppe eine IP-Adresse aus dem IP-Adressbereich haben.

- **DNS-Namen**. Einige drahtlose Zugriffspunkte können mit einem DNS-Namen konfiguriert werden. Konfigurieren Sie jeden drahtlosen Zugriffspunkt mit einem eindeutigen Namen. Wenn Sie eine bereitgestellte drahtlosen Zugriffspunkten in einem Multithread-Story Gebäude haben, können Sie z.B. die ersten drei Drahtloszugriffspunkte nennen, die auf die dritte Boden AP3\-01, AP3\-02 und AP3\-03 bereitgestellt werden.

- **Drahtlose Zugriffspunkt Subnetzmaske**. Um zu bestimmen, welcher Bereich der IP-Adresse ist die Netzwerk-ID und der Teil der IP-Adresse des Hosts zu konfigurieren.

- **AP DHCP-Dienst**. Wenn Ihr drahtlose Zugriffspunkt integrierten DHCP-Dienst hat, deaktivieren.

- **RADIUS-gemeinsamen geheimen Schlüssel**. Verwenden Sie einen eindeutigen RADIUS gemeinsamen geheimen Schlüssel für jeden drahtlosen Zugriffspunkt, es sei denn, Sie planen, konfigurieren Sie NPS RADIUS-Clients in Gruppen - unter welchen Umständen Sie alle der Zugriffspunkte in der Gruppe mit den gleichen gemeinsamen geheimen Schlüssel konfigurieren müssen. Gemeinsame geheime Schlüssel sollte eine zufällige Folge von mindestens 22 Zeichen lang sein, sowohl Groß- und Kleinbuchstaben, Zahlen und Satzzeichen. Um Zufälligkeit zu gewährleisten, können Sie ein zufälliger Zeichen Generation Programm der gemeinsame geheime Schlüssel erstellen. Es wird empfohlen, dass Sie den gemeinsamen geheimen Schlüssel für jeden drahtlosen Zugriffspunkt aufzeichnen und speichern es an einem sicheren Ort, z.B. eine sichere Office. Beim Konfigurieren von RADIUS-Clients in der NPS-Konsole erstellen Sie eine virtuelle Version der einzelnen Zugriffspunkt. Der gemeinsame geheime Schlüssel, den Sie auf jedem virtuellen Zugriffspunkt in NPS konfigurieren, muss den gemeinsamen geheimen Schlüssel auf dem tatsächlichen, physischen Zugriffspunkt übereinstimmen.

- **IP-Adresse des RADIUS-Servers**. Geben Sie die IP-Adresse des NPS-Servers, die Sie zur Authentifizierung und Autorisierung von Verbindungsanforderungen zu diesem Zugriffspunkt verwenden möchten.

- **UDP-Port\(s\)**. Standardmäßig verwendet NPS UDP-Ports 1812 und 1645 für RADIUS-Authentifizierungsnachrichten und UDP-Ports 1813 und 1646 für RADIUS-Kontoführungsnachrichten. Es wird empfohlen, dass Sie nicht die Standardeinstellungen für RADIUS-UDP-Ports ändern.

- **Herstellerspezifische**. Einige drahtlose Zugriffspunkte erfordern Vendor\-spezifische Attribute \(VSAs\) vollständige drahtlosen Zugriffspunkt zu ermöglichen.

- **DHCP-Filterung**. Konfigurieren von drahtlosen Zugriffspunkten zum Blockieren von Drahtlosclients IP-Pakete von UDP-Port 68 mit dem Netzwerk zu senden. Weitere Informationen finden Sie in der Dokumentation für Ihren drahtlosen Zugriffspunkt so konfigurieren Sie DHCP-Filterung.

- **DNS-Filterung**. Konfigurieren von drahtlosen Zugriffspunkten zum Blockieren von Drahtlosclients IP-Pakete von TCP- oder UDP-Port 53 mit dem Netzwerk zu senden. Weitere Informationen finden Sie in der Dokumentation für Ihren drahtlosen Zugriffspunkt so konfigurieren Sie DNS-Filterung.

## <a name="planning-wireless-client-configuration-and-access"></a>Planen der drahtlosen Client-Konfiguration und Zugriff

Bei der Planung der Bereitstellung von 802.1X\-Drahtloszugriff, müssen Sie mehrere Client-spezifische Faktoren berücksichtigen:

- **Planen der Unterstützung für mehrere Standards**.

    Bestimmen Sie, ob Ihre Drahtloscomputer alle verwenden die gleiche Version von Windows oder eine Mischung aus Computern unter anderen Betriebssystemen sind. Wenn sich diese unterscheiden, stellen Sie sicher, dass Sie wissen, dass alle Unterschiede zwischen den Standards, die von den Betriebssystemen unterstützt.

    Bestimmen Sie, ob alle den drahtlosen Netzwerkadaptern auf alle drahtlosen Clientcomputer den gleichen WLAN-Standards unterstützen, oder ob unterschiedlichen Standards unterstützt werden müssen. Beispielsweise ermitteln Sie, ob einige Hardware Netzwerkadaptertreiber unterstützen WPA2\-Enterprise und AES, während andere nur WPA\-Enterprise und TKIP unterstützen.

- **Client-Authentifizierung Planungsmodus**. Authentifizierungsmodi definieren, wie Windows-Clients Domänenanmeldeinformationen verarbeiten. Sie können aus den folgenden drei Netzwerk Authentifizierungsmodi in den Richtlinien für drahtlose Netzwerke auswählen.  

    1. **Benutzerauthentifizierung erneut**. In diesem Modus gibt an, dass die Authentifizierung immer mithilfe von Anmeldeinformationen, die basierend auf den aktuellen Zustand des Computers ausgeführt wird. Wenn kein Benutzer am Computer angemeldet sind, erfolgt die Authentifizierung mithilfe der Computeranmeldeinformationen. Wenn ein Benutzer am Computer angemeldet ist, wird die Authentifizierung immer mithilfe der Anmeldeinformationen des Benutzers ausgeführt.  

    2. **Nur Computer**. Computer nur Modus gibt an, dass die Authentifizierung erfolgt immer über nur die Computeranmeldeinformationen.  

    3.  **Benutzerauthentifizierung**. Benutzer-Authentifizierungsmodus gibt an, dass die Authentifizierung nur dann ausgeführt wird, wenn der Benutzer auf dem Computer angemeldet ist. Wenn keine Benutzer am Computer angemeldet sind, werden die Authentifizierungsversuche nicht ausgeführt.  

- **Planen der drahtlose Einschränkungen**. Bestimmen Sie, ob Sie alle Ihre drahtlosen Benutzer mit den gleichen Zugriff auf Ihr drahtloses Netzwerk bereitstellen möchten, oder gibt an, ob Sie den Zugriff für einige Ihrer drahtlosen Benutzer beschränken möchten. Sie können Einschränkungen auf dem Netzwerkrichtlinienserver für bestimmte Gruppen von Benutzern anwenden.  Beispielsweise können Sie bestimmte Tage und Stunden definieren, dass bestimmte Gruppen Zugriff auf das drahtlose Netzwerk zulässig sind.  

- **Planen der Methoden zum Hinzufügen von neuen Drahtloscomputer**. Für Wireless\-fähige Computer, die mit Ihrer Domäne verbunden sind, bevor Sie das drahtlose Netzwerk bereitstellen, wenn der Computer zu einem Segment verkabelten Netzwerk verbunden ist, die 802.1 X nicht geschützt ist, werden die funkkonfigurationseinstellungen automatisch angewendet, nachdem Sie Drahtlosnetzwerk konfigurieren \ (IEEE 802.11\) Richtlinien auf dem Domänencontroller und die Gruppenrichtlinien auf dem drahtlosen Client aktualisiert werden.  

    Für Computer, die nicht bereits mit der Domäne verbunden sind, aber Sie müssen planen, eine Methode zum Anwenden der Einstellungen, die für 802.1X\ erforderlich sind – ein authentifizierter Zugriff. Beispielsweise ermitteln Sie, ob Sie den Computer der Domäne mithilfe eines der folgenden Methoden hinzufügen möchten.

    1.  Verbinden Sie den Computer auf ein Segment verkabelten Netzwerk, das 802.1 X nicht geschützt ist, und klicken Sie dann fügen Sie den Computer der Domäne hinzu.

    2.  Die Schritteund die Einstellungen, die sie benötigen, um ihre eigenen Bootstrap-Drahtlosprofil, hinzufügen, d.h., sie zum Hinzufügen des Computers zur Domäne bereitstellen Sie Ihren drahtlosen Benutzern.

    3.  Weisen Sie IT-Mitarbeiter drahtlose Clients in der Domäne hinzufügen.

### <a name="planning-support-for-multiple-standards"></a>Planen der Unterstützung für mehrere Standards

Das Drahtlosnetzwerk \ (IEEE 802.11\) Erweiterung in der Gruppenrichtlinie bietet eine Breite Palette von Konfigurationsoptionen, um eine Vielzahl von Optionen für die Bereitstellung zu unterstützen.

Sie können Bereitstellen von drahtlosen Zugriffspunkten, die mit den Standards konfiguriert sind, die Sie unterstützen möchten, und konfigurieren Sie mehrere WLAN-Profilen in Drahtlosnetzwerk \ (IEEE 802.11\)-Richtlinien für jedes Profil angeben eines Satzes von Standards, die Sie benötigen.

Wenn beispielsweise Ihr Netzwerk Drahtloscomputer verfügt, die WPA2\-Enterprise und AES, andere Computer, auf denen WPA\-Enterprise und AES unterstützt und anderen Computern, die nur WPA\-Enterprise und TKIP, unterstützen unterstützen müssen Sie bestimmen, ob Sie möchten:

- Konfigurieren ein Profils, um alle drahtlose Computer unterstützen, indem Sie die schwächste Verschlüsselungsmethode, dass alle Computer – in diesem Fall WPA\-Enterprise und TKIP unterstützen.  
- Konfigurieren Sie zwei Profile, um die bestmögliche Sicherheit zu bieten, die von jedem drahtlosen Computer unterstützt wird. In diesem Beispiel konfigurieren Sie ein Profil, der angibt, die stärkste Verschlüsselung \ (WPA2\-Enterprise und AES\), und ein Profil, das die schwächere WPA\-Enterprise und TKIP-Verschlüsselung verwendet. In diesem Beispiel ist es wichtig, dass Sie das Profil einfügen, das wpa2\-Enterprise und AES in der Reihenfolge der obersten Ebene verwendet. Computer, die nicht mit WPA2\-Enterprise und AES können werden automatisch zum nächsten Profil in der Reihenfolge der überspringen und verarbeiten das Profil, das WPA\-Enterprise und TKIP angibt.

> [!IMPORTANT]
> Da beim Verbinden von Computern das erste Profil verwenden, die sie verwenden können, müssen Sie das Profil mit den sichersten Standards, die höher in der sortierte Liste von Profilen platzieren.

### <a name="planning-restricted-access-to-the-wireless-network"></a>Planen der eingeschränkten Zugriff auf das drahtlose Netzwerk

In vielen Fällen sollten Sie Benutzern mit unterschiedlichen Detailebenen Zugriff auf das drahtlose Netzwerk bereitzustellen. Sie möchten z.B. einige Benutzer uneingeschränkten Zugriff, jede Stunde des Tages, jeden Tag der Woche zulassen. Für andere Benutzer sollten Sie nur während der Geschäftszeiten Core Montag bis Freitag, Zugriff zulassen und Verweigern des Zugriffs auf Samstag und Sonntag.

Dieses Handbuch enthält Anweisungen zum Erstellen einer Access-Umgebung, in der alle drahtlosen Benutzer in einer Gruppe mit gemeinsamen Zugriff auf Ressourcen Drahtlosnetzwerke positioniert. Sie Erstellen einer Sicherheitsgruppe für Benutzer in den Active Directory-Benutzer und -Computer-Snap-In, und stellen Sie jedem Benutzer für den drahtlosen Zugriff gewähren, ein Mitglied dieser Gruppe werden sollen.

Wenn Sie NPS-Netzwerkrichtlinien konfigurieren, geben Sie die Sicherheitsgruppe mit drahtlosem als das Objekt, das NPS, beim Ermitteln der Autorisierung verarbeitet.

Wenn Ihre Bereitstellung Unterstützung für unterschiedliche Zugriffsebenen erfordert müssen Sie jedoch nur die folgenden ausführen:  

1. Erstellen Sie mehr als eine drahtlose Benutzer-Sicherheitsgruppe, um zusätzliche WLAN-Sicherheitsgruppen in Active Directory-Benutzer und -Computer erstellen. Sie können beispielsweise eine Gruppe erstellen, die Benutzer enthält, die Vollzugriff, einer Gruppe für diejenigen, die nur Zugriff während der regulären Arbeitszeit sowie weiteren Gruppen, die anderen Kriterien entsprechen, die Ihren Anforderungen entsprechen.

2. Fügen Sie Benutzer zu der entsprechenden Sicherheitsgruppen, die Sie erstellt haben.

3. Konfigurieren Sie zusätzliche NPS-Netzwerkrichtlinien für jede Gruppe zusätzlicher Schutz, und konfigurieren Sie die Richtlinien gelten die Bedingungen und Einschränkungen, die Sie für jede Gruppe benötigen.

### <a name="planning-methods-for-adding-new-wireless-computers"></a>Planen der Methoden zum Hinzufügen von neuen Drahtloscomputer

Die bevorzugte Methode zum neuen drahtlosen Computer auf die Domäne ein, und melden Sie sich bei der Domäne angehören, ist die Verwendung von einer drahtgebundene Verbindungs zu einem Segment des LANS, die Zugriff auf Domänencontroller, und nicht durch ein mit 802.1 X Authentifizierung Ethernet-Switch geschützt ist.

In einigen Fällen jedoch, es möglicherweise nicht praktikabel ist, eine Kabelverbindung zu verwenden, um das Hinzufügen von Computern zur Domäne oder für den Benutzer verwenden eine drahtgebundene Verbindung für ihre erste Anmeldung mithilfe von Computern, die bereits mit der Domäne verbunden sind.

Zum Hinzufügen eines Computers zur Domäne über eine drahtlose Verbindung oder für Benutzer an der Domäne anmelden müssen erstmals mit einem Domäne\ beigetretenen Computer und eine drahtlose Verbindung Drahtlosclients zunächst eine Verbindung mit dem Drahtlosnetzwerk auf ein Segment herstellen, die Zugriff auf das Netzwerk-Domänencontroller verfügt, indem Sie eine der folgenden Methoden.

1. **Ein Mitglied der IT-Mitarbeiter einen drahtlosen Computer der Domäne hinzugefügt, und anschließend ein einmaliges Anmelden Bootstrap-Drahtlosprofil konfiguriert.** Mit dieser Methode können IT-Administrator drahtlosen Computer mit dem Ethernet-Netzwerk verbunden, und dann wird der Computer der Domäne. Dann wird der Administrator des Computers für den Benutzer verteilt. Wenn der Benutzer den Computer gestartet wird, werden die Anmeldeinformationen für die Domäne, die sie manuell, für die Anmeldung des Benutzers angeben sowohl eine Verbindung mit dem Drahtlosnetzwerk herzustellen, und melden Sie sich bei der Domänenbenutzers verwendet.  

2. **Der Benutzer manuell Drahtloscomputer mit Bootstrap-Drahtlosprofil konfiguriert und dann zu der Domäne hinzugefügt.** Mit dieser Methode können konfigurieren Benutzer manuell ihre Drahtloscomputer mit einem Bootstrap-Drahtlosprofil basierend auf Informationen von einem IT-Administrator. Das Bootstrap-Drahtlosprofil kann Benutzer eine drahtlose Verbindung herzustellen, und klicken Sie dann den Computer der Domäne hinzufügen. Nach dem Hinzufügen des Computers zur Domäne und den Computer neu starten, kann der Benutzer anmelden mit der Domäne mit einer drahtlosen Verbindung und Anmeldeinformationen ihrer Domäne.

Zum Bereitstellen von drahtlosen Zugriff finden Sie unter [die Bereitstellung von drahtlosen Zugriff](e-wireless-access-deployment.md).
