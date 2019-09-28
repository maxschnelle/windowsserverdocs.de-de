---
title: Planung der Bereitstellung des Funkzugriffs
description: Dieses Thema ist Teil des Windows Server 2016-Netzwerk Handbuchs "Bereitstellen von Kenn Wort basiertem 802.1 x authentifizierten drahtlosen Zugriff".
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 8c632d02-2270-4a82-8fc4-74ea3747f079
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 44ca48ab05a7f63b1b9dd07f955e68accbcefdb7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356077"
---
# <a name="wireless-access-deployment-planning"></a>Planung der Bereitstellung des Funkzugriffs

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Bevor Sie drahtlos Zugriff bereitstellen, müssen Sie die folgenden Elemente planen:

- Installation von drahtlos Zugriffs Punkten \(\) in Ihrem Netzwerk

- Konfiguration und Zugriff auf drahtlose Clients

Die folgenden Abschnitte enthalten ausführliche Informationen zu diesen Planungsschritten.

## <a name="planning-wireless-ap-installations"></a>Planen von drahtlosen AP-Installationen
Wenn Sie die Lösung für den Drahtlos Netzwerk Zugriff entwerfen, müssen Sie die folgenden Schritte ausführen:

1. Bestimmen, welche Standards ihre drahtlos Zugriffspunkte unterstützen müssen
2. Bestimmen Sie die Abdeckungsbereiche, in denen Sie drahtlos Dienste bereitstellen möchten.
3. Bestimmen Sie, wo Sie drahtlos Zugriffspunkte suchen möchten.

Außerdem müssen Sie ein IP-Adress Schema für Ihre drahtlos Zugriffspunkt-und drahtlosen Clients planen. Weitere Informationen finden Sie im Abschnitt **Planen der Konfiguration von drahtlos Zugriffs Netzwerken in NPS** weiter unten.

### <a name="verify-wireless-ap-support-for-standards"></a>Überprüfen der Wireless AP-Unterstützung für Standards
Um die Bereitstellung und die Verwaltung von Zugriffs Punkten zu gewährleisten, wird empfohlen, drahtlos Zugriffspunkte derselben Marke und desselben Modells bereitzustellen.

Die drahtlos Zugriffspunkte, die Sie bereitstellen, müssen Folgendes unterstützen:

- **IEEE 802.1 X**

- **RADIUS-Authentifizierung**

- **Drahtlose Authentifizierung und Verschlüsselung.** In der Reihenfolge aufgelistet, in der Sie am wenigsten bevorzugt werden:

    1.  WPA2\-Enterprise mit AES

    2.  WPA2\-Enterprise mit TKIP

    3.  WPA\-Enterprise mit AES

    4.  WPA\-Enterprise mit TKIP

>[!NOTE]
>Zum Bereitstellen von WPA2 müssen Sie Drahtlos Netzwerkadapter und drahtlos Zugriffspunkte verwenden, die auch WPA2 unterstützen. Verwenden Sie andernfalls WPA\-Enterprise.

Außerdem müssen die drahtlos Zugriffspunkte die folgenden Sicherheitsoptionen unterstützen, um eine höhere Sicherheit für das Netzwerk zu gewährleisten:

- **DHCP-Filterung.** Der drahtlos Zugriffspunkt muss nach IP-Ports filtern, um die Übertragung von DHCP-Broadcast Nachrichten in Fällen zu verhindern, in denen der drahtlose Client als DHCP-Server konfiguriert ist. Der drahtlose Zugriffspunkt muss verhindern, dass der Client IP-Pakete vom UDP-Port 68 an das Netzwerk sendet.

- **DNS-Filterung.** Der drahtlos Zugriffspunkt muss nach IP-Ports filtern, um zu verhindern, dass ein Client als DNS-Server funktioniert. Der drahtlose Zugriffspunkt muss verhindern, dass der Client IP-Pakete vom TCP-oder UDP-Port 53 an das Netzwerk sendet.

