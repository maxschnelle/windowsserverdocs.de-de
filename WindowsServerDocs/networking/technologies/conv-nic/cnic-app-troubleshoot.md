---
title: Problembehandlung bei Converged NIC-Konfigurationen
description: Dieses Thema ist Teil des zusammengeführten NIC Configuration Guide für Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0bc6746f-2adb-43d8-a503-52f473833164
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3004ff9d6fe874410c24d174755a6d26f99f8f2a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59876481"
---
# <a name="troubleshooting-converged-nic-configurations"></a>Problembehandlung bei Converged NIC-Konfigurationen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können das folgende Skript verwenden, um zu überprüfen, ob die RDMA-Konfiguration auf dem Hyper-V-Host korrekt ist.

- [Download script Test-Rdma.ps1](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1)

Sie können auch die folgenden Windows PowerShell-Befehle verwenden, Problembehandlung, und überprüfen die Konfiguration Ihrer zusammengeführten NICs.

## <a name="get-netadapterrdma"></a>Get-NetAdapterRdma

Um RDMA Konfiguration des Netzwerkadapters zu überprüfen, führen Sie den folgenden Windows PowerShell-Befehl auf dem Hyper-V-Server aus.

    
    Get-NetAdapterRdma | fl *
    

Sie können die folgende erwartete und unerwartete Ergebnisse beim Identifizieren und beheben Probleme, nach dem Ausführen dieses Befehls auf dem Hyper-V-Host verwenden.

### <a name="get-netadapterrdma-expected-results"></a>Get-NetAdapterRdma erwartete Ergebnisse

Zeigen RDMA-Funktionen nicht 0 (null), Host-vNIC und der physischen NIC.

![Windows PowerShell erwartet-Ergebnissen](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-01.jpg)

### <a name="get-netadapterrdma-unexpected-results"></a>Get-NetAdapterRdma unerwartete Ergebnisse

Führen Sie die folgenden Schritte aus, wenn Sie unerwartete Ergebnisse, beim Ausführen erhalten der **Get-NetAdapterRdma** Befehl.

1. Stellen Sie sicher, dass die Mlnx Miniport und Mlnx Busfahrer neueste sind. Verwendung für Mellanox mindestens 42 löschen. 
2. Überprüfen Sie, ob Mlnx Miniport und Bus Treiber übereinstimmen, durch Überprüfen der Version des Treibers durch den Geräte-Manager. Die Bus-Treiber finden Sie in der System-Geräten. Der Name sollte mit Mellanox Connect-X-3 PRO VPI beginnen, wie im folgenden Screenshot der Eigenschaften des Netzwerkadapters dargestellt.

![Netzwerkadaptereigenschaften](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-02.jpg)

4. Stellen Sie sicher, dass auf die physische NIC und die Host-vNIC Network Direct (RDMA) aktiviert ist.
5. Stellen Sie sicher, dass vSwitch über den geeigneten physischen Adapter erstellt wird, durch die RDMA-Funktionen aktivieren.
6. Überprüfen Sie Systemprotokoll der Ereignisanzeige (eventviewer) und Filtern Sie nach "Hyper-V-VmSwitch"-Quelle.

--- 

## <a name="get-smbclientnetworkinterface"></a>Get-SmbClientNetworkInterface

Einem zusätzlichen Schritt, um die RDMA-Konfiguration zu überprüfen führen Sie den folgenden Windows PowerShell-Befehl auf dem Hyper-V-Server aus.


    Get-SmbClientNetworkInterface

### <a name="get-smbclientnetworkinterface-expected-results"></a>Get-SmbClientNetworkInterface erwartete Ergebnisse

Die Host-vNIC sollte auch die SMB-hinsichtlich wie RDMA-fähig angezeigt werden.

![Netzwerkadaptereigenschaften](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-03.jpg)


### <a name="get-smbclientnetworkinterface-unexpected-results"></a>Get-SmbClientNetworkInterface unerwartete Ergebnisse

1. Stellen Sie sicher, dass die Mlnx Miniport und Mlnx Busfahrer neueste sind. Verwendung für Mellanox mindestens 42 löschen. 
2. Überprüfen Sie, ob Mlnx Miniport und Bus Treiber übereinstimmen, durch Überprüfen der Version des Treibers durch den Geräte-Manager. Die Bus-Treiber finden Sie in der System-Geräten. Der Name sollte mit Mellanox Connect-X-3 PRO VPI beginnen, wie im folgenden Screenshot der Eigenschaften des Netzwerkadapters dargestellt.
3. Stellen Sie sicher, dass auf die physische NIC und die Host-vNIC Network Direct (RDMA) aktiviert ist.
4. Stellen Sie sicher, dass der Hyper-V-Switch über den geeigneten physischen Adapter erstellt wird, durch die RDMA-Funktionen aktivieren.
5. Überprüfen der Protokolle der Ereignisanzeige (eventviewer) für "SMB-Client" in **und Anwendungsdienste | Microsoft | Windows**.

--- 

## <a name="get-netadapterqos"></a>Get-NetAdapterQos

