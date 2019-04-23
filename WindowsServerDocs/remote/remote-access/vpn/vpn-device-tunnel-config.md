---
title: Konfigurieren des VPN-Gerät-Tunnels unter Windows 10
description: Erfahren Sie, wie Sie einen VPN-Gerät-Tunnel in Windows 10 zu erstellen.
ms.prod: windows-server-threshold
ms.date: 11/05/2018
ms.technology: networking-ras
ms.topic: article
ms.assetid: 158b7a62-2c52-448b-9467-c00d5018f65b
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: 005721873ad3a0df942bc9e23eba13728965ccba
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864551"
---
# <a name="configure-vpn-device-tunnels-in-windows-10"></a>Konfigurieren von VPN-Gerät-Tunnel unter Windows 10

>Gilt für: Windows 10, Version 1709

Always On-VPN-bietet Ihnen die Möglichkeit, ein dediziertes VPN-Profil für das Gerät oder Computer zu erstellen. Always On-VPN-Verbindungen sind zwei Typen der Tunnel an: 

- _Gerät Tunnel_ eine Verbindung mit der angegebenen VPN-Server vor dem Benutzer, melden Sie sich bei dem Gerät her. Verwenden Gerät-Tunnel, vor der Anmeldung konnektivitätsszenarien und geräteverwaltung.

- _Benutzer-Tunnel_ erst nach der Anmeldung eines Benutzers an das Gerät verbindet. Benutzer-Tunnel ermöglicht Zugriff auf Organisationsressourcen über VPN-Server.

Im Gegensatz zu _Benutzer Tunnel_, die nur eine Verbindung herstellt, nach der Anmeldung eines Benutzers an das Gerät oder Computer _Gerät Tunnel_ können Sie das VPN, eine Verbindung herzustellen, bevor der Benutzer anmeldet. Beide _Gerät Tunnel_ und _Benutzer Tunnel_ aber unabhängig voneinander mit ihrer VPN-Profilen, können gleichzeitig verbunden sein und können verschiedene Authentifizierungsmethoden und andere VPN-Konfigurationseinstellungen Je nach Bedarf. Benutzer-Tunnel unterstützt SSTP und IKEv2 und Gerät Tunnel unterstützt IKEv2, nur mit keine Unterstützung für SSTP-Fallback.

Benutzer Tunnel wird unterstützt, in Domäne eingebunden, (nicht-Domänenkonto eingebunden, Arbeitsgruppe) oder Azure AD – eingebundenen Geräten sowohl für Unternehmen als auch für BYOD-Szenarien ermöglichen. Es ist in allen Editionen von Windows verfügbar, und die Plattformfunktionen sind an Drittanbieter über UWP VPN-Plug-in Support verfügbar.

Gerät-Tunnel kann nur auf die Domäne eingebundene Geräte, die Ausführung von Windows 10 Enterprise oder Bildungseinrichtungen Version 1709 oder höher konfiguriert werden. Es gibt keine Unterstützung für Drittanbieter-Steuerelement des Tunnels, der Geräte.


## <a name="device-tunnel-requirements-and-features"></a>Anforderungen an die Geräte-Tunnel und Features
Sie müssen Aktivieren der Computerzertifikatauthentifizierung für VPN-Verbindungen und Definieren von einer Stammzertifizierungsstelle für die Authentifizierung eingehender VPN-Verbindungen. 

```PowerShell
$VPNRootCertAuthority = “Common Name of trusted root certification authority”
$RootCACert = (Get-ChildItem -Path cert:LocalMachine\root | Where-Object {$_.Subject -Like “*$VPNRootCertAuthority*” })
Set-VpnAuthProtocol -UserAuthProtocolAccepted Certificate, EAP -RootCertificateNameToAccept $RootCACert -PassThru
```

![Gerät-Tunnel-Funktionen und Anforderungen](../../media/device-tunnel-feature-and-requirements.png)

## <a name="vpn-device-tunnel-configuration"></a>VPN-Tunnel Gerätekonfiguration

Das Beispiel-Profil, die unten stehenden Anleitungen gut für Szenarien, in dem nur Client Pullvorgänge initiiert, durch den Tunnel Gerät erforderlich sind.  Die Datenverkehrsfilter werden genutzt, um den Geräte-Tunnel auf nur Verwaltungsdatenverkehr zu beschränken.  Diese Konfiguration eignet sich gut für Windows zu aktualisieren, typische Group Policy (GP) und Aktualisierungsszenarien für System Center Configuration Manager (SCCM), sowie VPN-Konnektivität für die erste Anmeldung ohne zwischengespeicherte Anmeldeinformationen und Szenarien für die kennwortzurücksetzung. 