- **Client Isolation** Wenn Ihr drahtloser Zugriffspunkt Client Isolations Funktionen bereitstellt, sollten Sie diese Funktion aktivieren, um mögliche \(Angriffe\) auf ARP-Spoofing zu verhindern.

### <a name="identify-areas-of-coverage-for-wireless-users"></a>Erkennen von Bereichen der Abdeckung für drahtlose Benutzer
Verwenden Sie die Architekturzeichnungen jeder Etage für jedes Gebäude, um die Bereiche zu identifizieren, in denen Sie drahtlos Abdeckung bereitstellen möchten. Identifizieren Sie z. b. die entsprechenden Niederlassungen, Konferenzräume, Lobbys, Cafeterias oder Höfe.

Geben Sie in den Zeichnungen alle Geräte an, die die drahtlosen Signale stören, wie z. b. medizinische Geräte, drahtlose Videokameras, drahtlose Telefone, die im Industrie-, wissenschaftlichen und \(medizinischen\) ISM 2,4 bis 2,5 GHz betrieben werden. Bereich und für Bluetooth\-aktivierte Geräte.

Markieren Sie auf der Zeichnung Aspekte der Erstellung, die möglicherweise durch drahtlose Signale beeinträchtigt werden. die bei der Erstellung eines Gebäudes verwendeten Metal-Objekte können sich auf das drahtlose Signal auswirken. Die folgenden allgemeinen Objekte können z. b. die Signal Weitergabe beeinträchtigen: Aufzüge, Heiz-und\-Klimaanlagen und konkrete Support-und konkrete Support.

Informationen zu Quellen, die möglicherweise eine drahtlose AP-Funkfrequenz Dämpfung verursachen, finden Sie unter Ihrem AP-Hersteller. Die meisten APS bieten Testsoftware, die Sie verwenden können, um die Signalstärke, die Fehlerrate und den Datendurchsatz zu überprüfen.

### <a name="determine-where-to-install-wireless-aps"></a>Bestimmen des Installations Orts für drahtlos Zugriffspunkte
Suchen Sie in den Architekturzeichnungen ihre drahtlos Zugriffspunkte, um ausreichend drahtlose Abdeckung bereitzustellen, aber weit genug voneinander entfernt, dass Sie sich nicht gegenseitig beeinträchtigen.

Die erforderliche Entfernung zwischen APS hängt von der Art von AP-und AP-Antennen, den Aspekten der Gebäude, in denen drahtlose Signale blockiert werden, und anderen Quellen für Störungen ab. Sie können drahtlose AP-Platzierungen markieren, sodass jeder drahtlos Zugriffspunkt nicht mehr als 300 Meter von einem angrenzenden drahtlos Zugriffspunkt ist. Informationen zu den Spezifikationen und Richtlinien für die Platzierung finden Sie in der Dokumentation des drahtlos Zugriffspunkt-Herstellers.

Installieren Sie vorübergehend drahtlos Zugriffspunkte an den Orten, die in ihren Architekturzeichnungen angegeben sind. Legen Sie dann mit einem Laptop, der mit einem 802,11-drahtlos Adapter ausgestattet ist, und der Standort Umfrage Software, die üblicherweise mit drahtlosen Adaptern bereitgestellt wird, die Signalstärke in den einzelnen Bereichen fest

Positionieren Sie in Abdeckungsbereichen, in denen die Signalstärke gering ist, den Zugriffspunkt, um die Signalstärke für den Abdeckungsbereich zu verbessern, zusätzliche drahtlos Zugriffspunkte zu installieren, um die erforderliche Abdeckung bereitzustellen, die Quelle von Signalstörungen  

Aktualisieren Sie die Architekturzeichnungen, um die endgültige Platzierung aller drahtlos Zugriffspunkte anzuzeigen. Eine genaue AP-Platzierungs Zuordnung wird später während der Problembehandlung oder beim Aktualisieren oder Ersetzen von APS unterstützt.

