---
title: Konfigurieren von Netzwerkrichtlinien
description: Dieses Thema enthält eine Übersicht über die Netzwerkkonfiguration der Richtlinie für Netzwerkrichtlinienserver in Windows Server2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: fe77655a-e2be-4949-92e1-aaaa215d86ea
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9abcd9343f10100884f96d17d82704382e2af760
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="configure-network-policies"></a>Konfigurieren von Netzwerkrichtlinien

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie auf dem Netzwerkrichtlinienserver Netzwerkrichtlinien konfigurieren.

## <a name="add-a-network-policy"></a>Hinzufügen einer Netzwerkrichtlinie

Network Policy Server \(NPS\) Netzwerkrichtlinien verwendet, und die DFÜ-Eigenschaften von Benutzerkonten bestimmen, ob eine Anforderung der Verbindung berechtigt ist, mit dem Netzwerk verbinden.

Sie können dieses Verfahren verwenden, so konfigurieren Sie eine neue Netzwerkrichtlinie in der NPS-Konsole oder der RAS-Konsole.

### <a name="performing-authorization"></a>Durchführen der Autorisierung

Wenn die Autorisierung einer Anforderung für die Verbindung von NPS ausgeführt wird, wird die Anforderung mit jede Netzwerkrichtlinie in der sortierte Liste der Richtlinien, beginnend mit der ersten Richtlinie, und ihn dann entlang der Liste der konfigurierten Richtlinien verglichen. NPS eine Richtlinie gefunden, deren Suchkriterien die Verbindungsanforderung, verwendet NPS der entsprechenden Richtlinie und der DFÜ-Eigenschaften des Benutzerkontos für die Autorisierung. Wenn die DFÜ-Eigenschaften des Benutzerkontos zum Gewähren von Zugriff oder Steuerelement Zugriff über die Netzwerkrichtlinien-konfiguriert sind, und die Verbindungsanforderung berechtigt ist, gilt NPS die Einstellungen, die in der Netzwerkrichtlinie für die Verbindung konfiguriert sind.

Wenn NPS eine Netzwerkrichtlinie nicht findet, die die Verbindungsanforderung entspricht, wird die Verbindungsanforderung abgelehnt, es sei denn, die DFÜ-Eigenschaften für das Benutzerkonto festgelegt sind, um Zugriff zu gewähren.

Wenn die DFÜ-Eigenschaften des Benutzerkontos festgelegt sind, um Zugriff zu verweigern, wird die Verbindungsanforderung von NPS abgelehnt.

### <a name="key-settings"></a>Schlüsseleinstellungen

Wenn Sie den Assistenten für neue Netzwerkrichtlinien verwenden, eine Netzwerkrichtlinie, die den Wert zu erstellen, die Sie, in angeben **Netzwerk Verbindungsmethode** wird verwendet, um die automatische Konfiguration der **Richtlinientyp** Bedingung: 

- Wenn Sie den Standardwert beibehalten, wird die Netzwerkrichtlinie, die Sie erstellen für alle Typen von NPS ausgewertet, die jede Art von Netzwerkzugriffsserver (NAS) verwenden.
- Wenn Sie eine Methode für die Verbindung angeben, wertet NPS die Netzwerkrichtlinie nur dann, wenn die Verbindungsanfrage vom Typ des Netzwerkzugriffsservers stammt, die Sie angeben.

Auf der **Zugriffsberechtigung** Seite müssen Sie auswählen, **Zugriff gewährt** Wenn Sie die Richtlinie zum Zulassen der Benutzer eine Verbindung mit dem Netzwerk herstellen möchten. Wenn Sie möchten, dass die Richtlinie, um zu verhindern, dass Benutzer eine Verbindung mit Ihrem Netzwerk, wählen **"Zugriff verweigert"**. 