Sehen Sie die Netzwerk-Adapter Dienstqualität \(QoS\) Konfiguration durch den folgenden Windows PowerShell-Befehl ausführen.

    Get-NetAdapterQos

### <a name="get-netadapterqos-expected-results"></a>Get-NetAdapterQos expected results

Prioritäten und Datenverkehrsklassen soll gemäß der erste Konfigurationsschritt angezeigt werden, die Sie mithilfe dieses Handbuchs ausgeführt.

![Quality of Serviceprioritäten und Klassen](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-04.jpg)

### <a name="get-netadapterqos-unexpected-results"></a>Get-NetAdapterQos unexpected results

Führen Sie die folgenden Schritte aus, wenn unerwartete die Ergebnisse sind.

1. Stellen Sie sicher, dass der physische Netzwerkadapter Data Center Bridging unterstützt \(DCB\) und QoS
2. Stellen Sie sicher, dass die Netzwerkadaptertreiber auf dem neuesten Stand sind.

--- 

## <a name="get-smbmultichannelconnection"></a>Get-SmbMultiChannelConnection

Sie können den folgenden Windows PowerShell-Befehl überprüfen, ob die IP-Adresse dem Remoteknoten RDMA ist\-kann.

    Get-SmbMultiChannelConnection


### <a name="get-smbmultichannelconnection-expected-results"></a>Get-SmbMultiChannelConnection erwartete Ergebnisse

Remote IP-Adresse wird als RDMA fähig angezeigt.

![RDMA-fähigen Remoteknoten IP-Adresse](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-05.jpg)

### <a name="get-smbmultichannelconnection-unexpected-results"></a>Get-SmbMultiChannelConnection unerwartete Ergebnisse

Führen Sie die folgenden Schritte aus, wenn unerwartete die Ergebnisse sind.

1. Stellen Sie sicher, dass Ping in beide Richtungen funktioniert.
2. Stellen Sie sicher, dass die Initiierung der SMB-Verbindung nicht in der Firewall blockiert wird. Aktivieren Sie insbesondere die Firewallregel für SMB Direct Port 5445 für iWARP und 445 für ROCE.

--- 

## <a name="get-smbclientnetworkinterface"></a>Get-SmbClientNetworkInterface

Sie können den folgenden Befehl aus, stellen Sie sicher, dass die virtuelle NIC für RDMA als RDMA gemeldet wird aktiviert\-von SMB kann.

    Get-SmbClientNetworkInterface


### <a name="get-smbclientnetworkinterface-expected-results"></a>Get-SmbClientNetworkInterface erwartete Ergebnisse

Virtuelle Netzwerkkarte, die für RDMA aktiviert wurde muss als RDMA-fähig SMB sichtbar sind.

![SMB gibt an, dass NICs RDMA-fähig sind.](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-06.jpg)

### <a name="get-smbclientnetworkinterface-unexpected-results"></a>Get-SmbClientNetworkInterface unerwartete Ergebnisse

Führen Sie die folgenden Schritte aus, wenn unerwartete die Ergebnisse sind.

1. Stellen Sie sicher, dass Ping in beide Richtungen funktioniert.
2. Stellen Sie sicher, dass die Initiierung der SMB-Verbindung nicht durch Firewall blockiert wird.

--- 

## <a name="vstat-mellanox-specific"></a>Vstat \(Mellanox-spezifisch\)

Wenn Sie Mellanox-Adapter verwenden, können Sie mithilfe der **Vstat** Befehl aus, um die RDMA over Converged Ethernet überprüfen \(RoCE\) -Version in Hyper-V-Knoten.

### <a name="vstat-expected-results"></a>Vstat erwartete Ergebnisse

Die Version RoCE auf beiden Knoten muss identisch sein. Dies ist auch eine gute Möglichkeit, um sicherzustellen, dass die Firmwareversion auf beiden Knoten aktuell ist.

![Ergebnis-Beispiele für RoCE Version überprüfen](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-07.jpg)

### <a name="vstat-unexpected-results"></a>Vstat unerwartete Ergebnisse

Führen Sie die folgenden Schritte aus, wenn unerwartete die Ergebnisse sind.

1. Legen Sie die richtige RoCE-Version, die mithilfe von Set-MlnxDriverCoreSetting
2. Installieren Sie die neueste Firmware von Mellanox-Website.

--- 

## <a name="perfmon-counters"></a>Perfmon-Leistungsindikatoren

Sie können die Leistungsindikatoren im Systemmonitor, um zu überprüfen, ob die RDMA-Aktivität, der Ihre Konfiguration überprüfen.

![Beispiele für die Performance Monitor-Ergebnis](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-08.jpg)

--- 

## <a name="related-topics"></a>Verwandte Themen

- [Zusammengeführte NIC-Konfiguration mit einem einzelnen Netzwerkadapter](cnic-single.md)
- [Zusammengeführte NIC in einem Team verwendete NIC-Konfiguration](cnic-datacenter.md)
- [Konfiguration der physischen Switch für zusammengeführte NIC](cnic-app-switch-config.md)

---
