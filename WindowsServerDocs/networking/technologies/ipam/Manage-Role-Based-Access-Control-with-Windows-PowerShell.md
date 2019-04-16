---
title: Verwalten der rollenbasierten Zugriffssteuerung mit WindowsPowerShell
description: Dieses Thema ist Teil des Handbuchs Verwaltung von IP-Adressverwaltung (IPAM) in Windows Server2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4f13f78e-0114-4e41-9a28-82a4feccecfc
ms.author: pashort
author: shortpatti
ms.openlocfilehash: df6fa423a4ec891f1ad3faefad6c6054519542c4
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="manage-role-based-access-control-with-windows-powershell"></a>Verwalten der rollenbasierten Zugriffssteuerung mit WindowsPowerShell

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können in diesem Thema erfahren Sie, wie Sie IPAM zum Verwalten der rollenbasierten Zugriffssteuerung mit Windows PowerShell verwenden.  
  
>[!NOTE]
>Die IPAM Windows PowerShell-Befehlsverzeichnis finden Sie unter [IP-Adressverwaltung (IPAM) Server-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/jj553807.aspx).  
  
Die neue Windows PowerShell-IPAM-Befehle bieten Ihnen die Möglichkeit zum Abrufen und ändern die zugriffsbereiche von DNS- und DHCP-Objekten. Die folgende Tabelle veranschaulicht den entsprechenden Befehl für jedes IPAM-Objekt verwenden.  
  
|IPAM-Objekt|Befehl|Beschreibung|  
|---------------|-----------|---------------|  
|DNS-Server|Get-IpamDnsServer|Dieses Cmdlet gibt die DNS-Server-Objekt zurück, in IPAM|  
|DNS-Zone|Get-IpamDnsZone|Dieses Cmdlet gibt das Objekt des DNS-Zone in IPAM|  
|DNS-Ressourceneintrag|Get-IpamResourceRecord|Dieses Cmdlet gibt die DNS-Datensatz Ressourcenobjekt in IPAM|  
|DNS-Weiterleitung|Get-IpamDnsConditionalForwarder|Dieses Cmdlet gibt das Objekt des DNS-Weiterleitung in IPAM|  
|DHCP-Server|Get-IpamDhcpServer|Dieses Cmdlet gibt das DHCP-Serverobjekt in IPAM|  
|DHCP-Bereichsgruppierung|Get-IpamDhcpSuperscope|Dieses Cmdlet gibt die DHCP-Bereichsgruppierung-Objekt zurück, in IPAM|  
|DHCP-Bereich|Get-IpamDhcpScope|Dieses Cmdlet gibt das Objekt des DHCP-Bereich in IPAM|  
  
Im folgenden Beispiel der Ausgabe des Befehls der `Get-IpamDnsZone` Cmdlet Ruft die **dublin.contoso.com** DNS-Zone.  
  
```  
PS C:\Users\Administrator.CONTOSO> Get-IpamDnsZone -ZoneType Forward -ZoneName dublin.contoso.com  
  
ZoneName             : dublin.contoso.com  
ZoneType             : Forward  
AccessScopePath      : \Global\Dublin  
IsSigned             : False  
DynamicUpdateStatus  : None  
ScavengeStaleRecords : False  
```  
  
## <a name="setting-access-scopes-on-ipam-objects"></a>Festlegen von Zugriffsbereichen für IPAM-Objekte  
Sie können zugriffsbereiche für IPAM-Objekte festlegen, mit der `Set-IpamAccessScope` Befehl. Sie können diesen Befehl verwenden, um beim Festlegen des Zugriffsbereichs auf einen bestimmten Wert für ein Objekt oder dazu führen, dass die Objekte Zugriffsbereich von übergeordneten Objekten vererbt. Es folgen die Objekte, die Sie mit diesem Befehl konfigurieren können.  
  
-   DHCP-Bereich  
  
-   DHCP-Server  
  
-   DHCP-Bereichsgruppierung  
  
-   DNS-Weiterleitung  
  
-   DNS-Ressourceneinträgen  
  
-   DNS-Server  
  
-   DNS-Zone  
  
-   IP-Adressblock  
  
-   IP-Adressbereich  
  
-   IP-Adressraums  
  
-   IP-Adresssubnetz  
  
Folgendes ist die Syntax für die `Set-IpamAccessScope` Befehl.  
  
```  
NAME  
    Set-IpamAccessScope  
  
SYNTAX  
    Set-IpamAccessScope [-IpamRange] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamDnsServer] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  
    [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamDhcpServer] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  
    [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamDhcpSuperscope] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  
    [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamDhcpScope] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  
    [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamDnsConditionalForwarder] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  
    [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamDnsResourceRecord] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  
    [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamDnsZone] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  
    [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamAddressSpace] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  
    [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamSubnet] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamBlock] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  [<CommonParameters>]  
```  
  
Im folgenden Beispiel den Zugriffsbereich der DNS-Zone **dublin.contoso.com** ändert sich von **Dublin** auf **Europa**.  
  
```  
PS C:\Users\Administrator.CONTOSO> Get-IpamDnsZone -ZoneType Forward -ZoneName dublin.contoso.com  
  
ZoneName             : dublin.contoso.com  
ZoneType             : Forward  
AccessScopePath      : \Global\Dublin  
IsSigned             : False  
DynamicUpdateStatus  : None  
ScavengeStaleRecords : False  
  
PS C:\Users\Administrator.CONTOSO> $a = Get-IpamDnsZone -ZoneType Forward -ZoneName dublin.contoso.com  
PS C:\Users\Administrator.CONTOSO> Set-IpamAccessScope -IpamDnsZone -InputObject $a -AccessScopePath \Global\Europe -PassThru  
  
ZoneName             : dublin.contoso.com  
ZoneType             : Forward  
AccessScopePath      : \Global\Europe  
IsSigned             : False  
DynamicUpdateStatus  : None  
ScavengeStaleRecords : False  
```  
  


