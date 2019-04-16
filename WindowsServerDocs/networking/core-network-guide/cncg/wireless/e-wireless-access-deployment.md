---
title: Bereitstellung des Funkzugriffs
description: In diesem Thema ist Teil des Windows Server 2016 Networking Guide "Deploy Password-Based 802.1 X Authenticated Wireless Access"
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 4b66f517-b17d-408c-828f-a3793086bc1f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f78da14b91e5c1e9a2dc22f92ea95c89153befa8
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="wireless-access-deployment"></a>Bereitstellung des Funkzugriffs

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Zum Bereitstellen von drahtlosen Zugriff, gehen Sie wie folgt vor:

- [Bereitstellen und Konfigurieren von drahtlosen Zugriffspunkten](#bkmk_aps)

- [Erstellen einer Sicherheitsgruppe für Wireless-Benutzer](#bkmk_groups)

- [Konfigurieren von drahtlosen Netzwerk \ (IEEE 802.11\) Richtlinien](#bkmk_policies)

- [Konfigurieren von NPS-Server](#bkmk_nps)

- [Hinzufügen von neuen drahtlosen Computern zur Domäne](#bkmk_domain)

## <a name="bkmk_aps"></a>Bereitstellen und Konfigurieren von drahtlosen Zugriffspunkten

Zum Bereitstellen und konfigurieren Ihre drahtlosen Zugriffspunkte, gehen Sie wie folgt vor:

- [WAP-Kanal-Frequenzen angeben](#bkmk_channel)

- [Konfigurieren von drahtlosen Zugriffspunkten](#bkmk_wirelessaps)

>[!NOTE]
>Die Verfahren in diesem Handbuch beinhalten keine Anweisungen für Fälle in der die **User Account Control** Dialogfeld geöffnet wird, um Ihre Zustimmung zum Fortfahren abzufragen. Wenn dieses Dialogfeld wird geöffnet, während Sie die Verfahren in diesem Handbuch durchgeführt werden, und wenn das Dialogfeld, als Antwort auf Ihre Aktionen geöffnet wurde auf **Weiter**.

### <a name="bkmk_channel"></a>WAP-Kanal-Frequenzen angeben

Wenn Sie mehrere Drahtloszugriffspunkte an einem einzelnen geografischen Standort bereitstellen, müssen Sie drahtlose Zugriffspunkte konfigurieren, die überlappende Signale mit eindeutigen Kanalfrequenzen um zwischen Drahtloszugriffspunkten zu reduzieren.

Die folgenden Richtlinien können Sie hilft Ihnen bei der Auswahl der Channel-Frequenzen, die nicht mit anderen Drahtlosnetzwerke an der geografischen Position des Drahtlosnetzwerks in Konflikt stehen.

- Bei anderen Organisationen mit Niederlassungen in der Nähe oder in demselben Gebäude als Ihre Organisation ermitteln, ob es keine drahtlosen Netzwerke, die im Besitz von diesen Organisationen sind. Erfahren Sie Frequenzen für ihre drahtlosen Zugriffspunkts, die Platzierung und den zugewiesenen Kanal da Sie Ihren Zugriffspunkts anderen Kanalfrequenzen zuweisen müssen und Sie bestimmen die beste Position für Ihren Zugriffspunkts installieren müssen

- Überlappende drahtlose Signale auf angrenzenden Etagen innerhalb Ihrer Organisation zu identifizieren. Nach dem Identifizieren überlappende Abdeckungsbereiche außerhalb und innerhalb Ihrer Organisation zuweisen Channel Frequenzen für Ihre drahtlosen Zugriffspunkte werden durch das sicherstellen, dass zwei drahtlose Zugriffspunkten mit überlappende Abdeckung anderen Kanalfrequenzen zugewiesen.

### <a name="bkmk_wirelessaps"></a>Konfigurieren von drahtlosen Zugriffspunkten

Verwenden Sie die folgende Informationen zusammen mit der Produktdokumentation des drahtlosen Zugriffspunkt-Herstellers, um Ihre drahtlosen Zugriffspunkte konfigurieren.

Dieses Verfahren zählt die Elemente, die häufig auf einen drahtlosen Zugriffspunkt konfiguriert. Die Namen der Elemente können je nach Marke und Modell variieren und sich erheblich von denen in der folgenden Liste werden können. Einzelheiten hierzu finden Sie unter der drahtlosen Zugriffspunkt-Dokumentation.

#### <a name="to-configure-your-wireless-aps"></a>So konfigurieren Sie Ihre drahtlosen Zugriffspunkte  

- **SSID**. Geben Sie den Namen der drahtlosen network\(s\) \ (z.B. ExampleWLAN\). Dies ist der Name, der für drahtlose Clients angekündigt wird.

- **Verschlüsselung**. Geben Sie WPA2\ Enterprise \(preferred\) oder WPA\-Unternehmen, und \(preferred\) AES oder TKIP Verschlüsselungsverfahren, je nachdem, welche Versionen von Netzwerkadaptern Ihrer drahtlosen Clientcomputer unterstützt werden.

- **Wireless-AP-IP-Adresse \(static\)**. Konfigurieren Sie auf jedem Zugriffspunkt eine eindeutige statische IP-Adresse, die innerhalb der Ausschlussbereich für den DHCP-Bereich für das Subnetz liegt. Eine Adresse, die von der Zuweisung von DHCP ausgeschlossen wird verhindert, dass den DHCP-Server die IP-Adresse auf einem Computer oder einem anderen Gerät zuweisen.

- **Subnetzmaske**. Konfigurieren Sie hier, um die Subnetz-Maske Einstellungen des LANS entsprechen, mit dem Sie den Drahtloszugriffspunkt verbunden haben.  

- **DNS-Namen**. Einige drahtlose Zugriffspunkte können mit einem DNS-Namen konfiguriert werden. Der DNS-Serverdienst im Netzwerk kann DNS-Namen in eine IP-Adresse aufgelöst werden. Geben Sie auf jeder drahtlose Zugriffspunkt, die diese Funktion unterstützt, einen eindeutigen Namen für die DNS-Auflösung.  

- **DHCP-Dienst**. Wenn Ihr drahtlose Zugriffspunkt integrierten DHCP-Dienst hat, deaktivieren.  

- **RADIUS-gemeinsamen geheimen Schlüssel**. Verwenden Sie einen eindeutigen RADIUS gemeinsamen geheimen Schlüssel für jeden drahtlosen Zugriffspunkt, es sei denn, Sie planen, Zugriffspunkte als RADIUS-Clients in NPS durch Gruppenrichtlinien konfigurieren. Wenn Sie nach Gruppe APs in NPS konfigurieren möchten, muss der gemeinsame geheimen Schlüssel für jedes Mitglied der Gruppe übereinstimmen. Darüber hinaus sollte jede gemeinsamen geheimen Schlüssel, den Sie verwenden eine zufällige Sequenz von mindestens 22 Zeichen, die bei dem Groß- und Kleinbuchstaben, Zahlen und Satzzeichen. Um Zufälligkeit zu gewährleisten, können Sie eine zufällige Zeichengenerator, z.B. die zufällige Zeichengenerator finden Sie in der NPS **konfigurieren 802.1 X** Assistenten, um die gemeinsamen geheimen Schlüssel zu erstellen.

>[!TIP]
>Notieren Sie den gemeinsamen geheimen Schlüssel für jeden drahtlosen Zugriffspunkt und an einem sicheren Ort, z.B. ein Office sicher zu speichern. Sie müssen den gemeinsamen geheimen Schlüssel für jeden drahtlosen Zugriffspunkt kennen, wenn Sie RADIUS-Clients in NPS konfigurieren.  

- **IP-Adresse des RADIUS-Servers**. Geben Sie die IP-Adresse des Servers, auf dem NPS ausgeführt wird.

- **UDP-Port\(s\)**. Standardmäßig verwendet NPS UDP-Ports 1812 und 1645 für die Authentifizierung von Nachrichten und UDP-Ports 1813 und 1646 für die Kontoführungsnachrichten. Es wird empfohlen, dass Sie die dieselben UDP-Ports für Ihre Zugriffspunkte, aber wenn Sie einen berechtigter Grund unterschiedliche Ports verwendet haben, stellen Sie sicher, dass Sie nicht nur die Zugriffspunkte mit den neuen Portnummern konfigurieren, sondern auch alle NPS-Server verwenden die gleichen Portnummern als APs neu konfigurieren. Wenn der Zugriffspunkte und der NPS-Server nicht mit der gleichen UDP-Ports konfiguriert sind, NPS nicht empfangen oder Verbindungsanforderungen von APs verarbeiten, und alle versucht, eine drahtlose Verbindung auf das Netzwerk schlägt fehl.

- **Herstellerspezifische**. Einige drahtlose Zugriffspunkte erfordern Vendor\-spezifische Attribute \(VSAs\) vollständige drahtlosen Zugriffspunkt zu ermöglichen. Herstellerspezifische Attribute werden in der NPS-Netzwerkrichtlinien hinzugefügt.

- **DHCP-Filterung**. Konfigurieren Sie drahtlose Zugriffspunkte Drahtlosclients IP-Pakete von UDP-Port 68 zu senden, mit dem Netzwerk zu blockieren, wie durch den Hersteller der drahtlosen Zugriffspunkt dokumentiert.

- **DNS-Filterung**. Konfigurieren von drahtlosen Zugriffspunkten Drahtlosclients IP-Pakete von TCP- oder UDP-Port 53 zu senden, mit dem Netzwerk zu blockieren, wie durch den Hersteller der drahtlosen Zugriffspunkt dokumentiert.

## <a name="create-security-groups-for-wireless-users"></a>Erstellen von Sicherheitsgruppen für Mobiltelefone

Gehen Sie folgendermaßen vor, um Benutzern eine oder mehrere Sicherheitsgruppen erstellen, und fügen Sie Benutzer zur Sicherheitsgruppe entsprechenden Benutzern:

- [Erstellen einer Sicherheitsgruppe für Wireless-Benutzer](#bkmk_groups)

- [Hinzufügen von Benutzern der Wireless-Sicherheitsgruppe](#bkmk_addusers)

### <a name="bkmk_groups"></a>Erstellen einer Sicherheitsgruppe für Wireless-Benutzer

Verwenden Sie dieses Verfahren zum Erstellen einer Schutz-Gruppe in der Active Directory-Benutzer und Computer Microsoft Management Console \(MMC\) snap\-in.  

Mitgliedschaft in **Domänen-Admins**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren auszuführen.

#### <a name="to-create-a-wireless-users-security-group"></a>Erstellen Sie eine Sicherheitsgruppe mit drahtlosem

1. Klicken Sie auf **starten**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Active Directory-Benutzer und -Computer**. Der Active Directory-Benutzer und -Computer-Snap-In wird geöffnet. Wenn es nicht bereits ausgewählt ist, klicken Sie auf den Knoten für Ihre Domäne. Angenommen, Ihre Domäne example.com, klicken Sie auf **example.com**.

2. Klicken Sie im Detailbereich mit der rechten Maustaste auf den Ordner in dem Sie eine neue Gruppe hinzufügen möchten \ (z.B. mit der rechten Maustaste auf **Benutzer**\), zeigen Sie auf **neu**, und klicken Sie dann auf **Gruppe**.

3. In **neues Objekt – Gruppe**im **Gruppenname**, geben Sie den Namen der neuen Gruppe. Geben Sie z.B. **Drahtlosnetzwerke**.

4. In **Gruppenbereich**, wählen Sie eine der folgenden Optionen:

    - **Lokale Domäne**

    - **Globale**

    - **Universal**

5. In **Gruppentyp**Option **Security**.

6. Klicken Sie auf **OK**.

Wenn Sie mehr als eine Sicherheitsgruppe für Mobiltelefone benötigen, wiederholen Sie folgendermaßen vor, um zusätzliche drahtlose Benutzer und Gruppen erstellen. Später können Sie einzelne Netzwerkrichtlinien auf dem Netzwerkrichtlinienserver zum Anwenden von verschiedenen Bedingungen und Constraints jeder Gruppe, und geben Sie diesen Zugriff auf unterschiedliche Berechtigungen und Konnektivität Regeln erstellen.

### <a name="bkmk_addusers"></a>Hinzufügen von Benutzern zu der Sicherheitsgruppe der Wireless-Benutzer

Verwenden Sie dieses Verfahren Ihrer drahtlosen Sicherheitsgruppe in der Active Directory-Benutzer und Computer Microsoft Management Console \(MMC\) snap\ Benutzer, Computer oder Gruppe hinzufügen-in.

Mitgliedschaft in **Domänen-Admins**, oder einer entsprechenden Gruppe die mindestvoraussetzung, um dieses Verfahren auszuführen.

#### <a name="to-add-users-to-the-wireless-security-group"></a>Der Schutz-Gruppe Benutzer hinzu

1. Klicken Sie auf **starten**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Active Directory-Benutzer und -Computer**. Die Active Directory-Benutzer und -Computer in der MMC wird geöffnet. Wenn es nicht bereits ausgewählt ist, klicken Sie auf den Knoten für Ihre Domäne. Angenommen, Ihre Domäne example.com, klicken Sie auf **example.com**.

2. Klicken Sie im Detailbereich, Variablenname auf den Ordner, die Ihrer drahtlosen Sicherheitsgruppe enthält.

3. Im Detailbereich, klicken Sie auf der drahtlosen Sicherheitsgruppe und klicken Sie dann auf **Eigenschaften**. Die **Eigenschaften** Dialogfeld für die Sicherheitsgruppe wird geöffnet.

4. Auf der **Mitglieder** auf **hinzufügen**, und führen Sie dann eine der folgenden Verfahren, um einen Computer hinzufügen oder einen Benutzer oder Gruppe hinzufügen.

##### <a name="to-add-a-user-or-group"></a>So fügen Sie einen Benutzer oder eine Gruppe hinzu

1. In **Geben Sie die zu verwendenden Objektnamen ein**, geben Sie den Namen des Benutzers oder Gruppe, die Sie hinzufügen möchten, und klicken Sie dann auf **OK**.

2. Mitgliedschaft in anderen Benutzern oder Gruppen zuweisen möchten, wiederholen Sie Schritt1 dieses Verfahrens.  

##### <a name="to-add-a-computer"></a>Hinzufügen eines Computers

1. Klicken Sie auf **Objekttypen**. Die **Objekttypen** Dialogfeld wird geöffnet.

2. In **Objekttypen**Option **Computer**, und klicken Sie dann auf **OK**.

3. In **Geben Sie die zu verwendenden Objektnamen ein**, geben Sie den Namen des Computers, den Sie hinzufügen möchten, und klicken Sie dann auf **OK**.

4. Andere Computer eine Gruppenmitgliedschaft zuweisen möchten, wiederholen Sie die Schritte1\ bis 3 dieses Verfahrens.

## <a name="bkmk_policies"></a>Konfigurieren von drahtlosen Netzwerk \ (IEEE 802.11\) Richtlinien

Gehen Sie zum Konfigurieren von Drahtlosnetzwerkrichtlinien \ (IEEE 802.11\) Erweiterung der Gruppenrichtlinie Richtlinien:

- [Öffnen Sie oder fügen Sie hinzu und öffnen Sie ein Gruppenrichtlinienobjekt](#bkmk_opengpme)

- [Standard-Drahtlosnetzwerk aktivieren \ (IEEE 802.11\) Richtlinien](#bkmk_activate)

- [Konfigurieren Sie die neue Drahtlosnetzwerkrichtlinie](#bkmk_policyconfig)

### <a name="bkmk_opengpme"></a>Öffnen Sie oder fügen Sie hinzu und öffnen Sie ein Gruppenrichtlinienobjekt

Standardmäßig ist das Feature "Gruppenrichtlinienverwaltung" installiert, auf Computern unter Windows Server2016, wenn die Active Directory-Domänendienste \(AD DS\)-Serverrolle installiert ist und der Server als Domänencontroller konfiguriert ist. Das folgende Verfahren, das beschreibt, wie Sie die Gruppenrichtlinien-Verwaltungskonsole \(GPMC\) auf dem Domänencontroller zu öffnen. Anschließend wird beschrieben, wie entweder zu öffnen einer vorhandenen Domäne\ Gruppenrichtlinie Objekt \(GPO\) zum Bearbeiten oder erstellen ein neues Gruppenrichtlinienobjekt der Domäne, und zur Bearbeitung zu öffnen.

Mitgliedschaft in **Domänen-Admins**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren auszuführen.

#### <a name="to-open-or-add-and-open-a-group-policy-object"></a>Zum Öffnen oder hinzufügen und öffnen Sie ein Gruppenrichtlinienobjekt

1. Klicken Sie auf dem Domänencontroller auf **starten**, klicken Sie auf **Windows-Verwaltungsprogramme**, und klicken Sie dann auf **die Gruppenrichtlinien-Verwaltungskonsole**. Die Gruppenrichtlinien-Verwaltungskonsole wird geöffnet.  

2. Im linken Bereich auf Variablenname der Gesamtstruktur. Z.B. doppelten Mausklick **Gesamtstruktur: example.com**.  

3. Im linken Bereich doppelten Mausklick **Domänen**, und klicken Sie dann Variablenname der Domäne für die Sie ein Gruppenrichtlinienobjekt verwalten möchten. Z.B. doppelten Mausklick **example.com**.  

4. Führen Sie einen der folgenden:

    -   **vorhandenes Gruppenrichtlinienobjekt Domäne\-Ebene zur Bearbeitung öffnen**, doppelklicken Sie auf die Domäne, die das Gruppenrichtlinienobjekt enthält, die Sie verwalten möchten, klicken Sie auf die Domänenrichtlinie zu verwalten, z.B. die Standardrichtlinie, und klicken Sie dann auf **bearbeiten**. **Gruppenrichtlinienverwaltungs-Editor** wird geöffnet.

    -   **Erstellen ein neues Gruppenrichtlinienobjekt, und öffnen zum Bearbeiten von**, klicken Sie auf die Domäne für die Sie möchten, erstellen ein neues Gruppenrichtlinienobjekt, und klicken Sie auf **ein Gruppenrichtlinienobjekt in dieser Domäne erstellen und verknüpfen Sie es hier**.

        In **Gruppenrichtlinienobjekt**im **Namen**, geben Sie einen Namen für das neue Gruppenrichtlinienobjekt, und klicken Sie dann auf **OK**.

        Mit der rechten Maustaste auf Ihr neues Gruppenrichtlinienobjekt, und klicken Sie dann auf **bearbeiten**. **Gruppenrichtlinienverwaltungs-Editor** wird geöffnet.

Verwenden Sie Gruppenrichtlinienverwaltungs-Editor im nächsten AbschnittWireless-Richtlinien erstellen.

### <a name="bkmk_activate"></a>Standard-Drahtlosnetzwerk aktivieren \ (IEEE 802.11\) Richtlinien

Dieses Verfahren wird beschrieben, wie die standardmäßige WLAN aktivieren \ (IEEE 802.11\)-Richtlinien mithilfe der Gruppenrichtlinienverwaltungs-Editor \(GPME\).

>[!NOTE]
>Nach dem Aktivieren der **Windows Vista und neuere Versionen** -Version Funknetzwerk \ (IEEE 802.11\) Richtlinien oder der **Windows XP** Version, die Version-Option wird von automatisch entfernt die Liste der Optionen Sie mit der rechten Maustaste auf **Drahtlosnetzwerke \ (IEEE 802.11\) Richtlinien**. Dies tritt auf, da nach der Auswahl einer Richtlinienversion die Richtlinie, klicken Sie im Detailbereich des Gruppenrichtlinienverwaltungs-Editor hinzugefügt wird bei der Auswahl der **Drahtlosnetzwerke \ (IEEE 802.11\) Richtlinien** Knoten. Dieser Zustand verbleibt, es sei denn, Sie dabei die Drahtlosnetzwerkrichtlinie-Version, klicken Sie auf zum Menü mit den für zurückgibt die Drahtlosnetzwerkrichtlinie löschen **Drahtlosnetzwerk \ (IEEE 802.11\) Richtlinien** im Gruppenrichtlinienverwaltungs-Editor. Die WLAN-Richtlinien werden darüber hinaus nur aufgeführt, klicken Sie im Gruppenrichtlinienverwaltungs-Editor Detailbereich bei der **Drahtlosnetzwerk \ (IEEE 802.11\) Richtlinien** Knoten ausgewählt ist.

Mitgliedschaft in **Domänen-Admins**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren auszuführen.

#### <a name="to-activate-default-wireless-network-ieee-80211-policies"></a>Standardmäßiges verkabelte Netzwerke aktivieren \ (IEEE 802.11\) Richtlinien  

1. Führen Sie die zuvor **zu öffnen oder hinzufügen und öffnen Sie ein Gruppenrichtlinienobjekt** Gruppenrichtlinienverwaltungs-Editor zu öffnen.

2. Im Gruppenrichtlinienverwaltungs-Editor, klicken Sie im linken Bereich doppelten Mausklick **Computerkonfiguration**, doppelten Mausklick **Richtlinien**, doppelten Mausklick **Windows-Einstellungen**, und klicken Sie dann Variablenname **Sicherheitseinstellungen**.

![802.1 X Wireless-Gruppenrichtlinie](../../../media/Wireless-GP/Wireless-GP.jpg)

3. In **Sicherheitseinstellungen**, klicken Sie auf **Drahtlosnetzwerke \ (IEEE 802.11\) Richtlinien**, und klicken Sie dann auf **erstellen Sie eine neue Wireless-Gruppenrichtlinie für Windows Vista und neuere Versionen**. 

![802. 1 x Wireless-Richtlinien](../../../media/Wireless-Policy/Wireless-Policy.jpg)

4. Die **Eigenschaften der neuen Drahtlosnetzwerkrichtlinie** Dialogfeld wird geöffnet. In **Richtlinienname**, geben Sie einen neuen Namen für die Richtlinie, oder übernehmen Sie den Standardnamen. Klicken Sie auf **OK** um die Richtlinie zu speichern. Die Standard-Richtlinie aktiviert ist, und klicken Sie im Detailbereich des Gruppenrichtlinienverwaltungs-Editor mit dem neuen Namen, die Sie angegeben haben oder mit dem Standardnamen aufgeführt **neuen Drahtlosnetzwerkrichtlinie**.

![Eigenschaften der neuen Drahtlosnetzwerkrichtlinie](../../../media/Wireless-Policy-Properties/Wireless-Policy-Properties.jpg)

5. Klicken Sie im Detailbereich doppelten Mausklick **neuen Drahtlosnetzwerkrichtlinie** um es zu öffnen.

Im nächsten Abschnittkönnen Sie die Konfiguration der Einstellung Verarbeitungsreihenfolge und Netzwerkberechtigungen ausführen.

### <a name="bkmk_policyconfig"></a>Konfigurieren Sie die neue Drahtlosnetzwerkrichtlinie

Sie können die Verfahren in diesem AbschnittDrahtlosnetzwerk konfigurieren \ (IEEE 802.11\) Richtlinie. Diese Richtlinie können Sie Einstellungen für Sicherheit und Authentifizierung konfigurieren, Verwalten der WLAN-Profilen und geben Sie Berechtigungen für drahtlose Netzwerke, die nicht als bevorzugte Netzwerke konfiguriert werden.

- [Konfigurieren eines Drahtlosverbindungsprofils für PEAP\-MS\-CHAP v2](#bkmk_configureprofile)  

- [Legen Sie die Reihenfolge für die drahtlose Verbindungsprofile](#bkmk_preferenceorder)  

- [Definieren Sie Netzwerkberechtigungen](#bkmk_permissions)  

#### <a name="bkmk_configureprofile"></a>Konfigurieren eines Drahtlosverbindungsprofils für PEAP\-MS\-CHAP v2

Dieses Verfahren beschreibt die erforderlichen Schrittezum Konfigurieren eines funkprofils für PEAP\-MS\-CHAP v2.  

Mitgliedschaft in **Domänen-Admins**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.

##### <a name="to-configure-a-wireless-connection-profile-for-peap-ms-chap-v2"></a>Konfigurieren ein drahtlosverbindungsprofils für PEAP\-MS\-CHAP v2

1. Im Gruppenrichtlinienverwaltungs-Editor im Dialogfeld Eigenschaften von drahtlosen Netzwerk für die Richtlinie, die Sie gerade auf erstellte der **allgemeine** Registerkarte im **Beschreibung**, geben Sie eine kurze Beschreibung für die Richtlinie.

2. Um anzugeben, dass WLAN-Autokonfigurationsdienst zum Konfigurieren von Einstellungen verwendet wird, sicher, dass **verwenden Windows WLAN AutoConfig-Dienst für Clients** ausgewählt ist.  

3. In **eine Verbindung zu verfügbaren Netzwerken in der Reihenfolge der unten aufgelisteten Profile**, klicken Sie auf **hinzufügen**, und wählen Sie dann **Infrastruktur**. Die **neue Profileigenschaften** Dialogfeld wird geöffnet.

4. In der**neue Profileigenschaften** Dialogfeld auf die **Verbindung** Registerkarte die **Profilname** Feld, und geben Sie einen neuen Namen für das Profil. Geben Sie z.B. **Example.com WLAN-Profil für Windows10**.

5. In **Netzwerk Name\(s\) \(SSID\)**, geben Sie die SSID, die für Ihre drahtlosen Zugriffspunkte konfigurierten SSID entspricht, und klicken Sie dann auf **hinzufügen**.

    Wenn Ihre Bereitstellung mehrere SSIDs verwendet und jeder drahtlose Zugriffspunkt dieselben Drahtlos Sicherheitseinstellungen verwendet, wiederholen Sie diesen Schritt, um die SSID für jeden drahtlosen Zugriffspunkt hinzuzufügen, wenn dieses Profil anwenden soll.

    Wenn Ihre Bereitstellung mehrere SSIDs verwendet und die Sicherheitseinstellungen für die einzelnen SSIDS nicht übereinstimmen, konfigurieren Sie ein separates Profil für jede Gruppe von SSIDs, die dieselben Sicherheitseinstellungen nutzen. Wenn Sie eine Gruppe von drahtlosen Zugriffspunkten für die Verwendung WPA2\-Enterprise und AES und eine andere Gruppe von drahtlosen Zugriffspunkten WPA\-Enterprise und TKIP konfiguriert haben, konfigurieren Sie ein Profil für jede Gruppe von drahtlosen Zugriffspunkten fest.

6. Wenn der Standardtext **NEWSSID** vorhanden ist, wählen Sie ihn, und klicken Sie dann auf **entfernen**.

7. Wenn Sie drahtlose Zugriffspunkte bereitgestellt haben, um das Übertragungssignal Unterdrücken, wählen Sie **verbinden, selbst wenn das Netzwerk keine Kennung aussendet**.

    > [!NOTE]
    > Durch das Aktivieren dieser Option kann ein Sicherheitsrisiko darstellen, da drahtlose Clients für die Firmenwebsite und Verbindungen mit einem Drahtlosnetzwerk versucht. Diese Einstellung ist standardmäßig nicht aktiviert.  

8. Klicken Sie auf die **Security** auf **erweitert**, und konfigurieren Sie dann Folgendes:

    1. So konfigurieren Sie erweiterte 802.1X-Einstellungen **IEEE 802.1 X**Option **erzwingen erweiterte 802.1X-Einstellungen**.

        Wenn die erweiterten 802.1X-Einstellungen erzwungen werden, die Standardwerte für **Max. Eapol\-Start-Meld**, **Wartezeitraum**, **Startzeitraum**, und **Authentifizierungszeitraum** sind für typische drahtlosbereitstellungen ausreichend. Aus diesem Grund müssen Sie nicht die Standardeinstellungen ändern, wenn Sie einen bestimmten Grund dafür haben.

    2. Um die einmalige Anmeldung zu aktivieren, wählen Sie **einmaliges Anmelden für dieses Netzwerk aktivieren **.

    3. Die restlichen Standardwerte bei **einmaliges Anmelden** sind für typische drahtlosbereitstellungen ausreichend.

    4. In **für die schnelle Serverspeicherung**, wenn Sie Ihren drahtlose Zugriffspunkt konfiguriert ist, für die registrierungseintragswert-Authentifizierung, wählen **Netzwerk verwendet registrierungseintragswert-Authentifizierung **.

9. Wählen Sie zum angeben, dass die Funkkommunikation FIPS-140\-2-Standards erfüllt **Kryptografie im FIPS-140\-2-zertifizierten Modus ausführen **.

10. Klicken Sie auf **OK** wieder die **Security** Registerkarte. In **Sicherheitsmethoden für dieses Netzwerk auswählen**im **Authentifizierung**Option **WPA2\ Enterprise**, wenn sie von Ihrem drahtlosen Zugriffspunkt und Ihren drahtlosen Client-Netzwerkadaptern unterstützt wird. Wählen Sie andernfalls **WPA\ Enterprise **.

11. In **Verschlüsselung**, wenn von Ihrem drahtlosen Zugriffspunkt und Ihren drahtlosen Client-Netzwerkadaptern wählen unterstützt **AES-CCMP **. Wenn Sie Zugriffspunkte und drahtlosen Netzwerkadaptern, die 802. 11ac unterstützen verwenden, wählen Sie **AES-GCMP **. Wählen Sie andernfalls **TKIP **.

    > [!NOTE]  
    > Die Einstellungen für beide **Authentifizierung** und **Verschlüsselung** muss die für Ihre drahtlosen Zugriffspunkte konfigurierten Einstellungen übereinstimmen. Die Standardeinstellungen für **Authentifizierungsmodus**, **Max. Authentifizierungsfehler**, und **Benutzerinformationen für zukünftige Verbindungen mit diesem Netzwerk zwischenspeichern** sind für typische drahtlosbereitstellungen ausreichend.  

12. In **Netzwerkauthentifizierungsmethode auswählen**Option **geschütztes EAP \(PEAP\)**, und klicken Sie dann auf **Eigenschaften **. Die **Eigenschaften für geschütztes EAP** Dialogfeld wird geöffnet.

13. In **Eigenschaften für geschütztes EAP**, überprüfen Sie, ob **überprüfen Sie die Identität des Servers mittels zertifikatprüfung** ausgewählt ist.

14. In **vertrauenswürdige Stammzertifizierungsstellen**, wählen die vertrauenswürdige Stammzertifizierungsstelle \(CA\), die den Server ausgestellt Zertifikat auf dem NPS-Server.

    > [!NOTE]  
    > Diese Einstellung beschränkt die Stamm-CAs, denen Clients auf die ausgewählten Zertifizierungsstellen vertrauen. Wenn keine vertrauenswürdiger Stammzertifizierungsstellen ausgewählt sind, werden Clients vertrauen, dass alle Zertifizierungsstellen, die in ihrem Zertifikatspeicher für vertrauenswürdige Stammzertifizierungsstellen aufgeführt-Stamm.  

15. In der **Authentifizierungsmethode auswählen** wählen **gesichertes Kennwort \ (EAP\-MS\-CHAP v2\)**.

16. Klicken Sie auf **konfigurieren**. In der **EAP-MSCHAPv2-Eigenschaften** Dialogfeld überprüfen Sie, ob **verwenden automatisch eigenen Windows-Anmeldenamen und Kennwort \ (und Domäne If Any\)** ausgewählt ist, und klicken Sie auf **OK **.

17. Um PEAP schnelle Wiederherstellung der Verbindung aktivieren, stellen Sie sicher, dass **schnelle Wiederherstellung der Verbindung aktivieren** ausgewählt ist.

18. Wählen Sie zum Server Kryptografiebindungs-TLV auf versucht, eine Verbindung zu erzwingen, **Verbindung trennen, wenn Server kein Kryptografiebindungs-TLV vorweist **.

19. Wählen Sie zum angeben, dass die Identität des Benutzers in der ersten Authentifizierung maskiert ist **Identitätsschutz aktivieren**, und klicken Sie in das Textfeld ein, geben Sie einen Namen für die anonyme Identität, oder das Textfeld leer lassen.

    >[! NOTIZEN]
    >- Die NPS-Richtlinie für 802.1 X Wireless muss erstellt werden, mit dem Netzwerkrichtlinienserver **Verbindungsanforderungsrichtlinie **. Wenn die NPS-Richtlinie erstellt wird, mit dem Netzwerkrichtlinienserver **Netzwerkrichtlinie**, und klicken Sie dann Identitätsschutz nicht verwendet werden.
    >- EAP-Identitätsschutz wird durch bestimmte EAP-Methoden bereitgestellt, ein leeres oder eine anonyme Identität \ (eine andere als die tatsächliche Identity\) wird als Antwort auf die EAP-Identity-Anforderung gesendet. PEAP sendet die Identität zweimal während der Authentifizierung. In der ersten Phase wird die Identität in Klartext gesendet, und diese Identität für das Routing, nicht für die Clientauthentifizierung verwendet wird. Die tatsächliche Identität – für die Authentifizierung verwendet, wird in der zweiten Phase der Authentifizierung und innerhalb der sicheren Tunnel, der in der ersten Phase hergestellt wurde gesendet. Wenn **Identitätsschutz aktivieren** aktiviert ist, wird der Benutzername mit dem Eintrag in das Textfeld angegebenen ersetzt. Nehmen wir beispielsweise an **Identitätsschutz aktivieren** ausgewählt ist und der Identität Datenschutz Alias **anonyme** angegeben ist, in das Textfeld ein. Für einen Benutzer mit einem echten Identitätsalias **jdoe@example.com**, die Identität, die in der ersten Phase der Authentifizierung gesendet wird geändert werden **anonymous@example.com**. Der Bereich Teil der 1. Phase Identität wird nicht geändert werden, da sie für das Routing verwendet wird.  

20. Klicken Sie auf **OK** zum Schließen der **Eigenschaften für geschütztes EAP** Dialogfeld.
21. Klicken Sie auf **OK** zum Schließen der **Security** Registerkarte.
22. Wenn Sie zusätzliche Profile erstellen möchten, klicken Sie auf **hinzufügen**, und wiederholen Sie die vorherigen Schritte, die verschiedene Optionen zum Anpassen der einzelnen Profile für die drahtlose Clients und Netzwerk, das Profil angewendet werden soll. Wenn Sie das Hinzufügen von Profilen abgeschlossen haben, klicken Sie auf **OK** um das Dialogfeld Eigenschaften der Drahtlosnetzwerkrichtlinie zu schließen.

Im nächsten Abschnittkönnen Sie die Richtlinienprofile für eine optimale Sicherheit bestellen.

#### <a name="bkmk_preferenceorder"></a>Legen Sie die Reihenfolge für die drahtlose Verbindungsprofile
Sie können dieses Verfahren verwenden, wenn Sie mehrere WLAN-Profilen in der Drahtlosnetzwerk-Richtlinie erstellt haben und Sie die Profile für eine optimale Effizienz und Sicherheit bestellen möchten.

Um sicherzustellen, dass Drahtlosclients, die mit der höchsten Sicherheit verbinden, die sie unterstützen können, platzieren Sie die restriktivsten Richtlinien am Anfang der Liste.

Beispielsweise haben zwei Profile, eine für Clients, WPA2 zu unterstützen, und eine für Clients, die Unterstützung von WPA, platzieren Sie die höhere WPA2-Profil in der Liste. Dadurch wird sichergestellt, dass die Clients, die WPA2 unterstützen diese Methode für die weniger sichere WPA, anstatt die Verbindung verwenden.

Dieses Verfahren beschreibt die Schritte, um die Reihenfolge anzugeben, in der drahtlose Verbindung von Profilen zur Domäne gehörende Drahtlosclients zu Drahtlosnetzwerken herzustellen.

Mitgliedschaft in **Domänen-Admins**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.

##### <a name="to-set-the-preference-order-for-wireless-connection-profiles"></a>Festlegen die Reihenfolge für die drahtlose Verbindungsprofile

1. Klicken Sie im Gruppenrichtlinienverwaltungs-Editor im Dialogfeld Eigenschaften von drahtlosen Netzwerk für die Richtlinie, die Sie soeben konfiguriert, auf die **allgemeine** Registerkarte.

2. Auf der **allgemeine** Registerkarte **eine Verbindung zu verfügbaren Netzwerken in der Reihenfolge der unten aufgelisteten Profile**Wählen der Profile, die Sie in der Liste verschieben möchten, und dann auf Schaltfläche entweder die "Pfeil nach oben" oder "Pfeil nach unten" gedrückt, um das Profil an die gewünschte Position in der Liste zu verschieben.

3.  Wiederholen Sie Schritt2 für die einzelnen Profile, die Sie in der Liste verschieben möchten.  

4.  Klicken Sie auf **OK** um alle Änderungen zu speichern.

Im folgenden Abschnittkönnen Sie die Netzwerkberechtigungen für die Drahtlosnetzwerkrichtlinie definieren.

#### <a name="bkmk_permissions"></a>Definieren Sie Netzwerkberechtigungen
Sie können die Einstellungen konfigurieren, auf die **Netzwerkberechtigungen** Registerkarte für die Mitglieder der Domäne, welche WLAN-Netzwerk \ (IEEE 802.11\)-Richtlinien gelten.

Können Sie die folgenden Einstellungen für drahtlose Netzwerke, die nicht konfiguriert sind nur anwenden der **allgemeine** Registerkarte die **Wireless Netzwerkrichtlinieneigenschaften** Seite:

- Zulassen oder Verweigern von Verbindungen mit bestimmten drahtlosen Netzwerken, die Sie angeben, indem Netzwerktyp und Service Set Identifier \(SSID\)

- Zulassen oder Verweigern von Verbindungen mit ad-hoc-Netzwerken

- Zulassen oder Verweigern von Verbindungen mit Infrastrukturnetzwerken

- Zulassen oder Verweigern von Benutzern das Anzeigen der Typen von \ (Ad Hoc oder Infrastructure\), deren Zugriff verweigert

- Zulassen oder Verweigern von Benutzern zum Erstellen eines Profils, das für alle Benutzer gilt

- Benutzer können nur zulässige Netzwerke eine Verbindung mithilfe von Gruppenrichtlinien-Profile

Mitgliedschaft in **Domänen-Admins**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um diese Verfahren abzuschließen.

##### <a name="to-allow-or-deny-connections-to-specific-wireless-networks"></a>Zulassen oder Verweigern von Verbindungen mit bestimmten drahtlosen Netzwerken

1. Klicken Sie im Gruppenrichtlinienverwaltungs-Editor, klicken Sie im Dialogfeld Eigenschaften von Wireless-Netzwerk auf die **Netzwerkberechtigungen** Registerkarte.

2. Auf der **Netzwerkberechtigungen** auf **hinzufügen **. Die **Neuer Berechtigungseintrag** Dialogfeld wird geöffnet.

3. In der **Neuer Berechtigungseintrag** Dialogfeld, in der **Netzwerknamen \(SSID\)** Feld, geben Sie die Netzwerk-SSID des Netzwerks für die Sie Berechtigungen festlegen möchten.

4.  In **Netzwerktyp**Option **Infrastruktur** oder **Ad-hoc-**.

    > [!NOTE]  
    > Wenn Sie unsicher sind, ob das Netzwerk senden eine Infrastruktur oder ad-hoc-Netzwerk ist, können Sie zwei Netzwerk-Berechtigungseinträge, einen für jeden Netzwerk konfigurieren.

5. In **Berechtigung**Option **zulassen** oder **Verweigern **.

6. Klicken Sie auf **OK**, um wieder die **Netzwerkberechtigungen** Registerkarte.

##### <a name="to-specify-additional-network-permissions-optional"></a>Weitere Berechtigungen \(Optional\) angeben

1.  Auf der **Netzwerkberechtigungen** Registerkarte, einige oder alle der folgenden Optionen konfigurieren:  

    -   Um die Mitglieder der Domäne den Zugriff auf ad-hoc-Netzwerke, aktivieren Sie **Verbindungen mit Ad\-Hoc-Netzwerken verhindern**.

    -   Wählen Sie die Mitglieder der Domäne Zugriff auf Infrastrukturnetzwerken verweigert, **Verbindungen mit Infrastrukturnetzwerken verhindern**.  

    -   Die Mitglieder der Domäne Netzwerktypen anzeigen zu \ (Ad Hoc oder Infrastructure\), dem sie der Zugriff darauf verweigert, wählen Sie **Benutzer erlauben, Anzeigen von abgelehnten Netzwerken**.

    -   Wählen Sie damit die Benutzer zum Erstellen von Profilen, die für alle Benutzer gelten, **Benutzern gestatten, erstellen Sie alle Benutzerprofile**.

    -   Wählen Sie zum angeben, dass Ihre Benutzer nur eine Verbindung herstellen können, dürfen Netzwerke mithilfe von Gruppenrichtlinien Profile **nur für zulässige Netzwerke verwenden Gruppenrichtlinien Profile**.

## <a name="bkmk_nps"></a>Die NPS-Server konfigurieren
Zum Konfigurieren von NPS-Server zum Ausführen von 802. 1 X-Authentifizierung für den drahtlosen Zugriff, gehen Sie wie folgt vor:

- [Registrierung von NPS in Active Directory-Domänendiensten](#bkmk_npsreg)

- [Konfigurieren Sie einen drahtlosen Zugriffspunkt als NPS RADIUS-Client](#bkmk_radiusclient)

- [Erstellen Sie NPS-Richtlinien für 802.1 X Wireless mithilfe eines Assistenten](#bkmk_npspolicy)

### <a name="bkmk_npsreg"></a>Registrierung von NPS in Active Directory-Domänendiensten
Dieses Verfahrens können zum Registrieren eines Servers mit Network Policy Server \(NPS\) in Active Directory Domain Services \(AD DS\) in der Domäne, in der NPS-Server Mitglied ist. Für die NPS-Server über die Berechtigung zum Lesen der Dial\-Eigenschaften von Benutzerkonten während des Autorisierungsprozesses gewährt werden soll muss jedes NPS-Server in AD DS registriert werden. Registrieren eines NPS-Servers den Server Fügt die **RAS- und IAS-Server** Sicherheitsgruppe in AD DS.

>[!NOTE]
>Sie können NPS auf einem Domänencontroller oder auf einem dedizierten Server installieren. Führen Sie den folgenden Windows PowerShell-Befehl NPS zu installieren, wenn Sie dies noch nicht getan haben:
    
    Install-WindowsFeature NPAS -IncludeManagementTools
    
Mitgliedschaft in **Domänen-Admins**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.

#### <a name="to-register-an-nps-server-in-its-default-domain"></a>So registrieren Sie einen NPS-Server in seiner Standarddomäne

1. Auf dem NPS-Server in **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Der NPS-Snap-In wird geöffnet.

2. Klicken Sie auf **NPS \(Local\)**, und klicken Sie dann auf **Server in Active Directory registrieren**. Die **Netzwerkrichtlinienserver** Dialogfeld wird geöffnet.

3. In **Netzwerkrichtlinienserver**, klicken Sie auf **OK**, und klicken Sie dann auf **OK** erneut.

### <a name="bkmk_radiusclient"></a>Konfigurieren Sie einen drahtlosen Zugriffspunkt als NPS RADIUS-Client
Verwenden Sie dieses Verfahren so konfigurieren Sie ein Zugriffspunkt, auch bekannt als eine *Netzwerkzugriffsserver \(NAS\)*, als Remote Authentication Dial\-In User Service \(RADIUS\) Client mithilfe der NPS-Snap-In. 

>[!IMPORTANT]
>Clientcomputer, z.B. tragbare Computer und andere Computer mit Clientbetriebssystemen, sind keine RADIUS-Clients. RADIUS-Clients sind Netzwerkzugriffsserver – z.B. Drahtloszugriffspunkte, 802.1X\-fähigen Switches, virtuelles privates Netzwerk \(VPN\) Server und Dial\ von Servern, da sie das RADIUS-Protokoll zur Kommunikation mit RADIUS-Servern, z.B. NPS verwenden.

Mitgliedschaft in **Domänen-Admins**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.

#### <a name="to-add-a-network-access-server-as-a-radius-client-in-nps"></a>Hinzufügen ein Netzwerk-Servers als RADIUS-Client auf dem Netzwerkrichtlinienserver

1. Auf dem NPS-Server in **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Der NPS-Snap-In wird geöffnet.

2. In der NPS Snap-In doppelten Mausklick **RADIUS-Clients und Servern**. Klicken Sie auf **RADIUS-Clients**, und klicken Sie dann auf **neu**.

3. In **Neuer RADIUS-Client**, überprüfen Sie, ob die **Aktivieren dieser RADIUS-Client** das Kontrollkästchen aktiviert ist.

4. In **Neuer RADIUS-Client**im **Anzeigenamen**, geben Sie einen Anzeigenamen für den drahtlosen Zugriffspunkt.

    Beispielsweise, wenn Sie eine drahtlose Zugriff hinzufügen möchten geben zeigen Sie mit dem Namen AP\-01 \(AP\) **AP\-01**.

5. In **Adresse \(IP or DNS\)**, geben Sie die IP-Adresse oder vollständig qualifizierter Domänenname \(FQDN\) des Netzwerkzugriffsservers.

    Um sicherzustellen, dass der Name richtig ist und in eine gültige IP-Adresse zugeordnet ist, wenn Sie den FQDN eingegeben haben, klicken Sie auf **überprüfen, ob**, und klicken Sie dann im **Adresse überprüfen**in der **Adresse** auf **beheben**. Wenn der FQDN-Name in eine gültige IP-Adresse zugeordnet ist, die IP-Adresse diesem NAS erscheint automatisch **IP-Adresse**. Wenn der FQDN nicht in eine IP-Adresse auflöst, erhalten Sie eine Meldung angezeigt, dass der Host bekannt ist. Wenn dies der Fall, stellen Sie sicher, dass Sie den richtigen AP haben und dass der Zugriffspunkt eingeschaltet und mit dem Netzwerk verbunden ist.  

    Klicken Sie auf **OK** schließen **Adresse überprüfen**.  

6. In **Neuer RADIUS-Client**im **gemeinsamen geheimen Schlüssel**, führen Sie eine der folgenden Optionen:  

    -   Um einen RADIUS-gemeinsamen geheimen Schlüssel manuell zu konfigurieren, wählen Sie **manuell**, und klicken Sie dann im **gemeinsamer geheimer Schlüssel**, geben Sie das sichere Kennwort, die auch auf dem NAS eingegeben werden. Geben Sie den gemeinsamen geheimen Schlüssel in **gemeinsamen geheimen Schlüssel bestätigen**.  

    -   Um einen gemeinsamen geheimen Schlüssel automatisch zu generieren, wählen Sie die **generieren**, und klicken Sie dann auf die **generieren** Schaltfläche. Speichern Sie die generierten gemeinsamen geheimen Schlüssel, und verwenden Sie diesen Wert NAS so konfigurieren, dass sie mit dem NPS-Server kommunizieren kann.  

        >[!IMPORTANT]
        >Der RADIUS-gemeinsame geheime Schlüssel, den Sie für Ihre virtuelle Ihres Zugriffspunkts in NPS eingeben muss genau den gemeinsamen geheimen Schlüssel RADIUS übereinstimmen, der auf des tatsächlichen drahtlosen Zugriffspunkts konfiguriert ist Wenn Sie die NPS-Option verwenden, um einen RADIUS-gemeinsamen geheimen Schlüssel zu generieren, müssen Sie den entsprechenden tatsächlichen drahtlosen Zugriffspunkt mit den gemeinsamen geheimen Schlüssel RADIUS konfigurieren, die vom NPS generiert wurde.

7. In **Neuer RADIUS-Client**auf die **erweitert** Registerkarte **Herstellername**, geben Sie den Namen des NAS-Herstellers. Wenn Sie nicht sicher, dass der Name des NAS-Herstellers sind, wählen Sie **RADIUS-Standards**.

8. In **zusätzliche Optionen**, wenn Sie Authentifizierungsmethoden EAP und PEAP verwenden, und wählen Sie, wenn Ihre NAS die Verwendung des Attributs Authentifikator Nachricht unterstützt **Nachrichten Zugriff anfordern müssen das Message\-Authentifikator-Attribut enthalten**.

9. Klicken Sie auf **OK**. NAS wird angezeigt, in der Liste der RADIUS-Clients, die auf dem NPS-Server konfiguriert.

### <a name="bkmk_npspolicy"></a>Erstellen Sie NPS-Richtlinien für 802.1 X Wireless mithilfe eines Assistenten
Mithilfe dieses Verfahrens können Sie die Verbindungsanforderungsrichtlinien erstellen und Richtlinien zum Bereitstellen von entweder 802.1X\ erforderlich-fähigen Drahtloszugriffspunkten als Remote Authentication Dial\-In User Service \(RADIUS\) Clients mit dem RADIUS-Server, die mit Netzwerkrichtlinienserver \(NPS\).  
Nachdem Sie den Assistenten ausführen, werden die folgenden Richtlinien erstellt:

- Eine Verbindungsanforderungsrichtlinie

- Eine Netzwerkrichtlinie

>[!NOTE]
>Jedes Mal, wenn Sie neue Richtlinien für Zugriff mit 802.1X-Authentifizierung erstellen möchten, können Sie den Assistenten für neue IEEE 802.1 X sichere verkabelte und drahtlose ausführen.

Mitgliedschaft in **Domänen-Admins**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.

#### <a name="create-policies-for-8021x-authenticated-wireless-by-using-a-wizard"></a>Erstellen Sie Richtlinien für 802.1 X authentifizierte drahtlose mithilfe ein Assistenten

1. Öffnen Sie die NPS-Snap-In. Wenn es nicht bereits ausgewählt ist, klicken Sie auf **NPS \(Local\)**. Wenn Sie die NPS-MMC-Snap-In ausführen und Richtlinien auf einem NPS-Remoteserver erstellen möchten, wählen Sie den Server.

2. In **Einstieg**im **Standardkonfiguration**Option **RADIUS-Server für 802.1 X drahtlose oder verkabelte 802.1X-Verbindungen**. Der Text und Links unter dem Text werden entsprechend Ihrer Auswahl angepasst.

3. Klicken Sie auf **konfigurieren 802.1 X**. Der konfigurieren 802.1 X-Assistent wird geöffnet.

4.  Auf der **wählen 802.1 X Verbindungen** Assistenten Seite **Typ von 802.1 X-Verbindungen**wählen **sicheren WLAN-Verbindungen**, und in **Namen**, geben Sie einen Namen für die Richtlinie, oder lassen Sie den Standardnamen **sicheren WLAN-Verbindungen**. Klicken Sie auf **Weiter**.

5.  Auf der **angeben 802.1 X-Switches** Assistenten Seite **RADIUS-Clients**, alle 802. 1 X-Switches und Drahtloszugriffspunkte, die Sie hinzugefügt haben, als RADIUS-Clients in der NPS-Snap-In angezeigt werden. Führen Sie einen der folgenden:

    -   Hinzufügen von zusätzlichen Netzwerk Access Server \(NASs\), z.B. drahtlose Zugriffspunkte in **RADIUS-Clients**, klicken Sie auf **hinzufügen**, und klicken Sie dann im **Neuer RADIUS-Client**, geben Sie die Informationen für: **Anzeigenamen**, **Adresse \(IP or DNS\)**, und **gemeinsamen geheimen Schlüssel**.

    -   So ändern Sie die Einstellungen für jeden NAS in **RADIUS-Clients**, wählen Sie den Zugriffspunkt für die Sie ändern die Einstellungen, und klicken Sie dann auf möchten **bearbeiten**. Ändern Sie die Einstellungen nach Bedarf.

    -   So entfernen Sie ein NAS aus der Liste in **RADIUS-Clients**, wählen Sie die NAS, und klicken Sie dann auf **entfernen**.

        >[!WARNING]
        >Entfernen einen RADIUS-Client innerhalb der **konfigurieren 802.1 X** Assistent löscht den Client aus der NPS-Serverkonfiguration. Alle hinzufügen, ändern und löschen, mit denen Sie innerhalb der **konfigurieren 802.1 X** -Assistenten, um RADIUS-Clients werden in der NPS Snap-In angezeigt, in dem **RADIUS-Clients** Knoten unter **NPS** \/ **RADIUS-Clients und Servern**. Beispielsweise wird bei Verwendung den Assistenten zum Entfernen von 802.1 X wechseln, aus der NPS-Snap-In wird auch der Switch entfernt.

6. Klicken Sie auf **Weiter**. Auf der **Konfigurieren einer Authentifizierungsmethode** Assistenten Seite **Typ \ (basiert auf der Konfiguration und Netzwerk fest)**wählen **Microsoft: geschütztes EAP \(PEAP\)**, und klicken Sie dann auf **konfigurieren**.

    >[!TIP]
    >Wenn Sie eine Fehlermeldung, dass ein Zertifikat kann nicht für die Verwendung mit der Authentifizierungsmethode gefunden werden, und Sie Active Directory Certificate Services, um RAS- und IAS-Server in Ihrem Netzwerk automatisch Zertifikate konfiguriert haben, stellen Sie zunächst sicher, dass Sie die Schrittezum Registrieren von NPS in Active Directory-Domänendiensten befolgt haben, verwenden die folgenden Schrittezum Aktualisieren der Gruppenrichtlinie : Klicken Sie auf **starten**, klicken Sie auf **Windows-System**, klicken Sie auf **ausführen**, und im **öffnen**, Typ **Gpupdate**, und drücken Sie dann die EINGABETASTE. Wenn der Befehl gibt Ergebnisse, die angibt, dass sowohl Benutzer-als auch eine Gruppenrichtlinie erfolgreich aktualisiert haben, wählen Sie **Microsoft: geschütztes EAP \(PEAP\)** erneut, und klicken Sie dann auf **konfigurieren**.
    >
    >Wenn nach der Aktualisierung der Gruppenrichtlinie weiterhin die Fehlermeldung angezeigt, der angibt, dass ein Zertifikat für die Verwendung mit der Authentifizierungsmethode gefunden werden kann, das Zertifikat nicht angezeigt wird, weil nicht die Mindestanforderungen für Serverzertifikate erfüllen, wird gemäß dem Kernnetzwerk-Begleithandbuch: [Bereitstellen von Serverzertifikaten für 802.1 X kabelgebundenen und drahtlosen Bereitstellungen](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments). In diesem Fall müssen Sie NPS-Konfiguration einstellen, Sperren Sie das Zertifikat ausgestellt für Ihre NPS server\(s\) und folgen Sie dann die Anweisungen, um ein neues Zertifikat zu konfigurieren, indem Sie im Bereitstellungshandbuch für Server-Zertifikate verwenden.

7.  Auf der **Eigenschaften für geschütztes EAP bearbeiten** Assistenten Seite **ausgestelltes Zertifikat**, stellen Sie sicher, dass das richtige Zertifikat des NPS-Server aktiviert ist, und führen Sie die folgenden:

    >[!NOTE]
    >Überprüfen Sie, ob der Wert im **Aussteller** korrekt für das Zertifikat im ausgewählten **ausgestelltes Zertifikat**. Der erwartete Aussteller für ein Zertifikat von einer Zertifizierungsstelle mit Active Directory Certificate Services \(AD CS\) mit dem Namen corp\DC1, in der Domäne contoso.com, ist z.B. **Corp\-DC1\-CA**.

    -   Wählen Sie damit die Benutzer mit ihren drahtlosen Computern zwischen Zugriffspunkten ohne jedes Mal erneut authentifiziert werden muss, verbinden Sie mit einem neuen Zugriffspunkt Roaming, **schnelle Wiederherstellung der Verbindung aktivieren**.

    -   Wählen Sie zum angeben, dass Drahtlosclients verbinden den Netzwerk-Authentifizierungsprozess beendet wird, wenn der RADIUS-Server kein Kryptografiebindungs Type\-Length\-Value \(TLV\) vorweist **trennen Clients ohne Kryptografiebindung**.  

    -   So ändern Sie die Richtlinie Einstellungen für das EAP eingeben, in **EAP-Typen**, klicken Sie auf **bearbeiten**im **EAP-MSCHAPv2-Eigenschaften**, ändern Sie die Einstellungen nach Bedarf, und klicken Sie dann auf **OK**.  

8.  Klicken Sie auf **OK**. Schließt das Dialogfeld Eigenschaften für geschütztes EAP bearbeiten, erneut die **konfigurieren 802.1 X** Assistenten. Klicken Sie auf **Weiter**.

9. In **Benutzergruppen angeben**, klicken Sie auf **hinzufügen**, und geben Sie den Namen der Sicherheitsgruppe ein, die Sie für die drahtlose Clients in der Active Directory-Benutzer und -Computer-Snap-In konfiguriert. Geben Sie z.B. Wenn Sie Ihrer drahtlosen Sicherheitsgruppe Drahtlosnetzwerke genannt, **Drahtlosnetzwerke**. Klicken Sie auf **Weiter**.

10. Klicken Sie auf **konfigurieren** zum Konfigurieren von RADIUS-Standardattribute und Vendor\-spezifische Attribute für die virtuellen LAN-\(VLAN\) nach Bedarf und als angegeben, die von Ihrem drahtlosen Zugriffspunkt Hardwareanbieter bereitgestellten Dokumentation. Klicken Sie auf **Weiter**.

11. Überprüfen Sie die Konfigurationsdetails, und klicken Sie dann auf **Fertig stellen**.

Die NPS-Richtlinien werden jetzt erstellt, und Sie können auf drahtlose Computer der Domäne verschieben.

## <a name="bkmk_domain"></a>Hinzufügen von neuen drahtlosen Computern zur Domäne
Die einfachste Methode zum Hinzufügen von neuer drahtlosen Computern zur Domäne physisch an den Computer an ein verkabeltes LAN-Segment ist \ (ein Segment nicht durch eine 802.1X-Authentifizierung X Switch\ gesteuert) vor dem Hinzufügen des Computers zur Domäne. Dies ist am einfachsten, da drahtlose Gruppenrichtlinieneinstellungen sofort angewendet, und wenn Sie Ihre eigene PKI bereitgestellt haben, wird der Computer das Zertifikat der Zertifizierungsstelle erhält und legt ihn in den Zertifikatspeicher vertrauenswürdiger Stammzertifizierungsstellen der Drahtlosclient NPS-Server mit Server-Zertifikate, die von der Zertifizierungsstelle ausgestellten vertrauen können.

Nach ein neuer drahtlosen Computer der Domäne angehört, ist die bevorzugte Methode für Benutzer mit der Domäne anmelden ebenso Protokoll ausführen, indem Sie über eine Kabelverbindung auf das Netzwerk.

### <a name="other-domain-join-methods"></a>Andere Methoden Domänenbeitritt
In Fällen, in denen es nicht praktikabel ist, Hinzufügen von Computern zur Domäne über eine verkabelte ethernetverbindung oder in Fällen, in denen der Benutzer anmelden kann, bei der Domäne für das erste Mal über eine Kabelverbindung, eine alternative Methode erforderlich.

- **IT-Mitarbeiter Computerkonfiguration**. Ein Mitglied der IT-Mitarbeiter einen drahtlosen Computer der Domäne hinzugefügt und ein einmaliges Anmelden Bootstrap-Drahtlosprofil konfiguriert. Mit dieser Methode wird der IT-Administrator den Drahtloscomputer mit dem Ethernet-Netzwerk verbunden und konfiguriert den Computer der Domäne beitritt. Dann wird der Administrator des Computers für den Benutzer verteilt. Beim Einrichten der Computer ohne über eine Kabelverbindung, die Anmeldeinformationen für die Domäne, die sie manuell für die Benutzeranmeldung als angeben, werden verwendet, um beide Benutzer gestartet wird, einer Verbindungs mit dem Drahtlosnetzwerk und zum Anmelden bei der Domäne.

Weitere Informationen finden Sie im Abschnitt [beitreten der Domäne und melden Sie sich mit der IT-Mitarbeiter Computer Configuration Methode](#bkmk_itstaff)

-   **Bootstrapping-Drahtlosprofil Konfiguration von Benutzern**. Der Benutzer manuell den Drahtloscomputer mit Bootstrap-Drahtlosprofil konfiguriert und der Domäne, basierend auf vom IT-Administrator erworben Anweisungen Beitritt. Das Bootstrap-Drahtlosprofil kann der Benutzer auf eine drahtlose Verbindung herzustellen, und treten Sie der Domäne. Nach dem Hinzufügen des Computers zur Domäne und den Computer neu starten, kann der Benutzer anmelden mit der Domäne mit einer drahtlosen Verbindung und Anmeldeinformationen ihrer Domäne.

Weitere Informationen finden Sie im Abschnitt [Verknüpfen der Domäne und Anmelden mithilfe eines Profils Bootstrap-Drahtloskonfiguration von Benutzern](#bkmk_userbootstrap).

### <a name="bkmk_itstaff"></a>Verknüpfen Sie die Domäne und Anmelden mithilfe eines die IT-Mitarbeiter Computer Konfigurationsmethode
Mitglied der Domänenbenutzer mit Domäne\ verbundene drahtlose Clientcomputer können ein temporäres Drahtlosprofil zur Verbindung mit einem 802.1X\-Drahtlosnetzwerk ohne zuerst eine Verbindung mit dem drahtgebundenen Netzwerk authentifiziert. Diese temporäre Drahtlosprofil heißt eine *Bootstrap-Drahtlosprofil*.

Bootstrap-Drahtlosprofil erfordert, dass die Benutzer ihre Anmeldeinformationen für das Domänenbenutzerkonto manuell angeben, und nicht das Zertifikat des Servers Remote Authentication Dial\-In User Service \(RADIUS\) Netzwerkrichtlinienserver \(NPS\) ausgeführt.

Nach der drahtlosen Verbindung hergestellt wurde, Gruppenrichtlinie wird angewendet, auf dem drahtlosen Clientcomputer, und wird automatisch ein neues Drahtlosprofil ausgegeben. Die neue Richtlinie verwendet die Anmeldeinformationen des Kontos Computer- und für die Clientauthentifizierung. 

Darüber hinaus als Teil der PEAP\-MS\-CHAP v2 gegenseitige Authentifizierung mit dem neuen Profil anstelle der Bootstrap-Profils, überprüft der Client die Anmeldeinformationen des RADIUS-Servers.

Nachdem Sie den Computer zur Domäne hinzuzufügen, verwenden Sie dieses Verfahren so konfigurieren Sie ein einmaliges Anmelden Bootstrap-Drahtlosprofil, vor der Verteilung der Drahtloscomputer für den Benutzer Domäne\-Member.

#### <a name="to-configure-a-single-sign-on-bootstrap-wireless-profile"></a>So konfigurieren Sie ein einmaliges Anmelden Bootstrap-Drahtlosprofil

1. Erstellen ein Bootstrap-Profils mithilfe des Verfahrens in diesem Handbuch mit dem Namen [Konfigurieren eines Verbindungsprofils Wireless für PEAP\-MS\-CHAP v2](#bkmk_configureprofile), und verwenden Sie die folgenden Einstellungen:

    - PEAP\-MS\-CHAP v2-Authentifizierung

    - Überprüfen Sie die RADIUS-Serverzertifikats deaktiviert

    - Einmaliges Anmelden aktiviert

2. In den Eigenschaften der Drahtlosnetzwerkrichtlinie, in dem Sie das neue Bootstrap-Profil erstellt, auf, die **allgemeine** Registerkarte, wählen Sie das Bootstrap-Profil, und klicken Sie dann auf **exportieren** um das Profil auf eine Netzwerkfreigabe zu exportieren, USB-Flashlaufwerk, oder andere leicht zugänglichen Speicherort. Das Profil wird als XML-Datei an den Speicherort gespeichert, die Sie angeben.

3. Fügen Sie den neuen drahtlosen Computer zur Domäne \ (z.B. über eine Ethernet-Verbindung, die keine IEEE 802.1X-Authentifizierung erfordert X Authentication\) und fügen Sie die Bootstrap-Drahtlosprofil auf den Computer mithilfe der **Netsh-WLAN-Profil hinzufügen** Befehl.

    >[!NOTE]
    >Weitere Informationen finden Sie unter Netsh-Befehle für Wireless Local Area Network \(WLAN\) am [http:///\/technet.microsoft.com\/library\/dd744890.aspx](https://technet.microsoft.com/library/dd744890).

4. Verteilen Sie den neuen Drahtloscomputer für den Benutzer mit den Schrittenzum "Melden Sie sich bei der Domäne mit einem Computer unter Windows10."

Wenn der Benutzer den Computer gestartet wird, fordert Windows den Benutzer ihre Domänenbenutzerkontonamen und ein Kennwort eingeben. Da einmaliges Anmelden aktiviert ist, verwendet der Computer die Anmeldeinformationen für das Domänenbenutzerkonto zuerst eine Verbindung mit dem Drahtlosnetzwerk ein, und melden Sie sich bei der Domäne herstellen.

#### <a name="bkmk_w10"></a>Melden Sie sich bei der Domäne mit einem Computer unter Windows10

1. Melden Sie den Computer oder starten Sie den Computer neu.

2. Drücken Sie eine beliebige Taste auf der Tastatur, oder klicken Sie auf dem Desktop. Der Anmeldebildschirm angezeigt wird, mit dem Namen eines lokalen Benutzerkontos angezeigt und ein Kennwort Eingabefeld unter dem Namen. Melden Sie sich nicht mit der lokalen Benutzerkontos an.

3. Klicken Sie in der unteren linken Ecke des Bildschirms, auf **anderer Benutzer**. Mit zwei Feldern, eine für Benutzernamen und einem Kennwort wird das Protokoll anderer Benutzer auf dem Bildschirm angezeigt. Unterhalb des Kennworts Feld ist der Text **melden Sie sich auf:** und dann den Namen der Domäne, in dem der Computer verbunden wird. Beispielsweise, wenn Ihre Domäne example.com heißt, der Text lautet **melden Sie sich auf: Beispiel**.

4. In **Benutzernamen**, geben Sie Ihren Domänennamen für den Benutzer.

5. In **Kennwort**, geben Sie das Domänenkennwort ein, und klicken Sie auf den Pfeil, oder drücken Sie die EINGABETASTE.

>[!NOTE]
>Wenn die **anderer Benutzer** Bildschirm enthält nicht den Text **melden Sie sich auf:** und den Domänennamen ein, geben Sie Ihren Benutzernamen im Format *Domäne\\Benutzer *. Z.B. zum Anmelden bei der Domäne example.com mit einem Konto mit dem Namen **durch den Benutzer-01**, Typ **Example\\User\-01**.

### <a name="bkmk_userbootstrap"></a>Verknüpfen Sie die Domäne und Anmelden mithilfe eines Bootstrap-Profil Drahtloskonfiguration durch Benutzer
Mit dieser Methode können Sie die Schritteim Abschnittzu allgemeinen Schritteausführen, und Sie Ihren Benutzern Domäne\-Member die Anweisungen dazu, wie Sie manuell einen Drahtloscomputer mit Bootstrap-Drahtlosprofil konfigurieren bereitstellen. Das Bootstrap-Drahtlosprofil kann der Benutzer auf eine drahtlose Verbindung herzustellen, und treten Sie der Domäne. Nachdem der Computer der Domäne hinzugefügt und neu gestartet wird, kann der Benutzer über eine drahtlose Verbindung an der Domäne anmelden.

#### <a name="general-steps"></a>Allgemeine Schritte

1. Konfigurieren Sie ein Administratorkonto des lokalen Computers in **Systemsteuerung**, für den Benutzer.

    >[!IMPORTANT]
    >Um einen Computer zu einer Domäne beizutreten, muss der Benutzer auf den Computer mit dem lokalen Administratorkonto angemeldet sein. Alternativ muss der Benutzer während des Vorgangs Hinzufügung des Computers zur Domäne die Anmeldeinformationen für das lokale Administratorkonto angeben. Darüber hinaus muss der Benutzer ein Benutzerkonto in der Domäne verfügen, der der Benutzer den Computer hinzufügen möchte. Bei der den Computer der Domäne hinzugefügt, der Benutzer aufgefordert werden Domänenkonto-Anmeldeinformationen \ (Benutzername und Password\).

2. Benutzer Ihrer Domäne mit den Anweisungen zum Konfigurieren von Bootstrap-Drahtlosprofil, bereitstellen, wie im folgenden Verfahren beschrieben **Bootstrap-Drahtlosprofil konfigurieren **.
3. Außerdem Benutzern zur Verfügung stellen beide Anmeldeinformationen für lokale \ (Benutzername und Password\), und Domänenanmeldeinformationen \ (Domänenbenutzerkontonamen und Password\) in Form *Domainname\\benutzername*, sowie die Verfahren, um den Computer der Domäne "Verbinden" und "Anmelden bei der Domäne" als dokumentierte in der Windows Server2016 [Handbuch zum Hauptnetzwerk ](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide).

#### <a name="to-configure-a-bootstrap-wireless-profile"></a>So konfigurieren Sie Bootstrap-Drahtlosprofil

1. Verwenden Sie die Anmeldeinformationen von Ihrem Netzwerkadministrator oder IT-Support bereitgestellt Professional auf dem Computer mit dem lokalen Computer Administratorkonto anmelden.

2. Klicken Sie auf das Netzwerksymbol auf dem Desktop, und klicken Sie dann auf **öffnen Netzwerk- und Freigabecenter **. **Netzwerk- und Freigabecenter** wird geöffnet. In **Ändern Ihrer Netzwerkeinstellungen**, klicken Sie auf **eine neue Verbindung oder neues Netzwerk einrichten **. Die **Einrichten einer Verbindung oder neues Netzwerk** Dialogfeld wird geöffnet.

3. Klicken Sie auf **manuell eine Verbindung mit einem Drahtlosnetzwerk herstellen**, und klicken Sie dann auf **Weiter **.

4. In **manuell eine Verbindung mit einem Drahtlosnetzwerk herstellen**im **Netzwerknamen**, geben Sie den SSID-Namen des Zugriffspunkts.  

5. In **Sicherheitstyp**, wählen Sie die Einstellung, die von Ihrem Administrator bereitgestellt.

6. In **Verschlüsselungstyp** und **Sicherheitsschlüssel**, auswählen, oder geben Sie die Einstellungen von Ihrem Administrator bereitgestellt.

7. Wählen Sie **diese Verbindung automatisch starten**, und klicken Sie dann auf **Weiter **.

8. In **erfolgreich hinzugefügt *** der Netzwerk-SSID*, klicken Sie auf **Verbindungseinstellungen ändern**.

9. Klicken Sie auf **Verbindungseinstellungen ändern **. Die *der Netzwerk-SSID* Eigenschaftendialogfeld für verkabelte Netzwerke wird geöffnet.

10. Klicken Sie auf die **Sicherheit** Registerkarte, und klicken Sie dann im **Netzwerkauthentifizierungsmethode auswählen**wählen **geschütztes EAP \(PEAP\)**.

11. Klicken Sie auf **Einstellungen**. Die **Eigenschaften für geschütztes EAP-\(PEAP\)** Seite geöffnet wird.

12. In der **Eigenschaften für geschütztes EAP-\(PEAP\)** Seite sicher, dass **Serverzertifikat** ist nicht aktiviert ist, klicken Sie auf **OK** zweimal, und klicken Sie dann auf **schließen **.

13. Windows versucht, eine Verbindung mit dem Drahtlosnetzwerk herstellen. Die Einstellungen für die Bootstrap-Drahtlosprofil geben, dass Sie Ihre Domänenanmeldeinformationen bereitstellen müssen. Wenn Windows Sie für einen Kontonamen und ein Kennwort einzugeben, geben die Anmeldeinformationen für die Domäne Konto wie folgt: *Domänenname\\benutzername*, *Domänenkennwort *.

##### <a name="to-join-a-computer-to-the-domain"></a>Zum Hinzufügen eines Computers zur Domäne

1. Melden Sie sich an den Computer mit dem lokalen Administratorkonto an.

2. Geben Sie in das Textfeld Suchen **PowerShell **. In den Suchergebnissen mit der rechten Maustaste **Windows PowerShell**, und klicken Sie dann auf **als Administrator ausführen **. Windows PowerShell wird mit einer Eingabeaufforderung mit erhöhten Rechten geöffnet.

3. Geben Sie in Windows PowerShell den folgenden Befehl, und drücken Sie dann die EINGABETASTE. Stellen Sie sicher, dass Sie die Variable Domänenname mit dem Namen der Domäne ersetzen, die Sie hinzufügen möchten.
    
    Add-Computer Domänenname
    
4. Wenn Sie aufgefordert werden, geben Ihre Domänenbenutzernamen und das Kennwort, und klicken Sie auf **OK **.
5. Starten Sie den Computer neu.
6. Gehen Sie wie im vorherigen Abschnitt [melden Sie sich bei der Domäne mit einem Computer unter Windows10](#bkmk_w10).