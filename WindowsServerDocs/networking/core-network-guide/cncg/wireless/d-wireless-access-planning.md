---
title: Planung der Bereitstellung des Funkzugriffs
description: Dieses Thema ist Teil des Windows Server 2016-Networking Guide "Deploy Password-Based 802.1 X Authenticated Wireless Access"
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 8c632d02-2270-4a82-8fc4-74ea3747f079
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a2571f509fbbca8384e626ad3c8c13f1c0a50400
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855461"
---
# <a name="wireless-access-deployment-planning"></a>Planung der Bereitstellung des Funkzugriffs

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Bevor Sie den drahtlosen Zugriff bereitstellen, müssen Sie Folgendes planen:

- Installation von drahtlosen Zugriffspunkten \(APs\) in Ihrem Netzwerk

- Konfiguration des drahtlosen Clients und Zugriff

Die folgenden Abschnitte enthalten Details zu diesen Schritten Planung.

## <a name="planning-wireless-ap-installations"></a>Planen der drahtlose AP-Installationen
Wenn Sie Ihre drahtlose Lösung entwerfen, müssen Sie Folgendes ausführen:

1. Welche Standards, die Ihre drahtlosen Zugriffspunkte unterstützen, müssen ermitteln
2. Bestimmen Sie die in allen Regionen, in dem Sie WLAN-Dienst bereitstellen möchten
3. Bestimmen Sie, wo Sie drahtlose Zugriffspunkte suchen sollen

Darüber hinaus müssen Sie planen ein Schema der IP-Adresse für Ihren drahtlosen Zugriffspunkts und drahtlosen Clients. Finden Sie im Abschnitt **sollten Sie die Konfiguration von drahtlosen Zugriffspunkt auf dem Netzwerkrichtlinienserver** unten Weitere Informationen.

### <a name="verify-wireless-ap-support-for-standards"></a>Überprüfen der drahtlose AP-Unterstützung für standards
Für den Zweck der Konsistenz und einfache Bereitstellung und Verwaltung von AP empfiehlt es sich, dass Sie die drahtlose Zugriffspunkten der gleichen Marke und Modell des bereitstellen.

Die Drahtloszugriffspunkte, die Sie bereitstellen, müssen Folgendes unterstützen:

- **IEEE 802.1X**

- **RADIUS-Authentifizierung**

- **Drahtlose Authentifizierung und Verschlüsselung.** Aufgeführt in der Reihenfolge Ihrer bevorzugten:

    1.  WPA2\-Enterprise mit AES

    2.  WPA2\-Enterprise und TKIP

    3.  WPA\-Enterprise mit AES

    4.  WPA\-Enterprise und TKIP

>[!NOTE]
>Um WPA2 bereitzustellen, müssen Sie verwenden, Drahtlosnetzwerkadaptern und Drahtloszugriffspunkten, die auch WPA2 unterstützen. Verwenden Sie andernfalls WPA\-Enterprise.

Um die erweiterte Sicherheit für das Netzwerk müssen den Drahtloszugriffspunkten darüber hinaus die folgenden Sicherheitsoptionen unterstützen:

- **DHCP-Filterung.** IP-Ports, um die Übertragung von DHCP-Broadcastmeldungen in diesen Fällen zu vermeiden, in denen der drahtlose Client als DHCP-Server konfiguriert ist, muss dem drahtlosen AP filtern. Der Drahtloszugriffspunkt muss es sich um den Client IP-Pakete von UDP-Port 68 zu senden, mit dem Netzwerk blockieren.

- **DNS-Filterung.** IP-Ports, um zu verhindern, dass einen Client eine DNS-Server ausführen muss dem drahtlosen AP filtern. Der drahtlose Zugriffspunkt muss den Client sendet, dass die IP-Pakete von TCP- oder UDP-port 53 mit dem Netzwerk blockieren.