### <a name="plan-wireless-ap-and-nps-radius-client-configuration"></a>Planen von drahtlos Zugriffspunkt-und NPS-RADIUS-Client Konfigurationen
Sie können NPS verwenden, um drahtlos Zugriffspunkte einzeln oder in Gruppen zu konfigurieren.

Wenn Sie ein großes Drahtlos Netzwerk bereitstellen, das viele APS umfasst, ist es viel einfacher, APS in Gruppen zu konfigurieren. Um die APS als RADIUS-Client Gruppen in NPS hinzuzufügen, müssen Sie die APS mit diesen Eigenschaften konfigurieren.

- Die drahtlos Zugriffspunkte werden mit IP-Adressen aus dem gleichen IP-Adressbereich konfiguriert.

- Die drahtlos Zugriffspunkte sind alle mit demselben gemeinsamen geheimen Schlüssel konfiguriert.

### <a name="plan-the-use-of-peap-fast-reconnect"></a>Planen der schnellen erneuten Verbindungs Herstellung mit PAP
In einer 802.1 x-Infrastruktur werden drahtlose Zugriffspunkte als RADIUS-Clients für RADIUS-Server konfiguriert. Wenn die schnelle Wiederherstellung von Peer-Verbindungen bereitgestellt wird, muss ein drahtloser Client, der zwischen zwei oder mehr Zugriffs Punkten wechselt, nicht mit jeder neuen Zuordnung authentifiziert werden.

Die schnelle Wiederherstellung von OLAP reduziert die Reaktionszeit für die Authentifizierung zwischen Client und Authentifikator, weil die Authentifizierungsanforderung vom neuen Zugriffspunkt an den NPS weitergeleitet wird, der ursprünglich die Authentifizierung und Autorisierung für den Client durchgeführt hat. Verbindungsanforderung.

Da sowohl der Peer-Client als auch der NPS die zuvor zwischen \(gespeicherten\) Transport Layer Security TLS \(-Verbindungs Eigenschaften verwenden, die als TLS-\)Handle bezeichnet werden, kann der NPS schnell feststellen, dass der Client ist für eine erneute Verbindung autorisiert.

>[!IMPORTANT]
>Damit die Funktion zum schnellen erneuten Verbinden ordnungsgemäß funktioniert, müssen die APS als RADIUS-Clients desselben NPS konfiguriert werden.

Wenn die ursprüngliche NPS nicht verfügbar ist oder der Client zu einem Zugriffspunkt wechselt, der als RADIUS-Client auf einem anderen RADIUS-Server konfiguriert ist, muss die vollständige Authentifizierung zwischen dem Client und dem neuen Authentifikator erfolgen.

### <a name="wireless-ap-configuration"></a>Drahtlose AP-Konfiguration
In der folgenden Liste werden die Elemente zusammengefasst,\-die häufig auf 802.1 x-fähigen drahtlos Zugriffs Punkten

> [!NOTE]
> Die Elementnamen können je nach Marke und Modell variieren und können sich von den in der folgenden Liste unterscheiden. Ausführliche Informationen zur Konfiguration\-finden Sie in der drahtlosen AP-Dokumentation.

