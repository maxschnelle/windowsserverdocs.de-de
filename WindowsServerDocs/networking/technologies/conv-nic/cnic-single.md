---
title: Zusammengeführte NIC-Konfiguration mit einem einzelnen Netzwerkadapter
description: In diesem Thema bieten wir Ihnen mit den Anweisungen zum Konfigurieren des zusammengeführten NIC mit einer einzelnen NIC in Ihrem Hyper-V-Host an.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: eed5c184-fa55-43a8-a879-b1610ebc70ca
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/14/2018
ms.openlocfilehash: 93d317534af46c87c4b2e874a5a5475687e2efa0
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447064"
---
# <a name="converged-nic-configuration-with-a-single-network-adapter"></a>Zusammengeführte NIC-Konfiguration mit einem einzelnen Netzwerkadapter

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema bieten wir Ihnen mit den Anweisungen zum Konfigurieren des zusammengeführten NIC mit einer einzelnen NIC in Ihrem Hyper-V-Host an.

Die Beispielkonfiguration in diesem Thema wird beschrieben, zwei Hyper-V-Hosts **Hyper-V-Host A**, und **Hyper-V-Host B**. Beide Hosts verfügen über eine einzelne physische NIC (pNIC) installiert, und die NICs verbunden sind, auf eine Top-of Rack \(ToR\) physischen Switch. Darüber hinaus die Hosts im gleichen Subnetz befinden sich auf die 192.168.1.x/24 ist.

![Hyper-V-Hosts](../../media/Converged-NIC/1-single-test-conn.jpg)


## <a name="step-1-test-the-connectivity-between-source-and-destination"></a>Schritt 1 Testen der Konnektivität zwischen Quelle und Ziel

Stellen Sie sicher, dass die physischen NIC auf dem Zielhost verbinden kann. Dieser Test zeigt die Verbindung mithilfe von Layer 3 \(L3\) - oder der IP-Schicht - sowie Layer 2 \(L2\).

1. Anzeigen von den Eigenschaften des Netzwerkadapters.

   ```PowerShell
   Get-NetAdapter
   ```

   _**Ergebnisse:** _  


   | Name |    InterfaceDescription     | ifIndex | Status |    MacAddress     | LinkSpeed |
   |------|-----------------------------|---------|--------|-------------------|-----------|
   |  M1  | Mellanox ConnectX-3 Pro... |    4    |   Nach oben   | 7C-FE-90-93-8F-A1 |  40 Gbit/s  |

   ---

2. Zeigen Sie zusätzliche Adapter-Eigenschaften, einschließlich der IP-Adresse an.

   ```PowerShell
   Get-NetAdapter M1 | fl *
   ```

   _**Ergebnisse:** _

   ```PowerShell   
    MacAddress   : 7C-FE-90-93-8F-A1
    Status   : Up
    LinkSpeed: 40 Gbps
    MediaType: 802.3
    PhysicalMediaType: 802.3
    AdminStatus  : Up
    MediaConnectionState : Connected
    DriverInformation: Driver Date 2016-08-28 Version 5.25.12665.0 NDIS 6.60
    DriverFileName   : mlx4eth63.sys
    NdisVersion  : 6.60
    ifOperStatus : Up
    ifAlias  : M1
    InterfaceAlias   : M1
    ifIndex  : 4
    ifDesc   : Mellanox ConnectX-3 Pro Ethernet Adapter
    ifName   : ethernet_32773
    DriverVersion: 5.25.12665.0
    LinkLayerAddress : 7C-FE-90-93-8F-A1
    Caption  :
    Description  :
    ElementName  :
    InstanceID   : {39B58B4C-8833-4ED2-A2FD-E105E7146D43}
    CommunicationStatus  :
    DetailedStatus   :
    HealthState  :
    InstallDate  :
    Name : M1
    OperatingStatus  :
    OperationalStatus:
    PrimaryStatus:
    StatusDescriptions   :
    AvailableRequestedStates :
    EnabledDefault   : 2
    EnabledState : 5
    OtherEnabledState:
    RequestedState   : 12
    TimeOfLastStateChange:
    TransitioningToState : 12
    AdditionalAvailability   :
    Availability :
    CreationClassName: MSFT_NetAdapter
   ``` 

## <a name="step-2-ensure-that-source-and-destination-can-communicate"></a>Schritt 2 Stellen Sie sicher, dass Quelle und Ziel kommunizieren kann