- **Clientisolation** Wenn Ihr drahtloser Zugriffspunkt Client Isolation Funktionen bereitstellt, müssen Sie die Funktion, um zu verhindern, dass mögliche Address Resolution Protocol aktivieren \(ARP\) spoofing-Angriffe.

### <a name="identify-areas-of-coverage-for-wireless-users"></a>Identifizieren von Coverage für Mobiltelefone
Verwenden Sie Grundrisse der einzelnen Floor für jedes Gebäude, um die Bereiche zu identifizieren, wo Sie drahtlose Abdeckung bereitstellen möchten. Beispielsweise identifizieren Sie die entsprechenden Büros, Räume für Konferenzen, Hotellobbys, Kantine oder Courtyards.

Geben Sie auf die Zeichnungen, an alle Geräte, die sich die drahtlose Signale, z. B. medizinischer Geräte, drahtlose Videokameras, kabellosen Telefone, die den Betrieb im 2,4 bis 2,5 GHz-Industrie, Wissenschaft und Medical störend \(ISM\) Bereich und Bluetooth-\--fähige Geräte.

Markieren Sie in der Zeichnung, Aspekte des Gebäudes, die drahtlose Signale behindert werden können; -Metal-Objekte, die bei der Erstellung eines Gebäudes verwendet, können die Funksignal auswirken. Beispielsweise können die folgenden allgemeinen Objekte Signal Weitergabe beeinträchtigen: Aufzüge, heizungs- und Air\-Vorbereitung, Kanäle und konkrete Unterstützung Girders.

Finden Sie in der AP-Hersteller Informationen zu Datenquellen, die drahtlosen AP Radio Frequency, Funkübertragung Attenuation verursachen können. Die meisten APs bieten testen Software, die Sie verwenden können, überprüfen Sie für die Signalstärke abnimmt, Fehlerrate und den Datendurchsatz.

### <a name="determine-where-to-install-wireless-aps"></a>Bestimmen des Installationsorts für drahtlose APs installieren
Suchen Sie auf die Architekturen Zeichnungen genug zusammen schließen Ihre drahtlosen Zugriffspunkte, um ausreichend Funkverbindung jedoch weit genug auseinander liegen Geben Sie, dass sie nicht miteinander in Konflikt treten.

Die ausreichend Abstand zwischen den APs hängt des Typs des AP und drahtlosen AP-Antenne Aspekte des Gebäudes, die eine Blockierung, Signale und andere Quellen von Störungen. Sie können drahtlose Zugriffspunkt Platzierungen markieren, sodass jeder drahtlose Zugriffspunkt nicht mehr als 300 Fuß von alle angrenzenden Drahtloszugriffspunkt ist. Finden Sie in der drahtlose AP Dokumentation des Herstellers für AP-Spezifikationen und Richtlinien für die Platzierung.

Installieren Sie die drahtlose Zugriffspunkten vorübergehend an den Speicherorten, die für Ihre Architekturen Zeichnungen angegeben. Anschließend verwenden einen Laptop mit einer 802.11-Drahtlosadapter und der Standort-Umfrage-Software, die häufig bereitgestellt werden mit Drahtlosadapter ausgestattet, bestimmen Sie die Signalstärke in jeden Bereich.

In allen Regionen, in denen Signalstärke niedrig ist, positionieren Sie den Zugriffspunkt Signalstärke für den Bereich zu verbessern, installieren zusätzliche drahtlose Zugriffspunkte zum Bereitstellen der erforderlichen Abdeckung, verschieben aus, oder Entfernen von Datenquellen Signal Störungen.  

Aktualisieren Sie Ihre Architekturen Zeichnungen aus, um die letzte Position alle Drahtloszugriffspunkte anzugeben. Müssen eine genaue AP Platzierung Zuordnung hilft, später während der Problembehandlung von Vorgängen oder wenn Sie aktualisieren oder zu APs ersetzen möchten.