- **SSID für \(den Service\)set-Bezeichner**. Dies ist der Name des drahtlos Netzwerks \(, z. b. examplewlan\)und der Name, der drahtlosen Clients angekündigt wird. Um Verwirrung zu vermeiden, sollte die SSID, die Sie ankündigen möchten, nicht mit der SSID verglichen werden, die von einem Drahtlos Netzwerk gesendet wird, das sich im Empfangsbereich Ihres drahtlos Netzwerks befindet.

    In Fällen, in denen mehrere drahtlos Zugriffspunkte als Teil desselben drahtlos Netzwerks bereitgestellt werden, konfigurieren Sie jeden drahtlos Zugriffspunkt mit derselben SSID. In Fällen, in denen mehrere drahtlos Zugriffspunkte als Teil desselben drahtlos Netzwerks bereitgestellt werden, konfigurieren Sie jeden drahtlos Zugriffspunkt mit derselben SSID.  

    In Fällen, in denen Sie verschiedene Drahtlos Netzwerke bereitstellen müssen, um bestimmte Geschäftsanforderungen zu erfüllen, sollte Ihr drahtlos Zugriffspunkt in einem Netzwerk eine andere SSID als die SSID Ihres anderen\(Netzwerks\)übertragen. Wenn Sie z. b. ein separates Drahtlos Netzwerk für Ihre Mitarbeiter und Gäste benötigen, können Sie Ihre drahtlos Zugriffspunkte für das Geschäftsnetzwerk konfigurieren, wobei die SSID auf Broadcast **examplewlan**festgelegt ist. Für Ihr Gastnetzwerk können Sie dann die SSID für jeden drahtlos Zugriffspunkt für die Übertragung von **guestwlan**festlegen. Auf diese Weise können Mitarbeiter und Gäste ohne unnötige Verwirrung eine Verbindung mit dem vorgesehenen Netzwerk herstellen.  

    > [!TIP]  
    > Einige drahtlos Zugriffspunkt haben die Möglichkeit, mehrere SSIDs zu übertragen, um\-mehrere Netzwerk Bereitstellungen zu ermöglichen. Drahtlos Zugriffspunkt, der mehrere SSIDs übertragen kann, kann die Bereitstellungs-und Betriebskosten senken.  

- **Drahtlose Authentifizierung und Verschlüsselung**.

    Die drahtlose Authentifizierung ist die Sicherheits Authentifizierung, die verwendet wird, wenn der drahtlose Client einem drahtlos Zugriffspunkt zugeordnet wird.  

    Die drahtlose Verschlüsselung ist das Verschlüsselungs Verschlüsselungsverfahren, das bei der drahtlosen Authentifizierung verwendet wird, um die Kommunikation zu schützen, die zwischen dem drahtlosen Zugriffspunkt und dem drahtlosen Client gesendet wird.  

- **Drahtlose AP-IP \(-\)Adresse statisch**. Konfigurieren Sie auf jedem drahtlos Zugriffspunkt eine eindeutige statische IP-Adresse. Wenn das Subnetz von einem DHCP-Server bedient wird, stellen Sie sicher, dass alle AP-IP-Adressen innerhalb eines DHCP-Ausschluss Bereichs liegen, damit der DHCP-Server nicht versucht, dieselbe IP-Adresse an einen anderen Computer oder ein anderes Gerät auszugeben. Ausschluss Bereiche werden im Haupt [Netzwerk Handbuch](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide)unter "So erstellen und aktivieren Sie einen neuen DHCP-Bereich" dokumentiert. Wenn Sie beabsichtigen, APS als RADIUS-Clients nach Gruppe in NPS zu konfigurieren, muss jede Zugriffspunkt Gruppe in der Gruppe über eine IP-Adresse aus dem gleichen IP-Adressbereich verfügen.

- **DNS-Name**. Einige drahtlos Zugriffspunkte können mit einem DNS-Namen konfiguriert werden. Konfigurieren Sie jeden drahtlos Zugriffspunkt mit einem eindeutigen Namen. Wenn Sie z. b. über ein bereitgestelltes drahtloses\-APS in einem mehrstöckigen Gebäude verfügen, können Sie die ersten drei drahtlos Zugriffspunkte benennen, die\-auf der dritten Etage bereitgestellt werden\-AP3 01, AP3\-02 und AP3 03.

- **Drahtlose AP-Subnetzmaske**. Konfigurieren Sie die Maske so, dass festgelegt wird, welcher Teil der IP-Adresse die Netzwerk-ID und welcher Teil der IP-Adresse der Host ist.

- **AP-DHCP-Dienst**. Wenn Ihr drahtlos Zugriffspunkt über einen\-integrierten DHCP-Dienst verfügt, deaktivieren Sie ihn.

