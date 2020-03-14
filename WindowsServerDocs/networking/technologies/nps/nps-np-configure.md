---
title: Konfigurieren von Netzwerkrichtlinien
description: Dieses Thema bietet einen Überblick über die Netzwerk Richtlinien Konfiguration für den Netzwerk Richtlinien Server unter Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: fe77655a-e2be-4949-92e1-aaaa215d86ea
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a2bde42ba9b9489ddcd8fb3673ec5ddf1fd4d970
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79322562"
---
# <a name="configure-network-policies"></a>Konfigurieren von Netzwerkrichtlinien

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema können Sie Netzwerk Richtlinien in NPS konfigurieren.

## <a name="add-a-network-policy"></a>Netzwerk Richtlinie hinzufügen

Der Netzwerk Richtlinien Server \(NPS-\) verwendet Netzwerk Richtlinien und die Einwähleigenschaften von Benutzerkonten, um zu bestimmen, ob eine Verbindungsanforderung zum Herstellen einer Verbindung mit dem Netzwerk autorisiert ist.

Mit diesem Verfahren können Sie eine neue Netzwerk Richtlinie in der NPS-Konsole oder der Remote Zugriffs Konsole konfigurieren.

### <a name="performing-authorization"></a>Ausführen der Autorisierung

Wenn die Autorisierung einer Verbindungsanforderung von NPS durchführt wird, wird die Anforderung mit jeder Netzwerk Richtlinie in der geordneten Liste der Richtlinien verglichen, beginnend mit der ersten Richtlinie und anschließend durch die Liste der konfigurierten Richtlinien. Wenn NPS eine Richtlinie findet, deren Bedingungen der Verbindungsanforderung entsprechen, verwendet NPS die abgleichsrichtlinie und die DFÜ-Eigenschaften des Benutzerkontos, um die Autorisierung auszuführen. Wenn die DFÜ-Eigenschaften des Benutzerkontos konfiguriert sind, um Zugriff zu gewähren oder den Zugriff über die Netzwerk Richtlinie zu steuern, und die Verbindungsanforderung autorisiert ist, wendet NPS die in der Netzwerk Richtlinie konfigurierten Einstellungen auf die Verbindung an.

Wenn NPS keine Netzwerk Richtlinie findet, die mit der Verbindungsanforderung übereinstimmt, wird die Verbindungsanforderung zurückgewiesen, es sei denn, die DFÜ-Eigenschaften für das Benutzerkonto sind so festgelegt, dass der Zugriff gewährt wird.

Wenn die DFÜ-Eigenschaften des Benutzerkontos so festgelegt sind, dass der Zugriff verweigert wird, wird die Verbindungsanforderung von NPS abgelehnt.

### <a name="key-settings"></a>Schlüssel Einstellungen

Wenn Sie den Assistenten für neue Netzwerk Richtlinien verwenden, um eine Netzwerk Richtlinie zu erstellen, wird der Wert, den Sie in der **Netzwerk Verbindungsmethode** angeben, zur automatischen Konfiguration der Richtlinientyp Bedingung verwendet: 

- Wenn Sie den Standardwert nicht angegeben beibehalten, wird die von Ihnen erstellte Netzwerk Richtlinie von NPS für alle Netzwerk Verbindungstypen ausgewertet, die eine beliebige Art von Netzwerk Zugriffs Server (NAS) verwenden.
- Wenn Sie eine Netzwerk Verbindungsmethode angeben, wertet NPS die Netzwerk Richtlinie nur aus, wenn die Verbindungsanforderung vom Typ des von Ihnen angegebenen Netzwerk Zugriffs Servers stammt.

Auf der Seite **Zugriffsberechtigung** müssen Sie **Zugriff gewährt** auswählen, wenn die Richtlinie Benutzern das Herstellen einer Verbindung mit Ihrem Netzwerk gestatten soll. Wenn Sie verhindern möchten, dass Benutzer eine Verbindung mit Ihrem Netzwerk herstellen, wählen Sie **Zugriff verweigert**aus. 

