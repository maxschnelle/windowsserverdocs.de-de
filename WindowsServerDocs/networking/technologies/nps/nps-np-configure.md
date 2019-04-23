---
title: Konfigurieren von Netzwerkrichtlinien
description: Dieses Thema enthält einen Überblick über die Netzwerkkonfiguration der Richtlinie für Netzwerkrichtlinienserver unter Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: fe77655a-e2be-4949-92e1-aaaa215d86ea
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e8a03a6c67ddd59549cefc9742ca92e0702f92a7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842001"
---
# <a name="configure-network-policies"></a>Konfigurieren von Netzwerkrichtlinien

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, um Netzwerkrichtlinien in NPS konfigurieren.

## <a name="add-a-network-policy"></a>Hinzufügen einer Netzwerkrichtlinie

Netzwerkrichtlinienserver \(NPS\) verwendet Netzwerk Richtlinien und die DFÜ-Eigenschaften von Benutzerkonten, um zu bestimmen, ob eine verbindungsanforderung autorisiert ist, eine Verbindung mit dem Netzwerk herstellen.

Sie können dieses Verfahren verwenden, so konfigurieren Sie eine neue Netzwerkrichtlinie in der NPS-Konsole oder der RAS-Konsole.

### <a name="performing-authorization"></a>Durchführen der Autorisierung

Wenn die Autorisierung des eine verbindungsanforderung von NPS ausgeführt wird, vergleicht er die Anforderung mit dem jede Netzwerkrichtlinie in der sortierten Liste der Richtlinien, beginnend mit der ersten Richtlinie, und klicken Sie dann in der Liste der konfigurierten Richtlinien verschieben. Wenn NPS eine Richtlinie findet, dessen Bedingungen die verbindungsanforderung übereinstimmen, verwendet NPS der Abgleichsrichtlinie und die Einwähleigenschaften des Benutzerkontos ein, um für die Autorisierung. Wenn die Einwähleigenschaften des Benutzerkontos so konfiguriert sind, dass der Zugriff oder Steuerelement Zugriff über die Netzwerkrichtlinien- und die verbindungsanforderung autorisiert ist, gilt der NPS die Einstellungen, die in der Netzwerkrichtlinie für die Verbindung konfiguriert sind.

Wenn Sie NPS nicht mit eine Netzwerkrichtlinie findet, die die verbindungsanforderung entspricht, wird die verbindungsanforderung abgelehnt, es sei denn, der DFÜ-Eigenschaften für das Benutzerkonto festgelegt werden, um Zugriff zu gewähren.

Wenn die Einwähleigenschaften des Benutzerkontos ein, den Zugriff verweigern festgelegt sind, wird die verbindungsanforderung von NPS abgelehnt.

### <a name="key-settings"></a>Wichtige Einstellungen

Wenn Sie den Assistenten für neue Netzwerkrichtlinien verwenden, um eine Netzwerkrichtlinie, die den Wert zu erstellen, die Sie, in angeben **Netzwerk Verbindungsmethode** wird verwendet, um automatisch konfigurieren die **Richtlinientyp** Bedingung: 

- Wenn Sie den Standardwert nicht angegeben lassen, wird die Netzwerkrichtlinie, die Sie Erstellen von NPS für alle Netzwerktypen Verbindung ausgewertet, die jede Art von Netzwerkzugriffsserver (NAS) verwenden.
- Wenn Sie eine Methode für die Verbindung angeben, wertet NPS die Netzwerkrichtlinie, nur dann, wenn die verbindungsanforderung aus dem Typ des Netzwerkzugriffsservers stammt, die Sie angeben.

Auf der **Zugriffsberechtigung** Seite Wählen Sie **Zugriffsgewährung** , wenn Sie die Richtlinie Benutzer mit dem Netzwerk verbinden können soll. Wenn Sie die Richtlinie verhindert, dass Benutzer die Verbindung mit Ihrem Netzwerk wählen möchten **Zugriffsverweigerung**. 

