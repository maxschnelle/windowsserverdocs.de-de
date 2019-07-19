---
title: Konfigurieren von Windows 10-Client immer auf VPN-Verbindungen
description: In diesem Schritt erfahren Sie mehr über die profileXML-Optionen und das Schema und konfigurieren die Windows 10-Client Computer für die Kommunikation mit dieser Infrastruktur über eine VPN-Verbindung.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.date: 05/29/2018
ms.assetid: d165822d-b65c-40a2-b440-af495ad22f42
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.reviewer: deverette
ms.openlocfilehash: c853926157a4efa414c56d97affa0a1d2faad629
ms.sourcegitcommit: 1bc3c229e9688ac741838005ec4b88e8f9533e8a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68314346"
---
# <a name="step-6-configure-windows-10-client-always-on-vpn-connections"></a>Schritt 6 Konfigurieren von Windows 10-Client Always on-VPN-Verbindungen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorher** Schritt 5 Konfigurieren von DNS und Firewalleinstellungen](vpn-deploy-dns-firewall.md)<br>
- [**Weiter** Schritt 7 Optionale Bedingter Zugriff für VPN-Konnektivität mithilfe von Azure AD](../../ad-ca-vpn-connectivity-windows10.md)

In diesem Schritt erfahren Sie mehr über die profileXML-Optionen und das Schema und konfigurieren die Windows 10-Client Computer für die Kommunikation mit dieser Infrastruktur über eine VPN-Verbindung.

Sie können den Always on VPN-Client über PowerShell, SCCM oder InTune konfigurieren. Alle drei erfordern ein XML-VPN-Profil, um die entsprechenden VPN-Einstellungen zu konfigurieren. Die Automatisierung der PowerShell-Registrierung für Organisationen ohne SCCM oder InTune ist möglich.

>[!NOTE]
>Gruppenrichtlinie enthält keine administrativen Vorlagen zum Konfigurieren des Windows 10-Remote Zugriffs Always on VPN-Clients.  Sie können jedoch Anmelde Skripts verwenden.

## <a name="profilexml-overview"></a>Übersicht über profileXML

ProfileXML ist ein URI-Knoten innerhalb des VPNv2-CSP. Anstatt jeden VPNv2 CSP-Knoten einzeln zu konfigurieren – beispielsweise Trigger, Routenlisten und Authentifizierungsprotokolle – verwenden Sie diesen Knoten, um einen Windows 10-VPN-Client zu konfigurieren, indem Sie alle Einstellungen als einen einzelnen XML-Block an einen einzelnen CSP-Knoten überführen. Das Schema "profileXML" gleicht das Schema der VPNv2-CSP-Knoten nahezu identisch ab, aber einige Begriffe unterscheiden sich geringfügig.

Sie verwenden profileXML in allen von dieser Bereitstellung beschriebenen Übermittlungs Methoden, einschließlich Windows PowerShell, System Center Configuration Manager und InTune. Es gibt zwei Möglichkeiten, den profileXML VPNv2 CSP-Knoten in dieser Bereitstellung zu konfigurieren:

- **OMA-DM**. Eine Möglichkeit ist die Verwendung eines MDM-Anbieters mithilfe von OMA-DM, wie bereits im Abschnitt [VPNv2 CSP-Knoten](../always-on-vpn-technology-overview.md#vpnv2-csp-nodes)erläutert. Mit dieser Methode können Sie das XML-Markup für die VPN-Profil Konfiguration bei Verwendung von InTune problemlos in den profileXML-CSP-Knoten einfügen.

- **Windows-Verwaltungsinstrumentation (WMI)-zu-CSP-Bridge**. Die zweite Methode zum Konfigurieren des profileXML-CSP-Knotens ist die Verwendung der WMI-zu-CSP-Bridge – eine WMI-Klasse mit dem Namen **MDM_VPNv2_01**–, die auf den Knoten VPNv2 CSP und den profileXML-Knoten zugreifen kann. Wenn Sie eine neue Instanz dieser WMI-Klasse erstellen, verwendet WMI den CSP, um das VPN-Profil zu erstellen, wenn Windows PowerShell und System Center Configuration Manager verwendet werden.

Obwohl sich diese Konfigurations Methoden unterscheiden, benötigen beide ein ordnungsgemäß formatiertes XML-VPN-Profil. Um die profileXML VPNv2 CSP-Einstellung zu verwenden, erstellen Sie XML, indem Sie das profileXML-Schema verwenden, um die für das einfache Bereitstellungs Szenario erforderlichen Tags zu konfigurieren. Weitere Informationen finden Sie unter [profileXML XSD](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-profile-xsd).

Unten finden Sie alle erforderlichen Einstellungen und das zugehörige profileXML-Tag. Sie konfigurieren jede Einstellung in einem bestimmten Tag im profileXML-Schema, und nicht alle werden im nativen Profil gefunden. Weitere tagplatzierung finden Sie unter dem profileXML-Schema.

[!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]

**Verbindungstyp:** Native IKEv2

ProfileXML-Element:

```xml
<NativeProtocolType>IKEv2</NativeProtocolType>
```

**Routing** Tunnelung aufteilen

ProfileXML-Element:

```xml
<RoutingPolicyType>SplitTunnel</RoutingPolicyType>
```

**Namensauflösung:** Domänen Namen-Informationsliste und DNS-Suffix

ProfileXML-Elemente:

```xml
<DomainNameInformation>
<DomainName>.corp.contoso.com</DomainName>
<DnsServers>10.10.1.10,10.10.1.50</DnsServers>
</DomainNameInformation>

<DnsSuffix>corp.contoso.com</DnsSuffix>
```

**Ängste** Erkennung von Always on und vertrauenswürdigen Netzwerken

ProfileXML-Elemente:

```xml
<AlwaysOn>true</AlwaysOn>
<TrustedNetworkDetection>corp.contoso.com</TrustedNetworkDetection>
```

**Genehmigung** Peer-TLS mit TPM-geschützten Benutzer Zertifikaten

ProfileXML-Elemente:

```xml
<Authentication>
<UserMethod>Eap</UserMethod>
<Eap>
<Configuration>...</Configuration>
</Eap>
</Authentication>
```

Sie können einfache Tags verwenden, um einige VPN-Authentifizierungsmechanismen zu konfigurieren. EAP und PEAP sind jedoch mehr beteiligt. Die einfachste Möglichkeit, das XML-Markup zu erstellen, besteht darin, einen VPN-Client mit seinen EAP-Einstellungen zu konfigurieren und diese Konfiguration anschließend in XML zu exportieren.

Weitere Informationen zu EAP-Einstellungen finden Sie unter [EAP-Konfiguration](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/eap-configuration).

## <a name="manually-create-a-template-connection-profile"></a>Manuelles Erstellen eines Vorlagen Verbindungs Profils

In diesem Schritt verwenden Sie das Protected Extensible Authentication Protocol (Peer) zum Sichern der Kommunikation zwischen dem Client und dem Server. Anders als bei einem einfachen Benutzernamen und einem Kennwort muss für diese Verbindung ein eindeutiger eapconfiguration-Abschnitt im VPN-Profil verwendet werden.

Anstatt zu beschreiben, wie das XML-Markup von Grund auf neu erstellt wird, verwenden Sie Einstellungen in Windows, um ein VPN-Vorlagen Profil zu erstellen. Nachdem Sie das Vorlagen-VPN-Profil erstellt haben, verwenden Sie Windows PowerShell, um den eapconfiguration-Teil aus dieser Vorlage zu verwenden, um die endgültige profileXML zu erstellen, die Sie später in der Bereitstellung bereitstellen.

### <a name="record-nps-certificate-settings"></a>NPS-Zertifikat Einstellungen aufzeichnen

Notieren Sie sich vor dem Erstellen der Vorlage den Hostnamen oder den voll qualifizierten Domänen Namen (Fully Qualified Domain Name, FQDN) des NPS-Servers aus dem Zertifikat des Servers und den Namen der Zertifizierungsstelle, die das Zertifikat ausgestellt hat.

**Dringlichkeit**

1. Öffnen Sie auf dem NPS-Server den Netzwerk Richtlinien Server.

2. Klicken Sie in der NPS-Konsole unter Richtlinien auf **Netzwerk Richtlinien**.

3. Klicken Sie mit der rechten Maustaste auf **VPN-Verbindungen (virtuelles privates Netzwerk)** , und klicken Sie auf **Eigenschaften**.

4. Klicken Sie auf die Registerkarte **Einschränkungen** , und klicken Sie auf **Authentifizierungsmethoden**.

5. Klicken Sie in EAP- **Typen auf Microsoft: Geschütztes EAP (PEAP)** , und klicken Sie auf **Bearbeiten**.

6. Notieren Sie die Werte für das **Zertifikat, das für** den **Aussteller**ausgestellt wurde

    Diese Werte werden in der bevorstehenden Konfiguration der VPN-Vorlage verwendet. Wenn z. b. der voll qualifizierte Name des Servers nps01.Corp.contoso.com und der Hostname nps01 lautet, basiert der Zertifikat Name auf dem voll qualifizierten Namen oder DNS-Namen des Servers, z. –. nps01.Corp.contoso.com.

7. Beenden Sie das Dialogfeld geschützte EAP-Eigenschaften bearbeiten.

8. Beenden Sie das Dialogfeld Eigenschaften für virtuelles privates Netzwerk (VPN).

9. Schließen Sie den Netzwerk Richtlinien Server.

>[!NOTE]
>Wenn Sie über mehrere NPS-Server verfügen, führen Sie diese Schritte nacheinander aus, damit das VPN-Profil überprüfen kann, ob die einzelnen Server verwendet werden sollen.

### <a name="configure-the-template-vpn-profile-on-a-domain-joined-client-computer"></a>Konfigurieren des VPN-Vorlagen Profils auf einem in die Domäne eingebundenen Client Computer

Nachdem Sie nun über die erforderlichen Informationen verfügen, konfigurieren Sie das Vorlagen-VPN-Profil auf einem in die Domäne eingebundenen Client Computer. Der von Ihnen verwendete Benutzer Kontotyp (d. h. Standardbenutzer oder Administrator) ist für diesen Teil des Prozesses nicht von Bedeutung.

Wenn Sie den Computer jedoch seit dem Konfigurieren der automatischen Zertifikat Registrierung nicht neu gestartet haben, sollten Sie dies vor dem Konfigurieren der VPN-Vorlagen Verbindung tun, um sicherzustellen, dass ein verwendbares Zertifikat für das Zertifikat registriert ist.

>[!NOTE]
>Es gibt keine Möglichkeit, erweiterte Eigenschaften von VPN manuell hinzuzufügen, z. b. NRPT-Regeln, Always on, Erkennung vertrauenswürdiger Netzwerke usw. Im nächsten Schritt erstellen Sie eine VPN-Testverbindung, um die Konfiguration des VPN-Servers zu überprüfen und eine VPN-Verbindung mit dem Server herzustellen.

**Manuelles Erstellen einer einzelnen Test-VPN-Verbindung**

1.  Melden Sie sich bei einem in die Domäne eingebundenen Client Computer als Mitglied der Gruppe " **VPN-Benutzer** " an.

2.  Geben Sie im Startmenü **VPN**ein, und drücken Sie die EINGABETASTE.

3.  Klicken Sie im Detailbereich auf **VPN-Verbindung hinzufügen**.

4.  Klicken Sie in der Liste VPN-Anbieter auf **Windows (integriert)** .

5.  Geben Sie unter Verbindungs Name die Bezeichnung **Vorlage**ein.

6.  Geben Sie unter Server Name oder Adresse den **externen** voll qualifizierten Namen des VPN-Servers ein (z. b. **VPN.contoso.com**).

7.  Klicken Sie auf **Speichern**.

8.  Klicken Sie unter Verwandte Einstellungen auf **Adapter Optionen ändern**.

9.  Klicken Sie mit der rechten Maustaste auf **Vorlage**, und klicken Sie auf **Eigenschaften**

10. Klicken Sie auf der Registerkarte **Sicherheit** unter **Typ des VPN**auf **IKEv2**.

11. Klicken Sie unter Datenverschlüsselung auf **Verschlüsselung der maximalen Stärke**.

12. Klicken Sie auf **Extensible Authentication Protocol (EAP) verwenden**. Klicken Sie **dann unter **Extensible Authentication Protocol (EAP) verwenden**auf Microsoft: Geschütztes EAP (PEAP) (Verschlüsselung aktiviert)** .

13. Klicken Sie auf **Eigenschaften** , um das Dialogfeld Eigenschaften für geschütztes EAP zu öffnen, und führen Sie die folgenden Schritte aus:

    a. Geben Sie im Feld **Verbindung mit diesen Servern herstellen** den Namen des NPS-Servers ein, den Sie aus den NPS-Server-Authentifizierungs Einstellungen weiter oben in diesem Abschnitt abgerufen haben (z. b. NPS01).

    >[!NOTE]
    >Der Servername, den Sie eingeben, muss mit dem Namen im Zertifikat identisch sein. Diesen Namen haben Sie zuvor in diesem Abschnitt wieder hergestellt. Wenn der Name nicht stimmt, schlägt die Verbindung fehl, und es wird angegeben, dass die Verbindung aufgrund einer Richtlinie, die auf Ihrem RAS/VPN-Server konfiguriert wurde, verhindert wurde.

    b.  Wählen Sie unter Vertrauenswürdige Stamm Zertifizierungsstellen die Stamm Zertifizierungsstelle aus, die das Zertifikat des NPS-Servers ausgestellt hat (z. b. "Configuration Manager").

    c.  Klicken Sie in Benachrichtigungen vor dem Herstellen einer Verbindung auf **Benutzer nicht zur Autorisierung neuer Server oder vertrauenswürdiger Zertifizierungsstellen**.

    d.  Wählen Sie unter Authentifizierungsmethode auswählen die Option **Smartcard oder anderes Zertifikat**aus, und klicken Sie dann auf **Konfigurieren**. Das Dialogfeld Smartcard-oder andere Zertifikat Eigenschaften wird geöffnet.

    e.  Klicken Sie **auf Zertifikat auf diesem Computer verwenden**.

    f.  Geben Sie im Feld Verbindung mit diesen Servern herstellen den Namen des NPS-Servers ein, den Sie in den vorherigen Schritten aus den NPS-Server Authentifizierungs Einstellungen abgerufen haben.

    g.  Wählen Sie unter Vertrauenswürdige Stamm Zertifizierungsstellen die Stamm Zertifizierungsstelle aus, von der das Zertifikat des NPS-Servers ausgestellt wurde.

    h.  Aktivieren Sie das Kontrollkästchen **Benutzer nicht zur Autorisierung neuer Server oder vertrauenswürdiger Zertifizierungsstellen auffordern** .

    i.  Klicken Sie auf **OK** , um das Dialogfeld Smartcard-oder andere Zertifikat Eigenschaften zu schließen.

    j.  Klicken Sie auf **OK** , um das Dialogfeld Eigenschaften für geschütztes EAP zu schließen.

14. Klicken Sie auf **OK** , um das Dialogfeld Vorlagen Eigenschaften zu schließen.

15. Schließen Sie das Fenster Netzwerkverbindungen.

16. Testen Sie das VPN in den Einstellungen, indem Sie auf **Vorlage**und dann auf **verbinden**klicken.

>[!IMPORTANT]
>Stellen Sie sicher, dass die VPN-Vorlagen Verbindung mit Ihrem VPN-Server erfolgreich ist. Dadurch wird sichergestellt, dass die EAP-Einstellungen korrekt sind, bevor Sie im nächsten Beispiel verwendet werden. Sie müssen mindestens einmal eine Verbindung herstellen, bevor Sie fortfahren. Andernfalls enthält das Profil nicht alle Informationen, die erforderlich sind, um eine Verbindung mit dem VPN herzustellen.

## <a name="create-the-profilexml-configuration-files"></a>Erstellen der profileXML-Konfigurationsdateien

Vergewissern Sie sich vor dem Abschließen dieses Abschnitts, dass Sie die VPN-Vorlagen Verbindung erstellt und getestet haben, die im Abschnitt [Manuelles Erstellen eines Vorlagen Verbindungs Profils](#manually-create-a-template-connection-profile) beschrieben wird. Das Testen der VPN-Verbindung ist erforderlich, um sicherzustellen, dass das Profil alle für die Verbindung mit dem VPN erforderlichen Informationen enthält.

Mit dem Windows PowerShell-Skript in der Liste 1 werden zwei Dateien auf dem Desktop erstellt, von denen beide **eapconfiguration** -Tags enthalten, die auf dem zuvor erstellten Vorlagen Verbindungsprofil basieren:

- **VPN_Profile. Xml.** Diese Datei enthält das XML-Markup, das erforderlich ist, um den profileXML-Knoten im VPNv2-CSP zu konfigurieren. Verwenden Sie diese Datei mit OMA-DM – kompatiblen MDM-Diensten wie InTune.

- **VPN_Profile. ps1.** Bei dieser Datei handelt es sich um ein Windows PowerShell-Skript, das Sie auf Client Computern ausführen können, um den profileXML-Knoten im VPNv2-CSP zu konfigurieren. Sie können den CSP auch konfigurieren, indem Sie dieses Skript über System Center Configuration Manager bereitstellen. Sie können dieses Skript nicht in einer Remotedesktop Sitzung ausführen, einschließlich einer erweiterten Hyper-V-Sitzung.

>[!IMPORTANT]
>Die folgenden Beispiel Befehle erfordern Windows 10 Build 1607 oder höher.

**Create VPN_Profile. XML und VPN_Proflie. ps1**

1. Melden Sie sich bei dem in die Domäne eingebundenen Client Computer an, auf dem das VPN-Vorlagen Profil mit dem gleichen Benutzerkonto enthalten ist, und [Erstellen Sie manuell ein Vorlagen Verbindungsprofil](#manually-create-a-template-connection-profile) .

2. Fügen Sie die Liste 1 in Windows PowerShell Integrated Scripting Environment (ISE) ein, und passen Sie die Parameter an, die in den Kommentaren beschrieben werden. Dabei handelt es sich um $Template, $ProfileName, $Servers, $DnsSuffix, $Domainname, $TrustedNetwork und $DnsServers. Eine vollständige Beschreibung der einzelnen Einstellungen finden Sie in den Kommentaren.

3. Führen Sie das Skript aus, um **VPN_Profile. XML** und **VPN_Profile. ps1** auf dem Desktop zu generieren.

#### <a name="listing-1-understanding-makeprofileps1"></a>Codebeispiel 1. Grundlegendes zu makeprofile. ps1

In diesem Abschnitt wird der Beispielcode erläutert, den Sie verwenden können, um ein Verständnis für die Erstellung eines VPN-Profils zu erhalten, insbesondere für die Konfiguration von profileXML im VPNv2-CSP.

Nachdem Sie ein Skript aus diesem Beispielcode assembliert und das Skript ausgeführt haben, generiert das Skript zwei Dateien: VPN_Profile. XML und VPN_Profile. ps1. Verwenden Sie VPN_Profile. XML, um profileXML in OMA-DM-kompatiblen MDM-Diensten wie z. b. Microsoft InTune zu konfigurieren.

Verwenden Sie das Skript **VPN_Profile. ps1** in Windows PowerShell oder System Center Configuration Manager, um profileXML auf dem Windows 10-Desktop zu konfigurieren.

>[!NOTE]
>Das vollständige Beispielskript finden Sie im Abschnitt [makeprofile. ps1 Full Script](#makeprofileps1-full-script).

#### <a name="parameters"></a>Parameter

Konfigurieren Sie die folgenden Parameter:

**$Template**. Der Name der Vorlage, aus der die EAP-Konfiguration abgerufen werden soll.

**$ProfileName**. Eindeutiger alphanumerischer Bezeichner für das Profil. Der Profilname darf keinen Schrägstrich (/) enthalten. Wenn der Profilname ein Leerzeichen oder ein anderes nicht alphanumerisches Zeichen enthält, muss er gemäß dem URL-Codierungsstandard ordnungsgemäß mit Escapezeichen versehen werden.

**$Servers**. Öffentliche oder Routing fähige IP-Adresse oder DNS-Name für das VPN-Gateway. Sie kann auf die externe IP-Adresse eines Gateways oder auf eine virtuelle IP-Adresse für eine Serverfarm zeigen. Beispiele, 208.147.66.130 oder VPN.contoso.com.

**$DnsSuffix**. Gibt ein oder mehrere durch Kommas getrennte DNS-Suffixe an. Der erste in der Liste wird auch als primäres Verbindungs spezifisches DNS-Suffix für die VPN-Schnittstelle verwendet. Die gesamte Liste wird auch der suffixsearchlist hinzugefügt.

**$Domainname**. Wird verwendet, um den Namespace anzugeben, auf den die Richtlinie angewendet wird. Wenn eine Namensabfrage ausgegeben wird, vergleicht der DNS-Client den Namen in der Abfrage mit allen Namespaces unter domainnameinformationlist, um eine Übereinstimmung zu finden. Dieser Parameter kann einen der folgenden Typen aufweisen:

- FQDN-vollständig qualifizierter Domänen Name
- Suffix: ein Domänen Suffix, das an die Kurznamen-Abfrage für die DNS-Auflösung angefügt wird. Um ein Suffix anzugeben, fügen Sie dem DNS-Suffix einen Zeitraum (.) vorangestellt.

**$DnsServers**. Liste der durch Trennzeichen getrennten DNS-Server-IP-Adressen, die für den Namespace verwendet werden sollen.

**$TrustedNetwork**. Durch Trennzeichen getrennte Zeichenfolge zum Identifizieren des vertrauenswürdigen Netzwerks. VPN stellt keine automatische Verbindung her, wenn sich der Benutzer in seinem Unternehmens-Drahtlos Netzwerk befindet, in dem geschützte Ressourcen direkt für das Gerät zugänglich sind.

Im folgenden finden Sie Beispiel Werte für Parameter, die in den folgenden Befehlen verwendet werden. Stellen Sie sicher, dass Sie diese Werte für Ihre Umgebung ändern.

```xml
$TemplateName = 'Template'
$ProfileName = 'Contoso AlwaysOn VPN'
$Servers = 'vpn.contoso.com'
$DnsSuffix = 'corp.contoso.com'
$DomainName = '.corp.contoso.com'
$DNSServers = '10.10.0.2,10.10.0.3'
$TrustedNetwork = 'corp.contoso.com'
```

### <a name="prepare-and-create-the-profile-xml"></a>Vorbereiten und Erstellen der Profil-XML

Mit den folgenden Beispiel Befehlen werden EAP-Einstellungen aus dem Vorlagen Profil angezeigt:

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

### <a name="create-the-profile-xml"></a>Erstellen der Profil-XML

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

### <a name="output-vpnprofilexml-for-intune"></a>Output VPN_Profile. XML for InTune

Sie können den folgenden Beispiel Befehl verwenden, um die XML-Profil Datei zu speichern:

```xml
$ProfileXML | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.xml')
```

### <a name="output-vpnprofileps1-for-the-desktop-and-system-center-configuration-manager"></a>Ausgabe von VPN_Profile. ps1 für den Desktop und System Center Configuration Manager

Der folgende Beispielcode konfiguriert eine AlwaysOn-IKEv2-VPN-Verbindung mit dem profileXML-Knoten im VPNv2-CSP.

Sie können dieses Skript auf dem Windows 10-Desktop oder in System Center Configuration Manager verwenden.

### <a name="define-key-vpn-profile-parameters"></a>Definieren von Schlüssel-VPN-Profil Parametern

```xml
$Script = '$ProfileName = ''' + $ProfileName + ''''
$ProfileNameEscaped = $ProfileName -replace ' ', '%20'
```

## <a name="define-vpn-profilexml"></a>Definieren von VPN profileXML

```xml
$ProfileXML = ''' + $ProfileXML + '''
```

### <a name="escape-special-characters-in-the-profile"></a>Sonderzeichen im Profil mit Escapezeichen versehen

```xml
$ProfileXML = $ProfileXML -replace '<', '&lt;'
$ProfileXML = $ProfileXML -replace '>', '&gt;'
$ProfileXML = $ProfileXML -replace '"', '&quot;'
```

### <a name="define-wmi-to-csp-bridge-properties"></a>Definieren von WMI-zu-CSP-Brücken Eigenschaften

```xml
$nodeCSPURI = "./Vendor/MSFT/VPNv2"
$namespaceName = "root\cimv2\mdm\dmmap"
$className = "MDM_VPNv2_01"
```

### <a name="determine-user-sid-for-vpn-profile"></a>Bestimmen Sie die Benutzer-SID für das VPN-Profil:

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

### <a name="define-wmi-session"></a>Definieren einer WMI-Sitzung:

```xml
$session = New-CimSession
$options = New-Object Microsoft.Management.Infrastructure.Options.CimOperationOptions
$options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Type", "PolicyPlatform_UserContext", $false)
$options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Id", "$SidValue", $false)
```

### <a name="detect-and-delete-previous-vpn-profile"></a>Vorheriges VPN-Profil erkennen und löschen:

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
Write-Host "$Message"
```

### <a name="save-the-profile-xml-file"></a>Speichern der XML-Profil Datei

```xml
$Script | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.ps1')

$Message = "Successfully created VPN_Profile.xml and VPN_Profile.ps1 on the desktop."
Write-Host "$Message"
```

## <a name="makeprofileps1-full-script"></a>Vollständiges Skript für makeprofile. ps1

In den meisten Beispielen wird das Windows PowerShell-Cmdlet Set-wmiinstance verwendet, um profileXML in eine neue Instanz der MDM_VPNv2_01-WMI-Klasse einzufügen. 

Dies funktioniert jedoch nicht in System Center Configuration Manager, da das Paket nicht im Kontext des Endbenutzers ausgeführt werden kann. Daher verwendet dieses Skript das Common Information Model, um eine WMI-Sitzung im Kontext des Benutzers zu erstellen. Anschließend wird eine neue Instanz der MDM_VPNv2_01-WMI-Klasse in dieser Sitzung erstellt. Diese WMI-Klasse verwendet die WMI-zu-CSP-Bridge, um den VPNv2-CSP zu konfigurieren. Daher konfigurieren Sie den CSP durch Hinzufügen der Klasseninstanz. 

>[!IMPORTANT]
>Die WMI-zu-CSP-Bridge erfordert die lokalen Administratorrechte. Zum Bereitstellen von pro-Benutzer-VPN-Profilen sollten Sie SCCM oder MDM verwenden.

>[!NOTE]
>Das Skript VPN_Profile. ps1 verwendet die SID des aktuellen Benutzers, um den Kontext des Benutzers zu identifizieren. Da keine SID in einer Remotedesktop Sitzung verfügbar ist, funktioniert das Skript nicht in einer Remotedesktop Sitzung. Ebenso funktioniert es nicht in einer erweiterten Hyper-V-Sitzung. Wenn Sie einen Remote Zugriff Always on-VPN auf virtuellen Computern testen, deaktivieren Sie die erweiterte Sitzung auf Ihren Client-VMS, bevor Sie dieses Skript ausführen.

Das folgende Beispielskript enthält alle Codebeispiele aus den vorherigen Abschnitten. Stellen Sie sicher, dass Sie Beispiel Werte in Werte ändern, die für Ihre Umgebung geeignet sind.
    
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
    
    $ProfileXML = ''' + $ProfileXML + ''''
    
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
    Write-Host "$Message"
    
    $Script | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.ps1')
    
    $Message = "Successfully created VPN_Profile.xml and VPN_Profile.ps1 on the desktop."
    Write-Host "$Message"
   ```

## <a name="configure-the-vpn-client-by-using-windows-powershell"></a>Konfigurieren des VPN-Clients mithilfe von Windows PowerShell

Um den VPNv2-CSP auf einem Windows 10-Client Computer zu konfigurieren, führen Sie das Windows PowerShell-Skript VPN_Profile. ps1 aus, das Sie im Abschnitt [Erstellen des Profils "XML](#create-the-profile-xml) " erstellt haben. Öffnen Sie Windows PowerShell als Administrator. Andernfalls erhalten Sie die Fehlermeldung " _Zugriff verweigert_".

Nach dem Ausführen von VPN_Profile. ps1 zum Konfigurieren des VPN-Profils können Sie jederzeit überprüfen, ob es erfolgreich war, indem Sie den folgenden Befehl im Windows PowerShell ISE ausführen:

```powershell
Get-WmiObject -Namespace root\cimv2\mdm\dmmap -Class MDM_VPNv2_01
```

**Erfolgreiche Ergebnisse des Cmdlets "Get-WmiObject"**

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

Die profileXML-Konfiguration muss in der Struktur, in der Rechtschreibung, in der Konfiguration und in manchen Fällen recht groß sein. Wenn Sie in der Struktur etwas anderes als das Auflisten 1 sehen, enthält das profileXML-Markup wahrscheinlich einen Fehler.

Wenn Sie eine Problembehandlung für das Markup durchsetzen müssen, ist es einfacher, es in einem XML-Editor zu platzieren, als es in der Windows PowerShell ISE behandeln zu müssen. Beginnen Sie in jedem Fall mit der einfachsten Version des Profils, und fügen Sie Komponenten nacheinander hinzu, bis das Problem erneut auftritt.

## <a name="configure-the-vpn-client-by-using-system-center-configuration-manager"></a>Konfigurieren des VPN-Clients mithilfe von System Center Configuration Manager

In System Center Configuration Manager können Sie VPN-profile bereitstellen, indem Sie den profileXML-CSP-Knoten genau wie in Windows PowerShell verwenden. Hier verwenden Sie das Windows PowerShell-Skript VPN_Profile. ps1, das Sie im Abschnitt [Erstellen der profileXML-Konfigurationsdateien](#create-the-profilexml-configuration-files)erstellt haben.

Wenn Sie System Center Configuration Manager für die Bereitstellung eines Remote Zugriffs Always on VPN-Profils für Windows 10-Client Computer verwenden möchten, müssen Sie zunächst eine Gruppe von Computern oder Benutzern erstellen, für die Sie das Profil bereitstellen. Erstellen Sie in diesem Szenario eine Benutzergruppe, um das Konfigurationsskript bereitzustellen.

### <a name="create-a-user-group"></a>Erstellen einer Benutzergruppe

1.  Öffnen Sie in der Configuration Manager Konsole Assets und Konformität\\Benutzer Sammlungen.

2.  Klicken Sie auf dem Menüband **Start** in der Gruppe **Erstellen** auf **Benutzer Sammlung erstellen**.

3.  Führen Sie auf der Seite Allgemein die folgenden Schritte aus:

    a. Geben Sie unter **Name den Namen** **VPN-Benutzer**ein.

    b. Klicken Sie auf **Durchsuchen**, dann auf **alle Benutzer** und dann auf **OK**.

    c. Klicken Sie auf **Weiter**.

4.  Führen Sie auf der Seite Mitgliedschafts Regeln die folgenden Schritte aus:

    a.  Klicken Sie unter **Mitgliedschafts Regeln**auf **Regel hinzufügen**, und klicken Sie auf **direkt Regel**. In diesem Beispiel fügen Sie einzelne Benutzer zur Benutzer Sammlung hinzu. Sie können jedoch eine Abfrage Regel verwenden, um dieser Sammlung für eine größere Bereitstellung dynamisch Benutzer hinzuzufügen.

    b.  Klicken Sie auf der **Willkommenseite** auf **Weiter**.

    c.  Geben Sie auf der Seite Ressourcen suchen unter **Wert**den Namen des Benutzers ein, den Sie hinzufügen möchten. Der Ressourcen Name enthält die Domäne des Benutzers. Um Ergebnisse auf der Grundlage einer Teil Übereinstimmung einzuschließen, fügen Sie das **%** Zeichen an beiden Enden des Such Kriteriums ein. Wenn Sie z. b. alle Benutzer suchen möchten, die die Zeichenfolge "Lori" enthalten, geben Sie **% Lori%** ein. Klicken Sie auf **Weiter**.

    d.  Wählen Sie auf der Seite Ressourcen auswählen die Benutzer aus, die Sie der Gruppe hinzufügen möchten, und klicken Sie auf **weiter**.

    e.  Klicken Sie auf der Seite Zusammenfassung auf **weiter**.

    f.  Klicken Sie auf der Seite Abschluss auf **Schließen**.

6.  Klicken Sie im Assistenten zum Erstellen von Benutzer Sammlungen auf der Seite Mitgliedschafts Regeln auf **weiter**.

7.  Klicken Sie auf der Seite Zusammenfassung auf **weiter**.

8.  Klicken Sie auf der Seite Abschluss auf **Schließen**.

Nachdem Sie die Benutzergruppe für den Empfang des VPN-Profils erstellt haben, können Sie ein Paket und ein Programm erstellen, um das Windows PowerShell-Konfigurationsskript bereitzustellen, das Sie im Abschnitt [Erstellen der profileXML-Konfigurationsdateien](#create-the-profilexml-configuration-files)erstellt haben.

### <a name="create-a-package-containing-the-profilexml-configuration-script"></a>Erstellen eines Pakets, das das profileXML-Konfigurationsskript enthält

1.  Hosten Sie das Skript VPN_Profile. ps1 auf einer Netzwerkfreigabe, auf die das Computer Konto des Standort Servers zugreifen kann.

2.  Öffnen Sie in der Configuration Manager-Konsole **Software\\Bibliothek Anwendungs\\Verwaltung Pakete**.

3.  Klicken Sie auf dem Menüband **Start** in der Gruppe **Erstellen** auf **Paket erstellen** , um den Assistenten zum Erstellen von Paketen und Programmen zu starten.

4.  Führen Sie auf der Seite Paket die folgenden Schritte aus:

    a. Geben Sie unter **Name den Namen** **Windows 10 Always on VPN-Profil**ein.

    b. Aktivieren Sie das Kontrollkästchen **Dieses Paket enthält Quelldateien** , und klicken Sie auf **Durchsuchen**.

    c. Klicken Sie im Dialogfeld Quellordner festlegen auf **Durchsuchen**, wählen Sie die Dateifreigabe mit VPN_Profile. ps1 aus, und klicken Sie auf **OK**.
        Stellen Sie sicher, dass Sie einen Netzwerkpfad und keinen lokalen Pfad auswählen. Anders ausgedrückt: der Pfad sollte in etwa wie folgt aussehen  *\\:\\File Server vpnscript*, nicht *c:\\vpnscript*.

1.  Klicken Sie auf **Weiter**.

2.  Klicken Sie auf der Seite Programmtyp auf **weiter**.

3.  Führen Sie auf der Seite Standard Programm die folgenden Schritte aus:

    a.  Geben Sie unter **Name den Namen** **VPN-Profil Skript**ein.

    b.  Geben Sie in der **Befehlszeile** **PowerShell. exe-ExecutionPolicy Bypass-file "VPN_Profile. ps1"** ein.

    c.  Klicken Sie im **Lauf Modus**auf **mit Administratorrechten ausführen**.

    d.  Klicken Sie auf **Weiter**.

4.  Führen Sie auf der Seite Anforderungen die folgenden Schritte aus:

    a.  Wählen Sie **dieses Programm kann nur auf bestimmten Plattformen ausgeführt werden aus**.

    b.  Aktivieren Sie die Kontrollkästchen **alle Windows 10 (32-Bit)** und **alle Windows 10 (64 Bit)** .

    c.  Geben Sie im Feld **Geschätzter Speicherplatz** **1 ein**.

    d.  Geben Sie unter **maximal zulässige Laufzeit (Minuten)** **15**ein.

    e.  Klicken Sie auf **Weiter**.

5.  Klicken Sie auf der Seite Zusammenfassung auf **weiter**.

6.  Klicken Sie auf der Seite Abschluss auf **Schließen**.

Nachdem Sie das Paket und das Programm erstellt haben, müssen Sie es für die **VPN-Benutzer** Gruppe bereitstellen.

### <a name="deploy-the-profilexml-configuration-script"></a>Bereitstellen des profileXML-Konfigurations Skripts

1.  Öffnen Sie in der Configuration Manager-Konsole Software\\Bibliothek Anwendungs\\Verwaltung Pakete.

2.  Klicken Sie unter **Pakete**auf **Windows 10 Always on VPN-Profil**.

3.  Klicken Sie auf der Registerkarte **Programme** unten im Detailbereich mit der rechten Maustaste auf **VPN-Profil Skript**, klicken Sie auf **Eigenschaften**, und führen Sie die folgenden Schritte aus:

    a.  Klicken Sie auf der Registerkarte **erweitert** in **Wenn dieses Programm einem Computer zugewiesen ist**, auf **einmal für jeden Benutzer, der sich anmeldet**.

    b.  Klicken Sie auf **OK**.

4.  Klicken **Sie mit der** rechten Maustaste auf **VPN-Profil Skript** , und klicken Sie auf bereitstellen, um den Assistenten zum

5.  Führen Sie auf der Seite Allgemein die folgenden Schritte aus:

    a.  Klicken Sie neben **Sammlung**auf **Durchsuchen**.

    b.  Klicken Sie in der Liste **Sammlungs Typen** (oben links) auf **Benutzer Sammlungen**.

    c.  Klicken Sie auf **VPN-Benutzer**und dann auf **OK**.

    d.  Klicken Sie auf **Weiter**.

6.  Führen Sie auf der Seite Inhalt die folgenden Schritte aus:

    a.  Klicken Sie auf **Hinzufügen**und **dann auf Verteilungs Punkt**.

    b.  Wählen Sie unter **Verfügbare Verteilungs Punkte**die Verteilungs Punkte aus, an die Sie das profileXML-Konfigurationsskript verteilen möchten, und klicken Sie auf **OK**.

    c.  Klicken Sie auf **Weiter**.

7.  Klicken Sie auf der Seite Bereitstellungs Einstellungen auf **weiter**.

8.  Führen Sie auf der Seite Zeitplanung die folgenden Schritte aus:

    a.  Klicken Sie auf **neu** , um das Dialogfeld Zuweisungs Zeitplan zu öffnen.

    b.  Klicken Sie auf **direkt nach diesem Ereignis zuweisen**, und klicken Sie auf **OK**.

    c.  Klicken Sie auf **Weiter**.

9.  Führen Sie auf der Seite Benutzer Darstellung die folgenden Schritte aus:

    1.  Aktivieren Sie das Kontrollkästchen **Software Installation** .

    2.  Klicken Sie auf **Übersicht**.

10. Klicken Sie auf der Seite Zusammenfassung auf **weiter**.

11. Klicken Sie auf der Seite Abschluss auf **Schließen**.

Melden Sie sich bei der Bereitstellung des profillexml-Konfigurations Skripts bei einem Windows 10-Client Computer mit dem Benutzerkonto an, das Sie beim Erstellen der Benutzer Sammlung ausgewählt haben. Überprüfen Sie die Konfiguration des VPN-Clients.

>[!NOTE]
>Das Skript VPN_Profile. ps1 funktioniert nicht in einer Remotedesktop Sitzung. Ebenso funktioniert es nicht in einer erweiterten Hyper-V-Sitzung. Wenn Sie einen Remote Zugriff Always on-VPN auf virtuellen Computern testen, deaktivieren Sie die erweiterte Sitzung auf Ihren Client-VMS, bevor Sie fortfahren.

### <a name="verify-the-configuration-of-the-vpn-client"></a>Überprüfen der Konfiguration des VPN-Clients

1.  Klicken Sie in der **Systemsteuerung\\unter System Sicherheit**auf **Configuration Manager**. 

2.  Führen Sie im Dialogfeld Configuration Manager Eigenschaften auf der Registerkarte **Aktionen** die folgenden Schritte aus:

    a.  Klicken Sie auf **Computer Richtlinien Abruf & Evaluierungs Zyklen**, klicken Sie auf **jetzt ausführen**, und klicken Sie auf **OK**.

    b.  Klicken Sie auf **Benutzerrichtlinien Abruf & Evaluierungs Zyklen**, klicken Sie auf **jetzt ausführen**, und klicken Sie auf **OK**.

    c.  Klicken Sie auf **OK**.

3.  Schließen Sie die Systemsteuerung.

Das neue VPN-Profil sollte in Kürze angezeigt werden.

## <a name="configure-the-vpn-client-by-using-intune"></a>Konfigurieren des VPN-Clients mithilfe von InTune

Zum Verwenden von InTune zum Bereitstellen von Windows 10-Remote Zugriff Always on VPN-Profilen können Sie den profileXML-CSP-Knoten mithilfe des VPN-Profils konfigurieren, das Sie im Abschnitt [Erstellen der profileXML-Konfigurationsdateien](#create-the-profilexml-configuration-files)erstellt haben, oder Sie können das bereitgestellte Basis-EAP-XML-Beispiel verwenden. untenstehende.

>[!NOTE]
>InTune verwendet nun Azure Ad Gruppen. Wenn Azure AD Connect die Gruppe "VPN-Benutzer" vom lokalen Standort aus mit Azure AD synchronisiert haben und Benutzer der Gruppe "VPN-Benutzer" zugewiesen sind, können Sie den Vorgang fortsetzen.

Erstellen Sie die VPN-Geräte Konfigurationsrichtlinie, um die Windows 10-Client Computer für alle Benutzer zu konfigurieren, die der Gruppe hinzugefügt wurden. Da die Intune-Vorlage VPN-Parameter bereitstellt, \<kopieren Sie nur den eaphostconfig-> \</EapHostConfig > Teil der VPN_ProfileXML-Datei.

### <a name="create-the-always-on-vpn-configuration-policy"></a>Erstellen der Always on VPN-Konfigurationsrichtlinie

1.  Melden Sie sich beim [Azure-Portal](https://portal.azure.com/) an.

2.  Wechseln Sie zu **InTune** > **Geräte Konfigurations** > **profile**.

3.  Klicken Sie zum Starten des Assistenten zum Erstellen von Profilen auf **Profil erstellen** .

4.  Geben Sie einen **Namen** für das VPN-Profil und (optional) eine Beschreibung ein.

1.   Wählen Sie unter **Plattform**die Option **Windows 10 oder**höher, **und wählen Sie** in der Dropdown-Dropdown-Dropdown-Dropdown-

     >[!TIP]
     >Wenn Sie ein benutzerdefiniertes VPN-Profil erstellen, finden Sie entsprechende Anweisungen unter [Anwenden von profileXML mithilfe von InTune](https://docs.microsoft.com/windows/security/identity-protection/vpn/vpn-profile-options#apply-profilexml-using-intune) .

2. Überprüfen oder legen Sie auf der Registerkarte **Basis-VPN** die folgenden Einstellungen fest:

    - **Verbindungs Name:** Geben Sie den Namen der VPN-Verbindung ein, wie er auf dem Client Computer auf der Registerkarte " **VPN** " unter " **Einstellungen**" angezeigt wird, z. b. "Configuration _autovpn_".  
    
    - **Webserver** Fügen Sie einen oder mehrere VPN-Server hinzu, indem Sie auf **Hinzufügen**
    
    - **Beschreibung** und **IP-Adresse oder voll qualifizierter** voll qualifizierten Namen: Geben Sie die Beschreibung und die IP-Adresse oder den voll qualifizierten Namen des VPN-Servers ein. Diese Werte müssen mit dem Antragsteller Namen im Authentifizierungszertifikat des VPN-Servers übereinstimmen. 
    
    - **Standard Server:** Wenn dies der VPN-Standard Server ist, legen Sie auf **true**fest. Dadurch kann dieser Server als Standard Server verwendet werden, der von Geräten zum Herstellen der Verbindung verwendet wird. 
    
    - **Verbindungstyp:** Legen Sie auf **IKEv2**fest.  
    
    - **Always on:** Legen Sie **so** fest, dass bei der Anmeldung automatisch eine Verbindung mit dem VPN hergestellt und die Verbindung bleibt, bis der Benutzer die Verbindung manuell trennt.
    
    - **Anmelde Informationen bei jeder Anmeldung speichern**:  Boolescher Wert (true oder false) zum Zwischenspeichern von Anmelde Informationen. Wenn der Wert auf true festgelegt ist, werden Anmelde Informationen nach Möglichkeit zwischengespeichert

3.  Kopieren Sie die folgende XML-Zeichenfolge in einen Text-Editor:
 
    [!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]
    
    
    ```XML
    <EapHostConfig xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><EapMethod><Type xmlns="https://www.microsoft.com/provisioning/EapCommon">25</Type><VendorId xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorId><VendorType xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorType><AuthorId xmlns="https://www.microsoft.com/provisioning/EapCommon">0</AuthorId></EapMethod><Config xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><Eap xmlns="https://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>25</Type><EapType xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV1"><ServerValidation><DisableUserPromptForServerValidation>true</DisableUserPromptForServerValidation><ServerNames>NPS.contoso.com</ServerNames><TrustedRootCA>5a 89 fe cb 5b 49 a7 0b 1a 52 63 b7 35 ee d7 1c c2 68 be 4b </TrustedRootCA></ServerValidation><FastReconnect>true</FastReconnect><InnerEapOptional>false</InnerEapOptional><Eap xmlns="https://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>13</Type><EapType xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV1"><CredentialsSource><CertificateStore><SimpleCertSelection>true</SimpleCertSelection></CertificateStore></CredentialsSource><ServerValidation><DisableUserPromptForServerValidation>true</DisableUserPromptForServerValidation><ServerNames>NPS.contoso.com</ServerNames><TrustedRootCA>5a 89 fe cb 5b 49 a7 0b 1a 52 63 b7 35 ee d7 1c c2 68 be 4b </TrustedRootCA></ServerValidation><DifferentUsername>false</DifferentUsername><PerformServerValidation xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">true</AcceptServerName></EapType></Eap><EnableQuarantineChecks>false</EnableQuarantineChecks><RequireCryptoBinding>false</RequireCryptoBinding><PeapExtensions><PerformServerValidation xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2">true</AcceptServerName></PeapExtensions></EapType></Eap></Config></EapHostConfig>
    ```

4.  Ersetzen Sie die  **\<Datei "treuhändrootca > 5A 89 FE CB 5B 49 A7 0B 1a 52 63 B7 35 EE T7 1C C2 68 be\/4B < treudrootca >** im Beispiel mit dem Zertifikat Fingerabdruck Ihrer lokalen Stamm Zertifizierungsstelle an beiden stellen.
  
    >[!Important]
    >Verwenden Sie den Beispiel Fingerabdruck nicht im \<Abschnitt "thumbdrootca >\</TrustedRootCA > weiter unten.  Der Treuhänder muss der Zertifikat Fingerabdruck der lokalen Stamm Zertifizierungsstelle sein, von der das Server Authentifizierungszertifikat für RRAS-und NPS-Server ausgestellt wurde. **Dabei darf es sich nicht um das Cloud-Stamm Zertifikat oder um den Fingerabdruck der zwischen ausstellenden Zertifizierungsstelle handeln**.

5.  Ersetzen Sie die  **\<Server Ames > NPS.\</ServerNames. >** in der XML-Beispieldatei durch den voll qualifizierten Domänen Namen der in die Domäne eingebundenen NPS, wo die Authentifizierung stattfindet. 

6.  Kopieren **Sie die**überarbeitete XML-Zeichenfolge, und fügen Sie Sie in das Feld **EAP XML** auf der Registerkarte Basis-VPN ein.
    Eine Always on VPN-Geräte Konfigurationsrichtlinie, die EAP verwendet, wird in InTune erstellt.


### <a name="sync-the-always-on-vpn-configuration-policy-with-intune"></a>Synchronisieren der Always on-VPN-Konfigurationsrichtlinie mit InTune

Um die Konfigurationsrichtlinie zu testen, melden Sie sich bei einem Windows 10-Client Computer als Benutzer an, den Sie der Gruppe **Always on-VPN-Benutzer** hinzugefügt haben, und synchronisieren Sie dann mit InTune.

1.  Klicken Sie im Startmenü auf **Einstellungen**.

2.  Klicken Sie unter Einstellungen auf Konten und dann auf **Arbeits-oder Schul** **Konto**zugreifen.

3.  Klicken Sie auf das MDM-Profil, und klicken Sie auf **Info**.

4.  Klicken Sie auf **Synchronisieren** , um die Bewertung und den Abruf einer InTune-Richtlinie zu

5.  Schließen Sie die Einstellungen. Nach der Synchronisierung sehen Sie, dass das VPN-Profil auf dem Computer verfügbar ist.

## <a name="next-steps"></a>Nächste Schritte

Sie haben die Bereitstellung Always on VPN abgeschlossen.  Weitere Funktionen, die Sie konfigurieren können, finden Sie in der folgenden Tabelle:

|Zweck  |Anzeige...  |
|---------|---------|
|Konfigurieren des bedingten Zugriffs für VPN    |[Schritt 7: Optionale Konfigurieren des bedingten Zugriffs für VPN-Konnektivität](../../ad-ca-vpn-connectivity-windows10.md)mithilfe von Azure AD: In diesem Schritt können Sie optimieren, wie autorisierte VPN-Benutzer mithilfe des [bedingten Zugriffs von Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)auf Ihre Ressourcen zugreifen. Mit Azure AD bedingten Zugriff für VPN-Konnektivität (virtuelles privates Netzwerk) können Sie die VPN-Verbindungen schützen. Beim bedingten Zugriff handelt es sich um ein richtlinienbasiertes Auswertungsmodul, mit dem Sie Zugriffsregeln für alle mit Azure Active Directory (Azure AD) verknüpften Anwendungen erstellen können.         |
|Weitere Informationen zu den erweiterten VPN-Features  |[Erweiterte VPN-Features](always-on-vpn-adv-options.md#advanced-vpn-features): Auf dieser Seite finden Sie Anleitungen zum Aktivieren von VPN-Datenverkehrs filtern, zum Konfigurieren automatischer VPN-Verbindungen mithilfe von App-Triggern und zum Konfigurieren von NPS für die ausschließliche Verwendung von VPN-Verbindungen von Clients mithilfe von Zertifikaten, die von Azure AD ausgestellt wurden.        |