Wenn Sie möchten, dass die Zugriffsberechtigung durch Benutzerkonto-Einwähleigenschaften in Active Directory&reg; Domänen Diensten \(AD DS\)festgelegt wird, können Sie das Kontrollkästchen **Zugriff wird durch Benutzer-DFÜ-Eigenschaften bestimmt** .

Zum Durchführen dieses Verfahrens ist mindestens die Mitgliedschaft in **Domänen-Admins** oder eine entsprechende Berechtigung erforderlich.

### <a name="to-add-a-network-policy"></a>So fügen Sie eine Netzwerk Richtlinie hinzu 

1. Öffnen Sie die NPS-Konsole, und doppelklicken Sie dann auf **Richtlinien**.

2. Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf **Netzwerk Richtlinien**, und klicken Sie dann auf **neu**. Der Assistent für neue Netzwerkrichtlinien wird geöffnet.

3. Verwenden Sie den Assistenten für neue Netzwerk Richtlinien, um eine Richtlinie zu erstellen.

## <a name="create-network-policies-for-dial-up-or-vpn-with-a-wizard"></a>Erstellen von Netzwerk Richtlinien für die DFÜ-oder VPN-Verbindung mit einem Assistenten

Mithilfe dieses Verfahrens können Sie die Verbindungs Anforderungs Richtlinien und Netzwerk Richtlinien erstellen, die erforderlich sind, um DFÜ-Server oder ein virtuelles privates Netzwerk \(VPN\)-Servern als Remote Authentication Dial-in User Service \(RADIUS\) Clients dem NPS-RADIUS-Server bereitzustellen.

>[!NOTE]
>Client Computer, z. b. Laptop Computer und andere Computer, auf denen Client Betriebssysteme ausgeführt werden, sind keine RADIUS-Clients. RADIUS-Clients sind Netzwerk Zugriffs Server – z. b. drahtlos Zugriffspunkte, 802.1 x-authentifizier Ende Switches, virtuelles privates Netzwerk \(VPN\) Servern und DFÜ-Server – da diese Geräte das RADIUS-Protokoll für die Kommunikation mit RADIUS-Servern wie NPSS verwenden.

In diesem Verfahren wird erläutert, wie der Assistent für neue DFÜ-oder virtuelle private Netzwerkverbindungen in NPS geöffnet wird.

Nachdem Sie den Assistenten ausgeführt haben, werden die folgenden Richtlinien erstellt:

- Eine Verbindungs Anforderungs Richtlinie
- Eine Netzwerk Richtlinie

Sie können den Assistenten für neue DFÜ-oder virtuelle private Netzwerkverbindungen jedes Mal ausführen, wenn Sie neue Richtlinien für DFÜ-Server und VPN-Server erstellen müssen.

Das Ausführen des Assistenten für neue DFÜ-oder VPN-Verbindungen ist nicht der einzige Schritt, der erforderlich ist, um DFÜ-oder VPN-Server als RADIUS-Clients für den NPS bereitzustellen. Für beide Netzwerk Zugriffsmethoden ist es erforderlich, dass Sie zusätzliche Hardware-und Softwarekomponenten bereitstellen.

Zum Durchführen dieses Verfahrens ist mindestens die Mitgliedschaft in **Domänen-Admins** oder eine entsprechende Berechtigung erforderlich.

### <a name="to-create-policies-for-dial-up-or-vpn-with-a-wizard"></a>So erstellen Sie Richtlinien für die DFÜ-oder VPN-Richtlinie mit einem Assistenten

1. Öffnen Sie die NPS-Konsole. Wenn Sie nicht bereits ausgewählt ist, klicken Sie auf **NPS \(lokalen\)** . Wenn Sie Richtlinien für eine Remote-NPS erstellen möchten, wählen Sie den Server aus.

2. Wählen Sie unter " **Start** " und " **Standard Konfiguration**" die Option **RADIUS-Server für DFÜ-oder VPN-Verbindungen**. Der Text und die Links unter dem Text ändern sich, um die Auswahl widerzuspiegeln.

3. Klicken Sie auf **VPN oder DFÜ mit einem Assistenten konfigurieren**. Der Assistent für neue DFÜ-oder virtuelle private Netzwerkverbindungen wird geöffnet.

4. Befolgen Sie die Anweisungen im Assistenten, um die Erstellung der neuen Richtlinien abzuschließen.

