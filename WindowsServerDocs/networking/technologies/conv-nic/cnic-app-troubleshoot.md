---
title: Problembehandlung bei zusammen getauschten NIC
description: Dieses Thema ist Teil des konvergierten NIC-Konfigurations Handbuchs für Windows Server 2016.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 0bc6746f-2adb-43d8-a503-52f473833164
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 90021956ebe85ec2f4abfea0aaafd96daebfd82f
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87520209"
---
# <a name="troubleshooting-converged-nic-configurations"></a>Problembehandlung bei zusammen getauschten NIC

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Mithilfe des folgenden Skripts können Sie überprüfen, ob die RDMA-Konfiguration auf dem Hyper-V-Host korrekt ist.

- [Skript Test-Rdma.ps1herunterladen](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1)

Sie können auch die folgenden Windows PowerShell-Befehle verwenden, um die Konfiguration der konvergierten NICs zu beheben und die Konfiguration zu überprüfen.

## <a name="get-netadapterrdma"></a>Get-netadapterrdma

Führen Sie den folgenden Windows PowerShell-Befehl auf dem Hyper-V-Server aus, um die RDMA-Konfiguration des Netzwerkadapters zu überprüfen.

```powershell
Get-NetAdapterRdma | fl *
```

Wenn Sie diesen Befehl auf dem Hyper-V-Host ausführen, können Sie die folgenden erwarteten und unerwarteten Ergebnisse verwenden, um Probleme zu identifizieren und zu beheben.

### <a name="get-netadapterrdma-expected-results"></a>Ergebnisse von "Get-netadapterrdma" erwartet

Host-vNIC und die physische NIC zeigen RDMA-Funktionen, die nicht NULL sind.

![Erwartete Ergebnisse von Windows PowerShell](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-01.jpg)

### <a name="get-netadapterrdma-unexpected-results"></a>Unerwartete Ergebnisse von "Get-netadapterrdma"

Führen Sie die folgenden Schritte aus, wenn Sie beim Ausführen des Befehls **Get-netadapterrdma** unerwartete Ergebnisse erhalten.

1. Stellen Sie sicher, dass die mlnx Mini Port-und mlnx-Bustreiber aktuell sind. Verwenden Sie für Mellanox mindestens Drop 42.
2. Überprüfen Sie, ob mlnx Mini Port-und Bustreiber Stimmen, indem Sie die Treiber Version über Geräte-Manager überprüfen. Der Bustreiber befindet sich in System Geräten. Der Name sollte mit Mellanox Connect-X 3 pro VPI beginnen, wie im folgenden Screenshot der Netzwerkadapter Eigenschaften veranschaulicht.

![Netzwerkadaptereigenschaften](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-02.jpg)

4. Stellen Sie sicher, dass Netzwerk Direct (RDMA) sowohl auf der physischen NIC als auch auf der Host-vNIC aktiviert ist.
5. Stellen Sie sicher, dass Vswitch über den richtigen physischen Adapter erstellt wird, indem Sie die RDMA-Funktionen überprüfen.
6. Überprüfen Sie das Ereignis Viewer-System Protokoll, und Filtern Sie nach der Quelle "Hyper-V-VMSwitch".

## <a name="get-smbclientnetworkinterface"></a>Get-smbclientnetworkinterface

Um die RDMA-Konfiguration zu überprüfen, führen Sie den folgenden Windows PowerShell-Befehl auf dem Hyper-V-Server aus.

```powershell
Get-SmbClientNetworkInterface
```

### <a name="get-smbclientnetworkinterface-expected-results"></a>Erwartete Ergebnisse von "Get-smbclientnetworkinterface"

Die Host-vNIC sollte auch als RDMA-fähig aus der Perspektive von SMB angezeigt werden.

![Netzwerkadaptereigenschaften](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-03.jpg)

### <a name="get-smbclientnetworkinterface-unexpected-results"></a>Unerwartete Ergebnisse von "Get-smbclientnetworkinterface"

1. Stellen Sie sicher, dass die mlnx Mini Port-und mlnx-Bustreiber aktuell sind. Verwenden Sie für Mellanox mindestens Drop 42.
2. Überprüfen Sie, ob mlnx Mini Port-und Bustreiber Stimmen, indem Sie die Treiber Version über Geräte-Manager überprüfen. Der Bustreiber befindet sich in System Geräten. Der Name sollte mit Mellanox Connect-X 3 pro VPI beginnen, wie im folgenden Screenshot der Netzwerkadapter Eigenschaften veranschaulicht.
3. Stellen Sie sicher, dass Netzwerk Direct (RDMA) sowohl auf der physischen NIC als auch auf der Host-vNIC aktiviert ist.
4. Stellen Sie sicher, dass der virtuelle Hyper-V-Switch über den richtigen physischen Adapter erstellt wird, indem Sie seine RDMA-Funktionen überprüfen.
5. Überprüfen der Ereignisanzeige Protokolle für "SMB-Client" in der **Anwendung und in den Diensten | Microsoft | Windows**.

## <a name="get-netadapterqos"></a>Get-netadapterqos

