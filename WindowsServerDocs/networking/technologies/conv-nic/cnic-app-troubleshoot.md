---
title: Problembehandlung bei zusammengeführten NIC-Konfigurationen
description: Dieses Thema ist Teil der zusammengeführten NIC Konfiguration Anleitung für Windows Server2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0bc6746f-2adb-43d8-a503-52f473833164
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 373ecd9b9fff62aaabd8caa176ff091ec98ad81c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="troubleshooting-converged-nic-configurations"></a>Problembehandlung bei zusammengeführten NIC-Konfigurationen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Das folgende Skript können Sie überprüfen, ob die RDMA-Konfiguration auf dem Hyper-V-Host korrekt ist.

- [Skript Test-Rdma ps1 herunterladen](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1)

Sie können auch die folgenden Windows PowerShell-Befehle verwenden, Problembehandlung und Überprüfen der Konfiguration Ihrer zusammengeführten NICs.

## <a name="get-netadapterrdma"></a>Get-NetAdapterRdma

Um RDMA Konfiguration des Netzwerkadapters zu überprüfen, führen Sie den folgenden Windows PowerShell-Befehl auf dem Hyper-V-Server.

    
    Get-NetAdapterRdma | fl *
    

Sie können die folgenden erwarteten und unerwarteten Ergebnissen identifizieren und beheben Probleme, nachdem Sie diesen Befehl auf dem Hyper-V-Host ausführen.

### <a name="get-netadapterrdma-expected-results"></a>Get-NetAdapterRdma erwartete Ergebnisse

Host-vNIC und die physische NIC anzeigen Nicht-NULL-RDMA-Funktion.

![Windows PowerShell, die erwarteten Ergebnisse](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-01.jpg)

### <a name="get-netadapterrdma-unexpected-results"></a>Get-NetAdapterRdma unerwartete Ergebnisse

Führen Sie die folgenden Schritteaus, wenn Sie unerwartete Ergebnisse, beim Ausführen erhalten der **Get-NetAdapterRdma** Befehl.

1. Stellen Sie sicher, dass die Mlnx Miniport und Mlnx-Bus-Treiber neuesten sind. Verwenden für Mellanox mindestens 42 löschen. 
2. Überprüfen Sie, ob Mlnx Miniport und Bus-Treiber durch Überprüfen der Version des Treibers über den Geräte-Manager entsprechen. Der Bustreiber finden Sie im System-Geräte. Der Name sollte mit Mellanox Connect-X-3 PRO VPI beginnen, wie in der Eigenschaften des Netzwerkadapters im folgenden Screenshot dargestellt.

![Eigenschaften des Netzwerkadapters](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-02.jpg)

4. Stellen Sie sicher, dass auf dem physischen NIC und die Host-vNIC Network Direct (RDMA) aktiviert ist.
5. Stellen Sie sicher, dass vSwitch über den geeigneten physischen Adapter erstellt wird, indem Sie die RDMA-Funktionen überprüfen.
6. Überprüfen Sie Nachrichtendatei Systemprotokoll und Filtern Sie nach der Quelle "Hyper-V-VmSwitch".

## <a name="get-smbclientnetworkinterface"></a>SmbClientNetworkInterface abrufen

Als einen zusätzlichen Schritt, die RDMA-Konfiguration zu überprüfen führen Sie den folgenden Windows PowerShell-Befehl auf dem Hyper-V-Server.


    Get SmbClientNetworkInterface

### <a name="get-smbclientnetworkinterface-expected-results"></a>Rufen Sie SmbClientNetworkInterface erwartete Ergebnisse

Die Host-vNIC sollte als RDMA-fähigen aus Sicht des SMB-auch angezeigt werden.

![Eigenschaften des Netzwerkadapters](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-03.jpg)


### <a name="get-smbclientnetworkinterface-unexpected-results"></a>Abrufen von SmbClientNetworkInterface unerwartete Ergebnisse

1. Stellen Sie sicher, dass die Mlnx Miniport und Mlnx-Bus-Treiber neuesten sind. Verwenden für Mellanox mindestens 42 löschen. 
2. Überprüfen Sie, ob Mlnx Miniport und Bus-Treiber durch Überprüfen der Version des Treibers über den Geräte-Manager entsprechen. Der Bustreiber finden Sie im System-Geräte. Der Name sollte mit Mellanox Connect-X-3 PRO VPI beginnen, wie in der Eigenschaften des Netzwerkadapters im folgenden Screenshot dargestellt.
3. Stellen Sie sicher, dass auf dem physischen NIC und die Host-vNIC Network Direct (RDMA) aktiviert ist.
4. Stellen Sie sicher, dass der virtuelle Hyper-V-Switch über den geeigneten physischen Adapter erstellt wird, durch die RDMA-Funktionen überprüfen.
5. Überprüfen der Nachrichtendatei Protokolle für "SMB-Client" in **und Webdienste | Microsoft | Windows**.

## <a name="get-netadapterqos"></a>Get-NetAdapterQos

Sie können die Netzwerk-Adapter Qualität der Dienstkonfiguration \(QoS\) anzeigen, indem Sie den folgenden Windows PowerShell-Befehl ausführen.

    Get-NetAdapterQos