- Frei gegebener **RADIUS**-Schlüssel. Verwenden Sie für jeden drahtlos Zugriffspunkt einen eindeutigen freigegebenen RADIUS-Schlüssel, es sei denn, Sie planen die Konfiguration von NPS-RADIUS-Clients in Gruppen. in diesem Fall müssen Sie alle APS in der Gruppe mit demselben gemeinsamen geheimen Schlüssel konfigurieren. Bei gemeinsam genutzten Geheimnissen sollte es sich um eine zufällige Sequenz von mindestens 22 Zeichen mit groß-und Kleinbuchstaben, Ziffern und Interpunktions Zeichen handeln. Um die Zufälligkeit sicherzustellen, können Sie ein Programm für die zufällige Zeichen Generierung verwenden, um ihre gemeinsamen geheimen Schlüssel zu erstellen. Es wird empfohlen, den gemeinsamen geheimen Schlüssel für jeden drahtlos Zugriffspunkt aufzuzeichnen und an einem sicheren Ort (z. b. einem Büro sicher) zu speichern. Wenn Sie RADIUS-Clients in der NPS-Konsole konfigurieren, erstellen Sie eine virtuelle Version jeder Zugriffspunkt-app. Der gemeinsame geheime Schlüssel, den Sie auf den einzelnen virtuellen Zugriffs Schlüsseln in NPS konfigurieren, muss mit dem gemeinsamen geheimen Schlüssel auf der tatsächlichen, physischen Zugriffspunkt-

- **IP-Adresse des RADIUS-Servers**. Geben Sie die IP-Adresse des NPS ein, den Sie verwenden möchten, um Verbindungsanforderungen für diesen Zugriffspunkt zu authentifizieren und zu autorisieren.

- **UDP-\(Port\)s**. Standardmäßig verwendet NPS UDP-Ports 1812 und 1645 für RADIUS-Authentifizierungs Nachrichten und UDP-Ports 1813 und 1646 für RADIUS-Buchhaltungs Nachrichten. Es wird empfohlen, dass Sie die Standardeinstellungen für die RADIUS-UDP-Ports nicht ändern.

- **VSAs**. Einige drahtlos Zugriffspunkte erfordern\-anbieterspezifische \(Attribute VSAs\) , um vollständige WLAN-Funktionen bereitzustellen.

- **DHCP-Filterung**. Konfigurieren Sie drahtlos Zugriffspunkte, um zu verhindern, dass drahtlose Clients IP-Pakete vom UDP-Port 68 an das Netzwerk senden. Informationen zum Konfigurieren der DHCP-Filterung finden Sie in der Dokumentation für Ihren drahtlos Zugriffspunkt.

- **DNS-Filterung**. Konfigurieren Sie drahtlos Zugriffspunkte, um zu verhindern, dass drahtlose Clients IP-Pakete von TCP-oder UDP-Port 53 an das Netzwerk senden. Informationen zum Konfigurieren der DNS-Filterung finden Sie in der Dokumentation für Ihren drahtlos Zugriffspunkt.

## <a name="planning-wireless-client-configuration-and-access"></a>Planen der Konfiguration und des Zugriffs für drahtlose Clients

Bei der Planung der Bereitstellung des\-drahtlos Zugriffs mit 802.1 x-Authentifizierung müssen Sie mehrere\-Client spezifische Faktoren berücksichtigen:

- **Planen der Unterstützung mehrerer Standards**.

    Stellen Sie fest, ob Ihre drahtlos Computer alle die gleiche Version von Windows verwenden oder ob es sich um eine Mischung aus Computern mit unterschiedlichen Betriebssystemen handelt. Wenn Sie sich unterscheiden, stellen Sie sicher, dass Sie alle Unterschiede in den von den Betriebssystemen unterstützten Standards verstehen.

    Stellen Sie fest, ob alle drahtlosen Netzwerkadapter auf allen drahtlosen Client Computern dieselben drahtlos Standards unterstützen, oder ob Sie unterschiedliche Standards unterstützen müssen. Stellen Sie z. b. fest, ob einige Netzwerkadapter\--Hardwaretreiber WPA2 Enterprise und AES unter\-stützen, während andere nur WPA Enterprise und TKIP unterstützen.