In diesem Schritt verwenden wir die **Test-NetConnection** Windows PowerShell-Befehl, doch wenn können Sie verwenden die **Ping** -Befehl, falls gewünscht. 

>[!TIP]
>Wenn Sie sicher sind, dass die Hosts miteinander kommunizieren können, können Sie diesen Schritt überspringen.

1. Überprüfen Sie die bidirektionale Kommunikation.

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

   _**Ergebnisse:** _


   |        Parameter         |    Wert    |
   |--------------------------|-------------|
   |       ComputerName       | 192.168.1.5 |
   |      RemoteAddress       | 192.168.1.5 |
   |      InterfaceAlias      |     M1      |
   |      SourceAddress       | 192.168.1.3 |
   |      PingSucceeded       |    True     |
   | PingReplyDetails \(RTT\) |    0 ms     |

   ---

   In einigen Fällen müssen Sie möglicherweise Windows-Firewall mit erweiterter Sicherheit dieser Test erfolgreich ausführen zu deaktivieren. Wenn Sie die Firewall deaktivieren, Bedenken Sie Sicherheit, und stellen Sie sicher, dass Ihre Konfiguration sicherheitsanforderungen Ihres Unternehmens erfüllt.

2. Deaktivieren Sie sämtliche Firewallprofile.

   ```PowerShell
   Set-NetFirewallProfile -All -Enabled False
   ```

3. Testen Sie nach der Deaktivierung der Firewall-Profilen die Verbindung erneut aus. 

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

   _**Ergebnisse:** _


   |        Parameter         |    Wert    |
   |--------------------------|-------------|
   |       ComputerName       | 192.168.1.5 |
   |      RemoteAddress       | 192.168.1.5 |
   |      InterfaceAlias      | Test-40G-1  |
   |      SourceAddress       | 192.168.1.3 |
   |      PingSucceeded       |    False    |
   | PingReplyDetails \(RTT\) |    0 ms     |

   ---



## <a name="step-3-optional-configure-the-vlan-ids-for-nics-installed-in-your-hyper-v-hosts"></a>Schritt 3 (Optional) Konfigurieren Sie die VLAN-IDs für Netzwerkadapter, die in Hyper-V-Hosts installiert

Viele Netzwerkkonfigurationen Verwenden von VLANs, und wenn Sie VLANs in Ihrem Netzwerk verwenden möchten, müssen Sie den vorherigen Test wiederholen, mit VLANs konfiguriert. Wenn Sie beabsichtigen, verwenden Sie RoCE für RDMA-Services müssen Sie außerdem VLANs aktivieren.

Für diesen Schritt werden die NICs im **Zugriff** Modus. Wenn Sie jedoch einen virtuellen Hyper-V-Switch erstellen \(vSwitch\) weiter unten in diesem Handbuch werden die VLAN-Eigenschaften auf der Portebene vSwitch angewendet. 

Da mehrere VLANs von ein Switch gehostet werden kann, ist es erforderlich für die Top-of-Rack \(ToR\) physischen Switch mit den Port verfügen, die mit der Host im Modus "Trunk" konfiguriert verbunden ist.

>[!NOTE]
>Anweisungen zum Konfigurieren des Modus "Trunk" auf dem Switch finden Sie in der Dokumentation Ihres ToR-Switch.

Die folgende Abbildung zeigt zwei Hyper-V-Hosts, jeweils mit einem physischen Netzwerkadapter, und jedes so konfiguriert, die auf VLAN 101 kommunizieren.

![Konfigurieren Sie die virtuelle lokale Netzwerke](../../media/Converged-NIC/2-single-configure-vlans.jpg)


>[!IMPORTANT]
>Führen Sie dies auf dem lokalen und den Zielserver aus. Wenn der Zielserver nicht mit derselben VLAN-ID wie der lokale Server konfiguriert ist, können nicht die beiden kommunizieren.