Für serverseitig initiierte Push-Fällen, z. B. Windows-Remoteverwaltung (WinRM), Remote-Gruppenrichtlinienaktualisierung und remote Szenarien für die SCCM-Update – müssen Sie eingehenden Datenverkehr auf der Gerät-Tunnel, zulassen, sodass die Datenverkehrsfilter, die verwendet werden können.  Wenn im Tunnel Geräteprofil, die, das Sie die Datenverkehrsfilter aktivieren, klicken Sie dann den Geräte-Tunnel eingehenden Datenverkehr verweigert wird.  Diese Einschränkung soll in zukünftigen Versionen entfernt werden soll.


### <a name="sample-vpn-profilexml"></a>Beispiel-VPN-"profileXML"

Es folgt die Beispiel-VPN-"profileXML".

``` xml
<VPNProfile>  
  <NativeProfile>  
<Servers>vpn.contoso.com</Servers>  
<NativeProtocolType>IKEv2</NativeProtocolType>  
<Authentication>  
  <MachineMethod>Certificate</MachineMethod>  
</Authentication>  
<RoutingPolicyType>SplitTunnel</RoutingPolicyType>  
 <!-- disable the addition of a class based route for the assigned IP address on the VPN interface -->
<DisableClassBasedDefaultRoute>true</DisableClassBasedDefaultRoute>  
  </NativeProfile> 
  <!-- use host routes(/32) to prevent routing conflicts -->  
  <Route>  
<Address>10.10.0.2</Address>  
<PrefixSize>32</PrefixSize>  
  </Route>  
  <Route>  
<Address>10.10.0.3</Address>  
<PrefixSize>32</PrefixSize>  
  </Route>  
<!-- traffic filters for the routes specified above so that only this traffic can go over the device tunnel --> 
  <TrafficFilter>  
<RemoteAddressRanges>10.10.0.2, 10.10.0.3</RemoteAddressRanges>  
  </TrafficFilter>
<!-- need to specify always on = true --> 
  <AlwaysOn>true</AlwaysOn> 
<!-- new node to specify that this is a device tunnel -->  
 <DeviceTunnel>true</DeviceTunnel>
<!--new node to register client IP address in DNS to enable manage out -->
<RegisterDNS>true</RegisterDNS>
</VPNProfile>
```

