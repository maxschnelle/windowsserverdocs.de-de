---
title: Konfigurieren von Windows 10-Client immer auf VPN-Verbindungen
description: In diesem Schritt erfahren Sie mehr über die ProfileXML-Optionen und Schema, und Konfigurieren der Windows 10-Clientcomputer für die Kommunikation mit dieser Infrastruktur mit einer VPN-Verbindung.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.date: 05/29/2018
ms.assetid: d165822d-b65c-40a2-b440-af495ad22f42
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.reviewer: deverette
ms.openlocfilehash: 6b383076686092e20448977bed3766f7d7d1c2b8
ms.sourcegitcommit: 4147e092d77d9458696e6686bccefe3788c90508
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2019
ms.locfileid: "9031314"
---
# Schritt 6. Konfigurieren von Windows 10-Client Always On VPN-Verbindungen

>Gilt für: WindowsServer (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows 10


& #171;  [ **Vorherigen:** Schritt 5. Konfigurieren von DNS und Firewall-Einstellungen](vpn-deploy-dns-firewall.md)<br>
& #187; [ **Weiter:** Schritt 7. (Optional) Bedingter Zugriff für VPN-Konnektivität mit Azure AD](../../ad-ca-vpn-connectivity-windows10.md)

In diesem Schritt erfahren Sie mehr über die ProfileXML-Optionen und Schema, und Konfigurieren der Windows 10-Clientcomputer für die Kommunikation mit dieser Infrastruktur mit einer VPN-Verbindung. 

Sie können den Always On VPN-Client über PowerShell, SCCM oder Intune konfigurieren. Alle drei erfordern eine XML-VPN-Profil so konfigurieren Sie die entsprechenden VPN-Einstellungen. Automatisieren von PowerShell ist die Registrierung für Organisationen ohne SCCM oder Intune möglich.

>[!NOTE]
>Gruppenrichtlinie enthält keine administrative Vorlagen, um den Windows 10 Remote Access Always On VPN-Client konfigurieren.  Allerdings können Sie Skripts zum Anmelden.

## ProfileXML-Übersicht

ProfileXML ist ein URI-Knoten in dem VPNv2-CSP. Anstatt jedem VPNv2-CSP-Knoten einzeln konfigurieren – z. B. Trigger, weiterleiten, Listen und Authentifizierungsprotokolle – verwenden Sie diesen Knoten zum Konfigurieren eines Windows 10-VPN-Clients durch die Bereitstellung von alle Einstellungen als einzelne XML-Block auf einen einzelnen CSP-Knoten. Das ProfileXML-Schema entspricht das Schema der Knoten VPNv2-CSP fast identisch, aber einige Begriffe unterscheiden sich leicht.

Verwenden Sie ProfileXML in alle erforderlichen, die diese Bereitstellung wird beschrieben, einschließlich Windows PowerShell, System Center Configuration Manager und Intune, die Bereitstellungsmethoden. Es gibt zwei Möglichkeiten, den ProfileXML VPNv2-CSP-Knoten in der Bereitstellung zu konfigurieren:

- **OMA-DM**. Eine Möglichkeit ist die Verwendung von OMA-DM, mit einem MDM-Anbieter, wie weiter oben im Abschnitt [VPNv2-CSP-Knoten](../always-on-vpn-technology-overview.md#vpnv2-csp-nodes)erläutert. Bei Verwendung dieser Methode können Sie einfach das VPN-Profil Configuration XML-Markup in den ProfileXML CSP-Knoten beim Einfügen Intune verwenden.

- **Windows-Verwaltungsinstrumentation (WMI) - zu - CSP-Brücke**. Die zweite Methode Konfigurieren des Knotens ProfileXML CSP ist die Verwendung die WMI-CSP-Brücke – eine WMI-Klasse namens **MDM_VPNv2_01**–, die Zugriff auf dem VPNv2-CSP und der ProfileXML-Knoten. Wenn Sie eine neue Instanz der WMI-Klasse erstellen, verwendet WMI CSP VPN-Profil erstellen, wenn Windows PowerShell und System Center Configuration Manager verwenden.

Obwohl diese Konfigurationsmethoden unterscheiden zu können, erfordern sowohl ein korrekt formatierten XML-VPN-Profil. Um die ProfileXML VPNv2-CSP-Einstellung verwenden, erstellen Sie XML mithilfe des ProfileXML-Schemas so konfigurieren Sie die Tags für das Szenario einfache Bereitstellung erforderlich. Weitere Informationen finden Sie unter [ProfileXML-XSD](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-profile-xsd).

Im Anschluss finden Sie die erforderlichen Einstellungen und dem entsprechenden ProfileXML-Tag. Konfigurieren Sie jede Einstellung in einem bestimmten Tag innerhalb des ProfileXML-Schemas, und nicht alle unter dem systemeigenen Profil gefunden werden. Zusätzliche Tag-Platzierung finden Sie unter den ProfileXML-Schema.

[!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]

**Verbindungstyp:** Systemeigene IKEv2

ProfileXML-Element:

    <NativeProtocolType>IKEv2</NativeProtocolType>

**Routing:** Split-tunneling

ProfileXML-Element:

    <RoutingPolicyType>SplitTunnel</RoutingPolicyType>

**Namensauflösung:** Domänennamen-Informationsliste und DNS-suffix

ProfileXML-Elemente:

    <DomainNameInformation>
    <DomainName>.corp.contoso.com</DomainName>
    <DnsServers>10.10.1.10,10.10.1.50</DnsServers>
    </DomainNameInformation>
    
    <DnsSuffix>corp.contoso.com</DnsSuffix>


**Auslösen:** Always On und Trusted Network Detection

ProfileXML-Elemente:

    <AlwaysOn>true</AlwaysOn>
    <TrustedNetworkDetection>corp.contoso.com</TrustedNetworkDetection>


**Authentifizierung:** PEAP-TLS mit TPM-geschütztes Benutzerzertifikate

ProfileXML-Elemente:

    <Authentication>
    <UserMethod>Eap</UserMethod>
    <Eap>
    <Configuration>...</Configuration>
    </Eap>
    </Authentication>

Sie können einfache Tags verwenden, einige Authentifizierungsmechanismen VPN konfigurieren. Allerdings sind EAP und PEAP komplizierter. Die einfachste Möglichkeit zum Erstellen von XML-Markup ist das Konfigurieren Sie eines VPN-Clients mit der EAP-Einstellungen, und die Konfiguration dann als XML-Datei exportieren. 

Weitere Informationen zu EAP-Einstellungen finden Sie unter [EAP-Konfiguration](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/eap-configuration). 

## <a name="bkmk_profile"></a>Erstellen Sie manuell eine Verbindung Profilvorlage

In diesem Schritt verwenden Sie Protected Extensible Authentication Protocol \(PEAP\) zum Schutz der Kommunikation zwischen dem Client und dem Server. Im Gegensatz zu einer einfachen Benutzername und Kennwort erfordert diese Verbindung einen einzigartigen EAPConfiguration Bereich im VPN-Profil funktioniert. 

Anstelle von beschreiben, wie Sie das XML-Markup von Grund auf neu erstellen, verwenden Sie Einstellungen in Windows eine Vorlage VPN-Profil erstellen. Nach dem Erstellen der Vorlage VPN-Profil, verwenden Sie Windows PowerShell, um den EAPConfiguration Teil aus dieser Vorlage zum Erstellen der endgültigen ProfileXML, die bereitgestellt werden später in der Bereitstellung nutzen.

### Notieren Sie die Einstellungen für NPS-Zertifikaten

Vor dem Erstellen der Vorlage, notieren Sie den Hostnamen oder der vollqualifizierte Domänenname (FQDN) des Netzwerkrichtlinienservers aus dem Server-Zertifikat und den Namen der Zertifizierungsstelle, die das Zertifikat ausgestellt.

**Verfahren:**

1.  Öffnen Sie auf dem Netzwerkrichtlinienserver Network Policy Server.

2.  Klicken Sie in der NPS-Konsole unter Richtlinien auf **Netzwerkrichtlinien**.

3.  Mit der rechten Maustaste **virtuelles privates Netzwerk \(VPN\) Verbindungen**, und klicken Sie auf **Eigenschaften**.

4.  Klicken Sie auf der Registerkarte " **Einschränkungen** ", und klicken Sie auf **Authentifizierungsmethoden zu verwenden**.

5.  Klicken Sie im EAP-Typen, auf **Microsoft: geschütztes EAP (PEAP)**, und klicken Sie auf **Bearbeiten**.

6.  Notieren Sie die Werte für das **Zertifikat ausgestellt wurde,** und **Aussteller**an.<p>Verwenden Sie diese Werte in der bevorstehenden VPN-Konfiguration. Z. B. Wenn Sie den FQDN des Servers nps01.corp.contoso.com und der Hostnamen NPS01, der Name des Zertifikats den FQDN oder DNS-Namen des Servers – z. B. nps01.corp.contoso.com basiert auf.

7.  Stornieren Sie das Dialogfeld Eigenschaften für geschütztes EAP bearbeiten.

8.  Stornieren Sie das Dialogfeld Virtual Private Network (VPN) Verbindungseigenschaften.

9.  Netzwerkrichtlinienserver zu schließen.

>[!NOTE]
>Wenn Sie mehrere NPS-Server verfügen, führen Sie diese Schritte auf jedem, damit das VPN-Profil Startlaufwerk überprüfen können sie verwendet werden sollen.

### Konfigurieren Sie die Vorlage VPN-Profil auf einem Domäne\ eingebunden Clientcomputer

Die nun die erforderliche Informationen, die die Vorlage VPN-Profil auf einem Domäne Clientcomputer zu konfigurieren. Der Typ des Benutzerkontos, die Sie verwenden \ (d. h. Standardbenutzer oder Administrator\) für diesen Teil des Prozesses keine Rolle spielt. 

Jedoch, wenn Sie den Computer neu gestartet noch nicht seit konfigurieren die automatische Registrierung von Zertifikaten, dazu vor dem Konfigurieren der Vorlage VPN-Verbindung, um sicherzustellen, dass Sie ein nutzbare Zertifikat darauf registriert haben.

>[!NOTE]
>Es gibt keine Möglichkeit keine erweiterten Eigenschaften-VPN-Verbindung, z. B. NRPT-Regeln, ständig manuell hinzufügen vertrauenswürdige Netzwerke usw.. Im nächsten Schritt erstellen Sie eine Test-VPN-Verbindung überprüfen die Konfiguration des VPN-Servers und, dass Sie eine VPN-Verbindung mit dem Server herstellen können.

**Erstellen Sie manuell einen einzelnen Test VPN-Verbindung**

1.  Melden Sie sich für einen Client Domäne als Mitglied der Gruppe **VPN-Benutzer** .

2.  Klicken Sie auf das Menü "Start" Geben Sie **VPN**, und drücken Sie die EINGABETASTE.

3.  Klicken Sie im Detailbereich auf **Hinzufügen einer VPN-Verbindung**.

4.  Klicken Sie in der Liste VPN-Anbieter auf **Windows (integrierten)**.

5.  Geben Sie im Feld Verbindungsname **Vorlage**.

6.  Geben Sie im Namen oder die Adresse, die **externe** FQDN des VPN-Servers \ (z. B.**vpn.contoso.com**\).

7.  Klicken Sie auf **Speichern**.

8.  Klicken Sie verwandte Einstellungen auf **Adapter-Optionen ändern**.

9.  Mit der rechten Maustaste **Vorlage**, und klicken Sie auf **Eigenschaften**.

10. Klicken Sie auf der Registerkarte " **Sicherheit** " in **VPN-Typ** **IKEv2**aus.

11. Verschlüsselung von Daten klicken Sie auf **Maximale Verschlüsselung**.

12. Klicken Sie auf **verwenden Extensible Authentication-Protokoll (EAP)**. in **Verwenden Extensible Authentication-Protokoll (EAP)**, klicken Sie dann auf **Microsoft: geschütztes EAP (PEAP) (Verschlüsselung aktiviert)**.

13. Klicken Sie auf **Eigenschaften** , um die Eigenschaften für geschütztes EAP-Dialogfeld zu öffnen, und führen Sie die folgenden Schritte aus:

    a. Geben Sie im Feld **Verbindung mit diesen Servern** den Namen des Netzwerkrichtlinienservers, die Sie aus den Einstellungen der NPS-Server-Authentifizierung weiter oben in diesem Abschnitt (z. B. NPS01) abgerufen.

    >[!NOTE]
    >Der Servername eingegebenen muss den Namen im Zertifikat übereinstimmen. Sie wiederhergestellt dieser Name weiter oben in diesem Abschnitt. Wenn der Name nicht übereinstimmt, fehl die Verbindung besagt, dass "die Verbindung durch eine Richtlinie auf dem RAS/VPN-Server konfiguriert verhindert wurde."

    b.  Wählen Sie unter Vertrauenswürdige Stammzertifizierungsstellen der Stammzertifizierungsstelle, die die NPS-Serverzertifikats (z. B. Contoso-CA) ausgestellt.

    c.  Benachrichtigungen vor dem Herstellen einer Verbindung klicken Sie auf **nicht Benutzer zum Autorisieren neuer Server oder vertrauenswürdiger Zertifizierungsstellen auffordern**.

    d.  Klicken Sie in Authentifizierungsmethode auswählen auf **Smartcard oder anderes Zertifikat**, und klicken Sie auf **Konfigurieren**. Die Smartcard oder andere Zertifikateigenschaften-Dialogfeld wird geöffnet.

    e.  Klicken Sie auf **ein Zertifikat auf diesem Computer verwenden**.

    f.  Geben Sie in dem diese Server-Feld Verbindung herstellen den Namen des Netzwerkrichtlinienservers, die Sie aus den Einstellungen der NPS-Server-Authentifizierung in den vorherigen Schritten abgerufen haben.

    g.  Wählen Sie unter Vertrauenswürdige Stammzertifizierungsstellen der Stammzertifizierungsstelle, die den Netzwerkrichtlinienserver Zertifikat ausgestellt.

    h.  Wählen Sie die **fordern Benutzer nicht zum neuen Server autorisieren oder vertrauenswürdigen Zertifizierungsstellen** Kontrollkästchen.

    i.  Klicken Sie auf **OK** , um die Smartcard oder andere Zertifikateigenschaften-Dialogfeld zu schließen.

    j.  Klicken Sie auf **OK** , um die Eigenschaften für geschütztes EAP-Dialogfeld zu schließen.

10. Klicken Sie auf **OK** , um die Eigenschaften der Dateiprüfungsvorlagen-Dialogfeld zu schließen.

11. Schließen Sie das Fenster Netzwerkverbindungen.

12. Testen Sie das VPN unter "Einstellungen" indem Sie auf **Vorlage**, und klicken Sie auf **Verbinden**.

>[!IMPORTANT]
>Stellen Sie sicher, dass die VPN-Verbindung mit dem VPN-Server-Vorlage erfolgreich ist. Dadurch wird sichergestellt, dass die EAP-Einstellungen korrekt sind, bevor Sie sie im nächsten Beispiel verwenden. Sie müssen mindestens einmal, bevor Sie fortfahren verbinden; Andernfalls wird das Profil nicht alle für die VPN-Verbindung erforderlichen Informationen enthalten.

## <a name="bkmk_ProfileXML"></a>Erstellen Sie die ProfileXML-Konfigurationsdateien

Vor dem Abschluss in diesem Abschnitt, stellen Sie sicher, dass Sie erstellt und die Vorlage VPN-Verbindung, die im Abschnitt [Erstellen Sie manuell eine Verbindung Profilvorlage](#bkmk_profile) beschreibt getestet haben. Testen die VPN-Verbindung ist erforderlich, um sicherzustellen, dass das Profil alle Informationen, die für die VPN-Verbindung die enthält.

Das Windows PowerShell-Skript in Codebeispiel 1 erstellt zwei Dateien auf dem Desktop, die beide enthalten **EAPConfiguration** -Tags, die basierend auf der Vorlage Profil, das Sie zuvor erstellt haben:

-   **VPN_Profile.Xml.** Diese Datei enthält das XML-Markup erforderlich, um den ProfileXML-Knoten in dem VPNv2-CSP zu konfigurieren. Verwenden Sie diese Datei mit OMA-DM-kompatiblen MDM-Dienste, z. B. Intune.

-   **VPN_Profile.ps1.** Diese Datei ist ein Windows PowerShell-Skript, die Sie ausführen können auf Clientcomputern den ProfileXML-Knoten in dem VPNv2-CSP zu konfigurieren. Sie können auch das CSP konfigurieren, durch die Bereitstellung von dieses Skript über System Center Configuration Manager. Dieses Skript kann nicht in einer Remotedesktop-Sitzung, einschließlich einer erweiterten Hyper-V-Sitzung ausgeführt werden.

>[!IMPORTANT]
>Die folgenden Beispielbefehle ist Windows 10 Build 1607 oder höher erforderlich.

**Erstellen Sie VPN_Profile.xml und VPN_Proflie.ps1**

1. Melden Sie sich bei der Domäne Clientcomputer mit der Vorlage VPN-Profil mit dem gleichen Benutzer berücksichtigen, die im Abschnitt "Erstellen Sie manuell eine Verbindung Profilvorlage" beschrieben.

2. Fügen Sie 1 Eintrag in Windows PowerShell integrated scripting Environment \(ISE\), und passen Sie die Parameter in den Kommentaren beschrieben. Hierbei handelt es sich $Template, $ProfileName, $Servers, $DnsSuffix, $DomainName, $TrustedNetwork und $DNSServers. Eine vollständige Beschreibung der einzelnen Einstellungen ist in den Kommentaren.

3.  Führen Sie das Skript zum Generieren von **VPN_Profile.xml** und **VPN_Profile.ps1** auf dem Desktop.

#### Codebeispiel 1. Grundlegendes zu MakeProfile.ps1

In diesem Abschnitt wird erläutert, den Beispielcode, den Sie verwenden können, um so erstellen Sie ein VPN-Profil, speziell für die Konfiguration von ProfileXML in dem VPNv2-CSP vertraut wird.

Nachdem Sie ein Skript aus dieser Beispielcode zusammenstellen, und führen Sie das Skript, das Skript zwei Dateien generiert: VPN_Profile.xml und VPN_Profile.ps1. Verwenden Sie VPN_Profile.xml, um ProfileXML in OMA-DM-kompatible MDM-Diensten wie Microsoft Intune konfigurieren.

Verwenden Sie das Skript **VPN_Profile.ps1** in Windows PowerShell oder System Center Configuration Manager, um ProfileXML auf dem Windows 10 Desktop zu konfigurieren.

>[!NOTE]
>Das Skript vollständiges Beispiel finden Sie unter im Abschnitt [MakeProfile.ps1 vollständige Skript](#bkmk_fullscript).

#### Parameter

Konfigurieren Sie die folgenden Parameter:

**$Template**. Der Name der Vorlage aus den EAP-Konfiguration abgerufen werden sollen.

**$ProfileName**. Eindeutige alphanumerische Kennung für das Profil. Den Namen des Profils darf keinen Schrägstrich (/) enthalten. Hat den Namen des Profils ein Leerzeichen oder andere nicht alphanumerischen Zeichen, muss es ordnungsgemäß gemäß der URL-Codierung mit Escapezeichen versehen werden.

**$Servers**. Öffentliche oder routingfähige IP-Adresse oder DNS-Namen für das VPN-Gateway. Es kann auf die externe IP-Adresse eines Gateways oder eine virtuelle IP-Adresse für eine Serverfarm verweisen. Beispiele, 208.147.66.130 oder vpn.contoso.com.

**$DnsSuffix**. Gibt an, dass eine oder mehrere Kommas DNS-Suffixe getrennt. Die erste in der Liste wird auch als das primäre verbindungsspezifische DNS-Suffix für die VPN-Schnittstelle verwendet. Die gesamte Liste wird auch in SuffixSearchList hinzugefügt werden.

**$DomainName**. Verwendet, um den Namespace anzugeben, auf dem die Richtlinie angewendet wird. Wenn eine Namensabfrage ausgegeben wird, vergleicht der DNS-Client den Namen in der Abfrage an alle Namespaces unter DomainNameInformationList eine Übereinstimmung gefunden. Dieser Parameter kann eine der folgenden Typen sein:

- FQDN - vollständig qualifizierten Domänennamen
- Suffix - Domänensuffix, die auf die Shortname-Abfrage für DNS-Auflösung angefügt werden. Um eine Suffix angeben, stellen Sie einen Zeitraum \ (.) das DNS-Suffix.

**$DNSServers**. Liste der durch Trennzeichen getrennte DNS-Server-IP-Adressen für den Namespace.

**$TrustedNetwork**. Durch Trennzeichen getrennte Zeichenfolge zur Identifizierung des vertrauenswürdigen Netzwerks. VPN wird nicht automatisch verbunden, wenn der Benutzer in ihrem WLAN-Unternehmensnetzwerk ist, in dem geschützte Ressourcen direkt auf das Gerät zugreifen können.

Folgendes Beispielwerte für Parameter, die in die folgenden Befehle verwendet werden. Stellen Sie sicher, dass Sie diese Werte für Ihre Umgebung ändern.

    $TemplateName = 'Template'
    $ProfileName = 'Contoso AlwaysOn VPN'
    $Servers = 'vpn.contoso.com'
    $DnsSuffix = 'corp.contoso.com'
    $DomainName = '.corp.contoso.com'
    $DNSServers = '10.10.0.2,10.10.0.3'
    $TrustedNetwork = 'corp.contoso.com'


### Vorbereiten Sie und erstellen Sie das Profil-XML

Die folgenden Beispielbefehle ein rufen EAP-Einstellungen aus der Profilvorlage:


    $Connection = Get-VpnConnection -Name $TemplateName
    if(!$Connection)
    {
    $Message = "Unable to get $TemplateName connection profile: $_"
    Write-Host "$Message"
    exit
    }
    $EAPSettings= $Connection.EapConfigXmlStream.InnerXml


### Erstellen Sie das Profil-XML

[!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]

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


### Ausgabe VPN_Profile.xml für Intune

Sie können den folgenden Befehl werden beispielsweise verwenden, um die Profil-XML-Datei zu speichern:

    $ProfileXML | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.xml')

### Ausgabe VPN_Profile.ps1 für den Desktop und System Center Configuration Manager

Im folgenden Codebeispiel wird eine AlwaysOn IKEv2-VPN-Verbindung mit der ProfileXML-Knoten in dem VPNv2-CSP konfiguriert.

Sie können dieses Skript auf dem Windows 10-Desktop oder in System Center Configuration Manager verwenden.

### Definieren Sie wichtige VPN-Profil-Parameter

    $Script = '$ProfileName = ''' + $ProfileName + '''
    $ProfileNameEscaped = $ProfileName -replace ' ', '%20'

## Definieren Sie die VPN-ProfileXML

    $ProfileXML = ''' + $ProfileXML + '''
    
### Escapezeichen Sie für Sonderzeichen im Profil

    $ProfileXML = $ProfileXML -replace '<', '&lt;'
    $ProfileXML = $ProfileXML -replace '>', '&gt;'
    $ProfileXML = $ProfileXML -replace '"', '&quot;'
    
### Definieren Sie WMI-CSP-Brücke-Eigenschaften

    $nodeCSPURI = "./Vendor/MSFT/VPNv2"
    $namespaceName = "root\cimv2\mdm\dmmap"
    $className = "MDM_VPNv2_01"

### Stellen Sie Benutzer-SID für VPN-Profil fest:

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
    

### Definieren Sie WMI-Sitzung:

    $session = New-CimSession
    $options = New-Object Microsoft.Management.Infrastructure.Options.CimOperationOptions
    $options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Type", "PolicyPlatform_UserContext", $false)
    $options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Id", "$SidValue", $false)


### Erkennen und vorheriges VPN-Profil löschen:

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
    

### Das VPN-Profil zu erstellen:

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

### Speichern Sie die Profil-XML-Datei

    $Script | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.ps1')
    
    $Message = "Successfully created VPN_Profile.xml and VPN_Profile.ps1 on the desktop."
    Write-Host "$Message"

## <a name="bkmk_fullscript"></a>Vollständige MakeProfile.ps1-Skript

Die meisten Beispiele verwenden des Set-WmiInstance Windows PowerShell-Cmdlets zum Einfügen von ProfileXML in eine neue Instanz der MDM_VPNv2_01 WMI-Klasse. 

Dies kann in System Center Configuration Manager jedoch nicht verwendet, da Sie das Paket im Kontext für die Endbenutzer nicht ausführen können. Aus diesem Grund dieses Skript verwendet das Modell für allgemeine Informationen zum Erstellen einer WMI-Sitzung im Kontext des Benutzers, und klicken Sie dann eine neue Instanz der MDM_VPNv2_01 WMI-Klasse in der Sitzung erstellt. Dieser WMI-Klasse verwendet die WMI-CSP-Brücke, um dem VPNv2-CSP zu konfigurieren. Durch das Hinzufügen der Klasseninstanz, konfigurieren Sie daher das CSP. 

>[!IMPORTANT]
>WMI-CSP-Brücke erfordert lokale Administratorrechte, entwurfsbedingt. Um pro Benutzer VPN-Profile sollten Sie SCCM oder MDM verwenden

>[!NOTE]
>Das Skript VPN_Profile.ps1 verwendet die SID des aktuellen Benutzers, um Kontext des Benutzers zu identifizieren. Da keine SID in einer Sitzung Remote Desktop verfügbar ist, funktioniert das Skript nicht in einer Remotedesktop-Sitzung. Ebenso funktioniert es nicht in einer Hyper-V-erweiterte Sitzung. Wenn Sie eine Remote Access Always On VPN auf virtuellen Computern testen, deaktivieren Sie die erweiterten Sitzungsmodus auf Ihrem Client VMs vor dem Ausführen dieses Skripts.

Das folgende Beispielskript enthält alle Codebeispiele aus den vorherigen Abschnitten. Stellen Sie sicher, dass Sie Beispielwerte Werte ändern, die für Ihre Umgebung geeignet sind.
    
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

## Konfigurieren des VPN-Clients mithilfe von Windows PowerShell

Um dem VPNv2-CSP auf einem Windows 10-Clientcomputer zu konfigurieren, führen Sie das VPN_Profile.ps1 Windows PowerShell-Skript, das Sie im Abschnitt [Erstellen Sie das XML-Profil](#create-the-profile-xml) erstellt. Öffnen Sie Windows PowerShell als Administrator; Andernfalls erhalten Sie eine Fehlermeldung, die besagt, _Zugriff verweigert_.

Nach dem Ausführen VPN_Profile.ps1 VPN-Profil zu konfigurieren, können Sie zu einem beliebigen Zeitpunkt überprüfen, dass diese erfolgreich war, mithilfe des folgenden Befehls in der Windows PowerShell ISE:

    Get-WmiObject -Namespace root\cimv2\mdm\dmmap -Class MDM_VPNv2_01

**Erfolgreiche Ergebnisse aus dem Cmdlet Get-WmiObject**


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

Die ProfileXML-Konfiguration muss in der Struktur, Rechtschreibprüfung, Konfiguration und manchmal Groß-/Kleinschreibung korrekt sein. Wenn Sie etwas anderes in Struktur auf 1 Eintrag angezeigt wird, enthält das ProfileXML-Markup wahrscheinlich einen Fehler.

Wenn Sie das Markup beheben müssen, ist es einfacher, die sie in einem XML-Editor als Fehlerbehebung es in der Windows PowerShell ISE versetzt. In beiden Fällen beginnen mit der einfachste Version des Profils, und fügen Sie Komponenten wieder nacheinander bis das Problem erneut auftritt.

## <a name="vpn-deploy-client-sccm"></a>Konfigurieren des VPN-Clients mithilfe von System Center Configuration Manager

In System Center Configuration Manager können Sie VPN-Profile bereitstellen, mithilfe des ProfileXML CSP-Knotens, so wie Sie in Windows PowerShell gemacht haben. Hier verwenden Sie das VPN_Profile.ps1 Windows PowerShell-Skript, das Sie im Abschnitt [Erstellen Sie die ProfileXML-Konfigurationsdateien](#bkmk_ProfileXML)erstellt haben.

Um die System Center Configuration Manager verwenden, um ein Remote Access Always On VPN-Profil auf Windows 10-Clientcomputern bereitstellen, müssen Sie zunächst erstellen eine Gruppe von Computern oder Benutzern, die Sie das Profil bereitstellen. Erstellen Sie in diesem Szenario eine Benutzergruppe aus, um das Skript bereitstellen.

### Erstellen Sie eine Benutzergruppe

1.  Öffnen Sie in der Configuration Manager-Konsole Ressourcen und Compliance\\User Sammlungen.

2.  Klicken Sie auf **Benutzer Sammlung erstellen**, auf dem Menüband **Home** in der Gruppe **Erstellen** .

3.  Führen Sie auf der Seite "Allgemein" die folgenden Schritte aus:

    a. Geben Sie den **Namen** **VPN-Benutzer**.

    b. Klicken Sie auf **Durchsuchen**, klicken Sie auf **Alle Benutzer** , und klicken Sie auf **OK**.

    c. Klicken Sie auf **Weiter**.

4.  Führen Sie auf der Seite "Mitgliedschaftsregeln" die folgenden Schritte aus:

    a.  **Mitgliedschaftsregeln**klicken Sie auf **Regel hinzufügen**, und klicken Sie auf **Direkte Regel**. In diesem Beispiel, das Sie einzelne Benutzer zu der Auflistung hinzufügen. Sie können jedoch Abfrageregel verwenden, um Benutzer diese Sammlung dynamisch für eine umfangreichere Bereitstellung hinzufügen.

    b.  Klicken Sie auf der Seite " **Willkommen** " auf **Weiter**.

    c.  Geben Sie den Namen des Benutzers, die Sie hinzufügen möchten, auf der Seite Ressourcen im **Wert**suchen. Der Name der enthält die Domäne des Benutzers. Um Ergebnisse auf Grundlage der eine teilweise Übereinstimmung einzubeziehen, setzen Sie die **%** Zeichen am Ende Ihren Suchkriterien. Geben Sie alle Benutzer, die mit der Zeichenfolge "Lori" zu finden, z. B. **% Lori %**. Klicken Sie auf **Weiter**.

    d.  Wählen Sie auf der Seite Ressourcen auswählen die Benutzer, die Sie der Gruppe hinzufügen möchten, und klicken Sie auf **Weiter**.

    e.  Klicken Sie auf der Seite "Zusammenfassung" auf " **Weiter**".

    f.  Klicken Sie auf der Seite Fertigstellung auf **Schließen**.

6.  Zurück auf der Seite des Assistenten zum Erstellen von Benutzer Sammlung Mitgliedschaftsregeln klicken Sie auf " **Weiter**".

7.  Klicken Sie auf der Seite "Zusammenfassung" auf " **Weiter**".

8.  Klicken Sie auf der Seite Fertigstellung auf **Schließen**.

Nachdem Sie die Benutzergruppe Empfang von VPN-Profil erstellen, können Sie erstellen, ein Paket und Programm, um das Windows PowerShell-Skript bereitzustellen, das Sie im Abschnitt [Erstellen Sie die ProfileXML-Konfigurationsdateien](#bkmk_ProfileXML)erstellt haben.

### Erstellen eines Pakets mit dem Skript für ProfileXML

1.  Hosten Sie das Skript VPN_Profile.ps1 auf einer Netzwerkfreigabe, die das Computerkonto der Site-Server zugreifen kann.

2.  Öffnen Sie in der Configuration Manager-Konsole **Software Library\\Application Management\\Packages**.

3.  Klicken Sie auf **Paket erstellen** , um das Paket erstellen und Programm-Assistenten zu starten, auf dem Menüband **Home** in der Gruppe **Erstellen** .

4.  Führen Sie auf der Seite "Paket" die folgenden Schritte aus:

    a. Geben Sie den **Namen** **Windows 10 immer auf VPN-Profil**.

    b. Aktivieren Sie das Kontrollkästchen **Dieses Paket enthält Quelldateien** , und klicken Sie auf **Durchsuchen**.

    c. Klicken Sie in das Dialogfeld Quellordner festlegen auf **Durchsuchen**, wählen Sie die Dateifreigabe mit VPN_Profile.ps1 und klicken Sie auf **OK**.<p>Stellen Sie sicher, dass Sie einen Netzwerkpfad, nicht auf einen lokalen Pfad auswählen. Anders ausgedrückt, sollte der Pfad etwa *\\fileserver\\vpnscript*, nicht *c:\\vpnscript*sein.

1.  Klicken Sie auf **Weiter**.

2.  Klicken Sie auf der Seite Programmtyp auf **Weiter**.

3.  Führen Sie auf der Seite "Standardprogramm" die folgenden Schritte aus:

    a.  Geben Sie den **Namen** **VPN-Profilskript**.

    b.  Geben Sie in der **Befehlszeile**, **PowerShell.exe - ExecutionPolicy umgehen - Datei "VPN_Profile.ps1"**.

    c.  Klicken Sie im **Ausführungsmodus**auf **mit Administratorrechten ausführen**.

    d.  Klicken Sie auf **Weiter**.

4.  Führen Sie auf der Seite "Anforderungen" die folgenden Schritte aus:

    a.  Wählen Sie **das Programm kann nur auf angegebenen Plattformen ausgeführt**.

    b.  Wählen Sie die Kontrollkästchen **Alle Windows 10 (32-Bit)** und **Alle Windows 10 (64-Bit)** .

    c.  Geben Sie im **geschätzte Speicherplatz**- **1**.

    d.  Geben Sie die **maximal zulässige Laufzeit (Minuten)** **15**.

    e.  Klicken Sie auf **Weiter**.

5.  Klicken Sie auf der Seite "Zusammenfassung" auf " **Weiter**".

6.  Klicken Sie auf der Seite Fertigstellung auf **Schließen**.

Mit dem Paket und Programm erstellt haben müssen Sie es für die **VPN-Benutzer** -Gruppe bereitstellen möchten.

### Das Skript für ProfileXML bereitstellen

1.  Öffnen Sie in der Configuration Manager-Konsole Software Library\\Application Management\\Packages.

2.  **Pakete**klicken Sie auf **Windows 10 immer auf VPN-Profil**.

3.  Auf der Registerkarte " **Programme** " am unteren Rand im Detailbereich mit der rechten Maustaste **VPN-Profilskript**, klicken Sie auf **Eigenschaften**und führen Sie die folgenden Schritte aus:

    a.  Klicken Sie auf der Registerkarte " **Erweitert** ", **Wenn dieses Programm auf einem Computer zugewiesen wird** **einmal für jeden Benutzer, die Benutzer sich anmeldet**.

    b.  Klicken Sie auf **OK**.

4.  Mit der rechten Maustaste **VPN-Profilskript** , und klicken Sie auf **Bereitstellen** , um den Assistenten zum Bereitstellen von Software starten.

5.  Führen Sie auf der Seite "Allgemein" die folgenden Schritte aus:

    a.  Neben der **Auflistung**klicken Sie auf " **Durchsuchen**".

    b.  Klicken Sie in der Liste **Sammlungstypen** (oben links) auf **Benutzer Sammlungen**.

    c.  Klicken Sie auf **VPN-Benutzer**, und klicken Sie auf **OK**.

    d.  Klicken Sie auf **Weiter**.

6.  Führen Sie auf der Seite Inhalt die folgenden Schritte aus:

    a.  Klicken Sie auf **Hinzufügen**, und klicken Sie auf **Verteilungspunkt**.

    b.  Wählen Sie im **verfügbaren Verteilungspunkte**die Verteilungspunkte für die Verteilung des ProfileXML Skripts, und klicken Sie auf **OK**werden soll.

    c.  Klicken Sie auf **Weiter**.

7.  Klicken Sie auf " **Weiter**" auf der Einstellungsseite Bereitstellung.

8.  Führen Sie auf der Seite Planung die folgenden Schritte aus:

    a.  Klicken Sie auf **neu** , um das Dialogfeld Zuweisungszeitplan zu öffnen.

    b.  Klicken Sie auf **direkt nach diesem Ereignis zuweisen**, und klicken Sie auf **OK**.

    c.  Klicken Sie auf **Weiter**.

9.  Führen Sie auf der Seite "Installationsoptionen" die folgenden Schritte aus:

    1.  Aktivieren Sie das Kontrollkästchen für die **Softwareinstallation** .

    2.  Klicken Sie auf **Zusammenfassung**.

10. Klicken Sie auf der Seite "Zusammenfassung" auf " **Weiter**".

11. Klicken Sie auf der Seite Fertigstellung auf **Schließen**.

Melden Sie mit der ProfileXML-Konfigurationsskript bereitgestellt sich auf einem Windows 10-Clientcomputer mit dem Benutzerkonto, die, das Sie ausgewählt, wenn Sie die Auflistung erstellt. Überprüfen Sie die Konfiguration des VPN-Clients.

>[!NOTE]
>Das Skript VPN_Profile.ps1 funktioniert nicht in einer Remotedesktop-Sitzung. Ebenso funktioniert es nicht in einer Hyper-V-erweiterte Sitzung. Wenn Sie eine Remote Access Always On VPN auf virtuellen Computern testen, deaktivieren Sie erweiterte Sitzung auf Ihrem Client VMs, bevor Sie fortfahren.

### Überprüfen Sie die Konfiguration des VPN-Clients

1.  Klicken Sie in der Systemsteuerung unter **System\\Security**, **Konfigurations-Manager**aus. 

2.  Führen Sie im Dialogfeld Configuration Manager-Eigenschaften auf der Registerkarte " **Aktionen** " die folgenden Schritte aus:

    a.  Klicken Sie auf **Computerrichtlinienabruf & Evaluierungszyklus**, klicken Sie auf **Jetzt ausführen**, und klicken Sie auf **OK**.

    b.  Klicken Sie auf **Benutzer Richtlinienabruf & Evaluierungszyklus**, klicken Sie auf **Jetzt ausführen**, und klicken Sie auf **OK**.

    c.  Klicken Sie auf **OK**.

3.  Schließen Sie die Systemsteuerung.

Das neue VPN-Profil sollte kurz angezeigt werden.

## Konfigurieren des VPN-Clients mithilfe von Intune

Um Intune verwenden, um Windows 10 Remote Access Always On VPN-Profile bereitzustellen, können Sie können den ProfileXML CSP-Knoten über das VPN-Profil, die, das Sie im Abschnitt [Erstellen Sie die ProfileXML-Konfigurationsdateien](#bkmk_ProfileXML)erstellt, konfigurieren, oder Sie das bereitgestellte base EAP-XML-Beispiel unten.

>[!NOTE]
>Intune verwendet nun Azure AD-Gruppen. Wenn Azure AD Connect die VPN-Benutzergruppe von einer lokalen Azure AD synchronisiert und Benutzer werden die VPN-Benutzer-Gruppe zugewiesen, sind Sie bereit sind, fahren Sie fort.

Erstellen Sie die VPN-Konfiguration für Informationen zum Konfigurieren der Windows 10-Clientcomputern für alle Benutzer zur Gruppe hinzugefügt. Da die Vorlage Intune VPN-Parameter enthält, nur kopieren Sie den \<EapHostConfig> \</EapHostConfig> Teil der VPN_ProfileXML-Datei. 


### Erstellen Sie die Richtlinie Always On VPN-Konfiguration

1.  Melden Sie sich im [Azure-Portal](https://portal.azure.com/).

2.  Wechseln Sie zu **Intune** > **Gerätekonfiguration** > **Profile**.

3.  Klicken Sie auf **Profil erstellen** , um das Profil erstellen Assistenten zu starten.

4.  Geben Sie einen **Namen** für das VPN-Profil und (optional) eine Beschreibung ein.

5.   Wählen Sie **Windows 10 oder höher**unter **Plattform**und wählen Sie das Profil Dropdownliste **VPN** .

     >[!TIP]
     >Wenn Sie eine benutzerdefinierte VPN-ProfileXML erstellen, finden Sie unter [Anwenden von ProfileXML mithilfe von Intune](https://docs.microsoft.com/windows/security/identity-protection/vpn/vpn-profile-options#apply-profilexml-using-intune) die Anweisungen.

6. Überprüfen Sie unter der Registerkarte **Base VPN** , oder legen Sie die folgenden Einstellungen:

    - **Name der Verbindung:** Geben Sie den Namen der VPN-Verbindung, wie er auf dem Clientcomputer in der **VPN** -Registerkarte unter **Einstellungen**, z. B. _Contoso AutoVPN_angezeigt wird.  
    
    - **Server:** Fügen Sie einen oder mehrere VPN-Server, indem Sie auf **hinzufügen.**
    
    - **Beschreibung** und **IP-Adresse oder FQDN:** Geben Sie die Beschreibung und IP-Adresse oder FQDN des VPN-Servers. Diese Werte müssen mit den Antragstellernamen in der VPN-Server-Authentifizierungszertifikat angepasst werden. 
    
    - **Standard-Server:** Wenn dies der Standard-VPN-Server ist, auf **"true"** festgelegt. Auf diese Weise können diesem Server wie der Standardserver, den Geräte verwenden, um die Verbindung herzustellen. 
    
    - **Verbindungstyp:** Legen Sie auf **IKEv2**.  
    
    - **Always On:** Legen Sie auf das VPN automatisch bei der Anmeldung herstellen und bleiben, bis der Benutzer manuell getrennt **Aktivieren** .
    
    - **Speichern von Anmeldeinformationen bei jeder Anmeldung**: boolescher Wert ("true" oder "false") für das Zwischenspeichern von Anmeldeinformationen. Wenn auf "true" Anmeldeinformationen zwischengespeichert werden, wann immer möglich.

7.  Kopieren Sie die folgende XML-Zeichenfolge in einem Text-Editor:<p>
 
    [!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]
    <p>
    
    ```XML
    <EapHostConfig xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><EapMethod><Type xmlns="https://www.microsoft.com/provisioning/EapCommon">25</Type><VendorId xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorId><VendorType xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorType><AuthorId xmlns="https://www.microsoft.com/provisioning/EapCommon">0</AuthorId></EapMethod><Config xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><Eap xmlns="https://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>25</Type><EapType xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV1"><ServerValidation><DisableUserPromptForServerValidation>true</DisableUserPromptForServerValidation><ServerNames>NPS.contoso.com</ServerNames><TrustedRootCA>5a 89 fe cb 5b 49 a7 0b 1a 52 63 b7 35 ee d7 1c c2 68 be 4b </TrustedRootCA></ServerValidation><FastReconnect>true</FastReconnect><InnerEapOptional>false</InnerEapOptional><Eap xmlns="https://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>13</Type><EapType xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV1"><CredentialsSource><CertificateStore><SimpleCertSelection>true</SimpleCertSelection></CertificateStore></CredentialsSource><ServerValidation><DisableUserPromptForServerValidation>true</DisableUserPromptForServerValidation><ServerNames>NPS.contoso.com</ServerNames><TrustedRootCA>5a 89 fe cb 5b 49 a7 0b 1a 52 63 b7 35 ee d7 1c c2 68 be 4b </TrustedRootCA></ServerValidation><DifferentUsername>false</DifferentUsername><PerformServerValidation xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">true</AcceptServerName></EapType></Eap><EnableQuarantineChecks>false</EnableQuarantineChecks><RequireCryptoBinding>false</RequireCryptoBinding><PeapExtensions><PerformServerValidation xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2">true</AcceptServerName></PeapExtensions></EapType></Eap></Config></EapHostConfig>
    ```

8.  Ersetzen Sie die **\<TrustedRootCA>5a 89 Fe Cb 5 b 49 a7 0 b 1a 52 63 b7 35 Ee d7 1c c2 68 werden 4b<\/TrustedRootCA>** im Beispiel durch den Fingerabdruck des Zertifikats, der Ihre lokale Stammzertifizierungsstelle an beiden Stellen vorhanden.
  
    >[!Important]
    >Verwenden Sie nicht den Fingerabdruck Beispiel \<TrustedRootCA>\</TrustedRootCA> unten im Abschnitt.  Die TrustedRootCA muss der Fingerabdruck des Zertifikats der Stammzertifizierungsstelle für die lokale sein, die das Server-Authentifizierungszertifikat für RRAS und NPS-Servern ausgestellt. **Dies darf nicht das Cloud-Stammzertifikat, noch intermediate ausstellenden Zertifizierungsstelle den Fingerabdruck des Zertifikats**.

10. Ersetzen Sie die **\<ServerNames>NPS.contoso.com\</ServerNames>** im XML-Beispiel, mit dem vollqualifizierten Domänennamen der Domäne NPS, an dem Authentifizierung erfolgt. 

11. Kopieren Sie die überarbeitete XML-Zeichenfolge und fügen Sie in der **EAP-Xml** -Feld unter der Registerkarte "VPN-Basis", und klicken Sie auf **OK**.<p>Eine immer auf VPN-Gerätekonfiguration-Richtlinie mithilfe von EAP wird in Intune erstellt.


### Synchronisieren Sie die Richtlinie Always On VPN-Konfiguration mit Intune

Um die Konfigurationsrichtlinie zu testen, melden Sie sich an einem Windows 10-Clientcomputer, als des Benutzers, die, den Sie der Gruppe **Immer auf VPN-Benutzer** hinzugefügt, und dann mit Intune synchronisieren.

1.  **Klicken Sie auf das Menü "Start".**

2.  Klicken Sie unter "Einstellungen" auf **Konten**, und klicken Sie auf **Arbeits- oder schulkonto zugreifen**.

3.  Klicken Sie auf das MDM-Profil, und klicken Sie auf **Informationen**.

4.  Klicken Sie auf **Synchronisierung** um eine Auswertung von Intune-Richtlinien und Abruf zu erzwingen.

5.  Schließen Sie die Einstellungen. Nach der Synchronisierung sehen Sie das VPN-Profil verfügbar, auf dem Computer.

## Nächster Schritt
Bereitstellen von Always On VPN erfolgt.  Andere Features, die Sie konfigurieren können, finden Sie in der folgenden Tabelle:

|Wenn Sie möchten...  |Anzeige...  |
|---------|---------|
|Konfigurieren des bedingten Zugriffs für VPN    |[Schritt 7. (Optional) Konfigurieren des bedingten Zugriffs für VPN-Konnektivität mit Azure AD](../../ad-ca-vpn-connectivity-windows10.md): In diesem Schritt können Sie optimieren wie autorisierten VPN-Benutzerzugriff von Ressourcen mithilfe von [bedingtem Zugriff von Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). Mit Azure AD Bedingter Zugriff für virtuelles privates Netzwerk (VPN)-Konnektivität können Sie schützen die VPN-Verbindungen. Beim bedingten Zugriff handelt es sich um ein richtlinienbasiertes Auswertungsmodul, mit dem Sie Zugriffsregeln für alle mit Azure Active Directory (Azure AD) verknüpften Anwendungen erstellen können.         |
|Erfahren Sie mehr über die erweiterten VPN-features  |[Erweiterte VPN-Funktionen](always-on-vpn-adv-options.md#advanced-vpn-features): Diese Seite enthält Informationen zum Aktivieren der VPN-Datenverkehrsfilter, so konfigurieren Sie die automatische VPN-Verbindungen mit App-Triggern und so konfigurieren Sie NPS, damit nur VPN-Verbindungen von Clients mithilfe von Azure ausgestellte Zertifikate AD.        |


---
