---
title: Konvergierte NIC-Konfiguration mit einem einzelnen Netzwerkadapter
description: In diesem Thema erhalten Sie die Anweisungen zum Konfigurieren einer konvergierten NIC mit einer einzelnen NIC auf dem Hyper-V-Host.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: eed5c184-fa55-43a8-a879-b1610ebc70ca
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/14/2018
ms.openlocfilehash: 5a088df043190de9e7f1df4dccdc2fc832751093
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80309623"
---
# <a name="converged-nic-configuration-with-a-single-network-adapter"></a>Konvergierte NIC-Konfiguration mit einem einzelnen Netzwerkadapter

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erhalten Sie die Anweisungen zum Konfigurieren einer konvergierten NIC mit einer einzelnen NIC auf dem Hyper-V-Host.

In der Beispielkonfiguration in diesem Thema werden zwei Hyper-v-Hosts, **Hyper-v-Host a**und **Hyper-v-Host B**beschrieben. Beide Hosts verfügen über eine einzige physische NIC (PNIC), und die NICs sind mit einem oberen \(Tor\) physischen Switch verbunden. Außerdem befinden sich die Hosts im gleichen Subnetz, d. h. 192.168.1. x/24.

![Hyper-V-Hosts](../../media/Converged-NIC/1-single-test-conn.jpg)


## <a name="step-1-test-the-connectivity-between-source-and-destination"></a>Schritt 1 Testen der Konnektivität zwischen Quelle und Ziel

Stellen Sie sicher, dass die physische NIC eine Verbindung mit dem Zielhost herstellen kann. In diesem Test wird die Konnektivität durch die Verwendung von Layer 3 \(L3\) oder der IP-Schicht sowie von Layer 2 \(L2-\)veranschaulicht.

1. Zeigen Sie die Eigenschaften des Netzwerkadapters an.

   ```PowerShell
   Get-NetAdapter
   ```

   _**Folgen**_  


   | Name |    Interfacedescription     | ifIndex | Status |    MacAddress     | LinkSpeed |
   |------|-----------------------------|---------|--------|-------------------|-----------|
   |  M1  | Mellanox ConnectX-3 pro... |    4    |   Nach oben   | 7C-FE-90-93-8F-a1 |  40 Gbit/s  |

   ---

2. Anzeigen zusätzlicher Adapter Eigenschaften, einschließlich der IP-Adresse.

   ```PowerShell
   Get-NetAdapter M1 | fl *
   ```

   _**Folgen**_

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

## <a name="step-2-ensure-that-source-and-destination-can-communicate"></a>Schritt 2 Stellen Sie sicher, dass Quelle und Ziel kommunizieren können

In diesem Schritt verwenden wir den Windows PowerShell-Befehl " **Test-NetConnection** ", aber wenn Sie dies bevorzugen, können Sie den **ping** -Befehl verwenden. 

>[!TIP]
>Wenn Sie sicher sind, dass Ihre Hosts miteinander kommunizieren können, können Sie diesen Schritt überspringen.

1. Überprüfen Sie die bidirektionale Kommunikation.

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

   _**Folgen**_


   |        Parameter         |    Wert    |
   |--------------------------|-------------|
   |       Computername       | 192.168.1.5 erstellt |
   |      RemoteAddress       | 192.168.1.5 erstellt |
   |      InterfaceAlias      |     M1      |
   |      SourceAddress       | 192.168.1.3 |
   |      Pingerfolg       |    True     |
   | Pingreplydetails \(RTT-\) |    0 ms     |

   ---

   In einigen Fällen müssen Sie möglicherweise die Windows-Firewall mit erweiterter Sicherheit deaktivieren, damit dieser Test erfolgreich durchgeführt werden kann. Wenn Sie die Firewall deaktivieren, sollten Sie die Sicherheit berücksichtigen und sicherstellen, dass Ihre Konfiguration die Sicherheitsanforderungen Ihrer Organisation erfüllt.

2. Deaktivieren Sie alle Firewallprofile.

   ```PowerShell
   Set-NetFirewallProfile -All -Enabled False
   ```