Je nach den Anforderungen der einzelnen bestimmten Bereitstellungsszenarien, eine weitere VPN-Funktion, die mit dem Gerät Tunnel konfiguriert werden kann ist [Erkennung für vertrauenswürdige Netzwerke](https://social.technet.microsoft.com/wiki/contents/articles/38546.new-features-for-vpn-in-windows-10-and-windows-server-2016.aspx#Trusted_Network_Detection).

```
 <!-- inside/outside detection --> 
  <TrustedNetworkDetection>corp.contoso.com</TrustedNetworkDetection> 
```

## <a name="deployment-and-testing"></a>Bereitstellen und testen

Sie können die Gerät-Tunnel konfigurieren, mit einem Windows PowerShell-Skript und die Windows-Verwaltungsinstrumentierung \(WMI\) Bridge. Der Always On-VPN-Gerät-Tunnel muss konfiguriert werden, im Rahmen der **lokales SYSTEM** Konto. Um dies zu erreichen, es wird erforderlich sein, verwenden Sie [PsExec](https://docs.microsoft.com/sysinternals/downloads/psexec)möglich von der [PsTools](https://docs.microsoft.com/sysinternals/downloads/pstools) in enthalten die [Sysinternals](https://docs.microsoft.com/sysinternals/) Sammlung von Hilfsprogrammen.

Richtlinien zum Bereitstellen einer pro Gerät `(.\Device)` im Vergleich zu einer pro Benutzer `(.\User)` möchten, finden Sie unter [mithilfe von PowerShell-Skripts mit dem WMI-Anbieter Bridge](https://docs.microsoft.com/windows/client-management/mdm/using-powershell-scripting-with-the-wmi-bridge-provider). 

Führen Sie den folgenden Windows PowerShell-Befehl, um sicherzustellen, dass Sie ein Geräteprofil erfolgreich bereitgestellt haben:

    `Get-VpnConnection -AllUserConnection`

Die Ausgabe zeigt eine Liste des Geräts\-wide VPN-Profile, die auf dem Gerät bereitgestellt werden.


### <a name="example-windows-powershell-script"></a>Windows PowerShell-Beispielskript

Sie können das folgende Windows PowerShell-Skript, beim Erstellen Ihres eigenen Skripts für die profilerstellung verwenden.

```PowerShell
Param(
[string]$xmlFilePath,
[string]$ProfileName
)

$a = Test-Path $xmlFilePath
echo $a

$ProfileXML = Get-Content $xmlFilePath

echo $XML

$ProfileNameEscaped = $ProfileName -replace ' ', '%20'

$Version = 201606090004

$ProfileXML = $ProfileXML -replace '<', '&lt;'
$ProfileXML = $ProfileXML -replace '>', '&gt;'
$ProfileXML = $ProfileXML -replace '"', '&quot;'

$nodeCSPURI = './Vendor/MSFT/VPNv2'
$namespaceName = "root\cimv2\mdm\dmmap"
$className = "MDM_VPNv2_01"

$session = New-CimSession

try
{
$newInstance = New-Object Microsoft.Management.Infrastructure.CimInstance $className, $namespaceName
$property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ParentID", "$nodeCSPURI", 'String', 'Key')
$newInstance.CimInstanceProperties.Add($property)
$property = [Microsoft.Management.Infrastructure.CimProperty]::Create("InstanceID", "$ProfileNameEscaped", 'String', 'Key')
$newInstance.CimInstanceProperties.Add($property)
$property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ProfileXML", "$ProfileXML", 'String', 'Property')
$newInstance.CimInstanceProperties.Add($property)

$session.CreateInstance($namespaceName, $newInstance)
$Message = "Created $ProfileName profile."
Write-Host "$Message"
}
catch [Exception]
{
$Message = "Unable to create $ProfileName profile: $_"
Write-Host "$Message"
exit
}
$Message = "Complete."
Write-Host "$Message"
```

## <a name="additional-resources"></a>Zusätzliche Ressourcen

Folgendes sind zusätzliche Ressourcen zur Unterstützung bei der VPN-Bereitstellung.

### <a name="vpn-client-configuration-resources"></a>VPN-Client-Ressourcen

Hierbei handelt es sich um VPN-Client-Ressourcen.

- [Erstellen von VPN-Profilen in System Center Configuration Manager](https://docs.microsoft.com/sccm/protect/deploy-use/create-vpn-profiles)
- [Konfigurieren Sie Windows 10-Clientsysteme Always On-VPN-Verbindungen](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)
- [VPN-Profil-Optionen](https://docs.microsoft.com/windows/access-protection/vpn/vpn-profile-options)

### <a name="remote-access-server-ras-gateway-resources"></a>RAS-Server \(RAS\) Gateway-Ressourcen

Nachfolgend sind RAS-Gateway-Ressourcen.

- [Konfigurieren von RRAS mit einem Computerauthentifizierungszertifikat](https://technet.microsoft.com/library/dd458982.aspx)
- [Problembehandlung für IKEv2-VPN-Verbindungen](https://technet.microsoft.com/library/dd941612.aspx)
- [Konfigurieren des Remotezugriffs IKEv2-basierten](https://technet.microsoft.com/library/ff687731.aspx)

>[!IMPORTANT]
>Wenn Gerät-Tunnel mit einem Microsoft RAS-Gateway verwenden, müssen Sie so konfigurieren Sie den RRAS-Server zur Unterstützung von IKEv2-Computerzertifikatauthentifizierung durch Aktivieren der **zulassen-Computerzertifikatauthentifizierung für IKEv2** Authentifizierungsmethode beschriebenen [hier](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee922682%28v=ws.10%29). Wenn diese Einstellung aktiviert ist, es wird dringend empfohlen, die die **Set-VpnAuthProtocol** PowerShell-Cmdlet zusammen mit den **RootCertificateNameToAccept** Optionaler Parameter wird verwendet, um sicherzustellen, dass RRAS-IKEv2-Verbindungen sind nur für VPN-Clientzertifikate dieser Kette zu einem explizit definierten internen/privaten Stammzertifikate von Zertifizierungsstellen zulässig. Sie können auch die **Trusted Root Certification Authorities** Speicher auf dem RRAS-Server sollte geändert werden, um sicherzustellen, dass es keine öffentlichen Zertifizierungsstellen enthält wie bereits erwähnt [hier](https://blogs.technet.microsoft.com/rrasblog/2009/06/10/what-type-of-certificate-to-install-on-the-vpn-server/). Ähnliche Methoden müssen möglicherweise auch für andere VPN-Gateways berücksichtigt werden.

---
