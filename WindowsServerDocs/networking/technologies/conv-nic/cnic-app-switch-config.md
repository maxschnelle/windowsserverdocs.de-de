---
title: Physischen Switch-Konfiguration für zusammengeführte NIC
description: In diesem Thema bieten wir Richtlinien für den physischen Switches konfigurieren.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 6d53c797-fb67-4b9e-9066-1c9a8b76d2aa
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/14/2018
ms.openlocfilehash: e31d7b83fee84d9055d938f77b49389205786244
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829401"
---
# <a name="physical-switch-configuration-for-converged-nic"></a>Physischen Switch-Konfiguration für zusammengeführte NIC

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema bieten wir Richtlinien für den physischen Switches konfigurieren. 


Dies sind nur für Befehle und deren Verwendung. Sie müssen die Ports, mit denen die NICs verbunden sind, in Ihrer Umgebung bestimmen. 

>[!IMPORTANT]
>Stellen Sie sicher, dass das VLAN und nicht ablegen-Richtlinie festgelegt ist, für die Priorität, die über den SMB konfiguriert ist.

## <a name="arista-switch-dcs-7050s-64-eos-4137m"></a>Arista Switch \(Dcs\-7050s\-64, EOS\-4.13.7M\)

1.  En \(wechseln Sie zur Administratormodus, in der Regel nach einem Kennwort gefragt.\)
2.  Config \(in den Konfigurationsmodus eingeben\)
3.  Anzeigen der Ausführung \(zeigt aktuell ausgeführte Konfiguration\)
4.  Erfahren Sie, Switch-Ports, die mit denen Ihre NICs verbunden sind. Im folgenden Beispiel sind sie 14/1,15/1,16/1,17/1.
5.  Int-Eth 14/1,15/1,16/1,17/1 \(Geben Sie in der Config-Modus für diese Ports\)
6.  Dcbx Modus ieee
7.  flusspriorisierung Modus auf
8.  Switchport native Trunk-Vlan 225
9.  Switchport "Trunk" zulässige Vlan 100 bis 225
10. Switchport im Modus "Trunk"
11. Priorität der flusssteuerung Priorität 3 keine Ablage
12. QoS vertrauen, cos
13. Anzeigen der Ausführung \(stellen Sie sicher, dass die Konfiguration ist die Einrichtung ordnungsgemäß an den Ports\)
14. WR \(, stellen die Einstellungen weiterhin besteht, über den Switch-Neustart\)

### <a name="tips"></a>Tipps:
1.  Keine #Command # negiert ein Befehls
2.  Gewusst wie: Hinzufügen ein neues VLAN: Int Vlan 100 \(Speichernetzwerk ist auf VLAN 100\)
3.  So prüfen Sie vorhandene VLANs: Anzeigen von Vlan
4.  Weitere Informationen zum Konfigurieren von Arista Switch, suchen Sie online nach: Arista EOS manuell
5.  Mit diesem Befehl können Sie um PCF-Einstellungen zu überprüfen: flusspriorisierung Leistungsindikatoren Details anzeigen

--- 

## <a name="dell-switch-s4810-ftos-99-00"></a>Dell-Switch \(S4810, FTOS 9.9 \(0,0\)\)

    
    !
    dcb enable
    ! put pfc control on qos class 3
    configure
    dcb-map dcb-smb
    priority group 0 bandwidth 90 pfc on
    priority group 1 bandwidth 10 pfc off
    priority-pgid 1 1 1 0 1 1 1 1
    exit
    ! apply map to ports 0-31
    configure
    interface range ten 0/0-31
    dcb-map dcb-smb
    exit
    
--- 

## <a name="cisco-switch-nexus-3132-version-602u61"></a>Cisco-Switch \(Nexus 3132, Version 6.0\(2\)U6\(1\)\)

### <a name="global"></a>Global
    
    class-map type qos match-all RDMA
    match cos 3
    class-map type queuing RDMA
    match qos-group 3
    policy-map type qos QOS_MARKING
    class RDMA
    set qos-group 3
    class class-default
    policy-map type queuing QOS_QUEUEING
    class type queuing RDMA
    bandwidth percent 50
    class type queuing class-default
    bandwidth percent 50
    class-map type network-qos RDMA
    match qos-group 3
    policy-map type network-qos QOS_NETWORK
    class type network-qos RDMA
    mtu 2240
    pause no-drop
    class type network-qos class-default
    mtu 9216
    system qos
    service-policy type qos input QOS_MARKING
    service-policy type queuing output QOS_QUEUEING
    service-policy type network-qos QOS_NETWORK
    

### <a name="port-specific"></a>Bestimmte Ports

    
    switchport mode trunk
    switchport trunk native vlan 99
    switchport trunk allowed vlan 99,2000,2050   çuse VLANs that already exists
    spanning-tree port type edge
    flowcontrol receive on (not supported with PFC in Cisco NX-OS)
    flowcontrol send on (not supported with PFC in Cisco NX-OS)
    no shutdown
    priority-flow-control mode on
    
--- 

## <a name="related-topics"></a>Verwandte Themen

- [Zusammengeführte NIC-Konfiguration mit einem einzelnen Netzwerkadapter](cnic-single.md)
- [Zusammengeführte NIC in einem Team verwendete NIC-Konfiguration](cnic-datacenter.md)
- [Problembehandlung bei Converged NIC-Konfigurationen](cnic-app-troubleshoot.md)

--- 