---
title: Konfigurieren von Zugriffssteuerungslisten für die Rechenzentrumsfirewall
description: Sie können bestimmte ACLs auf Netzwerkschnittstellen anwenden.  Wenn ACLs auch für das virtuelle Subnetz festgelegt sind, mit dem die Netzwerkschnittstelle verbunden ist, werden beide ACLs angewendet, aber die ACLs der Netzwerkschnittstelle sind oberhalb der ACLs des virtuellen Subnetzes priorisiert.
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 25f18927-a63e-44f3-b02a-81ed51933187
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/23/2018
ms.openlocfilehash: f6b1078f88b2d377c3c49934e2b1bd219641d82e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854563"
---
# <a name="configure-datacenter-firewall-access-control-lists-acls"></a>Konfigurieren von Rechenzentrums Firewall-Access Control Listen (ACLs)

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Nachdem Sie eine ACL erstellt und einem virtuellen Subnetz zugewiesen haben, können Sie diese Standard-ACL im virtuellen Subnetz mit einer bestimmten Zugriffs Steuerungs Liste für eine einzelne Netzwerkschnittstelle außer Kraft setzen.  In diesem Fall wenden Sie bestimmte ACLs direkt auf Netzwerkschnittstellen an, die an VLANs angefügt sind, anstelle des virtuellen Netzwerks. Wenn Sie ACLs für das virtuelle Subnetz festgelegt haben, das mit der Netzwerkschnittstelle verbunden ist, werden beide Zugriffs Steuerungs Listen angewendet und priorisiert die ACLs der Netzwerkschnittstelle oberhalb der ACLs des virtuellen Subnetzes.

>[!IMPORTANT]
>Wenn Sie keine ACL erstellt und einem virtuellen Netzwerk zugewiesen haben, finden Sie weitere Informationen unter [Verwenden von Access Control Listen (ACLs) zum Verwalten des Netzwerk Datenverkehrs für Daten Center](Use-Access-Control-Lists--ACLs--to-Manage-Datacenter-Network-Traffic-Flow.md) , um eine ACL zu erstellen und Sie einem virtuellen Subnetz zuzuweisen.  

In diesem Thema erfahren Sie, wie Sie einer Netzwerkschnittstelle eine ACL hinzufügen. Wir zeigen Ihnen außerdem, wie Sie eine ACL mithilfe von Windows PowerShell und der Rest-API des Netzwerk Controllers aus einer Netzwerkschnittstelle entfernen.

- [Beispiel: Hinzufügen einer ACL zu einer Netzwerkschnittstelle](#example-add-an-acl-to-a-network-interface)
- [Beispiel: Entfernen einer ACL aus einer Netzwerkschnittstelle mithilfe von Windows PowerShell und der Netzwerk Controller-Rest-API](#example-remove-an-acl-from-a-network-interface-by-using-windows-powershell-and-the-network-controller-rest-api)


## <a name="example-add-an-acl-to-a-network-interface"></a>Beispiel: Hinzufügen einer ACL zu einer Netzwerkschnittstelle
In diesem Beispiel wird veranschaulicht, wie Sie einem virtuellen Netzwerk eine ACL hinzufügen. 

>[!TIP]
>Es ist auch möglich, eine ACL hinzuzufügen, wenn Sie die Netzwerkschnittstelle erstellen.

1. Rufen Sie die Netzwerkschnittstelle ab, der Sie die ACL hinzufügen möchten, oder erstellen Sie Sie.
 
   ```PowerShell
   $nic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"
   ```
 
2. Rufen Sie die ACL ab, die Sie der Netzwerkschnittstelle hinzufügen, oder erstellen Sie Sie.
 
   ```PowerShell
   $acl = get-networkcontrolleraccesscontrollist -ConnectionUri $uri -resourceid "AllowAllACL"
   ```
 
3. Zuweisen der ACL zur AccessControlList-Eigenschaft der Netzwerkschnittstelle
 
   ```PowerShell
    $nic.properties.ipconfigurations[0].properties.AccessControlList = $acl
   ```
 
4. Hinzufügen der Netzwerkschnittstelle im Netzwerk Controller
 
   ```
   new-networkcontrollernetworkinterface -ConnectionUri $uri -Properties $nic.properties -ResourceId $nic.resourceid
   ```
 
## <a name="example-remove-an-acl-from-a-network-interface-by-using-windows-powershell-and-the-network-controller-rest-api"></a>Beispiel: Entfernen einer ACL aus einer Netzwerkschnittstelle mithilfe von Windows PowerShell und der Netzwerk Controller-Rest-API
In diesem Beispiel erfahren Sie, wie Sie eine ACL entfernen. Durch das Entfernen einer ACL wird der Standardsatz von Regeln auf die Netzwerkschnittstelle angewendet. Der Standardsatz von Regeln ermöglicht den gesamten ausgehenden Datenverkehr, blockiert jedoch den gesamten eingehenden Datenverkehr.

>[!NOTE]
>Wenn Sie den gesamten eingehenden Datenverkehr zulassen möchten, müssen Sie dem vorherigen [Beispiel](#example-add-an-acl-to-a-network-interface) folgen, um eine ACL hinzuzufügen, die den gesamten eingehenden und ausgehenden Datenverkehr zulässt.


1. Holen Sie sich die Netzwerkschnittstelle, von der Sie die ACL entfernen.<br>
   ```PowerShell
   $nic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"
   ```
 
2. Weisen Sie $NULL der AccessControlList-Eigenschaft der ipconfiguration zu.<br>
   ```PowerShell
   $nic.properties.ipconfigurations[0].properties.AccessControlList = $null
   ```
 
3. Fügen Sie das Netzwerkschnittstellen Objekt im Netzwerk Controller hinzu.<br>
   ```PowerShell
   new-networkcontrollernetworkinterface -ConnectionUri $uri -Properties $nic.properties -ResourceId $nic.resourceid
   ```