1. Konfigurieren Sie die VLAN-ID für die Netzwerkkarten in Hyper-V-Hosts installiert.

   >[!IMPORTANT]
   >Werden Sie mit diesem Befehl nicht ausgeführt, Sie an den Host Remote über diese Schnittstelle verbunden sind, da dies zum Verlust des Zugriffs auf den Host führt.

   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name M1 -RegistryKeyword VlanID -RegistryValue "101"
   Get-NetAdapterAdvancedProperty -Name M1 | Where-Object {$_.RegistryKeyword -eq "VlanID"} 
   ```

   _**Ergebnisse:** _


   | Name | DisplayName | DisplayValue | RegistryKeyword | RegistryValue |
   |------|-------------|--------------|-----------------|---------------|
   |  M1  |   VLAN-ID   |     101      |     VlanID      |     {101}     |

   ---

2. Starten Sie den Netzwerkadapter die VLAN ID. anwenden

   ```PowerShell
   Restart-NetAdapter -Name "M1"
   ```

3. Sicherstellen, dass der Status ist **einrichten**.

   ```PowerShell
   Get-NetAdapter -Name "M1"
   ```

   _**Ergebnisse:** _


   | Name |          InterfaceDescription           | ifIndex | Status |    MacAddress     | LinkSpeed |
   |------|-----------------------------------------|---------|--------|-------------------|-----------|
   |  M1  | Mellanox ConnectX-3 Pro-Ethernet-Ada... |    4    |   Nach oben   | 7C-FE-90-93-8F-A1 |  40 Gbit/s  |

   ---

   >[!IMPORTANT]
   >Es kann einige Sekunden für das Gerät neu starten und im Netzwerk verfügbar sind, dauern. 

4. Überprüfen Sie die Verbindung aus.<p>Bei einem Verbindungsfehler, überprüfen Sie den Switch VLAN-Konfiguration oder das Ziel Teilnahme im gleichen VLAN. 

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

## <a name="step-4-configure-quality-of-service-qos"></a>Schritt 4 Konfigurieren von Quality of Service \(QoS\)

>[!NOTE]
>Sie müssen alle der folgenden Schritte für DCB und QoS auf allen Hosts ausführen, die miteinander kommunizieren sollen.

1. Installieren der Data Center Bridging \(DCB\) auf jedem Hyper-V-Hosts.

   - **Optionale** für Netzwerkkonfigurationen, die iWarp für RDMA-Dienste verwenden.
   - **Erforderliche** für Netzwerkkonfigurationen, mit denen RoCE \(eine beliebige Version\) für RDMA-Dienste.

   ```PowerShell
   Install-WindowsFeature Data-Center-Bridging
   ```

2. Legen Sie die QoS-Richtlinien für SMB Direct an:

   - **Optionale** für Netzwerkkonfigurationen, iWarp zu verwenden.
   - **Erforderliche** für Netzwerkkonfigurationen, die RoCE verwenden.

   Im unten stehenden Beispielbefehl ist der Wert "3" willkürlich. Sie können einen beliebigen Wert zwischen 1 und 7 verwenden, solange Sie konsistent den gleichen Wert in der Konfiguration von QoS-Richtlinien verwenden.

   ```PowerShell
   New-NetQosPolicy "SMB" -NetDirectPortMatchCondition 445 -PriorityValue8021Action 3
   ```

   _**Ergebnisse:** _


   |   Parameter    |          Wert           |
   |----------------|--------------------------|
   |      Name      |           SMB            |
   |     Besitzer      | Eine Gruppenrichtlinie \(Computer\) |
   | NetworkProfile |           All            |
   |   Rangfolge   |           127            |
   |   JobObject    |          &nbsp;          |
   | NetDirectPort  |           445            |
   | PriorityValue  |            3             |

   ---

3. Aktivieren für RoCE Bereitstellungen **Priorität flusssteuerung** für SMB-Datenverkehr ist der nicht für iWarp erforderlich.

   ```PowerShell
   Enable-NetQosFlowControl -priority 3
   Get-NetQosFlowControl
   ```

   _**Ergebnisse:** _


   | Priority | Enabled | PolicySet | IfIndex | IfAlias |
   |----------|---------|-----------|---------|---------|
   |    0     |  False  |  Global   | &nbsp;  | &nbsp;  |
   |    1     |  False  |  Global   | &nbsp;  | &nbsp;  |
   |    2     |  False  |  Global   | &nbsp;  | &nbsp;  |
   |    3     |  True   |  Global   | &nbsp;  | &nbsp;  |
   |    4     |  False  |  Global   | &nbsp;  | &nbsp;  |
   |    5     |  False  |  Global   | &nbsp;  | &nbsp;  |
   |    6     |  False  |  Global   | &nbsp;  | &nbsp;  |
   |    7     |  False  |  Global   | &nbsp;  | &nbsp;  |

   ---

4. Aktivieren Sie QoS für die lokale und Ziel-Netzwerkadapter.

   - **Nicht erforderlich,** für Netzwerkkonfigurationen, iWarp zu verwenden.
   - **Erforderliche** für Netzwerkkonfigurationen, die RoCE verwenden.

   ```PowerShell
   Enable-NetAdapterQos -InterfaceAlias "M1"
   Get-NetAdapterQos -Name "M1"
   ```

   _**Ergebnisse:** _

   **Name**: M1  
   **Aktiviert**: True  

   _**Funktionen:** _   


   |      Parameter      |   Hardware   |   Aktuelle    |
   |---------------------|--------------|--------------|
   |    MacSecBypass     | NotSupported | NotSupported |
   |     DcbxSupport     |     Keine     |     Keine     |
   | NumTCs(Max/ETS/PFC) |    8/8/8     |    8/8/8     |

   ---

   _**OperationalTrafficClasses:** _ 


   | TC | TSA | Bandbreite | Prioritäten |
   |----|-----|-----------|------------|
   | 0  | ETS |    70%    |  0-2,4-7   |
   | 1  | ETS |    30 %    |     3      |

   ---

   _**OperationalFlowControl:** _  

   Priorität 3 aktiviert  

   _**OperationalClassifications:** _  


   | Protokoll  | Porttyp / | Priority |
   |-----------|-----------|----------|
   |  Default  |  &nbsp;   |    0     |
   | NetDirect |    445    |    3     |

   ---

5. Reservieren Sie einen Prozentsatz der Bandbreite für SMB Direct \(RDMA\).

    In diesem Beispiel wird eine bandbreitenreservierung 30 % verwendet. Sie sollten einen Wert auswählen, der darstellt, was Sie erwarten, dass Ihr Storage-Datenverkehr ist erforderlich. 

   ```PowerShell
   New-NetQosTrafficClass "SMB" -Priority 3 -BandwidthPercentage 30 -Algorithm ETS
   ```

   _**Ergebnisse:** _


   | Name | Algorithmus | Bandwidth(%) | Priority | PolicySet | IfIndex | IfAlias |
   |------|-----------|--------------|----------|-----------|---------|---------|
   | SMB  |    ETS    |      30      |    3     |  Global   | &nbsp;  | &nbsp;  |

   ---                                      

6. Zeigen Sie die bandbreiteneinstellungen für die Reservierung an.  

   ```PowerShell
   Get-NetQosTrafficClass
   ```

   _**Ergebnisse:** _


   |   Name    | Algorithmus | Bandwidth(%) | Priority | PolicySet | IfIndex | IfAlias |
   |-----------|-----------|--------------|----------|-----------|---------|---------|
   | [Standard] |    ETS    |      70      | 0-2,4-7  |  Global   | &nbsp;  | &nbsp;  |
   |    SMB    |    ETS    |      30      |    3     |  Global   | &nbsp;  | &nbsp;  |

   ---

## <a name="step-5-optional-resolve-the-mellanox-adapter-debugger-conflict"></a>Schritt 5 (Optional) Lösen Sie den Mellanox-Adapter-Debugger-Konflikt 

In der Standardeinstellung, wenn Sie einen Mellanox-Adapter verwenden blockiert der angefügte Debugger NetQos, dies ist ein bekanntes Problem. Wenn Sie einen Adapter aus Mellanox verwenden und einen Debugger anfügen möchten, verwenden Sie den folgenden Befehl Auflösen aus diesem Grund dieses Problem. Dieser Schritt ist nicht erforderlich, wenn Sie nicht beabsichtigen, die einen Debugger anfügen, oder wenn Sie nicht über einen Mellanox-Adapter verwenden.

   ```PowerShell    
   Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 –Force
   ``` 

## <a name="step-6-verify-the-rdma-configuration-native-host"></a>Schritt 6 Überprüfen Sie die RDMA-Konfiguration (Native Host)

Sie möchten sicherstellen, dass das Fabric vor einen vSwitch erstellen und auf RDMA (NIC konvergiert) ordnungsgemäß konfiguriert ist. 

Die folgende Abbildung zeigt den aktuellen Zustand des Hyper-V-Hosts.

![Test RDMA](../../media/Converged-NIC/4-single-test-rdma.jpg)

1. Überprüfen Sie die RDMA-Konfiguration.

   ```PowerShell
   Get-NetAdapterRdma
   ```
   _**Ergebnisse:** _


   | Name |           InterfaceDescription           | Enabled |
   |------|------------------------------------------|---------|
   |  M1  | Mellanox ConnectX-3 Pro-Ethernet-Adapter |  True   |

   ---

2. Bestimmen der **IfIndex** Wert der Ziel-Adapter.<p>Sie verwenden diesen Wert in den nachfolgenden Schritten aus, wenn Sie das Skript ausführen, die, das Sie herunterladen.

   ```PowerShell
   Get-NetIPConfiguration -InterfaceAlias "M*" | ft InterfaceAlias,InterfaceIndex,IPv4Address
   ```

   _**Ergebnisse:** _ 


   | InterfaceAlias | InterfaceIndex |  IPv4-Adresse  |
   |----------------|----------------|---------------|
   |       M2       |       14       | {192.168.1.5} |

   ---

3. Herunterladen der [DiskSpd.exe Hilfsprogramm](https://aka.ms/diskspd) und extrahieren Sie es in C:\TEST\.

4. Herunterladen der [Test-RDMA-Powershell-Skript](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1) in einem Testordner auf dem lokalen Laufwerk, z. B. C:\TEST\.

5. Führen Sie die **Test-Rdma.ps1** PowerShell-Skript für den IfIndex-Wert an das Skript, mit der IP-Adresse des remote-Adapters in demselben VLAN zu übergeben.<p>In diesem Beispiel leitet das Skript die **IfIndex** Wert 14 Remotenetzwerk Adapter IP-Adresse 192.168.1.5 erstellt.

   ```PowerShell
    C:\TEST\Test-RDMA.PS1 -IfIndex 14 -IsRoCE $true -RemoteIpAddress 192.168.1.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\

    VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\\diskspd.exe
    VERBOSE: The adapter M2 is a physical adapter
    VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
    VERBOSE: QoS/DCB/PFC configuration is correct.
    VERBOSE: RDMA configuration is correct.
    VERBOSE: Checking if remote IP address, 192.168.1.5, is reachable.
    VERBOSE: Remote IP 192.168.1.5 is reachable.
    VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
    VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 0 RDMA bytes sent per second
    VERBOSE: 662979201 RDMA bytes written per second
    VERBOSE: 37561021 RDMA bytes sent per second
    VERBOSE: 1023098948 RDMA bytes written per second
    VERBOSE: 8901349 RDMA bytes sent per second
    VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
    VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.1.5
   ```

   >[!NOTE]
   >Wenn der RDMA-Datenverkehr für den Fall RoCE insbesondere ein Fehler auftritt, finden Sie in Ihrer Konfiguration der ToR-Switch geeigneten PCF/ETS-Konfigurationseinstellungen, die die Einstellungen für den Host übereinstimmen sollten. Finden Sie in den QoS-Abschnitt in diesem Dokument Referenzwerte.

## <a name="step-7-remove-the-access-vlan-setting"></a>Schritt 7 Entfernen Sie die Access-VLAN-Einstellung

Wechseln Sie zur Vorbereitung für das Hyper-V erstellen, müssen Sie die VLAN-Einstellungen, die, denen Sie über installiert, entfernen.  

1. Entfernen Sie die ACCESS-VLAN-Einstellung über die physische NIC aus, um zu verhindern, dass die NIC automatische Kennzeichnung des ausgehende Datenverkehrs durch die falsche VLAN-ID.<p>Entfernen diese Einstellung verhindert, dass auch sie Filtern eingehender Datenverkehr, der mit die ACCESS-VLAN-ID übereinstimmt

   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name M1 -RegistryKeyword VlanID -RegistryValue "0"
   ```    