3. Nachdem Sie die Firewallprofile deaktiviert haben, testen Sie die Verbindung erneut. 

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

   _**Folgen**_


   |        Parameter         |    Wert    |
   |--------------------------|-------------|
   |       Computername       | 192.168.1.5 erstellt |
   |      RemoteAddress       | 192.168.1.5 erstellt |
   |      InterfaceAlias      | Test-40G-1  |
   |      SourceAddress       | 192.168.1.3 |
   |      Pingerfolg       |    False    |
   | Pingreplydetails \(RTT-\) |    0 ms     |

   ---



## <a name="step-3-optional-configure-the-vlan-ids-for-nics-installed-in-your-hyper-v-hosts"></a>Schritt 3: Optionale Konfigurieren der VLAN-IDs für NICs, die auf Ihren Hyper-V-Hosts installiert sind

Bei vielen Netzwerkkonfigurationen werden VLANs verwendet, und wenn Sie beabsichtigen, VLANs in Ihrem Netzwerk zu verwenden, müssen Sie den vorherigen Test mit konfigurierten VLANs wiederholen. Wenn Sie die Verwendung von ROCE für RDMA-Dienste planen, müssen Sie VLANs auch aktivieren.

Bei diesem Schritt befinden sich die NICs im **Zugriffs** Modus. Wenn Sie jedoch einen virtuellen Hyper-V-Switch \(Vswitch später in diesem Handbuch\) erstellen, werden die VLAN-Eigenschaften auf der Vswitch-Port Ebene angewendet. 

Da ein Switch mehrere VLANs hosten kann, ist es erforderlich, dass der obere Bereich \(Tor\) physischen Switch den Port hat, mit dem der Host verbunden ist, der im trunk Modus konfiguriert ist.

>[!NOTE]
>In der Tor-switchdokumentation finden Sie Anweisungen zum Konfigurieren des trunk Modus auf dem Switch.

Die folgende Abbildung zeigt zwei Hyper-V-Hosts mit jeweils einem physischen Netzwerkadapter, die jeweils für die Kommunikation mit VLAN 101 konfiguriert sind.

![Konfigurieren von virtuellen lokalen Netzwerken](../../media/Converged-NIC/2-single-configure-vlans.jpg)


>[!IMPORTANT]
>Führen Sie dies auf dem lokalen Server und auf dem Zielserver aus. Wenn der Zielserver nicht mit derselben VLAN-ID wie der lokale Server konfiguriert ist, können die beiden nicht miteinander kommunizieren.


