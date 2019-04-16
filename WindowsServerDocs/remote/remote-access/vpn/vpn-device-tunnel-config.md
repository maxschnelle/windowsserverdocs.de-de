---
title: Konfigurieren des VPN-Tunnels Gerät in Windows 10
description: Erfahren Sie, wie Sie einen VPN-Gerätetunnel in Windows 10 erstellen.
ms.prod: windows-server-threshold
ms.date: 11/05/2018
ms.technology: networking-ras
ms.topic: article
ms.assetid: 158b7a62-2c52-448b-9467-c00d5018f65b
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: 005721873ad3a0df942bc9e23eba13728965ccba
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067311"
---
# Konfigurieren von VPN-Gerät Tunnel in Windows 10

>Gilt für: Windows 10 Version 1709

Always On VPN bietet Ihnen die Möglichkeit, eine dedizierte VPN-Profil für Computer oder Gerät zu erstellen. Always On VPN-Verbindungen sind zwei Arten von Tunneln: 

- _Gerätetunnelfunktion_ mit einem angegebenen VPN-Server vor dem Benutzer melden Sie sich auf dem Gerät verbunden. Mithilfe der gerätetunnelfunktion vor der Anmeldung konnektivitätsszenarien und Device Management Zwecke.

- _Benutzer Tunnel_ verbindet erst nach der Anmeldung eines Benutzers an das Gerät. Benutzer Tunnel ermöglicht Benutzern den Zugriff auf Unternehmensressourcen über VPN-Servern.

Im Gegensatz zu _Benutzer Tunnel_, der nur nach der Anmeldung eines Benutzers an das Gerät oder Computer verbunden ist, können _gerätetunnelfunktion_ VPN-Verbindung Verbindung herzustellen, bevor der Benutzer anmeldet. _Gerätetunnelfunktion_ und _Benutzer Tunnel_ funktionieren unabhängig mit ihrer VPN-Profile, zur gleichen Zeit verbunden werden können, und können je nach Bedarf andere Authentifizierungsmethoden zu verwenden und andere Einstellungen für die VPN-Konfiguration verwenden. Benutzer Tunnel unterstützt SSTP und IKEv2 und gerätetunnelfunktion IKEv2 nur mit keine Unterstützung für SSTP Fallback unterstützt.

Benutzer Tunnel wird auf unterstützt Domäne, keiner Domäne beigetreten sind (Arbeitsgruppe) oder Azure AD eingebundene Geräte sowohl für Unternehmens- und BYOD-Szenarien. Es ist in allen Windows-Editionen verfügbar, und die Plattformfeatures sind für Dritte über UWP VPN-Plug-in-Unterstützung verfügbar.

Gerätetunnelfunktion kann nur auf die Domäne eingebundene Geräte unter Windows 10 Enterprise oder Education Version 1709 oder höher konfiguriert werden. Es gibt keine Unterstützung für Drittanbieter-Kontrolle über den Gerätetunnel.


## Device Tunnel Anforderungen und Features
Sie müssen Computerzertifikatauthentifizierung für VPN-Verbindungen zu aktivieren und definieren eine Stammzertifizierungsstelle für die Authentifizierung von eingehender VPN-Verbindungen. 

```PowerShell
$VPNRootCertAuthority = “Common Name of trusted root certification authority”
$RootCACert = (Get-ChildItem -Path cert:LocalMachine\root | Where-Object {$_.Subject -Like “*$VPNRootCertAuthority*” })
Set-VpnAuthProtocol -UserAuthProtocolAccepted Certificate, EAP -RootCertificateNameToAccept $RootCACert -PassThru
```

![Device Tunnel-Funktionen und Anforderungen](../../media/device-tunnel-feature-and-requirements.png)

## VPN-Tunnels Gerätekonfiguration

Das Beispiel für ein Profil, die unten stehenden Hinweise gut für Szenarien, in denen nur Client zieht initiiert, werden über den Gerätetunnel benötigt.  Datenverkehrsfilter werden genutzt, um den Gerätetunnel nur Management-Datenverkehr zu minimieren.  Diese Konfiguration eignet sich gut für Windows Update, typisch Group Policy (GP) und System Center Configuration Manager (SCCM) Updateszenarien als auch VPN-Konnektivität für die erste Anmeldung ohne zwischengespeicherte Anmeldeinformationen oder Kennwort zurücksetzen Szenarien. 

Server-initiierte Push in Fällen, z. B. Windows-Remoteverwaltung (WinRM) Remote GPUpdate und remote SCCM-Aktualisierungsszenarios – müssen Sie eingehenden Datenverkehr auf den Gerätetunnel zulassen, sodass Datenverkehrsfilter verwendet werden können.  Wenn im Gerät Tunnel Profil Sie Datenverkehrsfilter aktivieren, wird den Gerätetunnel eingehenden Datenverkehr verweigert.  Diese Einschränkung wird nicht in künftigen Versionen entfernt werden.