2. Überprüfen Sie, ob die **VLAN-Einstellung** wird die VLAN-ID-Wert als 0 (null).

   ```PowerShell    
   Get-NetAdapterAdvancedProperty -name m1 | Where-Object {$_.RegistryKeyword -eq 'VlanID'} 
   ```  


## <a name="step-8-create-a-hyper-v-vswitch-on-your-hyper-v-hosts"></a>Schritt 8. Erstellen Sie einen Hyper-V-Switchs auf den Hyper-V-hosts

Die folgende Abbildung zeigt die Hyper-V Host 1 mit einem vSwitch.

![Erstellen eines virtuellen Hyper-V-Switch](../../media/Converged-NIC/5-single-create-vswitch.jpg)


1. Erstellen Sie einen externen vSwitch für Hyper-V in Hyper-V auf Hyper-V-Host A. <p>In diesem Beispiel heißt der Switch VMSTEST. Außerdem wird der Parameter **AllowManagementOS** erstellt eine Host-vNIC, die erbt die Mac- und IP-Adressen der physischen NIC fest.

   ```PowerShell
   New-VMSwitch -Name VMSTEST -NetAdapterName "M1" -AllowManagementOS $true
   ```
   _**Ergebnisse:** _


   |  Name   | SwitchType |      NetAdapterInterfaceDescription      |
   |---------|------------|------------------------------------------|
   | VMSTEST |  Extern  | Mellanox ConnectX-3 Pro-Ethernet-Adapter |

   ---