1. Konfigurieren Sie die VLAN-ID für NICs, die auf Ihren Hyper-V-Hosts installiert sind.

   >[!IMPORTANT]
   >Führen Sie diesen Befehl nicht aus, wenn Sie eine Remote Verbindung mit dem Host über diese Schnittstelle herstellen, da dies zu einem Verlust des Zugriffs auf den Host führt.

   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name M1 -RegistryKeyword VlanID -RegistryValue "101"
   Get-NetAdapterAdvancedProperty -Name M1 | Where-Object {$_.RegistryKeyword -eq "VlanID"} 
   ```

   _**Folgen**_


   | Name | DisplayName | Display value | Registryschlüsselwort | REGISTRYVALUE |
   |------|-------------|--------------|-----------------|---------------|
   |  M1  |   VLAN-ID   |     101      |     VlanID      |     {101}     |

   ---

2. Starten Sie den Netzwerkadapter neu, um die VLAN-ID anzuwenden.

   ```PowerShell
   Restart-NetAdapter -Name "M1"
   ```

3. Stellen **Sie sicher,** dass der Status "aktiv"

   ```PowerShell
   Get-NetAdapter -Name "M1"
   ```

   _**Folgen**_


   | Name |          Interfacedescription           | ifIndex | Status |    MacAddress     | LinkSpeed |
   |------|-----------------------------------------|---------|--------|-------------------|-----------|
   |  M1  | Mellanox ConnectX-3 pro Ethernet Ada... |    4    |   Nach oben   | 7C-FE-90-93-8F-a1 |  40 Gbit/s  |

   ---

   >[!IMPORTANT]
   >Es kann einige Sekunden dauern, bis das Gerät neu gestartet und im Netzwerk verfügbar wird. 

4. Überprüfen Sie die Konnektivität.<p>Wenn eine Verbindung nicht hergestellt werden kann, überprüfen Sie die Switch-VLAN-Konfiguration oder die Ziel Teilnahme im gleichen VLAN. 

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

## <a name="step-4-configure-quality-of-service-qos"></a>Schritt 4 Konfigurieren von Quality of Service \(QoS\)

>[!NOTE]
>Sie müssen alle der folgenden DCB-und QoS-Konfigurationsschritte auf allen Hosts ausführen, die miteinander kommunizieren sollen.

1. Installieren Sie Data Center Bridging \(DCB-\) auf den einzelnen Hyper-V-Hosts.

   - **Optional** für Netzwerkkonfigurationen, die IWarp für RDMA-Dienste verwenden.
   - **Erforderlich** für Netzwerkkonfigurationen, die ROCE-\(beliebige Versions\) für RDMA-Dienste verwenden.

   ```PowerShell
   Install-WindowsFeature Data-Center-Bridging
   ```

2. Legen Sie die QoS-Richtlinien für SMB-Direct fest:

   - **Optional** für Netzwerkkonfigurationen, die IWarp verwenden.
   - **Erforderlich** für Netzwerkkonfigurationen, die ROCE verwenden.

   Im folgenden Beispiel Befehl ist der Wert "3" beliebig. Sie können einen beliebigen Wert zwischen 1 und 7 verwenden, solange Sie während der Konfiguration der QoS-Richtlinien einheitlich denselben Wert verwenden.

   ```PowerShell
   New-NetQosPolicy "SMB" -NetDirectPortMatchCondition 445 -PriorityValue8021Action 3
   ```

   _**Folgen**_


   |   Parameter    |          Wert           |
   |----------------|--------------------------|
   |      Name      |           SMB            |
   |     Owner      | Gruppenrichtlinie \(Computer\) |
   | " |           Alle            |
   |   Rangfolge   |           127            |
   |   JobObject    |          &nbsp;          |
   | Netdirectport  |           445            |
   | PriorityValue  |            3             |

   ---

3. Aktivieren Sie bei ROCE-bereit Stellungen die **Prioritäts Fluss Steuerung** für SMB-Datenverkehr, der für IWarp nicht erforderlich ist.

   ```PowerShell
   Enable-NetQosFlowControl -priority 3
   Get-NetQosFlowControl
   ```

   _**Folgen**_


   | Priority | Aktiviert | Policyset | ifIndex | Ifalias |
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

4. Aktivieren Sie QoS für den lokalen Netzwerkadapter und den Zielnetzwerk Adapter.

   - Für Netzwerkkonfigurationen, die IWarp verwenden, **nicht erforderlich** .
   - **Erforderlich** für Netzwerkkonfigurationen, die ROCE verwenden.

   ```PowerShell
   Enable-NetAdapterQos -InterfaceAlias "M1"
   Get-NetAdapterQos -Name "M1"
   ```

   _**Folgen**_

   **Name**: M1  
   **Aktiviert**: true  

   _**Eigenschaften**_   


   |      Parameter      |   Hardware   |   Aktuell    |
   |---------------------|--------------|--------------|
   |    Macsecbypass     | NotSupported | NotSupported |
   |     Dcbxsupport     |     Keine     |     Keine     |
   | Numtcs (max/ETS/PFC) |    8/8/8     |    8/8/8     |

   ---

   _**Operationaltrafficclasses:**_ 


   | TC | Bewundernswert | Bandbreite | Prioritäten |
   |----|-----|-----------|------------|
   | 0  | Blättern |    70 %    |  0-2, 4-7   |
   | 1  | Blättern |    30 %    |     3      |

   ---

   _**Operationalflowcontrol:**_  

   Priorität 3 aktiviert  

   _**Operationalclassikationen:**_  


   | Protokoll  | Port/Typ | Priority |
   |-----------|-----------|----------|
   |  Standard  |  &nbsp;   |    0     |
   | NetDirect |    445    |    3     |

   ---

5. Reservieren Sie einen Prozentsatz der Bandbreite für SMB Direct \(RDMA\).

    In diesem Beispiel wird eine Bandbreiten Reservierung von 30% verwendet. Wählen Sie einen Wert aus, der angibt, was für den Speicher Datenverkehr erforderlich ist. 

   ```PowerShell
   New-NetQosTrafficClass "SMB" -Priority 3 -BandwidthPercentage 30 -Algorithm ETS
   ```

   _**Folgen**_


   | Name | Algorithmus | Bandbreite (%) | Priority | Policyset | ifIndex | Ifalias |
   |------|-----------|--------------|----------|-----------|---------|---------|
   | SMB  |    Blättern    |      30      |    3     |  Global   | &nbsp;  | &nbsp;  |

   ---                                      

6. Anzeigen der Einstellungen für die Bandbreiten Reservierung.  

   ```PowerShell
   Get-NetQosTrafficClass
   ```

   _**Folgen**_


   |   Name    | Algorithmus | Bandbreite (%) | Priority | Policyset | ifIndex | Ifalias |
   |-----------|-----------|--------------|----------|-----------|---------|---------|
   | [Default] |    Blättern    |      70      | 0-2, 4-7  |  Global   | &nbsp;  | &nbsp;  |
   |    SMB    |    Blättern    |      30      |    3     |  Global   | &nbsp;  | &nbsp;  |

   ---

## <a name="step-5-optional-resolve-the-mellanox-adapter-debugger-conflict"></a>Schritt 5 Optionale Auflösen des Konflikts des Mellanox-Adapter Debuggers 

Wenn ein Mellanox-Adapter verwendet wird, blockiert der angefügte Debugger standardmäßig NetQoS, was ein bekanntes Problem ist. Wenn Sie also einen Adapter von Mellanox verwenden und einen Debugger anfügen möchten, verwenden Sie den folgenden Befehl, um dieses Problem zu beheben. Dieser Schritt ist nicht erforderlich, wenn Sie nicht beabsichtigen, einen Debugger anzufügen, oder wenn Sie keinen Mellanox-Adapter verwenden.

   ```PowerShell    
   Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 –Force
   ``` 

## <a name="step-6-verify-the-rdma-configuration-native-host"></a>Schritt 6 Überprüfen der RDMA-Konfiguration (nativer Host)

Sie möchten sicherstellen, dass das Fabric ordnungsgemäß konfiguriert ist, bevor Sie einen Vswitch erstellen und zu RDMA (konvergierte NIC) wechseln. 

Die folgende Abbildung zeigt den aktuellen Status der Hyper-V-Hosts.

![Testen von RDMA](../../media/Converged-NIC/4-single-test-rdma.jpg)

1. Überprüfen Sie die RDMA-Konfiguration.

   ```PowerShell
   Get-NetAdapterRdma
   ```
   _**Folgen**_


   | Name |           Interfacedescription           | Aktiviert |
   |------|------------------------------------------|---------|
   |  M1  | Mellanox ConnectX-3 pro-Ethernet-Adapter |  True   |

   ---

2. Bestimmen Sie den **ifindex** -Wert des Ziel Adapters.<p>Sie verwenden diesen Wert in nachfolgenden Schritten, wenn Sie das Skript ausführen, das Sie herunterladen.

   ```PowerShell
   Get-NetIPConfiguration -InterfaceAlias "M*" | ft InterfaceAlias,InterfaceIndex,IPv4Address
   ```

   _**Folgen**_ 


   | InterfaceAlias | InterfaceIndex |  IPv4-Adresse  |
   |----------------|----------------|---------------|
   |       Groß       |       14       | 192.168.1.5 erstellt |

   ---

3. Laden Sie das [Hilfsprogramm diskspd. exe](https://aka.ms/diskspd) herunter, und extrahieren Sie es in c:\test\.

4. Laden Sie das [PowerShell-Skript "Test-RDMA](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1) " in einen Test Ordner auf dem lokalen Laufwerk herunter, z. b. "c:\Test"\.

5. Führen Sie das PowerShell-Skript **Test-RDMA. ps1** aus, um den ifindex-Wert zusammen mit der IP-Adresse des Remote Adapters im gleichen VLAN an das Skript zu übergeben.<p>In diesem Beispiel übergibt das Skript den **ifindex** -Wert 14 auf der IP-Adresse 192.168.1.5 erstellt des Remote Netzwerkadapters.

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
   >Wenn der RDMA-Datenverkehr fehlschlägt, wenden Sie sich für den speziellen ROCE-Fall an die Tor-Switchkonfiguration, um geeignete PFC/ETS-Einstellungen zu erhalten, die den Host Einstellungen entsprechen. Referenzwerte finden Sie im Abschnitt QoS in diesem Dokument.

## <a name="step-7-remove-the-access-vlan-setting"></a>Schritt 7. Entfernen der VLAN-Zugriffs Einstellung

Um den Hyper-V-Switch zu erstellen, müssen Sie die zuvor installierten VLAN-Einstellungen entfernen.  

1. Entfernen Sie die VLAN-Zugriffs Einstellung von der physischen NIC, um zu verhindern, dass die NIC den ausgehenden Datenverkehr automatisch mit der falschen VLAN-ID kennzeichnen.<p>Durch das Entfernen dieser Einstellung wird auch verhindert, dass eingehender Datenverkehr gefiltert wird, der nicht mit der Zugriffs-VLAN-ID identisch ist

   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name M1 -RegistryKeyword VlanID -RegistryValue "0"
   ```    

