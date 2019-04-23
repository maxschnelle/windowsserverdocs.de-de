---
title: BGP-Befehlsreferenz für Windows PowerShell
description: Sie können in diesem Thema als Referenz beim Schreiben von Windows PowerShell-Skripts in Windows Server 2016, hinzufügen, konfigurieren und Entfernen von BGP-Funktionen von Routern für RAS-Gateway und Remote Access Local Area Network (LAN).
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b0240a3-b927-4a1e-b241-5f8f29a9552f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 07f4dde61f732d5b3f839ee14a6eeb43a421f23f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859971"
---
# <a name="bgp-windows-powershell-command-reference"></a>BGP-Befehlsreferenz für Windows PowerShell

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema als Referenz beim Schreiben von Windows PowerShell-Skripts hinzufügen, konfigurieren und Entfernen von BGP-Funktionen von Routern für RAS-Gateway und Remote Access Local Area Network (LAN).  
  
Diese BGP-Befehle sind Teil der Remotezugriffs-Windows PowerShell-Befehlssatz für Windows Server 2016. In diesem Thema können Sie schnell die BGP-Befehle, die Sie in Skripts verwenden möchten.  
  
Weitere Informationen zu allen RAS-Befehle, finden Sie unter [Remotezugriff-Cmdlets](https://technet.microsoft.com/library/hh918399.aspx).  
  
## <a name="bgp-command-reference"></a>BGP-Befehlsreferenz  
Die folgenden Abschnitte enthalten die Befehlsnamen, Zweck und die Syntax für jeden BGP-Befehl als auch einen Link zu den Befehl in der RAS-Referenz, die ausführlichere Informationen zu jedem Befehl enthält.  
  
Diese Referenz enthält die folgenden Abschnitte.  
  
-   [Hinzufügen von Befehlen](#bkmk_add)  
  
-   [Clear-Befehle](#bkmk_clear)  
  
-   [Deaktivieren und Aktivieren von Befehlen](#bkmk_disable)  
  
-   [Get-Befehle](#bkmk_get)  
  
-   [Installieren Sie Befehle](#bkmk_install)  
  
-   [Entfernen von Befehlen](#bkmk_remove)  
  
-   ["Set"-Befehlen](#bkmk_set)  
  
-   [Start- und Stop-Befehle](#bkmk_start)  
  
-   [Deinstallationsbefehle](#bkmk_uninstall)  
  
### <a name="bkmk_add"></a>Hinzufügen von Befehlen  
Im folgenden werden die BGP-Hinzufügen von Befehlen.  
  
[Add-BgpCustomRoute](https://technet.microsoft.com/library/dn262684.aspx)  
  
Benutzerdefinierte Routen und BGP-Routingtabelle hinzugefügt.  
  
```  
Add-BgpCustomRoute [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-Interface <String[]> ] [-Network <String[]> ] [-PassThru] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Add-BgpPeer](https://technet.microsoft.com/library/dn262687.aspx)  
  
Fügt ein neuer BGP-Peer hinzu.  
  
```  
Add-BgpPeer [-Name] <String> -LocalIPAddress <IPAddress> -PeerASN <UInt32> -PeerIPAddress <IPAddress> [-CimSession <CimSession[]> ] [-HoldTimeSec <UInt16> ] [-IdleHoldTimeSec <UInt16> ] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-LocalASN <UInt32> ] [-MaxAllowedPrefix <UInt32> ] [-OperationMode <OperationMode> {Mixed | Server} ] [-PassThru] [-PeeringMode <PeeringMode> {Automatic | Manual} ] [-RouteReflectorClient <Boolean> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Weight <UInt16> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Add-BgpRouteAggregate](https://technet.microsoft.com/library/mt463113.aspx)  
  
Fügt einen neuen aggregierten Route für bestimmte BGP-Routen hinzu.  
  
```  
Add-BgpRouteAggregate -Prefix <String> [-AttributePolicy <String[]> ] [-CimSession <CimSession[]> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-PassThru] [-PreserveASPath <PreserveASPath> ] [-RoutingDomain <String> ] [-SummaryOnly <SummaryOnly> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Add-BgpRouter](https://technet.microsoft.com/library/dn262665.aspx)  
  
Fügt einen BGP-Router für den angegebenen Mandanten-ID.  
  
```  
Add-BgpRouter -BgpIdentifier <IPAddress> -LocalASN <UInt32> [-CimSession <CimSession[]> ] [-ClientToClientReflection <ClientToClientReflection> ] [-ClusterId <UInt32> ] [-CompareMEDAcrossASN <Boolean> ] [-DefaultGatewayRouting <Boolean> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-IPv6Routing <IPv6RoutingState> {Disabled | Enabled} ] [-LocalIPv6Address <IPAddress> ] [-PassThru] [-RouteReflector <RouteReflector> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-TransitRouting <TransitRouting> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Add-BgpRoutingPolicy](https://technet.microsoft.com/library/dn262662.aspx)  
  
Fügt den Richtlinienspeicher eine BGP-Routingrichtlinie hinzu.  
  
```  
Add-BgpRoutingPolicy [-Name] <String> [-PolicyType] <PolicyType> {Deny | Allow | ModifyAttribute} [-AddCommunity <String[]> ] [-CimSession <CimSession[]> ] [-ClearMED] [-Force] [-IgnorePrefix <String[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-MatchASNRange <UInt32[]> ] [-MatchCommunity <String[]> ] [-MatchNextHop <IPAddress[]> ] [-MatchPrefix <String[]> ] [-NewLocalPref <UInt32]> ] [-NewMED <UInt32]> ] [-NewNextHop <IPAddress> ] [-PassThru] [-RemoveAllCommunities] [-RemoveCommunity <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Add-BgpRoutingPolicyForPeer](https://technet.microsoft.com/library/dn262680.aspx)  
  
BGP-Peers wird BGP-Routingrichtlinien hinzugefügt.  
  
```  
Add-BgpRoutingPolicyForPeer -Direction <PolicyDirection> {Ingress | Egress} -PolicyName <String[]> [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-PeerName <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
### <a name="bkmk_clear"></a>Clear-Befehle  
Es folgen die Clear-Befehle für BGP  
  
[Clear-BgpRouteFlapDampening](https://technet.microsoft.com/library/mt463114.aspx)  
  
Löscht die Route Flap-Dämpfung Informationen für den angegebenen Satz von BGP-Routen an.  
  
```  
Clear-BgpRouteFlapDampening [-CimSession <CimSession[]> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-Prefix <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
### <a name="bkmk_disable"></a>Deaktivieren und Aktivieren von Befehlen  
Im folgenden sind die Befehle deaktivieren und aktivieren Sie für BGP  
  
[Disable-BgpRouteFlapDampening](https://technet.microsoft.com/library/mt463100.aspx)  
  
Deaktiviert die Route, die für das Flügelschlagen BGP-Routen Dämpfung.  
  
```  
Disable-BgpRouteFlapDampening [-CimSession <CimSession[]> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Enable-BgpRouteFlapDampening](https://technet.microsoft.com/library/mt463102.aspx)  
  
Ermöglicht das Weiterleiten von Dämpfung für das Flügelschlagen BGP-Routen.  
  
```  
Enable-BgpRouteFlapDampening [-CimSession <CimSession[]> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-PassThru] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
### <a name="bkmk_get"></a>Get-Befehle  
Im folgenden werden die Befehle Get für BGP.  
  
[Get-BgpCustomRoute](https://technet.microsoft.com/library/dn262664.aspx)  
  
Ruft benutzerdefinierte Routeninformationen aus der BGP-Router ab.  
  
```  
Get-BgpCustomRoute [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Get-BgpPeer](https://technet.microsoft.com/library/dn262659.aspx)  
  
Ruft die Konfigurationsinformationen für BGP-Peers ab.  
  
```  
Get-BgpPeer [[-Name] <String[]> ] [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Get-BgpRouteAggregate](https://technet.microsoft.com/library/mt463103.aspx)  
  
Ruft alle aggregierten BGP-Routen vom Administrator konfiguriert wurde.  
  
```  
Get-BgpRouteAggregate [-CimSession <CimSession[]> ] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-Prefix <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Get-BgpRouteFlapDampening](https://technet.microsoft.com/library/mt463108.aspx)  
  
Ruft die Konfiguration einer BGP-Route Kauf-Engine ab.  
  
```  
Get-BgpRouteFlapDampening [-CimSession <CimSession[]> ] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Get-BgpRouteInformation](https://technet.microsoft.com/library/dn262667.aspx)  
  
Ruft die BGP-Route-Informationen für eine oder mehrere Netzwerkpräfixe aus der BGP-Routingtabelle ab.  
  
```  
Get-BgpRouteInformation [-CimSession <CimSession[]> ] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-Network <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Type <RouteType> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Get-BgpRouter](https://technet.microsoft.com/library/dn262660.aspx)  
  
Ruft die Konfigurationsinformationen für die BGP-Router ab.  
  
```  
Get-BgpRouter [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String[]> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Get-BgpRoutingPolicy](https://technet.microsoft.com/library/dn262672.aspx)  
  
Ruft die Konfigurationsinformationen des BGP-Routingrichtlinien ab.  
  
```  
Get-BgpRoutingPolicy [[-Name] <String[]> ] [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-PolicyType <PolicyType> {Deny | Allow | ModifyAttribute} ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Get-BgpStatistics](https://technet.microsoft.com/library/dn262685.aspx)  
  
Ruft die BGP-peering Nachrichten- und Ankündigung Statistiken ab.  
  
```  
Get-BgpStatistics [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-PeerName <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
### <a name="bkmk_install"></a>Installieren Sie Befehle  
Im folgenden werden die Befehle zur Installation für RAS-Gateways und BGP.  
  
[Install-RemoteAccess](https://technet.microsoft.com/library/hh918408.aspx)  
  
Führt Überprüfungen der Voraussetzungen für DirectAccess (DA), stellen Sie sicher, dass sie installiert werden kann, werden die Daten für den Remotezugriff (RA) (einschließlich der Verwaltung von Remoteclients) oder für die Verwaltung von Remoteclients nur installiert, VPN (Remote Access VPN und Standort-zu-Standort-VPN), installiert und BGP-Routing-Installationen.  
  
```  
Parameter Set: MultiTenant  
Install-RemoteAccess [-MultiTenancy] [-CapacityKbps <UInt64> ] [-CimSession <CimSession[]> ] [-ComputerName <String> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-MsgAuthenticator <String> {Enabled | Disabled} ] [-PassThru] [-RadiusPort <UInt16> ] [-RadiusScore <Byte> ] [-RadiusServer <String> ] [-RadiusTimeout <UInt32> ] [-SharedSecret <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
  
Parameter Set: Vpn  
Install-RemoteAccess [-VpnType] <String> {Vpn | VpnS2S | SstpProxy | RoutingOnly} [-CimSession <CimSession[]> ] [-ComputerName <String> ] [-EntrypointName <String> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-IPAddressRange <String[]> ] [-IPv6Prefix <String> ] [-Legacy] [-MsgAuthenticator <String> {Enabled | Disabled} ] [-PassThru] [-RadiusPort <UInt16> ] [-RadiusScore <Byte> ] [-RadiusServer <String> ] [-RadiusTimeout <UInt32> ] [-SharedSecret <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
> [!IMPORTANT]  
> Bei der Installation von RAS-Gateway im mehrinstanzenmodus müssen Sie angeben, ob BGP für jeden Mandanten, mithilfe aktiviert ist der **Enable-RemoteAccessRoutingDomain** Windows PowerShell-Befehl mit der **-Typ** Parameterwert **alle**. Der folgende Beispielcode veranschaulicht, wie zum Installieren von RAS im mehrinstanzenmodus mit allen RAS-Funktionen (Punkt-zu-Standort-VPN-Standort-zu-Standort-VPN und BGP routing) für zwei Mandanten, Contoso und Fabrikam aktiviert.  
  
```  
$Contoso_RoutingDomain = "ContosoTenant"  
$Fabrikam_RoutingDomain = "FabrikamTenant"  
  
Install-RemoteAccess -MultiTenancy  
  
Enable-RemoteAccessRoutingDomain -Name $Contoso_RoutingDomain -Type All -PassThru  
Enable-RemoteAccessRoutingDomain -Name $Fabrikam_RoutingDomain -Type All -PassThru  
```  
  
Wenn Sie den Remotezugriff als LAN-Router statt als Gateway verwenden, können Sie weiterhin BGP bietet den Vorteil, dass dynamisches routing in Ihrem Intranet. Klicken Sie zum Installieren von Remote-Zugriff im LAN mit BGP-Router Geben Sie den folgenden Befehl in einer Windows PowerShell-Eingabeaufforderung, und drücken Sie dann die EINGABETASTE.  
  
```  
Install-RemoteAccess -VpnType RoutingOnly  
```  
  
### <a name="bkmk_remove"></a>Entfernen von Befehlen  
Im folgenden werden die Befehle entfernen für BGP.  
  
[Remove-BgpCustomRoute](https://technet.microsoft.com/library/dn262669.aspx)  
  
Entfernt benutzerdefinierte Routen aus der BGP-Router an.  
  
```  
Remove-BgpCustomRoute [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-Interface <String[]> ] [-Network <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Remove-BgpPeer](https://technet.microsoft.com/library/dn262675.aspx)  
  
Wird BGP-Peers aus einem Router entfernt.  
  
```  
Remove-BgpPeer [-Name] <String[]> [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Remove-BgpRouteAggregate](https://technet.microsoft.com/library/mt463110.aspx)  
  
Entfernt die angegebenen aggregate BGP-Routen.  
  
```  
Remove-BgpRouteAggregate [-CimSession <CimSession[]> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-Prefix <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Remove-BgpRouter](https://technet.microsoft.com/library/dn262678.aspx)  
  
Entfernt einen BGP-Router.  
  
```  
Remove-BgpRouter [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String[]> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Remove-BgpRoutingPolicy](https://technet.microsoft.com/library/dn262656.aspx)  
  
Entfernt einen routing Richtlinien für den Richtlinienspeicher.  
  
```  
Remove-BgpRoutingPolicy [-Name] <String[]> [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Remove-BgpRoutingPolicyForPeer](https://technet.microsoft.com/library/dn262681.aspx)  
  
Entfernt einen routing-Richtlinien über das BGP-Peers.  
  
```  
Parameter Set: Remove1  
Remove-BgpRoutingPolicyForPeer [-CimSession <CimSession[]> ] [-Direction <PolicyDirection> {Ingress | Egress} ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-PeerName <String[]> ] [-PolicyName <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
### <a name="bkmk_set"></a>"Set"-Befehlen  
Im folgenden werden die "Set"-Befehlen für BGP.  
  
[Set-BgpPeer](https://technet.microsoft.com/library/dn262673.aspx)  
  
Aktualisiert die Konfiguration des angegebenen BGP-Peers.  
  
```  
Set-BgpPeer [-Name] <String> [-CimSession <CimSession[]> ] [-ClearPrefixLimit] [-Force] [-HoldTimeSec <UInt16> ] [-IdleHoldTimeSec <UInt16> ] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-LocalASN <UInt32> ] [-LocalIPAddress <IPAddress> ] [-MaxAllowedPrefix <UInt32> ] [-OperationMode <OperationMode> {Mixed | Server} ] [-PassThru] [-PeerASN <UInt32> ] [-PeeringMode <PeeringMode> {Automatic | Manual} ] [-PeerIPAddress <IPAddress> ] [-RouteReflectorClient <Boolean> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Weight <UInt16> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Set-BgpRouteAggregate](https://technet.microsoft.com/library/mt463115.aspx)  
  
Aktualisiert die Eigenschaften der angegebenen aggregate BGP-Route.  
  
```  
Set-BgpRouteAggregate -Prefix <String> [-AttributePolicy <String[]> ] [-CimSession <CimSession[]> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-PassThru] [-PreserveASPath <PreserveASPath> ] [-RoutingDomain <String> ] [-SummaryOnly <SummaryOnly> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Set-BgpRouteFlapDampening](https://technet.microsoft.com/library/mt463116.aspx)  
  
Konfiguriert die BGP-Route-Dämpfung Engine.  
  
```  
Set-BgpRouteFlapDampening [-CimSession <CimSession[]> ] [-Force] [-HalfLife <UInt32> ] [-HalfLifeUnreachable <UInt32> ] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-MaxSuppressTime <UInt32> ] [-PassThru] [-ReuseThreshold <UInt32> ] [-RoutingDomain <String> ] [-SuppressThreshold <UInt32> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Set-BgpRouter](https://technet.microsoft.com/library/dn262652.aspx)  
  
Aktualisiert die Konfiguration des lokalen BGP-Routers für die Mandanten-ID.  
  
```  
Set-BgpRouter [-BgpIdentifier <IPAddress> ] [-CimSession <CimSession[]> ] [-ClientToClientReflection <ClientToClientReflection> ] [-ClusterId <UInt32> ] [-CompareMEDAcrossASN <Boolean> ] [-DefaultGatewayRouting <Boolean> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-IPv6Routing <IPv6RoutingState> {Disabled | Enabled} ] [-LocalASN <UInt32> ] [-LocalIPv6Address <IPAddress> ] [-PassThru] [-RouteReflector <RouteReflector> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-TransitRouting <TransitRouting> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Set-BgpRoutingPolicy](https://technet.microsoft.com/library/dn262670.aspx)  
  
Ändert eine Richtlinie Routingkonfiguration.  
  
```  
Set-BgpRoutingPolicy [-Name] <String> [-AddCommunity <String[]> ] [-CimSession <CimSession[]> ] [-ClearMED] [-Force] [-IgnorePrefix <String[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-MatchASNRange <UInt32[]> ] [-MatchCommunity <String[]> ] [-MatchNextHop <IPAddress[]> ] [-MatchPrefix <String[]> ] [-NewLocalPref <UInt32]> ] [-NewMED <UInt32]> ] [-NewNextHop <IPAddress> ] [-PassThru] [-PolicyType <PolicyType> {Deny | Allow | ModifyAttribute} ] [-RemoveAllCommunities] [-RemoveCommunity <String[]> ] [-RemovePolicyClause <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Set-BgpRoutingPolicyForPeer](https://technet.microsoft.com/library/dn262674.aspx)  
  
Ändert BGP-Routingrichtlinien für BGP-Peers an.  
  
```  
Set-BgpRoutingPolicyForPeer -Direction <PolicyDirection> {Ingress | Egress} -PolicyName <String[]> [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-PeerName <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
### <a name="bkmk_start"></a>Start- und Stop-Befehle  
Es folgen die Start- und Stop-Befehle für BGP.  
  
[Start-BgpPeer](https://technet.microsoft.com/library/dn262683.aspx)  
  
Startet das routing von Sitzungen für BGP-Peers.  
  
```  
Start-BgpPeer [-Name] <String[]> [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Stop-BgpPeer](https://technet.microsoft.com/library/dn262661.aspx)  
  
Beendet die Weiterleitung von Sitzungen für BGP-Peers.  
  
```  
Stop-BgpPeer [-Name] <String[]> [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
### <a name="bkmk_uninstall"></a>Deinstallationsbefehle  
Im folgenden werden die Deinstallationsbefehle für RAS-Gateways und BGP.  
  
[Uninstall-RemoteAccess](https://technet.microsoft.com/library/hh918390.aspx)  
  
Deinstalliert den Remotezugriff auf dem Computer, einschließlich aller Features für RAS und Funktionen (RAS-Gateway, BGP, usw.).  
  
```  
Uninstall-RemoteAccess [-CimSession <CimSession[]> ] [-ComputerName <String> ] [-EntrypointName <String> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-ThrottleLimit <Int32> ] [-VpnType <String> {Vpn | VpnS2S} ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  