### <a name="plan-wireless-ap-and-nps-radius-client-configuration"></a>Planen der drahtlosen Zugriffspunkt und Ihren NPS RADIUS-Client-Konfiguration
Sie können NPS verwenden, drahtlose Zugriffspunkten einzeln oder in Gruppen zu konfigurieren.

Wenn Sie ein großes drahtloses Netzwerk, das viele APs enthält bereitstellen, ist es viel einfacher zu APs in Gruppen zu konfigurieren. Um die Zugriffspunkte als RADIUS-Client-Gruppen auf dem Netzwerkrichtlinienserver hinzuzufügen, müssen Sie den APs mit diesen Eigenschaften konfigurieren.

- Zugriffspunkte werden mit IP-Adressen aus der gleichen IP-Adressbereich konfiguriert.

- Zugriffspunkte werden alle mit den gleichen gemeinsamen geheimen Schlüssel konfiguriert.

### <a name="plan-the-use-of-peap-fast-reconnect"></a>Planen der Verwendung von PEAP schnelle Wiederherstellung der Verbindung
In einer 802.1 X-Infrastruktur sind drahtlose Zugriffspunkte als RADIUS-Clients, RADIUS-Server konfiguriert. Wenn PEAP schnelle Wiederherstellung der Verbindung bereitgestellt wird, ein drahtloser Client, der zwischen zwei oder mehr Zugriffspunkte wechselt ist nicht erforderlich, um bei jeder neuen Zuordnung authentifiziert werden.

Verbinden von PEAP-Verbindungen die Antwortzeit für die Authentifizierung zwischen Client und dem Authentifikator reduziert, weil die Authentifizierungsanforderung von der neuen Zugriffspunkt an den NPS weitergeleitet wird, die ursprünglich Authentifizierung und Autorisierung für den Client durchgeführt die verbindungsanforderung.

Da der PEAP-Client und der NPS, beide verwenden die zuvor Transport Layer Security zwischengespeicherte \(TLS\) Verbindungseigenschaften \(die Auflistung der Namen des TLS-Handles\), den NPS können schnell ermitteln, der Client ist für eine erneute Verbindung autorisiert.

>[!IMPORTANT]
>Für schnell wieder Verbindungen herstellen, um korrekt zu funktionieren, APs müssen als RADIUS-Clients, der den gleichen NPS konfiguriert sein.

Wenn der ursprüngliche NPS nicht mehr verfügbar ist, oder wechselt der Client mit einem Zugriffspunkt, der als RADIUS-Client auf einen anderen RADIUS-Server konfiguriert ist, muss eine vollständige Authentifizierung zwischen dem Client und der neue Authentifikator stattfinden.

### <a name="wireless-ap-configuration"></a>Drahtlose AP-Konfiguration
Die folgende Liste enthält Elemente, die häufig in 802.1X-authentifizierten konfiguriert\-Drahtloszugriffspunkt:

> [!NOTE]
> Die Elementnamen je nach Marke und Modell variieren können, und es können sich von denen in der folgenden Liste werden. Finden Sie unter der drahtlose AP-Dokumentation für die Konfiguration\-spezifische Details.