## <a name="create-network-policies-for-8021x-wired-or-wireless-with-a-wizard"></a>Erstellen von Netzwerk Richtlinien für 802.1 x-Kabel-oder drahtlos Netzwerke mit einem Assistenten

Mithilfe dieses Verfahrens können Sie die Verbindungs Anforderungs Richtlinie und die Netzwerk Richtlinie erstellen, die für die Bereitstellung von 802.1 x-authentifizier enden Switches oder drahtlosen 802.1 x-Zugriffs Punkten als Remote Authentication Dial-in User Service (RADIUS)-Clients an den NPS erforderlich sind. RADIUS-Server.

In diesem Verfahren wird erläutert, wie Sie den neuen IEEE 802.1 x-Assistenten für sichere Kabel-und Drahtlos Verbindungen in NPS starten.

Nachdem Sie den Assistenten ausgeführt haben, werden die folgenden Richtlinien erstellt:

- Eine Verbindungs Anforderungs Richtlinie
- Eine Netzwerk Richtlinie

Wenn Sie neue Richtlinien für den 802.1 x-Zugriff erstellen müssen, können Sie den neuen IEEE 802.1 x-Assistenten für sichere Kabel-und Drahtlos Verbindungen ausführen.

Das Ausführen des neuen IEEE 802.1 x-Assistenten für sichere Kabel-und Drahtlos Verbindungen ist nicht der einzige Schritt, der erforderlich ist, um 802.1 x-authentifizier Ende Switches und drahtlos Zugriffspunkte als RADIUS-Clients für den NPS bereitzustellen. Für beide Netzwerk Zugriffsmethoden ist es erforderlich, dass Sie zusätzliche Hardware-und Softwarekomponenten bereitstellen.

Zum Durchführen dieses Verfahrens ist mindestens die Mitgliedschaft in **Domänen-Admins** oder eine entsprechende Berechtigung erforderlich.

### <a name="to-create-policies-for-8021x-wired-or-wireless-with-a-wizard"></a>So erstellen Sie Richtlinien für 802.1 x-Kabel-oder drahtlos Verbindungen mit einem Assistenten

1. Klicken Sie auf dem NPS in Server-Manager auf **Extras, und klicken Sie dann**auf **Netzwerk Richtlinien Server**. Die NPS-Konsole wird geöffnet. 

2. Wenn Sie nicht bereits ausgewählt ist, klicken Sie auf **NPS \(lokalen\)** . Wenn Sie Richtlinien für eine Remote-NPS erstellen möchten, wählen Sie den Server aus.

3. Wählen Sie unter " **Start** " und " **Standard Konfiguration**" **RADIUS-Server für drahtlose oder verkabelte 802.1 x-Verbindungen aus**. Der Text und die Links unter dem Text ändern sich, um die Auswahl widerzuspiegeln.

4. Klicken Sie **mit einem Assistenten auf 802.1 x konfigurieren**. Der neue IEEE 802.1 x-Assistent für sichere Kabel-und Drahtlos Verbindungen wird geöffnet.

5. Befolgen Sie die Anweisungen im Assistenten, um die Erstellung der neuen Richtlinien abzuschließen.

## <a name="configure-nps-to-ignore-user-account-dial-in-properties"></a>Konfigurieren von NPS zum Ignorieren von Benutzerkonto-DFÜ-Eigenschaften

Verwenden Sie dieses Verfahren, um eine NPS-Netzwerk Richtlinie so zu konfigurieren, dass die DFÜ-Eigenschaften von Benutzerkonten in Active Directory während des Autorisierungs Vorgangs ignoriert werden. Benutzerkonten in Active Directory Benutzern und Computern verfügen über DFÜ-Eigenschaften, die NPS während der Autorisierung auswertet, es sei denn, die Eigenschaft **Netzwerk Zugriffsberechtigung** des Benutzerkontos ist so festgelegt, dass der **Zugriff über die NPS-Netzwerk Richtlinie gesteuert**wird. 

Es gibt zwei Situationen, in denen Sie NPS so konfigurieren möchten, dass die DFÜ-Eigenschaften von Benutzerkonten in Active Directory ignoriert werden:

- Wenn Sie die NPS-Autorisierung mithilfe der Netzwerk Richtlinie vereinfachen möchten, aber nicht für alle Benutzerkonten die Eigenschaft **Netzwerk Zugriffsberechtigung** festgelegt ist, um den **Zugriff über die NPS-Netzwerk Richtlinie zu steuern**. Beispielsweise kann für einige Benutzerkonten die Eigenschaft **Netzwerk Zugriffsberechtigung** für das Benutzerkonto festgelegt werden, um **Zugriff zu verweigern** oder **Zugriff zuzulassen**.

- Wenn andere Einwähleigenschaften von Benutzerkonten nicht auf den Verbindungstyp anwendbar sind, der in der Netzwerk Richtlinie konfiguriert ist. Beispielsweise gelten andere Eigenschaften als die Einstellung für die **Netzwerk Zugriffsberechtigung** nur für Einwähl-oder VPN-Verbindungen, aber die Netzwerk Richtlinie, die Sie erstellen, ist für drahtlose oder authentifizier Ende Switchverbindungen vorgesehen.

Mit diesem Verfahren können Sie NPS so konfigurieren, dass Benutzerkonto-Einwähleigenschaften ignoriert werden. Wenn eine Verbindungsanforderung mit der Netzwerk Richtlinie übereinstimmt, in der dieses Kontrollkästchen aktiviert ist, verwendet NPS nicht die DFÜ-Eigenschaften des Benutzerkontos, um zu bestimmen, ob der Benutzer bzw. der Computer für den Zugriff auf das Netzwerk autorisiert ist. nur die Einstellungen in der Netzwerk Richtlinie werden zur Bestimmung der Autorisierung verwendet.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.

1. Klicken Sie auf dem NPS in Server-Manager auf **Extras, und klicken Sie dann**auf **Netzwerk Richtlinien Server**. Die NPS-Konsole wird geöffnet.

2. Doppelklicken Sie auf **Richtlinien**, klicken Sie auf **Netzwerk Richtlinien**, und doppelklicken Sie dann im Detailbereich auf die Richtlinie, die Sie konfigurieren möchten.

3. Aktivieren Sie im Dialogfeld Richtlinien **Eigenschaften** auf der Registerkarte **Übersicht** unter **Zugriffsberechtigung**das Kontrollkästchen **Benutzerkonto-Einwähleigenschaften ignorieren** , und klicken Sie dann auf **OK**.

### <a name="to-configure-nps-to-ignore-user-account-dial-in-properties"></a>So konfigurieren Sie NPS zum Ignorieren von Benutzerkonto-Einwähleigenschaften



## <a name="configure-nps-for-vlans"></a>Konfigurieren von NPS für VLANs

Mithilfe von VLAN-fähigen Netzwerk Zugriffs Servern und NPS in Windows Server 2016 können Sie Gruppen von Benutzern mit Zugriff auf die Netzwerkressourcen bereitstellen, die für Ihre Sicherheits Berechtigungen geeignet sind. Beispielsweise können Sie den Besuchern drahtlosen Zugriff auf das Internet ermöglichen, ohne dass Sie auf Ihr Organisations Netzwerk zugreifen können. 

Darüber hinaus ermöglichen VLANs das logische Gruppieren von Netzwerkressourcen, die sich an unterschiedlichen physischen Standorten oder in verschiedenen physischen Subnetzen befinden. Beispielsweise können sich die Mitglieder Ihrer Vertriebsabteilung und ihre Netzwerkressourcen, z. b. Client Computer, Server und Drucker, in verschiedenen Gebäuden in Ihrer Organisation befinden, aber Sie können all diese Ressourcen in einem VLAN platzieren, das dieselbe IP-Adresse verwendet. Adressbereich. Das VLAN fungiert dann aus der Sicht des Endbenutzers als einzelnes Subnetz.

Sie können auch VLANs verwenden, wenn Sie ein Netzwerk zwischen verschiedenen Benutzergruppen trennen möchten. Nachdem Sie festgelegt haben, wie Sie Ihre Gruppen definieren möchten, können Sie im Snap-in Active Directory Benutzer und Computer Sicherheitsgruppen erstellen und dann den Gruppenmitglieder hinzufügen.