2. Vergewissern Sie sich, dass die **VLANID-Einstellung** den VLAN-ID-Wert auf NULL zeigt.

   ```PowerShell    
   Get-NetAdapterAdvancedProperty -name m1 | Where-Object {$_.RegistryKeyword -eq 'VlanID'} 
   ```  


## <a name="step-8-create-a-hyper-v-vswitch-on-your-hyper-v-hosts"></a>Schritt 8. Erstellen eines Hyper-v-Vswitch auf Ihren Hyper-v-Hosts

In der folgenden Abbildung ist Hyper-V-Host 1 mit einem Vswitch dargestellt.

![Erstellen eines virtuellen Hyper-V-Switches](../../media/Converged-NIC/5-single-create-vswitch.jpg)


1. Erstellen Sie einen externen Hyper-v-Vswitch in Hyper-v auf dem Hyper-v-Host A. <p>In diesem Beispiel hat der Schalter den Namen vmstest. Außerdem erstellt der Parameter " **allowmanagementos** " eine Host-vNIC, die den Mac und die IP-Adressen der physischen NIC erbt.

   ```PowerShell
   New-VMSwitch -Name VMSTEST -NetAdapterName "M1" -AllowManagementOS $true
   ```
   _**Folgen**_


   |  Name   | SwitchType extern |      Netadapterinterfacedescription      |
   |---------|------------|------------------------------------------|
   | Vmstest |  Extern  | Mellanox ConnectX-3 pro-Ethernet-Adapter |

   ---

