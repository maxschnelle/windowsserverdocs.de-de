---
title: Windows Server 2019-Gatewayleistung
description: ''
manager: dougkim
ms.prod: windows-server
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: ''
ms.author: lizross
author: eross-msft
ms.date: 08/22/2018
ms.openlocfilehash: e8cdf4e100c65fae11637c681924746115444f71
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80313022"
---
# <a name="windows-server-2019-gateway-performance"></a>Windows Server 2019-Gatewayleistung

>Gilt für: Windows Server


In Windows Server 2016 war eines der Kunden Bedenken, dass das Sdn-Gateway die Durchsatzanforderungen moderner Netzwerke nicht erfüllen konnte. Der Netzwerk Durchsatz der IPSec-und GRE-Tunnel wies Beschränkungen mit dem einzelnen Verbindungs Durchsatz für IPSec-Konnektivität von etwa 300 Mbit/s und für GRE-Konnektivität etwa 2,5 Gbit/s auf.

Wir haben sich in Windows Server 2019 erheblich verbessert, wobei die Zahlen auf 1,8 Gbit/s und 15 Gbit/s für IPSec-bzw. gre-Verbindungen steigen. All dies mit erheblichen Reduzierungen in den CPU-Zyklen pro Byte, wodurch ein extrem leistungsstarker Durchsatz mit einer deutlich geringeren CPU-Auslastung erzielt wird.

## <a name="enable-high-performance-with-gateways-in-windows-server-2019"></a>Aktivieren der hohen Leistung mit Gateways in Windows Server 2019

Bei **GRE-Verbindungen**sollte die verbesserte Leistung automatisch angezeigt werden, sobald Sie Windows Server 2019-Builds auf den Gateway-VMS bereitstellen bzw. ein Upgrade darauf durchführen. Es sind keine manuellen Schritte erforderlich.

Bei **IPSec-Verbindungen**erhalten Sie standardmäßig den Windows Server 2016-Datenpfad und die Leistungs Nummern, wenn Sie die Verbindung für Ihre virtuellen Netzwerke erstellen. Gehen Sie folgendermaßen vor, um den Windows Server 2019-Datenpfad zu aktivieren:

   1. Wechseln Sie auf einer Sdn-Gateway-VM zu **Dienste** Konsole (Services. msc).
   2. Suchen Sie nach dem Dienst mit dem Namen **Azure Gateway Service**, und legen Sie den Starttyp auf **automatisch**fest.
   3. Starten Sie die Gateway-VM neu.
      Die aktiven Verbindungen auf diesem Gateway-Failover auf eine redundante Gateway-VM.
   4. Wiederholen Sie die vorherigen Schritte für den Rest der Gateway-VMS.

>[!TIP]
>Um die besten Ergebnisse zu erzielen, stellen Sie sicher, dass die Eigenschaften "ciphertransformationconstant" und "authenticationtransformconstant" in den Schnellmodus-Einstellungen der IPSec-Verbindung die **GCMAES256** Verschlüsselungs Suite verwenden.
>
>Um die maximale Leistung zu erzielen, muss die gatewayhosthardware die CPU-Anweisungs Sätze AES-NI und Pclmulqdq unterstützen. Diese sind für alle Westmere (32nm) und spätere Intel CPU verfügbar, außer bei Modellen, in denen AES-NI deaktiviert wurde. Sie können sich die Hardwarehersteller Dokumentation ansehen, um festzustellen, ob die CPU AES-NI-und Pclmulqdq-CPU-Anweisungs Sätze unterstützt.

Im folgenden finden Sie ein Rest-Beispiel für eine IPSec-Verbindung mit optimalen Sicherheits Algorithmen:

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

Wir haben in unseren Testlabors umfassende Leistungstests für die Sdn-Gateways durchgeführt. In den Tests haben wir die gatewaynetzwerkleistung mit Windows Server 2019 in Sdn-Szenarien und nicht-Sdn-Szenarios verglichen. Die im Blog Artikel erfassten Ergebnisse und Test Setup Details finden Sie [hier](https://blogs.technet.microsoft.com/networking/2018/08/15/high-performance-gateways/).

---