- **Dienst festgelegt Bezeichner \(SSID\)**. Dies ist der Name des Drahtlosnetzwerks \(z. B. ExampleWlan\), und der Name, der für drahtlose Clients angekündigt wird. Um Verwechslungen zu vermeiden, sollte die SSID, die Sie auswählen, angekündigt werden soll nicht die SSID übereinstimmen, die von allen drahtlosen Netzwerken übertragen wird, die im Empfangsbereich des Ihr drahtloses Netzwerk befinden.

    Konfigurieren Sie in Fällen, die in denen mehrere drahtlose Zugriffspunkte als Teil des gleichen drahtlosen Netzwerk bereitgestellt werden jeden drahtlosen Zugriffspunkt mit derselben SSID ein. Konfigurieren Sie in Fällen, die in denen mehrere drahtlose Zugriffspunkte als Teil des gleichen drahtlosen Netzwerk bereitgestellt werden jeden drahtlosen Zugriffspunkt mit derselben SSID ein.  

    In Fällen Sie mehrere Drahtlosnetzwerke haben, um bestimmte geschäftsanforderungen zu erfüllen bereitstellen müssen, sollten Ihre drahtlosen APS in einem Netzwerk übertragen, eine andere SSID als die SSID Ihrer anderen Netzwerke\(s\). Z. B., wenn Sie ein separates drahtloses Netzwerk für Ihre Mitarbeiter und Gäste benötigen, Sie können Ihre drahtlosen Zugriffspunkte für das Business-Netzwerk mit konfigurieren die SSID senden festgelegt **ExampleWLAN**. Für Ihr Netzwerk Gast anschließend jeden drahtlosen Zugriffspunkt SSID senden, legen **GuestWLAN**. Auf diese Weise können Ihre Mitarbeiter und Gäste mit dem gewünschten Netzwerk, ohne dass unnötige Verwirrung entsteht eine Verbindung herstellen.  

    > [!TIP]  
    > Einige drahtlose APs haben die Möglichkeit, mehrere SSID zum Aufnehmen von mehreren übertragen\-Netzwerk-Bereitstellungen. Drahtlose Zugriffspunkt, der mehrere SSID übertragen werden kann, können bereitstellungs- und Wartungsaufgaben Kosten reduzieren.  

- **Drahtlose Authentifizierung und Verschlüsselung**.

    Drahtlose Authentifizierung ist die Sicherheitsauthentifizierung, die verwendet wird, wenn der drahtlose Client mit einem drahtlosen Zugriffspunkt zuordnet.  

    Drahtlose Verschlüsselung ist die Sicherheit-Verschlüsselungsverfahren, das mit der drahtlosen Authentifizierung verwendet wird, um die Kommunikation zu schützen, die zwischen dem drahtlosen Zugriffspunkt und Ihren drahtlosen Client gesendet werden.  

- **Wireless-Zugriffspunkt IP-Adresse \(statische\)**. Konfigurieren Sie für jeden drahtlosen Zugriffspunkt eine eindeutige statische IP-Adresse ein. Das Subnetz einen DHCP-Server bedient wird, sicher, dass alle AP IP-Adressen innerhalb eines DHCP-Ausschlussbereichs fallen, sodass der DHCP-Server nicht versucht wird, um die IP-Adresse an einem anderen Computer oder Gerät ausgeben. Ausschlussbereiche in im Verfahren "So erstellen und aktivieren einen neuen DHCP-Bereich" dokumentiert sind, der [Core Network Guide](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide). Wenn Sie Zugriffspunkte als RADIUS-Clients auf Gruppenbasis in NPS konfigurieren möchten, müssen jeden Zugriffspunkt in der Gruppe eine IP-Adresse aus der gleichen IP-Adressbereich.

- **DNS-Namen**. Einigen Drahtloszugriffspunkten können mit einem DNS-Namen konfiguriert werden. Konfigurieren Sie jeden drahtlosen Zugriffspunkt mit einem eindeutigen Namen ein. Für, wenn Sie z. B. eine bereitgestellte Drahtloszugriffspunkten in einem Multithread\-Geschichte erstellen, können Sie die ersten drei Drahtloszugriffspunkte, die in der dritten Etage AP3 bereitgestellt werden Namen\-01 AP3\-02 und AP3\-03.

- **Drahtlose AP-Subnetzmaske**. Konfigurieren Sie die Maske, um anzugeben, welcher Bereich der IP-Adresse ist die Netzwerk-ID und welcher Teil der IP-Adresse des Hosts.

- **AP-DHCP-Dienst**. Wenn Ihr drahtlose Zugriffspunkt eines integrierten verfügt\-im DHCP-Dienst deaktivieren.