2. Zeigen Sie die Eigenschaften des Netzwerkadapters an.

   ```PowerShell
   Get-NetAdapter | ft -AutoSize
   ```

   _**Folgen**_


   |         Name          |        Interfacedescription         | ifIndex | Status |    MacAddress     | LinkSpeed |
   |-----------------------|-------------------------------------|---------|--------|-------------------|-----------|
   | vethernet \(vmstest\) | Virtueller Hyper-V-Ethernet-Adapter #2 |   27    |   Nach oben   | E4-1D-2D-07-40-71 |  40 Gbit/s  |

   ---

3. Verwalten Sie die Host-vNIC auf zwei Arten. 

   - Die **netadapter** -Ansicht wird basierend auf dem Namen "vethernet \(vmstest\)" betrieben. In dieser Ansicht werden nicht alle Netzwerkadapter Eigenschaften angezeigt.
   - In der **vmnetworkadapter** -Sicht wird das Präfix "vethernet" gelöscht und einfach der Name des vmswitchs verwendet. (Empfohlen) 

   ```PowerShell
   Get-VMNetworkAdapter –ManagementOS | ft -AutoSize
   ```

   _**Folgen**_


   |         Name         | Ismanagementos |        VMName        |  SwitchName  | MacAddress | Status | IpAddresses |
   |----------------------|----------------|----------------------|--------------|------------|--------|-------------|
   | Corp-externer Switch |      True      | Corp-externer Switch | 001b785768aa |    Okay    | &nbsp; |             |
   |       Vmstest        |      True      |       Vmstest        | E41D2D074071 |    Okay    | &nbsp; |             |

   ---

4. Testen Sie die Verbindung.

   ```Powershell    
   Test-NetConnection 192.168.1.5
   ```

   _**Folgen**_ 

   ```
    ComputerName   : 192.168.1.5
    RemoteAddress  : 192.168.1.5
    InterfaceAlias : vEthernet (CORP-External-Switch)
    SourceAddress  : 192.168.1.3
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
   ```