Wenn Berechtigungen durch DFÜ-Eigenschaften des Benutzerkontos in Active Directory ermittelt werden soll&reg; Domänendienste \(AD DS\), wählen Sie die **Zugriff wird bestimmt, indem Benutzer DFÜ-Eigenschaften** Kontrollkästchen.

Mitgliedschaft in **Domänen-Admins**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.

### <a name="to-add-a-network-policy"></a>So fügen Sie eine Netzwerkrichtlinie hinzu 

1. Öffnen Sie die NPS-Konsole, und doppelklicken Sie dann auf **Richtlinien**.

2. In der Konsolenstruktur mit der rechten Maustaste **Netzwerkrichtlinien**, und klicken Sie auf **neu**. Die Assistenten für neue Netzwerkrichtlinien wird geöffnet.

3. Verwenden Sie den Assistenten für neue Netzwerkrichtlinien, um eine Richtlinie erstellen.

## <a name="create-network-policies-for-dial-up-or-vpn-with-a-wizard"></a>Erstellen von Netzwerkrichtlinien für DFÜ- oder VPN mithilfe eines Assistenten

Dieses Verfahrens können zum Erstellen des Verbindungsanforderungsrichtlinien und Netzwerkrichtlinien für die Bereitstellung von DFÜ-Server oder virtuellen privaten Netzwerks \(VPN\) Server als Remote Authentication Dial-in User Service \(RADIUS\) Clients an den NPS-RADIUS-Server erforderlich.

>[!NOTE]
>Clientcomputer, z.B. Laptops und andere Computer mit Clientbetriebssystemen, sind keine RADIUS-Clients. RADIUS-Clients sind Netzwerkzugriffsserver – z.B. Drahtloszugriffspunkte, 802.1X-Authentifizierungsswitches, VPN-\(VPN\) Server und DFÜ-Server, da diese Geräte das RADIUS-Protokoll verwendet, um die Kommunikation mit RADIUS-Servern, z.B. NPS.

Dieses Verfahren wird erläutert, wie die Assistenten für neue DFÜ- oder VPN-Netzwerk-Verbindungen auf dem Netzwerkrichtlinienserver zu öffnen.

Nachdem Sie den Assistenten ausführen, werden die folgenden Richtlinien erstellt:

- Eine Verbindungsanforderungsrichtlinie
- Eine Netzwerkrichtlinie

Jedes Mal, wenn Sie neue Richtlinien für DFÜ- und VPN-Server erstellen möchten, können Sie den Assistenten für neue DFÜ-Verbindung oder virtuelle Private Netzwerkverbindungen ausführen.

Mit dem Assistenten für neue DFÜ- oder VPN-Netzwerk-Verbindungen ist nicht der einzige Schrittzum Bereitstellen von DFÜ- oder VPN-Server als RADIUS-Clients auf dem NPS-Server erforderlich. Beide Methoden für den Netzwerkzugriff erforderlich, dass Sie zusätzliche Hardware- und Softwarekomponenten bereitstellen.

Mitgliedschaft in **Domänen-Admins**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.

### <a name="to-create-policies-for-dial-up-or-vpn-with-a-wizard"></a>Richtlinien für DFÜ- oder VPN mithilfe eines Assistenten erstellen

1. Öffnen Sie die NPS-Konsole. Wenn es nicht bereits ausgewählt ist, klicken Sie auf **NPS \(Local\)**. Wenn Sie Richtlinien auf einem NPS-Remoteserver erstellen möchten, wählen Sie den Server.

2. In **Einstieg** und **Standardkonfiguration**Option **RADIUS-Server für DFÜ- oder VPN-Verbindungen**. Der Text und Links unter dem Text werden entsprechend Ihrer Auswahl angepasst.

3. Klicken Sie auf **konfigurieren VPN- oder DFÜ-Verbindung mit einem Assistenten**. Der Assistent für DFÜ- oder VPN-Netzwerk-Verbindungen wird geöffnet.

4. Folgen Sie den Anweisungen im Assistenten zum Abschließen der Erstellung der neuen Richtlinien.