Sie können die Quality of Service QoS-Konfiguration des Netzwerkadapters anzeigen, \( \) indem Sie den folgenden Windows PowerShell-Befehl ausführen.

```powershell
Get-NetAdapterQos
```

### <a name="get-netadapterqos-expected-results"></a>Ergebnisse von "Get-netadapterqos" erwartet

Die Prioritäten und die Datenverkehrs Klassen sollten gemäß dem ersten Konfigurationsschritt angezeigt werden, den Sie mit diesem Handbuch ausgeführt haben.

![Quality of Service-Prioritäten und-Klassen](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-04.jpg)

### <a name="get-netadapterqos-unexpected-results"></a>Unerwartete Ergebnisse von "Get-netadapterqos"

Wenn die Ergebnisse unerwartet ausfallen, führen Sie die folgenden Schritte aus.

1. Stellen Sie sicher, dass der physische Netzwerkadapter Rechenzentrums Bridging \( DCB \) und QoS unterstützt.
2. Stellen Sie sicher, dass die Treiber für Netzwerkadapter auf dem neuesten Stand sind.

## <a name="get-smbmultichannelconnection"></a>Get-smbmultichannelconnection

Mit dem folgenden Windows PowerShell-Befehl können Sie überprüfen, ob die IP-Adresse des Remote Knotens RDMA- \- fähig ist.

```powershell
Get-SmbMultiChannelConnection
```

### <a name="get-smbmultichannelconnection-expected-results"></a>Ergebnisse von "Get-smbmultichannelconnection" erwartet

Die IP-Adresse des Remote Knotens wird als RDMA-fähig angezeigt.

![RDMA-fähige Remote Knoten-IP-Adresse](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-05.jpg)

### <a name="get-smbmultichannelconnection-unexpected-results"></a>Unerwartete Ergebnisse von "Get-smbmultichannelconnection"

Wenn die Ergebnisse unerwartet ausfallen, führen Sie die folgenden Schritte aus.

1. Stellen Sie sicher, dass Ping auf beide Arten funktioniert.
2. Stellen Sie sicher, dass die Firewall keine SMB-Verbindungs Initiierung blockiert. Aktivieren Sie insbesondere die Firewallregel für den SMB Direct-Port 5445 für IWarp und 445 für ROCE.

## <a name="get-smbclientnetworkinterface"></a>Get-smbclientnetworkinterface

Mit dem folgenden Befehl können Sie überprüfen, ob die für RDMA aktivierte virtuelle NIC als RDMA- \- fähig von SMB gemeldet wird.

```powershell
Get-SmbClientNetworkInterface
```

### <a name="get-smbclientnetworkinterface-expected-results"></a>Erwartete Ergebnisse von "Get-smbclientnetworkinterface"

Die für RDMA aktivierte virtuelle NIC muss von SMB als RDMA-fähig betrachtet werden.

![SMB meldet, dass NICs RDMA-fähig sind.](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-06.jpg)

### <a name="get-smbclientnetworkinterface-unexpected-results"></a>Unerwartete Ergebnisse von "Get-smbclientnetworkinterface"

Wenn die Ergebnisse unerwartet ausfallen, führen Sie die folgenden Schritte aus.

1. Stellen Sie sicher, dass Ping auf beide Arten funktioniert.
2. Stellen Sie sicher, dass die Firewall keine SMB-Verbindungs Initiierung blockiert.

## <a name="vstat-mellanox-specific"></a>vstat \( Mellanox-spezifisch\)

Wenn Sie Mellanox-Netzwerkadapter verwenden, können Sie den **vstat** -Befehl verwenden, um die RDMA over converdown Ethernet \( ROCE- \) Version auf Hyper-V-Knoten zu überprüfen.

### <a name="vstat-expected-results"></a>erwartete vstat-Ergebnisse

Die ROCE-Version auf beiden Knoten muss identisch sein. Dies ist auch eine gute Möglichkeit, um zu überprüfen, ob die Firmwareversion auf beiden Knoten aktuell ist.

![Beispiele für die Überprüfung der ROCE-Version](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-07.jpg)

### <a name="vstat-unexpected-results"></a>unerwartete vstat-Ergebnisse

Wenn die Ergebnisse unerwartet ausfallen, führen Sie die folgenden Schritte aus.

1. Festlegen der korrekten ROCE-Version mithilfe von "Set-mlnxdrivercoresesetting"
2. Installieren Sie die neueste Firmware von der Mellanox-Website.

## <a name="perfmon-counters"></a>Perfmon-Leistungsindikatoren

Sie können die Leistungsindikatoren im System Monitor überprüfen, um die RDMA-Aktivität Ihrer Konfiguration zu überprüfen.

![System Monitor-Ergebnis Beispiele](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-08.jpg)

## <a name="related-topics"></a>Zugehörige Themen

- [Konvergierte NIC-Konfiguration mit einem einzelnen Netzwerk Adapter](cnic-single.md)
- [Konvergierte NIC-Konfiguration mit Nic](cnic-datacenter.md)
- [Konfiguration des physischen Switches für konvergierte NIC](cnic-app-switch-config.md)