5. Zuweisen und Anzeigen der VLAN-Einstellungen für den Netzwerkadapter.

   ```PowerShell
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "VMSTEST" -VlanId "101" -Access -ManagementOS
   Get-VMNetworkAdapterVlan -ManagementOS -VMNetworkAdapterName "VMSTEST"
   ```    

   _**Folgen**_


   | VMName | Vmnetworkadaptername |  Modus  | Vlanlist angezeigt |
   |--------|----------------------|--------|----------|
   | &nbsp; |       Vmstest        | Access |   101    |

   ---  

6. Testen Sie die Verbindung.<p>Es kann einige Sekunden dauern, bis Sie erfolgreich ein Ping an den anderen Adapter durchführen können.  

   ```PowerShell    
   Test-NetConnection 192.168.1.5
   ```

   _**Folgen**_

   ```
    ComputerName   : 192.168.1.5
    RemoteAddress  : 192.168.1.5
    InterfaceAlias : vEthernet (VMSTEST)
    SourceAddress  : 192.168.1.3
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
   ```

## <a name="step-9-test-hyper-v-virtual-switch-rdma-mode-2"></a>Schritt 9. Testen des virtuellen Hyper-V-Switches RDMA (Modus 2)

Die folgende Abbildung zeigt den aktuellen Status der Hyper-v-Hosts, einschließlich des Vswitch auf dem Hyper-v-Host 1.

![Testen des virtuellen Hyper-V-Switches](../../media/Converged-NIC/6-single-test-vswitch-rdma.jpg)


1. Legen Sie das Prioritätstag ging auf der Host-vNIC fest.

   ```PowerShell    
   Set-VMNetworkAdapter -ManagementOS -Name "VMSTEST" -IeeePriorityTag on
   Get-VMNetworkAdapter -ManagementOS -Name "VMSTEST" | fl Name,IeeePriorityTag
   ```  

   _**Folgen**_

    Name: vmstest ieeeprioritytag: on


2. Anzeigen der RDMA-Informationen des Netzwerkadapters. 

   ```PowerShell
   Get-NetAdapterRdma
   ```   

   _**Folgen**_


   |         Name          |        Interfacedescription         | Aktiviert |
   |-----------------------|-------------------------------------|---------|
   | vethernet \(vmstest\) | Virtueller Hyper-V-Ethernet-Adapter #2 |  False  |

   ---

   >[!NOTE]
   >Wenn der **aktivierte** Parameter den Wert **false**aufweist, bedeutet dies, dass RDMA nicht aktiviert ist.


3. Anzeigen der Informationen zum Netzwerkadapter.

   ```PowerShell
   Get-NetAdapter
   ```

   _**Folgen**_   


   |        Name         |        Interfacedescription         | ifIndex | Status |    MacAddress     | LinkSpeed |
   |---------------------|-------------------------------------|---------|--------|-------------------|-----------|
   | vethernet (vmstest) | Virtueller Hyper-V-Ethernet-Adapter #2 |   27    |   Nach oben   | E4-1D-2D-07-40-71 |  40 Gbit/s  |

   ---


4. Aktivieren Sie RDMA auf der Host-vNIC.

   ```PowerShell
   Enable-NetAdapterRdma -Name "vEthernet (VMSTEST)"
   Get-NetAdapterRdma -Name "vEthernet (VMSTEST)"
   ```

   _**Folgen**_


   |         Name          |        Interfacedescription         | Aktiviert |
   |-----------------------|-------------------------------------|---------|
   | vethernet \(vmstest\) | Virtueller Hyper-V-Ethernet-Adapter #2 |  True   |

   ---

   >[!NOTE]
   >Wenn der **aktivierte** Parameter den Wert **true**aufweist, bedeutet dies, dass RDMA aktiviert ist.

5. Ausführen von RDMA-Datenverkehrs Tests.

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

Die letzte Zeile in der Ausgabe "RDMA-Datenverkehrs Test erfolgreich: RDMA-Datenverkehr wurde an 192.168.1.5 erstellt gesendet" zeigt, dass Sie die konvergierte NIC erfolgreich auf dem Adapter konfiguriert haben.

## <a name="related-topics"></a>Verwandte Themen
- [Konvergierte NIC-Konfiguration mit Nic](cnic-datacenter.md)
- [Konfiguration des physischen Switches für konvergierte NIC](cnic-app-switch-config.md)
- [Problembehandlung bei zusammen getauschten NIC](cnic-app-troubleshoot.md)