2. Anzeigen von den Eigenschaften des Netzwerkadapters.

   ```PowerShell
   Get-NetAdapter | ft -AutoSize
   ```

   _**Ergebnisse:** _


   |         Name          |        InterfaceDescription         | ifIndex | Status |    MacAddress     | LinkSpeed |
   |-----------------------|-------------------------------------|---------|--------|-------------------|-----------|
   | vEthernet \(VMSTEST\) | Virtuelle Hyper-V-Ethernet-Adapter #2 |   27    |   Nach oben   | E4-1D-2D-07-40-71 |  40 Gbit/s  |

   ---

3. Verwalten Sie die Host-vNIC auf zwei Arten an. 

   - **NetAdapter** Ansicht funktioniert auf Grundlage der "vEthernet \(VMSTEST\)" Namen. In diesem Abschnitt werden nicht alle Eigenschaften des Netzwerkadapters angezeigt.
   - **VMNetworkAdapter** löscht das Präfix "vEthernet" und wird einfach der Vmswitch-Name verwendet. (Empfohlen) 

   ```PowerShell
   Get-VMNetworkAdapter –ManagementOS | ft -AutoSize
   ```

   _**Ergebnisse:** _


   |         Name         | IsManagementOs |        VMName        |  SwitchName  | MacAddress | Status | IP-Adressen |
   |----------------------|----------------|----------------------|--------------|------------|--------|-------------|
   | CORP-External-Switch |      True      | CORP-External-Switch | 001B785768AA |    {Ok}    | &nbsp; |             |
   |       VMSTEST        |      True      |       VMSTEST        | E41D2D074071 |    {Ok}    | &nbsp; |             |

   ---

