---
title: Bereitstellung des Funkzugriffs
description: Dieses Thema ist Teil des Windows Server 2016-Networking Guide "Deploy Password-Based 802.1 X Authenticated Wireless Access"
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 4b66f517-b17d-408c-828f-a3793086bc1f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b2e237cee6eac6be809add37a2ac29fdf1c92118
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446493"
---
# <a name="wireless-access-deployment"></a>Bereitstellung des Funkzugriffs

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Um den drahtlosen Zugriff bereitzustellen, gehen Sie wie folgt vor:

- [Bereitstellung und Konfiguration von Drahtloszugriffspunkten](#bkmk_aps)

- [Erstellen einer Sicherheitsgruppe der Wireless-Benutzer](#bkmk_groups)

- [Konfigurieren von drahtlosen Netzwerk \(IEEE 802.11\) Richtlinien](#bkmk_policies)

- [Konfigurieren von NPSs](#bkmk_nps)

- [Verknüpfen der neuen Drahtloscomputer mit der Domäne](#bkmk_domain)

## <a name="bkmk_aps"></a>Bereitstellung und Konfiguration von Drahtloszugriffspunkten

Zum Bereitstellen und konfigurieren Ihre drahtlosen Zugriffspunkte, gehen Sie wie folgt vor:

- [Geben Sie die drahtlosen Zugriffspunkt Kanalfrequenzen](#bkmk_channel)

- [Konfigurieren von drahtlosen Zugriffspunkten](#bkmk_wirelessaps)

>[!NOTE]
>Die Verfahren in diesem Handbuch beinhalten keine Anweisungen für Fälle, in denen das Dialogfeld **Benutzerkontensteuerung** geöffnet wird, um die Zustimmung zum Fortfahren abzufragen. Klicken Sie auf **Weiter**, wenn das Dialogfeld während der Ausführung der Verfahren in dieser Anleitung geöffnet wird und als Folge der ausgeführten Aktionen geöffnet wurde.

### <a name="bkmk_channel"></a>Geben Sie die drahtlosen Zugriffspunkt Kanalfrequenzen

Wenn Sie mehrere Drahtloszugriffspunkte an einem geografischen Ort bereitstellen, müssen Sie drahtlose Zugriffspunkte konfigurieren, die überlappende Signale eindeutigen Kanalfrequenzen verwenden, um Störungen zwischen Drahtloszugriffspunkten zu reduzieren.

Sie können die folgenden Richtlinien verwenden, bei der bei der Auswahl von Channel-Frequenzen, die nicht mit anderen drahtlosen Netzwerken auf den geografischen Standort des Drahtlosnetzwerks in Konflikt stehen.

- Wenn es anderen Organisationen mit Niederlassungen in der Nähe oder im selben Gebäude als Ihrer Organisation, zu identifizieren, ob im Besitz von Organisationen drahtloser Netzwerke vorhanden sind. Erfahren Sie Häufigkeit ihrer drahtlosen APs, sowohl die Platzierung und den entsprechenden Kanal, da Sie Ihres Zugriffspunkts anderen Kanalfrequenzen zuweisen möchten, und Sie den besten Speicherort zum Installieren Ihres Zugriffspunkts zu bestimmen müssen

- Identifizieren Sie überlappende auf angrenzenden Stockwerken innerhalb Ihrer Organisation drahtlose Signale. Nach dem Identifizieren von überlappenden Abdeckungsbereiche außerhalb und innerhalb Ihrer Organisation zuweisen Kanalfrequenzen für Ihre drahtlosen Zugriffspunkte werden durch das sichergestellt wird, dass zwei drahtlosen APs mit sich möglicherweise überschneidenden Deckung anderen Kanalfrequenzen zugewiesen.

### <a name="bkmk_wirelessaps"></a>Konfigurieren von drahtlosen Zugriffspunkten

Verwenden Sie die folgende Informationen zusammen mit der Produktdokumentation des drahtlosen AP-Herstellers, um Ihre drahtlosen Zugriffspunkte zu konfigurieren.

Diese Prozedur Listet Elemente, die häufig auf einem drahtlosen Zugriffspunkt konfiguriert. Die Elementnamen je nach Marke und Modell variieren können, und es können sich von denen in der folgenden Liste werden. Spezifische Details finden Sie unter der drahtlose AP-Dokumentation.

#### <a name="to-configure-your-wireless-aps"></a>So konfigurieren Sie Ihre drahtlosen Zugriffspunkte  

- **SSID**. Geben Sie den Namen des Drahtlosnetzwerks\(s\) \(z. B. ExampleWLAN\). Dies ist der Name, der für drahtlose Clients angekündigt wird.

- **Verschlüsselung**. Geben Sie WPA2\-Enterprise \(bevorzugte\) oder WPA\-Enterprise und entweder AES \(bevorzugte\) oder TKIP-Verschlüsselungsverfahren, je nachdem, welche Versionen werden unterstützt Ihre Netzwerkkarten für den drahtlosen Client-Computers.

- **Wireless-Zugriffspunkt IP-Adresse \(statische\)** . Konfigurieren Sie für jeden Zugriffspunkt und eine eindeutige statische IP-Adresse, die innerhalb des Ausschlussbereichs ein, von dem DHCP-Bereich des Subnetzes liegt. Mit einer Adresse, die Zuweisung von DHCP ausgeschlossen wird verhindert, dass den DHCP-Server einen Computer oder einem anderen Gerät die gleiche IP-Adresse zuweisen.

- **Die Netzwerksubnetz-Maske**. Konfigurieren Sie diese entsprechend die Maske subnetzeinstellungen des LANS, mit dem Sie der Drahtloszugriffspunkt verbunden haben.  

- **DNS-Namen**. Einigen Drahtloszugriffspunkten können mit einem DNS-Namen konfiguriert werden. Der DNS-Dienst im Netzwerk kann DNS-Namen in eine IP-Adresse aufgelöst werden. Geben Sie für jeden drahtlosen Zugriffspunkt, der dieses Feature unterstützt wird einen eindeutigen Namen für die DNS-Auflösung.  

- **DHCP-Dienst**. Wenn Ihr drahtlose Zugriffspunkt eines integrierten verfügt\-im DHCP-Dienst deaktivieren.  

- **RADIUS-gemeinsamen geheimen Schlüssel**. Verwenden Sie einen eindeutigen RADIUS gemeinsamen geheimen Schlüssel für jeden drahtlosen Zugriffspunkt, es sei denn, Sie planen, konfigurieren Sie Zugriffspunkte als RADIUS-Clients in NPS auf Gruppenbasis. Wenn Sie APs auf Gruppenbasis in NPS konfigurieren möchten, muss der gemeinsame geheimen Schlüssel für jedes Mitglied der Gruppe identisch sein. Darüber hinaus sollte jede gemeinsamen geheimen Schlüssel, die, den Sie verwenden, eine zufällige Sequenz von mindestens 22 Zeichen, die Mischung aus Groß- und Kleinbuchstaben, Zahlen und Interpunktionszeichen. Um sicherzustellen, dass hinsichtlich Ihrer Zufälligkeit, können Sie einen zufälligen Zeichengenerator, z. B. der zufälligen Zeichengenerator finden Sie in der NPS **konfigurieren 802.1 X** Assistenten erstellen Sie den gemeinsamen geheimen Schlüssel.

>[!TIP]
>Notieren Sie den gemeinsamen geheimen Schlüssel für jeden drahtlosen Zugriffspunkt und in einem sicheren Speicherort, z. B. Office sicher zu speichern. Sie müssen den gemeinsamen geheimen Schlüssel für jeden drahtlosen Zugriffspunkt kennen, wenn Sie RADIUS-Clients in NPS konfigurieren.  

- **IP-Adresse des RADIUS-Servers**. Geben Sie die IP-Adresse des Servers, auf dem NPS ausgeführt wird.

- **UDP-Port\(s\)** . Standardmäßig verwendet NPS UDP-Ports 1812 und 1645 für die Authentifizierung von Nachrichten und UDP-Ports 1813 und 1646 für Kontoführungsnachrichten an. Es wird empfohlen, dass Sie die gleichen UDP-Ports für Ihre Zugriffspunkte, aber einen berechtigter Grund für unterschiedliche Ports verwenden, achten Sie darauf, dass Sie nicht nur die APs mit den neuen Portnummern konfigurieren aber auch alle Ihre NPSs verwenden dieselben Portnummern als APs neu konfiguriert werden. Wenn die Zugriffspunkten und dem NPSs nicht mit den gleichen UDP-Ports konfiguriert sind, NPS nicht empfangen oder verarbeitet verbindungsanforderungen von APs und allen drahtlosen Verbindung im Netzwerk nicht möglich.

- **Herstellerspezifische Attribute**. Einige drahtlose Zugriffspunkte müssen Hersteller\-bestimmte Attribute \(VSAs\) vollständige drahtlosen AP-Funktionalität bereitstellen. Herstellerspezifische Attribute werden in der Netzwerkrichtlinie für NPS hinzugefügt.

- **DHCP-Filterung**. Konfigurieren Sie drahtlose Zugriffspunkte zum drahtlosen Clients IP-Pakete von UDP-Port 68 zu senden, mit dem Netzwerk zu blockieren, wie vom drahtlosen AP Hersteller dokumentiert.

- **DNS-Filterung**. Konfigurieren von Drahtloszugriffspunkten, um drahtlose Clients IP-Pakete von TCP- oder UDP-Port 53 zu senden, mit dem Netzwerk zu blockieren, wie vom drahtlosen AP Hersteller dokumentiert.

## <a name="create-security-groups-for-wireless-users"></a>Erstellen Sie Sicherheitsgruppen für Mobiltelefone

Führen Sie diese Schritte aus, um eine oder mehrere drahtlose Benutzer Sicherheitsgruppen erstellen, und klicken Sie dann Hinzufügen von Benutzern zu der entsprechenden drahtlosen Sicherheitsgruppe:

- [Erstellen einer Sicherheitsgruppe der Wireless-Benutzer](#bkmk_groups)

- [Hinzufügen von Benutzern der Wireless-Sicherheitsgruppe](#bkmk_addusers)

### <a name="bkmk_groups"></a>Erstellen einer Sicherheitsgruppe der Wireless-Benutzer

Sie können dieses Verfahren zum Erstellen von einer Gruppe für die Sicherheit bei drahtlosen Verbindungen in der Active Directory-Benutzer und Computer MMC \(MMC\) ausrichten\-in.  

Sie müssen mindestens Mitglied der Gruppe **Domänen-Admins** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.

#### <a name="to-create-a-wireless-users-security-group"></a>Erstellen Sie eine Sicherheitsgruppe mit drahtlosem

1. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Active Directory-Benutzer und -Computer**. Das Snap-in Active Directory-Benutzer und-Computer\-in wird geöffnet. Klicken Sie auf den Knoten für Ihre Domäne, wenn diese noch nicht ausgewählt ist. Wenn Ihre Domäne beispielsweise den Namen „beispiel.com“ besitzt, klicken Sie auf **beispiel.com**.

2. Klicken Sie im Detailbereich der rechten Maustaste\-klicken Sie auf den Ordner, in dem Sie eine neue Gruppe hinzufügen möchten \(z. B. rechten\-klicken Sie auf **Benutzer**\), zeigen Sie auf **neu**, und klicken Sie dann auf **Gruppe**.

3. Geben Sie im Dialogfeld **Neues Objekt – Gruppe** in das Feld **Gruppenname** einen Namen für die neue Gruppe ein. Geben Sie z. B. **Drahtlosnetzwerken**.

4. Wählen Sie unter **Gruppenbereich** eine der folgenden Optionen aus:

    - **Lokale Domäne**

    - **Global**

    - **Universal**

5. Wählen Sie unter **Gruppentyp** die Option **Sicherheit** aus.

6. Klicken Sie auf **OK**.

Wenn Sie mehr als eine Sicherheitsgruppe für drahtlose Benutzer benötigen, wiederholen Sie diese Schritte aus, um zusätzliche drahtlose Benutzergruppen erstellen. Später können Sie einzelne Netzwerkrichtlinien in NPS, um unterschiedliche Bedingungen und für die Constraints auf jede Gruppe bereit, mit unterschiedlichen Zugriffsberechtigungen und Konnektivität Regeln anwenden erstellen.

### <a name="bkmk_addusers"></a> Hinzufügen von Benutzern zu der Sicherheitsgruppe der Wireless-Benutzer

Verwenden Sie dieses Verfahren, um einem Benutzer, Computer oder einer Gruppe Ihrer drahtlosen Sicherheitsgruppe in den Active Directory-Benutzer und Computer MMC hinzuzufügen \(MMC\) ausrichten\-in.

Für dieses Verfahren müssen Sie mindestens Mitglied der Gruppe **Domänen-Admins** oder einer gleichwertigen Gruppe sein.

#### <a name="to-add-users-to-the-wireless-security-group"></a>Die Sicherheit bei drahtlosen Verbindungen Gruppe Benutzer hinzufügen

1. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Active Directory-Benutzer und -Computer**. Das MMC-Snap-In %%amp;quot;Active Directory-Benutzer und -Computer%%amp;quot; wird geöffnet. Klicken Sie auf den Knoten für Ihre Domäne, wenn diese noch nicht ausgewählt ist. Wenn Ihre Domäne beispielsweise den Namen „beispiel.com“ besitzt, klicken Sie auf **beispiel.com**.

2. Doppelklicken Sie im Detailbereich,\-klicken Sie auf den Ordner mit Ihrer drahtlosen Sicherheitsgruppe.

3. Klicken Sie im Detailbereich der rechten Maustaste\-auf die Sicherheit bei drahtlosen Verbindungen-Gruppe, und klicken Sie dann auf **Eigenschaften**. Die **Eigenschaften** Dialogfeld für die Sicherheitsgruppe wird geöffnet.

4. Auf der **Mitglieder** auf **hinzufügen**, und schließen Sie dann eine der folgenden Verfahren, um einen Computer hinzufügen oder einen Benutzer oder Gruppe hinzufügen.

##### <a name="to-add-a-user-or-group"></a>Um einen Benutzer oder Gruppe hinzufügen

1. In **Geben Sie die zu verwendenden Objektnamen**, geben Sie den Namen des Benutzers oder Gruppe, die Sie hinzufügen möchten, und klicken Sie dann auf **OK**.

2. Um anderen Benutzern oder Gruppen die Gruppenmitgliedschaft zuzuweisen, wiederholen Sie Schritt 1 dieses Verfahrens aus.  

##### <a name="to-add-a-computer"></a>So fügen Sie einen Computer hinzu

1. Klicken Sie auf **Objekttypen**. Die **Objekttypen** Dialogfeld wird geöffnet.

2. In **Objekttypen**Option **Computer**, und klicken Sie dann auf **OK**.

3. In **Geben Sie die zu verwendenden Objektnamen**, geben Sie den Namen des Computers ein, die Sie hinzufügen möchten, und klicken Sie dann auf **OK**.

4. Wiederholen Sie Schritt 1, um die Gruppenmitgliedschaft auf anderen Computern zuzuweisen,\-3 dieses Verfahrens.

## <a name="bkmk_policies"></a>Konfigurieren von drahtlosen Netzwerk \(IEEE 802.11\) Richtlinien

Führen Sie diese Schritte zum Konfigurieren von Drahtlosnetzwerkrichtlinien \(IEEE 802.11\) gruppenrichtlinienerweiterung für Richtlinien:

- [Öffnen Sie oder fügen Sie hinzu, und öffnen Sie ein Gruppenrichtlinienobjekt](#bkmk_opengpme)

- [Aktivieren Sie die Standard-Drahtlosnetzwerk \(IEEE 802.11\) Richtlinien](#bkmk_activate)

- [Konfigurieren Sie die neue Richtlinie für Drahtlosnetzwerke](#bkmk_policyconfig)

### <a name="bkmk_opengpme"></a>Öffnen Sie oder fügen Sie hinzu, und öffnen Sie ein Gruppenrichtlinienobjekt

Standardmäßig ist das Feature "Gruppenrichtlinienverwaltung" installiert, auf Computern unter Windows Server 2016, wenn das Active Directory Domain Services \(AD DS\) -Serverrolle installiert ist, und der Server als Domänencontroller konfiguriert ist. Das folgende Verfahren, die beschreibt, wie Sie die Gruppenrichtlinien-Verwaltungskonsole öffnen \(GPMC\) auf Ihrem Domänencontroller. Das Verfahren wird beschrieben, wie zum Öffnen einer vorhandenen Domäne\-auf Gruppenrichtlinienobjekt \(GPO\) für die Bearbeitung oder eine neue Domäne ein Gruppenrichtlinienobjekt erstellen und zur Bearbeitung öffnen.

Sie müssen mindestens Mitglied der Gruppe **Domänen-Admins** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.

#### <a name="to-open-or-add-and-open-a-group-policy-object"></a>Zum Öffnen oder hinzufügen, und öffnen Sie ein Gruppenrichtlinienobjekt

1. Klicken Sie auf dem Domänencontroller auf **starten**, klicken Sie auf **Windows-Verwaltung**, und klicken Sie dann auf **Gruppenrichtlinienverwaltung**. Die Gruppenrichtlinien-Verwaltungskonsole wird geöffnet.  

2. Doppelklicken Sie im linken Bereich\-klicken Sie auf die Gesamtstruktur. Doppelklicken Sie z. B.\-klicken Sie auf **Gesamtstruktur: "example.com"** .  

3. Doppelklicken Sie im linken Bereich\-klicken Sie auf **Domänen**, und doppelklicken dann\-klicken Sie auf die Domäne, die für die Sie ein Gruppenrichtlinienobjekt verwalten möchten. Doppelklicken Sie z. B.\-klicken Sie auf **"example.com"** .  

4. Führen Sie eines der folgenden Verfahren aus:

    -   **Zum Öffnen einer vorhandenen Domäne\-Ebene Gruppenrichtlinienobjekt zur Bearbeitung**, doppelklicken klicken Sie auf die Domäne, die das Gruppenrichtlinienobjekt enthält, die Sie direkt verwalten möchten\-klicken Sie auf die Domänenrichtlinie, z. B. die Standarddomänenrichtlinie verwalten möchten, und klicken Sie dann auf **bearbeiten**. **Gruppenrichtlinienverwaltungs-Editor** wird geöffnet.

    -   **Erstellen ein neues Gruppenrichtlinienobjekt, und öffnen zum Bearbeiten von**mit der rechten Maustaste\-klicken Sie auf die Domäne für die Sie erstellen ein neues Gruppenrichtlinienobjekt, und klicken Sie dann auf möchten **erstellen Sie ein Gruppenrichtlinienobjekt in dieser Domäne, und hier**.

        In **neues Gruppenrichtlinienobjekt**im **Namen**, geben Sie einen Namen für das neue Gruppenrichtlinienobjekt, und klicken Sie dann auf **OK**.

        Rechts\-klicken Sie auf das neue Gruppenrichtlinienobjekt, und klicken Sie dann auf **bearbeiten**. **Gruppenrichtlinienverwaltungs-Editor** wird geöffnet.

Im nächsten Abschnitt verwenden Sie Gruppenrichtlinienverwaltungs-Editor zum Erstellen der Richtlinie für Drahtlosnetzwerke.

### <a name="bkmk_activate"></a>Aktivieren Sie die Standard-Drahtlosnetzwerk \(IEEE 802.11\) Richtlinien

Diesem Verfahren wird beschrieben, wie Sie die Standardeinstellung Wireless Network aktivieren \(IEEE 802.11\) Richtlinien über den Gruppenrichtlinienverwaltungs-Editor \(Gruppenrichtlinienverwaltungs-Editor\).

>[!NOTE]
>Nach dem Aktivieren der **Windows Vista und neuere Versionen** Version des drahtlosen Netzwerks \(IEEE 802.11\) Richtlinien oder **Windows XP** Version, die Version-Option ist aus der Liste der Optionen automatisch entfernt, wenn Sie nach rechts\-klicken Sie auf **Wireless Network \(IEEE 802.11\) Richtlinien**. Dies tritt auf, nachdem Sie eine Richtlinienversion auswählen, die Richtlinie im Detailbereich des Gruppenrichtlinienverwaltungs-Editor hinzugefügt wird bei der Auswahl der **Wireless Network \(IEEE 802.11\) Richtlinien** Knoten. Dieser Zustand bleibt, es sei denn, Sie die Richtlinie für drahtlose Netzwerke, löschen, zu diesem Zeitpunkt wird die Richtlinie für Drahtlosnetzwerke-Version auf der rechten Seite zurückgibt\-klicken Sie im Menü für **Drahtlosnetzwerk \(IEEE 802.11\) Richtlinien** im Gruppenrichtlinienverwaltungs-Editor . Darüber hinaus die WLAN-Richtlinien nur finden Sie im Detailbereich Gruppenrichtlinienverwaltungs-Editor bei den **Drahtlosnetzwerk \(IEEE 802.11\) Richtlinien** Knoten ist ausgewählt.

Sie müssen mindestens Mitglied der Gruppe **Domänen-Admins** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.

#### <a name="to-activate-default-wireless-network-ieee-80211-policies"></a>Zum Aktivieren der standardmäßigen Wireless Network \(IEEE 802.11\) Richtlinien  

1. Führen Sie die vorherige Schritte, **zu öffnen oder hinzufügen, und öffnen Sie ein Gruppenrichtlinienobjekt** um den Gruppenrichtlinienverwaltungs-Editor zu öffnen.

2. Doppelklicken Sie im Gruppenrichtlinienverwaltungs-Editor, klicken Sie im linken Bereich\-klicken Sie auf **Computerkonfiguration**, double\-klicken Sie auf **Richtlinien**, double\-klicken Sie auf **Windows-Einstellungen** , und doppelklicken dann\-klicken Sie auf **Sicherheitseinstellungen**.

![802.1 X-Wireless-Gruppenrichtlinie](../../../media/Wireless-GP/Wireless-GP.jpg)

3. In **Sicherheitseinstellungen**mit der rechten Maustaste\-klicken Sie auf **Wireless Network \(IEEE 802.11\) Richtlinien**, und klicken Sie dann auf **erstellen Sie eine neue Richtlinie für Drahtlosnetzwerke für Windows Vista und späteren Versionen**. 

![802.1 x-Richtlinie für Drahtlosnetzwerke](../../../media/Wireless-Policy/Wireless-Policy.jpg)

4. Die **Eigenschaften der neuen Drahtlosnetzwerkrichtlinie** Dialogfeld wird geöffnet. In **Richtlinienname**, geben Sie einen neuen Namen für die Richtlinie, oder behalten Sie den Standardnamen. Klicken Sie auf **OK** zum Speichern der Richtlinie. Die Standardrichtlinie ist aktiviert und im Detailbereich des Gruppenrichtlinienverwaltungs-Editor mit dem neuen Namen, die Sie angegeben haben, oder mit dem Standardnamen aufgeführt **neuen Drahtlosnetzwerkrichtlinie**.

![Eigenschaften der neuen Drahtlosnetzwerkrichtlinie](../../../media/Wireless-Policy-Properties/Wireless-Policy-Properties.jpg)

5. Doppelklicken Sie im Detailbereich,\-klicken Sie auf **neuen Drahtlosnetzwerkrichtlinie** um ihn zu öffnen.

Im nächsten Abschnitt können Sie die Richtlinienkonfiguration, Richtlinienreihenfolge der Verarbeitung und Netzwerkberechtigungen ausführen.

### <a name="bkmk_policyconfig"></a>Konfigurieren Sie die neue Richtlinie für Drahtlosnetzwerke

Können Sie die Verfahren in diesem Abschnitt zum Konfigurieren von Drahtlosnetzwerkrichtlinien \(IEEE 802.11\) Richtlinie. Diese Richtlinie können Sie Einstellungen für Sicherheit und Authentifizierung konfigurieren, verwalten WLAN-Profilen und Angeben von Berechtigungen für drahtlose Netzwerke, die nicht als bevorzugte Netzwerke konfiguriert sind.

- [Konfigurieren ein Drahtlosverbindungsprofils für PEAP\-MS\-CHAP-v2](#bkmk_configureprofile)  

- [Legen Sie die Priorität für drahtlose Verbindungsprofile](#bkmk_preferenceorder)  

- [Definieren von Netzwerkberechtigungen](#bkmk_permissions)  

#### <a name="bkmk_configureprofile"></a>Konfigurieren ein Drahtlosverbindungsprofils für PEAP\-MS\-CHAP-v2

Dieses Verfahren beschreibt die erforderlichen Schritte zum Konfigurieren einer PEAP\-MS\-CHAP-v2-Drahtlosprofil.  

Grundvoraussetzung für die Ausführung dieses Vorgangs ist die Mitgliedschaft in **Domänen-Admins** oder einer gleichwertigen Gruppe.

##### <a name="to-configure-a-wireless-connection-profile-for-peap-ms-chap-v2"></a>Konfigurieren ein drahtlosverbindungsprofils für PEAP\-MS\-CHAP-v2

1. Im Gruppenrichtlinienverwaltungs-Editor, in das Dialogfeld Eigenschaften von drahtlosen Netzwerk für die Richtlinie, die Sie gerade auf erstellt, die **allgemeine** Registerkarte und im **Beschreibung**, geben Sie eine kurze Beschreibung für die Richtlinie.

2. Um anzugeben, dass für die automatische WLAN-Konfiguration zum Konfigurieren der Einstellungen des Drahtlosnetzwerkadapters verwendet wird, stellen sicher, dass **verwenden Windows WLAN-Autokonfigurationsdienst für Clients** ausgewählt ist.  

3. In **Herstellen einer Verbindung mit der verfügbaren Netzwerke in der Reihenfolge der unten aufgelisteten Profile**, klicken Sie auf **hinzufügen**, und wählen Sie dann **Infrastruktur**. Die **neue Profileigenschaften** Dialogfeld wird geöffnet.

4. In der**neue Profileigenschaften** Dialogfeld auf die **Verbindung** Registerkarte die **Profilname** Feld, und geben Sie einen neuen Namen für das Profil. Geben Sie z. B. **"example.com" WLAN-Profil für Windows 10**.

5. In **Netzwerknamen\(s\) \(SSID\)** , geben Sie die SSID, die die für Ihre drahtlosen Zugriffspunkte konfigurierten SSID entspricht, und klicken Sie dann auf **hinzufügen**.

    Wenn Ihre Bereitstellung mehrere SSIDs verwendet und jeder drahtlose Zugriffspunkt dieselben Drahtlos-Sicherheitseinstellungen nutzt, wiederholen Sie diesen Schritt, um den SSID für jeden drahtlosen Zugriffspunkt hinzuzufügen, für den dieses Profil angewendet werden soll.

    Wenn Ihre Bereitstellung mehrere SSIDs verwendet und die Sicherheitseinstellungen für die einzelnen SSIDs nicht übereinstimmen, konfigurieren Sie ein separates Profil für jede Gruppe von SSIDs, die dieselben Sicherheitseinstellungen nutzen. Beispielsweise, wenn man eine Gruppe von drahtlosen Zugriffspunkten konfiguriert zur Verwendung von WPA2\-Enterprise und AES und eine andere Gruppe von drahtlosen Zugriffspunkten mit WPA\-Enterprise und TKIP, konfigurieren Sie ein Profil für jede Gruppe drahtloser Zugriffspunkte.

6. Wenn der Standardtext **NEWSSID** vorhanden ist, wählen Sie ihn, und klicken Sie dann auf **entfernen**.

7. Wenn Sie drahtlose Zugriffspunkte bereitgestellt haben, die das Übertragungssignal unterdrücken, wählen Sie **Verbinden, selbst wenn das Netzwerk keine Kennung aussendet**.

    > [!NOTE]
    > Durch Aktivieren dieser Option kann ein Sicherheitsrisiko erstellt werden, da drahtlose Clients für Test und Verbindungen zu einem beliebigen Drahtlosnetzwerk versucht. Standardmäßig ist diese Einstellung nicht aktiviert.  

8. Klicken Sie auf die Registerkarte **Sicherheit** und auf **Erweitert**, und konfigurieren Sie dann Folgendes:

    1. Um die erweiterten 802.1X-Einstellungen zu konfigurieren, wählen Sie bei **IEEE 802.1X** die Option **Erweiterte 802.1X-Einstellungen erzwingen**.

        Wenn die erweiterten 802.1X-Einstellungen erzwungen werden, die Standardwerte für **Max. Eapol\-Start-Meld**, **Wartezeitraum**, **Startzeitraum**, und  **Authentifizierungszeitraum** sind für typische drahtlosbereitstellungen ausreichend. Aus diesem Grund müssen Sie nicht die Standardeinstellungen zu ändern, es sei denn, Sie einen bestimmten Grund dafür haben.

    2. Um die einmalige Anmeldung zu aktivieren, wählen Sie **Einmaliges Anmelden für dieses Netzwerk aktivieren**.

    3. Die restlichen Standardwerte bei **Einmaliges Anmelden** sind für typische Drahtlosbereitstellungen ausreichend.

    4. In **für die schnelle Serverspeicherung**, wenn Ihr drahtlose Zugriffspunkt konfiguriert ist, für den Status vor\--Authentifizierung die Option **dieses Netzwerk verwendet ein vorab\-Authentifizierung**.

9. Um anzugeben, dass die Funkkommunikation mit FIPS 140 erfüllen\-2-Standards, Option **führen Sie die Kryptografie im FIPS 140\-2-zertifizierten Modus**.

10. Klicken Sie auf **OK**, um zur Registerkarte **Sicherheit** zurückzukehren. In **Sicherheitsmethoden für dieses Netzwerk auswählen**im **Authentifizierung**Option **WPA2\-Enterprise** , wenn sie von Ihrem drahtlosen Zugriffspunkt und Ihren drahtlosen unterstützt wird Client-Netzwerkadaptern. Wählen Sie andernfalls **WPA\-Enterprise**.

11. In **Verschlüsselung**, wenn von Ihrem drahtlosen Zugriffspunkt und Ihren drahtlosen Client-Netzwerkadaptern auf unterstützt **AES-CCMP**. Wenn Sie Zugriffspunkten und drahtlosen Netzwerkadaptern, die 802. 11ac unterstützen verwenden, wählen Sie **AES-GCMP**. Wählen Sie andernfalls **TKIP**.

    > [!NOTE]  
    > Die Einstellungen für **Authentifizierung** und **Verschlüsselung** für Ihre drahtlosen Zugriffspunkte konfigurierten Einstellungen übereinstimmen. Die Standardeinstellungen für **Authentifizierungsmodus**, **Max. Authentifizierungsfehler**, und **Benutzerinformationen für zukünftige Verbindungen mit diesem Netzwerk zwischenspeichern** sind für typische drahtlosbereitstellungen ausreichend.  

12. In **Netzwerkauthentifizierungsmethode auswählen**Option **Protected EAP \(PEAP\)** , und klicken Sie dann auf **Eigenschaften**. Die **Eigenschaften für geschütztes EAP** Dialogfeld wird geöffnet.

13. In **Eigenschaften für geschütztes EAP**, überprüfen Sie, ob **die Identität des Servers mittels zertifikatprüfung überprüfen** ausgewählt ist.

14. In **vertrauenswürdige Stammzertifizierungsstellen**, wählen Sie den vertrauenswürdigen Stammzertifizierungsstelle \(Zertifizierungsstelle\) , die das Serverzertifikat ausgestellt, für den NPS.

    > [!NOTE]  
    > Diese Einstellung beschränkt die Stamm-CAs, denen Clients vertrauen, auf die ausgewählten CAs. Wenn keine vertrauenswürdigen Stammzertifizierungsstellen ausgewählt sind, klicken Sie dann vertrauen die Clients allen Stamm-CAs, die in ihrem Zertifikatspeicher vertrauenswürdige Stammzertifizierungsstellen aufgeführt.  

15. In der **Authentifizierungsmethode auswählen** wählen **gesichertes Kennwort \(EAP\-MS\-CHAP-v2\)** .

16. Klicken Sie auf **Konfigurieren**. In der **EAP-MSCHAPv2-Eigenschaften** Dialogfeld überprüfen Sie, ob **verwenden automatisch eigenen Windows-Anmeldenamen und Kennwort \(und Domäne, falls vorhanden\)**  ausgewählt ist, und klicken Sie auf  **OK**.

17. Um PEAP schnelle Wiederherstellung der Verbindung zu aktivieren, stellen sicher, dass **ermöglichen die schnelle Verbindungswiederherstellung** ausgewählt ist.

18. Wählen Sie zum Server Kryptografiebindungs-TLV auf versucht, eine Verbindung zu erfordern, **getrennt wird, wenn Server kein Kryptografiebindungs-TLV vorweist**.

19. Um anzugeben, dass die Identität des Benutzers in Phase 1 der Authentifizierung maskiert sind, wählen Sie **Identitätsschutz aktivieren**, und klicken Sie im Textfeld Geben Sie einen Namen für die anonyme Identität, oder lassen Sie das Textfeld leer.

    > [!HINWEISE]
    > - Die NPS-Richtlinie für 802.1 X (verkabelt) muss erstellt werden, mit dem Netzwerkrichtlinienserver **Verbindungsanforderungsrichtlinie**. Wenn die NPS-Richtlinie erstellt wurde, mit dem Netzwerkrichtlinienserver **Netzwerkrichtlinie**, Identitätsschutz nicht funktioniert.
    > - EAP-Identitätsschutz erfolgt über bestimmte EAP-Methoden, wenn eine leere oder eine anonyme Identität \(unterscheidet die tatsächliche Identität\) als Antwort auf die EAP-identitätsanforderung gesendet wird. PEAP sendet die Identität während der Authentifizierung zweimal an. In der ersten Phase werden die Identität wird als Klartext gesendet, und diese Identität für Routingzwecke, nicht für die Clientauthentifizierung verwendet wird. Die tatsächliche Identität – für die Authentifizierung verwendet, erhält jedes Mal in der zweiten Phase der Authentifizierung, in der sichere Tunnel, die in der ersten Phase hergestellt wird. Wenn **Identitätsschutz aktivieren** aktiviert ist, wird der Benutzername mit dem Eintrag im Textfeld für die angegebene ersetzt. Nehmen wir beispielsweise an **Identitätsschutz aktivieren** ausgewählt ist und der Datenschutz-Identitätsalias **anonyme** angegeben ist, in das Textfeld ein. Für einen Benutzer mit einem echten Identitätsalias <strong>jdoe@example.com</strong>, die Identität, die in der ersten Phase der Authentifizierung gesendet wird geändert werden <strong>anonymous@example.com</strong>. Der Realm-Abschnitt, der Identität des 1. Phase wird nicht geändert werden, da sie für das routing verwendet wird.  

20. Klicken Sie auf **OK** schließen die **Eigenschaften für geschütztes EAP** Dialogfeld.
21. Klicken Sie auf **OK** schließen die **Sicherheit** Registerkarte.
22. Wenn Sie weitere Profile erstellen möchten, klicken Sie auf **hinzufügen**, und wiederholen Sie die vorherigen Schritten haben unterschiedliche Entscheidungen zum Anpassen von jedes Profil für die drahtlose Clients und das Netzwerk an, das Profil angewendet werden sollen. Wenn Sie das Hinzufügen von Profilen fertig sind, klicken Sie auf **OK** um das Dialogfeld Eigenschaften der Drahtlosnetzwerkrichtlinie zu schließen.

Im nächsten Abschnitt können Sie die Richtlinienprofile für eine optimale Sicherheit bestellen.

#### <a name="bkmk_preferenceorder"></a>Legen Sie die Priorität für drahtlose Verbindungsprofile
Sie können dieses Verfahren verwenden, wenn Sie mehrere WLAN-Profilen in Ihrer Richtlinie für Drahtlosnetzwerke erstellt haben, und Sie die Profile für eine optimale Effizienz und Sicherheit sortieren möchten.

Um sicherzustellen, dass die drahtlosen Clients eine Verbindung mit der höchsten Sicherheit herstellen, die sie unterstützen können, platzieren Sie die am stärksten einschränkende Richtlinien am oberen Rand der Liste aus.

Platzieren Sie das höher WPA2-Profil in der Liste z. B. Wenn Sie über zwei Profile, eine für Clients, die WPA2 unterstützen und eine für Clients, die WPA-Unterstützung verfügen. Dadurch wird sichergestellt, dass die Clients, die WPA2 unterstützen diese Methode für die weniger sichere WPA, anstatt die Verbindung verwendet.

Dieses Verfahren beschreibt die Schritte aus, um die Reihenfolge anzugeben, in der drahtlosen Verbindung von Profilen zur drahtlosen Clients von Domäne Member zu Drahtlosnetzwerken herzustellen.

Grundvoraussetzung für die Ausführung dieses Vorgangs ist die Mitgliedschaft in **Domänen-Admins** oder einer gleichwertigen Gruppe.

##### <a name="to-set-the-preference-order-for-wireless-connection-profiles"></a>Die bevorzugte Reihenfolge für drahtlose Verbindungsprofile festlegen

1. Klicken Sie im Gruppenrichtlinienverwaltungs-Editor, in das Dialogfeld Eigenschaften von drahtlosen Netzwerk für die Richtlinie, die Sie gerade konfiguriert haben, auf die **allgemeine** Registerkarte.

2. Auf der **allgemeine** Registerkarte **Herstellen einer Verbindung mit der verfügbaren Netzwerke in der Reihenfolge der unten aufgelisteten Profile**, wählen Sie das Profil, das Sie in der Liste verschieben möchten, und klicken Sie dann entweder "Pfeil nach oben" oder "Pfeil nach unten" Schaltfläche, um das Profil an die gewünschte Position in der Liste zu verschieben.

3.  Wiederholen Sie Schritt 2 für jedes Profil, das Sie in der Liste verschieben möchten.  

4.  Klicken Sie auf **OK** um alle Änderungen zu speichern.

Im folgenden Abschnitt können Sie die Netzwerkberechtigungen für die Drahtlosnetzwerkrichtlinie definieren.

#### <a name="bkmk_permissions"></a>Definieren von Netzwerkberechtigungen
Sie können Einstellungen konfigurieren, auf der **Netzwerkberechtigungen** Registerkarte für die Mitglieder der Domäne, der Wireless Network \(IEEE 802.11\) Richtlinien anwenden.

Kann nur angewendet werden die folgenden Einstellungen für drahtlose Netzwerke, die nicht konfiguriert sind die **allgemeine** Registerkarte die **drahtlosen Netzwerkrichtlinieneigenschaften** Seite:

- Zulassen oder Verweigern von Verbindungen mit bestimmten Drahtlosnetzwerken, die Sie angeben, durch den Typ des Netzwerks und Service Set Identifier \(SSID\)

- Zulassen oder Verweigern von Verbindungen mit ad-hoc-Netzwerken

- Zulassen oder Verweigern von Verbindungen mit Infrastrukturnetzwerken

- Zulassen oder Verweigern von Benutzern für die Anzeige von Netzwerktypen \(Ad-Hoc- oder Infrastruktur\) , deren Zugriff verweigert

- Zulassen oder Verweigern von Benutzern, die ein Profil zu erstellen, die für alle Benutzer gilt

- Benutzer können nur zugelassene Netzwerke eine Verbindung mithilfe von Gruppenrichtlinien-Profilen

Mitgliedschaft in **Domänen-Admins**, oder einer entsprechenden Gruppe sein, um diese Verfahren abzuschließen.

##### <a name="to-allow-or-deny-connections-to-specific-wireless-networks"></a>Zulassen oder verweigern Verbindungen mit bestimmten Drahtlosnetzwerken

1. Klicken Sie im Gruppenrichtlinienverwaltungs-Editor, klicken Sie im Dialogfeld mit den Eigenschaften der drahtlosen Netzwerk auf die **Netzwerkberechtigungen** Registerkarte.

2. Auf der **Netzwerkberechtigungen** auf **hinzufügen**. Die **Neuer Berechtigungseintrag** Dialogfeld wird geöffnet.

3. In der **Neuer Berechtigungseintrag** Dialogfeld die **Netzwerknamen \(SSID\)**  Feld Geben Sie die Netzwerk-SSID des Netzwerks für die Sie, um Berechtigungen zu definieren möchten.

4.  In **Netzwerktyp**Option **Infrastruktur** oder **Ad-hoc-** .

    > [!NOTE]  
    > Wenn Sie unsicher sind, ob das Netzwerk für die Übertragung einer Infrastruktur oder die ad-hoc-Netzwerk ist, können Sie zwei Netzwerk Berechtigung einen Eintrag für jeden Netzwerk konfigurieren.

5. In **Berechtigung**Option **zulassen** oder **Verweigern**.

6. Klicken Sie auf **OK**, zum Zurückgeben der **Netzwerkberechtigungen** Registerkarte.

##### <a name="to-specify-additional-network-permissions-optional"></a>Zusätzliche Netzwerkberechtigungen angeben, \(Optional\)

1.  Auf der **Netzwerkberechtigungen** konfigurieren eine oder alle der folgenden:  

    -   Wählen Sie zum Verweigern von Zugriff auf ad-hoc-Netzwerken Ihrer Mitglieder der Domäne **zu verhindern, dass Verbindungen mit Ad\-hoc-Netzwerken**.

    -   Wählen Sie zum Verweigern von Ihrer Mitglieder der Domäne den Zugriff auf Infrastrukturnetzwerken **Verbindungen mit Infrastrukturnetzwerken verhindern**.  

    -   Ihre Domänenmitglieder Netzwerktypen anzeigen dürfen \(Ad-Hoc- oder Infrastruktur\) an, sie sind, wählen Sie den Zugriff verweigert **Benutzer erlauben, Anzeigen von abgelehnten Netzwerken**.

    -   Damit Benutzer Profile erstellen, die für alle Benutzer gilt, wählen Sie **können alle Benutzer alle Benutzerprofile erstellen**.

    -   Wählen, um anzugeben, dass Ihre Benutzer können nur zulässige Netzwerke mithilfe von Gruppenrichtlinien Profilen verbinden **nur Gruppenrichtlinienprofile für zulässige Netzwerke verwenden**.

## <a name="bkmk_nps"></a>Konfigurieren Sie Ihre NPSs
Um NPSs Durchführung der 802.1X-Authentifizierung für den drahtlosen Zugriff zu konfigurieren, gehen Sie wie folgt vor:

- [Registrierung von NPS in Active Directory-Domänendienste](#bkmk_npsreg)

- [Konfigurieren von einem Drahtloszugriffspunkt als NPS RADIUS-Client](#bkmk_radiusclient)

- [Erstellen Sie die NPS-Richtlinien für 802.1 X (verkabelt) mithilfe eines Assistenten](#bkmk_npspolicy)

### <a name="bkmk_npsreg"></a>Registrierung von NPS in Active Directory-Domänendienste
Sie können dieses Verfahren verwenden, Registrieren eines Servers, der Netzwerkrichtlinienserver ausgeführt \(NPS\) in Active Directory Domain Services \(AD DS\) in der Domäne, in dem der NPS Mitglied ist. Für NPSs zu gewährenden Berechtigung zum Lesen der Drehknopf\-in den Eigenschaften von Benutzerkonten während des Autorisierungsprozesses, muss jedes NPS in AD DS registriert werden. Registrieren einen NPS, fügt den Server die **RAS- und IAS-Server** Sicherheitsgruppe in AD DS.

>[!NOTE]
>Sie können NPS auf einem Domänencontroller oder auf einem dedizierten Server installieren. Führen Sie den folgenden Windows PowerShell-Befehl, um NPS zu installieren, wenn Sie noch nicht getan haben:
    
    Install-WindowsFeature NPAS -IncludeManagementTools
    
Grundvoraussetzung für die Ausführung dieses Vorgangs ist die Mitgliedschaft in **Domänen-Admins** oder einer gleichwertigen Gruppe.

#### <a name="to-register-an-nps-in-its-default-domain"></a>So registrieren Sie einen Netzwerkrichtlinienserver in der Standarddomäne

1. Auf Ihrem NPS in **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Der NPS-snap\-in wird geöffnet.

2. Rechts\-klicken Sie auf **NPS \(lokalen\)** , und klicken Sie dann auf **Server in Active Directory registrieren**. Das Dialogfeld **Netzwerkrichtlinienserver** wird geöffnet.

3. Klicken Sie im Dialogfeld **Netzwerkrichtlinienserver** auf **OK**, und klicken Sie erneut auf **OK**.

### <a name="bkmk_radiusclient"></a>Konfigurieren von einem Drahtloszugriffspunkt als NPS RADIUS-Client
Sie können dieses Verfahren verwenden, konfigurieren Sie eine App, auch bekannt als eine *Netzwerkzugriffsservers \(NAS\)* , wie ein Remote Authentication Dial\-In User Service \(RADIUS\) Client mithilfe der NPS-Snap\-in. 

>[!IMPORTANT]
>Clientcomputer, z. B. tragbare Computer und andere Computer, auf denen Clientbetriebssysteme ausgeführt werden, sind keine RADIUS-Clients. RADIUS-Clients sind Netzwerkzugriffsserver – z. B. Drahtloszugriffspunkte, 802.1 X\-fähigen Switches, virtuelles privates Netzwerk \(-VPN-\) -Server, und wählen\-Server einrichten, da sie das RADIUS-Protokoll zu verwenden die Kommunikation mit RADIUS-Servern, z. B. NPSs.

Grundvoraussetzung für die Ausführung dieses Vorgangs ist die Mitgliedschaft in **Domänen-Admins** oder einer gleichwertigen Gruppe.

#### <a name="to-add-a-network-access-server-as-a-radius-client-in-nps"></a>Hinzufügen ein Netzwerk-Servers als RADIUS-Client auf dem Netzwerkrichtlinienserver

1. Auf Ihrem NPS in **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Der NPS-snap\-in wird geöffnet.

2. In der NPS ausrichten\-doppelklicken,\-klicken Sie auf **RADIUS-Clients und Servern**. Rechts\-klicken Sie auf **RADIUS-Clients**, und klicken Sie dann auf **neu**.

3. In **Neuer RADIUS-Client**, überprüfen Sie, ob die **aktivieren Sie dieses RADIUS-Clients** das Kontrollkästchen aktiviert ist.

4. In **Neuer RADIUS-Client**im **Anzeigenamen**, geben Sie einen Anzeigenamen für den drahtlosen Zugriffspunkt.

    Angenommen, Sie einen drahtlosen Zugriffspunkt hinzufügen möchten \(AP\) mit dem Namen AP\-01, Typ **AP\-01**.

5. In **Adresse \(IP-Adresse oder DNS-\)** , geben Sie den IP-Adresse oder den vollständig qualifizierten Domänennamen \(FQDN\) des Netzwerkzugriffsservers.

    Um sicherzustellen, dass der Name richtig ist und ordnet eine gültige IP-Adresse ein, wenn Sie den vollqualifizierten Domänennamen eingeben, klicken Sie auf **überprüfen**, und klicken Sie dann im **Adresse überprüfen**in die **Adresse** auf  **Beheben**. Wenn der FQDN-Name in eine gültige IP-Adresse zugeordnet ist, wird die IP-Adresse, NAS automatisch in angezeigt **IP-Adresse**. Wenn der FQDN nicht zu einer IP-Adresse aufgelöst werden kann, dass Sie erhalten eine Meldung gibt an, dass der angegebene Host ist unbekannt. In diesem Fall stellen Sie sicher, dass Sie den richtigen AP-Namen verwenden und der Zugriffspunkt eingeschaltet und mit dem Netzwerk verbunden ist.  

    Klicken Sie auf **OK** schließen **überprüfen Adresse**.  

6. In **Neuer RADIUS-Client**im **gemeinsamer geheimer Schlüssel**, führen Sie einen der folgenden:  

    -   Um einen RADIUS-gemeinsamen geheimen Schlüssel manuell zu konfigurieren, wählen **manuelle**, und klicken Sie dann im **gemeinsamer geheimer Schlüssel**, geben Sie das starke Kennwort, die auch auf dem NAS eingegeben werden. Geben Sie den gemeinsamen geheimen Schlüssel im **gemeinsamen geheimen Schlüssel bestätigen**.  

    -   Um einen gemeinsamen geheimen Schlüssel automatisch generieren zu können, wählen die **generieren** , und klicken Sie dann auf die **generieren** Schaltfläche. Speichern Sie den generierten gemeinsamen geheimen Schlüssel ein, und dann verwenden Sie diesen Wert, das NAS so konfigurieren, dass er mit der NPS kommunizieren kann.  

        >[!IMPORTANT]
        >Der RADIUS-gemeinsame geheime Schlüssel, den Sie für Ihre virtuellen APS in NPS eingeben muss das gemeinsame Geheimnis des RADIUS-genau übereinstimmen, das auf Ihren tatsächlichen drahtlosen Zugriffspunkts konfiguriert ist Wenn Sie die NPS-Option verwenden, um einen RADIUS-gemeinsamen geheimen Schlüssel zu generieren, müssen Sie der entsprechenden tatsächlichen Drahtloszugriffspunkt mit dem gemeinsamen geheimen RADIUS-Schlüssel konfigurieren, die vom NPS generiert wurde.

7. In **Neuer RADIUS-Client**auf die **erweitert** Registerkarte **Herstellername**, geben Sie den Namen der NAS-Hersteller. Wenn Sie nicht über den Herstellernamen NAS sicher sind, wählen Sie **RADIUS-Standards**.

8. In **zusätzliche Optionen**, sofern andere Authentifizierungsmethoden als EAP und PEAP verwenden, und wenn Ihre NAS über die Verwendung des Attributs Authenticator Nachricht, unterstützt wählen Sie **müssen Access-Request-Meldungen enthalten die Nachricht\-Authenticator Attribut**.

9. Klicken Sie auf **OK**. Ihre NAS wird angezeigt, in der Liste der RADIUS-Clients, die für den NPS konfiguriert.

### <a name="bkmk_npspolicy"></a>Erstellen Sie die NPS-Richtlinien für 802.1 X (verkabelt) mithilfe eines Assistenten
Sie können dieses Verfahren verwenden, erstellen Sie die Verbindung Request-Richtlinien und Netzwerkrichtlinien, die zum Bereitstellen von entweder 802.1X-Authentifizierung erforderlich\-funkzugriffspunkte als Remote Authentication Dial\-In User Service \(RADIUS\) Clients an den RADIUS-Server, Netzwerkrichtlinienserver ausgeführt \(NPS\).  
Nachdem Sie den Assistenten ausführen, werden die folgenden Richtlinien erstellt:

- Eine Verbindungsanforderungsrichtlinie

- Eine Netzwerkrichtlinie

>[!NOTE]
>Sie können den Assistenten für neue IEEE 802.1 X Secure verkabelte und drahtlose ausführen, jedes Mal, wenn Sie neue Richtlinien für den Zugriff mit 802.1X-Authentifizierung erstellen möchten.

Grundvoraussetzung für die Ausführung dieses Vorgangs ist die Mitgliedschaft in **Domänen-Admins** oder einer gleichwertigen Gruppe.

#### <a name="create-policies-for-8021x-authenticated-wireless-by-using-a-wizard"></a>Erstellen von Richtlinien für 802.1 X authentifizierte drahtlose mithilfe ein Assistenten

1. Öffnen der NPS-snap\-in. Wenn sie nicht bereits ausgewählt ist, klicken Sie auf **NPS \(lokalen\)** . Wenn Sie die NPS-MMC-Snap ausführen\-in und Erstellen von Richtlinien auf einem Remoteserver NPS, wählen Sie den Server.

2. In **Einstieg**im **Standardkonfiguration**Option **RADIUS-Server für 802.1 X drahtlose oder verkabelte 802.1X-Verbindungen**. Der Text und Links unter den Text ändern sich entsprechend Ihrer Auswahl.

3. Klicken Sie auf **konfigurieren 802.1 X**. Das Konfigurieren von 802.1 X-Assistent wird geöffnet.

4.  Auf der **wählen 802.1 X Verbindungen** Assistentenseite **Typ von 802.1 X-Verbindungen**Option **sichere drahtlose Verbindungen**, und klicken Sie in **Namen**, geben Sie einen Namen für Ihre Richtlinie ein, oder übernehmen Sie den Standardnamen **sichere drahtlose Verbindungen**. Klicken Sie auf **Weiter**.

5.  Auf der **802.1 X-Schalter angeben** Assistentenseite **RADIUS-Clients**, alle 802.1 X-Switches und funkzugriffspunkte, die Sie als RADIUS-Clients, in der NPS-Snap hinzugefügt haben\-in werden angezeigt. Führen Sie eine der folgenden Aktionen durch:

    -   Hinzufügen von weiteren Netzwerkzugriffsservern \(NAS\), z. B. Drahtloszugriffspunkte, in **RADIUS-Clients**, klicken Sie auf **hinzufügen**, und klicken Sie dann im **Neuer RADIUS-Client**, geben Sie die Informationen für: **Anzeigename des**, **Adresse \(IP-Adresse oder DNS-\)** , und **gemeinsamer geheimer Schlüssel**.

    -   So ändern Sie die Einstellungen für alle NAS in **RADIUS-Clients**, wählen Sie den Zugriffspunkt für die Sie ändern die Einstellungen, und klicken Sie dann auf möchten **bearbeiten**. Ändern Sie die Einstellungen nach Bedarf.

    -   So entfernen Sie ein NAS in der Liste in **RADIUS-Clients**, wählen Sie das NAS, und klicken Sie dann auf **entfernen**.

        >[!WARNING]
        >Entfernen einen RADIUS-Client innerhalb der **konfigurieren 802.1 X** Assistent löscht den Client aus der NPS-Konfiguration. Alle Hinzufügungen, Änderungen und löschungen, die Sie, in vornehmen der **konfigurieren 802.1 X** Assistenten, um RADIUS-Clients in NPS widergespiegelt, Snap\-in, in der **RADIUS-Clients** Knoten unter  **NPS** \/ **RADIUS-Clients und Servern**. Z. B. Wenn Sie den Assistenten verwenden, um eine 802.1X-Switch zu entfernen, der Schalter ist ebenfalls entfernt von der NPS Snap\-in.

6. Klicken Sie auf **Weiter**. Auf der **Konfigurieren einer Authentifizierungsmethode** Assistentenseite **Typ \(basierend auf Zugriffs- und Netzwerkfehlern Konfigurationsmethode\)** Option **Microsoft: Geschütztes EAP \(PEAP\)** , und klicken Sie dann auf **konfigurieren**.

    >[!TIP]
    >Wenn Sie eine Fehlermeldung, der angibt, dass ein Zertifikat wurde nicht für die Verwendung mit der Authentifizierungsmethode gefunden, und Sie die Active Directory Certificate Services, um automatisch RAS- und IAS-Server in Ihrem Netzwerk zuerst Zertifikate konfiguriert haben Stellen Sie sicher, dass Sie die Schritte zum Registrieren von NPS in Active Directory-Domänendienste ausgeführt haben, und verwenden die folgenden Schritte aus, um die Gruppenrichtlinien aktualisieren: Klicken Sie auf **starten**, klicken Sie auf **Windows System**, klicken Sie auf **ausführen**, und klicken Sie in **öffnen**, Typ **Gpupdate**, und klicken Sie dann Drücken Sie die EINGABETASTE. Wenn der Befehl gibt an, dass sowohl die Benutzer-als auch die Gruppenrichtlinie des Computers erfolgreich aktualisiert wurden Ergebnisse zurückgegeben wird, wählen Sie **Microsoft: Geschütztes EAP \(PEAP\)**  erneut, und klicken Sie dann auf **konfigurieren**.
    >
    >Wenn nach der Aktualisierung der Gruppenrichtlinie, die Sie weiterhin die Fehlermeldung angezeigt, der angibt, dass ein Zertifikat für die Verwendung mit der Authentifizierungsmethode gefunden werden kann, wird das Zertifikat nicht angezeigt, da sie nicht das Serverzertifikat für die Mindestanforderungen erfüllt Anforderungen an, wie in der Core Network Companion Guide: [Bereitstellen von Serverzertifikaten für 802.1X-authentifizierte Kabelnetzwerke und Drahtlosnetzwerke Bereitstellungen](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments). In diesem Fall muss die NPS-Konfiguration einstellen, Sperren Sie das Zertifikat ausgestellt für den NPS\(s\), und befolgen Sie dann die Anweisungen, um ein neues Zertifikat zu konfigurieren, indem Sie im Bereitstellungshandbuch für Server-Zertifikate verwenden.

7.  Auf der **Eigenschaften für geschütztes EAP bearbeiten** Assistentenseite **ausgestelltes Zertifikat**, stellen Sie sicher, dass das richtige Zertifikat für den NPS aktiviert ist, und führen Sie Folgendes:

    >[!NOTE]
    >Überprüfen Sie, ob der Wert in **Aussteller** ist korrekt für das Zertifikat, das in ausgewählten **ausgestelltes Zertifikat**. Z. B. den erwarteten Aussteller für ein Zertifikat von einer Zertifizierungsstelle mit Active Directory Certificate Services \(AD CS\) ist mit dem Namen corp\DC1, in der Domäne "contoso.com" **corp\-DC1\-Zertifizierungsstelle**.

    -   Damit Benutzer mit ihren Drahtloscomputer zwischen Zugriffspunkte ohne diese jedes Mal erneut authentifizieren, ordnen sie eine neue Anwendung wechseln können, wählen Sie **ermöglichen die schnelle Verbindungswiederherstellung**.

    -   Um anzugeben, dass die Verbindung von drahtlosen Clients die Netzwerkauthentifizierungsprozess beenden wird, wenn der RADIUS-Server kein Kryptografiebindungs Typ vorweist\-Länge\-Wert \(TLV\)Option **trennen Clients ohne Kryptografiebindung**.  

    -   Um die Richtlinie ändern, Einstellungen für das EAP eingeben, in **EAP-Typen**, klicken Sie auf **bearbeiten**im **EAP-MSCHAPv2-Eigenschaften**, ändern Sie die Einstellungen nach Bedarf, und klicken Sie dann auf **OK**.  

8.  Klicken Sie auf **OK**. Das Dialogfeld "Eigenschaften für geschütztes EAP bearbeiten" wird geschlossen und Sie die **konfigurieren 802.1 X** Assistenten. Klicken Sie auf **Weiter**.

9. In **Benutzergruppen angeben**, klicken Sie auf **hinzufügen**, und geben Sie den Namen der Sicherheitsgruppe, die Sie konfiguriert haben, für die drahtlosen Clients in Active Directory-Benutzer und Computer ausrichten\-in. Geben Sie beispielsweise, wenn Sie Ihre drahtlose Sicherheitsgruppe Drahtlosnetzwerken genannt, **Drahtlosnetzwerken**. Klicken Sie auf **Weiter**.

10. Klicken Sie auf **konfigurieren** so konfigurieren Sie RADIUS-Standardattribute und Hersteller\-bestimmte Attribute für die virtuellen LAN \(VLAN\) je nach Bedarf, und als gemäß der Dokumentation Ihrer drahtlose AP-Hardwarehersteller. Klicken Sie auf **Weiter**.

11. Überprüfen Sie die Konfigurationsdetails für die Zusammenfassung, und klicken Sie dann auf **Fertig stellen**.

Die NPS-Richtlinien sind jetzt erstellt, und Sie können fortfahren, drahtlose Computer zur Domäne hinzugefügt.

## <a name="bkmk_domain"></a>Verknüpfen der neuen Drahtloscomputer mit der Domäne
Die einfachste Methode zum neuen Drahtloscomputer mit der Domäne zu verknüpfen ist physisch Anfügen von dem Computer an ein verkabeltes LAN-Segment \(ein Segment, das nicht von einer 802.1X-Switch kontrolliert\) vor dem Hinzufügen des Computers zur Domäne. Dies ist am einfachsten, da drahtlose gruppenrichtlinieneinstellungen sofort und automatisch angewendet und, wenn Sie Ihre eigene PKI bereitgestellt haben, dem Computer, empfängt das ZS-Zertifikat, und platziert sie in den Zertifikatspeicher vertrauenswürdige Stammzertifizierungsstellen, zulassen, dass der drahtlose Client, NPSs mit Server-Zertifikate, die von der Zertifizierungsstelle ausgestellten zu vertrauen.

Nachdem Sie ein neuer Drahtloscomputer mit der Domäne angehört, ist die bevorzugte Methode für Benutzer mit der Domäne anmelden ebenso Log auf Ausführen, mithilfe einer Kabelverbindung zum Netzwerk.

### <a name="other-domain-join-methods"></a>Andere Methoden für den Domänenbeitritt
In Fällen, in denen es nicht müssen sehr praktisch, Hinzufügen von Computern zur Domäne mit einem Ethernet-Kabelverbindung oder in Fällen, in denen der Benutzer nicht anmelden kann, bei der Domäne zum ersten Mal mit einer Kabelverbindung verwenden Sie eine alternative Methode verwenden.

- **IT-Mitarbeiter Computerkonfiguration**. Ein Mitglied der IT-Mitarbeiter verknüpfen einen Drahtloscomputer mit der Domäne und einmaliges Anmelden bootstrap-Drahtlosprofil konfiguriert. Mit dieser Methode wird der IT-Administrator den Drahtloscomputer mit der Ethernet-Netzwerk verbunden und der Computer der Domäne hinzugefügt. Dann wird der Administrator des Computers mit dem Benutzer verteilt. Wenn der Benutzer startet der Computer ohne Verwendung einer Kabelverbindung verwenden die Anmeldeinformationen für die Domäne, die sie manuell, für die Benutzeranmeldung angeben werden verwendet, um sowohl das eine Verbindung mit dem Drahtlosnetzwerk verbinden, und melden Sie sich bei der Domäne einrichten.

Weitere Informationen finden Sie im Abschnitt [verknüpfen Sie die Domäne und anmelden, indem Sie die IT-Personal Computer "Configuration"-Methode](#bkmk_itstaff)

-   **Bootstrap-Drahtlosprofil Konfiguration von Benutzern**. Der Benutzer konfiguriert den Drahtloscomputer mit einem bootstrap-Drahtlosprofil manuell und mit der Domäne, die basierend auf Anweisungen, die von IT-Administrator abgerufenen verknüpft. Der bootstrap-Drahtlosprofil ermöglicht den Benutzer zum Herstellen einer Drahtlosverbindung ein, und klicken Sie dann der Domäne beizutreten. Nach dem Hinzufügen des Computers zur Domäne und Neustart des Computers, kann der Benutzer anmelden mit der Domäne unter Verwendung einer drahtlosen Verbindung und ihre Anmeldeinformationen für ein Domänenkonto.

Weitere Informationen finden Sie im Abschnitt [verknüpfen Sie die Domäne und anmelden, indem Sie die Konfiguration für drahtloses Profil Bootstrap von Benutzern](#bkmk_userbootstrap).

### <a name="bkmk_itstaff"></a>Verknüpfen Sie die Domäne und anmelden, indem Sie die IT-Personal Computer "Configuration"-Methode
Member der Domänenbenutzer mit Domäne\-verknüpften drahtlose Clientcomputer ein temporäres Drahtlosprofil verwenden können, für die Verbindung mit einem 802.1X-authentifizierten\-drahtloses Netzwerk authentifiziert, ohne zunächst eine Verbindung mit das verdrahtete LAN. Diesem temporäre Drahtlosprofil heißt eine *bootstrap-Drahtlosprofil*.

Bootstrap-Drahtlosprofil erfordert, dass die Benutzer ihre Anmeldeinformationen für das Domänenbenutzerkonto manuell angeben, und überprüft nicht das Zertifikat für die Remote Authentication Dial\-In User Service \(RADIUS\) Server Ausführen des Netzwerkrichtlinienservers \(NPS\).

Nachdem drahtlose Verbindungen eingerichtet wurde, Gruppenrichtlinie wird angewendet, auf dem drahtlosen Client und ein neues Drahtlosprofil wird automatisch ausgegeben. Die neue Richtlinie verwendet die Computer- und Kontoanmeldeinformationen für die Clientauthentifizierung an. 

Darüber hinaus als Teil der PEAP\-MS\-CHAP v2-gegenseitige Authentifizierung mithilfe des neuen Profils anstelle der bootstrap-Drahtlosprofil, der Client überprüft die Anmeldeinformationen des RADIUS-Servers.

Nachdem Sie die Computer der Domäne hinzugefügt haben, verwenden Sie dieses Verfahren Single Sign On bootstrap-Drahtlosprofil, zu konfigurieren, bevor Sie den Drahtloscomputer mit der Domäne verteilt\-Mitgliedsbenutzer.

#### <a name="to-configure-a-single-sign-on-bootstrap-wireless-profile"></a>So konfigurieren Sie einmaliges Anmelden bootstrap-Drahtlosprofil

1. Erstellen von einem bootstrap-Drahtlosprofil mithilfe des Verfahrens in diesem Handbuch, die mit dem Namen [konfigurieren Sie ein WLAN-Verbindungsprofil für PEAP\-MS\-CHAP-v2](#bkmk_configureprofile), und verwenden Sie die folgenden Einstellungen:

    - PEAP\-MS\-CHAP-v2-Authentifizierung

    - Überprüfen des RADIUS-Serverzertifikats deaktiviert

    - Einmaliges Anmelden aktiviert

2. In den Eigenschaften der Drahtlosnetzwerkrichtlinie, die Sie erstellt, in dem das neue bootstrap-Profil, auf die **allgemeine** , wählen Sie das bootstrap-Profil, und klicken Sie dann auf **exportieren** So exportieren Sie das Profil ein Netzwerkfreigabe, USB-Flashlaufwerk oder andere leicht zugänglichen Speicherort. Das Profil wird als eine XML-Datei zu dem Speicherort gespeichert, die Sie angeben.

3. Verknüpfen Sie den neuen Drahtloscomputer mit der Domäne \(z. B. über eine Ethernet-Verbindung, die keine IEEE 802.1X-Authentifizierung erfordert Authentifizierung\) und Hinzufügen von bootstrap-Drahtlosprofils auf den Computer mithilfe der **Netsh Wlan Profil hinzufügen** Befehl.

    >[!NOTE]
    >Weitere Informationen finden Sie unter Netsh-Befehle für Wireless Local Area Network \(WLAN\) am [http:\/\/technet.microsoft.com\/Bibliothek\/dd744890.aspx](https://technet.microsoft.com/library/dd744890).

4. Verteilen Sie den neuen Drahtloscomputer für den Benutzer mit der Vorgehensweise "Melden Sie sich bei der Domäne mit Computern unter Windows 10."

Wenn der Benutzer den Computer startet, wird der Benutzer ihre Domänenbenutzerkontonamen und ein Kennwort eingeben von Windows aufgefordert. Da einmaliges Anmelden aktiviert ist, verwendet der Computer die Anmeldeinformationen des Domänenkontos Benutzer zuerst eine Verbindung mit dem drahtlosen Netzwerk und dann melden Sie sich bei der Domäne herstellen.

#### <a name="bkmk_w10"></a>Melden Sie sich bei der Domäne mit Computern unter Windows 10

1. Melden Sie den Computer ab, oder starten Sie ihn neu.

2. Auf der Tastatur drücken Sie, oder klicken Sie auf dem Desktop. Der Anmeldebildschirm wird angezeigt, mit dem Namen eines lokalen Benutzerkontos angezeigt und ein Kennwort-Eingabefeld unterhalb des Namens. Melden Sie sich nicht mit dem lokalen Benutzerkonto an.

3. Klicken Sie in der unteren linken Ecke des Bildschirms auf **anderer Benutzer**. Das Protokoll anderer Benutzer auf dem Bildschirm wird angezeigt, mit zwei Felder enthalten, von denen eine für den Benutzernamen und einem Kennwort. Nachfolgend das Kennwort ist das Feld der Text **melden Sie sich auf:** , und klicken Sie dann den Namen der Domäne, in dem der Computer gehört. Beispielsweise wenn Ihre Domäne "example.com" heißt, die der Text liest **melden Sie sich auf: BEISPIEL**.

4. In **Benutzernamen**, geben Sie Ihre Domänenbenutzername.

5. Geben Sie im Feld **Kennwort** das Domänenkennwort ein, und klicken Sie auf den Pfeil, oder drücken Sie die EINGABETASTE.

>[!NOTE]
>Wenn die **anderer Benutzer** Bildschirm enthält keinen Text **melden Sie sich auf:** sowie Ihren Domänennamen ein, Sie sollten Ihren Benutzernamen eingeben, im Format *Domäne\\Benutzer*. Z. B. zum Anmelden mit einem Konto mit dem Namen der Domäne "example.com" **Benutzer\-01**, Typ **Beispiel\\Benutzer\-01**.

### <a name="bkmk_userbootstrap"></a>Verknüpfen Sie die Domäne und anmelden, indem Sie die Konfiguration für drahtloses Profil Bootstrap von Benutzern
Mit dieser Methode können Sie die Schritte im Abschnitt allgemeine Schritte, und geben Sie Ihre Domäne\-Mitglieder mit den Anweisungen dazu, wie Sie einen Drahtloscomputer mit einem bootstrap-Drahtlosprofil manuell konfigurieren. Der bootstrap-Drahtlosprofil ermöglicht den Benutzer zum Herstellen einer Drahtlosverbindung ein, und klicken Sie dann der Domäne beizutreten. Nach der Computer der Domäne hinzugefügt und neu gestartet wird, kann der Benutzer über eine Drahtlosverbindung an der Domäne anmelden.

#### <a name="general-steps"></a>Allgemeine Schritte

1. Konfigurieren Sie ein lokales Computerkonto von Administrator in **Systemsteuerung**, für den Benutzer.

    >[!IMPORTANT]
    >Um einen Computer einer Domäne hinzugefügt haben, muss der Benutzer beim Computer mit dem lokalen Administratorkonto angemeldet sein. Alternativ muss der Benutzer die Anmeldeinformationen für das lokale Administratorkonto bei der Hinzufügung des Computers zur Domäne bereitstellen. Darüber hinaus muss der Benutzer ein Benutzerkonto in der Domäne verfügen, auf die der Benutzer der Computer beitreten möchte. Der Benutzer wird bei der der Computer der Domäne beitritt, für die Anmeldeinformationen für ein Domänenkonto aufgefordert werden \(des Benutzernamens und Kennworts\).

2. Benutzer Ihrer Domäne mit den Anweisungen zum Konfigurieren von bootstrap-Drahtlosprofil, geben Sie in der folgenden Prozedur beschriebenen **konfigurieren ein bootstrap-Drahtlosprofil**.
3. Darüber hinaus geben Sie Benutzern sowohl die Anmeldedaten des lokalen Computers \(des Benutzernamens und Kennworts\), und die Anmeldeinformationen für die Domäne \(Domänenbenutzerkontonamen und das Kennwort\) im Formular *Domänenname \\Benutzername*, sowie die Verfahren, um den Computer mit der Domäne "verknüpfen" und "Melden Sie sich bei der Domäne" als in Windows Server 2016 dokumentiert [Core Network Guide](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide).

#### <a name="to-configure-a-bootstrap-wireless-profile"></a>So konfigurieren Sie die bootstrap-Drahtlosprofil

1. Verwenden Sie die Anmeldeinformationen, die von Ihrem Netzwerkadministrator oder den IT-Support bereitgestellten professionelle, auf dem Computer mit dem lokalen Computer-Administratorkonto anzumelden.

2. Rechts\-klicken Sie auf das Symbol "Netzwerk" auf dem Desktop, und klicken Sie auf **öffnen Netzwerk- und Freigabecenter**. **Netzwerk- und Freigabecenter** wird geöffnet. In **ändern Sie Ihre Netzwerkeinstellungen**, klicken Sie auf **richten Sie eine neue Verbindung oder Netzwerk**. Die **eine Verbindung einrichten oder Netzwerk** Dialogfeld wird geöffnet.

3. Klicken Sie auf **manuell eine Verbindung mit einem drahtlosen Netzwerk herstellen**, und klicken Sie dann auf **Weiter**.

4. In **manuell eine Verbindung mit einem drahtlosen Netzwerk herstellen**im **Netzwerknamen**, geben Sie den SSID-Namen des jeweiligen APS.  

5. In **Sicherheitstyp**, wählen Sie die Einstellung, die von Ihrem Administrator bereitgestellt.

6. In **Verschlüsselungstyp** und **Sicherheitsschlüssel**, wählen Sie, oder geben Sie die Einstellungen, die von Ihrem Administrator bereitgestellt.

7. Wählen Sie **automatisch starten, diese Verbindung**, und klicken Sie dann auf **Weiter**.

8. In **wurde erfolgreich hinzugefügt. *** der Netzwerk-SSID*, klicken Sie auf **Ändern der Verbindungseinstellungen**.

9. Klicken Sie auf **Ändern der Verbindungseinstellungen**. Die *der Netzwerk-SSID* Wireless Network-Eigenschaft (Dialogfeld) wird geöffnet.

10. Klicken Sie auf der **Sicherheit** Registerkarte, und klicken Sie dann im **Netzwerkauthentifizierungsmethode auswählen**Option **Protected EAP \(PEAP\)** .

11. Klicken Sie auf **Einstellungen**. Die **Protected EAP \(PEAP\) Eigenschaften** -Seite wird geöffnet.

12. In der **Protected EAP \(PEAP\) Eigenschaften** Seite **Serverzertifikat überprüfen** ist nicht aktiviert ist, klicken Sie auf **OK** zweimal und Klicken Sie dann auf **schließen**.

13. Windows versucht, eine Verbindung mit dem drahtlosen Netzwerk herstellen. Die Einstellungen des bootstrap-Drahtlosprofils angeben, dass Sie stattdessen die Domänenanmeldeinformationen bereitstellen müssen. Wenn Windows für einen Kontonamen und Kennwort aufgefordert werden, geben Sie Ihren Domänenkonto-Anmeldeinformationen wie folgt:  *Domänenname\\Benutzernamen*, *Domänenkennwort*.

##### <a name="to-join-a-computer-to-the-domain"></a>Zum Hinzufügen eines Computers zur Domäne

1. Melden Sie sich bei dem Computer mit dem lokalen Administratorkonto an.

2. Geben Sie in das Suchfeld ein, **PowerShell**. In den Suchergebnissen angezeigt wird, mit der Maustaste **Windows PowerShell**, und klicken Sie dann auf **als Administrator ausführen**. Windows PowerShell wird mit einer Eingabeaufforderung mit erhöhten Rechten geöffnet.

3. Geben Sie den folgenden Befehl in Windows PowerShell, und drücken Sie dann die EINGABETASTE. Stellen Sie sicher, dass Sie die Variable Domänenname mit dem Namen der Domäne ersetzen, die Sie hinzufügen möchten.
    
    Add-Computer-Domänenname
    
4. Bei entsprechender Aufforderung Ihren Domänenbenutzernamen und Ihr Kennwort ein, und klicken Sie auf **OK**.
5. Starten Sie den Computer neu.
6. Befolgen Sie die Anweisungen im vorherigen Abschnitt [melden Sie sich bei der Domäne mit Computern unter Windows 10](#bkmk_w10).