- **Planen des Client Authentifizierungsmodus**. Authentifizierungs Modi definieren, wie die Windows-Clients Domänen Anmelde Informationen verarbeiten. In den Richtlinien für Drahtlos Netzwerke können Sie aus den folgenden drei Netzwerk Authentifizierungs Modi auswählen.  

    1. **Erneute\-Benutzerauthentifizierung**. Dieser Modus gibt an, dass die Authentifizierung immer mithilfe von Sicherheits Anmelde Informationen durchgeführt wird, die auf dem aktuellen Zustand des Computers basieren. Wenn keine Benutzer am Computer angemeldet sind, wird die Authentifizierung mithilfe der Computer Anmelde Informationen ausgeführt. Wenn ein Benutzer am Computer angemeldet ist, wird die Authentifizierung immer mit den Benutzer Anmelde Informationen ausgeführt.  

    2. **Nur Computer**. Nur Computer Modus gibt an, dass die Authentifizierung immer nur mit den Computer Anmelde Informationen ausgeführt wird.  

    3.  **Benutzerauthentifizierung**. Der Benutzer Authentifizierungsmodus gibt an, dass die Authentifizierung nur durchgeführt wird, wenn der Benutzer am Computer angemeldet ist. Wenn keine Benutzer am Computer angemeldet sind, werden keine Authentifizierungs Versuche ausgeführt.  

- **Planen von drahtlos Einschränkungen**. Legen Sie fest, ob Sie alle drahtlosen Benutzer mit der gleichen Zugriffsebene für Ihr Drahtlos Netzwerk bereitstellen möchten oder ob Sie den Zugriff für einige ihrer drahtlosen Benutzer einschränken möchten. Sie können Einschränkungen in NPS für bestimmte Gruppen drahtloser Benutzer anwenden.  Beispielsweise können Sie bestimmte Tage und Stunden definieren, denen bestimmte Gruppen Zugriff auf das Drahtlos Netzwerk erlauben.  

- **Planen von Methoden zum Hinzufügen neuer drahtlos Computer**. Bei drahtlos\-fähigen Computern, die vor der Bereitstellung Ihres drahtlos Netzwerks mit Ihrer Domäne verknüpft sind, ist der Computer, der mit einem Segment des verkabelten Netzwerks verbunden ist, das nicht durch 802.1 x geschützt ist, mit den drahtlos Konfigurationseinstellungen wird automatisch angewendet, nachdem Sie die \(Richtlinien\) für das Drahtlos Netzwerk IEEE 802,11 auf dem Domänen Controller und nach der Aktualisierung Gruppenrichtlinie auf dem drahtlosen Client konfiguriert haben.  

    Für Computer, die noch nicht mit Ihrer Domäne verknüpft sind, müssen Sie jedoch eine Methode zum Anwenden der Einstellungen planen, die für den authentifizierten\-802.1 x-Zugriff erforderlich sind. Bestimmen Sie z. b., ob Sie den Computer mit einer der folgenden Methoden der Domäne hinzufügen möchten.

    1.  Verbinden Sie den Computer mit einem Segment des verkabelten Netzwerks, das nicht durch 802.1 x geschützt ist, und fügen Sie dann den Computer der Domäne hinzu.

    2.  Stellen Sie Ihren drahtlosen Benutzern die Schritte und Einstellungen zur Verfügung, die Sie zum Hinzufügen eines eigenen drahtlosen Bootstrap-Profils benötigen, mit dem der Computer der Domäne beitreten kann.

    3.  Weisen Sie IT-Mitarbeitern den Beitritt zu drahtlosen Clients zur Domäne zu.

### <a name="planning-support-for-multiple-standards"></a>Planen der Unterstützung für mehrere Standards