Zugriffsberechtigungen für die durch die Dial-in Eigenschaften von Benutzerkonten in Active Directory ermittelt werden ggf.&reg; Domain Services \(AD DS\), können Sie auswählen, die **Zugriff durch Benutzer DFÜ-Eigenschaftengesteuertwird** Kontrollkästchen.

Grundvoraussetzung für die Ausführung dieses Vorgangs ist die Mitgliedschaft in **Domänen-Admins** oder einer gleichwertigen Gruppe.

### <a name="to-add-a-network-policy"></a>Hinzufügen eine Netzwerkrichtlinie 

1. Öffnen Sie die NPS-Konsole, und doppelklicken Sie dann auf **Richtlinien**.

2. In der Konsolenstruktur mit der Maustaste **Netzwerkrichtlinien**, und klicken Sie auf **neu**. Der Assistent für neue Netzwerkrichtlinien wird geöffnet.

3. Verwenden Sie den Assistenten für neue Netzwerkrichtlinien, um eine Richtlinie zu erstellen.

## <a name="create-network-policies-for-dial-up-or-vpn-with-a-wizard"></a>Erstellen von Netzwerkrichtlinien für DFÜ- oder VPN mithilfe eines Assistenten

Sie können dieses Verfahren verwenden, Request-Richtlinien für die Verbindung erstellt und Netzwerkrichtlinien, die zur Bereitstellung von DFÜ-Server oder virtuellen privaten Netzwerk erforderlich \(VPN\) -Servern als Remote Authentication Dial-in User Service \(RADIUS\) Clients an den NPS RADIUS-Server.

>[!NOTE]
>Clientcomputer, z. B. Laptops und andere Computer mit Clientbetriebssystemen, sind keine RADIUS-Clients. RADIUS-Clients sind Netzwerkzugriffsserver – z. B. Drahtloszugriffspunkte, 802.1X-Authentifizierungsswitches, virtuelles privates Netzwerk \(VPN\) -Server und DFÜ-Server, da diese Geräte das RADIUS-Protokoll verwenden, um die Kommunikation mit RADIUS-Servern, z. B. NPSs.

Dieses Verfahren wird erläutert, wie die Assistenten für neue DFÜ- oder VPN-Verbindungen auf dem Netzwerkrichtlinienserver zu öffnen.

Nachdem Sie den Assistenten ausführen, werden die folgenden Richtlinien erstellt:

- Eine Verbindungsanforderungsrichtlinie
- Eine Netzwerkrichtlinie

Jedes Mal, wenn Sie neue Richtlinien für die DFÜ-Server und VPN-Server erstellen müssen, können Sie den Assistenten für neue DFÜ- oder VPN-Verbindungen ausführen.

Mit dem Assistenten für neue DFÜ- oder VPN-Verbindungen ist nicht der einzige Schritt, die zum Bereitstellen von DFÜ- oder VPN-Server als RADIUS-Clients an den NPS erforderlich. Beide Methoden für den Netzwerkzugriff erfordern, dass Sie zusätzliche Hardware und Software-Komponenten bereitstellen.

Grundvoraussetzung für die Ausführung dieses Vorgangs ist die Mitgliedschaft in **Domänen-Admins** oder einer gleichwertigen Gruppe.

### <a name="to-create-policies-for-dial-up-or-vpn-with-a-wizard"></a>Um Richtlinien für DFÜ- oder VPN mit einem Assistenten erstellen

1. Öffnen Sie die NPS-Konsole. Wenn sie nicht bereits ausgewählt ist, klicken Sie auf **NPS \(lokalen\)**. Wenn Sie eine remote-NPS-Richtlinien erstellen möchten, wählen Sie den Server.

2. In **Einstieg** und **Standardkonfiguration**Option **RADIUS-Server für DFÜ- oder VPN-Verbindungen**. Der Text und Links unter den Text ändern sich entsprechend Ihrer Auswahl.

3. Klicken Sie auf **konfigurieren VPN- oder DFÜ-Verbindung mit einem Assistenten**. Der Assistent für DFÜ- oder VPN-Verbindungen wird geöffnet.