### <a name="get-netadapterqos-expected-results"></a>Get-NetAdapterQos erwartete Ergebnisse

Prioritäten und Datenverkehrsklassen sollen gemäß der erste Konfigurationsschritt angezeigt werden, die Sie mithilfe dieses Handbuchs ausgeführt.

![Quality of Serviceprioritäten und Klassen](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-04.jpg)

### <a name="get-netadapterqos-unexpected-results"></a>Get-NetAdapterQos unerwartete Ergebnisse

Wenn Ihre Ergebnisse unerwartete sind, führen Sie die folgenden Schritteaus.

1. Stellen Sie sicher, dass der physische Netzwerkadapter \(DCB\) Data Center Bridging und QoS unterstützt
2. Stellen Sie sicher, dass der Netzwerkadapter-Treiber auf dem neuesten Stand sind.


## <a name="get-smbmultichannelconnection"></a>Get-SmbMultiChannelConnection

Die folgenden Windows PowerShell-Befehl können Sie überprüfen, ob die IP-Adresse des Knotens RDMA\-fähig ist.

    Get-SmbMultiChannelConnection


### <a name="get-smbmultichannelconnection-expected-results"></a>Get-SmbMultiChannelConnection erwartete Ergebnisse

Des Knotens für den Remote-IP-Adresse wird als RDMA fähig angezeigt.

![RDMA-fähigen Remoteknoten IP-Adresse](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-05.jpg)

### <a name="get-smbmultichannelconnection-unexpected-results"></a>Get-SmbMultiChannelConnection unerwartete Ergebnisse

Wenn Ihre Ergebnisse unerwartete sind, führen Sie die folgenden Schritteaus.

1. Stellen Sie sicher, dass Ping beides funktioniert.
2. Stellen Sie sicher, dass die Firewall blockiert nicht SMB-Verbindung initiieren. Aktivieren Sie genauer gesagt die Firewallregel für SMB Direct Port 5445 für iWARP und 445 für ROCE.

## <a name="get-smbclientnetworkinterface"></a>Get-SmbClientNetworkInterface

Den folgenden Befehl können Sie überprüfen, ob die virtuelle Netzwerkkarte, die Sie für RDMA aktiviert als RDMA\-fähigen SMB gemeldet wird.

    Get-SmbClientNetworkInterface


### <a name="get-smbclientnetworkinterface-expected-results"></a>Get-SmbClientNetworkInterface erwartete Ergebnisse

Virtuelle Netzwerkkarte, die für RDMA aktiviert wurde, muss als RDMA-fähig durch SMB betrachtet werden.

![SMB meldet, dass die NICs RDMA-fähig sind.](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-06.jpg)

### <a name="get-smbclientnetworkinterface-unexpected-results"></a>Get-SmbClientNetworkInterface unerwartete Ergebnisse

Wenn Ihre Ergebnisse unerwartete sind, führen Sie die folgenden Schritteaus.

1. Stellen Sie sicher, dass Ping beides funktioniert.
2. Sicherstellen Sie, dass die Firewall Initiierung der SMB-Verbindung nicht blockiert wird.

## <a name="vstat-mellanox-specific"></a>Vstat \(Mellanox specific\)

Wenn Sie Mellanox-Netzwerkadapter verwenden, können Sie mithilfe der **Vstat** Befehl aus, um die RDMA über Ethernet zusammengeführten \(RoCE\) Version auf Hyper-V-Knoten zu überprüfen.

### <a name="vstat-expected-results"></a>Vstat erwartete Ergebnisse

Die Version RoCE auf beiden Knoten muss identisch sein. Dies ist auch eine gute Möglichkeit, stellen Sie sicher, dass die Firmwareversion auf beiden Knoten neuesten ist.

![Beispiele für RoCE Version Kontrollkästchen Ergebnis](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-07.jpg)

### <a name="vstat-unexpected-results"></a>Vstat unerwartete Ergebnisse

Wenn Ihre Ergebnisse unerwartete sind, führen Sie die folgenden Schritteaus.

1. Festlegen Sie richtige RoCE Version mit Set-MlnxDriverCoreSetting
2. Installieren Sie die neueste Firmware von Mellanox-Website.


## <a name="perfmon-counters"></a>Perfmon-Leistungsindikatoren

Sie können Leistungsindikatoren im Systemmonitor Überprüfen der Konfiguration die RDMA-Aktivität überprüfen.

![Performance Monitor Ergebnis Beispiele](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-08.jpg)

## <a name="all-topics-in-this-guide"></a>Alle Themen in diesem Handbuch

Dieses Handbuch enthält die folgenden Themen.

- [Zusammengeführtes NIC-Konfiguration mit einem einzelnen Netzwerkadapter](cnic-single.md)
- [Zusammengeführtes NIC kombinierten NIC-Konfiguration](cnic-datacenter.md)
- [Physischen Switch-Konfiguration für die zusammengeführten NIC](cnic-app-switch-config.md)
- [Problembehandlung bei zusammengeführten NIC-Konfigurationen](cnic-app-troubleshoot.md)