Die Erweiterung für \(Drahtlos Netzwerk\) IEEE 802,11-Richtlinien in Gruppenrichtlinie bietet eine Vielzahl von Konfigurationsoptionen, um eine Vielzahl von Bereitstellungs Optionen zu unterstützen.

Sie können drahtlos Zugriffspunkte bereitstellen, die mit den Standards konfiguriert werden, die Sie unterstützen möchten, und dann mehrere drahtlos profile \(in drahtlos\) Netzwerk-IEEE 802,11-Richtlinien konfigurieren, wobei jedes Profil einen Satz von Standards angibt. die Sie benötigen.

Wenn Ihr Netzwerk beispielsweise über drahtlose Computer verfügt, die WPA2\-Enterprise und AES unterstützen, andere Computer\-, die WPA Enterprise und AES unterstützen, und\-andere Computer, die nur WPA Enterprise und TKIP unterstützen, müssen Sie bestimmen Sie, ob Sie folgende Aktionen ausführen möchten:

- Konfigurieren Sie ein einzelnes Profil, um alle drahtlos Computer mit der schwächsten Verschlüsselungsmethode zu unterstützen, die von all ihren Computern unterstützt wird (in\-diesem Fall WPA Enterprise und TKIP).  
- Konfigurieren Sie zwei Profile, um die bestmögliche Sicherheit bereitzustellen, die von den einzelnen drahtlosen Computern unterstützt wird. In dieser Instanz würden Sie ein Profil konfigurieren \(, das das stärkste\-Enterprise-und AES\)-Verschlüsselungs Konzept und ein Profil angibt, das\-die schwächere WPA Enterprise-und TKIP-Verschlüsselung verwendet. In diesem Beispiel ist es von entscheidender Bedeutung, dass Sie das Profil, das\-WPA2 Enterprise und AES verwendet, in der Einstellungs Reihenfolge am höchsten platzieren. Computer, von denen WPA2\-Enterprise und AES nicht verwendet werden können, werden automatisch mit dem nächsten Profil in der bevorzugten Reihenfolge überspringen und das Profil, das WPA\-Enterprise und TKIP angibt, verarbeiten.

> [!IMPORTANT]
> Sie müssen das Profil mit den sichersten Standards in der geordneten Liste der Profile höher platzieren, da das Verbinden von Computern das erste Profil verwendet, das Sie verwenden können.

### <a name="planning-restricted-access-to-the-wireless-network"></a>Planen des eingeschränkten Zugriffs auf das Drahtlos Netzwerk

In vielen Fällen empfiehlt es sich, drahtlosen Benutzern unterschiedliche Zugriffsebenen für das Funk Netzwerk bereitzustellen. Beispielsweise kann es vorkommen, dass Sie Benutzern einen uneingeschränkten Zugriff auf jeden Tag der Woche gewähren möchten. Für andere Benutzer empfiehlt es sich, den Zugriff nur während der Haupt Zeit, Montag bis Freitag, zuzulassen und den Zugriff auf Samstag und Sonntag abzulehnen.

Dieses Handbuch enthält Anweisungen zum Erstellen einer Zugriffs Umgebung, in der alle drahtlosen Benutzer in einer Gruppe mit gemeinsamen Zugriff auf drahtlose Ressourcen platziert werden. Erstellen Sie im Active Directory Benutzer und Computer das Snap\--in "Benutzer und Computer", und legen Sie dann jeden Benutzer, dem Sie drahtlos Zugriff gewähren möchten, auf ein Mitglied dieser Gruppe fest.

Wenn Sie NPS-Netzwerk Richtlinien konfigurieren, geben Sie die Sicherheitsgruppe "drahtlose Benutzer" als das Objekt an, das NPS verarbeitet, wenn die Autorisierung bestimmt wird.

Wenn die Bereitstellung jedoch unterschiedliche Zugriffsebenen erfordert, müssen Sie nur folgende Aktionen ausführen:  