4. Führen Sie die Anweisungen im Assistenten, um die Erstellung Ihrer neuen Richtlinien abzuschließen.

## <a name="create-network-policies-for-8021x-wired-or-wireless-with-a-wizard"></a>Erstellen von Netzwerkrichtlinien für 802.1 X Kabel- oder Drahtlosnetzwerk mithilfe eines Assistenten

Sie können dieses Verfahren verwenden, erstellt die Verbindungsanforderungsrichtlinie und Netzwerkrichtlinie, die zum Bereitstellen von entweder 802.1X-Authentifizierungsswitches oder 802.1 X drahtlose Zugriffspunkte als Remote Authentication Dial-in User Service (RADIUS)-Clients an den NPS erforderlich sind RADIUS-Server.

Dieses Verfahren wird erläutert, wie den Assistenten für neue IEEE 802.1 X sichere verkabelte und drahtlose Verbindungen auf dem Netzwerkrichtlinienserver zu starten.

Nachdem Sie den Assistenten ausführen, werden die folgenden Richtlinien erstellt:

- Eine Verbindungsanforderungsrichtlinie
- Eine Netzwerkrichtlinie

Sie können den Assistenten für neue IEEE 802.1 X Secure verkabelte und drahtlose ausführen, jedes Mal, wenn Sie neue Richtlinien für den Zugriff mit 802.1X-Authentifizierung erstellen möchten.

Ausführen des Assistenten für neue IEEE 802.1 X sichere verkabelte und Drahtlosverbindungen ist nicht der einzige Schritt, die zum Bereitstellen von 802.1 X Authentifizierung Switches und drahtlose Zugriffspunkte als RADIUS-Clients an den NPS erforderlich. Beide Methoden für den Netzwerkzugriff erfordern, dass Sie zusätzliche Hardware und Software-Komponenten bereitstellen.

Grundvoraussetzung für die Ausführung dieses Vorgangs ist die Mitgliedschaft in **Domänen-Admins** oder einer gleichwertigen Gruppe.

### <a name="to-create-policies-for-8021x-wired-or-wireless-with-a-wizard"></a>Um Richtlinien für 802.1X-authentifizierte Kabel- oder Drahtlosnetzwerk mithilfe eines Assistenten erstellen

1. Klicken Sie auf den NPS, im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Die NPS-Konsole wird geöffnet. 

2. Wenn sie nicht bereits ausgewählt ist, klicken Sie auf **NPS \(lokalen\)**. Wenn Sie eine remote-NPS-Richtlinien erstellen möchten, wählen Sie den Server.

3. In **Einstieg** und **Standardkonfiguration**Option **RADIUS-Server für 802.1 X drahtlose oder verkabelte 802.1X-Verbindungen**. Der Text und Links unter den Text ändern sich entsprechend Ihrer Auswahl.

4. Klicken Sie auf **konfigurieren 802.1 X mithilfe eines Assistenten**. Der neue IEEE 802.1 X Secure verkabelte und drahtlose-Assistent wird geöffnet.

5. Führen Sie die Anweisungen im Assistenten, um die Erstellung Ihrer neuen Richtlinien abzuschließen.

## <a name="configure-nps-to-ignore-user-account-dial-in-properties"></a>Konfigurieren von NPS, um die Einwähleigenschaften des Kontos ignorieren

Verwenden Sie dieses Verfahren zum Konfigurieren einer Netzwerkrichtlinie NPS, um die DFÜ-Eigenschaften von Benutzerkonten in Active Directory während des Autorisierungsprozesses zu ignorieren. Benutzerkonten in Active Directory-Benutzer und-Computer verfügen DFÜ-Eigenschaften, die NPS während des Autorisierungsprozesses ausgewertet wird, es sei denn, die **Netzwerk Zugriffsberechtigung** des Benutzerkontos-Eigenschaftensatz auf **Steuerelement Zugriff über die Netzwerkrichtlinie für NPS**. 

