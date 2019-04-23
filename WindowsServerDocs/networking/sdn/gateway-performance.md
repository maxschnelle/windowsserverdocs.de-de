---
title: Windows Server 2019 Gateway-Leistung
description: ''
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.date: 08/22/2018
ms.openlocfilehash: a6530b29ce7ffb0d18e0266e70cb2ca45188915c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845631"
---
# <a name="windows-server-2019-gateway-performance"></a>Windows Server 2019 Gateway-Leistung

>Gilt für: Windows Server


In Windows Server 2016 wurde eine der Kunden sorgen die Unfähigkeit des SDN-Gateway auf die Durchsatz-Anforderungen von modernen Netzwerken. Der Netzwerkdurchsatz der IPSec- und GRE-Tunnel mussten Einschränkungen im Zusammenhang mit den einzelnen Verbindung-Durchsatz für IPsec-Verbindungen, die über 300 Mbit/s wird und für die GRE-Konnektivität wird ungefähr 2,5 Gbit/s an.

Wir haben erheblich in Windows Server-2019, mit der schnell wachsenden 15 Gbit/s für IPSec- und GRE-Verbindungen zu 1,8 Gbit/s bzw. verbessert. All dies, mit deutlichen in die CPU-Zyklen / pro Byte, wodurch äußerst leistungsfähige Durchsatz mit deutlich weniger CPU-Auslastung.

## <a name="enable-high-performance-with-gateways-in-windows-server-2019"></a>Ermöglichen einer hohen Leistung von Gateways in Windows Server-2019

Für **GRE-Verbindungen**, sobald Sie bereitstellen bzw. 2019 für Windows Server-Builds auf den Gateway-VMs mit dem Upgrade, sollten Sie automatisch die verbesserte Leistung angezeigt. Keine manuellen Schritte sind erforderlich.

Für **IPsec-Verbindungen**, bei der Erstellung der Verbindungs für Ihren virtuellen Netzwerken erhalten Sie standardmäßig die Windows Server 2016-Data-Pfad und die Leistung Zahlen. Führen Sie folgende Schritte aus, um der Windows Server-2019 Datenpfad zu aktivieren:

   1. Wechseln Sie in einer SDN-Gateway-VM, zur **Services** Konsole ("Services.msc").
   2. Suchen Sie den Dienst, mit dem Namen **Azure-Gatewaydienst**, und legen Sie den Starttyp auf **automatische**.
   3. Starten Sie die Gateway-VM neu.
      Die aktiven Verbindungen für dieses gatewayfailover auf einen redundanten Gateway-VM.
   4. Wiederholen Sie die vorherigen Schritte für die restlichen den Gateway-VMs.

>[!TIP]
>Für optimale Leistung zu erzielen, sicherstellen, dass die CipherTransformationConstant und AuthenticationTransformConstant in QuickMode-Einstellungen von der IPSec-Verbindung verwendet das **GCMAES256** Verschlüsselungssammlung.
>
>Für maximale Leistung muss es sich bei die Gateway-Hosthardware AES-NI und PCLMULQDQ CPU-Befehlssätze unterstützen. Diese werden für alle Westmere (32nm) und höher Intel-CPU mit Ausnahme von auf Modellen, in dem AES-NI deaktiviert wurde. Sehen Sie sich der Herstellerdokumentation Hardware, um festzustellen, ob die CPU unterstützt die AES-NI und PCLMULQDQ CPU-Anweisung legt diese fest.

Im folgenden sehen Sie ein Beispiel für REST-IPsec-Verbindung mit Algorithmen für optimale Sicherheit:

```PowerShell
# NOTE: The virtual gateway must be created before creating the IPsec connection. More details here.
# Create a new object for Tenant Network IPsec Connection  
$nwConnectionProperties = New-Object Microsoft.Windows.NetworkController.NetworkConnectionProperties   

# Update the common object properties  
$nwConnectionProperties.ConnectionType = "IPSec"   
$nwConnectionProperties.OutboundKiloBitsPerSecond = 2000000   
$nwConnectionProperties.InboundKiloBitsPerSecond = 2000000  

# Update specific properties depending on the Connection Type  
$nwConnectionProperties.IpSecConfiguration = New-Object Microsoft.Windows.NetworkController.IpSecConfiguration   
$nwConnectionProperties.IpSecConfiguration.AuthenticationMethod = "PSK"   
$nwConnectionProperties.IpSecConfiguration.SharedSecret = "111_aaa"   

$nwConnectionProperties.IpSecConfiguration.QuickMode = New-Object Microsoft.Windows.NetworkController.QuickMode   
$nwConnectionProperties.IpSecConfiguration.QuickMode.PerfectForwardSecrecy = "PFS2048"   
$nwConnectionProperties.IpSecConfiguration.QuickMode.AuthenticationTransformationConstant = "GCMAES256"   
$nwConnectionProperties.IpSecConfiguration.QuickMode.CipherTransformationConstant = "GCMAES256"   
$nwConnectionProperties.IpSecConfiguration.QuickMode.SALifeTimeSeconds = 3600   
$nwConnectionProperties.IpSecConfiguration.QuickMode.IdleDisconnectSeconds = 500   
$nwConnectionProperties.IpSecConfiguration.QuickMode.SALifeTimeKiloBytes = 2000   

$nwConnectionProperties.IpSecConfiguration.MainMode = New-Object Microsoft.Windows.NetworkController.MainMode   
$nwConnectionProperties.IpSecConfiguration.MainMode.DiffieHellmanGroup = "Group2"   
$nwConnectionProperties.IpSecConfiguration.MainMode.IntegrityAlgorithm = "SHA256"   
$nwConnectionProperties.IpSecConfiguration.MainMode.EncryptionAlgorithm = "AES256"   
$nwConnectionProperties.IpSecConfiguration.MainMode.SALifeTimeSeconds = 28800
$nwConnectionProperties.IpSecConfiguration.MainMode.SALifeTimeKiloBytes = 2000   

# L3 specific configuration (leave blank for IPSec)  
$nwConnectionProperties.IPAddresses = @()   
$nwConnectionProperties.PeerIPAddresses = @()   

# Update the IPv4 Routes that are reachable over the site-to-site VPN Tunnel  
$nwConnectionProperties.Routes = @()   
$ipv4Route = New-Object Microsoft.Windows.NetworkController.RouteInfo   
$ipv4Route.DestinationPrefix = "<<On premise subnet that must be reachable over the VPN tunnel. Ex: 10.0.0.0/24>>"   
$ipv4Route.metric = 10   
$nwConnectionProperties.Routes += $ipv4Route   

# Tunnel Destination (Remote Endpoint) Address  
$nwConnectionProperties.DestinationIPAddress = "<<Public IP address of the On-Premise VPN gateway. Ex: 192.168.3.4>>"   

# Add the new Network Connection for the tenant. Note that the virtual gateway must be created before creating the IPsec connection. $uri is the REST URI of your deployment and must be in the form of “https://<REST URI>”  
New-NetworkControllerVirtualGatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId $virtualGW.ResourceId -ResourceId "Contoso_IPSecGW" -Properties $nwConnectionProperties -Force
```

## <a name="testing-results"></a>Testergebnisse

Wir haben umfangreiche Leistungstests für SDN-Gateways in unseren Testlabors durchgeführt. In den Tests haben wir Gateway Leistung des Netzwerks mit Windows Server-2019 in SDN und nicht-SDN-Szenarien verglichen. Sie finden Sie die Ergebnisse und erfasst im Blogartikel Einstellungsdetails testen [hier](https://blogs.technet.microsoft.com/networking/2018/08/15/high-performance-gateways/).

---