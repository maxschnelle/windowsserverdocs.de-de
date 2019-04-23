---
title: Verwalten der rollenbasierten Zugriffssteuerung mit Windows PowerShell
description: Dieses Thema ist Teil des Leitfadens Verwaltung von IP-Adressverwaltung (IPAM) in Windows Server 2016.
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
ms.openlocfilehash: e0318db1b2b1b2730ee6dc57b7b9df6d16fe57e8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841471"
---
# <a name="manage-role-based-access-control-with-windows-powershell"></a>Verwalten der rollenbasierten Zugriffssteuerung mit Windows PowerShell

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, erfahren, wie IPAM zum Verwalten der rollenbasierten Zugriffssteuerung mit Windows PowerShell verwenden.  
  
>[!NOTE]
>Der IPAM-Windows-PowerShell-Befehlsreferenz finden Sie unter den [IpamServer-Cmdlets in Windows PowerShell](https://docs.microsoft.com/powershell/module/ipamserver/?view=win10-ps).  
  
Die neue Windows PowerShell-IPAM-Befehle bieten Ihnen die Möglichkeit zum Abrufen und ändern den zugriffsbereichen der DNS- und DHCP-Objekte. Die folgende Tabelle zeigt den richtigen Befehl für die einzelnen IPAM-Objekte verwenden.  
  
|IPAM-Objekt|Befehl|Beschreibung|  
|---------------|-----------|---------------|  
|DNS-Server|Get-IpamDnsServer|Dieses Cmdlet gibt die DNS-Server-Objekt zurück, in IPAM|  
|DNS-Zone|Get-IpamDnsZone|Dieses Cmdlet gibt die DNS-Zone-Objekts zurück, in IPAM|  
|DNS-Ressourceneintrag|Get-IpamResourceRecord|Dieses Cmdlet gibt die DNS-Datensatz Ressourcenobjekt in IPAM zurück.|  
|DNS-Weiterleitung mit Bedingungen|Get-IpamDnsConditionalForwarder|Dieses Cmdlet gibt die bedingte Weiterleitung DNS-Objekts zurück, in IPAM|  
|DHCP-Server|Get-IpamDhcpServer|Dieses Cmdlet gibt die DHCP-Server-Objekt zurück, in IPAM|  
|DHCP-Bereichsgruppierung|Get-IpamDhcpSuperscope|Dieses Cmdlet gibt die DHCP-Bereichsgruppierung-Objekt zurück, in IPAM|  
|DHCP-Bereich|Get-IpamDhcpScope|Dieses Cmdlet gibt das Bereichsobjekt DHCP in IPAM zurück.|  
  
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
Sie können zugriffsbereiche für IPAM-Objekte festlegen, mit der `Set-IpamAccessScope` Befehl. Sie können diesen Befehl verwenden, um den Zugriffsbereich auf einen bestimmten Wert für ein Objekt festgelegt oder dazu führen, dass die Objekte des Zugriffsbereichs von übergeordneten Objekten geerbt. Es folgen die Objekte, die Sie mit dem folgenden Befehl konfigurieren können.  
  
-   DHCP-Bereich  
  
-   DHCP-Server  
  
-   DHCP-Bereichsgruppierung  
  
-   DNS-Weiterleitung mit Bedingungen  
  
-   DNS-Ressourceneinträgen  
  
-   DNS-Server  
  
-   DNS-Zone  
  
-   IP-Adressblock  
  
-   IP-Adressbereich  
  
-   IP-Adressbereich  
  
-   IP-Adresssubnetz  
  
Nachfolgend ist die Syntax für die `Set-IpamAccessScope` Befehl.  
  
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
  
Im folgenden Beispiel ist der DNS-Zone auf den Zugriffsbereich **dublin.contoso.com** ändert sich von **Dublin** zu **Europa**.  
  
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
  