4. Testen Sie die Verbindung ein.

   ```Powershell    
   Test-NetConnection 192.168.1.5
   ```

   _**Ergebnisse:** _ 

   ```
    ComputerName   : 192.168.1.5
    RemoteAddress  : 192.168.1.5
    InterfaceAlias : vEthernet (CORP-External-Switch)
    SourceAddress  : 192.168.1.3
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
   ```

5. Weisen Sie ein, und zeigen Sie die Einstellungen des Netzwerkadapters VLAN.

   ```PowerShell
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "VMSTEST" -VlanId "101" -Access -ManagementOS
   Get-VMNetworkAdapterVlan -ManagementOS -VMNetworkAdapterName "VMSTEST"
   ```    

   _**Ergebnisse:** _


   | VMName | VMNetworkAdapterName |  Modus  | VlanList |
   |--------|----------------------|--------|----------|
   | &nbsp; |       VMSTEST        | Zugriff |   101    |

   ---  

6. Testen Sie die Verbindung ein.<p>Es dauert ein paar Sekunden abgeschlossen werden, bevor Sie erfolgreich den andere Adapter pingen können.  

   ```PowerShell    
   Test-NetConnection 192.168.1.5
   ```

   _**Ergebnisse:** _

   ```
    ComputerName   : 192.168.1.5
    RemoteAddress  : 192.168.1.5
    InterfaceAlias : vEthernet (VMSTEST)
    SourceAddress  : 192.168.1.3
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
   ```

## <a name="step-9-test-hyper-v-virtual-switch-rdma-mode-2"></a>Schritt 9: Testen von virtuellen Hyper-V-Switch RDMA (Modus 2)

Die folgende Abbildung zeigt den aktuellen Zustand des Hyper-V-Hosts, einschließlich der vSwitch auf dem Hyper-V Host 1.

![Testen Sie den virtuellen Hyper-V-Switch](../../media/Converged-NIC/6-single-test-vswitch-rdma.jpg)