- **RADIUS-gemeinsamen geheimen Schlüssel**. Verwenden Sie einen eindeutigen RADIUS gemeinsamen geheimen Schlüssel für jeden drahtlosen Zugriffspunkt, es sei denn, Sie planen, Konfigurieren von NPS RADIUS-Clients in Gruppen –, in welcher Situation Sie alle APs in der Gruppe mit den gleichen gemeinsamen geheimen Schlüssel konfigurieren müssen. Gemeinsame geheime Schlüssel muss eine zufällige Sequenz von mindestens 22 Zeichen lang sein, mit Groß- und Kleinbuchstaben, Zahlen und Interpunktionszeichen. Um sicherzustellen, dass hinsichtlich Ihrer Zufälligkeit, können Sie eine zufällige Zeichen-Programm Ihrer gemeinsamen geheimen Schlüssel zu erstellen. Es wird empfohlen, dass Sie den gemeinsamen geheimen Schlüssel für jeden drahtlosen Zugriffspunkt aufzeichnen und speichern Sie sie an einem sicheren Ort, z. B. eine sichere Office. Beim Konfigurieren von RADIUS-Clients in der NPS-Konsole erstellen Sie eine virtuelle Version der einzelnen Pazifik. Der gemeinsame geheime Schlüssel, den Sie für jede virtuelle AP in NPS konfigurieren, muss den gemeinsamen geheime Schlüssel auf dem tatsächlichen, physischen Zugriffspunkt übereinstimmen.

- **IP-Adresse des RADIUS-Servers**. Geben Sie die IP-Adresse des NPS, die zum Authentifizieren und Autorisieren von verbindungsanforderungen an diesem Zugriffspunkt verwendet werden sollen.

- **UDP-Port\(s\)**. Standardmäßig verwendet NPS UDP-Ports 1812 und 1645 für RADIUS-Authentifizierungsnachrichten und UDP-Ports 1813 und 1646 für RADIUS-Kontoführungsnachrichten. Es wird empfohlen, dass Sie die Standardeinstellungen für RADIUS-UDP-Ports nicht ändern.

- **Herstellerspezifische Attribute**. Einige drahtlose Zugriffspunkte müssen Hersteller\-bestimmte Attribute \(VSAs\) vollständige drahtlosen AP-Funktionalität bereitstellen.

- **DHCP-Filterung**. Konfigurieren Sie drahtlose Zugriffspunkte zum Blockieren von drahtlosen Clients IP-Pakete von UDP-Port 68 mit dem Netzwerk zu senden. Finden Sie in der Dokumentation für Ihren drahtlosen Zugriffspunkt so konfigurieren Sie DHCP-Filterung.

- **DNS-Filterung**. Konfigurieren Sie drahtlose Zugriffspunkte zum Blockieren von drahtlosen Clients IP-Pakete von TCP- oder UDP-Port 53 mit dem Netzwerk zu senden. Finden Sie in der Dokumentation für Ihren drahtlosen Zugriffspunkt so konfigurieren Sie DNS-Filterung.

## <a name="planning-wireless-client-configuration-and-access"></a>Planen der Konfiguration des drahtlosen Clients und Zugriff

Beim Planen der Bereitstellung von 802.1 X\-Drahtloszugriff, müssen Sie mehrere Clients berücksichtigen\-bestimmte Faktoren:

- **Planen der Unterstützung für mehrere Standards für**.

    Bestimmen Sie, ob Ihre drahtlose Computer alle verwenden die gleiche Version von Windows oder als eine Kombination von Computern, auf denen andere Betriebssysteme ausgeführt werden. Wenn sie unterschiedlich sind, stellen Sie sicher, dass Sie verstehen, dass alle Unterschiede zwischen den Standards, die von den Betriebssystemen unterstützt.

    Bestimmen Sie, ob alle den drahtlosen Netzwerkadaptern auf den drahtlosen Client-Computern die gleichen drahtlosstandards unterstützen oder unterschiedlichen Standards unterstützt werden sollen. Beispielsweise ermitteln, ob einige Netzwerkadapter Hardware-Treiber WPA2 unterstützen\-Enterprise und AES, während andere nur WPA-Unterstützung\-Enterprise und TKIP.