Es gibt zwei Situationen, in dem Sie NPS, um das Ignorieren der DFÜ-Eigenschaften von Benutzerkonten in Active Directory konfigurieren möchten:

- Wenn Sie NPS-Autorisierung mithilfe Netzwerks Gruppenrichtlinie vereinfachen möchten, aber nicht alle Ihre Benutzerkonten haben die **Netzwerk Zugriffsberechtigung** -Eigenschaft auf festgelegt **steuern den Zugriff über die Netzwerkrichtlinie für NPS**. Einige Benutzerkonten möglicherweise z. B. die **Netzwerk-Zugriffsberechtigung** Eigenschaftensatz des Benutzerkontos ein, um **Verweigern des Zugriffs** oder **zulassen des Zugriffs**.

- Wenn andere DFÜ-Eigenschaften von Benutzerkonten nicht in den Verbindungstyp gelten, die in der Netzwerkrichtlinie konfiguriert ist. Z. B. Eigenschaften außer die **Netzwerk Zugriffsberechtigung** Einstellung gelten nur für DFÜ- oder VPN-Verbindungen, aber die Netzwerkrichtlinie, die Sie erstellen, die für Switch- oder drahtlosen Verbindungen ist.

Sie können dieses Verfahren verwenden, Konfigurieren von NPS, um die Einwähleigenschaften des Kontos ignorieren. Wenn eine verbindungsanforderung die Netzwerkrichtlinie übereinstimmt, in dem Sie das Kontrollkästchen aktiviert ist, wird NPS nicht die Einwähleigenschaften des Benutzerkontos um zu bestimmen, ob der Benutzer oder Computer autorisiert ist, auf das Netzwerk zugreifen verwendet. nur die Einstellungen in der Netzwerkrichtlinie werden verwendet, um die Autorisierung zu ermitteln.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.

1. Klicken Sie auf den NPS, im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Die NPS-Konsole wird geöffnet.

2. Doppelklicken Sie auf **Richtlinien**, klicken Sie auf **Netzwerkrichtlinien**, und doppelklicken Sie dann im Detailbereich auf die Richtlinie, die Sie konfigurieren möchten.

3. In der Richtlinie **Eigenschaften** Dialogfelds die **Übersicht über die** Registerkarte **Zugriffsberechtigung**, wählen die **ignorieren DFÜ-Eigenschaften des Benutzerkontos**, und klicken Sie dann auf **OK**.

### <a name="to-configure-nps-to-ignore-user-account-dial-in-properties"></a>So konfigurieren Sie den NPS, um die Einwähleigenschaften des Kontos ignorieren



## <a name="configure-nps-for-vlans"></a>Konfigurieren von NPS für VLANs

Mithilfe von VLAN-fähigen Netzwerkzugriffsserver und NPS in Windows Server 2016, können Sie Gruppen von Benutzern mit nur den Zugriff auf die Netzwerkressourcen bereitstellen, die für ihre Sicherheitsberechtigungen geeignet sind. Beispielsweise können Sie Besucher mit drahtlosen Zugriff mit dem Internet bereitstellen ohne diese Zugriff auf das Netzwerk Ihrer Organisation. 

Darüber hinaus können VLANs Sie logisch Netzwerk Ressourcen gruppieren, die in unterschiedlichen physischen Standorten oder auf andere physische Subnetze vorhanden sind. Z. B. Mitglieder Ihre Vertriebsabteilung wenden und ihre Netzwerkressourcen wie Client-Computern, Servern und Drucker, möglicherweise in mehreren verschiedenen Gebäuden in Ihrer Organisation befinden, aber Sie können all diese Ressourcen platzieren, auf ein VLAN, die die gleiche IP-Adresse verwendet Adressbereich. Das VLAN und die Funktionen, die aus Sicht der Endbenutzer kann als ein einzelnes Subnetz.

Sie können auch die VLANs verwenden, wenn Sie ein Netzwerk zwischen den verschiedenen Gruppen von Benutzern verteilen möchten. Nachdem Sie ermittelt haben, wie Sie Ihre Gruppen definieren möchten, können Sie Sicherheitsgruppen in Active Directory-Benutzer und Computer-Snap-in erstellen, und klicken Sie dann die Gruppen Mitglieder hinzufügen.