### <a name="configure-a-network-policy-for-vlans"></a>Konfigurieren einer Netzwerk Richtlinie für VLANs

Mithilfe dieses Verfahrens können Sie eine Netzwerk Richtlinie konfigurieren, die Benutzer einem VLAN zuweist. Bei der Verwendung von VLAN-fähigen Netzwerkhardware (z. b. Routern, Switches und Zugriffs Controllern) können Sie die Netzwerk Richtlinie so konfigurieren, dass die Zugriffs Server Mitglieder bestimmter Active Directory Gruppen auf bestimmten VLANs platzieren. Diese Möglichkeit, Netzwerkressourcen logisch mit VLANs zu gruppieren, bietet Flexibilität beim Entwerfen und Implementieren von Netzwerklösungen.

Wenn Sie die Einstellungen einer NPS-Netzwerk Richtlinie für die Verwendung mit VLANs konfigurieren, müssen Sie die Attribute **Tunnel-mittlere-Typ**, **Tunnel-Pvt-Gruppen-ID**, **Tunneltyp**und **tunneltag**konfigurieren. 

Dieses Verfahren wird als Richtlinie bereitgestellt. die Netzwerkkonfiguration erfordert möglicherweise andere Einstellungen als die unten beschriebenen Einstellungen.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.

### <a name="to-configure-a-network-policy-for-vlans"></a>So konfigurieren Sie eine Netzwerk Richtlinie für VLANs

1. Klicken Sie auf dem NPS in Server-Manager auf **Extras, und klicken Sie dann**auf **Netzwerk Richtlinien Server**. Die NPS-Konsole wird geöffnet.

2. Doppelklicken Sie auf **Richtlinien**, klicken Sie auf **Netzwerk Richtlinien**, und doppelklicken Sie dann im Detailbereich auf die Richtlinie, die Sie konfigurieren möchten.

3. Klicken Sie im Dialogfeld Richtlinien **Eigenschaften** auf die Registerkarte **Einstellungen** .

4. Stellen Sie in den Richtlinien **Eigenschaften**unter **Einstellungen**in **RADIUS-Attribute**sicher, dass **Standard** ausgewählt ist.

5. Im Detailbereich wird in **Attribute**das **Service Type-** Attribut mit dem Standardwert " **gerahmt**" konfiguriert. Standardmäßig wird für Richtlinien mit Zugriffsmethoden für VPN und DFÜ das Attribut " **Attributes Protokoll** " mit dem Wert **PPP**konfiguriert. Zum Angeben zusätzlicher Verbindungs Attribute, die für VLANs erforderlich sind, klicken Sie auf **Hinzufügen**. Das Dialogfeld **Standard-RADIUS-Attribut hinzufügen** wird geöffnet.

6. Scrollen Sie unter **Standard-RADIUS-Attribut hinzufügen**in Attribute zu, und fügen Sie die folgenden Attribute hinzu:

    - **Tunnel-Mittel--Typ**. Wählen Sie einen Wert aus, der der vorherigen Auswahl entspricht, die Sie für die Richtlinie vorgenommen haben. Wenn z. b. die Netzwerk Richtlinie, die Sie konfigurieren, eine drahtlos Richtlinie ist, wählen Sie **Wert: 802 (enthält alle 802-Medien und kanonische Ethernet-Format)** .

    - **Tunnel-Pvt-Group-ID**. Geben Sie die ganze Zahl ein, die die VLAN-Nummer darstellt, der Gruppenmitglieder zugewiesen werden. 

    - **Tunneltyp**. Wählen Sie **virtuelle LANs (VLAN)** aus.


7. Klicken Sie in **Standard-RADIUS-Attribut hinzufügen**auf **Schließen**. 

