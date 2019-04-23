---
title: Konfigurieren von Zugriffssteuerungslisten für die Rechenzentrumsfirewall
description: Sie können bestimmte ACLs auf Netzwerkschnittstellen anwenden.  Wenn ACLs auch für das virtuelle Subnetz festgelegt sind mit denen die Netzwerkschnittstelle verbunden ist, sowohl ACLs werden angewendet, aber die Netzwerkschnittstelle ACLs werden über das virtuelle Subnetz ACLs priorisiert.
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 25f18927-a63e-44f3-b02a-81ed51933187
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: 77a7706e39da265eedd65342a0ccf2174ab050ea
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853401"
---
# <a name="configure-datacenter-firewall-access-control-lists-acls"></a>Konfigurieren der Datacenter Firewall Zugriffssteuerungslisten (ACLs)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sobald Sie eine ACL erstellt und ein virtuelles Subnetz zugewiesen haben, empfiehlt es sich, diese Standard-ACL auf das virtuelle Subnetz mit der eine bestimmte ACL für eine einzelne Netzwerkschnittstelle außer Kraft zu setzen.  In diesem Fall wenden Sie spezielle ACLs, direkt auf Netzwerkschnittstellen, VLANs, anstelle des virtuellen Netzwerks. Wenn Sie die ACLs für das virtuelle Subnetz verbunden, die der Netzwerkschnittstelle festgelegt haben, werden beide ACLs werden angewendet und priorisiert die ACLs, die über die Zugriffssteuerungslisten für das virtuelle Subnetz der Netzwerkschnittstelle.

>[!IMPORTANT]
>Wenn Sie keine ACL erstellt und ein virtuelles Netzwerk zugewiesen haben, finden Sie unter [verwenden Zugriffssteuerungslisten (ACLs) zum Verwalten von Datencenter-Netzwerk fließt der Datenverkehr](Use-Access-Control-Lists--ACLs--to-Manage-Datacenter-Network-Traffic-Flow.md) eine ACL erstellen und zu einem virtuellen Subnetz zuweisen.  

In diesem Thema erfahren Sie, wie eine Netzwerkschnittstelle eine ACL hinzu. Wir zeigen auch, wie zum Entfernen einer ACL von einer Netzwerkschnittstelle, die mithilfe von Windows PowerShell und die Netzwerk-Controller-REST-API.

- [Beispiel: Hinzufügen einer ACL zu einer Netzwerkschnittstelle](#example-add-an-acl-to-a-network-interface)
- [Beispiel: Entfernen Sie eine ACL mithilfe von Windows Powershell und die Netzwerk-Controller-REST-API von einer Netzwerkschnittstelle](#example-remove-an-acl-from-a-network-interface-by-using-windows-powershell-and-the-network-controller-rest-api)


## <a name="example-add-an-acl-to-a-network-interface"></a>Beispiel: Hinzufügen einer ACL zu einer Netzwerkschnittstelle
In diesem Beispiel wir veranschaulicht, wie eine ACL zu einem virtuellen Netzwerk hinzufügen. 

>[!TIP]
>Es ist auch möglich, eine ACL gleichzeitig hinzuzufügen, die Sie die Netzwerkschnittstelle erstellen.

1. Rufen Sie aus, oder erstellen Sie die Netzwerkschnittstelle, die Sie die ACL hinzufügen möchten.
 
   ```PowerShell
   $nic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"
   ```
 
2. Rufen Sie aus, oder erstellen Sie die ACL, die Sie die Netzwerkschnittstelle hinzufügen möchten.
 
   ```PowerShell
   $acl = get-networkcontrolleraccesscontrollist -ConnectionUri $uri -resourceid "AllowAllACL"
   ```
 
3. Weisen Sie der ACL der AccessControlList-Objekt-Eigenschaft der Netzwerkschnittstelle
 
   ```PowerShell
    $nic.properties.ipconfigurations[0].properties.AccessControlList = $acl
   ```
 
4. Die Netzwerkschnittstelle im Netzwerkcontroller hinzufügen
 
   ```
   new-networkcontrollernetworkinterface -ConnectionUri $uri -Properties $nic.properties -ResourceId $nic.resourceid
   ```
 
## <a name="example-remove-an-acl-from-a-network-interface-by-using-windows-powershell-and-the-network-controller-rest-api"></a>Beispiel: Entfernen Sie eine ACL mithilfe von Windows Powershell und die Netzwerk-Controller-REST-API von einer Netzwerkschnittstelle
In diesem Beispiel erläutert, wie Sie eine ACL zu entfernen. Entfernt eine ACL wendet den Standardsatz von Regeln, die der Netzwerkschnittstelle. Der Standardsatz von Regeln können die gesamte ausgehenden Datenverkehr jedoch sämtlicher eingehenden Datenverkehr blockiert.

>[!NOTE]
>Wenn Sie alle eingehenden Datenverkehr zulassen möchten, müssen Sie die vorherige befolgen [Beispiel](#example-add-an-acl-to-a-network-interface) eine ACL hinzufügen, die sämtlichen eingehenden und den gesamten ausgehenden Datenverkehr zulässt.


1. Rufen Sie die ACL der Netzwerkschnittstelle aus, die Sie entfernen möchten.<br>
   ```PowerShell
   $nic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"
   ```
 
2. $NULL und die Eigenschaft AccessControlList-Objekt, von der IP-Konfiguration zuweisen.<br>
   ```PowerShell
   $nic.properties.ipconfigurations[0].properties.AccessControlList = $null
   ```
 
3. Fügen Sie das Netzwerkschnittstellenobjekt im Netzwerkcontroller hinzu.<br>
   ```PowerShell
   new-networkcontrollernetworkinterface -ConnectionUri $uri -Properties $nic.properties -ResourceId $nic.resourceid
   ```