- **Planung clientauthentifizierungsmodus**. Authentifizierungsmodi definieren, wie Anmeldeinformationen für die Domäne von Windows-Clients verarbeiten. Sie können über die folgenden drei Netzwerk Authentifizierungsmodi in der Drahtlosnetzwerk-Richtlinien auswählen.  

    1. **Der Benutzer erneut\-Authentifizierung**. In diesem Modus gibt an, dass die Authentifizierung immer mithilfe der Sicherheitsanmeldeinformationen, die basierend auf den aktuellen Zustand des Computers ausgeführt wird. Wenn keine Benutzer am Computer angemeldet sind, erfolgt die Authentifizierung mithilfe der Computeranmeldeinformationen. Wenn ein Benutzer auf dem Computer angemeldet ist, wird Authentifizierung immer mithilfe der Anmeldeinformationen des Benutzers ausgeführt.  

    2. **Nur Computer**. Computer nur im Modus gibt an, die Authentifizierung erfolgt immer mit die Computer-Anmeldeinformationen.  

    3.  **Benutzerauthentifizierung**. Benutzer-Authentifizierungsmodus gibt an, dass die Authentifizierung nur dann ausgeführt wird, wenn der Benutzer auf dem Computer angemeldet ist. Wenn keine Benutzer am Computer angemeldet sind, werden die Authentifizierungsversuche nicht ausgeführt.  

- **Planen der drahtlose Einschränkungen**. Bestimmen Sie, ob Sie alle Ihre drahtlose Benutzer mit der gleichen Ebene des Zugriffs auf Ihr drahtloses Netzwerk bereitstellen möchten, oder, ob Sie den Zugriff für einige Ihrer drahtlosen Benutzer beschränken möchten. Sie können Einschränkungen auf dem Netzwerkrichtlinienserver für bestimmte Benutzergruppen drahtlosen anwenden.  Beispielsweise können Sie bestimmten Tagen und Stunden definieren, dass bestimmte Gruppen Zugriff auf das drahtlose Netzwerk zulässig sind.  

- **Planen der Methoden zum Hinzufügen von neuen Drahtloscomputer**. Für drahtlose\-kann Computer, die mit der Domäne verbunden sind, bevor Sie Ihr drahtlose Netzwerk, bereitstellen, wenn der Computer in ein Segment des verdrahteten Netzwerks verbunden ist, die durch 802.1 X nicht geschützt ist, die funkkonfigurationseinstellungen sind automatisch angewendet werden, nachdem Sie Drahtlosnetzwerk konfigurieren \(IEEE 802.11\) Richtlinien, die auf dem Domänencontroller und die Gruppenrichtlinie auf dem drahtlosen Client aktualisiert wird.  

    Bei Computern, die nicht bereits mit der Domäne verknüpft sind, jedoch Sie müssen planen, eine Methode, um die Einstellungen, die für 802.1 X erforderlich sind, gelten\-ein authentifizierter Zugriff. Ermitteln Sie beispielsweise an, ob den Computer mit der Domäne zu verknüpfen, indem Sie eine der folgenden Methoden werden sollen.

    1.  Verbinden Sie den Computer, auf ein Segment des verdrahteten Netzwerks, das durch 802.1 X nicht geschützt ist, und fügen Sie den Computer der Domäne.

    2.  Geben Sie Ihre drahtlose Benutzer mit den Schritten und Einstellungen, die sie benötigen, um ihre eigenen bootstrap-Drahtlosprofil hinzufügen, d. h., sie mit der Domäne beitritt.

    3.  Weisen Sie IT-Personal, drahtlose Clients mit der Domäne zu verknüpfen.

### <a name="planning-support-for-multiple-standards"></a>Planen der Unterstützung für mehrere-standards