1. Festlegen der Priorität für die Host-vNIC markieren.

   ```PowerShell    
   Set-VMNetworkAdapter -ManagementOS -Name "VMSTEST" -IeeePriorityTag on
   Get-VMNetworkAdapter -ManagementOS -Name "VMSTEST" | fl Name,IeeePriorityTag
   ```  

   _**Ergebnisse:** _

    Name: VMSTEST IeeePriorityTag: On


2. Zeigen Sie den Netzwerkadapter RDMA-Informationen. 

   ```PowerShell
   Get-NetAdapterRdma
   ```   

   _**Ergebnisse:** _


   |         Name          |        InterfaceDescription         | Enabled |
   |-----------------------|-------------------------------------|---------|
   | vEthernet \(VMSTEST\) | Virtuelle Hyper-V-Ethernet-Adapter #2 |  False  |

   ---

   >[!NOTE]
   >Wenn der Parameter **aktiviert** hat den Wert **"false"** , dies bedeutet, dass RDMA nicht aktiviert ist.


3. Zeigen Sie Informationen zum Netzwerkadapter an.

   ```PowerShell
   Get-NetAdapter
   ```

   _**Ergebnisse:** _   


   |        Name         |        InterfaceDescription         | ifIndex | Status |    MacAddress     | LinkSpeed |
   |---------------------|-------------------------------------|---------|--------|-------------------|-----------|
   | vEthernet (VMSTEST) | Virtuelle Hyper-V-Ethernet-Adapter #2 |   27    |   Nach oben   | E4-1D-2D-07-40-71 |  40 Gbit/s  |

   ---


4. Aktivieren Sie RDMA auf dem Host-vNIC ein.

   ```PowerShell
   Enable-NetAdapterRdma -Name "vEthernet (VMSTEST)"
   Get-NetAdapterRdma -Name "vEthernet (VMSTEST)"
   ```

   _**Ergebnisse:** _


   |         Name          |        InterfaceDescription         | Enabled |
   |-----------------------|-------------------------------------|---------|
   | vEthernet \(VMSTEST\) | Virtuelle Hyper-V-Ethernet-Adapter #2 |  True   |

   ---

   >[!NOTE]
   >Wenn der Parameter **aktiviert** hat den Wert **"true"** , dies bedeutet, dass RDMA aktiviert ist.

5. RDMA-Datenverkehr Test ausführen.

   ```PowerShell    
    C:\TEST\Test-RDMA.PS1 -IfIndex 27 -IsRoCE $true -RemoteIpAddress 192.168.1.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
    VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\\diskspd.exe
    VERBOSE: The adapter vEthernet (VMSTEST) is a virtual adapter
    VERBOSE: Retrieving vSwitch bound to the virtual adapter
    VERBOSE: Found vSwitch: VMSTEST
    VERBOSE: Found the following physical adapter(s) bound to vSwitch: TEST-40G-1
    VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
    VERBOSE: QoS/DCB/PFC configuration is correct.
    VERBOSE: RDMA configuration is correct.
    VERBOSE: Checking if remote IP address, 192.168.1.5, is reachable.
    VERBOSE: Remote IP 192.168.1.5 is reachable.
    VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
    VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 0 RDMA bytes sent per second
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 0 RDMA bytes sent per second
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 0 RDMA bytes sent per second
    VERBOSE: 0 RDMA bytes written per second
    VERBOSE: 9162492 RDMA bytes sent per second
    VERBOSE: 938797258 RDMA bytes written per second
    VERBOSE: 34621865 RDMA bytes sent per second
    VERBOSE: 933572610 RDMA bytes written per second
    VERBOSE: 35035861 RDMA bytes sent per second
    VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
    VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.1.5
   ```

Die letzte Zeile in dieser Ausgabe ist "RDMA-Datenverkehr Test erfolgreich: RDMA-Datenverkehr wurde an 192.168.1.5 erstellt, gesendet"zeigt, dass Sie erfolgreich Converged NIC auf dem Adapter konfiguriert haben.

## <a name="related-topics"></a>Verwandte Themen
- [Zusammengeführte NIC in einem Team verwendete NIC-Konfiguration](cnic-datacenter.md)
- [Konfiguration der physischen Switch für zusammengeführte NIC](cnic-app-switch-config.md)
- [Problembehandlung bei Converged NIC-Konfigurationen](cnic-app-troubleshoot.md)