## <a name="create-network-policies-for-8021x-wired-or-wireless-with-a-wizard"></a>Erstellen von Netzwerkrichtlinien für 802.1 X Kabel- oder Drahtlosnetzwerk mit einem Assistenten

Sie können dieses Verfahren verwenden, zum Erstellen der Verbindungsanforderungsrichtlinie und Netzwerkrichtlinie, die zum Bereitstellen von 802.1X-Authentifizierungsswitches oder 802.1 X drahtlose Zugriffspunkte als Remote Authentication Dial-in User Service (RADIUS)-Clients an den NPS-RADIUS-Server erforderlich sind.

Dieses Verfahren wird erläutert, wie die Assistenten für neue IEEE 802.1 X sichere verkabelte und drahtlose in NPS starten.

Nachdem Sie den Assistenten ausführen, werden die folgenden Richtlinien erstellt:

- Eine Verbindungsanforderungsrichtlinie
- Eine Netzwerkrichtlinie

Jedes Mal, wenn Sie neue Richtlinien für Zugriff mit 802.1X-Authentifizierung erstellen müssen, können Sie den Assistenten für neue IEEE 802.1 X sichere verkabelte und drahtlose ausführen.

Ausführen des Assistenten für neue IEEE 802.1 X sichere verkabelte und drahtlose Verbindung ist nicht der einzige Schrittzum Bereitstellen von 802.1 X-Authentifizierung Switches und drahtlose Zugriffspunkte als RADIUS-Clients an den Netzwerkrichtlinienserver erforderlich. Beide Methoden für den Netzwerkzugriff erforderlich, dass Sie zusätzliche Hardware- und Softwarekomponenten bereitstellen.

Mitgliedschaft in **Domänen-Admins**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.

### <a name="to-create-policies-for-8021x-wired-or-wireless-with-a-wizard"></a>Um die Richtlinien für 802.1X-authentifizierte Kabel- oder Drahtlosnetzwerk mit einem Assistenten erstellen

1. Klicken Sie auf dem NPS-Server im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Die NPS-Konsole wird geöffnet. 

2. Wenn es nicht bereits ausgewählt ist, klicken Sie auf **NPS \(Local\)**. Wenn Sie Richtlinien auf einem NPS-Remoteserver erstellen möchten, wählen Sie den Server.

3. In **Einstieg** und **Standardkonfiguration**Option **RADIUS-Server für 802.1 X drahtlose oder verkabelte 802.1X-Verbindungen**. Der Text und Links unter dem Text werden entsprechend Ihrer Auswahl angepasst.

4. Klicken Sie auf **konfigurieren 802.1 X mithilfe eines Assistenten**. Der neue IEEE 802.1 X sichere verkabelte und Wireless-Assistent wird geöffnet.

5. Folgen Sie den Anweisungen im Assistenten zum Abschließen der Erstellung der neuen Richtlinien.

## <a name="configure-nps-to-ignore-user-account-dial-in-properties"></a>Konfigurieren von NPS-Einwahl Eigenschaften des Benutzerkontos ignorieren

Verwenden Sie dieses Verfahren zum Konfigurieren einer Richtlinie NPS Netzwerk, um die DFÜ-Eigenschaften von Benutzerkonten in Active Directory während des Autorisierungsprozesses zu ignorieren. Benutzerkonten in Active Directory-Benutzer und -Computer verfügen, DFÜ-Eigenschaften, die NPS während des Autorisierungsprozesses ausgewertet wird, es sei denn, die **Netzwerkzugriffsberechtigungen** -Eigenschaft des Benutzerkontos auf festgelegt ist **steuern den Zugriff über die NPS-Netzwerkrichtlinien**. 

Es gibt zwei Situationen, in denen Sie NPS ignorieren die DFÜ-Eigenschaften von Benutzerkonten in Active Directory konfigurieren möchten:

- Wenn Sie NPS-Autorisierung mithilfe von Netzwerkrichtlinien vereinfachen möchten, aber nicht alle Benutzerkonten der **Netzwerkzugriffsberechtigungen** -Eigenschaft **steuern den Zugriff über die NPS-Netzwerkrichtlinien**. Zum Beispiel möglicherweise einige Benutzerkonten die **Netzwerkzugriffsberechtigungen** -Eigenschaft des Benutzerkontos auf festgelegt **Verweigern des Zugriffs** oder **Zugriff zulassen**.

- Wenn andere DFÜ-Eigenschaften von Benutzerkonten nicht für den Verbindungstyp zutreffen, die in der Netzwerkrichtlinie konfiguriert ist. Z.B. andere Eigenschaften als die **Netzwerkzugriffsberechtigungen** Einstellung gelten nur für DFÜ- oder VPN-Verbindungen, aber die Netzwerkrichtlinie, die Sie erstellen, die für Switch- oder drahtlosen Verbindungen.

Dieses Verfahrens können zum Konfigurieren von NPS-Einwahl Eigenschaften des Benutzerkontos ignorieren. Wenn eine Anforderung der Verbindung die Netzwerkrichtlinie übereinstimmt, in denen dieses Kontrollkästchen aktiviert ist, wird NPS nicht die DFÜ-Eigenschaften des Benutzerkontos um zu bestimmen, ob der Benutzer oder Computer autorisiert ist, Zugriff auf das Netzwerk verwendet. nur die Einstellungen in der Netzwerkrichtlinie dienen zum Ermitteln der Autorisierung.

Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.

1. Klicken Sie auf dem NPS-Server im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Die NPS-Konsole wird geöffnet.

2. Doppelklicken Sie auf **Richtlinien**, klicken Sie auf **Netzwerkrichtlinien**, und doppelklicken Sie dann im Detailbereich auf die Richtlinie, die Sie konfigurieren möchten.

3. In der Richtlinie **Eigenschaften** Dialogfeld auf die **(Übersicht)** Registerkarte **Zugriffsberechtigung**, wählen die **ignorieren DFÜ-Eigenschaften des Benutzerkontos**, und klicken Sie dann auf **OK**.

### <a name="to-configure-nps-to-ignore-user-account-dial-in-properties"></a>So konfigurieren Sie NPS-Einwahl Eigenschaften des Benutzerkontos ignorieren



## <a name="configure-nps-for-vlans"></a>Konfigurieren des Netzwerkrichtlinienservers für VLANs

VLAN-fähig Netzwerkzugriffsserver und NPS in Windows Server2016 verwenden, können Sie Gruppen von Benutzern nur den Zugriff auf die Netzwerkressourcen bereitstellen, die für ihre Sicherheitsberechtigungen geeignet sind. Beispielsweise erhalten Besucher Sie von drahtlosen Zugriff auf das Internet ohne deren Zugriff auf das Netzwerk Ihrer Organisation. 

Darüber hinaus können VLANs Sie logisch Gruppe Netzwerk-Ressourcen, die in verschiedenen physischen Standorten oder auf andere physische Subnetze vorhanden sind. Beispielsweise Mitglieder der Vertriebsabteilung und ihre Netzwerkressourcen, z.B. von Clientcomputern, Servern und Druckern, möglicherweise in mehreren verschiedenen Gebäuden in Ihrer Organisation befinden, aber Sie können alle diese Ressourcen in einem VLAN, die im selben IP-Adressbereich verwendet platzieren. Das VLAN und die Funktionen, aus der Perspektive des Endbenutzers, als ein einzelnes Subnetz.

Sie können auch VLANs verwenden, wenn Sie ein Netzwerk zwischen den verschiedenen Gruppen von Benutzern zu verteilen möchten. Nachdem Sie ermittelt haben, wie Sie Ihre Gruppen definieren möchten, können Sie Sicherheitsgruppen in Active Directory-Benutzer und -Computer-Snap-In erstellen und Mitglieder der Gruppen hinzugefügt.