Funknetzwerk \(IEEE 802.11\) richtlinienerweiterung in der Gruppenrichtlinie bietet eine Vielzahl von Konfigurationsoptionen für eine Vielzahl von Optionen für die Bereitstellung unterstützen.

Sie können drahtlosen Zugriffspunkte, die mit den Standards konfiguriert sind, die Sie unterstützen möchten bereitstellen und konfigurieren Sie mehrere WLAN-Profilen in Drahtlosnetzwerk \(IEEE 802.11\) Richtlinien, mit den einzelnen Profilen, die Angabe eines Satzes von Standards die Sie benötigen.

Wenn Ihr Netzwerk Drahtloscomputer verfügt, die WPA2 unterstützen z. B.\-Enterprise und AES, andere Computer, die WPA-Unterstützung\-Enterprise und AES und anderen Computern, die nur WPA-Unterstützung\-Enterprise und TKIP, müssen Sie Bestimmt, ob Sie möchten:

- Ein einzelnes Profil, um die Unterstützung aller den Drahtloscomputer mit die schwächste Verschlüsselungsmethode konfigurieren, dass alle Ihre Computer – in diesem Fall WPA unterstützt\-Enterprise und TKIP.  
- Konfigurieren Sie zwei Profile, um die optimale Sicherheit zu gewährleisten bereitzustellen, die von jedem drahtlosen Computer unterstützt wird. In diesem Fall würden Sie ein Profil aus, der angibt, die stärkste Verschlüsselung konfigurieren \(WPA2\-Enterprise und AES\), und ein Profil mit den schwächere WPA\-Enterprise und TKIP-Verschlüsselung. In diesem Beispiel ist es wichtig, dass Sie das Profil platzieren, die WPA2 verwendet\-Enterprise und AES, die in der Reihenfolge der höchsten. Computer, auf denen keine Verwendung von WPA2 ist\-Enterprise und AES automatisch zum nächsten Profil in der Reihenfolge der überspringen und verarbeiten Sie das Profil, das WPA gibt\-Enterprise und TKIP.

> [!IMPORTANT]
> Das Profil mit den sichersten höhere Standards müssen in der sortierten Liste von Profilen, platziert werden, da Verbinden von Computern über das erste Profil verwenden, die sie verwenden können.

### <a name="planning-restricted-access-to-the-wireless-network"></a>Planen eingeschränkten Zugriff auf dem drahtlosen Netzwerk

In vielen Fällen empfiehlt es sich, drahtlose Benutzern unterschiedliche Ebenen des Zugriffs auf dem drahtlosen Netzwerk bereitzustellen. Beispielsweise empfiehlt es sich um einige Benutzer uneingeschränkten Zugriff, jede Stunde des Tages, jeden Tag der Woche zu ermöglichen. Für andere Benutzer sollten Sie nur Zugriff während der kernstunden, Montag bis Freitag, zulassen und Verweigern des Zugriffs auf Samstag und Sonntag.

Dieses Handbuch enthält Anweisungen zum Erstellen einer Access-Umgebung, die alle Ihre drahtlose Benutzer in einer Gruppe mit gemeinsamen Zugriff auf Ressourcen Drahtlosnetzwerke platziert. Sie erstellen eine Sicherheitsgruppe für drahtlose Benutzer-in Active Directory-Benutzer und Computer ausrichten\-in, und nehmen Sie dann auf jeden Benutzer, die für den drahtlosen Zugriff auf ein Mitglied dieser Gruppe gewähren möchten.

Wenn Sie die NPS-Netzwerkrichtlinien konfigurieren, geben Sie die Sicherheitsgruppe für drahtlose Benutzer-als das Objekt, das NPS verarbeitet, bei der Autorisierung zu ermitteln.

Wenn Ihre Bereitstellung Unterstützung für verschiedene Ebenen des Zugriffs erfordert müssen Sie jedoch nur die folgenden ausführen:  