### <a name="configure-a-network-policy-for-vlans"></a>Konfigurieren einer Netzwerkrichtlinie für VLANs

Sie können dieses Verfahren verwenden, so konfigurieren Sie eine Netzwerkrichtlinie, die von Benutzern mit einem VLAN zugewiesen. Bei der Verwendung von VLAN-fähigen Netzwerkhardware wie Router, Switches und den Zugriff auf Controller, können Sie die Netzwerkrichtlinie um anzuweisen, die Clientzugriffsservern Mitgliedern bestimmter Active Directory-Gruppen auf bestimmten VLANs platzieren konfigurieren. Diese Möglichkeit, die Gruppe von Netzwerkressourcen mit VLANs logisch bietet Flexibilität beim Entwerfen und Implementieren von netzwerklösungen.

Wenn Sie die Einstellungen von einem NPS-Netzwerkrichtlinien für die Verwendung mit VLANs konfigurieren, müssen Sie konfigurieren, dass die Attribute **Mittel-Tunneltyp**, **Tunnel-Pvt-Group-ID**, **Tunneltyp**, und **Tunnel-Tag**. 

Dieses Verfahren wird als Richtlinie bereitgestellt wird. Konfiguration des Netzwerks möglicherweise andere Einstellungen als die unten beschrieben.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.

### <a name="to-configure-a-network-policy-for-vlans"></a>So konfigurieren Sie eine Netzwerkrichtlinie für VLANs

1. Klicken Sie auf den NPS, im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Die NPS-Konsole wird geöffnet.

2. Doppelklicken Sie auf **Richtlinien**, klicken Sie auf **Netzwerkrichtlinien**, und doppelklicken Sie dann im Detailbereich auf die Richtlinie, die Sie konfigurieren möchten.

3. In der Richtlinie **Eigenschaften** Dialogfeld klicken Sie auf die **Einstellungen** Registerkarte.

4. In der Richtlinie **Eigenschaften**im **Einstellungen**im **RADIUS-Attribute**, sicher, dass **Standard** ausgewählt ist.

5. Klicken Sie im Bereich "Details" in **Attribute**, **Diensttyp** Attribut konfiguriert ist, hat den Standardwert des **"eingerahmt"**. Standardmäßig wird für Richtlinien mit VPN- und DFÜ-Zugriff auf Methoden der **"eingerahmt"-Protokoll** Attribut konfiguriert ist, mit dem Wert **PPP**. Wenn zusätzliche Verbindung erforderliche Attribute für VLANs angeben möchten, klicken Sie auf **hinzufügen**. Die **RADIUS-Standardattribut** Dialogfeld wird geöffnet.

6. In **RADIUS-Standardattribut**im Attribute einen Bildlauf nach unten zu, und fügen Sie die folgenden Attribute hinzu:

    - **Tunnel-Medium-Type**. Wählen Sie einen Wert für die zuvor vorgenommenen Auswahlen, die Sie für die Richtlinie vorgenommen haben. Wählen Sie z. B. ist die Netzwerkrichtlinie, die Sie Konfigurieren einer Richtlinie für Drahtlosnetzwerke, **Wert: 802 (umfasst alle 802 Media plus kanonischen Format Ethernet)**.

    - **Tunnel-Pvt-Group-ID**. Geben Sie die ganze Zahl, die die VLAN-Nummer darstellt, die Mitglieder der Gruppe zugewiesen werden soll. 

    - **Tunnel-Type**. Wählen Sie **virtuelle LANs (VLANs)**.


7. In **RADIUS-Standardattribut**, klicken Sie auf **schließen**. 