### <a name="configure-a-network-policy-for-vlans"></a>Konfigurieren Sie eine Netzwerkrichtlinie für VLANs

Sie können dieses Verfahren verwenden, so konfigurieren Sie eine Netzwerkrichtlinie, die von Benutzern mit einem VLAN zugewiesen. Bei Verwendung der VLAN-fähig Netzwerkhardware, z.B. Routern, Switches und Access-Controller, können Sie Netzwerkrichtlinien um anzuweisen, die Access-Server an bestimmten Active Directory-Gruppen angehören, auf bestimmte VLANs konfigurieren. Diese Fähigkeit auf Netzwerkressourcen logisch mit VLANs Gruppe bietet Flexibilität beim Entwerfen und Implementieren von Netzwerk-Lösungen.

Wenn Sie die Einstellungen von einem NPS-Netzwerkrichtlinien für die Verwendung mit VLANs konfigurieren, müssen Sie die Attribute konfigurieren **Mittel Tunneltyp**, **Tunnel-Pvt-Group-ID**, **Tunneltyp**, und **Tunnel-Tag**. 

Dieses Verfahren steht als Richtlinie zur Verfügung. die Netzwerkkonfiguration möglicherweise nicht den unten beschriebenen erforderlich.

Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.

### <a name="to-configure-a-network-policy-for-vlans"></a>So konfigurieren Sie eine Netzwerkrichtlinie für VLANs

1. Klicken Sie auf dem NPS-Server im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Die NPS-Konsole wird geöffnet.

2. Doppelklicken Sie auf **Richtlinien**, klicken Sie auf **Netzwerkrichtlinien**, und doppelklicken Sie dann im Detailbereich auf die Richtlinie, die Sie konfigurieren möchten.

3. In der Richtlinie **Eigenschaften** Dialogfeld, klicken Sie auf die **Einstellungen** Registerkarte.

4. In der Richtlinie **Eigenschaften**im **Einstellungen**im **RADIUS-Attribute**, stellen Sie sicher, dass **Standard** ausgewählt ist.

5. Klicken Sie im Detailbereich in **Attribute**, die **Diensttyp** Attribut mit einem Standardwert von konfiguriert **"eingerahmt"**. Standardmäßig mit Zugriff auf Methoden VPN- und DFÜ-Richtlinien für die **"eingerahmt"-Protokoll** Attribut konfiguriert ist, mit dem Wert **PPP**. Um weitere erforderliche Attribute für VLANs anzugeben, klicken Sie auf **hinzufügen**. Die **Standard RADIUS-Attribut hinzufügen** Dialogfeld wird geöffnet.

6. In **Standard RADIUS-Attribut hinzufügen**-Attribute, einen Bildlauf nach unten, um und fügen Sie die folgenden Attribute:

    - **Mittel Tunneltyp**. Wählen Sie einen Wert für die vorherige Auswahl, die Sie für die Richtlinie vorgenommen haben. Beispielsweise ist die Netzwerkrichtlinie, die Sie konfigurieren eine Richtlinie für drahtlose Netzwerke, wählen **Wert: 802 (enthält alle 802 Medien sowie kanonischen Ethernet-Format)**.

    - **Tunnel-Pvt-Group-ID**. Geben Sie die ganze Zahl, die VLAN-Nummer darstellt, die Mitglieder der Gruppe zugewiesen werden soll. 

    - **Tunneltyp**. Wählen Sie **virtuelles LAN (VLAN)**.


7. In **Standard RADIUS-Attribut hinzufügen**, klicken Sie auf **schließen**. 