1. Erstellen Sie mehrere drahtlose Sicherheitsgruppe "Benutzer" um zusätzliche Sicherheit bei drahtlosen Verbindungen Gruppen in Active Directory-Benutzer und-Computer zu erstellen. Beispielsweise können Sie eine Gruppe erstellen, die Benutzer enthält, die haben vollständigen Zugriff wird eine Gruppe für Benutzer, die haben nur Zugriff während der regulären Arbeitszeiten und andere Gruppen, die andere Kriterien entsprechen, die Ihren Anforderungen entsprechen.

2. Hinzufügen von Benutzern zu den entsprechenden Sicherheitsgruppen, die Sie erstellt haben.

3. Konfigurieren Sie zusätzliche Netzwerkrichtlinienserver Netzwerkrichtlinien für jede Gruppe für zusätzliche Sicherheit bei drahtlosen Verbindungen, und konfigurieren Sie die Richtlinien gelten die Bedingungen und Einschränkungen, die für jede Gruppe erforderlich sind.

### <a name="planning-methods-for-adding-new-wireless-computers"></a>Planen der Methoden zum Hinzufügen von neuen Drahtloscomputer

Die bevorzugte Methode zum neuen Drahtloscomputer mit der Domäne ein, und melden Sie sich bei der Domäne zu verknüpfen, wird mithilfe einer Kabelverbindung in ein Segment des LANS, die Zugriff auf Domänencontroller und nicht durch ein mit 802.1 X Authentifizierung Ethernet-Switch geschützt.

In einigen Fällen allerdings es möglicherweise nicht praktikabel ist, verwenden Sie eine Kabelverbindung zum Hinzufügen von Computern zur Domäne oder, für einen Benutzer verwenden eine Kabelverbindung für die der ersten Anmeldung beim Versuch, mithilfe von Computern, die bereits mit der Domäne verbunden sind.

Zum Hinzufügen eines Computers mit der Domäne über eine drahtlose Verbindung oder für Benutzer mit der Domäne die erste Zeit mit einer Domäne anmelden\-gehörenden Computer und einer drahtlosen Verbindung, drahtlose Clients müssen zunächst eine Verbindung herstellen mit dem drahtlosen Netzwerk auf einem ein Segment, das mithilfe einer der folgenden Methoden auf den Domänencontroller zugreifen.

1. **Ein Mitglied der IT-Mitarbeiter verknüpfen einen Drahtloscomputer mit der Domäne, und anschließend Single Sign On bootstrap-Drahtlosprofil konfiguriert.** Mit dieser Methode können IT-Administrator den Drahtloscomputer mit der Ethernet-Netzwerk verbunden, und klicken Sie dann die Domäne der Computer hinzugefügt. Dann wird der Administrator des Computers mit dem Benutzer verteilt. Wenn der Benutzer den Computer startet, werden die Anmeldeinformationen für die Domäne, die sie manuell, für die Anmeldung des Benutzers angeben verwendet, sowohl eine Verbindung mit dem drahtlosen Netzwerk herstellen, und melden Sie sich bei der Domänenadministrators.  

2. **Der Benutzer konfigurieren Ihren Drahtloscomputer mit bootstrap-Drahtlosprofil manuell, und klicken Sie dann mit der Domäne verknüpft.** Mit dieser Methode können konfigurieren Benutzer manuell ihren Drahtloscomputer mit einem bootstrap-Drahtlosprofil basierend auf Anweisungen aus der IT-Administrator. Der bootstrap-Drahtlosprofil ermöglicht Benutzern das Herstellen einer Drahtlosverbindung und fügen Sie dann den Computer mit der Domäne. Nach dem Hinzufügen des Computers zur Domäne und Neustart des Computers, kann der Benutzer anmelden mit der Domäne unter Verwendung einer drahtlosen Verbindung und ihre Anmeldeinformationen für ein Domänenkonto.

Zum drahtlosen Zugriff bereitstellen zu können, finden Sie unter [die Bereitstellung von drahtlosen Zugriff](e-wireless-access-deployment.md).
