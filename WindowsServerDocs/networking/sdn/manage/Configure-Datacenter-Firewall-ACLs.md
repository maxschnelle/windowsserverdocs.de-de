---
title: Konfigurieren von Zugriffssteuerungslisten (ACLs) für Datacenter Firewall
description: Dieses Thema ist Teil der Software Defined Networking-Anleitung für zum Verwalten von Mandantenworkloads und virtuellen Netzwerken in Windows Server2016.
manager: brianlic
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
ms.openlocfilehash: d5f7c4baad24a720e073857cb6c835167e5b419b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="configure-datacenter-firewall-access-control-lists-acls"></a>Konfigurieren von Zugriffssteuerungslisten (ACLs) für Datacenter Firewall

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können bestimmte ACLs auf Netzwerkschnittstellen anwenden.  Wenn ACLs auch für das virtuelle Subnetz festgelegt sind mit denen die Netzwerkschnittstelle verbunden ist, sowohl ACLs angewendet werden, aber die Netzwerkschnittstelle ACLs über das virtuelle Subnetz ACLs priorisiert werden.

Dieses Thema enthält die folgenden Abschnitte.

- [Beispiel: Hinzufügen einer ACL zu einer Netzwerkschnittstelle](#bkmk_addacl)
- [Beispiel: Entfernen einer ACL aus einer Netzwerkschnittstelle mithilfe von Windows Powershell und der Netzwerk-Controller-REST-API](#bkmk_removeacl)

##<a name="bkmk_addacl"></a>Beispiel: Hinzufügen einer ACL zu einer Netzwerkschnittstelle

Im Thema [verwenden Zugriffssteuerungslisten (ACLs) zum Verwalten von Netzwerkdatenverkehrsflusses](Use-Access-Control-Lists--ACLs--to-Manage-Datacenter-Network-Traffic-Flow.md) haben Sie gelernt, eine ACL zu erstellen und ein virtuelles Subnetz zuweisen.  In einigen Fällen jedoch, möchten Sie, die standardmäßig die ACL im Subnetz Virtaul mit einer bestimmten ACL für eine einzelne Netzwerkschnittstelle außer Kraft zu setzen.  Sie müssen auch ACLs direkt auf Netzwerkschnittstellen anwenden, die mit VLANs anstelle von virtuellen Netzwerken verbunden sind.

In diesem Beispiel wird veranschaulicht, wie ein virtuelles Netzwerk eine ACL hinzugefügt. 

>[!NOTE]
>Es ist auch möglich, eine ACL auf einmal hinzufügen, die Sie die Netzwerkschnittstelle erstellen.

###<a name="step-1-get-or-create-the-network-interface-to-which-you-will-add-the-acl"></a>Schritt 1: Rufen Sie ab oder erstellen Sie die Netzwerkschnittstelle, die Sie die ACL hinzufügen möchten

    $nic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"

###<a name="step-2-get-or-create-the-acl-you-will-add-to-the-network-interface"></a>Schritt 2: Rufen Sie ab oder erstellen Sie die ACL, die Sie die Netzwerkschnittstelle hinzufügen möchten
Befehl im folgenden Beispiel können Sie abrufen oder die ACL zu erstellen. 

    $acl = get-networkcontrolleraccesscontrollist -ConnectionUri $uri -resourceid "AllowAllACL"

###<a name="step-3-assign-the-acl-to-the-accesscontrollist-property-of-the-network-interface"></a>Schritt 3: Zuweisen der ACL der AccessControlList-Eigenschaft der Netzwerkschnittstelle
Befehl im folgenden Beispiel können Sie die ACL der AccessControlList-Eigenschaft zuweisen.

    $nic.properties.ipconfigurations[0].properties.AccessControlList = $acl

###<a name="step-4-add-the-network-interface-in-network-controller"></a>Schritt 4: Hinzufügen der Netzwerkschnittstelle in Netzwerk-Controller
Befehl im folgenden Beispiel können die Netzwerkschnittstelle in Netzwerk-Controller hinzu.

    new-networkcontrollernetworkinterface -ConnectionUri $uri -Properties $nic.properties -ResourceId $nic.resourceid


##<a name="bkmk_removeacl"></a>Beispiel: Entfernen einer ACL aus einer Netzwerkschnittstelle mithilfe von Windows Powershell und der Netzwerk-Controller-REST-API
Sie können in diesem Beispiel wird eine ACL entfernt werden soll. Wenn Sie eine ACL entfernen, der Standardsatz von Regeln gelten für die Netzwerkschnittstelle.

Die Standardgruppe von Regeln ermöglicht der gesamte ausgehenden Datenverkehr jedoch blockiert alle eingehenden Datenverkehr.

>[!NOTE]
>Wenn Sie alle eingehenden Datenverkehr zulassen möchten, müssen Sie im vorherige Beispiel um eine ACL hinzuzufügen, alle eingehenden und alle ausgehenden Datenverkehr zulässt, befolgen.

###<a name="step-1-get-the-network-interface-from-which-you-will-remove-the-acl"></a>Schritt 1: Abrufen der Netzwerkschnittstelle, die von der Sie die ACL entfernt werden soll
Befehl im folgenden Beispiel können Sie die Netzwerkschnittstelle abzurufen.

    $nic = get-networkcontrollernetworkinterface -ConnectionUri $uri -ResourceId "MyVM_Ethernet1"

###<a name="step-2-assign-null-to-the-accesscontrollist-property-of-the-ipconfiguration"></a>Schritt 2: Die AccessControlList-Eigenschaft der IPKonfigurationsdateiAddress $NULL zuweisen
Befehl im folgenden Beispiel können Sie die Eigenschaft AccessControlList $NULL zuweisen.

    $nic.properties.ipconfigurations[0].properties.AccessControlList = $null

###<a name="step-3-add-the-network-interface-object-in-network-controller"></a>Schritt 3: Hinzufügen der Schnittstelle Netzwerkobjekt in Netzwerk-Controller
Befehl im folgenden Beispiel können Sie das Netzwerkschnittstellen-Objekt in Netzwerkcontroller hinzufügen,

    new-networkcontrollernetworkinterface -ConnectionUri $uri -Properties $nic.properties -ResourceId $nic.resourceid

