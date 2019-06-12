---
title: Konfigurieren von Windows 10-Client immer auf VPN-Verbindungen
description: In diesem Schritt haben Sie erfahren Sie mehr über die Optionen für "profileXML" und das Schema und die Windows 10-Clientcomputern für die Kommunikation mit dieser Infrastruktur mit einer VPN-Verbindung konfigurieren.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.date: 05/29/2018
ms.assetid: d165822d-b65c-40a2-b440-af495ad22f42
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.reviewer: deverette
ms.openlocfilehash: fdf640d7e98781ca054ab982027bdfe8c3fb64d6
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749627"
---
# <a name="step-6-configure-windows-10-client-always-on-vpn-connections"></a>Schritt 6 Konfigurieren von Windows 10-Always On-VPN-Clientverbindungen

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorherige:** Schritt 5 Konfigurieren von DNS und Firewalleinstellungen](vpn-deploy-dns-firewall.md)<br>
- [**nächster:** Schritt 7 (Optional) Bedingter Zugriff für VPN-Verbindungen mithilfe von Azure AD](../../ad-ca-vpn-connectivity-windows10.md)

In diesem Schritt haben Sie erfahren Sie mehr über die Optionen für "profileXML" und das Schema, und Konfigurieren der Windows 10-Clientcomputer für die Kommunikation mit dieser Infrastruktur mit einer VPN-Verbindung.

Sie können Always On-VPN-Client über PowerShell, SCCM oder Intune konfigurieren. Alle drei erfordern ein XML VPN-Profil so konfigurieren Sie die entsprechenden VPN-Einstellungen. Automatisieren von PowerShell ist die Registrierung für Organisationen ohne SCCM oder Intune möglich.

>[!NOTE]
>Die Gruppenrichtlinie umfasst keine administrative Vorlagen zum Konfigurieren des Windows 10 Remote Access Always On-VPN-Clients.  Allerdings können Sie Anmeldeskripts verwenden.

## <a name="profilexml-overview"></a>Übersicht über die "profileXML"

"ProfileXML" ist ein URI-Knoten innerhalb der VPNv2 CSP. Anstatt jeden VPNv2 CSP-Knoten einzeln zu konfigurieren, wie z. B. Trigger, weiterleiten, Listen und Authentifizierungsprotokolle – verwenden Sie diesen Knoten so konfigurieren Sie Windows 10-VPN-Client durch die Bereitstellung alle Einstellungen als ein einziger XML-Block auf einen einzelnen CSP-Knoten. Das Schema "profileXML" entspricht das Schema der VPNv2 CSP-Knoten, fast identisch, aber einige Begriffe unterscheiden sich geringfügig.

In allen die Übermittlungsmethoden, die diese Bereitstellung wird beschrieben, wie z.B. Windows PowerShell System Center Configuration Manager und Intune, die verwenden Sie "profileXML". Es gibt zwei Möglichkeiten, den Knoten "profileXML" VPNv2 CSP in dieser Bereitstellung zu konfigurieren:

- **OMA-DM**. Eine Möglichkeit ist die Verwendung einen MDM-Anbieter mithilfe von OMA-DM, wie im Abschnitt bereits erwähnt [VPNv2 CSP Knoten](../always-on-vpn-technology-overview.md#vpnv2-csp-nodes). Mit dieser Methode können Sie einfach das VPN-Profil Konfigurations-XML-Markup in der ProfileXML CSP-Knoten einfügen bei Verwendung von Intune.

- **Windows-Verwaltungsinstrumentation (WMI) - zu - CSP-Bridge**. Die zweite Methode der Konfiguration des ProfileXML CSP-Knotens wird die WMI-zu-CSP-Bridge verwenden – eine WMI-Klasse mit dem Namen **MDM_VPNv2_01**–, die auf den VPNv2 CSP und den Knoten "profileXML" zugreifen können. Wenn Sie eine neue Instanz der WMI-Klasse erstellen, mithilfe von WMI den CSP das VPN-Profil zu erstellen, wenn Windows PowerShell und der System Center Configuration Manager verwenden.

Obwohl diese Konfigurationsmethoden unterscheiden zu können, benötigen eine ordnungsgemäß formatierte XML VPN-Profil. Um die Einstellung "profileXML" VPNv2 CSP zu verwenden, erstellen Sie die XML mit dem Schema "profileXML" So konfigurieren Sie die Tags für das einfache Szenario erforderlich sind. Weitere Informationen finden Sie unter [ProfileXML XSD](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-profile-xsd).

Im folgenden finden Sie alle erforderlichen Einstellungen und die entsprechende "profileXML"-Tag. Konfigurieren Sie jede Einstellung in einem bestimmten Tag innerhalb des Schemas "profileXML", und nicht alle unter dem systemeigenen Profil gefunden werden. Zusätzliches Tag Platzierung finden Sie in das Schema "profileXML".

[!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]

**Verbindungstyp:** Native IKEv2

"ProfileXML"-Element:

```xml
<NativeProtocolType>IKEv2</NativeProtocolType>
```

**Routing:** Split-tunneling

"ProfileXML"-Element:

```xml
<RoutingPolicyType>SplitTunnel</RoutingPolicyType>
```

**Namensauflösung:** Liste der Domänennameninformationen und DNS-suffix

"ProfileXML"-Elemente:

```xml
<DomainNameInformation>
<DomainName>.corp.contoso.com</DomainName>
<DnsServers>10.10.1.10,10.10.1.50</DnsServers>
</DomainNameInformation>

<DnsSuffix>corp.contoso.com</DnsSuffix>
```

**Auslösen:** Erkennung von Always On und vertrauenswürdiges Netzwerk

"ProfileXML"-Elemente:

```xml
<AlwaysOn>true</AlwaysOn>
<TrustedNetworkDetection>corp.contoso.com</TrustedNetworkDetection>
```

**Authentifizierung:** PEAP-TLS mit TPM-geschützten Benutzerzertifikate

"ProfileXML"-Elemente:

```xml
<Authentication>
<UserMethod>Eap</UserMethod>
<Eap>
<Configuration>...</Configuration>
</Eap>
</Authentication>
```

Sie können einfache Tags verwenden, einige VPN-Authentifizierungsmechanismen zu konfigurieren. EAP und PEAP sind jedoch komplizierter. Die einfachste Möglichkeit zum Erstellen von XML-Markup wird einen VPN-Client mit der EAP-Einstellungen konfigurieren, und klicken Sie dann die gewünschte Konfiguration in XML exportieren.

Weitere Informationen zu EAP-Einstellungen finden Sie unter [EAP-Konfiguration](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/eap-configuration).

## <a name="manually-create-a-template-connection-profile"></a>Manuelles Erstellen eines Verbindungsprofils Vorlage

In diesem Schritt verwenden Sie Protected Extensible Authentication Protokoll (PEAP) zum Sichern der Kommunikation zwischen dem Client und dem Server. Im Gegensatz zu einer einfachen Benutzernamen und das Kennwort benötigt diese Verbindung einen eindeutigen EAPConfiguration-Abschnitt in das VPN-Profil funktioniert.

Statt einer Beschreibung, wie Sie das XML-Markup von Grund auf neu zu erstellen, verwenden Sie Einstellungen in Windows zum Erstellen einer Vorlage VPN-Profil ein. Nach dem Erstellen der Vorlage für VPN-Profil verwenden Sie Windows PowerShell den EAPConfiguration Teil aus dieser Vorlage zum Erstellen der endgültigen "profileXML", die Sie bereitstellen, weiter unten in der Bereitstellung nutzen.

### <a name="record-nps-certificate-settings"></a>Notieren Sie die NPS-zertifikateinstellungen

Notieren Sie sich vor dem Erstellen der Vorlage für den Hostnamen oder den vollqualifizierten Domänennamen (FQDN) des NPS-Servers aus dem Zertifikat des Servers und den Namen der Zertifizierungsstelle, die das Zertifikat ausgestellt hat.

**Vorgehensweise:**

1. Öffnen Sie Network Policy Server, auf Ihrem NPS-Server.

2. Klicken Sie in der NPS-Konsole unter Richtlinien auf **Netzwerkrichtlinien**.

3. Mit der rechten Maustaste **virtuelles privates Netzwerk (VPN) Verbindungen**, und klicken Sie auf **Eigenschaften**.

4. Klicken Sie auf die **Einschränkungen** Registerkarte, und klicken Sie auf **Authentifizierungsmethoden**.

5. Klicken Sie in der EAP-Typen, auf **Microsoft: Geschütztes EAP (PEAP)** , und klicken Sie auf **bearbeiten**.

6. Notieren Sie die Werte für **Zertifikat ausgestellt für** und **Aussteller**.

    Sie können diese Werte in der bevorstehenden Konfiguration der VPN-Vorlage verwenden. Z. B. Wenn Sie den FQDN des Servers ist nps01.corp.contoso.com und der Hostnamen NPS01, den Namen des Zertifikats basiert auf den FQDN oder die DNS-Namen des Servers, z. B. nps01.corp.contoso.com.

7. Brechen Sie das Dialogfeld Eigenschaften für geschütztes EAP bearbeiten.

8. Brechen Sie das Dialogfeld Verbindungseigenschaften virtuelles privates Netzwerk (VPN).

9. Schließen Sie Netzwerkrichtlinienserver.

>[!NOTE]
>Wenn Sie mehrere NPS-Server verfügen, gehen Sie auf die einzelnen, damit das VPN-Profil jeweils überprüfen können sie verwendet werden sollen.

### <a name="configure-the-template-vpn-profile-on-a-domain-joined-client-computer"></a>Konfigurieren Sie die Vorlage VPN-Profil auf einem Computer mit domänenverknüpfung

Nun, da Sie die erforderlichen Informationen, konfigurieren die Vorlage für VPN-Profil auf einem Computer mit domänenverknüpfung haben. Der Typ des Benutzers Konto, das Sie verwenden (d. h. Standardbenutzer oder Administrator) für diesen Teil des Prozesses ist keine Rolle spielt.

Wenn Sie den Computer neu gestartet noch nicht seit der Konfiguration der automatischen Registrierung von Zertifikaten, gehen Sie hierbei jedoch vor dem Konfigurieren der Vorlage VPN-Verbindung, um sicherzustellen, dass Sie ein verwendbares Zertifikat für sie registriert haben.

>[!NOTE]
>Es gibt keine Möglichkeit, alle erweiterten Eigenschaften des VPN-, z. B. NRPT-Regeln, Always On, manuell hinzufügen vertrauenswürdiger, Netzwerk usw. Im nächsten Schritt erstellen Sie eine VPN-Testverbindung, um die Konfiguration des VPN-Servers zu überprüfen und, dass Sie eine VPN-Verbindung mit dem Server herstellen können.

**Manuelles Erstellen eines einzelnen Tests VPN-Verbindung**

1.  Melden Sie sich bei einer Domäne eingebundenen Client-Computer als Mitglied der **VPN-Benutzer** Gruppe.

2.  Geben Sie im Menü Start **VPN**, und drücken Sie EINGABETASTE.

3.  Klicken Sie im Detailbereich auf **fügen Sie eine VPN-Verbindung**.

4.  Klicken Sie in der Liste VPN-Anbieter auf **Windows (integriert)** .

5.  Geben Sie in der Verbindung **Vorlage**.

6.  Geben Sie im Server-Namen oder die Adresse, die **externe** FQDN Ihres VPN-Servers (z. B. **vpn.contoso.com**).

7.  Klicken Sie auf **Speichern**.

8.  Klicken Sie unter "Verwandte Einstellungen" auf **ändern Sie Adapteroptionen für die**.

9.  Mit der rechten Maustaste **Vorlage**, und klicken Sie auf **Eigenschaften**.

10. Auf der **Sicherheit** Registerkarte **VPN-Typ**, klicken Sie auf **IKEv2**.

11. Bei der datenverschlüsselung, klicken Sie auf **maximale Verschlüsselung**.

12. Klicken Sie auf **verwenden Extensible Authentication Protocol (EAP)** ; klicken Sie auf **verwenden Extensible Authentication Protocol (EAP)** , klicken Sie auf **Microsoft: Geschütztes EAP (PEAP) (Verschlüsselung aktiviert)** .

13. Klicken Sie auf **Eigenschaften** zum Öffnen des Dialogfelds Eigenschaften für geschütztes EAP, und schließen die folgenden Schritte aus:

    a. In der **Herstellen einer Verbindung mit diesen Servern** geben den Namen des NPS-Servers, die Sie die Authentifizierungseinstellungen des NPS-Server weiter oben in diesem Abschnitt (z. B. NPS01) entnommen.

    >[!NOTE]
    >Der eingegebene Servername muss der Name im Zertifikat übereinstimmen. Sie wiederhergestellt diesen Namen oben in diesem Abschnitt haben. Wenn der Name nicht übereinstimmt, schlägt die Verbindung mit dem Hinweis, dass "die Verbindung aufgrund einer auf dem RAS-/VPN-Server konfigurierte Richtlinie verhindert wurde." fehl,

    b.  Wählen Sie die Stamm-ZS, die dem NPS-Server-Zertifikat (z. B. Contoso-CA) ausgestellt, unter Vertrauenswürdige Stammzertifizierungsstellen.

    c.  Klicken Sie in den Benachrichtigungen vor der verbindungsherstellung, **nicht Fragen Benutzer zum Autorisieren neuer Server oder vertrauenswürdiger Zertifizierungsstellen**.

    d.  Authentifizierungsmethode auswählen, klicken Sie auf **Smartcard- oder anderes Zertifikat**, und klicken Sie auf **konfigurieren**. Die Smartcard oder andere Zertifikateigenschaften-Dialogfeld wird geöffnet.

    e.  Klicken Sie auf **verwenden Sie ein Zertifikat auf diesem Computer**.

    f.  Geben Sie auf das Feld für diese Server verbinden den Namen des NPS-Servers, die Sie über die Authentifizierungseinstellungen des NPS-Server in den vorherigen Schritten abgerufen.

    g.  Wählen Sie die Stamm-ZS, die dem NPS-Server-Zertifikat ausgestellt hat, unter Vertrauenswürdige Stammzertifizierungsstellen.

    h.  Wählen Sie die **keine benutzeraufforderung zur Autorisierung neuer Server oder vertrauenswürdiger Zertifizierungsstellen** Kontrollkästchen.

    i.  Klicken Sie auf **OK** Smartcard- oder andere Zertifikateigenschaften-Dialogfeld zu schließen.

    j.  Klicken Sie auf **OK** um das Dialogfeld "Eigenschaften für geschütztes EAP" zu schließen.

14. Klicken Sie auf **OK** um das Dialogfeld "Eigenschaften" zu schließen.

15. Schließen Sie das Fenster Netzwerkverbindungen.

16. Testen Sie das VPN in den Einstellungen, indem Sie auf **Vorlage**, und klicken Sie auf **Connect**.

>[!IMPORTANT]
>Stellen Sie sicher, dass die Vorlage VPN-Verbindung mit Ihrem VPN-Server erfolgreich war. Dadurch wird sichergestellt, dass die EAP-Einstellungen richtig sind, bevor Sie sie im nächsten Beispiel verwenden. Sie müssen eine Verbindung herstellen, mindestens einmal, bevor Sie fortfahren, Andernfalls wird das Profil nicht alle für die Verbindung mit dem VPN erforderlichen Informationen enthalten.

## <a name="create-the-profilexml-configuration-files"></a>Erstellen Sie die Konfigurationsdateien "profileXML"

Bevor Sie in diesem Abschnitt ausführen, stellen Sie sicher, dass Sie erstellt und die Vorlage VPN-Verbindung getestet haben, die im Abschnitt [manuell erstellen ein Verbindungsprofils Vorlage](#manually-create-a-template-connection-profile) beschreibt. Testen die VPN-Verbindung ist erforderlich, um sicherzustellen, dass das Profil alle für die Verbindung mit dem VPN erforderlichen Informationen enthält.

Das Windows PowerShell-Skript in Codebeispiel 1 erstellt zwei Dateien auf dem Desktop, die beide enthalten **EAPConfiguration** Transponderereignisse basierend auf den Verbindungs-Profilvorlage, die Sie zuvor erstellt haben:

- **VPN_Profile.Xml.** Diese Datei enthält das XML-Markup erforderlich, um den Knoten "profileXML" im VPNv2 CSP konfigurieren. Verwenden Sie diese Datei mit den OMA-DM-kompatible MDM-Diensten wie z.B. Intune ein.

- **VPN_Profile.ps1.** Diese Datei ist ein Windows PowerShell-Skript, das Sie ausführen können, auf den Clientcomputern so konfigurieren Sie den Knoten "profileXML" im VPNv2 CSP. Sie können auch den CSP konfigurieren, durch Bereitstellen dieser über System Center Configuration Manager-Skripts. Sie können nicht mit diesem Skript in einer Remotedesktopsitzung, einschließlich einer Hyper-V erweiterte Sitzungs ausführen.

>[!IMPORTANT]
>Die folgenden Beispielbefehle erfordern Windows 10-Build 1607 oder höher.

**Erstellen Sie VPN_Profile.xml und VPN_Proflie.ps1**

1. Melden Sie sich auf die Domäne eingebundene Clientcomputer mit der Vorlage VPN-Profil mit demselben Benutzer berücksichtigen, die im Abschnitt [manuell erstellen ein Verbindungsprofils Vorlage](#manually-create-a-template-connection-profile) beschrieben.

2. Fügen Sie Liste 1 in Windows PowerShell integrated scripting Environment (ISE), und passen Sie die Parameter, die in den Kommentaren beschrieben. Dies sind $Template "," $ProfileName "," $Servers "," $DnsSuffix "," $DomainName "," $TrustedNetwork, und "$DNSServers. Eine vollständige Beschreibung der einzelnen Einstellungen werden in den Kommentaren ist.

3. Führen Sie das Skript zum generieren **VPN_Profile.xml** und **VPN_Profile.ps1** auf dem Desktop.

#### <a name="listing-1-understanding-makeprofileps1"></a>Codebeispiel 1. Grundlegendes zu MakeProfile.ps1

In diesem Abschnitt wird erläutert, den Beispielcode, den Sie verwenden können, um einen Überblick über die Vorgehensweise: Erstellen Sie ein VPN-Profil, speziell für das Konfigurieren von "profileXML" in der VPNv2 CSP zu erhalten.

Nachdem Sie ein Skript, aus dieser Beispielcode zusammenstellen, und führen Sie das Skript, das Skript zwei Dateien generiert: VPN_Profile.XML und VPN_Profile.ps1. Verwenden Sie VPN_Profile.xml "profileXML" in der OMA-DM-kompatible MDM-Diensten wie z.B. Microsoft Intune konfigurieren.

Verwenden der **VPN_Profile.ps1** Skripts in Windows PowerShell oder System Center Configuration Manager so konfigurieren Sie "profileXML" auf dem Windows 10-Desktop.

>[!NOTE]
>Wenn das vollständige Beispielskript anzeigen möchten, finden Sie im Abschnitt [MakeProfile.ps1 vollständige Skript](#makeprofileps1-full-script).

#### <a name="parameters"></a>Parameter

Konfigurieren Sie die folgenden Parameter:

**$Template**. Der Name der Vorlage aus dem die EAP-Konfiguration abgerufen werden soll.

**$ProfileName**. Eindeutiger alphanumerischer Bezeichner für das Profil. Der Profilname darf keine mit einen Schrägstrich (/) enthalten. Weist der Namen des Profils ein Leerzeichen oder andere nicht alphanumerische Zeichen, müssen sie ordnungsgemäß entsprechend den URL-Codierung mit Escapezeichen versehen werden.

**$Servers**. Öffentliche oder routingfähige IP-Adresse oder DNS-Namen für das VPN-Gateway. Sie können auf die externe IP-Adresse, der ein Gateway oder eine virtuelle IP-Adresse für eine Serverfarm verweisen. Beispiele, 208.147.66.130 oder vpn.contoso.com.

**$DnsSuffix**. Gibt an, dass eine oder mehrere Kommas DNS-Suffixe getrennt. Die erste in der Liste wird auch als primäres verbindungsspezifischen DNS-Suffix für die VPN-Schnittstelle verwendet. Die gesamte Liste wird auch in der SuffixSearchList hinzugefügt werden.

**$DomainName**. Verwendet, um den Namespace anzugeben, den die Richtlinie angewendet wird. Bei eine benannten Abfrage ausgegeben wird, vergleicht der DNS-Client den Namen in der Abfrage alle Namespaces unter DomainNameInformationList eine Übereinstimmung gefunden. Dieser Parameter kann einen der folgenden Typen sein:

- FQDN – voll qualifizierter Domänenname
- Suffix - ein Domänensuffix, die auf die Abfrage "Shortname" für DNS-Auflösung angefügt wird. Wenn ein Suffix angeben möchten, stellen Sie einen Punkt (.), die dem DNS-Suffix voran.

**$DNSServers**. Liste von durch Trennzeichen getrennte DNS-Server IP-Adressen für den Namespace verwenden.

**$TrustedNetwork**. Durch Trennzeichen getrennte Zeichenfolge, die im vertrauenswürdige Netzwerk zu identifizieren. VPN wird nicht automatisch verbinden, wenn der Benutzer auf ihrem drahtlosen Unternehmensnetzwerk ist, in dem geschützte Ressourcen direkt an das Gerät zugegriffen werden kann.

Folgendes ist die Beispielwerte für Parameter, die in die folgenden Befehle verwendet. Stellen Sie sicher, dass Sie diese Werte für Ihre Umgebung ändern.

```xml
$TemplateName = 'Template'
$ProfileName = 'Contoso AlwaysOn VPN'
$Servers = 'vpn.contoso.com'
$DnsSuffix = 'corp.contoso.com'
$DomainName = '.corp.contoso.com'
$DNSServers = '10.10.0.2,10.10.0.3'
$TrustedNetwork = 'corp.contoso.com'
```

### <a name="prepare-and-create-the-profile-xml"></a>Vorbereiten Sie und erstellen Sie das Profil-XML

Die folgenden Beispielbefehle rufen Sie EAP-Einstellungen aus der Profilvorlage:

```xml
$Connection = Get-VpnConnection -Name $TemplateName
if(!$Connection)
{
$Message = "Unable to get $TemplateName connection profile: $_"
Write-Host "$Message"
exit
}
$EAPSettings= $Connection.EapConfigXmlStream.InnerXml
```

### <a name="create-the-profile-xml"></a>Erstellen Sie das Profil-XML

[!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]

```xml
$ProfileXML =
'<VPNProfile>
  <DnsSuffix>' + $DnsSuffix + '</DnsSuffix>
  <NativeProfile>
<Servers>' + $Servers + '</Servers>
<NativeProtocolType>IKEv2</NativeProtocolType>
<Authentication>
  <UserMethod>Eap</UserMethod>
  <Eap>
    <Configuration>
  '+ $EAPSettings + '
    </Configuration>
  </Eap>
</Authentication>
<RoutingPolicyType>SplitTunnel</RoutingPolicyType>
  </NativeProfile>
  <AlwaysOn>true</AlwaysOn>
  <RememberCredentials>true</RememberCredentials>
  <TrustedNetworkDetection>' + $TrustedNetwork + '</TrustedNetworkDetection>
  <DomainNameInformation>
<DomainName>' + $DomainName + '</DomainName>
<DnsServers>' + $DNSServers + '</DnsServers>
</DomainNameInformation>
</VPNProfile>'
```

### <a name="output-vpnprofilexml-for-intune"></a>Ausgabe VPN_Profile.xml für Intune

Sie können Befehl im folgenden Beispiel verwenden, um die Profil-XML-Datei zu speichern:

```xml
$ProfileXML | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.xml')
```

### <a name="output-vpnprofileps1-for-the-desktop-and-system-center-configuration-manager"></a>Ausgabe VPN_Profile.ps1 für Desktop und System Center Configuration Manager

Im folgenden Beispielcode wird eine AlwaysOn-IKEv2-VPN-Verbindung mithilfe des Knotens "profileXML" im VPNv2 CSP konfiguriert.

Sie können dieses Skript auf dem Windows 10 Desktop oder in System Center Configuration Manager verwenden.

### <a name="define-key-vpn-profile-parameters"></a>Definieren von Schlüsselparametern für VPN-Profil

```xml
$Script = '$ProfileName = ''' + $ProfileName + '''
$ProfileNameEscaped = $ProfileName -replace ' ', '%20'
```

## <a name="define-vpn-profilexml"></a>Definieren Sie die VPN-"profileXML"

```xml
$ProfileXML = ''' + $ProfileXML + '''
```

### <a name="escape-special-characters-in-the-profile"></a>Escapesonderzeichen Sie in das Profil

```xml
$ProfileXML = $ProfileXML -replace '<', '&lt;'
$ProfileXML = $ProfileXML -replace '>', '&gt;'
$ProfileXML = $ProfileXML -replace '"', '&quot;'
```

### <a name="define-wmi-to-csp-bridge-properties"></a>Definieren Sie Eigenschaften für WMI-zu-CSP-Bridge

```xml
$nodeCSPURI = "./Vendor/MSFT/VPNv2"
$namespaceName = "root\cimv2\mdm\dmmap"
$className = "MDM_VPNv2_01"
```

### <a name="determine-user-sid-for-vpn-profile"></a>Bestimmen Sie die Benutzer-SID für VPN-Profil:

```xml
try
{
$username = Gwmi -Class Win32_ComputerSystem | select username
$objuser = New-Object System.Security.Principal.NTAccount($username.username)
$sid = $objuser.Translate([System.Security.Principal.SecurityIdentifier])
$SidValue = $sid.Value
$Message = "User SID is $SidValue."
Write-Host "$Message"
}
catch [Exception]
{
$Message = "Unable to get user SID. User may be logged on over Remote Desktop: $_"
Write-Host "$Message"
exit
}
```

### <a name="define-wmi-session"></a>Definieren Sie die WMI-Sitzung:

```xml
$session = New-CimSession
$options = New-Object Microsoft.Management.Infrastructure.Options.CimOperationOptions
$options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Type", "PolicyPlatform_UserContext", $false)
$options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Id", "$SidValue", $false)
```

### <a name="detect-and-delete-previous-vpn-profile"></a>Erkennen Sie, und löschen Sie die vorherige VPN-Profil:

```xml
try
{
  $deleteInstances = $session.EnumerateInstances($namespaceName, $className, $options)
  foreach ($deleteInstance in $deleteInstances)
  {
    $InstanceId = $deleteInstance.InstanceID
    if ("$InstanceId" -eq "$ProfileNameEscaped")
    {
        $session.DeleteInstance($namespaceName, $deleteInstance, $options)
        $Message = "Removed $ProfileName profile $InstanceId"
        Write-Host "$Message"
    } else {
        $Message = "Ignoring existing VPN profile $InstanceId"
        Write-Host "$Message"
    }
  }
}
catch [Exception]
{
  $Message = "Unable to remove existing outdated instance(s) of $ProfileName profile: $_"
  Write-Host "$Message"
  exit
}
```

### <a name="create-the-vpn-profile"></a>Erstellen Sie das VPN-Profil:

```xml
try
{
  $newInstance = New-Object Microsoft.Management.Infrastructure.CimInstance $className, $namespaceName
  $property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ParentID", "$nodeCSPURI", "String", "Key")
  $newInstance.CimInstanceProperties.Add($property)
  $property = [Microsoft.Management.Infrastructure.CimProperty]::Create("InstanceID", "$ProfileNameEscaped", "String", "Key")
  $newInstance.CimInstanceProperties.Add($property)
  $property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ProfileXML", "$ProfileXML", "String", "Property")
  $newInstance.CimInstanceProperties.Add($property)
  $session.CreateInstance($namespaceName, $newInstance, $options)
  $Message = "Created $ProfileName profile."


  Write-Host "$Message"
}
catch [Exception]
{
$Message = "Unable to create $ProfileName profile: $_"
Write-Host "$Message"
exit
}

$Message = "Script Complete"
Write-Host "$Message"'
```

### <a name="save-the-profile-xml-file"></a>Speichern der Profil-XML-Datei

```xml
$Script | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.ps1')

$Message = "Successfully created VPN_Profile.xml and VPN_Profile.ps1 on the desktop."
Write-Host "$Message"
```

## <a name="makeprofileps1-full-script"></a>Vollständiges Skript MakeProfile.ps1

Die meisten Beispiele verwenden die Set-WmiInstance Windows PowerShell-Cmdlet zum Einfügen von "profileXML" in eine neue Instanz der MDM_VPNv2_01 WMI-Klasse. 

Dies ist jedoch nicht in System Center Configuration Manager arbeiten, da es sich bei Ausführen des Pakets in der Endbenutzer-Kontext kann nicht. Aus diesem Grund wird dieses Skript verwendet das Common Information Model zum Erstellen einer WMI-Sitzung im Kontext des Benutzers, und erstellt dann eine neue Instanz der MDM_VPNv2_01 WMI-Klasse in dieser Sitzung. Diese WMI-Klasse verwendet die WMI-zu-CSP-Bridge, um die VPNv2 CSP konfigurieren. Durch Hinzufügen der Klasseninstanz, konfigurieren Sie daher den CSP. 

>[!IMPORTANT]
>WMI-zu-CSP-Bridge erfordert lokale Administratorrechte verfügen, beabsichtigt. Um pro Benutzer VPN-Profile bereitstellen, sollten Sie SCCM oder MDM einsetzen

>[!NOTE]
>Das Skript VPN_Profile.ps1 verwendet die SID des aktuellen Benutzers, um den Kontext des Benutzers zu identifizieren. Da keine SID in einer Remotedesktopsitzung verfügbar ist, funktioniert das Skript nicht in einer Remotedesktopsitzung. Ebenso funktioniert es nicht in einer Sitzung für Hyper-V erweitert. Wenn Sie eine Remotezugriffsbereitstellung immer auf VPN auf virtuellen Computern testen, deaktivieren Sie die erweiterten Sitzungsmodus auf dem Client-VMs vor dem Ausführen dieses Skripts.

Das folgende Beispielskript enthält alle Codebeispiele in den vorherigen Abschnitten. Stellen Sie sicher, dass Sie die Beispielwerte in Werte ändern, die für Ihre Umgebung geeignet sind.
    
   ```XML
    $TemplateName = 'Template'
    $ProfileName = 'Contoso AlwaysOn VPN'
    $Servers = 'vpn.contoso.com'
    $DnsSuffix = 'corp.contoso.com'
    $DomainName = '.corp.contoso.com'
    $DNSServers = '10.10.0.2,10.10.0.3'
    $TrustedNetwork = 'corp.contoso.com'

    
    $Connection = Get-VpnConnection -Name $TemplateName
    if(!$Connection)
    {
    $Message = "Unable to get $TemplateName connection profile: $_"
    Write-Host "$Message"
    exit
    }
    $EAPSettings= $Connection.EapConfigXmlStream.InnerXml
    
    $ProfileXML =
    '<VPNProfile>
      <DnsSuffix>' + $DnsSuffix + '</DnsSuffix>
      <NativeProfile>
    <Servers>' + $Servers + '</Servers>
    <NativeProtocolType>IKEv2</NativeProtocolType>
    <Authentication>
      <UserMethod>Eap</UserMethod>
      <Eap>
       <Configuration>
     '+ $EAPSettings + '
       </Configuration>
      </Eap>
    </Authentication>
    <RoutingPolicyType>SplitTunnel</RoutingPolicyType>
      </NativeProfile>
    <AlwaysOn>true</AlwaysOn>
    <RememberCredentials>true</RememberCredentials>
    <TrustedNetworkDetection>' + $TrustedNetwork + '</TrustedNetworkDetection>
      <DomainNameInformation>
    <DomainName>' + $DomainName + '</DomainName>
    <DnsServers>' + $DNSServers + '</DnsServers>
    </DomainNameInformation>
    </VPNProfile>'
    
    $ProfileXML | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.xml')
    
    $Script = '$ProfileName = ''' + $ProfileName + '''
    $ProfileNameEscaped = $ProfileName -replace ' ', '%20'
    
    $ProfileXML = ''' + $ProfileXML + '''
    
    $ProfileXML = $ProfileXML -replace '<', '&lt;'
    $ProfileXML = $ProfileXML -replace '>', '&gt;'
    $ProfileXML = $ProfileXML -replace '"', '&quot;'
    
    $nodeCSPURI = "./Vendor/MSFT/VPNv2"
    $namespaceName = "root\cimv2\mdm\dmmap"
    $className = "MDM_VPNv2_01"
    
    try
    {
    $username = Gwmi -Class Win32_ComputerSystem | select username
    $objuser = New-Object System.Security.Principal.NTAccount($username.username)
    $sid = $objuser.Translate([System.Security.Principal.SecurityIdentifier])
    $SidValue = $sid.Value
    $Message = "User SID is $SidValue."
    Write-Host "$Message"
    }
    catch [Exception]
    {
    $Message = "Unable to get user SID. User may be logged on over Remote Desktop: $_"
    Write-Host "$Message"
    exit
    }
    
    $session = New-CimSession
    $options = New-Object Microsoft.Management.Infrastructure.Options.CimOperationOptions
    $options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Type", "PolicyPlatform_UserContext", $false)
    $options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Id", "$SidValue", $false)
    
        try
    {
        $deleteInstances = $session.EnumerateInstances($namespaceName, $className, $options)
        foreach ($deleteInstance in $deleteInstances)
        {
            $InstanceId = $deleteInstance.InstanceID
            if ("$InstanceId" -eq "$ProfileNameEscaped")
            {
                $session.DeleteInstance($namespaceName, $deleteInstance, $options)
                $Message = "Removed $ProfileName profile $InstanceId"
                Write-Host "$Message"
            } else {
                $Message = "Ignoring existing VPN profile $InstanceId"
                Write-Host "$Message"
            }
        }
    }
    catch [Exception]
    {
        $Message = "Unable to remove existing outdated instance(s) of $ProfileName profile: $_"
        Write-Host "$Message"
        exit
    }
    
    try
    {
        $newInstance = New-Object Microsoft.Management.Infrastructure.CimInstance $className, $namespaceName
        $property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ParentID", "$nodeCSPURI", "String", "Key")
        $newInstance.CimInstanceProperties.Add($property)
        $property = [Microsoft.Management.Infrastructure.CimProperty]::Create("InstanceID", "$ProfileNameEscaped", "String", "Key")
        $newInstance.CimInstanceProperties.Add($property)
        $property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ProfileXML", "$ProfileXML", "String", "Property")
        $newInstance.CimInstanceProperties.Add($property)
        $session.CreateInstance($namespaceName, $newInstance, $options)
        $Message = "Created $ProfileName profile."

        Write-Host "$Message"
    }
    catch [Exception]
    {
        $Message = "Unable to create $ProfileName profile: $_"
        Write-Host "$Message"
        exit
    }
    
    $Message = "Script Complete"
    Write-Host "$Message"'
    
    $Script | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.ps1')
    
    $Message = "Successfully created VPN_Profile.xml and VPN_Profile.ps1 on the desktop."
    Write-Host "$Message"
   ```

## <a name="configure-the-vpn-client-by-using-windows-powershell"></a>Konfigurieren des VPN-Clients mithilfe von Windows PowerShell

Um die VPNv2 CSP auf einem Windows 10-Clientcomputer zu konfigurieren, führen Sie das VPN_Profile.ps1 Windows PowerShell-Skript, das Sie in erstellt die [erstellen Sie das Profil-XML](#create-the-profile-xml) Abschnitt. Öffnen Sie Windows PowerShell als Administrator an. Andernfalls erhalten Sie eine Fehlermeldung _Zugriffsverweigerung_.

Nach der Ausführung VPN_Profile.ps1 das VPN-Profil konfigurieren, können Sie jederzeit überprüfen, dass es erfolgreich war, indem Sie den folgenden Befehl in der Windows PowerShell ISE ausführen:

```powershell
Get-WmiObject -Namespace root\cimv2\mdm\dmmap -Class MDM_VPNv2_01
```

**Erfolgreiche Ergebnisse aus dem Get-WmiObject-cmdlet**

```powershell
__GENUS : 2
__CLASS : MDM_VPNv2_01
__SUPERCLASS:
__DYNASTY   : MDM_VPNv2_01
__RELPATH   : MDM_VPNv2_01.InstanceID="Contoso%20AlwaysOn%20VPN",ParentID
  ="./Vendor/MSFT/VPNv2"
__PROPERTY_COUNT: 10
__DERIVATION: {}
__SERVER: WIN01
__NAMESPACE : root\cimv2\mdm\dmmap
__PATH  : \\WIN01\root\cimv2\mdm\dmmap:MDM_VPNv2_01.InstanceID="Conto
  so%20AlwaysOn%20VPN",ParentID="./Vendor/MSFT/VPNv2"
AlwaysOn: True
ByPassForLocal  :
DnsSuffix   : corp.contoso.com
EdpModeId   :
InstanceID  : Contoso%20AlwaysOn%20VPN
LockDown:
ParentID: ./Vendor/MSFT/VPNv2
ProfileXML  : <VPNProfile><RememberCredentials>true</RememberCredentials>
  <AlwaysOn>true</AlwaysOn><DnsSuffix>corp.contoso.com</DnsSu
  ffix><TrustedNetworkDetection>corp.contoso.com</TrustedNetw
  orkDetection><NativeProfile><Servers>vpn.contoso.com;vpn.co
  ntoso.com</Servers><RoutingPolicyType>SplitTunnel</RoutingP
  olicyType><NativeProtocolType>Ikev2</NativeProtocolType><Au
  thentication><UserMethod>Eap</UserMethod><MachineMethod>Eap
  </MachineMethod><Eap><Configuration><EapHostConfig xmlns="h
  ttp://www.microsoft.com/provisioning/EapHostConfig"><EapMet
  hod><Type xmlns="https://www.microsoft.com/provisioning/EapC
  ommon">25</Type><VendorId xmlns="https://www.microsoft.com/p
  rovisioning/EapCommon">0</VendorId><VendorType xmlns="http:
  //www.microsoft.com/provisioning/EapCommon">0</VendorType><
  AuthorId xmlns="https://www.microsoft.com/provisioning/EapCo
  mmon">0</AuthorId></EapMethod><Config xmlns="https://www.mic
  rosoft.com/provisioning/EapHostConfig"><Eap xmlns="https://w
  ww.microsoft.com/provisioning/BaseEapConnectionPropertiesV1
  "><Type>25</Type><EapType xmlns="https://www.microsoft.com/p
  rovisioning/MsPeapConnectionPropertiesV1"><ServerValidation
  ><DisableUserPromptForServerValidation>true</DisableUserPro
  mptForServerValidation><ServerNames>NPS</ServerNames><Trust
  edRootCA>3f 07 88 e8 ac 00 32 e4 06 3f 30 f8 db 74 25 e1
  2e 5b 84 d1 </TrustedRootCA></ServerValidation><FastReconne
  ct>true</FastReconnect><InnerEapOptional>false</InnerEapOpt
  ional><Eap xmlns="https://www.microsoft.com/provisioning/Bas
  eEapConnectionPropertiesV1"><Type>13</Type><EapType xmlns="
  https://www.microsoft.com/provisioning/EapTlsConnectionPrope
  rtiesV1"><CredentialsSource><CertificateStore><SimpleCertSe
  lection>true</SimpleCertSelection></CertificateStore></Cred
  entialsSource><ServerValidation><DisableUserPromptForServer
  Validation>true</DisableUserPromptForServerValidation><Serv
  erNames>NPS</ServerNames><TrustedRootCA>3f 07 88 e8 ac 00
  32 e4 06 3f 30 f8 db 74 25 e1 2e 5b 84 d1 </TrustedRootCA><
  /ServerValidation><DifferentUsername>false</DifferentUserna
  me><PerformServerValidation xmlns="https://www.microsoft.com
  /provisioning/EapTlsConnectionPropertiesV2">true</PerformSe
  rverValidation><AcceptServerName xmlns="https://www.microsof
  t.com/provisioning/EapTlsConnectionPropertiesV2">true</Acce
  ptServerName></EapType></Eap><EnableQuarantineChecks>false<
  /EnableQuarantineChecks><RequireCryptoBinding>false</Requir
  eCryptoBinding><PeapExtensions><PerformServerValidation xml
  ns="https://www.microsoft.com/provisioning/MsPeapConnectionP
  ropertiesV2">true</PerformServerValidation><AcceptServerNam
  e xmlns="https://www.microsoft.com/provisioning/MsPeapConnec
  tionPropertiesV2">true</AcceptServerName></PeapExtensions><
  /EapType></Eap></Config></EapHostConfig></Configuration></E
  ap></Authentication></NativeProfile><DomainNameInformation>
  <DomainName>corp.contoso.com</DomainName><DnsServers>10.10.
      0.2,10.10.0.3</DnsServers><AutoTrigger>true</AutoTrigger></
  DomainNameInformation></VPNProfile>
RememberCredentials : True
TrustedNetworkDetection : corp.contoso.com
PSComputerName  : WIN01
```

Die "profileXML"-Konfiguration muss in der Struktur, Rechtschreibung, Konfiguration und manchmal Groß-/Kleinschreibung korrekt sein. Wenn Sie etwas anderes in der Struktur, Liste 1 angezeigt wird, enthält das "profileXML"-Markup, das wahrscheinlich einen Fehler aus.

Wenn Sie das Markup beheben müssen, ist es einfacher, es in einem XML-Editor als, beheben sie in der Windows PowerShell ISE zu platzieren. Beginnen Sie in beiden Fällen mit der einfachsten Version des Profils, und fügen Sie Komponenten wieder einzeln nacheinander bis das Problem erneut auftritt.

## <a name="configure-the-vpn-client-by-using-system-center-configuration-manager"></a>Konfigurieren des VPN-Clients mithilfe von System Center Configuration Manager

In System Center Configuration Manager können Sie VPN-Profile mithilfe des ProfileXML CSP-Knotens, wie Sie in Windows PowerShell bereitstellen. Hier verwenden Sie das VPN_Profile.ps1 Windows PowerShell-Skript, das Sie im Abschnitt erstellten [erstellen die Konfigurationsdateien "profileXML"](#create-the-profilexml-configuration-files).

Um System Center Configuration Manager verwenden, um eine Remote Access Always On-VPN-Profil für Windows 10-Clientcomputern bereitstellen, müssen Sie erstellen Sie zunächst eine Gruppe von Computern oder Benutzern, die Sie das Profil bereitstellen. Erstellen Sie in diesem Szenario eine Benutzergruppe aus, um das Skript bereitzustellen.

### <a name="create-a-user-group"></a>Erstellen einer Benutzergruppe

1.  Öffnen Sie in der Configuration Manager-Konsole Bestand und Kompatibilität\\Benutzersammlungen.

2.  Auf der **Startseite** im Menüband in die **erstellen** auf **Benutzersammlung erstellen**.

3.  Führen Sie auf der Seite Allgemein die folgenden Schritte aus:

    a. In **Namen**, Typ **VPN-Benutzer**.

    b. Klicken Sie auf **Durchsuchen**, klicken Sie auf **alle Benutzer** , und klicken Sie auf **OK**.

    c. Klicken Sie auf **Weiter**.

4.  Führen Sie die folgenden Schritte aus, auf der Seite Mitgliedschaftsregeln:

    a.  In **Mitgliedschaftsregeln**, klicken Sie auf **Regel hinzufügen**, und klicken Sie auf **Direktregel**. In diesem Beispiel sind die User-Auflistung einzelner Benutzer hinzugefügt werden. Allerdings können Sie eine Abfrageregel verwenden, um Benutzer, die dieser Sammlung dynamisch für eine größere Bereitstellung hinzuzufügen.

    b.  Klicken Sie auf der **Willkommenseite** auf **Weiter**.

    c.  Auf der Seite "Ressourcen" Suchen in **Wert**, geben Sie den Namen des Benutzers, die Sie hinzufügen möchten. Der Ressourcenname enthält die Domäne des Benutzers. Um Ergebnisse auf Grundlage einer teilweisen Übereinstimmung einzubinden, fügen die **%** -Zeichen am Ende des Ihre Suchkriterium. Um alle Benutzer, die mit der Zeichenfolge "Lori" zu suchen, geben Sie z. B. **% Lori %** . Klicken Sie auf **Weiter**.

    d.  Wählen Sie auf der Seite Ressourcen auswählen die Benutzer, die Sie verwenden möchten, zur Gruppe hinzufügen, und klicken Sie auf **Weiter**.

    e.  Klicken Sie auf der Seite Zusammenfassung auf **Weiter**.

    f.  Klicken Sie auf der Seite auf **schließen**.

6.  Klicken Sie auf der Seite Mitgliedschaftsregeln des Assistenten zum Erstellen von Benutzer-Auflistung auf **Weiter**.

7.  Klicken Sie auf der Seite Zusammenfassung auf **Weiter**.

8.  Klicken Sie auf der Seite auf **schließen**.

Nachdem Sie die Gruppe "Benutzer" erhalten das VPN-Profil erstellen, können Sie erstellen, ein Paket und Programm, das Windows PowerShell-Konfigurationsskript bereitzustellen, die Sie im Abschnitt erstellt haben [erstellen die Konfigurationsdateien "profileXML"](#create-the-profilexml-configuration-files).

### <a name="create-a-package-containing-the-profilexml-configuration-script"></a>Erstellen eines Pakets mit das Konfigurationsskript "profileXML"

1.  Hosten Sie das Skript VPN_Profile.ps1 auf einer Netzwerkfreigabe, die das Computerkonto des Standorts zugreifen können.

2.  Öffnen Sie in der Configuration Manager-Konsole **Softwarebibliothek\\Anwendungsverwaltung\\Pakete**.

3.  Auf der **Startseite** im Menüband in die **erstellen** gruppieren, klicken Sie auf **Erstellen eines Pakets** zum Erstellen von Paketen und Programmerstellungs-Assistenten zu starten.

4.  Führen Sie auf der Seite Paket die folgenden Schritte aus:

    a. In **Namen**, Typ **Windows 10 immer auf VPN-Profil**.

    b. Wählen Sie die **dieses Paket enthält Quelldateien** , und klicken Sie auf **Durchsuchen**.

    c. Klicken Sie in das Dialogfeld Quellordner festlegen, auf **Durchsuchen**, wählen Sie die Dateifreigabe, die VPN_Profile.ps1 enthält, und klicken Sie auf **OK**.
        Stellen Sie sicher, dass Sie einen Netzwerkpfad, der nicht auf einen lokalen Pfad auswählen. Das heißt, der Pfad sollte etwa wie  *\\Fileserver\\Vpnscript*, nicht *c:\\Vpnscript*.

1.  Klicken Sie auf **Weiter**.

2.  Klicken Sie auf der Seite Programmtyp **Weiter**.

3.  Führen Sie auf der Seite "Standardprogramm" die folgenden Schritte aus:

    a.  In **Namen**, Typ **VPN-Profilskript**.

    b.  In **Befehlszeile**, Typ **umgehen, PowerShell.exe - ExecutionPolicy - Datei "VPN_Profile.ps1"** .

    c.  In **Ausführmodus**, klicken Sie auf **mit Administratorrechten ausführen**.

    d.  Klicken Sie auf **Weiter**.

4.  Führen Sie auf der Seite Anforderungen die folgenden Schritte aus:

    a.  Wählen Sie **dieses Programm kann nur auf bestimmten Plattformen ausgeführt**.

    b.  Wählen Sie die **alle Windows 10 (32-Bit)** und **alle Windows 10 (64-Bit)** Kontrollkästchen.

    c.  In **geschätzter Speicherplatz**, Typ **1**.

    d.  In **maximal zulässige Laufzeit (Minuten)** , Typ **15**.

    e.  Klicken Sie auf **Weiter**.

5.  Klicken Sie auf der Seite Zusammenfassung auf **Weiter**.

6.  Klicken Sie auf der Seite auf **schließen**.

Mit dem Paket und Programm erstellt haben, müssen Sie zum Bereitstellen der **VPN-Benutzer** Gruppe.

### <a name="deploy-the-profilexml-configuration-script"></a>Das Konfigurationsskript "profileXML" bereitstellen

1.  Öffnen Sie in der Configuration Manager-Konsole Softwarebibliothek\\Anwendungsverwaltung\\Pakete.

2.  In **Pakete**, klicken Sie auf **Windows 10 immer auf VPN-Profil**.

3.  Auf der **Programme** Registerkarte am unteren Rand der rechten Maustaste **VPN-Profilskript**, klicken Sie auf **Eigenschaften**, und führen Sie die folgenden Schritte aus:

    a.  Auf der **erweitert** Registerkarte **Wenn dieses Programm auf einem Computer zugewiesen ist**, klicken Sie auf **einmal für jeden Benutzer, der sich anmeldet**.

    b.  Klicken Sie auf **OK**.

4.  Mit der rechten Maustaste **VPN-Profilskript** , und klicken Sie auf **bereitstellen** um den Assistenten zum Bereitstellen von Software zu starten.

5.  Führen Sie auf der Seite Allgemein die folgenden Schritte aus:

    a.  Neben **Auflistung**, klicken Sie auf **Durchsuchen**.

    b.  In der **Auflistungstypen** Liste (links oben), klicken Sie auf **Benutzersammlungen**.

    c.  Klicken Sie auf **VPN-Benutzer**, und klicken Sie auf **OK**.

    d.  Klicken Sie auf **Weiter**.

6.  Führen Sie auf der Seite Inhalt die folgenden Schritte aus:

    a.  Klicken Sie auf **hinzufügen**, und klicken Sie auf **Verteilungspunkt**.

    b.  In **verfügbaren Verteilungspunkte**, wählen Sie die Verteilungspunkte, die Sie verteilen das Konfigurationsskript "profileXML", und klicken Sie auf möchten **OK**.

    c.  Klicken Sie auf **Weiter**.

7.  Klicken Sie auf die Bereitstellungseinstellungen (Seite), auf **Weiter**.

8.  Führen Sie auf der Seite zeitplanung die folgenden Schritte aus:

    a.  Klicken Sie auf **neu** um das Dialogfeld "Zuweisungszeitplan" zu öffnen.

    b.  Klicken Sie auf **direkt nach diesem Ereignis zuweisen**, und klicken Sie auf **OK**.

    c.  Klicken Sie auf **Weiter**.

9.  Führen Sie auf der Seite Benutzerfreundlichkeit die folgenden Schritte aus:

    1.  Wählen Sie die **Softwareinstallation** Kontrollkästchen.

    2.  Klicken Sie auf **Zusammenfassung**.

10. Klicken Sie auf der Seite Zusammenfassung auf **Weiter**.

11. Klicken Sie auf der Seite auf **schließen**.

Melden Sie sich auf einem Windows 10-Clientcomputer mit dem Benutzerkonto an, die, das Sie ausgewählt, wenn Sie die User-Auflistung erstellt, mit "profileXML" Konfigurationsskript bereitgestellt. Überprüfen Sie die Konfiguration des VPN-Clients aus.

>[!NOTE]
>Das Skript VPN_Profile.ps1 funktioniert nicht in einer Remotedesktopsitzung. Ebenso funktioniert es nicht in einer Sitzung für Hyper-V erweitert. Wenn Sie eine Remotezugriffsbereitstellung immer auf VPN auf virtuellen Computern testen, deaktivieren Sie die erweiterten Sitzungsmodus auf dem virtuellen Computer-Client, bevor Sie fortfahren.

### <a name="verify-the-configuration-of-the-vpn-client"></a>Überprüfen Sie die Konfiguration des VPN-Clients

1.  In der Systemsteuerung unter **System\\Sicherheit**, klicken Sie auf **Configuration Manager**. 

2.  Klicken Sie im Dialogfeld "Configuration Manager-Eigenschaften" auf die **Aktionen** Registerkarte, die folgenden Schritte ausführen:

    a.  Klicken Sie auf **Computerrichtlinienabruf und Evaluierungszyklus**, klicken Sie auf **Run Now**, und klicken Sie auf **OK**.

    b.  Klicken Sie auf **Benutzerrichtlinienabruf und Auswertungszyklus**, klicken Sie auf **Run Now**, und klicken Sie auf **OK**.

    c.  Klicken Sie auf **OK**.

3.  Schließen Sie die Systemsteuerung.

Das neue VPN-Profil sollte in Kürze angezeigt werden.

## <a name="configure-the-vpn-client-by-using-intune"></a>Konfigurieren des VPN-Clients mit Intune

Um Intune zum Bereitstellen von Windows 10 Remote Access Always On-VPN-Profilen zu verwenden, können Sie konfigurieren Sie den ProfileXML CSP-Knoten mithilfe des VPN-Profils, die Sie im Abschnitt erstellten [erstellen die Konfigurationsdateien "profileXML"](#create-the-profilexml-configuration-files), oder Sie können die Basis EAP XML-Beispiel unten.

>[!NOTE]
>Intune verwendet jetzt die Azure AD-Gruppen. Wenn Azure AD Connect der VPN-Benutzergruppe von lokalen Standorten mit Azure AD synchronisiert und der VPN-Benutzergruppe Benutzer zugewiesen sind, sind Sie bereit sind, fortzufahren.

Erstellen Sie die VPN-Gerät-Konfigurationsrichtlinie zum Konfigurieren der Windows 10-Clientcomputern für alle Benutzer der Gruppe hinzugefügt. Da die Vorlage mit Intune VPN-Parameter bereitstellt, kopieren Sie nur die \<EapHostConfig > \</EapHostConfig > Teil der VPN_ProfileXML-Datei.

### <a name="create-the-always-on-vpn-configuration-policy"></a>Erstellen Sie die Richtlinie für Always On-VPN-Konfiguration

1.  Melden Sie sich bei der [Azure-Portal](https://portal.azure.com/).

2.  Wechseln Sie zu **Intune** > **Gerätekonfiguration** > **Profile**.

3.  Klicken Sie auf **Profil erstellen** um das Profil erstellen Assistenten zu starten.

4.  Geben Sie einen **Namen** für das VPN-Profil und (optional) eine Beschreibung.

1.   Unter **Plattform**wählen **Windows 10 oder höher**, und wählen Sie **-VPN-** aus dem Profil Typ Dropdownliste aus.

     >[!TIP]
     >Wenn Sie ein benutzerdefiniertes VPN "profileXML" erstellen, finden Sie unter [anwenden "profileXML" mithilfe von Intune](https://docs.microsoft.com/windows/security/identity-protection/vpn/vpn-profile-options#apply-profilexml-using-intune) Anweisungen.

2. Unter den **Basis-VPN** Registerkarte, stellen Sie sicher, oder legen Sie die folgenden Einstellungen:

    - **Verbindungsname:** Geben Sie den Namen der VPN-Verbindung, wie er auf dem Clientcomputer die **VPN** Registerkarte **Einstellungen**, z. B. _Contoso AutoVPN_.  
    
    - **Server:** Fügen Sie einen oder mehrere VPN-Server, indem Sie auf **hinzufügen.**
    
    - **Beschreibung** und **IP-Adresse oder FQDN:** Geben Sie die Beschreibung und die IP-Adresse oder den vollqualifizierten Domänennamen des VPN-Server. Diese Werte müssen mit dem Antragstellernamen in der VPN-Server-Authentifizierungszertifikat ausgerichtet werden. 
    
    - **Standardserver:** Wenn dies der VPN-Standardserver ist, legen Sie auf **"true"** . Dies aktiviert diesen Server als Standardserver, den Geräte zu verwenden, um die Verbindung herzustellen. 
    
    - **Verbindungstyp:** Legen Sie auf **IKEv2**.  
    
    - **AlwaysOn:** Legen Sie auf **aktivieren** das VPN automatisch bei der Anmeldung herstellen und diese in Verbindung bleiben, bis der Benutzer manuell getrennt wird.
    
    - **Beachten Sie bei jeder Anmeldung**:  Boolescher Wert ("true" oder "false") für die Zwischenspeicherung von Anmeldeinformationen. Wenn es sich bei Festlegung auf "true", Anmeldeinformationen zwischengespeichert werden, wann immer möglich.

3.  Kopieren Sie die folgende XML-Zeichenfolge in einen Texteditor ein:
 
    [!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]
    
    
    ```XML
    <EapHostConfig xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><EapMethod><Type xmlns="https://www.microsoft.com/provisioning/EapCommon">25</Type><VendorId xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorId><VendorType xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorType><AuthorId xmlns="https://www.microsoft.com/provisioning/EapCommon">0</AuthorId></EapMethod><Config xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><Eap xmlns="https://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>25</Type><EapType xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV1"><ServerValidation><DisableUserPromptForServerValidation>true</DisableUserPromptForServerValidation><ServerNames>NPS.contoso.com</ServerNames><TrustedRootCA>5a 89 fe cb 5b 49 a7 0b 1a 52 63 b7 35 ee d7 1c c2 68 be 4b </TrustedRootCA></ServerValidation><FastReconnect>true</FastReconnect><InnerEapOptional>false</InnerEapOptional><Eap xmlns="https://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>13</Type><EapType xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV1"><CredentialsSource><CertificateStore><SimpleCertSelection>true</SimpleCertSelection></CertificateStore></CredentialsSource><ServerValidation><DisableUserPromptForServerValidation>true</DisableUserPromptForServerValidation><ServerNames>NPS.contoso.com</ServerNames><TrustedRootCA>5a 89 fe cb 5b 49 a7 0b 1a 52 63 b7 35 ee d7 1c c2 68 be 4b </TrustedRootCA></ServerValidation><DifferentUsername>false</DifferentUsername><PerformServerValidation xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">true</AcceptServerName></EapType></Eap><EnableQuarantineChecks>false</EnableQuarantineChecks><RequireCryptoBinding>false</RequireCryptoBinding><PeapExtensions><PerformServerValidation xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2">true</AcceptServerName></PeapExtensions></EapType></Eap></Config></EapHostConfig>
    ```

4.  Ersetzen Sie die  **\<TrustedRootCA > 5a 89 Fe Cb 5 b 49 a7 0 b 1a 52 63 b7 35 Ee d7 1c c2 68 werden 4 b <\/TrustedRootCA >** im obigen Beispiel durch den Zertifikatfingerabdruck der Stammzertifizierungsstelle für Ihre lokalen an beiden Orten.
  
    >[!Important]
    >Verwenden Sie nicht den Beispiel-Fingerabdruck in der \<TrustedRootCA >\</TrustedRootCA > Weiter unten.  Die TrustedRootCA muss den Zertifikatfingerabdruck der Stammzertifizierungsstelle für die lokale sein, die das Serverauthentifizierungszertifikat für RRAS und NPS-Server ausgestellt hat. **Dies muss nicht das Stammzertifikat für die Cloud, und der intermediate Zertifikatfingerabdruck für die ausstellende Zertifizierungsstelle**.

5.  Ersetzen Sie die  **\<ServerNames > NPS.contoso.com\</ServerNames >** in der XML-Beispieldatei mit dem vollqualifizierten Domänennamen, der die Domäne eingebundenen NPS, in denen Authentifizierung erfolgt. 

6.  Kopieren Sie die geänderte XML-Zeichenfolge, und fügen Sie in der **EAP-Xml** Feld auf der Basis-VPN-Registerkarte, und klicken Sie auf **OK**.
    Eine immer auf VPN-Gerätekonfiguration-Richtlinie mithilfe von EAP wird in Intune erstellt.


### <a name="sync-the-always-on-vpn-configuration-policy-with-intune"></a>Synchronisieren Sie die Always On-VPN-Konfigurationsrichtlinie mit Intune

Um die Richtlinie für die Konfiguration zu testen, melden Sie sich auf einem Windows 10-Client-Computer als der Benutzer Sie hinzugefügt haben, um die **immer auf VPN-Benutzer** Gruppe und dann auf mit Intune synchronisieren.

1.  Klicken Sie auf im Menü Start auf **Einstellungen**.

2.  Klicken Sie unter "Einstellungen" auf **Konten**, und klicken Sie auf **Zugriff auf Geschäfts-, Schul- oder unikonto**.

3.  Klicken Sie auf das Profil für die Verwaltung mobiler Geräte, und klicken Sie auf **Informationen**.

4.  Klicken Sie auf **Sync** zu erzwingen, dass eine Auswertung der Intune-Richtlinie und abrufen.

5.  Schließen Sie die Einstellungen. Nach der Synchronisierung sehen Sie das VPN-Profil verfügbar sind, auf dem Computer.

## <a name="next-steps"></a>Nächste Schritte

Bereitstellen von Always On-VPN-erfolgt.  Finden Sie für andere Funktionen, die Sie konfigurieren können in der folgenden Tabelle:

|Wenn Sie möchten...  |Anzeige...  |
|---------|---------|
|Konfigurieren des bedingten Zugriffs für VPN    |[Schritt 7: (Optional) Konfigurieren des bedingten Zugriffs für VPN-Verbindungen mithilfe von Azure AD](../../ad-ca-vpn-connectivity-windows10.md): In diesem Schritt haben Sie präzise steuern von autorisierten VPN-Benutzerzugriff Ihre Ressourcen mit [Azure Active Directory (Azure AD) bedingten Zugriff](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). Mit Azure AD für bedingten Zugriff für Verbindungen über virtuelles privates Netzwerk (VPN) helfen Ihnen, die VPN-Verbindungen schützen. Beim bedingten Zugriff handelt es sich um ein richtlinienbasiertes Auswertungsmodul, mit dem Sie Zugriffsregeln für alle mit Azure Active Directory (Azure AD) verknüpften Anwendungen erstellen können.         |
|Erfahren Sie mehr über die erweiterten VPN-Funktionen  |[Erweiterte VPN-Features](always-on-vpn-adv-options.md#advanced-vpn-features): Diese Seite enthält Anleitungen zur VPN-IP-Filter aktivieren, konfigurieren Sie automatische VPN-Verbindungen mithilfe von App-Trigger und Gewusst wie: Konfigurieren von NPS, um VPN-Verbindungen nur von Clients mithilfe von Azure AD ausgestellten Zertifikaten zu ermöglichen.        |