### Beispiel für VPN-profileXML

Im folgenden sehen die Beispiel-VPN-ProfileXML.

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

Je nach jedem Szenario bestimmte Bereitstellung ist eine andere VPN-Feature, das mit den Gerätetunnel konfiguriert werden kann [Trusted Network Detection](https://social.technet.microsoft.com/wiki/contents/articles/38546.new-features-for-vpn-in-windows-10-and-windows-server-2016.aspx#Trusted_Network_Detection).

```
 <!-- inside/outside detection --> 
  <TrustedNetworkDetection>corp.contoso.com</TrustedNetworkDetection> 
```

## Bereitstellung und testen

Sie können Device Tunnel konfigurieren, verwenden ein Windows PowerShell-Skript, und mithilfe der Windows-Verwaltungsinstrumentation \(WMI\)-Brücke. Die Always On VPN-gerätetunnelfunktion muss im Kontext des **Lokalen** Systemkontos konfiguriert werden. Um dies zu erreichen, werden muss [PsExec](https://docs.microsoft.com/sysinternals/downloads/psexec), eines der [PsTools](https://docs.microsoft.com/sysinternals/downloads/pstools) enthalten in der [Sysinternals](https://docs.microsoft.com/sysinternals/) -Suite mit Hilfsprogrammen verwendet.

Richtlinien zur Bereitstellung einer pro Gerät `(.\Device)` im Vergleich zu einer pro Benutzer `(.\User)` Profil, finden Sie unter [Verwendung von PowerShell-Skripterstellung mit der WMI-Bridge-Anbieter](https://docs.microsoft.com/windows/client-management/mdm/using-powershell-scripting-with-the-wmi-bridge-provider). 

Führen Sie den folgenden Windows PowerShell-Befehl zu überprüfen, ob Sie ein Geräteprofil erfolgreich bereitgestellt haben:

    `Get-VpnConnection -AllUserConnection`

Die Ausgabe zeigt eine Liste der Device\-weiten VPN-Profile, die bereitgestellt werden, auf dem Gerät.


### Beispielskript für Windows PowerShell

Sie können das folgende Windows PowerShell-Skript, beim Erstellen Ihrer eigenen Skripts für profilerstellung verwenden.

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

## Weitere Ressourcen

Im folgenden werden weitere Ressourcen zur Unterstützung bei der VPN-Bereitstellung.

### VPN-Client-Konfigurationsressourcen

Hierbei handelt es sich um VPN-Client-Konfigurationsressourcen.

- [So erstellen Sie VPN-Profile in System Center Configuration Manager](https://docs.microsoft.com/sccm/protect/deploy-use/create-vpn-profiles)
- [Konfigurieren von Windows 10-Client immer auf VPN-Verbindungen](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)
- [VPN-Profiloptionen](https://docs.microsoft.com/windows/access-protection/vpn/vpn-profile-options)

### Remote Access-Server \(RAS\) Gateway-Ressourcen

Im folgenden werden RAS-Gateway-Ressourcen.

- [Konfigurieren von RRAS mit einem Computer-Authentifizierungszertifikat](https://technet.microsoft.com/library/dd458982.aspx)
- [Problembehandlung für IKEv2-VPN-Verbindungen](https://technet.microsoft.com/library/dd941612.aspx)
- [Konfigurieren des Remotezugriffs IKEv2-basierte](https://technet.microsoft.com/library/ff687731.aspx)

>[!IMPORTANT]
>Wenn Gerätetunnelfunktion mit einem Microsoft RAS-Gateway zu verwenden, müssen Sie zum Konfigurieren des RRAS-Servers zur Unterstützung von IKEv2 Computerzertifikatauthentifizierung durch Aktivieren der **Zulassen Computerzertifikatauthentifizierung für IKEv2** -Authentifizierungsmethode wie beschrieben [hier](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee922682%28v=ws.10%29). Sobald diese Einstellung aktiviert ist, wird empfohlen, dass das **Satz-VpnAuthProtocol** PowerShell-Cmdlet, zusammen mit dem optionalen Parameter **RootCertificateNameToAccept** verwendet wird, um sicherzustellen, dass nur IKEv2 RRAS-Verbindungen zulässig ist VPN-Client Zertifikate auf einer definierten interne/Private Stammzertifizierungsstelle. Alternativ sollte der **Vertrauenswürdige Stammzertifizierungsstellen** -Store auf dem RRAS-Server geändert werden, um sicherzustellen, dass es keine öffentlichen Zertifizierungsstellen wie erwähnt [hier](https://blogs.technet.microsoft.com/rrasblog/2009/06/10/what-type-of-certificate-to-install-on-the-vpn-server/)enthält. Ähnliche Methoden müssen möglicherweise auch für andere VPN-Gateways berücksichtigt werden.

---