8. Wenn Ihre Netzwerkzugriffsserver (NAS) erforderlich ist der **Tunnel-Tag** Attribut, verwenden Sie die folgenden Schritte aus, zum Hinzufügen der **Tunnel-Tag** -Attribut auf die Netzwerkrichtlinie. Wenn die dieses Attribut nicht von der NAS-Dokumentation erwähnt werden, fügen Sie es nicht an der Richtlinie. Falls erforderlich, fügen Sie die Attribute wie folgt:

    - In der Richtlinie **Eigenschaften**im **Einstellungen**im **RADIUS-Attribute**, klicken Sie auf **Hersteller bestimmte**. 

    - Klicken Sie im Detailbereich auf **hinzufügen**. Die **bestimmten Hersteller-Attribut hinzufügen** Dialogfeld wird geöffnet.

    - In **Attribute**, führen Sie einen Bildlauf nach unten zu, und wählen Sie **Tunnel-Tag**, und klicken Sie dann auf **hinzufügen**. Die **Attributinformationen** Dialogfeld wird geöffnet. 

    - In **-Attributwert**, geben Sie den Wert an, die Sie in der Hardwaredokumentation zu erhalten.

## <a name="configure-the-eap-payload-size"></a>Konfigurieren Sie die Größe der EAP-Nutzlast

In einigen Fällen verwerfen Routern oder Firewalls Pakete, da sie konfiguriert sind, um Pakete zu verwerfen, die Fragmentierung zu erfordern.

Wenn Sie NPS bereitstellen, mit den Netzwerkrichtlinien, die das Extensible Authentication-Protokoll verwenden \(EAP\) mit Transport Layer Security \(TLS\), oder EAP-TLS als Authentifizierungsmethode, der maximale Standardwert Maximum Transmission Unit \(MTU\) NPS für EAP-Nutzlasten verwendet 1500 Bytes ist. 

Diese maximale Größe für die EAP-Nutzlast kann RADIUS-Nachrichten erstellen, die Fragmentierung durch einen Router oder eine Firewall zwischen den NPS- und RADIUS-Client erfordern. Ist dies der Fall, kann einen Router oder Firewall zwischen dem RADIUS-Client und dem NPS positioniert automatisch einige Fragmente Authentifizierungsfehler und der Unfähigkeit des Access-Clients für die Verbindung mit dem Netzwerk zu verwerfen.

Verwenden Sie das folgende Verfahren, um die maximale Größe zu verringern, die NPS für EAP-Nutzlasten verwendet werden, indem Sie das "eingerahmt"-MTU-Attribut in einer Netzwerkrichtlinie auf einen Wert nicht größer als 1344 anpassen.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.

### <a name="to-configure-the-framed-mtu-attribute"></a>So konfigurieren Sie das Attribut "eingerahmt"-MTU

1. Klicken Sie auf den NPS, im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Die NPS-Konsole wird geöffnet.
 
2. Doppelklicken Sie auf **Richtlinien**, klicken Sie auf **Netzwerkrichtlinien**, und doppelklicken Sie dann im Detailbereich auf die Richtlinie, die Sie konfigurieren möchten.

3. In der Richtlinie **Eigenschaften** Dialogfeld klicken Sie auf die **Einstellungen** Registerkarte.

4. In **Einstellungen**im **RADIUS-Attribute**, klicken Sie auf **Standard**. Klicken Sie im Detailbereich auf **hinzufügen**. Die **RADIUS-Standardattribut** Dialogfeld wird geöffnet.

5. In **Attribute**, scrollen Sie zu, und klicken Sie auf **"eingerahmt"-MTU**, und klicken Sie dann auf **hinzufügen**. Die **Attributinformationen** Dialogfeld wird geöffnet.

6. In **Attributwert**, geben Sie einen Wert gleich oder kleiner als **1344**. Klicken Sie auf **OK**, klicken Sie auf **schließen**, und klicken Sie dann auf **OK**.



Weitere Informationen zu Richtlinien für Netzwerke, finden Sie unter [Netzwerkrichtlinien](nps-np-overview.md).

Beispiele für die Syntax zum Angeben von Mustervergleich Richtlinienattribute Netzwerk, finden Sie unter [Verwenden von regulären Ausdrücken in NPS](nps-crp-reg-expressions.md).

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).
