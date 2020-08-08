---
title: Bereitstellung des Funkzugriffs
description: Dieses Thema ist Teil des Windows Server 2016-Netzwerk Handbuchs "Bereitstellen von Kenn Wort basiertem 802.1 x authentifizierten drahtlosen Zugriff".
manager: brianlic
ms.topic: article
ms.assetid: 4b66f517-b17d-408c-828f-a3793086bc1f
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 32e54b5129bf2215758adf35bd23c4d99ab2d8e9
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996965"
---
# <a name="wireless-access-deployment"></a>Bereitstellung des Funkzugriffs

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Führen Sie diese Schritte aus, um drahtlosen Zugriff bereitzustellen

- [Bereitstellen und Konfigurieren von drahtlos Zugriffs Punkten](#bkmk_aps)

- [Erstellen einer Sicherheitsgruppe für drahtlose Benutzer](#bkmk_groups)

- [Konfigurieren von \( IEEE 802,11- \) Richtlinien für Drahtlos Netzwerke](#bkmk_policies)

- [Konfigurieren von NPSS](#bkmk_nps)

- [Neue drahtlos Computer der Domäne beitreten](#bkmk_domain)

## <a name="deploy-and-configure-wireless-aps"></a><a name="bkmk_aps"></a>Bereitstellen und Konfigurieren von drahtlos Zugriffs Punkten

Führen Sie diese Schritte aus, um Ihre drahtlos Zugriffspunkte bereitzustellen und zu konfigurieren

- [Angeben von drahtlosen AP-Kanal Frequenzen](#bkmk_channel)

- [Konfigurieren von drahtlos Zugriffs Punkten](#bkmk_wirelessaps)

>[!NOTE]
>Die Verfahren in diesem Handbuch beinhalten keine Anweisungen für Fälle, in denen das Dialogfeld **Benutzerkontensteuerung** geöffnet wird, um die Zustimmung zum Fortfahren abzufragen. Klicken Sie auf **Weiter**, wenn das Dialogfeld während der Ausführung der Verfahren in dieser Anleitung geöffnet wird und als Folge der ausgeführten Aktionen geöffnet wurde.

### <a name="specify-wireless-ap-channel-frequencies"></a><a name="bkmk_channel"></a>Angeben von drahtlosen AP-Kanal Frequenzen

Wenn Sie an einem einzelnen geografischen Standort mehrere drahtlos Zugriffspunkte bereitstellen, müssen Sie drahtlos Zugriffspunkte konfigurieren, die überlappende Signale aufweisen, um die Störungen zwischen drahtlos Zugriffs Punkten zu verringern.

Sie können die folgenden Richtlinien verwenden, um Sie bei der Auswahl von Kanal Frequenzen zu unterstützen, die nicht mit anderen Drahtlos Netzwerken im geografischen Standort Ihres drahtlos Netzwerks in Konflikt stehen.

- Wenn es andere Organisationen gibt, die Niederlassungen in unmittelbarer Nähe haben oder sich in demselben Gebäude wie Ihre Organisation befinden, ermitteln Sie, ob es sich um drahtlos Netzwerke handelt, die sich im Besitz dieser Organisationen befinden. Ermitteln Sie sowohl die Platzierung als auch die zugewiesenen Kanal Frequenzen Ihrer drahtlosen Zugriffspunkt-Verbindungen, da Sie Ihren Zugriffsmöglichkeiten unterschiedliche Kanal Frequenzen zuweisen müssen, und Sie müssen den optimalen Speicherort für die Installation Ihrer Zugriffspunkt-App ermitteln.

- Identifizieren Sie überlappende drahtlose Signale auf angrenzenden Etagen innerhalb ihrer eigenen Organisation. Nachdem Sie überlappende Coverage-Bereiche außerhalb und innerhalb Ihrer Organisation identifiziert haben, weisen Sie Kanal Frequenzen für Ihre drahtlos Zugriffspunkte zu, und stellen Sie sicher, dass zwei drahtlos Zugriffs Punkten mit überlappender Abdeckung verschiedene Kanal Frequenzen zugewiesen

### <a name="configure-wireless-aps"></a><a name="bkmk_wirelessaps"></a>Konfigurieren von drahtlos Zugriffs Punkten

Verwenden Sie die folgenden Informationen zusammen mit der Produktdokumentation des drahtlosen AP-Herstellers, um Ihre drahtlos Zugriffspunkte zu konfigurieren.

Diese Prozedur listet die Elemente auf, die in einem drahtlos Zugriffspunkt häufig konfiguriert sind. Die Elementnamen können je nach Marke und Modell variieren und können sich von den in der folgenden Liste unterscheiden. Ausführliche Informationen finden Sie in der drahtlosen AP-Dokumentation.

#### <a name="to-configure-your-wireless-aps"></a>So konfigurieren Sie Ihre drahtlos Zugriffspunkte

- **SSID**. Geben Sie den Namen des drahtlos Netzwerks \( \) \( an, z. b. examplewlan \) . Dies ist der Name, der drahtlosen Clients angekündigt wird.

- **Verschlüsselung**. Geben Sie WPA2 \- Enterprise \( Preferred \) oder WPA \- Enterprise an, und entweder AES \( Preferred \) oder TKIP Encryption Chiffre, je nachdem, welche Versionen von den Netzwerkadaptern des drahtlos Client Computers unterstützt werden.

- **Drahtlose AP-IP-Adresse \( statisch \) **. Konfigurieren Sie auf jedem AP eine eindeutige statische IP-Adresse, die innerhalb des Ausschluss Bereichs des DHCP-Bereichs für das Subnetz liegt. Durch die Verwendung einer Adresse, die von der Zuweisung durch DHCP ausgeschlossen wird, wird verhindert, dass der DHCP-Server einem Computer oder einem anderen Gerät dieselbe IP-Adresse zuweist.

- **Subnetzmaske**. Konfigurieren Sie diese so, dass Sie den Subnetzmasken-Einstellungen des LANs entspricht, mit dem Sie den drahtlos Zugriffspunkt verbunden haben.

- **DNS-Name**. Einige drahtlos Zugriffspunkte können mit einem DNS-Namen konfiguriert werden. Der DNS-Dienst im Netzwerk kann DNS-Namen in eine IP-Adresse auflösen. Geben Sie auf jedem drahtlos Zugriffspunkt, der diese Funktion unterstützt, einen eindeutigen Namen für die DNS-Auflösung ein.

- **DHCP-Dienst**. Wenn Ihr drahtlos Zugriffspunkt über einen integrierten \- DHCP-Dienst verfügt, deaktivieren Sie ihn.

- Frei gegebener **RADIUS**-Schlüssel. Verwenden Sie für jeden drahtlos Zugriffspunkt einen eindeutigen freigegebenen RADIUS-Schlüssel, es sei denn, Sie planen die Konfiguration von APS als RADIUS-Clients in NPS nach Gruppe. Wenn Sie Vorhaben, APS nach Gruppe in NPS zu konfigurieren, muss der gemeinsame geheime Schlüssel für jedes Mitglied der Gruppe identisch sein. Außerdem sollte jeder gemeinsame geheime Schlüssel, den Sie verwenden, eine zufällige Sequenz von mindestens 22 Zeichen sein, die Groß-und Kleinbuchstaben, Ziffern und Interpunktions Zeichen vermischt. Um die Zufälligkeit sicherzustellen, können Sie einen Zufallszeichen Generator verwenden, z. b. den Zufallszeichen Generator, der im NPS- **configure 802.1 x** -Assistenten gefunden wurde, um die gemeinsamen geheimen Schlüssel zu erstellen.

>[!TIP]
>Notieren Sie den gemeinsamen geheimen Schlüssel für jeden drahtlos Zugriffspunkt, und speichern Sie ihn an einem sicheren Ort, z. b. in einem Büro. Beim Konfigurieren von RADIUS-Clients in NPS müssen Sie den gemeinsamen geheimen Schlüssel für jeden drahtlos Zugriffspunkt kennen.

- **IP-Adresse des RADIUS-Servers**. Geben Sie die IP-Adresse des Servers ein, auf dem NPS ausgeführt wird

- **UDP- \( Port \) s**. Standardmäßig verwendet NPS die UDP-Ports 1812 und 1645 für Authentifizierungs Nachrichten und die UDP-Ports 1813 und 1646 für Buchhaltungs Nachrichten. Es wird empfohlen, dass Sie dieselben UDP-Ports auf Ihren APS verwenden. Wenn Sie jedoch einen gültigen Grund für die Verwendung anderer Ports haben, stellen Sie sicher, dass Sie die APS nicht nur mit den neuen Portnummern konfigurieren, sondern auch alle NPSS so konfigurieren, dass Sie dieselben Portnummern wie die APS verwenden. Wenn APS und NPSS nicht mit denselben UDP-Ports konfiguriert sind, kann NPS keine Verbindungsanforderungen von APS empfangen oder verarbeiten, und alle drahtlosen Verbindungsversuche im Netzwerk können nicht ausgeführt werden.

- **VSAs**. Einige drahtlos Zugriffspunkte erfordern Anbieter \- spezifische Attribute \( VSAs \) , um vollständige WLAN-Funktionen bereitzustellen. VSAs werden in NPS-Netzwerk Richtlinien hinzugefügt.

- **DHCP-Filterung**. Konfigurieren von drahtlos Zugriffs Punkten, um zu verhindern, dass drahtlose Clients IP-Pakete vom UDP-Port 68 an das Netzwerk senden, wie vom drahtlosen AP-Hersteller dokumentiert.

- **DNS-Filterung**. Konfigurieren von drahtlos Zugriffs Punkten, um zu verhindern, dass drahtlose Clients IP-Pakete vom TCP-oder UDP-Port 53 an das Netzwerk senden, wie vom drahtlosen AP-Hersteller dokumentiert.

## <a name="create-security-groups-for-wireless-users"></a>Erstellen von Sicherheitsgruppen für drahtlose Benutzer

Führen Sie die folgenden Schritte aus, um eine oder mehrere Sicherheitsgruppen für drahtlose Benutzer zu erstellen, und fügen Sie dann Benutzer der entsprechenden Sicherheitsgruppe für drahtlose Benutzer hinzu:

- [Erstellen einer Sicherheitsgruppe für drahtlose Benutzer](#bkmk_groups)

- [Hinzufügen von Benutzern zur drahtlos Sicherheitsgruppe](#bkmk_addusers)

### <a name="create-a-wireless-users-security-group"></a><a name="bkmk_groups"></a>Erstellen einer Sicherheitsgruppe für drahtlose Benutzer

Mit diesem Verfahren können Sie im MMC-Snap-in "Active Directory-Benutzer und-Computer" eine drahtlose Sicherheitsgruppe erstellen \( \) \- .

Sie müssen mindestens Mitglied der Gruppe **Domänen-Admins** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.

#### <a name="to-create-a-wireless-users-security-group"></a>So erstellen Sie eine Sicherheitsgruppe für drahtlose Benutzer

1. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Active Directory-Benutzer und -Computer**. Das Snap-in Active Directory Benutzer und Computer wird \- geöffnet. Klicken Sie auf den Knoten für Ihre Domäne, wenn diese noch nicht ausgewählt ist. Wenn Ihre Domäne beispielsweise den Namen „beispiel.com“ besitzt, klicken Sie auf **beispiel.com**.

2. Klicken Sie im Detailfenster mit \- der rechten Maustaste auf den Ordner, in dem Sie eine neue Gruppe hinzufügen möchten, klicken Sie mit der \( rechten \- Maustaste auf **Benutzer** \) , zeigen Sie auf **neu**, und klicken Sie dann auf **Gruppe**.

3. Geben Sie im Dialogfeld **Neues Objekt – Gruppe** in das Feld **Gruppenname** einen Namen für die neue Gruppe ein. Geben Sie beispielsweise **drahtlose Gruppe**ein.

4. Wählen Sie unter **Gruppenbereich** eine der folgenden Optionen aus:

    - **Lokale Domäne**

    - **Global**

    - **Universal**

5. Wählen Sie unter **Gruppentyp** die Option **Sicherheit** aus.

6. Klicken Sie auf **OK**.

Wenn Sie für drahtlose Benutzer mehr als eine Sicherheitsgruppe benötigen, wiederholen Sie diese Schritte, um weitere drahtlos Benutzergruppen zu erstellen. Später können Sie einzelne Netzwerk Richtlinien in NPS erstellen, um unterschiedliche Bedingungen und Einschränkungen für jede Gruppe anzuwenden und Ihnen unterschiedliche Zugriffsberechtigungen und konnektivitätsregeln zur Verfügung zu stellen.

### <a name="add-users-to-the-wireless-users-security-group"></a><a name="bkmk_addusers"></a>Hinzufügen von Benutzern zur Sicherheitsgruppe "drahtlose Benutzer"

Mithilfe dieses Verfahrens können Sie einen Benutzer, einen Computer oder eine Gruppe zur drahtlos Sicherheitsgruppe im MMC-Snap-in "Active Directory Benutzer und Computer Microsoft Management Console" hinzufügen \( \) \- .

Für dieses Verfahren müssen Sie mindestens Mitglied der Gruppe **Domänen-Admins** oder einer gleichwertigen Gruppe sein.

#### <a name="to-add-users-to-the-wireless-security-group"></a>So fügen Sie Benutzer zur drahtlos Sicherheitsgruppe hinzu

1. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Active Directory-Benutzer und -Computer**. Das MMC-Snap-In %%amp;quot;Active Directory-Benutzer und -Computer%%amp;quot; wird geöffnet. Klicken Sie auf den Knoten für Ihre Domäne, wenn diese noch nicht ausgewählt ist. Wenn Ihre Domäne beispielsweise den Namen „beispiel.com“ besitzt, klicken Sie auf **beispiel.com**.

2. Doppelklicken Sie im Detailbereich \- auf den Ordner, der die drahtlos Sicherheitsgruppe enthält.

3. Klicken Sie im Detailfenster mit \- der rechten Maustaste auf die Gruppe drahtlose Sicherheit, und klicken Sie dann auf **Eigenschaften**. Das Dialogfeld **Eigenschaften** für die Sicherheitsgruppe wird geöffnet.

4. Klicken Sie auf der Registerkarte **Mitglieder** auf **Hinzufügen**, und führen Sie dann eines der folgenden Verfahren aus, um entweder einen Computer hinzuzufügen oder einen Benutzer oder eine Gruppe hinzuzufügen.

##### <a name="to-add-a-user-or-group"></a>So fügen Sie einen Benutzer oder einer Gruppe hinzu

1. Geben Sie unter **Geben Sie die zu ausgewäfenden Objektnamen**ein den Namen des Benutzers oder der Gruppe ein, den Sie hinzufügen möchten, und klicken Sie dann auf **OK**.

2. Um anderen Benutzern oder Gruppen eine Gruppenmitgliedschaft zuzuweisen, wiederholen Sie Schritt 1 dieses Verfahrens.

##### <a name="to-add-a-computer"></a>So fügen Sie einen Computer hinzu

1. Klicken Sie auf **Objekttypen**. Das Dialogfeld **Objekttypen** wird geöffnet.

2. Wählen Sie unter **Objekttypen**die Option **Computer**aus, und klicken Sie dann auf **OK**.

3. Geben Sie unter **Geben Sie die zu ausgewäfenden Objektnamen**ein den Namen des Computers ein, den Sie hinzufügen möchten, und klicken Sie dann auf **OK**.

4. Um anderen Computern eine Gruppenmitgliedschaft zuzuweisen, wiederholen Sie die Schritte 1 \- 3 dieses Verfahrens.

## <a name="configure-wireless-network-ieee-80211-policies"></a><a name="bkmk_policies"></a>Konfigurieren von \( IEEE 802,11- \) Richtlinien für Drahtlos Netzwerke

Führen Sie die folgenden Schritte aus, um \( IEEE 802,11-Richtlinien für Drahtlos Netzwerke \) Gruppenrichtlinie Erweiterung

- [Öffnen oder hinzufügen und Öffnen eines Gruppenrichtlinie Objekts](#bkmk_opengpme)

- [Aktivieren der standardmäßigen Drahtlos Netzwerk- \( IEEE 802,11- \) Richtlinien](#bkmk_activate)

- [Konfigurieren der neuen Richtlinie für Drahtlos Netzwerke](#bkmk_policyconfig)

### <a name="open-or-add-and-open-a-group-policy-object"></a><a name="bkmk_opengpme"></a>Öffnen oder hinzufügen und Öffnen eines Gruppenrichtlinie Objekts

Standardmäßig wird das Gruppenrichtlinie Verwaltungs Feature auf Computern installiert, auf denen Windows Server 2016 ausgeführt wird, wenn die Active Directory Domain Services \( AD DS \) Server-Rolle installiert ist und der Server als Domänen Controller konfiguriert ist. Im folgenden Verfahren wird beschrieben, wie Sie die Gruppenrichtlinien-Verwaltungskonsole \( GPMC \) auf Ihrem Domänen Controller öffnen. Anschließend wird beschrieben, wie Sie entweder eine vorhandene Domänen \- Ebene Gruppenrichtlinie Objekt \( -GPO \) für die Bearbeitung öffnen oder ein neues Domänen-Gruppenrichtlinien Objekt erstellen und zum Bearbeiten öffnen.

Sie müssen mindestens Mitglied der Gruppe **Domänen-Admins** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.

#### <a name="to-open-or-add-and-open-a-group-policy-object"></a>So öffnen oder öffnen Sie ein Gruppenrichtlinie Objekt und öffnen es

1. Klicken Sie auf dem Domänen Controller auf **Start**, klicken Sie auf **Windows-Verwaltungs Tools**, und klicken Sie dann auf **Gruppenrichtlinie Verwaltung**. Die Gruppenrichtlinien-Verwaltungskonsole wird geöffnet.

2. Doppelklicken Sie im linken Bereich \- auf Ihre Gesamtstruktur. Doppel \- Klicken Sie z. b. auf **Forest: example.com**.

3. Doppel \- Klicken Sie im linken Bereich auf **Domänen**, und doppelklicken Sie dann auf \- die Domäne, für die Sie ein Gruppenrichtlinie Objekt verwalten möchten. Beispiel: Doppel \- Klicken Sie auf **example.com**.

4. Führen Sie eines der folgenden Verfahren aus:

    - **Um ein vorhandenes Gruppenrichtlinien Objekt auf Domänen \- Ebene für die Bearbeitung zu öffnen**, doppelklicken Sie auf die Domäne mit dem Gruppenrichtlinie Objekt, das Sie verwalten möchten, klicken Sie mit der rechten \- Maustaste auf die Domänen Richtlinie, die **Edit**Sie verwalten möchten, z. b. die Standard Domänen Richtlinie, und klicken **Gruppenrichtlinienverwaltungs-Editor** wird geöffnet.

    - Wenn Sie **ein neues Gruppenrichtlinie Objekt erstellen und für die Bearbeitung öffnen**möchten, klicken Sie mit \- der rechten Maustaste auf die Domäne, für die Sie ein neues Gruppenrichtlinie Objekt erstellen möchten, und klicken Sie dann auf Gruppenrichtlinien Objekt **in dieser Domäne erstellen und verknüpfen**.

        Geben Sie in **Neues Gruppenrichtlinienobjekt** in das Feld **Name** den Namen des neuen Gruppenrichtlinienobjekts ein, und klicken Sie dann auf **OK**.

        \-Klicken Sie mit der rechten Maustaste auf das neue Objekt Gruppenrichtlinie und klicken Sie dann auf **Bearbeiten**. **Gruppenrichtlinienverwaltungs-Editor** wird geöffnet.

Im nächsten Abschnitt verwenden Sie Gruppenrichtlinienverwaltungs-Editor, um eine drahtlose Richtlinie zu erstellen.

### <a name="activate-default-wireless-network-ieee-80211-policies"></a><a name="bkmk_activate"></a>Aktivieren der standardmäßigen Drahtlos Netzwerk- \( IEEE 802,11- \) Richtlinien

In diesem Verfahren wird beschrieben, wie Sie die standardmäßigen Drahtlos Netzwerk- \( IEEE 802,11- \) Richtlinien mithilfe der Gruppenrichtlinienverwaltungs-Editor \( GPME aktivieren \) .

>[!NOTE]
>Nachdem Sie die Version von **Windows Vista und höhere Versionen** der Drahtlos Netzwerk- \( IEEE 802,11- \) Richtlinien oder der **Windows XP** -Version aktiviert haben, wird die Versions Option automatisch aus der Liste der Optionen entfernt, wenn Sie mit der rechten \- Maustaste auf ** \( \) Richtlinien für Drahtlos Netzwerk IEEE 802,11**klicken. Dies liegt daran, dass nach der Auswahl einer Richtlinien Version die Richtlinie im Detailbereich der GPME hinzugefügt wird, wenn Sie den Knoten **Drahtlos Netzwerk \( IEEE 802,11- \) Richtlinien** auswählen. Dieser Status bleibt bestehen, es sei denn, Sie löschen die drahtlos Richtlinie. zu diesem Zeitpunkt kehrt die Version der drahtlos Richtlinie zum Kontext \- Menü für **Drahtlos Netzwerk \( IEEE 802,11- \) Richtlinien** in der GPME zurück. Außerdem werden die drahtlos Richtlinien nur im Bereich GPME-Details aufgeführt, wenn der Knoten ** \( \) Richtlinien für Drahtlos Netzwerk IEEE 802,11** ausgewählt ist.

Sie müssen mindestens Mitglied der Gruppe **Domänen-Admins** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.

#### <a name="to-activate-default-wireless-network-ieee-80211-policies"></a>So aktivieren Sie die \( IEEE 802,11-Standard \) Richtlinien

1. Führen Sie die vorherige Prozedur aus, **um ein Gruppenrichtlinie-Objekt zu öffnen oder hinzuzufügen und zu öffnen** , um die GPME zu öffnen.

2. Doppelklicken Sie in der GPME im linken Bereich auf \- **Computer Konfiguration**, Doppel \- Klicken Sie auf **Richtlinien**, Doppel \- Klicken Sie auf **Windows-Einstellungen**, und doppelklicken Sie dann auf \- **Sicherheitseinstellungen**.

![802.1 x-drahtlos Gruppenrichtlinie](../../../media/Wireless-GP/Wireless-GP.jpg)

3. Klicken Sie unter **Sicherheitseinstellungen**mit der rechten \- Maustaste auf **Drahtlos Netzwerk \( IEEE 802,11- \) Richtlinien**, und klicken Sie dann auf **neue drahtlos Richtlinie für Windows Vista und spätere Versionen erstellen**.

![802.1 x-drahtlos Richtlinie](../../../media/Wireless-Policy/Wireless-Policy.jpg)

4. Das Dialogfeld **Eigenschaften der neuen Drahtlos Netzwerk Richtlinie** wird geöffnet. Geben Sie unter **Richtlinien Name**einen neuen Namen für die Richtlinie ein, oder behalten Sie den Standardnamen bei. Klicken Sie zum Speichern der Richtlinie auf **OK** . Die Standard Richtlinie wird aktiviert und im Detailbereich der GPME mit dem neuen Namen aufgelistet, den Sie angegeben haben, oder mit dem Standardnamen **neue Drahtlos Netzwerk Richtlinie**.

![Eigenschaften der neuen Drahtlos Netzwerk Richtlinie](../../../media/Wireless-Policy-Properties/Wireless-Policy-Properties.jpg)

5. Doppelklicken Sie im Detailbereich \- auf **neue Drahtlos Netzwerk Richtlinie** , um Sie zu öffnen.

Im nächsten Abschnitt können Sie die Richtlinien Konfiguration, die Reihenfolge der Richtlinien Verarbeitung und die Netzwerk Berechtigungen ausführen.

### <a name="configure-the-new-wireless-network-policy"></a><a name="bkmk_policyconfig"></a>Konfigurieren der neuen Richtlinie für Drahtlos Netzwerke

Mithilfe der Verfahren in diesem Abschnitt können Sie die Richtlinie für das Drahtlos Netzwerk \( IEEE 802,11 konfigurieren \) . Diese Richtlinie ermöglicht Ihnen das Konfigurieren von Sicherheits-und Authentifizierungs Einstellungen, das Verwalten von drahtlos Profilen und das Angeben von Berechtigungen für Drahtlos Netzwerke, die nicht als bevorzugte Netzwerke konfiguriert sind.

- [Konfigurieren eines drahtlos Verbindungs Profils für das Peer- \- MS- \- CHAP v2](#bkmk_configureprofile)

- [Festlegen der bevorzugte Reihenfolge für drahtlos Verbindungsprofile](#bkmk_preferenceorder)

- [Definieren von Netzwerk Berechtigungen](#bkmk_permissions)

#### <a name="configure-a-wireless-connection-profile-for-peap-ms-chap-v2"></a><a name="bkmk_configureprofile"></a>Konfigurieren eines drahtlos Verbindungs Profils für das Peer- \- MS- \- CHAP v2

Dieses Verfahren enthält die Schritte, die erforderlich sind, um ein PAP \- MS \- CHAP v2-drahtlos Profil zu konfigurieren.

Zum Durchführen dieses Verfahrens ist mindestens die Mitgliedschaft in **Domänen-Admins** oder eine entsprechende Berechtigung erforderlich.

##### <a name="to-configure-a-wireless-connection-profile-for-peap-ms-chap-v2"></a>So konfigurieren Sie ein drahtlos Verbindungsprofil für "Peer- \- MS- \- CHAP v2"

1. Geben Sie in GPME im Dialogfeld Eigenschaften für Drahtlos Netzwerk für die Richtlinie, die Sie soeben erstellt haben, auf der Registerkarte **Allgemein** und in **Beschreibung**eine kurze Beschreibung für die Richtlinie ein.

2. Um anzugeben, dass die automatische WLAN-Konfiguration verwendet wird, um Einstellungen für den Drahtlos Netzwerkadapter zu konfigurieren, stellen Sie sicher, dass die Option **Windows WLAN-Auto Konfigurations Dienst für Clients verwenden**

3. Klicken Sie unter in **der Reihenfolge der unten aufgeführten Profile mit verfügbaren Netzwerken verbinden**auf **Hinzufügen**, und wählen Sie dann **Infrastruktur**aus. Das Dialogfeld **neue Profil Eigenschaften** wird geöffnet.

4. Geben Sie im Dialogfeld**Eigenschaften für neues Profil** auf der Registerkarte **Verbindung** im Feld **Profilname** einen neuen Namen für das Profil ein. Geben Sie z. b. **example.com WLAN Profile für Windows 10**ein.

5. Geben Sie unter **Netzwerk Name \( s \) \( SSID \) **die SSID ein, die der für Ihre drahtlos Zugriffspunkte konfigurierten SSID entspricht, und klicken Sie dann auf **Hinzufügen**.

    Wenn Ihre Bereitstellung mehrere SSIDs verwendet und jeder drahtlose Zugriffspunkt dieselben Drahtlos-Sicherheitseinstellungen nutzt, wiederholen Sie diesen Schritt, um den SSID für jeden drahtlosen Zugriffspunkt hinzuzufügen, für den dieses Profil angewendet werden soll.

    Wenn Ihre Bereitstellung mehrere SSIDs verwendet und die Sicherheitseinstellungen für die einzelnen SSIDs nicht übereinstimmen, konfigurieren Sie ein separates Profil für jede Gruppe von SSIDs, die dieselben Sicherheitseinstellungen nutzen. Wenn Sie z. b. eine Gruppe von drahtlos Zugriffs Punkten konfiguriert haben, die für die Verwendung von WPA2 \- Enterprise und AES konfiguriert sind, und eine andere Gruppe von drahtlos Zugriffs Punkten, um WPA \- Enterprise und TKIP zu verwenden, konfigurieren Sie für jede Gruppe von drahtlos Zugriffs Punkten

6. Wenn der Standardtext **newssid** vorhanden ist, wählen Sie ihn aus, und klicken Sie dann auf **Entfernen**.

7. Wenn Sie drahtlose Zugriffspunkte bereitgestellt haben, die das Übertragungssignal unterdrücken, wählen Sie **Verbinden, selbst wenn das Netzwerk keine Kennung aussendet**.

    > [!NOTE]
    > Wenn Sie diese Option aktivieren, kann ein Sicherheitsrisiko entstehen, da drahtlose Clients Verbindungen mit einem beliebigen Drahtlos Netzwerk suchen und versuchen, Verbindungen mit ihnen herzustellen. Standardmäßig ist diese Einstellung nicht aktiviert.

8. Klicken Sie auf die Registerkarte **Sicherheit** und auf **Erweitert**, und konfigurieren Sie dann Folgendes:

    1. Um die erweiterten 802.1X-Einstellungen zu konfigurieren, wählen Sie bei **IEEE 802.1X** die Option **Erweiterte 802.1X-Einstellungen erzwingen**.

        Wenn die erweiterten 802.1 x-Einstellungen erzwungen werden, reichen die Standardwerte für **Max. EAPOL- \- Start-Msgs**, **beibehaltenen Zeitraum**, **Start Zeitraum**und Authentifizierungs **Zeitraum** für typische drahtlos Bereitstellungen aus. Daher müssen Sie die Standardeinstellungen nicht ändern, es sei denn, Sie haben einen bestimmten Grund dafür.

    2. Um die einmalige Anmeldung zu aktivieren, wählen Sie **Einmaliges Anmelden für dieses Netzwerk aktivieren**.

    3. Die restlichen Standardwerte bei **Einmaliges Anmelden** sind für typische Drahtlosbereitstellungen ausreichend.

    4. Wenn Ihr drahtlos Zugriffspunkt für die Vorauthentifizierung konfiguriert ist, wählen Sie unter **schnelles Roaming**die Option \- **dieses Netzwerk verwendet \- Vorauthentifizierung**aus.

9. Um anzugeben, dass die drahtlose Kommunikation die Standards der Standard-140 \- 2 erfüllt, wählen Sie **Kryptografie im Modus "fps 140 \- 2 Certified" aus**.

10. Klicken Sie auf **OK** , um zur Registerkarte **Sicherheit** zurückzukehren. Wählen Sie unter **Sicherheitsmethoden für dieses Netzwerk auswählen**bei **Authentifizierung**die Option **WPA2 \- Enterprise** aus, wenn Sie von Ihrem drahtlos Zugriffspunkt und drahtlosen Client-Netzwerkadaptern unterstützt wird. Wählen Sie andernfalls **WPA \- Enterprise**aus.

11. Wählen Sie unter **Verschlüsselung**, wenn dies von Ihrem drahtlos Zugriffspunkt und den Netzwerkadaptern für drahtlose Clients unterstützt wird, **AES-CCMP**. Wenn Sie Zugriffspunkte und drahtlose Netzwerkadapter verwenden, die 802.11 AC unterstützen, wählen Sie **AES-gcmp**aus. Wählen Sie andernfalls **TKIP**.

    > [!NOTE]
    > Die Einstellungen für **Authentifizierung** und **Verschlüsselung** müssen den Einstellungen entsprechen, die auf Ihren drahtlos Zugriffs Punkten konfiguriert sind. Die Standardeinstellungen für **Authentifizierungsmodus**, **Maximale Authentifizierungsfehler**und **Cache Benutzerinformationen für nachfolgende Verbindungen mit diesem Netzwerk** sind für typische drahtlos Bereitstellungen ausreichend.

12. Wählen Sie unter **Netzwerk Authentifizierungsmethode auswählen**die Option **geschütztes EAP- \( PEAP \) **aus, und klicken Sie dann auf **Eigenschaften**. Das Dialogfeld **Eigenschaften für geschütztes EAP** wird geöffnet.

13. Überprüfen Sie unter **geschützte EAP-Eigenschaften**, ob **die Identität des Servers überprüft wird, indem Sie überprüfen, ob das Zertifikat** ausgewählt ist.

14. Wählen Sie unter **Vertrauenswürdige Stamm Zertifizierungs**stellen die Zertifizierungsstelle der vertrauenswürdigen Stamm Zertifizierungsstelle aus, die \( \) das Serverzertifikat für Ihren NPS ausgestellt hat.

    > [!NOTE]
    > Diese Einstellung beschränkt die Stamm-CAs, denen Clients vertrauen, auf die ausgewählten CAs. Wenn keine vertrauenswürdigen Stamm-CAs ausgewählt werden, Vertrauen die Clients allen Stamm Zertifizierungsstellen, die im Zertifikat Speicher vertrauenswürdiger Stamm Zertifizierungsstellen aufgelistet sind.

15. Wählen Sie in der Liste **Authentifizierungsmethode auswählen** die Option **Gesichertes Kennwort \( EAP \- MS \- CHAP v2 \) **aus.

16. Klicken Sie auf **Konfigurieren**. Überprüfen Sie im Dialogfeld **EAP-MSCHAPv2-Eigenschaften** , **ob der Windows-Anmelde Name und das Kennwort und die Domäne automatisch verwenden, \( sofern vorhanden \) ** , und klicken Sie auf **OK**.

17. Stellen Sie sicher, dass die Option **schnelle Wiederherstellung aktivieren aktiviert** ist, um die schnelle Wiederherstellung der Verbindung zu ermöglichen.

18. Wählen Sie zum Anfordern von Server-kryptobindungs-TLV bei Verbindungs versuchen die Option **trennen, wenn der Server nicht Kryptografiebindungs TLV enthält**.

19. Um anzugeben, dass die Benutzeridentität in Phase 1 der Authentifizierung maskiert wird, wählen Sie **Identitätsschutz aktivieren**aus, und geben Sie im Textfeld einen anonymen Identitäts Namen ein, oder lassen Sie das Textfeld leer.

    > [!HINWEISE]
    > - Die NPS-Richtlinie für 802.1 x Wireless muss mithilfe der NPS- **Verbindungs Anforderungs Richtlinie**erstellt werden. Wenn die NPS-Richtlinie mithilfe der NPS- **Netzwerk Richtlinie**erstellt wird, kann der Identitätsschutz nicht verwendet werden.
    > - Der Datenschutz der EAP-Identität wird von bestimmten EAP-Methoden bereitgestellt, bei denen eine leere oder eine anonyme Identität \( , die von der tatsächlichen Identität abweicht \) , als Antwort auf die EAP-Identitäts Anforderung gesendet Die Identität wird von der Peer-ID während der Authentifizierung zweimal gesendet. In der ersten Phase wird die Identität als nur-Text gesendet, und diese Identität wird für Routing Zwecke und nicht für die Client Authentifizierung verwendet. Die tatsächliche Identität –, die für die Authentifizierung verwendet wird – wird während der zweiten Phase der Authentifizierung innerhalb des sicheren Tunnels gesendet, der in der ersten Phase eingerichtet wurde. Wenn das Kontrollkästchen **Identitätsschutz aktivieren aktiviert** ist, wird der Benutzername durch den Eintrag ersetzt, der im Textfeld angegeben ist. Nehmen Sie beispielsweise an, dass **Identitätsschutz aktivieren** ausgewählt ist und der Identitätsdaten Schutz Alias **Anonym** im Textfeld angegeben wird. Bei einem Benutzer mit einem echten identitätsalias <strong>jdoe@example.com</strong> wird die in der ersten Phase der Authentifizierung gesendete Identität in geändert <strong>anonymous@example.com</strong> . Der Bereichs Teil der 1.-Phasen Identität wird nicht geändert, weil er für Routing Zwecke verwendet wird.

20. Klicken Sie auf **OK** , um das Dialogfeld **Eigenschaften für geschütztes EAP** zu schließen.
21. Klicken Sie zum Schließen der Registerkarte **Sicherheit** auf **OK** .
22. Wenn Sie zusätzliche Profile erstellen möchten, klicken Sie auf **Hinzufügen**, und wiederholen Sie dann die vorherigen Schritte, und wählen Sie dann verschiedene Optionen zum Anpassen der einzelnen Profile für die drahtlosen Clients und das Netzwerk aus, auf die das Profil angewendet werden soll. Wenn Sie das Hinzufügen von Profilen abgeschlossen haben, klicken Sie auf **OK** , um das Dialogfeld Eigenschaften der Drahtlos Netzwerk Richtlinie zu schließen.

Im nächsten Abschnitt können Sie die Richtlinien Profile für eine optimale Sicherheit anordnen.

#### <a name="set-the-preference-order-for-wireless-connection-profiles"></a><a name="bkmk_preferenceorder"></a>Festlegen der bevorzugte Reihenfolge für drahtlos Verbindungsprofile
Sie können dieses Verfahren verwenden, wenn Sie mehrere drahtlos Profile in ihrer Drahtlos Netzwerk Richtlinie erstellt haben und die Profile für eine optimale Effektivität und Sicherheit sortieren möchten.

Um sicherzustellen, dass drahtlose Clients eine Verbindung mit der höchsten Sicherheitsstufe herstellen, die Sie unterstützen können, platzieren Sie die restriktivsten Richtlinien am Anfang der Liste.

Wenn Sie z. b. über zwei Profile verfügen, eine für Clients, die WPA2 unterstützen, und eine für Clients, die WPA unterstützen, platzieren Sie das WPA2-Profil in der Liste höher. Dadurch wird sichergestellt, dass die Clients, die WPA2 unterstützen, diese Methode anstelle der weniger sicheren WPA-Methode für die Verbindung verwenden.

Dieses Verfahren enthält die Schritte zum Angeben der Reihenfolge, in der drahtlose Verbindungsprofile verwendet werden, um die Verbindung von Domänen Mitglieds-drahtlos Clients mit Drahtlos Netzwerken herzustellen.

Zum Durchführen dieses Verfahrens ist mindestens die Mitgliedschaft in **Domänen-Admins** oder eine entsprechende Berechtigung erforderlich.

##### <a name="to-set-the-preference-order-for-wireless-connection-profiles"></a>So legen Sie die bevorzugte Reihenfolge für drahtlos Verbindungsprofile fest

1. Klicken Sie in GPME im Dialogfeld Eigenschaften für Drahtlos Netzwerk für die soeben konfigurierte Richtlinie auf die Registerkarte **Allgemein** .

2. Wählen Sie auf der Registerkarte **Allgemein** in **der Reihenfolge der unten aufgeführten Profile Verbindung mit verfügbaren Netzwerken herstellen**aus, und klicken Sie dann auf die Schaltfläche mit dem Pfeil nach oben oder auf die Schaltfläche mit dem Pfeil nach unten, um das Profil an die gewünschte Position in der Liste zu verschieben.

3.  Wiederholen Sie Schritt 2 für jedes Profil, das Sie in der Liste verschieben möchten.

4.  Klicken Sie auf **OK** , um alle Änderungen zu speichern.

Im folgenden Abschnitt können Sie Netzwerk Berechtigungen für die drahtlos Richtlinie definieren.

#### <a name="define-network-permissions"></a><a name="bkmk_permissions"></a>Definieren von Netzwerk Berechtigungen
Sie können Einstellungen auf der Registerkarte **Netzwerk Berechtigungen** für die Domänen Mitglieder konfigurieren, auf die die Richtlinien für Drahtlos Netzwerk \( IEEE 802,11 \) angewendet werden.

Sie können nur die folgenden Einstellungen für Drahtlos Netzwerke anwenden, die auf der Registerkarte **Allgemein** auf der Seite **Eigenschaften der Drahtlos Netzwerk Richtlinie** nicht konfiguriert sind:

- Zulassen oder Verweigern von Verbindungen zu bestimmten Drahtlos Netzwerken, die Sie nach Netzwerktyp und Service Set Identifier \( -SSID angeben\)

- Zulassen oder Verweigern von Verbindungen mit Ad-hoc-Netzwerken

- Zulassen oder Verweigern von Verbindungen mit Infrastruktur Netzwerken

- Zulassen oder Verweigern von Benutzern zum Anzeigen von Netzwerktypen in \( Ad-hoc-oder-Infrastruktur, \) denen der Zugriff verweigert wird

- Hiermit wird Benutzern das Erstellen eines Profils gestattet oder verweigert, das für alle Benutzer gilt.

- Benutzer können mit Gruppenrichtlinie Profilen nur Verbindungen mit zugelassenen Netzwerken herstellen.

Sie müssen mindestens Mitglied der Gruppe **Domänen-Admins**oder einer entsprechenden Gruppe sein, um diese Verfahren ausführen zu können.

##### <a name="to-allow-or-deny-connections-to-specific-wireless-networks"></a>So lassen Sie Verbindungen zu bestimmten Drahtlos Netzwerken zu oder verweigern Sie

1. Klicken Sie in GPME im Dialogfeld Eigenschaften des drahtlos Netzwerks auf die Registerkarte **Netzwerk Berechtigungen** .

2. Klicken Sie auf der Registerkarte **Netzwerk Berechtigungen** auf **Hinzufügen**. Das Dialogfeld **neuer Berechtigungs Eintrag** wird geöffnet.

3. Geben Sie im Dialogfeld **neuer Berechtigungs Eintrag** im Feld **Netzwerk Name \( SSID \) ** die Netzwerk-SSID des Netzwerks ein, für das Sie Berechtigungen definieren möchten.

4.  Wählen Sie unter **Netzwerktyp**die Option **Infrastruktur** oder **Ad-hoc**aus.

    > [!NOTE]
    > Wenn Sie unsicher sind, ob es sich bei dem Übertragungs Netzwerk um ein Infrastruktur-oder Ad-hoc-Netzwerk handelt, können Sie zwei Netzwerk Berechtigungs Einträge konfigurieren, eine für jeden Netzwerktyp.

5. Wählen Sie unter **Berechtigung**die Option **zulassen** oder **verweigern**aus.

6. Klicken Sie auf **OK**, um zur Registerkarte **Netzwerk Berechtigungen** zurückzukehren.

##### <a name="to-specify-additional-network-permissions-optional"></a>So geben Sie zusätzliche Netzwerk \( Berechtigungen an\)

1.  Konfigurieren Sie auf der Registerkarte **Netzwerk Berechtigungen** eine oder alle der folgenden Aktionen:

    - Um Ihren Domänen Mitgliedern den Zugriff auf Ad-hoc-Netzwerke zu verweigern, wählen Sie **Verbindungen mit AD \- -hoc-Netzwerken verhindern**

    - Um Ihren Domänen Mitgliedern den Zugriff auf Infrastruktur Netzwerke zu verweigern, wählen Sie **Verbindungen mit Infrastruktur Netzwerken verhindern**aus.

    - Um Ihren Domänen Mitgliedern das Anzeigen von Netzwerktypen in \( Ad-hoc-oder-Infrastruktur zu ermöglichen \) , denen der Zugriff verweigert wird, wählen Sie **Benutzern gestatten, abgelehnte Netzwerke anzuzeigen**.

    - Damit Benutzerprofile erstellen können, die für alle Benutzer gelten, wählen Sie alle **Benutzerprofile erstellen**aus.

    - Wenn Sie angeben möchten, dass die Benutzer nur über Gruppenrichtlinie Profile eine Verbindung mit zugelassenen Netzwerken herstellen können, wählen Sie **nur Gruppenrichtlinie Profile für zulässige Netzwerke verwenden**.

## <a name="configure-your-npss"></a><a name="bkmk_nps"></a>Konfigurieren des NPSS
Führen Sie die folgenden Schritte aus, um NPSS zum Ausführen der 802.1 x-Authentifizierung für drahtlos Zugriff zu konfigurieren:

- [Registrieren von NPS in Active Directory Domain Services](#bkmk_npsreg)

- [Konfigurieren eines drahtlos Zugriffs Punkts als NPS-RADIUS-Client](#bkmk_radiusclient)

- [Erstellen von NPS-Richtlinien für 802.1 x Wireless mithilfe eines Assistenten](#bkmk_npspolicy)

### <a name="register-nps-in-active-directory-domain-services"></a><a name="bkmk_npsreg"></a>Registrieren von NPS in Active Directory Domain Services
Mit diesem Verfahren können Sie einen Server, auf dem der Netzwerk Richtlinien Server- \( NPS ausgeführt \) wird, in Active Directory Domain Services \( AD DS in der Domäne registrieren, in der \) das NPS Mitglied ist. Damit NPSS \- während des Autorisierungs Prozesses die Berechtigung zum Lesen der Eigenschaften von Benutzerkonten erhält, muss jede NPS in AD DS registriert werden. Beim Registrieren eines NPS wird der Server der Sicherheitsgruppe **RAS-und IAS-Server** in AD DS hinzugefügt.

>[!NOTE]
>NPS kann auf einem Domänen Controller oder auf einem dedizierten Server installiert werden. Führen Sie den folgenden Windows PowerShell-Befehl aus, um NPS zu installieren, falls Sie dies noch nicht getan haben:

```powershell
Install-WindowsFeature NPAS -IncludeManagementTools
```

Zum Durchführen dieses Verfahrens ist mindestens die Mitgliedschaft in **Domänen-Admins** oder eine entsprechende Berechtigung erforderlich.

#### <a name="to-register-an-nps-in-its-default-domain"></a>So registrieren Sie einen NPS in seiner Standard Domäne

1. Klicken Sie auf dem NPS in **Server-Manager**auf **Extras, und klicken Sie dann**auf **Netzwerk Richtlinien Server**. Das NPS-Snap- \- in wird geöffnet.

2. \-Klicken Sie mit der rechten Maustaste auf **NPS \( \) local**, und klicken Sie dann **auf Server registrieren in Active Directory** Das Dialogfeld **Netzwerkrichtlinienserver** wird geöffnet.

3. Klicken Sie im Dialogfeld **Netzwerkrichtlinienserver** auf **OK**, und klicken Sie erneut auf **OK**.

### <a name="configure-a-wireless-ap-as-an-nps-radius-client"></a><a name="bkmk_radiusclient"></a>Konfigurieren eines drahtlos Zugriffs Punkts als NPS-RADIUS-Client
Mithilfe dieses Verfahrens können Sie einen Zugriffs Steuerungspunkt (auch *Netzwerk Zugriffs Server- \( NAS \) *) als Remote Authentication Dial \- in User Service \( RADIUS- \) Client über das NPS-Snap- \- in konfigurieren.

>[!IMPORTANT]
>Clientcomputer, z. B. tragbare Computer und andere Computer, auf denen Clientbetriebssysteme ausgeführt werden, sind keine RADIUS-Clients. RADIUS-Clients sind Netzwerk Zugriffs Server – beispielsweise drahtlose Zugriffspunkte, 802.1 x- \- fähige Switches, VPN-Server für virtuelle private Netzwerke und DFÜ \( -Server \) \- – da Sie das RADIUS-Protokoll für die Kommunikation mit RADIUS-Servern wie z. b. NPSS verwenden.

Zum Durchführen dieses Verfahrens ist mindestens die Mitgliedschaft in **Domänen-Admins** oder eine entsprechende Berechtigung erforderlich.

#### <a name="to-add-a-network-access-server-as-a-radius-client-in-nps"></a>So fügen Sie einen Netzwerk Zugriffs Server als RADIUS-Client in NPS hinzu

1. Klicken Sie auf dem NPS in **Server-Manager**auf **Extras, und klicken Sie dann**auf **Netzwerk Richtlinien Server**. Das NPS-Snap- \- in wird geöffnet.

2. Doppelklicken Sie im NPS-Snap- \- in auf \- **RADIUS-Clients und-Server**. Klicken Sie mit der rechten \- Maustaste auf **RADIUS-Clients**und dann auf **neu**.

3. Vergewissern Sie sich, dass im **neuen RADIUS-Client**das Kontrollkästchen **diesen RADIUS-Client aktivieren aktiviert** ist.

4. Geben Sie im **neuen RADIUS-Client**unter Anzeige **Name**einen anzeigen Amen für den drahtlos Zugriffspunkt ein.

    Wenn Sie z. b. einen drahtlos Zugriffspunkt- \( AP \) namens AP 01 hinzufügen möchten \- , geben Sie **AP \- 01**ein.

5. Geben Sie unter **Adress \( - \) IP oder DNS**die IP-Adresse oder den voll qualifizierten Domänen Namen- \( FQDN \) für das NAS ein.

    Wenn Sie den FQDN eingeben, um zu überprüfen, ob der Name richtig ist und einer gültigen IP-Adresse zugeordnet ist, klicken Sie auf **überprüfen**, und klicken Sie dann unter **Adresse überprüfen**im Feld **Adresse** auf **Auflösen**. Wenn der FQDN-Name einer gültigen IP-Adresse zugeordnet ist, wird die IP-Adresse dieses NAS automatisch in der **IP-Adresse**angezeigt. Wenn der FQDN nicht in eine IP-Adresse aufgelöst wird, erhalten Sie eine Meldung, die besagt, dass kein solcher Host bekannt ist. Wenn dies der Fall ist, überprüfen Sie, ob Sie über den richtigen AP-Namen verfügen und dass der AP eingeschaltet und mit dem Netzwerk verbunden ist.

    Klicken Sie auf **OK** , um **Adresse überprüfen**zu schließen.

6. Führen Sie unter " **gemeinsamer geheimer**Schlüssel" unter " **Neuer RADIUS-Client**" einen der folgenden Schritte aus:

    - Um einen gemeinsamen RADIUS-Schlüssel manuell zu konfigurieren **, wählen Sie manuell aus, und**geben Sie dann unter **gemeinsames Geheimnis**das sichere Kennwort ein, das auch im NAS eingegeben wird. Geben Sie den gemeinsamen geheimen Schlüssel in **Confirm Shared Secret**erneut ein.

    - Aktivieren Sie zum automatischen Generieren eines gemeinsamen geheimen Schlüssels das Kontrollkästchen **generieren** , und klicken Sie dann auf die Schaltfläche **generieren** . Speichern Sie den generierten gemeinsamen geheimen Schlüssel, und verwenden Sie dann diesen Wert, um den NAS so zu konfigurieren, dass er mit dem NPS kommunizieren kann.

        >[!IMPORTANT]
        >Der gemeinsame RADIUS-Schlüssel, den Sie für Ihre virtuellen Zugriffs Elemente in NPS eingegeben haben, muss exakt mit dem gemeinsamen RADIUS-Geheimnis übereinstimmen, das in ihren tatsächlichen drahtlos Zugriffs Schlüsseln konfiguriert ist. Wenn Sie die NPS-Option verwenden, um einen gemeinsamen RADIUS-Schlüssel zu generieren, müssen Sie den übereinstimmenden tatsächlichen drahtlos Zugriffspunkt mit dem von NPS generierten gemeinsamen RADIUS-Schlüssel konfigurieren.

7. Geben Sie im **neuen RADIUS-Client**auf der Registerkarte **erweitert** unter **Herstellername**den Namen des NAS-Herstellers an. Wenn Sie sich nicht sicher sind, ob der NAS-Hersteller den Namen hat, wählen Sie **RADIUS Standard**aus.

8. Wenn Sie in **zusätzlichen Optionen**andere Authentifizierungsmethoden als EAP und PEAP verwenden und Ihr NAS die Verwendung des Message Authenticator-Attributs unterstützt, wählen Sie **Zugriffs Anforderungs Nachrichten müssen das Message \- Authenticator-Attribut enthalten**.

9. Klicken Sie auf **OK**. Ihr NAS wird in der Liste der auf dem NPS konfigurierten RADIUS-Clients angezeigt.

### <a name="create-nps-policies-for-8021x-wireless-using-a-wizard"></a><a name="bkmk_npspolicy"></a>Erstellen von NPS-Richtlinien für 802.1 x Wireless mithilfe eines Assistenten
Mithilfe dieses Verfahrens können Sie die Verbindungs Anforderungs Richtlinien und Netzwerk Richtlinien erstellen, die erforderlich sind, um entweder 802.1 x- \- fähige drahtlos Zugriffspunkte als Remote-Authentifizierungstyp für \- \( \) den RADIUS-Server, auf dem der Netzwerk Richtlinien Server ausgeführt wird, zu verwenden \( \) .
Nachdem Sie den Assistenten ausgeführt haben, werden die folgenden Richtlinien erstellt:

- Eine Verbindungs Anforderungs Richtlinie

- Eine Netzwerk Richtlinie

>[!NOTE]
>Wenn Sie neue Richtlinien für den authentifizierten 802.1 x-Zugriff erstellen müssen, können Sie den neuen IEEE 802.1 x-Assistenten für sichere Kabel-und Drahtlos Verbindungen ausführen.

Zum Durchführen dieses Verfahrens ist mindestens die Mitgliedschaft in **Domänen-Admins** oder eine entsprechende Berechtigung erforderlich.

#### <a name="create-policies-for-8021x-authenticated-wireless-by-using-a-wizard"></a>Erstellen von Richtlinien für 802.1 x-authentifizierte drahtlos Verbindungen mithilfe eines Assistenten

1. Öffnen Sie das Snap-in "NPS" \- . Wenn Sie nicht bereits ausgewählt ist, klicken Sie auf **NPS \( local \) **. Wenn Sie das NPS-MMC-Snap \- -in ausführen und Richtlinien für einen NPS-Remote Server erstellen möchten, wählen Sie den Server aus.

2. Wählen **Sie unter "** **Standard Konfiguration**" die Option **RADIUS-Server für drahtlose oder verkabelte 802.1 x-Verbindungen**aus. Der Text und die Links unterhalb des Texts ändern sich, um Ihre Auswahl widerzuspiegeln.

3. Klicken Sie auf **802.1 x konfigurieren**. Der Assistent zum Konfigurieren von 802.1 x wird geöffnet.

4.  Wählen Sie auf der Assistenten Seite **Select 802.1 x Connections** in **Type of 802.1 x Connections**den Typ **Secure Wireless Connections**aus, und geben Sie unter **Name**einen Namen für die Richtlinie ein, oder belassen Sie den Standardnamen **Secure Wireless Connections**. Klicken Sie auf **Weiter**.

5.  Auf der Seite Assistent zum **Angeben von 802.1 x-Switches** werden unter **RADIUS-Clients**alle 802.1 x-Switches und drahtlos Zugriffspunkte angezeigt, die Sie als RADIUS-Clients im NPS-Snap-in hinzugefügt haben \- . Führen Sie einen der folgenden Schritte aus:

    - Zum Hinzufügen zusätzlicher Netzwerk Zugriffs Server, z. b. drahtlos Zugriffspunkte, \( \) Klicken Sie in **RADIUS-Clients**auf **Hinzufügen**, und geben Sie dann unter **Neuer RADIUS-Client**die folgenden Informationen ein: Anzeige **Name**, ** \( IP-Adresse oder DNS \) **und **gemeinsamer geheimer**Schlüssel.

    - Wenn Sie die Einstellungen für NAS ändern möchten, wählen Sie in **RADIUS-Clients**den Zugriffspunkt aus, für den Sie die Einstellungen ändern möchten, und klicken Sie dann auf **Bearbeiten**. Ändern Sie die Einstellungen nach Bedarf.

    - Wenn Sie ein NAS aus der Liste entfernen möchten, wählen Sie in **RADIUS-Clients**den NAS aus, und klicken Sie dann auf **Entfernen**.

        >[!WARNING]
        >Durch das Entfernen eines RADIUS-Clients aus dem Assistenten zum **Konfigurieren von 802.1 x** wird der Client aus der NPS-Konfiguration gelöscht. Alle Ergänzungen, Änderungen und Löschungen, die Sie im Assistenten zum **Konfigurieren von 802.1 x** für RADIUS-Clients vornehmen, werden im NPS-Snap-in \- im Knoten " **RADIUS-Clients** " unter **NPS** \/ **-RADIUS-Clients und-Server**angezeigt. Wenn Sie z. b. den Assistenten zum Entfernen eines 802.1 x-Schalters verwenden, wird der Switch auch aus dem NPS-Snap- \- in entfernt.

6. Klicken Sie auf **Weiter**. Wählen Sie auf der Seite Assistent zum **Konfigurieren einer Authentifizierungsmethode** unter **Typ \( basierend auf Zugriffsmethode und Netzwerk \) Konfiguration**die Option **Microsoft: geschützter EAP- \( PEAP \) **aus, und klicken Sie dann auf **Konfigurieren**.

    >[!TIP]
    >Wenn Sie eine Fehlermeldung erhalten, die besagt, dass ein Zertifikat für die Verwendung mit der Authentifizierungsmethode nicht gefunden werden kann, und Sie haben Active Directory Zertifikat Dienste so konfiguriert, dass Zertifikate automatisch für RAS-und IAS-Server in Ihrem Netzwerk ausgestellt werden. Stellen Sie zunächst sicher, dass Sie die Schritte zum Registrieren von NPS in Active Directory Domain Services befolgt **haben, und**drücken Sie **Run**dann die folgenden Schritte **Open** **, um**die Gruppenrichtlinie zu aktualisieren: **Windows System** Wenn der Befehl Ergebnisse zurückgibt, die anzeigen, dass der Benutzer und der Computer Gruppenrichtlinie erfolgreich aktualisiert wurden, wählen Sie erneut **Microsoft: geschützter EAP- \( \) PEAP** aus, und klicken Sie dann auf **Konfigurieren**.
    >
    >Wenn Sie nach der Aktualisierung Gruppenrichtlinie weiterhin die Fehlermeldung erhalten, dass ein Zertifikat für die Verwendung mit der Authentifizierungsmethode nicht gefunden werden kann, wird das Zertifikat nicht angezeigt, weil es die Mindestanforderungen an das Serverzertifikat nicht erfüllt, wie im Hauptnetzwerk-Begleit Handbuch: bereitstellen [von Server Zertifikaten für Kabel-und drahtlos Bereitstellungen mit 802.1 x](../server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments.md)dokumentiert. Wenn dies der Fall ist, müssen Sie die NPS-Konfiguration einstellen, das Zertifikat, das für Ihre NPS ausgestellt wurde, widerrufen \( \) und dann die Anweisungen zum Konfigurieren eines neuen Zertifikats mithilfe des Bereitstellungs Handbuchs für Server Zertifikate befolgen.

7.  Vergewissern Sie sich, dass auf der Seite **geschützter EAP-Eigenschaften bearbeiten** unter **Zertifikat ausgestellt**das richtige NPS-Zertifikat ausgewählt ist, und gehen Sie dann wie folgt vor:

    >[!NOTE]
    >Überprüfen Sie, ob der Wert des **Ausstellers** für das im **Zertifikat ausgegebene**Zertifikat richtig ist. Der erwartete Aussteller für ein Zertifikat, das von einer Zertifizierungsstelle mit dem \( \) Namen corp\dc1 in der Domäne contoso.com Active Directory ausgeführt wird, ist beispielsweise **Corp \- DC1 \- ca**.

    - Um Benutzern das Roaming mit Ihren drahtlosen Computern zwischen Zugriffs Punkten zu ermöglichen, ohne dass Sie jedes Mal erneut authentifiziert werden müssen, wenn Sie einem neuen AP zugeordnet sind, **Aktivieren Sie schnelle Wiederherstellung der Verbindung aktivieren**.

    - Um anzugeben, dass die Verbindung von drahtlosen Clients den Netzwerk Authentifizierungsprozess beenden soll, wenn der RADIUS-Server den Länge Wert TLV für den kryptobindungstyp nicht erfüllt \- \- \( \) , wählen Sie **Clients ohne kryptoverbindung trennen**aus.

    - Wenn Sie die Richtlinien Einstellungen für den EAP-Typ ändern möchten, klicken Sie in **EAP-Typen**auf **Bearbeiten**, und ändern Sie in **EAP-MSCHAPv2-Eigenschaften**die Einstellungen nach Bedarf, und klicken Sie dann auf **OK**.

8.  Klicken Sie auf **OK**. Das Dialogfeld geschützte EAP-Eigenschaften bearbeiten wird geschlossen, und Sie kehren zum Assistenten zum Konfigurieren von " **802.1 x** " zurück. Klicken Sie auf **Weiter**.

9. Klicken Sie unter **Benutzergruppen angeben**auf **Hinzufügen**, und geben Sie dann den Namen der Sicherheitsgruppe ein, die Sie im Active Directory Benutzer und Computer im Snap-in für die drahtlosen Clients konfiguriert haben \- . Wenn Sie z. b. Ihre drahtlos Sicherheitsgruppe "drahtlos Gruppe" genannt haben, geben Sie **drahtlos Gruppe**ein. Klicken Sie auf **Weiter**.

10. Klicken Sie auf **Konfigurieren** , um die RADIUS-Standard Attribute und die Anbieter \- spezifischen Attribute für das virtuelle LAN \( -VLAN nach Bedarf zu konfigurieren \) . Dies wird in der Dokumentation Ihres drahtlosen AP-Hardwareherstellers angegeben. Klicken Sie auf **Weiter**.

11. Überprüfen Sie die Konfigurations Übersichts Details, und klicken Sie dann auf **Fertig**stellen.

Ihre NPS-Richtlinien werden jetzt erstellt, und Sie können mit der Verbindung zwischen drahtlos Computern und der Domäne fortfahren.

## <a name="join-new-wireless-computers-to-the-domain"></a><a name="bkmk_domain"></a>Neue drahtlos Computer der Domäne beitreten
Die einfachste Methode, um neue drahtlos Computer mit der Domäne zu verknüpfen, besteht darin, den Computer physisch an ein Segment des verkabelten LANs anzufügen, \( ein Segment, das nicht von einem 802.1 x-Switch gesteuert wird, \) bevor der Computer der Domäne hinzugefügt wird. Dies ist am einfachsten, weil die Einstellungen für drahtlose Gruppenrichtlinien automatisch und sofort angewendet werden. Wenn Sie eine eigene PKI bereitgestellt haben, erhält der Computer das Zertifizierungsstellen Zertifikat und platziert ihn im Zertifikat Speicher Vertrauenswürdige Stamm Zertifizierungsstellen, sodass der drahtlose Client NPSS mit von Ihrer Zertifizierungsstelle ausgestellten Server Zertifikaten vertraut.

Wenn ein neuer drahtloser Computer der Domäne hinzugefügt wurde, ist die bevorzugte Methode für Benutzer, sich bei der Domäne anzumelden, die Anmeldung über eine kabelgebundene Verbindung mit dem Netzwerk auszuführen.

### <a name="other-domain-join-methods"></a>Weitere Domänen Beitritts Methoden
In Fällen, in denen es nicht praktikabel ist, Computer über eine verkabelte Ethernet-Verbindung mit der Domäne zu verknüpfen, oder wenn sich der Benutzer nicht zum ersten Mal mithilfe einer kabelgebundenen Verbindung bei der Domäne anmelden kann, müssen Sie eine alternative Methode verwenden.

- **IT-Mitarbeiter Computer Konfiguration**. Ein Mitglied des IT-Personals verbindet einen drahtlos Computer mit der Domäne und konfiguriert ein Bootstrap-drahtlos Profil für einmaliges Anmelden. Bei dieser Methode verbindet der IT-Administrator den drahtlos Computer mit dem verkabelten Ethernet-Netzwerk und verknüpft den Computer mit der Domäne. Dann verteilt der Administrator den Computer an den Benutzer. Wenn der Benutzer den Computer ohne eine kabelgebundene Verbindung startet, werden die Domänen Anmelde Informationen, die manuell für die Benutzeranmeldung angegeben werden, zum Herstellen einer Verbindung mit dem Drahtlos Netzwerk und zum Anmelden bei der Domäne verwendet.

Weitere Informationen finden Sie im Abschnitt [beitreten zur Domäne und Anmelden mithilfe der Computer Konfigurations Methode des IT-Personals](#bkmk_itstaff) .

- **Bootstrap der drahtlos Profil Konfiguration durch Benutzer**. Der Benutzer konfiguriert den drahtlos Computer manuell mit einem Bootstrap-drahtlos Profil und wird der Domäne basierend auf den von einem IT-Administrator erworbenen Anweisungen beitreten. Das Bootstrap-drahtlos Profil ermöglicht dem Benutzer das Herstellen einer drahtlos Verbindung und das anschließende beitreten zur Domäne. Nachdem Sie den Computer der Domäne hinzufügen und den Computer neu gestartet haben, kann sich der Benutzer mit einer drahtlos Verbindung und seinen Anmelde Informationen für das Domänen Konto bei der Domäne anmelden.

Weitere Informationen finden Sie im Abschnitt [beitreten zur Domäne und Anmelden mit der Konfiguration des Bootstrap-drahtlos Profils durch Benutzer](#bkmk_userbootstrap).

### <a name="join-the-domain-and-log-on-by-using-the-it-staff-computer-configuration-method"></a><a name="bkmk_itstaff"></a>Beitreten zur Domäne und Anmelden mithilfe der Computer Konfigurations Methode des IT-Personals
Domänen Mitglieds Benutzer mit in die Domäne eingebundenen \- drahtlosen Client Computern können ein temporäres drahtlos Profil verwenden, um eine Verbindung mit einem Drahtlos Netzwerk mit 802.1 x herzustellen, \- ohne zuvor eine Verbindung mit dem verkabelten LAN herzustellen Dieses temporäre drahtlos Profil wird als *Bootstrap-drahtlos Profil*bezeichnet.

Ein Bootstrap-drahtlos Profil erfordert, dass der Benutzer die Anmelde Informationen für das Domänen Benutzerkonto manuell angibt, und überprüft nicht das Zertifikat des Remote Authentifizierungs wählelements \- im RADIUS-Server des Benutzer Dienstanbieter mit dem \( \) Netzwerk Richtlinien Server- \( NPS \) .

Nachdem die drahtlose Verbindung hergestellt wurde, wird Gruppenrichtlinie auf den drahtlosen Client Computer angewendet, und automatisch wird ein neues drahtlos Profil ausgegeben. Die neue Richtlinie verwendet die Anmelde Informationen des Computers und des Benutzerkontos für die Client Authentifizierung.

Außerdem \- überprüft der Client im Rahmen der gegenseitigen Peer-MS- \- CHAP v2-Authentifizierung mit dem neuen Profil anstelle des Bootstrap-Profils die Anmelde Informationen des RADIUS-Servers.

Nachdem Sie den Computer der Domäne hinzugefügt haben, verwenden Sie dieses Verfahren, um ein Bootstrap-drahtlos Profil für einmaliges Anmelden zu konfigurieren, bevor Sie den drahtlos Computer an den Domänen \- Mitglieds Benutzer verteilen.

#### <a name="to-configure-a-single-sign-on-bootstrap-wireless-profile"></a>So konfigurieren Sie ein Bootstrap-drahtlos Profil für einmaliges Anmelden

1. Erstellen Sie ein Bootstrap-Profil mithilfe des Verfahrens in diesem Handbuch unter [Konfigurieren eines drahtlos Verbindungs Profils für die Peer-MS-Version \- \- v2](#bkmk_configureprofile), und verwenden Sie die folgenden Einstellungen:

    - Peer- \- MS- \- CHAP v2-Authentifizierung

    - Überprüfen des RADIUS-Serverzertifikats deaktiviert

    - Einmaliges Anmelden aktiviert

2. Wählen Sie in den Eigenschaften der Drahtlos Netzwerk Richtlinie, in der Sie das neue Bootstrap-Profil erstellt haben, auf der Registerkarte **Allgemein** das Bootstrap-Profil aus, und klicken Sie dann auf **exportieren** , um das Profil in eine Netzwerkfreigabe, einen USB-Speicherstick oder einen anderen leicht zugänglichen Speicherort zu exportieren. Das Profil wird als *. XML-Datei an dem von Ihnen angegebenen Speicherort gespeichert.

3. Verknüpfen Sie den neuen drahtlos Computer mit der Domäne \( , z. b. über eine Ethernet-Verbindung, bei der keine IEEE 802.1 x-Authentifizierung erforderlich ist, \) und fügen Sie das Bootstrap-drahtlos Profil dem Computer mithilfe des Befehls **Netsh WLAN Add profile** hinzu.

    >[!NOTE]
    >Weitere Informationen finden Sie unter Netsh Commands for Wireless Local Area Network \( WLAN \) unter [http: \/ \/ TechNet.Microsoft.com \/ Library \/ dd744890. aspx](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd744890(v=ws.10)).

4. Verteilen Sie den neuen drahtlos Computer mit dem Verfahren zum Anmelden bei der Domäne mithilfe von Computern, auf denen Windows 10 ausgeführt wird, an den Benutzer.

Wenn der Benutzer den Computer startet, wird der Benutzer von Windows aufgefordert, den Namen und das Kennwort für den Domänen Benutzerkonto einzugeben. Da einmaliges Anmelden aktiviert ist, verwendet der Computer die Anmelde Informationen des Domänen Benutzerkontos, um zuerst eine Verbindung mit dem Drahtlos Netzwerk herzustellen und sich dann bei der Domäne anzumelden.

#### <a name="log-on-to-the-domain-using-computers-running-windows-10"></a><a name="bkmk_w10"></a>Anmelden bei der Domäne mit Computern, auf denen Windows 10 ausgeführt wird

1. Melden Sie den Computer ab, oder starten Sie ihn neu.

2. Drücken Sie eine beliebige Taste auf der Tastatur, oder klicken Sie auf den Desktop. Der Anmeldebildschirm wird angezeigt, und es wird ein lokaler Benutzerkonto Name und ein Kennwort-Eingabefeld unterhalb des Namens angezeigt. Melden Sie sich nicht mit dem lokalen Benutzerkonto an.

3. Klicken Sie in der unteren linken Ecke des Bildschirms auf **anderer Benutzer**. Der andere Benutzer Anmeldebildschirm wird mit zwei Feldern angezeigt: einer für den Benutzernamen und einer für das Kennwort. Unter dem Feld Kennwort befindet sich der Text **Anmelden bei:** und dann der Name der Domäne, der der Computer hinzugefügt wird. Wenn Ihre Domäne z. b. den Namen example.com hat, liest der Text **Sign on to: example**.

4. Geben Sie unter **Benutzername**Ihren Domänen Benutzernamen ein.

5. Geben Sie im Feld **Kennwort** das Domänenkennwort ein, und klicken Sie auf den Pfeil, oder drücken Sie die EINGABETASTE.

>[!NOTE]
>Wenn auf dem **anderen Benutzer** Bildschirm nicht der Text **Anmelden** bei und Ihr Domänen Name enthalten ist, geben Sie Ihren Benutzernamen im Format *Domäne \\ Benutzer*ein. Wenn Sie sich z. b. bei der Domäne example.com mit einem Konto mit dem Namen **User \- 01**anmelden möchten, geben Sie **Beispiel \\ Benutzer \- 01**ein.

### <a name="join-the-domain-and-log-on-by-using-bootstrap-wireless-profile-configuration-by-users"></a><a name="bkmk_userbootstrap"></a>Beitreten zur Domäne und Anmelden mithilfe der Bootstrap-drahtlos Profil Konfiguration durch Benutzer
Mit dieser Methode führen Sie die Schritte im Abschnitt Allgemeine Schritte aus. Anschließend geben Sie Ihren Domänen \- Mitglieds Benutzern die Anweisungen zum manuellen Konfigurieren eines drahtlos Computers mit einem Bootstrap-drahtlos Profil. Das Bootstrap-drahtlos Profil ermöglicht dem Benutzer das Herstellen einer drahtlos Verbindung und das anschließende beitreten zur Domäne. Nachdem der Computer der Domäne hinzugefügt und neu gestartet wurde, kann sich der Benutzer über eine drahtlose Verbindung bei der Domäne anmelden.

#### <a name="general-steps"></a>Allgemeine Schritte

1. Konfigurieren Sie in der **Systemsteuerung**für den Benutzer ein Administrator Konto für den lokalen Computer.

    >[!IMPORTANT]
    >Wenn Sie einen Computer einer Domäne hinzufügen möchten, muss der Benutzer am Computer mit dem lokalen Administrator Konto angemeldet sein. Alternativ muss der Benutzer die Anmelde Informationen für das lokale Administrator Konto beim Hinzufügen des Computers zur Domäne angeben. Außerdem muss der Benutzer über ein Benutzerkonto in der Domäne verfügen, der der Benutzer den Computer hinzufügen möchte. Beim Hinzufügen des Computers zur Domäne wird der Benutzer zur Eingabe der Anmelde Informationen des Domänen Kontos aufgefordert, den \( Benutzernamen und das Kennwort einzugeben \) .

2. Geben Sie Ihren Domänen Benutzern die Anweisungen zum Konfigurieren eines Bootstrap-drahtlos Profils, wie im folgenden Verfahren beschrieben, **um ein Bootstrap-drahtlos Profil zu konfigurieren**.
3. Außerdem können Sie den Benutzern sowohl die Anmelde Informationen des lokalen Computers als \( \) auch das Kennwort und \( das Kennwort des Domänen Benutzerkontos und das Kennwort des \) Domänen Benutzers in Form von *Domänen Name \\ username*sowie die Verfahren zum Hinzufügen des Computers zur Domäne und zum Anmelden bei der Domäne bereitstellen, wie im Windows Server 2016- [Kern Netzwerk Handbuch](../../core-network-guide.md)beschrieben.

#### <a name="to-configure-a-bootstrap-wireless-profile"></a>So konfigurieren Sie ein Bootstrap-drahtlos Profil

1. Verwenden Sie die Anmelde Informationen Ihres Netzwerkadministrators oder IT-Supports, um sich beim Computer mit dem Administrator Konto des lokalen Computers anzumelden.

2. \-Klicken Sie mit der rechten Maustaste auf den Desktop, und klicken Sie dann auf **Netzwerk-und Freigabe Center öffnen**. **Netzwerk- und Freigabecenter** wird geöffnet. Klicken Sie unter **Netzwerkeinstellungen ändern**auf **neue Verbindung oder Netzwerk einrichten**. Das Dialogfeld **Verbindung oder Netzwerk einrichten** wird geöffnet.

3. Klicken Sie auf **Verbindung mit einem Drahtlos Netzwerk manuell herstellen**, und klicken Sie dann auf **weiter**.

4. Geben **Sie in manuell Verbindung mit einem Drahtlos Netzwerk herstellen**in **Netzwerkname**den SSID-Namen des Zugriffs Punkts ein.

5. Wählen Sie unter **Sicherheitstyp**die Einstellung aus, die von Ihrem Administrator bereitgestellt wird.

6. Wählen Sie unter **Verschlüsselungstyp** und **Sicherheitsschlüssel**die vom Administrator bereitgestellten Einstellungen aus, oder geben Sie Sie ein.

7. Wählen Sie **diese Verbindung automatisch starten**aus, und klicken Sie dann auf **weiter**.

8. Klicken Sie in **hinzugefügt * * * Ihre Netzwerk-SSID*, klicken Sie auf **Verbindungseinstellungen ändern**.

9. Klicken Sie auf **Verbindungseinstellungen ändern**. Das Dialogfeld Eigenschaften des drahtlos Netzwerks *Ihres Netzwerks* wird geöffnet.

10. Klicken Sie auf die Registerkarte **Sicherheit** , und wählen Sie dann in **Netzwerk Authentifizierungsmethode auswählen**die Option **geschütztes EAP- \( PEAP \) **aus.

11. Klicken Sie auf **Einstellungen**. Die Seite mit den **geschützten EAP- \( PEAP- \) Eigenschaften** wird geöffnet.

12. Vergewissern Sie sich, dass auf der Seite **geschützte EAP- \( PEAP- \) Eigenschaften** die Option **Serverzertifikat** überprüfen deaktiviert ist, klicken Sie zweimal auf **OK** , und klicken Sie dann auf **Schließen**.

13. Windows versucht dann, eine Verbindung mit dem Drahtlos Netzwerk herzustellen. In den Einstellungen des Bootstrap-drahtlos Profils wird angegeben, dass Sie Ihre Anmelde Informationen für die Domäne angeben müssen. Wenn Sie von Windows *aufgefordert werden,* einen Kontonamen und ein Kennwort einzugeben, geben Sie die Anmelde Informationen für das Domänen Konto wie folgt ein: *Domänen Name \\ Benutzername*,

##### <a name="to-join-a-computer-to-the-domain"></a>So fügen Sie einen Computer der Domäne hinzu

1. Melden Sie sich bei dem Computer mit dem lokalen Administratorkonto an.

2. Geben Sie im Textfeld Suchen **PowerShell**ein. Klicken Sie in den Suchergebnissen mit der rechten Maustaste auf **Windows PowerShell**, und klicken Sie dann auf **als Administrator ausführen**. Windows PowerShell wird mit einer Eingabeaufforderung mit erhöhten Rechten geöffnet.

3. Geben Sie in Windows PowerShell den folgenden Befehl ein, und drücken Sie die EINGABETASTE: Stellen Sie sicher, dass Sie die Variable Domain Name durch den Namen der Domäne ersetzen, der Sie beitreten möchten.

    Add-Computer Domänen Name

4. Wenn Sie dazu aufgefordert werden, geben Sie Ihren Domänen Benutzernamen und Ihr Kennwort ein und klicken auf **OK**
5. Starten Sie den Computer neu.
6. Befolgen Sie die Anweisungen im vorherigen Abschnitt [Anmelden bei der Domäne mit Computern, auf denen Windows 10 ausgeführt](#bkmk_w10)wird.