1. Erstellen Sie mehr als eine Sicherheitsgruppe für drahtlose Benutzer, um zusätzliche drahtlos Sicherheitsgruppen in Active Directory Benutzer und Computern zu erstellen. Beispielsweise können Sie eine Gruppe erstellen, die Benutzer mit Vollzugriff enthält, eine Gruppe für Benutzer, die nur während der regulären Arbeitszeiten Zugriff haben, und andere Gruppen, die mit Ihren Anforderungen übereinstimmen.

2. Fügen Sie Benutzer zu den entsprechenden Sicherheitsgruppen hinzu, die Sie erstellt haben.

3. Konfigurieren Sie zusätzliche NPS-Netzwerk Richtlinien für jede zusätzliche drahtlose Sicherheitsgruppe, und konfigurieren Sie die Richtlinien, um die Bedingungen und Einschränkungen anzuwenden, die Sie für die einzelnen Gruppen benötigen.

### <a name="planning-methods-for-adding-new-wireless-computers"></a>Planungsmethoden für das Hinzufügen neuer drahtlos Computer

Die bevorzugte Methode zum Einbinden neuer drahtlos Computer zur Domäne und zum Anmelden bei der Domäne ist die Verwendung einer kabelgebundenen Verbindung mit einem LAN des LANs, das Zugriff auf Domänen Controller hat und nicht durch einen 802.1 x-authentifizier enden Ethernet-Switch geschützt wird.

In einigen Fällen ist es jedoch möglicherweise nicht sinnvoll, eine kabelgebundene Verbindung zum Hinzufügen von Computern zur Domäne zu verwenden, oder, damit ein Benutzer eine kabelgebundene Verbindung für den ersten Anmeldeversuch mithilfe von Computern verwendet, die bereits mit der Domäne verbunden sind.

Wenn Sie einen Computer mithilfe einer drahtlos Verbindung zur Domäne hinzufügen oder Benutzer sich zum ersten Mal bei der Domäne anmelden möchten, indem Sie einen in\-die Domäne eingebundener Computer und eine drahtlos Verbindung verwenden, müssen drahtlose Clients zunächst eine Verbindung mit dem Drahtlos Netzwerk auf einem Segment, das mithilfe einer der folgenden Methoden Zugriff auf die Netzwerk Domänen Controller hat.

1. **Ein Mitglied des IT-Personals verbindet einen drahtlos Computer mit der Domäne und konfiguriert dann ein Bootstrap-drahtlos Profil für einmaliges Anmelden.** Bei dieser Methode verbindet ein IT-Administrator den drahtlos Computer mit dem verkabelten Ethernet-Netzwerk und verknüpft dann den Computer mit der Domäne. Dann verteilt der Administrator den Computer an den Benutzer. Wenn der Benutzer den Computer startet, werden die Domänen Anmelde Informationen, die für den Benutzer Anmeldevorgang manuell angegeben werden, verwendet, um eine Verbindung mit dem Drahtlos Netzwerk herzustellen und sich bei der Domäne anzumelden.  

2. **Der Benutzer konfiguriert den drahtlos Computer manuell mit einem Bootstrap-drahtlos Profil und fügt dann die Domäne an.** Mit dieser Methode konfigurieren Benutzer ihre drahtlos Computer manuell mit einem Bootstrap-drahtlos Profil, das auf Anweisungen von einem IT-Administrator basiert. Das Bootstrap-drahtlos Profil ermöglicht Benutzern das Herstellen einer drahtlos Verbindung und das anschließende Hinzufügen des Computers zur Domäne. Nachdem Sie den Computer der Domäne hinzufügen und den Computer neu gestartet haben, kann sich der Benutzer mit einer drahtlos Verbindung und seinen Anmelde Informationen für das Domänen Konto bei der Domäne anmelden.

Informationen zum Bereitstellen von drahtlos Zugriff finden Sie unter [Bereitstellung des drahtlos Zugriffs](e-wireless-access-deployment.md)