8. Wenn Ihre Netzwerkzugriffsserver (NAS) mit erfordert die **Tunnel-Tag** -Attribut, verwenden Sie die folgenden Schrittezum Hinzufügen der **Tunnel-Tag** -Attribut auf die Netzwerkrichtlinie. Wenn der NAS-Dokumentation dieses Attribut nicht erwähnt ist, fügen Sie es nicht mit der Richtlinie. Falls erforderlich, fügen Sie die Attribute wie folgt:

    - In der Richtlinie **Eigenschaften**im **Einstellungen**im **RADIUS-Attribute**, klicken Sie auf **Anbieter bestimmte**. 

    - Klicken Sie im Detailbereich auf **hinzufügen**. Die **bestimmten Anbieter-Attribut hinzufügen** Dialogfeld wird geöffnet.

    - In **Attribute**, führen Sie einen Bildlauf nach unten, und wählen Sie **Tunnel-Tag**, und klicken Sie dann auf **hinzufügen**. Die **Attributinformationen** Dialogfeld wird geöffnet. 

    - In **Attributwert**, geben Sie den Wert, den Sie in der Hardwaredokumentation abgerufen haben.

## <a name="configure-the-eap-payload-size"></a>Konfigurieren Sie die Größe der EAP-Nutzlast

In einigen Fällen verwerfen Routern oder Firewalls Pakete, da sie konfiguriert sind, um Pakete zu verwerfen, die Fragmentierung erfordern.

Wenn Sie NPS mit den Netzwerkrichtlinien, die das Extensible Authentication Protocol-\(EAP\) mit Transport Layer Security \(TLS\) oder EAP-TLS als Authentifizierungsmethode verwenden bereitstellen, ist die standardmäßige maximale Übertragungseinheit \(MTU\), mit denen NPS für EAP-Nutzlasten 1500 Bytes. 

Diese maximale Größe für die EAP-Nutzlast kann RADIUS-Nachrichten erstellen, die Fragmentierung durch einen Router oder eine Firewall zwischen dem NPS-Server und RADIUS-Client erfordern. Wenn dies der Fall ist, kann ein Router oder eine Firewall zwischen den RADIUS-Client und dem NPS-Server automatisch einige Fragmente, was Fehler bei der Authentifizierung und die Unfähigkeit des Access-Clients eine Verbindung mit dem Netzwerk verwerfen.

Verwenden Sie das folgende Verfahren, um die maximale Größe zu verringern, die NPS für EAP-Nutzlasten verwendet werden, indem das Attribut "eingerahmt"-MTU in einer neuen Richtlinie auf einen Wert nicht größer als 1344 anpassen.

Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.

### <a name="to-configure-the-framed-mtu-attribute"></a>So konfigurieren Sie das Attribut "eingerahmt"-MTU

1. Klicken Sie auf dem NPS-Server im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Die NPS-Konsole wird geöffnet.
 
2. Doppelklicken Sie auf **Richtlinien**, klicken Sie auf **Netzwerkrichtlinien**, und doppelklicken Sie dann im Detailbereich auf die Richtlinie, die Sie konfigurieren möchten.

3. In der Richtlinie **Eigenschaften** Dialogfeld, klicken Sie auf die **Einstellungen** Registerkarte.

4. In **Einstellungen**im **RADIUS-Attribute**, klicken Sie auf **Standard**. Klicken Sie im Detailbereich auf **hinzufügen**. Die **Standard RADIUS-Attribut hinzufügen** Dialogfeld wird geöffnet.

5. In **Attribute**, führen Sie einen Bildlauf nach unten, und klicken Sie auf **"eingerahmt"-MTU**, und klicken Sie dann auf **hinzufügen**. Die **Attributinformationen** Dialogfeld wird geöffnet.

6. In **Attributwert**, geben Sie einen Wert kleiner oder gleich als **1344**. Klicken Sie auf **OK**, klicken Sie auf **schließen**, und klicken Sie dann auf **OK**.



Weitere Informationen zu Richtlinien finden Sie unter [Netzwerkrichtlinien](nps-np-overview.md).

Beispiele für mustervergleichssyntax an Attribute Netzwerk, finden Sie unter [reguläre Ausdrücke in NPS](nps-crp-reg-expressions.md).

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).
