---
title: BGP-Befehlsreferenz für Windows PowerShell
description: Sie können dieses Thema als Referenz verwenden, wenn Sie Windows PowerShell-Skripts in Windows Server 2016 schreiben, um BGP-Funktionen über RAS-Gateway und RAS-LAN-Router (Local Area Network) hinzuzufügen, zu konfigurieren und zu entfernen.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b0240a3-b927-4a1e-b241-5f8f29a9552f
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 22f4475df00e975ffc5cd0956a0126673a67f907
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80309273"
---
# <a name="bgp-windows-powershell-command-reference"></a>BGP-Befehlsreferenz für Windows PowerShell

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Sie können dieses Thema als Referenz verwenden, wenn Sie Windows PowerShell-Skripts schreiben, um BGP-Funktionen über RAS-Gateway und RAS-LAN-Router (Local Area Network) hinzuzufügen, zu konfigurieren und zu entfernen.  
  
Diese BGP-Befehle sind Teil des Windows PowerShell-Befehlssatzes für Remote Zugriff für Windows Server 2016. Dieses Thema hilft Ihnen dabei, die BGP-Befehle, die Sie in Skripts verwenden möchten, schnell zu finden.  
  
Weitere Informationen zu allen Remote Zugriffs Befehlen finden Sie unter [Remote Access-Cmdlets](https://technet.microsoft.com/library/hh918399.aspx).  
  
## <a name="bgp-command-reference"></a>BGP-Befehlsreferenz  
In den folgenden Abschnitten finden Sie einen Befehlsnamen, einen Zweck und eine Syntax für jeden BGP-Befehl sowie einen Link zum Befehl in der RAS-Referenz, der ausführlichere Informationen zu den einzelnen Befehlen enthält.  
  
Diese Referenz umfasst folgende Abschnitte:  
  
-   [Befehle hinzufügen](#bkmk_add)  
  
-   [Befehle löschen](#bkmk_clear)  
  
-   [Deaktivieren und Aktivieren von Befehlen](#bkmk_disable)  
  
-   [Get-Befehle](#bkmk_get)  
  
-   [Installieren von Befehlen](#bkmk_install)  
  
-   [Befehle entfernen](#bkmk_remove)  
  
-   [Befehle festlegen](#bkmk_set)  
  
-   [Starten und Abbrechen von Befehlen](#bkmk_start)  
  
-   [Deinstallations Befehle](#bkmk_uninstall)  
  
### <a name="add-commands"></a><a name="bkmk_add"></a>Befehle hinzufügen  
Die folgenden BGP-Befehle werden hinzugefügt.  
  
[Add-bgpcustomroute](https://technet.microsoft.com/library/dn262684.aspx)  
  
Fügt der BGP-Routing Tabelle benutzerdefinierte Routen hinzu.  
  
```  
Add-BgpCustomRoute [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-Interface <String[]> ] [-Network <String[]> ] [-PassThru] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Add-bgppeer](https://technet.microsoft.com/library/dn262687.aspx)  
  
Fügt einen neuen BGP-Peer hinzu.  
  
```  
Add-BgpPeer [-Name] <String> -LocalIPAddress <IPAddress> -PeerASN <UInt32> -PeerIPAddress <IPAddress> [-CimSession <CimSession[]> ] [-HoldTimeSec <UInt16> ] [-IdleHoldTimeSec <UInt16> ] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-LocalASN <UInt32> ] [-MaxAllowedPrefix <UInt32> ] [-OperationMode <OperationMode> {Mixed | Server} ] [-PassThru] [-PeeringMode <PeeringMode> {Automatic | Manual} ] [-RouteReflectorClient <Boolean> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Weight <UInt16> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Add-bgprouteaggregate](https://technet.microsoft.com/library/mt463113.aspx)  
  
Fügt eine neue Aggregat Route für bestimmte BGP-Routen hinzu.  
  
```  
Add-BgpRouteAggregate -Prefix <String> [-AttributePolicy <String[]> ] [-CimSession <CimSession[]> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-PassThru] [-PreserveASPath <PreserveASPath> ] [-RoutingDomain <String> ] [-SummaryOnly <SummaryOnly> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Add-bgprouter](https://technet.microsoft.com/library/dn262665.aspx)  
  
Fügt einen BGP-Router für die angegebene Mandanten-ID hinzu.  
  
```  
Add-BgpRouter -BgpIdentifier <IPAddress> -LocalASN <UInt32> [-CimSession <CimSession[]> ] [-ClientToClientReflection <ClientToClientReflection> ] [-ClusterId <UInt32> ] [-CompareMEDAcrossASN <Boolean> ] [-DefaultGatewayRouting <Boolean> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-IPv6Routing <IPv6RoutingState> {Disabled | Enabled} ] [-LocalIPv6Address <IPAddress> ] [-PassThru] [-RouteReflector <RouteReflector> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-TransitRouting <TransitRouting> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Add-bgproutingpolicy](https://technet.microsoft.com/library/dn262662.aspx)  
  
Fügt dem Richtlinien Speicher eine BGP-Routing Richtlinie hinzu.  
  
```  
Add-BgpRoutingPolicy [-Name] <String> [-PolicyType] <PolicyType> {Deny | Allow | ModifyAttribute} [-AddCommunity <String[]> ] [-CimSession <CimSession[]> ] [-ClearMED] [-Force] [-IgnorePrefix <String[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-MatchASNRange <UInt32[]> ] [-MatchCommunity <String[]> ] [-MatchNextHop <IPAddress[]> ] [-MatchPrefix <String[]> ] [-NewLocalPref <UInt32]> ] [-NewMED <UInt32]> ] [-NewNextHop <IPAddress> ] [-PassThru] [-RemoveAllCommunities] [-RemoveCommunity <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Add-bgproutingpolicyforpeer](https://technet.microsoft.com/library/dn262680.aspx)  
  
Fügt BGP-Routing Richtlinien BGP-Peers hinzu.  
  
```  
Add-BgpRoutingPolicyForPeer -Direction <PolicyDirection> {Ingress | Egress} -PolicyName <String[]> [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-PeerName <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
### <a name="clear-commands"></a><a name="bkmk_clear"></a>Befehle löschen  
Im folgenden finden Sie die unverschlüsselten Befehle für BGP.  
  
[Clear-bgprouteflapdampening](https://technet.microsoft.com/library/mt463114.aspx)  
  
Löscht die Weiterleitungs Klappen-Feuchtigkeits Informationen für den angegebenen Satz von BGP-Routen.  
  
```  
Clear-BgpRouteFlapDampening [-CimSession <CimSession[]> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-Prefix <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
### <a name="disable-and-enable-commands"></a><a name="bkmk_disable"></a>Deaktivieren und Aktivieren von Befehlen  
Im folgenden finden Sie die Befehle zum Deaktivieren und aktivieren für BGP.  
  
[Deaktivieren-bgprouteflapdampening](https://technet.microsoft.com/library/mt463100.aspx)  
  
Deaktiviert die Routen Dämpfung für die Fluktuation BGP-Routen.  
  
```  
Disable-BgpRouteFlapDampening [-CimSession <CimSession[]> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Enable-bgprouteflapdampening](https://technet.microsoft.com/library/mt463102.aspx)  
  
Aktiviert die Routen Dämpfung für die Fluktuation BGP-Routen.  
  
```  
Enable-BgpRouteFlapDampening [-CimSession <CimSession[]> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-PassThru] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
### <a name="get-commands"></a><a name="bkmk_get"></a>Get-Befehle  
Im folgenden finden Sie die Get-Befehle für BGP.  
  
[Get-bgpcustomroute](https://technet.microsoft.com/library/dn262664.aspx)  
  
Ruft benutzerdefinierte Routeninformationen vom BGP-Router ab.  
  
```  
Get-BgpCustomRoute [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Get-bgppeer](https://technet.microsoft.com/library/dn262659.aspx)  
  
Ruft Konfigurationsinformationen für BGP-Peers ab.  
  
```  
Get-BgpPeer [[-Name] <String[]> ] [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Get-bgprouteaggregate](https://technet.microsoft.com/library/mt463103.aspx)  
  
Ruft alle vom Administrator konfigurierten BGP-Aggregat Routen ab.  
  
```  
Get-BgpRouteAggregate [-CimSession <CimSession[]> ] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-Prefix <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Get-bgprouteflapdampening](https://technet.microsoft.com/library/mt463108.aspx)  
  
Ruft die Konfiguration einer BGP-Weiterleitungs-däfungs-Engine ab.  
  
```  
Get-BgpRouteFlapDampening [-CimSession <CimSession[]> ] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Get-bgprouteinformation](https://technet.microsoft.com/library/dn262667.aspx)  
  
Ruft BGP-Routeninformationen für mindestens ein Netzwerk Präfix aus der BGP-Routing Tabelle ab.  
  
```  
Get-BgpRouteInformation [-CimSession <CimSession[]> ] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-Network <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Type <RouteType> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Get-bgprouter](https://technet.microsoft.com/library/dn262660.aspx)  
  
Ruft Konfigurationsinformationen für BGP-Router ab.  
  
```  
Get-BgpRouter [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String[]> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Get-bgproutingpolicy](https://technet.microsoft.com/library/dn262672.aspx)  
  
Ruft Konfigurationsinformationen der BGP-Routing Richtlinien ab.  
  
```  
Get-BgpRoutingPolicy [[-Name] <String[]> ] [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-PolicyType <PolicyType> {Deny | Allow | ModifyAttribute} ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Get-bgpstatistics](https://technet.microsoft.com/library/dn262685.aspx)  
  
Abrufen von BGP-Peering-bezogenen Nachrichten-und Routen Ankündigungs Statistiken.  
  
```  
Get-BgpStatistics [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-PeerName <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
### <a name="install-commands"></a><a name="bkmk_install"></a>Installieren von Befehlen  
Im folgenden finden Sie die Installations Befehle für RAS-Gateway und BGP.  
  
[Install-remoteaccess](https://technet.microsoft.com/library/hh918408.aspx)  
  
Führt Voraussetzungs Prüfungen für DirectAccess (da) aus, um sicherzustellen, dass die Installation möglich ist, ob für den Remote Zugriff (einschließlich der Verwaltung von Remote Clients) installiert ist, und installiert VPN (sowohl RAS-VPN als auch Standort-zu-Standort-VPN), und installiert BGP-Routing.  
  
```  
Parameter Set: MultiTenant  
Install-RemoteAccess [-MultiTenancy] [-CapacityKbps <UInt64> ] [-CimSession <CimSession[]> ] [-ComputerName <String> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-MsgAuthenticator <String> {Enabled | Disabled} ] [-PassThru] [-RadiusPort <UInt16> ] [-RadiusScore <Byte> ] [-RadiusServer <String> ] [-RadiusTimeout <UInt32> ] [-SharedSecret <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
  
Parameter Set: Vpn  
Install-RemoteAccess [-VpnType] <String> {Vpn | VpnS2S | SstpProxy | RoutingOnly} [-CimSession <CimSession[]> ] [-ComputerName <String> ] [-EntrypointName <String> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-IPAddressRange <String[]> ] [-IPv6Prefix <String> ] [-Legacy] [-MsgAuthenticator <String> {Enabled | Disabled} ] [-PassThru] [-RadiusPort <UInt16> ] [-RadiusScore <Byte> ] [-RadiusServer <String> ] [-RadiusTimeout <UInt32> ] [-SharedSecret <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
> [!IMPORTANT]  
> Wenn Sie das RAS-Gateway im mehr Instanzen fähigen Modus installieren, müssen Sie angeben, ob BGP für jeden Mandanten aktiviert ist, indem Sie den Windows PowerShell-Befehl **enable-remoteaccessroutingdomain** mit dem **-Type-** Parameterwert **all**verwenden. Der folgende Beispielcode veranschaulicht, wie Sie RAS im mehr Instanzen Modus mit allen RAS-Funktionen (Punkt-zu-Standort-VPN, Site-to-Site-VPN und BGP-Routing) installieren können, die für zwei Mandanten aktiviert sind: "mso" und "Fabrikam".  
  
```  
$Contoso_RoutingDomain = "ContosoTenant"  
$Fabrikam_RoutingDomain = "FabrikamTenant"  
  
Install-RemoteAccess -MultiTenancy  
  
Enable-RemoteAccessRoutingDomain -Name $Contoso_RoutingDomain -Type All -PassThru  
Enable-RemoteAccessRoutingDomain -Name $Fabrikam_RoutingDomain -Type All -PassThru  
```  
  
Wenn Sie den Remote Zugriff als LAN-Router anstelle von als Gateway verwenden, können Sie weiterhin BGP verwenden, was den Vorteil bietet, dass Sie das dynamische Routing in Ihrem Intranet verwenden. Geben Sie den folgenden Befehl in einer Windows PowerShell-Eingabeaufforderung ein, und drücken Sie die EINGABETASTE, um den Remote Zugriff als BGP-LAN-Router zu installieren.  
  
```  
Install-RemoteAccess -VpnType RoutingOnly  
```  
  
### <a name="remove-commands"></a><a name="bkmk_remove"></a>Befehle entfernen  
Im folgenden finden Sie die Remove-Befehle für BGP.  
  
[Remove-bgpcustomroute](https://technet.microsoft.com/library/dn262669.aspx)  
  
Entfernt benutzerdefinierte Routen vom BGP-Router.  
  
```  
Remove-BgpCustomRoute [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-Interface <String[]> ] [-Network <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Remove-bgppeer](https://technet.microsoft.com/library/dn262675.aspx)  
  
Entfernt BGP-Peers von einem Router.  
  
```  
Remove-BgpPeer [-Name] <String[]> [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Remove-bgprouteaggregate](https://technet.microsoft.com/library/mt463110.aspx)  
  
Entfernt den Satz der angegebenen aggregierten BGP-Routen.  
  
```  
Remove-BgpRouteAggregate [-CimSession <CimSession[]> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-Prefix <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Remove-bgprouter](https://technet.microsoft.com/library/dn262678.aspx)  
  
Entfernt einen BGP-Router.  
  
```  
Remove-BgpRouter [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String[]> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Remove-bgproutingpolicy](https://technet.microsoft.com/library/dn262656.aspx)  
  
Entfernt Routing Richtlinien aus dem Richtlinien Speicher.  
  
```  
Remove-BgpRoutingPolicy [-Name] <String[]> [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Remove-bgproutingpolicyforpeer](https://technet.microsoft.com/library/dn262681.aspx)  
  
Entfernt Routing Richtlinien von BGP-Peers.  
  
```  
Parameter Set: Remove1  
Remove-BgpRoutingPolicyForPeer [-CimSession <CimSession[]> ] [-Direction <PolicyDirection> {Ingress | Egress} ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-PeerName <String[]> ] [-PolicyName <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
### <a name="set-commands"></a><a name="bkmk_set"></a>Befehle festlegen  
Im folgenden finden Sie die SET-Befehle für BGP.  
  
[Set-bgppeer](https://technet.microsoft.com/library/dn262673.aspx)  
  
Aktualisiert die Konfiguration des angegebenen BGP-Peers.  
  
```  
Set-BgpPeer [-Name] <String> [-CimSession <CimSession[]> ] [-ClearPrefixLimit] [-Force] [-HoldTimeSec <UInt16> ] [-IdleHoldTimeSec <UInt16> ] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-LocalASN <UInt32> ] [-LocalIPAddress <IPAddress> ] [-MaxAllowedPrefix <UInt32> ] [-OperationMode <OperationMode> {Mixed | Server} ] [-PassThru] [-PeerASN <UInt32> ] [-PeeringMode <PeeringMode> {Automatic | Manual} ] [-PeerIPAddress <IPAddress> ] [-RouteReflectorClient <Boolean> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Weight <UInt16> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Set-bgprouteaggregate](https://technet.microsoft.com/library/mt463115.aspx)  
  
Aktualisiert die Eigenschaften der angegebenen Aggregat-BGP-Route.  
  
```  
Set-BgpRouteAggregate -Prefix <String> [-AttributePolicy <String[]> ] [-CimSession <CimSession[]> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-PassThru] [-PreserveASPath <PreserveASPath> ] [-RoutingDomain <String> ] [-SummaryOnly <SummaryOnly> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Set-bgprouteflapdampening](https://technet.microsoft.com/library/mt463116.aspx)  
  
Konfiguriert die BGP-Weiterleitungs-Engine für die Routen Dämpfung.  
  
```  
Set-BgpRouteFlapDampening [-CimSession <CimSession[]> ] [-Force] [-HalfLife <UInt32> ] [-HalfLifeUnreachable <UInt32> ] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-MaxSuppressTime <UInt32> ] [-PassThru] [-ReuseThreshold <UInt32> ] [-RoutingDomain <String> ] [-SuppressThreshold <UInt32> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Set-bgprouter](https://technet.microsoft.com/library/dn262652.aspx)  
  
Aktualisiert die Konfiguration des lokalen BGP-Routers für die angegebene Mandanten-ID.  
  
```  
Set-BgpRouter [-BgpIdentifier <IPAddress> ] [-CimSession <CimSession[]> ] [-ClientToClientReflection <ClientToClientReflection> ] [-ClusterId <UInt32> ] [-CompareMEDAcrossASN <Boolean> ] [-DefaultGatewayRouting <Boolean> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-IPv6Routing <IPv6RoutingState> {Disabled | Enabled} ] [-LocalASN <UInt32> ] [-LocalIPv6Address <IPAddress> ] [-PassThru] [-RouteReflector <RouteReflector> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-TransitRouting <TransitRouting> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Set-bgproutingpolicy](https://technet.microsoft.com/library/dn262670.aspx)  
  
Ändert eine Routing Richtlinien Konfiguration.  
  
```  
Set-BgpRoutingPolicy [-Name] <String> [-AddCommunity <String[]> ] [-CimSession <CimSession[]> ] [-ClearMED] [-Force] [-IgnorePrefix <String[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-MatchASNRange <UInt32[]> ] [-MatchCommunity <String[]> ] [-MatchNextHop <IPAddress[]> ] [-MatchPrefix <String[]> ] [-NewLocalPref <UInt32]> ] [-NewMED <UInt32]> ] [-NewNextHop <IPAddress> ] [-PassThru] [-PolicyType <PolicyType> {Deny | Allow | ModifyAttribute} ] [-RemoveAllCommunities] [-RemoveCommunity <String[]> ] [-RemovePolicyClause <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Set-bgproutingpolicyforpeer](https://technet.microsoft.com/library/dn262674.aspx)  
  
Ändert BGP-Routing Richtlinien für BGP-Peers.  
  
```  
Set-BgpRoutingPolicyForPeer -Direction <PolicyDirection> {Ingress | Egress} -PolicyName <String[]> [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-PeerName <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
### <a name="start-and-stop-commands"></a><a name="bkmk_start"></a>Starten und Abbrechen von Befehlen  
Im folgenden finden Sie die Befehle zum Starten und Abbrechen für BGP.  
  
[Start-bgppeer](https://technet.microsoft.com/library/dn262683.aspx)  
  
Startet das Routing von Sitzungen für BGP-Peers.  
  
```  
Start-BgpPeer [-Name] <String[]> [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
["Beendigung-bgppeer"](https://technet.microsoft.com/library/dn262661.aspx)  
  
Beendet das Routing von Sitzungen für BGP-Peers.  
  
```  
Stop-BgpPeer [-Name] <String[]> [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
### <a name="uninstall-commands"></a><a name="bkmk_uninstall"></a>Deinstallations Befehle  
Im folgenden finden Sie die Deinstallations Befehle für RAS-Gateway und BGP.  
  
[Deinstallieren-remoteaccess](https://technet.microsoft.com/library/hh918390.aspx)  
  
Deinstalliert den Remote Zugriff vom Computer, einschließlich aller Remote Zugriffs Features und-Funktionen (RAS-Gateway, BGP usw.).  
  
```  
Uninstall-RemoteAccess [-CimSession <CimSession[]> ] [-ComputerName <String> ] [-EntrypointName <String> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-ThrottleLimit <Int32> ] [-VpnType <String> {Vpn | VpnS2S} ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  


