---
title: Konfiguration des physischen Switches für konvergierte NIC
description: In diesem Thema erhalten Sie Richtlinien für die Konfiguration physischer Switches.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 6d53c797-fb67-4b9e-9066-1c9a8b76d2aa
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/14/2018
ms.openlocfilehash: 8d227098fb23b233b416cb9342a15d6d4ca0699e
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87520219"
---
# <a name="physical-switch-configuration-for-converged-nic"></a>Konfiguration des physischen Switches für konvergierte NIC

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erhalten Sie Richtlinien für die Konfiguration physischer Switches.

Dabei handelt es sich nur um Befehle und deren Verwendung. Sie müssen die Ports, mit denen die NICs verbunden sind, in Ihrer Umgebung bestimmen.

>[!IMPORTANT]
>Stellen Sie sicher, dass die VLAN-und die No-Drop-Richtlinie für die Priorität festgelegt ist, über die SMB konfiguriert ist

## <a name="arista-switch-dcs-7050s-64-eos-4137m"></a>Arista Switch \( DCS \- 7050s \- 64, EOS \- 4.13.7 m\)

1.  \(zum Admin-Modus wechseln, in der Regel nach einem Kennwort gefragt werden\)
2.  Konfiguration \( , die in den Konfigurations Modus eingegeben werden soll\)
3.  Ausführung anzeigen \( zeigt die aktuell laufende Konfiguration an\)
4.  Suchen Sie die Switchports, mit denen die NICs verbunden sind. In diesem Beispiel lauten Sie 14/1, 15/1, 16/1, 17/1.
5.  int 1, 16/1, 16/1, 17/1, \( in den Konfigurations Modus für diese Ports.\)
6.  dcbx-Modus IEEE
7.  Prioritäts Fluss-Steuerungs Modus für
8.  Switchport-trunk natives VLAN 225
9.  Switchport-trunk zulässige VLAN 100-225
10. switchportmodus-trunk
11. Prioritäts Fluss-Steuerungs Priorität 3 nicht ablegen
12. QoS Trust COS
13. ausführen anzeigen \( Überprüfen Sie, ob die Konfiguration auf den Ports ordnungsgemäß eingerichtet ist\)
14. WR \( , damit die Einstellungen über den switchneustart beibehalten werden\)

### <a name="tips"></a>Tipps:
1.  Nein #Command # negiert einen Befehl.
2.  Vorgehensweise beim Hinzufügen eines neuen VLANs: int VLAN 100 \( if Storage Network on VLAN 100\)
3.  Überprüfen vorhandener VLANs: VLAN anzeigen
4.  Weitere Informationen zum Konfigurieren des Arista-Switchs finden Sie online nach: Arista EOS Manual
5.  Verwenden Sie diesen Befehl, um die PFC-Einstellungen zu überprüfen: Details der Prioritäts Fluss-Steuerungs Zähler anzeigen

## <a name="dell-switch-s4810-ftos-99-00"></a>Dell Switch \( S4810, f: 9,9 \( 0,0\)\)

```
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
```

## <a name="cisco-switch-nexus-3132-version-602u61"></a>Cisco Switch \( Nexus 3132, Version 6,0 \( 2, \) U6 \( 1\)\)

### <a name="global"></a>Global

```
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
```

### <a name="port-specific"></a>Port spezifisch

```
    switchport mode trunk
    switchport trunk native vlan 99
    switchport trunk allowed vlan 99,2000,2050   çuse VLANs that already exists
    spanning-tree port type edge
    flowcontrol receive on (not supported with PFC in Cisco NX-OS)
    flowcontrol send on (not supported with PFC in Cisco NX-OS)
    no shutdown
    priority-flow-control mode on
```

## <a name="related-topics"></a>Zugehörige Themen

- [Konvergierte NIC-Konfiguration mit einem einzelnen Netzwerk Adapter](cnic-single.md)
- [Konvergierte NIC-Konfiguration mit Nic](cnic-datacenter.md)
- [Problembehandlung bei zusammen getauschten NIC](cnic-app-troubleshoot.md)