8. Wenn Ihr Netzwerk Zugriffs Server (NAS) die Verwendung des **Tunnel-Tag-** Attributs erfordert, führen Sie die folgenden Schritte aus, um das **Tunnel-Tag-** Attribut der Netzwerk Richtlinie hinzuzufügen. Wenn dieses Attribut in der NAS-Dokumentation nicht erwähnt wird, fügen Sie es nicht der Richtlinie hinzu. Fügen Sie die Attribute bei Bedarf wie folgt hinzu:

    - Klicken Sie in den Richtlinien **Eigenschaften**unter **Einstellungen**in **RADIUS-Attribute**auf **Hersteller spezifisch**. 

    - Klicken Sie im Detailbereich auf **Hinzufügen**. Das Dialogfeld **Anbieter spezifisches Attribut hinzufügen** wird geöffnet.

    - Führen Sie unter **Attribute**einen Bildlauf nach unten durch, und wählen Sie **tunneltag**aus. Klicken Sie dann auf **Hinzufügen** Das Dialogfeld **Attributinformationen** wird geöffnet. 

    - Geben Sie in **Attribut Wert**den Wert ein, den Sie aus der Hardware Dokumentation abgerufen haben.

## <a name="configure-the-eap-payload-size"></a>Konfigurieren der EAP-Nutzlastgröße

In einigen Fällen werden von Routern oder Firewalls Pakete gelöscht, da Sie so konfiguriert sind, dass Sie Pakete verwerfen, die Fragmentierungen erfordern.

Wenn Sie NPS mit Netzwerk Richtlinien bereitstellen, die das Extensible Authentication-Protokoll \(EAP-\) mit Transport Layer Security \(TLS\)oder EAP-TLS als Authentifizierungsmethode verwenden, ist die standardmäßige maximale Übertragungseinheit \(MTU\), die NPS für EAP-Nutzlasten verwendet, 1500 Bytes. 

Diese maximale Größe für die EAP-Nutzlast kann RADIUS-Nachrichten erstellen, die eine Fragmentierung von einem Router oder einer Firewall zwischen dem NPS und einem RADIUS-Client erfordern. Wenn dies der Fall ist, werden von einem Router oder einer Firewall, der zwischen dem RADIUS-Client und dem NPS positioniert ist, möglicherweise einige Fragmente verworfen, was zu einem Authentifizierungsfehler und zum Ausfall der Verbindungs Herstellung mit dem Netzwerk führen kann.

Gehen Sie folgendermaßen vor, um die maximale Größe zu verringern, die NPS für EAP-Nutzlasten verwendet, indem Sie das Attribut "gerahmt-MTU" in einer Netzwerk Richtlinie auf einen Wert "nicht größer als 1344" einstellen.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.

### <a name="to-configure-the-framed-mtu-attribute"></a>So konfigurieren Sie das Attribut "gerahmte MTU"

1. Klicken Sie auf dem NPS in Server-Manager auf **Extras, und klicken Sie dann**auf **Netzwerk Richtlinien Server**. Die NPS-Konsole wird geöffnet.
 
2. Doppelklicken Sie auf **Richtlinien**, klicken Sie auf **Netzwerk Richtlinien**, und doppelklicken Sie dann im Detailbereich auf die Richtlinie, die Sie konfigurieren möchten.

3. Klicken Sie im Dialogfeld Richtlinien **Eigenschaften** auf die Registerkarte **Einstellungen** .

4. Klicken Sie unter **Einstellungen**in **RADIUS-Attribute**auf **Standard**. Klicken Sie im Detailbereich auf **Hinzufügen**. Das Dialogfeld **Standard-RADIUS-Attribut hinzufügen** wird geöffnet.

5. Führen Sie unter **Attribute**einen Bildlauf nach unten durch, und klicken Sie auf **gerahmt-MTU**und dann auf **Hinzufügen**. Das Dialogfeld **Attributinformationen** wird geöffnet.

6. Geben Sie in **Attribut Wert**einen Wert ein, der kleiner oder gleich **1344**ist. Klicken Sie auf **OK**, auf **Schließen**und dann auf **OK**.



Weitere Informationen zu Netzwerk Richtlinien finden Sie unter [Netzwerk Richtlinien](nps-np-overview.md).

Beispiele für Muster Vergleichs Syntax zum Angeben von Netzwerk Richtlinien Attributen finden Sie unter [Verwenden regulärer Ausdrücke in NPS](nps-crp-reg-expressions.md).

Weitere Informationen zu NPS finden Sie unter [Netzwerk Richtlinien Server (Network Policy Server, NPS)](nps-top.md).
