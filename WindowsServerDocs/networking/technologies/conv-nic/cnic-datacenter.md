---
title: Konvergierte NIC in einer kombinierten NIC-Konfiguration (Datacenter)
description: In diesem Thema erhalten Sie Anweisungen zum Bereitstellen einer konvergenten NIC in einer kombinierten NIC-Konfiguration mit Switch Embedded Teaming (Set).
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: f01546f8-c495-4055-8492-8806eee99862
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/17/2018
ms.openlocfilehash: 8229b72d69968d3690ece87d5116b215bdf78a08
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70869873"
---
# <a name="converged-nic-in-a-teamed-nic-configuration-datacenter"></a>Konvergierte NIC in einer kombinierten NIC-Konfiguration (Datacenter)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erhalten Sie Anweisungen zum Bereitstellen einer konvergenten NIC in einer kombinierten NIC-Konfiguration mit dem Switch Embedded \(Teaming-Satz\). 

In der Beispielkonfiguration in diesem Thema werden zwei Hyper-v-Hosts, **Hyper-v-Host 1** und **Hyper-v-Host 2**, beschrieben. Beide Hosts verfügen über zwei Netzwerkadapter. Auf jedem Host ist ein Adapter mit dem Subnetz 192.168.1. x/24 verbunden, und ein Adapter ist mit dem 192.168.2. x/24-Subnetz verbunden.

![Hyper-V-Hosts](../../media/Converged-NIC/1-datacenter-test-conn.jpg)

## <a name="step-1-test-the-connectivity-between-source-and-destination"></a>Schritt 1 Testen der Konnektivität zwischen Quelle und Ziel

Stellen Sie sicher, dass die physische NIC eine Verbindung mit dem Zielhost herstellen kann.  In diesem Test wird die Konnektivität mithilfe von \(Layer\) 3 L3 oder der IP-Schicht sowie des VLANs der \(virtuellen\) VLANs\)der Layer \(2 L2 Virtual Local Area Networks veranschaulicht.

1. Zeigen Sie die ersten Netzwerkadapter Eigenschaften an.

   ```PowerShell
   Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize
   ```

   _**Folgen**_


   |    Name    |           Interfacedescription           | ifIndex | Status |    macAddress     | LinkSpeed |
   |------------|------------------------------------------|---------|--------|-------------------|-----------|
   | Test-40G-1 | Mellanox ConnectX-3 pro-Ethernet-Adapter |   11    |   Nach oben   | E4-1D-2D-07-43-D0 |  40 Gbit/s  |

   ---

2. Anzeigen zusätzlicher Eigenschaften für den ersten Adapter, einschließlich der IP-Adresse. 

   ```PowerShell
   Get-NetIPAddress -InterfaceAlias "Test-40G-1"
   Get-NetIPAddress -InterfaceAlias "TEST-40G-1" | Where-Object {$_.AddressFamily -eq "IPv4"} | fl InterfaceAlias,IPAddress
   ```

   _**Folgen**_


   |   Parameter    |    Wert    |
   |----------------|-------------|
   |   IPAddress    | 192.168.1.3 |
   | InterfaceIndex |     11      |
   | InterfaceAlias | Test-40G-1  |
   | AddressFamily  |    IPv4     |
   |      Typ      |   Unicast   |
   |  PrefixLength  |     24      |

   ---

3. Anzeigen der zweiten Netzwerkadapter Eigenschaften.

   ```PowerShell
   Get-NetAdapter -Name "Test-40G-2" | ft -AutoSize
   ```

   _**Folgen**_


   |    Name    |          Interfacedescription           | ifIndex | Status |    macAddress     | LinkSpeed |
   |------------|-----------------------------------------|---------|--------|-------------------|-----------|
   | TEST-40G-2 | Mellanox ConnectX-3 pro Ethernet A... #2 |   13    |   Nach oben   | E4-1D-2D-07-40-70 |  40 Gbit/s  |

   ---

4. Anzeigen zusätzlicher Eigenschaften für den zweiten Adapter, einschließlich der IP-Adresse.

   ```PowerShell
   Get-NetIPAddress -InterfaceAlias "Test-40G-2"
   Get-NetIPAddress -InterfaceAlias "Test-40G-2" | Where-Object {$_.AddressFamily -eq "IPv4"} | fl InterfaceAlias,IPAddress
   ```

   _**Folgen**_


   |   Parameter    |    Wert    |
   |----------------|-------------|
   |   IPAddress    | 192.168.2.3 |
   | InterfaceIndex |     13      |
   | InterfaceAlias | TEST-40G-2  |
   | AddressFamily  |    IPv4     |
   |      Typ      |   Unicast   |
   |  PrefixLength  |     24      |

   ---

5. Überprüfen Sie, ob andere NIC-Team-oder Set-Member-pnics eine gültige IP-Adresse aufweisen<p>Verwenden Sie ein separates Subnetz \(, xxx.xxx. **2**. xxx im Vergleich zu xxx.xxx. **1**. xxx\), um das Senden von diesem Adapter an das Ziel zu vereinfachen. Wenn Sie beide pnics im gleichen Subnetz finden, wird die Windows-TCP/IP-Stapel Last zwischen den Schnittstellen und der einfachen Validierung komplizierter.


## <a name="step-2-ensure-that-source-and-destination-can-communicate"></a>Schritt 2 Stellen Sie sicher, dass Quelle und Ziel kommunizieren können

In diesem Schritt verwenden wir den Windows PowerShell-Befehl " **Test-NetConnection** ", aber wenn Sie dies bevorzugen, können Sie den **ping** -Befehl verwenden. 

1. Überprüfen Sie die bidirektionale Kommunikation.

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

   _**Folgen**_


   |        Parameter         |    Wert    |
   |--------------------------|-------------|
   |       ComputerName       | 192.168.1.5 erstellt |
   |      RemoteAddress       | 192.168.1.5 erstellt |
   |      InterfaceAlias      | Test-40G-1  |
   |      SourceAddress       | 192.168.1.3 |
   |      Pingerfolg       |    False    |
   | Pingreplydetails \(RTT\) |    0 ms     |

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
   |       ComputerName       | 192.168.1.5 erstellt |
   |      RemoteAddress       | 192.168.1.5 erstellt |
   |      InterfaceAlias      | Test-40G-1  |
   |      SourceAddress       | 192.168.1.3 |
   |      Pingerfolg       |    False    |
   | Pingreplydetails \(RTT\) |    0 ms     |

   ---


4. Überprüfen Sie die Konnektivität für zusätzliche NICs. Wiederholen Sie die vorherigen Schritte für alle nachfolgenden pnics, die im NIC-oder Set-Team enthalten sind.

   ```PowerShell    
   Test-NetConnection 192.168.2.5
   ```

   _**Folgen**_


   |        Parameter         |    Wert    |
   |--------------------------|-------------|
   |       ComputerName       | 192.168.2.5 |
   |      RemoteAddress       | 192.168.2.5 |
   |      InterfaceAlias      | Test-40G-2  |
   |      SourceAddress       | 192.168.2.3 |
   |      Pingerfolg       |    False    |
   | Pingreplydetails \(RTT\) |    0 ms     |

   ---

## <a name="step-3-configure-the-vlan-ids-for-nics-installed-in-your-hyper-v-hosts"></a>Schritt 3 Konfigurieren der VLAN-IDs für NICs, die auf Ihren Hyper-V-Hosts installiert sind

Bei vielen Netzwerkkonfigurationen werden VLANs verwendet, und wenn Sie beabsichtigen, VLANs in Ihrem Netzwerk zu verwenden, müssen Sie den vorherigen Test mit konfigurierten VLANs wiederholen.

Bei diesem Schritt befinden sich die NICs im **Zugriffs** Modus. Wenn Sie jedoch später in diesem Handbuch einen virtuellen Hyper- \(V-\) Switch-Vswitch erstellen, werden die VLAN-Eigenschaften auf der Vswitch-Port Ebene angewendet. 

Da ein Switch mehrere VLANs hosten kann, ist es erforderlich, dass der \(\) physische Switch des oberen Rands den Port hat, mit dem der Host verbunden ist, der im trunk Modus konfiguriert ist.

>[!NOTE]
>In der Tor-switchdokumentation finden Sie Anweisungen zum Konfigurieren des trunk Modus auf dem Switch.

In der folgenden Abbildung sind zwei Hyper-V-Hosts mit jeweils zwei Netzwerkadaptern dargestellt, für die in den Netzwerkadapter Eigenschaften VLAN 101 und VLAN 102 konfiguriert sind.

![Konfigurieren von virtuellen lokalen Netzwerken](../../media/Converged-NIC/2-datacenter-configure-vlans.jpg)


>[!TIP]
>Gemäß den IEEE\) -Netzwerkstandards "Institute of \(Electrical and Electronics Engineers" werden \(die Quality of Service\) QoS-Eigenschaften in der physischen NIC für den eingebetteten 802.1 p-Header ausgeführt. im 802.1 q \(-VLAN\) -Header, wenn Sie die VLAN-ID konfigurieren.

1. Konfigurieren Sie die VLAN-ID auf der ersten NIC, Test-40G-1.

   ```PowerShell    
   Set-NetAdapterAdvancedProperty -Name "Test-40G-1" -RegistryKeyword VlanID -RegistryValue "101"
   Get-NetAdapterAdvancedProperty -Name "Test-40G-1" | Where-Object {$_.RegistryKeyword -eq "VlanID"} | ft -AutoSize
   ```

   _**Folgen**_   


   |    Name    | DisplayName | Display value | Registryschlüsselwort | REGISTRYVALUE |
   |------------|-------------|--------------|-----------------|---------------|
   | TEST-40G-1 |   VLAN-ID   |     101      |     VlanID      |     {101}     |

   ---

2. Starten Sie den Netzwerkadapter neu, um die VLAN-ID anzuwenden.

   ```PowerShell
   Restart-NetAdapter -Name "Test-40G-1"
   ```

3. Stellen **Sie sicher,** dass der Status "aktiv"

   ```PowerShell
   Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize
   ```

   _**Folgen**_


   |    Name    |          Interfacedescription           | ifIndex | Status |    macAddress     | LinkSpeed |
   |------------|-----------------------------------------|---------|--------|-------------------|-----------|
   | Test-40G-1 | Mellanox ConnectX-3 pro Ethernet Ada... |   11    |   Nach oben   | E4-1D-2D-07-43-D0 |  40 Gbit/s  |

   ---

4. Konfigurieren Sie die VLAN-ID auf der zweiten NIC, Test-40G-2.

   ```PowerShell    
   Set-NetAdapterAdvancedProperty -Name "Test-40G-2" -RegistryKeyword VlanID -RegistryValue "102"
   Get-NetAdapterAdvancedProperty -Name "Test-40G-2" | Where-Object {$_.RegistryKeyword -eq "VlanID"} | ft -AutoSize
   ``` 

   _**Folgen**_


   |    Name    | DisplayName | Display value | Registryschlüsselwort | REGISTRYVALUE |
   |------------|-------------|--------------|-----------------|---------------|
   | TEST-40G-2 |   VLAN-ID   |     102      |     VlanID      |     {102}     |

   ---

5. Starten Sie den Netzwerkadapter neu, um die VLAN-ID anzuwenden.

   ```PowerShell
   Restart-NetAdapter -Name "Test-40G-2" 
   ```

6. Stellen **Sie sicher,** dass der Status "aktiv"

   ```PowerShell
   Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize
   ```

   _**Folgen**_


   |    Name    |          Interfacedescription           | ifIndex | Status |    macAddress     | LinkSpeed |
   |------------|-----------------------------------------|---------|--------|-------------------|-----------|
   | Test-40G-2 | Mellanox ConnectX-3 pro Ethernet Ada... |   11    |   Nach oben   | E4-1D-2D-07-43-D1 |  40 Gbit/s  |

   ---

   >[!IMPORTANT]
   >Es kann einige Sekunden dauern, bis das Gerät neu gestartet und im Netzwerk verfügbar wird. 

7. Überprüfen Sie die Konnektivität für die erste NIC, Test-40G-1.<p>Wenn eine Verbindung nicht hergestellt werden kann, überprüfen Sie die Switch-VLAN-Konfiguration oder die Ziel Teilnahme im gleichen VLAN. 

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

   _**Folgen**_   


   |        Parameter         |    Wert    |
   |--------------------------|-------------|
   |       ComputerName       | 192.168.1.5 erstellt |
   |      RemoteAddress       | 192.168.1.5 erstellt |
   |      InterfaceAlias      | Test-40G-1  |
   |      SourceAddress       | 192.168.1.5 erstellt |
   |      Pingerfolg       |    True     |
   | Pingreplydetails \(RTT\) |    0 ms     |

   ---

8. Überprüfen Sie die Konnektivität für die erste NIC, Test-40G-2.<p>Wenn eine Verbindung nicht hergestellt werden kann, überprüfen Sie die Switch-VLAN-Konfiguration oder die Ziel Teilnahme im gleichen VLAN.

   ```PowerShell    
   Test-NetConnection 192.168.2.5
   ```

   _**Folgen**_    


   |        Parameter         |    Wert    |
   |--------------------------|-------------|
   |       ComputerName       | 192.168.2.5 |
   |      RemoteAddress       | 192.168.2.5 |
   |      InterfaceAlias      | Test-40G-2  |
   |      SourceAddress       | 192.168.2.3 |
   |      Pingerfolg       |    True     |
   | Pingreplydetails \(RTT\) |    0 ms     |

   ---

   >[!IMPORTANT]
   >Es ist nicht ungewöhnlich, dass ein **Test-NetConnection** -oder Ping-Fehler unmittelbar nach dem Ausführen von **Restart-netadapter**auftritt.  Warten Sie daher, bis der Netzwerkadapter vollständig initialisiert wurde, und wiederholen Sie dann den Vorgang.
   >
   >Wenn die VLAN 101-Verbindungen funktionieren, aber die VLAN 102-Verbindungen nicht, besteht das Problem möglicherweise darin, dass der Switch so konfiguriert werden muss, dass Port Datenverkehr auf dem gewünschten VLAN zugelassen wird. Sie können dies überprüfen, indem Sie die fehlerhaften Adapter vorübergehend auf VLAN 101 festlegen und den Konnektivitätstest wiederholen.


   Die folgende Abbildung zeigt Ihre Hyper-V-Hosts nach der erfolgreichen Konfiguration von VLANs.

   ![Konfigurieren von Quality of Service](../../media/Converged-NIC/3-datacenter-configure-qos.jpg)


## <a name="step-4-configure-quality-of-service-qos"></a>Schritt 4 Konfigurieren von \(Quality of Service QoS\)

>[!NOTE]
>Sie müssen alle der folgenden DCB-und QoS-Konfigurationsschritte auf allen Hosts ausführen, die miteinander kommunizieren sollen.

1. Installieren Sie Data Center \(Bridging DCB\) auf allen Hyper-V-Hosts.

   - **Optional** für Netzwerkkonfigurationen, die IWarp verwenden.
   - **Erforderlich** für Netzwerkkonfigurationen, die eine beliebige \(Version\) von ROCE für RDMA-Dienste verwenden.

   ```PowerShell
   Install-WindowsFeature Data-Center-Bridging
   ```

   _**Folgen**_


   | Erfolgreich | Neustart erforderlich | Exitcode |     Funktionsergebnis     |
   |---------|----------------|-----------|------------------------|
   |  True   |       Nein       |  Erfolgreich  | {Data Center Bridging} |

   ---

2. Legen Sie die QoS-Richtlinien für SMB-Direct fest:

   - **Optional** für Netzwerkkonfigurationen, die IWarp verwenden.
   - **Erforderlich** für Netzwerkkonfigurationen, die eine beliebige \(Version\) von ROCE für RDMA-Dienste verwenden.

   Im folgenden Beispiel Befehl ist der Wert "3" beliebig. Sie können einen beliebigen Wert zwischen 1 und 7 verwenden, solange Sie während der Konfiguration der QoS-Richtlinien einheitlich denselben Wert verwenden.

   ```PowerShell
   New-NetQosPolicy "SMB" -NetDirectPortMatchCondition 445 -PriorityValue8021Action 3
   ```

   _**Folgen**_


   |   Parameter    |          Wert           |
   |----------------|--------------------------|
   |      Name      |           SMB            |
   |     Besitzer      | Gruppenrichtlinie \(Computer\) |
   | " |           All            |
   |   Rangfolge   |           127            |
   |   JobObject    |          &nbsp;          |
   | Netdirectport  |           445            |
   | PriorityValue  |            3             |

   ---

3. Legen Sie zusätzliche QoS-Richtlinien für anderen Datenverkehr auf der Schnittstelle fest.   

   ```PowerShell
   New-NetQosPolicy "DEFAULT" -Default -PriorityValue8021Action 0
   ```

   _**Folgen**_   


   |   Parameter    |          Wert           |
   |----------------|--------------------------|
   |      Name      |         DEFAULT          |
   |     Besitzer      | Gruppenrichtlinie \(Computer\) |
   | " |           All            |
   |   Rangfolge   |           127            |
   |    Vorlage    |         Default          |
   |   JobObject    |          &nbsp;          |
   | PriorityValue  |            0             |

   ---

4. Aktivieren Sie die **Prioritäts Fluss Steuerung** für SMB-Datenverkehr, der für IWarp nicht erforderlich ist.

   ```PowerShell
   Enable-NetQosFlowControl -priority 3
   Get-NetQosFlowControl
   ```

   _**Folgen**_


   | Priorität | Enabled | Policyset | IfIndex | Ifalias |
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

   >**Wichtig** Wenn Ihre Ergebnisse nicht mit diesen Ergebnissen identisch sind, weil andere Elemente als 3 den aktivierten Wert true aufweisen, müssen Sie **FlowControl** für diese Klassen deaktivieren.
   >
   >```PowerShell
   >Disable-NetQosFlowControl -priority 0,1,2,4,5,6,7
   >Get-NetQosFlowControl
   >```
   >Bei komplexeren Konfigurationen sind für die anderen Datenverkehrs Klassen möglicherweise Fluss Steuerung erforderlich. diese Szenarien werden jedoch nicht in diesem Handbuch behandelt.


5. Aktivieren Sie QoS für die erste NIC, Test-40G-1.

   ```PowerShell
   Enable-NetAdapterQos -InterfaceAlias "Test-40G-1"
   Get-NetAdapterQos -Name "Test-40G-1"

   Name: TEST-40G-1 
   Enabled: True
   ```
   _**Funktionen**:_   


   |      Parameter      |   Hardware   |   Strömung    |
   |---------------------|--------------|--------------|
   |    Macsecbypass     | NotSupported | NotSupported |
   |     Dcbxsupport     |     None     |     None     |
   | Numtcs (max/ETS/PFC) |    8/8/8     |    8/8/8     |

   ---

   _**Operationaltrafficclasses**:_    


   | TC |  BEWUNDERNSWERT   | Bandbreite | Prioritäten |
   |----|--------|-----------|------------|
   | 0  | Strengeren |  &nbsp;   |    0-7     |

   ---

   _**Operationalflowcontrol**:_  

   Priorität 3 aktiviert  

   _**Operationalclassikationen**:_  


   | Protokoll  | Port/Typ | Priorität |
   |-----------|-----------|----------|
   |  Default  |  &nbsp;   |    0     |
   | NetDirect |    445    |    3     |

   ---

6. Aktivieren Sie QoS für die zweite NIC, Test-40G-2.

   ```PowerShell
   Enable-NetAdapterQos -InterfaceAlias "Test-40G-2"
   Get-NetAdapterQos -Name "Test-40G-2"

   Name: TEST-40G-2 
   Enabled: True 
   ```

   _**Funktionen**:_ 


   |      Parameter      |   Hardware   |   Strömung    |
   |---------------------|--------------|--------------|
   |    Macsecbypass     | NotSupported | NotSupported |
   |     Dcbxsupport     |     Keine     |     None     |
   | Numtcs (max/ETS/PFC) |    8/8/8     |    8/8/8     |

   ---

   _**Operationaltrafficclasses**:_  


   | TC |  BEWUNDERNSWERT   | Bandbreite | Prioritäten |
   |----|--------|-----------|------------|
   | 0  | Strengeren |  &nbsp;   |    0-7     |

   ---

    _**Operationalflowcontrol**:_  

    Priorität 3 aktiviert  

   _**Operationalclassikationen**:_  


   | Protokoll  | Port/Typ | Priorität |
   |-----------|-----------|----------|
   |  Default  |  &nbsp;   |    0     |
   | NetDirect |    445    |    3     |

   ---


7. Reservieren der Hälfte der Bandbreite für \(SMB Direct RDMA\)

   ```PowerShell
   New-NetQosTrafficClass "SMB" -priority 3 -bandwidthpercentage 50 -algorithm ETS
   ```

   _**Folgen**_  


   | Name | Algorithmus | Bandbreite (%) | Priorität | Policyset | IfIndex | Ifalias |
   |------|-----------|--------------|----------|-----------|---------|---------|
   | SMB  |    BLÄTTERN    |      50      |    3     |  Global   | &nbsp;  | &nbsp;  |

   ---

8. Anzeigen der Einstellungen für die Bandbreiten Reservierung:   

   ```PowerShell
   Get-NetQosTrafficClass | ft -AutoSize
   ```

   _**Folgen**_  


   |   Name    | Algorithmus | Bandbreite (%) | Priorität | Policyset | IfIndex | Ifalias |
   |-----------|-----------|--------------|----------|-----------|---------|---------|
   | Vorgegebene |    BLÄTTERN    |      50      | 0-2, 4-7  |  Global   | &nbsp;  | &nbsp;  |
   |    SMB    |    BLÄTTERN    |      50      |    3     |  Global   | &nbsp;  | &nbsp;  |

   ---

9. Optionale Erstellen Sie zwei weitere Datenverkehrs Klassen für den Mandanten-IP-Datenverkehr 

   >[!TIP]
   >Sie können die Werte "IP1" und "IP2" weglassen.

   ```PowerShell
   New-NetQosTrafficClass "IP1" -Priority 1 -bandwidthpercentage 10 -algorithm ETS
   ```

   _**Folgen**_


   | Name | Algorithmus | Bandbreite (%) | Priorität | Policyset | IfIndex | Ifalias |
   |------|-----------|--------------|----------|-----------|---------|---------|
   | IP1  |    BLÄTTERN    |      10      |    1     |  Global   | &nbsp;  | &nbsp;  |

   ---

   ```PowerShell
   New-NetQosTrafficClass "IP2" -Priority 2 -bandwidthpercentage 10 -algorithm ETS
   ```

   _**Folgen**_


   | Name | Algorithmus | Bandbreite (%) | Priorität | Policyset | IfIndex | Ifalias |
   |------|-----------|--------------|----------|-----------|---------|---------|
   | IP2  |    BLÄTTERN    |      10      |    2     |  Global   | &nbsp;  | &nbsp;  |

   ---

10. Zeigen Sie die QoS-Datenverkehrs Klassen an.

    ```PowerShell
    Get-NetQosTrafficClass | ft -AutoSize
    ```

    _**Folgen**_


    |   Name    | Algorithmus | Bandbreite (%) | Priorität | Policyset | IfIndex | Ifalias |
    |-----------|-----------|--------------|----------|-----------|---------|---------|
    | Vorgegebene |    BLÄTTERN    |      30      |  0, 4-7   |  Global   | &nbsp;  | &nbsp;  |
    |    SMB    |    BLÄTTERN    |      50      |    3     |  Global   | &nbsp;  | &nbsp;  |
    |    IP1    |    BLÄTTERN    |      10      |    1     |  Global   | &nbsp;  | &nbsp;  |
    |    IP2    |    BLÄTTERN    |      10      |    2     |  Global   | &nbsp;  | &nbsp;  |

    ---

11. Optionale Überschreiben Sie den Debugger.<p>Standardmäßig blockiert der angefügte Debugger NetQoS. 

    ```PowerShell
    Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 –Force
    Get-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" | ft AllowFlowControlUnderDebugger
    ```

    _**Folgen**_  

    ```
    AllowFlowControlUnderDebugger
    -----------------------------
    1
    ```

## <a name="step-5-verify-the-rdma-configuration-mode-1"></a>Schritt 5 Überprüfen des RDMA \(-Konfigurations Modus 1\) 

Sie möchten sicherstellen, dass das Fabric ordnungsgemäß konfiguriert ist, bevor Sie einen Vswitch erstellen und in den \(RDMA\)-Modus 2 übergehen.

Die folgende Abbildung zeigt den aktuellen Status der Hyper-V-Hosts.

![Testen von RDMA](../../media/Converged-NIC/4-datacenter-test-rdma.jpg)


1. Überprüfen Sie die RDMA-Konfiguration.

   ```PowerShell
   Get-NetAdapterRdma | ft -AutoSize
   ```

   _**Folgen**_


   |    Name    |        Interfacedescription        | Enabled |
   |------------|------------------------------------|---------|
   | TEST-40G-1 | Mellanox ConnectX-4 VPI-Adapter #2 |  True   |
   | TEST-40G-2 |  Mellanox ConnectX-4 VPI-Adapter   |  True   |

   ---

2. Bestimmen Sie den **ifindex** -Wert der Ziel Adapter.<p>Sie verwenden diesen Wert in nachfolgenden Schritten, wenn Sie das Skript ausführen, das Sie herunterladen.   

   ```PowerShell
   Get-NetIPConfiguration -InterfaceAlias "TEST*" | ft InterfaceAlias,InterfaceIndex,IPv4Address
   ```

   _**Folgen**_


   | InterfaceAlias | InterfaceIndex |  IPv4-Adresse  |
   |----------------|----------------|---------------|
   |   TEST-40G-1   |       14       | {192.168.1.3} |
   |   TEST-40G-2   |       13       | {192.168.2.3} |

   ---

3. Laden Sie das [Hilfsprogramm diskspd. exe](https://aka.ms/diskspd) herunter, und extrahieren Sie es in c:\test.\.

4. Laden Sie das [PowerShell-Skript "Test-RDMA](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1) " in einen Test Ordner auf dem lokalen Laufwerk herunter, z. b. "c:\Test".\.

5. Führen Sie das PowerShell-Skript **Test-RDMA. ps1** aus, um den ifindex-Wert zusammen mit der IP-Adresse des ersten Remote Adapters im gleichen VLAN an das Skript zu übergeben.<p>In diesem Beispiel übergibt das Skript den **ifindex** -Wert 14 auf der IP-Adresse 192.168.1.5 erstellt des Remote Netzwerkadapters.

   ```PowerShell
   C:\TEST\Test-RDMA.PS1 -IfIndex 14 -IsRoCE $true -RemoteIpAddress 192.168.1.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**Folgen**_ 

   ```   
   VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\diskspd.exe
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

6. Führen Sie das PowerShell-Skript **Test-RDMA. ps1** aus, um den ifindex-Wert zusammen mit der IP-Adresse des zweiten Remote Adapters im gleichen VLAN an das Skript zu übergeben.<p>In diesem Beispiel übergibt das Skript den **ifindex** -Wert 13 auf der IP-Adresse 192.168.2.5 des Remote Netzwerkadapters.

   ```PowerShell
   C:\TEST\Test-RDMA.PS1 -IfIndex 13 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**Folgen**_ 

   ```   
   VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\diskspd.exe
   VERBOSE: The adapter TEST-40G-2 is a physical adapter
   VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
   VERBOSE: QoS/DCB/PFC configuration is correct.
   VERBOSE: RDMA configuration is correct.
   VERBOSE: Checking if remote IP address, 192.168.2.5, is reachable.
   VERBOSE: Remote IP 192.168.2.5 is reachable.
   VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
   VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
   VERBOSE: 0 RDMA bytes written per second
   VERBOSE: 0 RDMA bytes sent per second
   VERBOSE: 541185606 RDMA bytes written per second
   VERBOSE: 34821478 RDMA bytes sent per second
   VERBOSE: 954717307 RDMA bytes written per second
   VERBOSE: 35040816 RDMA bytes sent per second
   VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
   VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.2.5
   ``` 

## <a name="step-6-create-a-hyper-v-vswitch-on-your-hyper-v-hosts"></a>Schritt 6 Erstellen eines Hyper-v-Vswitch auf Ihren Hyper-v-Hosts


Die folgende Abbildung zeigt Hyper-V-Host 1 mit einem Vswitch.

![Erstellen eines virtuellen Hyper-V-Switches](../../media/Converged-NIC/5-datacenter-create-vswitch.jpg)

1. Erstellen Sie einen Vswitch im Set-Modus auf dem Hyper-V-Host 1.

   ```PowerShell
   New-VMSwitch –Name "VMSTEST" –NetAdapterName "TEST-40G-1","TEST-40G-2" -EnableEmbeddedTeaming $true -AllowManagementOS $true
   ```

   _**Dadurch**_


   |  Name   | SwitchType extern | Netadapterinterfacedescription |
   |---------|------------|--------------------------------|
   | VMSTEST |  Extern  |        Zusammenfassung        |

   ---

2. Zeigen Sie das physische Adapter Team in der Gruppe an.

   ```PowerShell
   Get-VMSwitchTeam -Name "VMSTEST" | fl
   ```

   _**Folgen**_  

   ```
   Name: VMSTEST  
   Id: ad9bb542-dda2-4450-a00e-f96d44bdfbec  
   NetAdapterInterfaceDescription: {Mellanox ConnectX-3 Pro Ethernet Adapter, Mellanox ConnectX-3 Pro Ethernet Adapter #2}  
   TeamingMode: SwitchIndependent  
   LoadBalancingAlgorithm: Dynamic   
   ```

3. Anzeigen von zwei Ansichten der Host-vNIC

   ```PowerShell
    Get-NetAdapter
   ```

   _**Folgen**_


   |        Name         |        Interfacedescription         | ifIndex | Status |    macAddress     | LinkSpeed |
   |---------------------|-------------------------------------|---------|--------|-------------------|-----------|
   | vethernet (vmstest) | Virtueller Hyper-V-Ethernet-Adapter #2 |   28    |   Nach oben   | E4-1D-2D-07-40-71 |  80 Gbit/s  |

   ---

4. Anzeigen zusätzlicher Eigenschaften der Host-vNIC. 

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS
   ```

   _**Folgen**_


   |  Name   | Ismanagementos | VMName  |  SwitchName  | macAddress | Status | IpAddresses |
   |---------|----------------|---------|--------------|------------|--------|-------------|
   | VMSTEST |      True      | VMSTEST | E41D2D074071 |    Okay    | &nbsp; |             |

   ---


5. Testen Sie die Netzwerkverbindung mit dem Remote-VLAN 101-Adapter.

   ```PowerShell
   Test-NetConnection 192.168.1.5 
   ```

   _**Folgen**_  

   ```
   WARNING: Ping to 192.168.1.5 failed -- Status: DestinationHostUnreachable

   ComputerName   : 192.168.1.5
   RemoteAddress  : 192.168.1.5
   InterfaceAlias : vEthernet (CORP-External-Switch)
   SourceAddress  : 10.199.48.170
   PingSucceeded  : False
   PingReplyDetails (RTT) : 0 ms
   ```

## <a name="step-7-remove-the-access-vlan-setting"></a>Schritt 7 Entfernen der VLAN-Zugriffs Einstellung

In diesem Schritt entfernen Sie die VLAN-Zugriffs Einstellung aus der physischen NIC und legen die VLANID mithilfe des Vswitch fest.

Sie müssen die VLAN-Zugriffs Einstellung entfernen, um zu verhindern, dass sowohl der ausgehende Datenverkehr mit der falschen VLAN-ID automatisch markiert wird, als auch der eingehende Datenverkehr zu filtern, der nicht mit der VLAN-ID des Zugriffs

1. Entfernen Sie die Einstellung.

   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name "Test-40G-1" -RegistryKeyword VlanID -RegistryValue "0"
   Set-NetAdapterAdvancedProperty -Name "Test-40G-2" -RegistryKeyword VlanID -RegistryValue "0"
   ```

2. Legen Sie die VLAN-ID fest.

   ```PowerShell
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "VMSTEST" -VlanId "101" -Access -ManagementOS
   Get-VMNetworkAdapterVlan -ManagementOS -VMNetworkAdapterName "VMSTEST"
   ```

   _**Folgen**_  

   ```
   VMName VMNetworkAdapterName Mode   VlanList
   ------ -------------------- ----   --------
          VMSTEST              Access 101     
   ```


3. Testen Sie die Netzwerkverbindung.

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

   >**Wichtig** Wenn die Ergebnisse den Beispiel Ergebnissen nicht ähneln, schlägt Ping mit der Meldung "Warnung: Fehler beim Ping an 192.168.1.5 erstellt-Status: Destinationhostunerreich, "vergewissern Sie sich, dass das" vethernet (vmstest) "über die richtige IP-Adresse verfügt.
   >
   >```PowerShell
   >Get-NetIPAddress -InterfaceAlias "vEthernet (VMSTEST)"
   >```
   >
   >Wenn die IP-Adresse nicht festgelegt ist, beheben Sie das Problem.
   >
   >```PowerShell
   >New-NetIPAddress -InterfaceAlias "vEthernet (VMSTEST)" -IPAddress 192.168.1.3 -PrefixLength 24
   >
   >IPAddress : 192.168.1.3
   >InterfaceIndex: 37
   >InterfaceAlias: vEthernet (VMSTEST)
   >AddressFamily : IPv4
   >Type  : Unicast
   >PrefixLength  : 24
   >PrefixOrigin  : Manual
   >SuffixOrigin  : Manual
   >AddressState  : Tentative
   >ValidLifetime : Infinite ([TimeSpan]::MaxValue)
   >PreferredLifetime : Infinite ([TimeSpan]::MaxValue)
   >SkipAsSource  : False
   >PolicyStore   : ActiveStore
   >```  


4. Benennen Sie die Verwaltungs-NIC um.

   ```PowerShell
   Rename-VMNetworkAdapter -ManagementOS -Name “VMSTEST” -NewName “MGT”
   Get-VMNetworkAdapter -ManagementOS
   ```

   _**Folgen**_ 


   |         Name         | Ismanagementos | VMName |      SwitchName      |  macAddress  | Status | IpAddresses |
   |----------------------|----------------|--------|----------------------|--------------|--------|-------------|
   | Corp-externer Switch |      True      | &nbsp; | Corp-externer Switch | 001B785768AA |  Okay  |   &nbsp;    |
   |         VERWALTUNG          |      True      | &nbsp; |       VMSTEST        | E41D2D074071 |  Okay  |   &nbsp;    |

   ---

5. Anzeigen zusätzlicher NIC-Eigenschaften.

   ```PowerShell
   Get-NetAdapter
   ```

   _**Folgen**_


   |      Name       |        Interfacedescription         | ifIndex | Status |    macAddress     | LinkSpeed |
   |-----------------|-------------------------------------|---------|--------|-------------------|-----------|
   | vethernet (mgt) | Virtueller Hyper-V-Ethernet-Adapter #2 |   28    |   Nach oben   | E4-1D-2D-07-40-71 |  80 Gbit/s  |

   ---

## <a name="step-8-test-hyper-v-vswitch-rdma"></a>Schritt 8. Testen von Hyper-V Vswitch RDMA

Die folgende Abbildung zeigt den aktuellen Status der Hyper-v-Hosts, einschließlich des Vswitch auf dem Hyper-v-Host 1.

![Testen des virtuellen Hyper-V-Switches](../../media/Converged-NIC/6-datacenter-test-vswitch-rdma.jpg)

1. Legen Sie die Prioritätstag Markierung auf der Host-vNIC fest, um die vorherigen VLAN-Einstellungen zu ergänzen.

   ```PowerShell    
   Set-VMNetworkAdapter -ManagementOS -Name "MGT" -IeeePriorityTag on
   Get-VMNetworkAdapter -ManagementOS -Name "MGT" | fl Name,IeeePriorityTag
   ```

   _**Folgen**_  

   Benennen VERWALTUNG  
   Ieeeprioritytag:  On  

2. Erstellen Sie zwei Host-vNICs für RDMA, und verbinden Sie Sie mit dem Vswitch vmstest.

   ```PowerShell    
   Add-VMNetworkAdapter –SwitchName "VMSTEST" –Name SMB1 –ManagementOS
   Add-VMNetworkAdapter –SwitchName "VMSTEST" –Name SMB2 –ManagementOS
   ```

3. Zeigen Sie die Eigenschaften der Verwaltungs-NIC an.

   ```PowerShell    
   Get-VMNetworkAdapter -ManagementOS
   ```

   _**Folgen**_ 


   |         Name         | Ismanagementos |        VMName        |  SwitchName  | macAddress | Status | IpAddresses |
   |----------------------|----------------|----------------------|--------------|------------|--------|-------------|
   | Corp-externer Switch |      True      | Corp-externer Switch | 001B785768AA |    Okay    | &nbsp; |             |
   |         Verwaltung          |      True      |       VMSTEST        | E41D2D074071 |    Okay    | &nbsp; |             |
   |         SERVER MESSAGE BLOCK         |      True      |       VMSTEST        | 00155D30AA00 |    Okay    | &nbsp; |             |
   |         SMB2         |      True      |       VMSTEST        | 00155D30AA01 |    Okay    | &nbsp; |             |

   ---

## <a name="step-9-assign-an-ip-address-to-the-smb-host-vnics-vethernet-smb1-and-vethernet-smb2"></a>Schritt 9: Zuweisen einer IP-Adresse zu den SMB-Host-vNICs \(vethernet Server Message Block\) und \(vethernet SMB2\)

Die physischen Adapter "Test-40G-1" und "Test-40G-2" verfügen weiterhin über das konfigurierte zugriffsvlan 101 und 102. Aus diesem Grund markieren die Adapter den Datenverkehr, und der Ping-Vorgang ist erfolgreich. Zuvor haben Sie beide PNIC-VLAN-IDs auf NULL festgelegt und dann vmstest Vswitch auf VLAN 101 festgelegt. Anschließend konnten Sie den Remote-VLAN 101-Adapter weiterhin mithilfe von mgt vNIC pingen, aber zurzeit sind keine VLAN 102-Mitglieder vorhanden.



1. Entfernen Sie die VLAN-Zugriffs Einstellung von der physischen NIC, um zu verhindern, dass der ausgehende Datenverkehr mit der falschen VLAN-ID automatisch gekennzeichnet wird, und verhindern Sie, dass der eingehende Datenverkehr gefiltert wird, der nicht mit der Zugriffs-VLAN-ID identisch ist.

   ```PowerShell    
   New-NetIPAddress -InterfaceAlias "vEthernet (SMB1)" -IPAddress 192.168.2.111 -PrefixLength 24
   ```

   _**Folgen**_  

   ```   
   IPAddress : 192.168.2.111
   InterfaceIndex: 40
   InterfaceAlias: vEthernet (SMB1)
   AddressFamily : IPv4
   Type  : Unicast
   PrefixLength  : 24
   PrefixOrigin  : Manual
   SuffixOrigin  : Manual
   AddressState  : Invalid
   ValidLifetime : Infinite ([TimeSpan]::MaxValue)
   PreferredLifetime : Infinite ([TimeSpan]::MaxValue)
   SkipAsSource  : False
   PolicyStore   : PersistentStore
   ```

2. Testen Sie den Remote-VLAN 102-Adapter.

   ```PowerShell
   Test-NetConnection 192.168.2.5 
   ```

   _**Folgen**_  

   ```
   ComputerName   : 192.168.2.5
   RemoteAddress  : 192.168.2.5
   InterfaceAlias : vEthernet (SMB1)
   SourceAddress  : 192.168.2.111
   PingSucceeded  : True
   PingReplyDetails (RTT) : 0 ms
   ```

3. Fügen Sie eine neue IP-Adresse für die Schnitt \(Stelle\)vethernet SMB2 hinzu.

   ```PowerShell
   New-NetIPAddress -InterfaceAlias "vEthernet (SMB2)" -IPAddress 192.168.2.222 -PrefixLength 24 
   ```

   _**Folgen**_ 

   ```
   IPAddress : 192.168.2.222
   InterfaceIndex: 44
   InterfaceAlias: vEthernet (SMB2)
   AddressFamily : IPv4
   Type  : Unicast
   PrefixLength  : 24
   PrefixOrigin  : Manual
   SuffixOrigin  : Manual
   AddressState  : Invalid
   ValidLifetime : Infinite ([TimeSpan]::MaxValue)
   PreferredLifetime : Infinite ([TimeSpan]::MaxValue)
   SkipAsSource  : False
   PolicyStore   : PersistentStore
   ```

4. Testen Sie die Verbindung erneut.    


5. Platzieren Sie die RDMA-Host-vNICs auf dem bereits vorhandenen VLAN 102.

   ```PowerShell
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "SMB1" -VlanId "102" -Access -ManagementOS
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "SMB2" -VlanId "102" -Access -ManagementOS

   Get-VMNetworkAdapterVlan -ManagementOS
   ```

   _**Folgen**_ 

   ```   
   VMName VMNetworkAdapterName Mode VlanList
   ------ -------------------- ---- --------
      SMB1 Access   102 
      Mgt  Access   101 
      SMB2 Access   102 
      CORP-External-Switch Untagged
   ```

6. Überprüfen Sie die Zuordnung von Server Message Block und SMB2 zu den zugrunde liegenden physischen NICs im Vswitch-Team.<p>Die Zuordnung von Host-vNIC zu physischen NICs ist zufällig und unterliegt der Neuausrichtung während der Erstellung und Zerstörung. In diesem Fall können Sie einen indirekten Mechanismus verwenden, um die aktuelle Zuordnung zu überprüfen. Die Mac-Adressen von Server Message Block und SMB2 sind dem NIC-Team Mitglied Test-40G-2 zugeordnet. Dies ist nicht ideal, da Test-40G-1 über keine zugeordnete SMB-Host-vNIC verfügt und die Verwendung von RDMA-Datenverkehr über den Link erst dann zulässt, wenn ihm eine SMB-Host-vNIC zugeordnet ist.

   ```PowerShell    
   Get-NetAdapterVPort (Preferred)

   Get-NetAdapterVmqQueue
   ```

   _**Folgen**_ 

   ```
   Name   QueueID MacAddressVlanID Processor VmFriendlyName
   ----   ------- ---------------- --------- --------------
   TEST-40G-1 1   E4-1D-2D-07-40-71 1010:17
   TEST-40G-2 1   00-15-5D-30-AA-00 1020:17
   TEST-40G-2 2   00-15-5D-30-AA-01 1020:17
   ```

7. Anzeigen der Eigenschaften des VM-Netzwerkadapters.

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS
   ```

   _**Folgen**_ 

   ```
   Name IsManagementOs VMName SwitchName   MacAddress   Status IPAddresses
   ---- -------------- ------ ----------   ----------   ------ -----------
   CORP-External-Switch True  CORP-External-Switch 001B785768AA {Ok}  
   Mgt  True  VMSTEST  E41D2D074071 {Ok}  
   SMB1 True  VMSTEST  00155D30AA00 {Ok}  
   SMB2 True  VMSTEST  00155D30AA01 {Ok}  
   ```

8. Anzeigen der Netzwerkadapter-Team Zuordnung.<p>Die Ergebnisse sollten keine Informationen zurückgeben, da Sie noch keine Zuordnung durchgeführt haben.

   ```PowerShell
   Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName SMB1
   Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName SMB2
   ```


9. Ordnen Sie Server Message Block und SMB2 zu, um die physischen NIC-Teammitglieder voneinander zu trennen und die Ergebnisse ihrer Aktionen anzuzeigen.

   >[!IMPORTANT]
   >Stellen Sie sicher, dass Sie diesen Schritt ausführen, bevor Sie fortfahren, oder die Implementierung schlägt fehl

   ```PowerShell
   Set-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName "SMB1" -PhysicalNetAdapterName "Test-40G-1"
   Set-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName "SMB2" -PhysicalNetAdapterName "Test-40G-2"

   Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST
   ```

   _**Folgen**_ 

   ```   
   NetAdapterName : Test-40G-1
   NetAdapterDeviceId : {BAA9A00F-A844-4740-AA93-6BD838F8CFBA}
   ParentAdapter  : VMInternalNetworkAdapter, Name = 'SMB1'
   IsTemplate : False
   CimSession : CimSession: .
   ComputerName   : 27-3145G0803
   IsDeleted  : False

   NetAdapterName : Test-40G-2
   NetAdapterDeviceId : {B7AB5BB3-8ACB-444B-8B7E-BC882935EBC8}
   ParentAdapter  : VMInternalNetworkAdapter, Name = 'SMB2'
   IsTemplate : False
   CimSession : CimSession: .
   ComputerName   : 27-3145G0803
   IsDeleted  : False
   ```

10. Bestätigen Sie die zuvor erstellten Mac-Zuordnungen.

    ```PowerShell    
    Get-NetAdapterVmqQueue
    ```

    _**Folgen**_ 

    ```   
    Name   QueueID MacAddressVlanID Processor VmFriendlyName
    ----   ------- ---------------- --------- --------------
    TEST-40G-1 1   E4-1D-2D-07-40-71 1010:17
    TEST-40G-1 2   00-15-5D-30-AA-00 1020:17
    TEST-40G-2 1   00-15-5D-30-AA-01 1020:17
    ```


11. Testen Sie die Verbindung vom Remote System, da sich beide Host-vNICs im selben Subnetz befinden und dieselbe VLAN- \(ID\)102 aufweisen.

    ```PowerShell 
    Test-NetConnection 192.168.2.111
    ```

    _**Folgen**_   

    ```
    ComputerName   : 192.168.2.111
    RemoteAddress  : 192.168.2.111
    InterfaceAlias : Test-40G-2
    SourceAddress  : 192.168.2.5
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
    ```

    ```PowerShell   
    Test-NetConnection 192.168.2.222
    ```

    _**Folgen**_   

    ```
    ComputerName   : 192.168.2.222
    RemoteAddress  : 192.168.2.222
    InterfaceAlias : Test-40G-2
    SourceAddress  : 192.168.2.5
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms 
    ```
12. Legen Sie den Namen, den Switchnamen und die Prioritätstags fest.   

    ```PowerShell
    Set-VMNetworkAdapter -ManagementOS -Name "SMB1" -IeeePriorityTag on
    Set-VMNetworkAdapter -ManagementOS -Name "SMB2" -IeeePriorityTag on
    Get-VMNetworkAdapter -ManagementOS -Name "SMB*" | fl Name,SwitchName,IeeePriorityTag,Status
    ```

    _**Folgen**_   

    ```
    Name: SMB1
    SwitchName  : VMSTEST
    IeeePriorityTag : On 
    Status  : {Ok}

    Name: SMB2
    SwitchName  : VMSTEST
    IeeePriorityTag : On
    Status  : {Ok}
    ```

13. Anzeigen der Eigenschaften des vethernet-Netzwerkadapters.

    ```PowerShell
    Get-NetAdapterRdma -Name "vEthernet*" | sort Name | ft -AutoSize
    ```

    _**Folgen**_   

    ```
    Name  InterfaceDescription Enabled
    ----  -------------------- -------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  False  
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  False  
    vEthernet (MGT)   Hyper-V Virtual Ethernet Adapter #2  False   
    ```

14. Aktivieren Sie die vethernet-Netzwerkadapter.  

    ```PowerShell
    Enable-NetAdapterRdma -Name "vEthernet (SMB1)"
    Enable-NetAdapterRdma -Name "vEthernet (SMB2)"
    Get-NetAdapterRdma -Name "vEthernet*" | sort Name | fl *
    ```

    _**Folgen**_   

    ```
    Name  InterfaceDescription Enabled
    ----  -------------------- -------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  True   
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  True  
    vEthernet (MGT)   Hyper-V Virtual Ethernet Adapter #2  False
    ```

## <a name="step-10-validate-the-rdma-functionality"></a>Schritt 10. Überprüfen Sie die RDMA-Funktionalität.

Sie möchten die RDMA-Funktionalität vom Remote System auf das lokale System, das über einen Vswitch verfügt, an beide Mitglieder des Vswitch Set-Teams überprüfen.<p>Da sowohl Host-vNICs \(Server Message Block als auch SMB2\) VLAN 102 zugewiesen sind, können Sie den VLAN 102-Adapter auf dem Remote System auswählen. <p>In diesem Beispiel führt der NIC-Test-40G-2 RDMA zu Server Message Block (192.168.2.111) und SMB2 (192.168.2.222).

>[!TIP]
>Möglicherweise müssen Sie die Firewall auf diesem System deaktivieren.  Weitere Informationen finden Sie in der Fabric-Richtlinie.
>
>```PowerShell
>Set-NetFirewallProfile -All -Enabled False
>    
>Get-NetAdapterAdvancedProperty -Name "Test-40G-2"
>```
>
>_**Folgen**_ 
>   
>```
>Name  DisplayNameDisplayValue   RegistryKeyword RegistryValue  
>----  -----------------------   --------------- -------------  
> .
> .
>Test-40G-2VLAN ID102VlanID  {102} 
>```

1. Zeigen Sie die Eigenschaften des Netzwerkadapters an.

   ```PowerShell
   Get-NetAdapter
   ```

   _**Folgen**_ 

   ```
   Name  InterfaceDescriptionifIndex Status   MacAddress LinkSpeed
   ----  --------------------------- ------   ---------- ---------
   Test-40G-2Mellanox ConnectX-3 Pro Ethernet A...#3   3 Up   E4-1D-2D-07-43-D140 Gbps
   ```

2. Anzeigen der RDMA-Informationen des Netzwerkadapters.

   ```PowerShell
   Get-NetAdapterRdma
   ```

   _**Folgen**_  

   ```
   Name  InterfaceDescription Enabled
   ----  -------------------- -------
   Test-40G-2Mellanox ConnectX-3 Pro Ethernet Adap... True   
   ```

3. Führen Sie den RDMA-Datenverkehrs Test für den ersten physischen Adapter aus.

   ```PowerShell 
   C:\TEST\Test-RDMA.PS1 -IfIndex 3 -IsRoCE $true -RemoteIpAddress 192.168.2.111 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**Folgen**_ 

   ```
   VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\diskspd.exe
   VERBOSE: The adapter Test-40G-2 is a physical adapter
   VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
   VERBOSE: QoS/DCB/PFC configuration is correct.
   VERBOSE: RDMA configuration is correct.
   VERBOSE: Checking if remote IP address, 192.168.2.111, is reachable.
   VERBOSE: Remote IP 192.168.2.111 is reachable.
   VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
   VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
   VERBOSE: 34251744 RDMA bytes sent per second
   VERBOSE: 967346308 RDMA bytes written per second
   VERBOSE: 35698177 RDMA bytes sent per second
   VERBOSE: 976601842 RDMA bytes written per second
   VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
   VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.2.111
   ```

4. Führen Sie den RDMA-Datenverkehrs Test für den zweiten physischen Adapter aus.

   ```PowerShell
   C:\TEST\Test-RDMA.PS1 -IfIndex 3 -IsRoCE $true -RemoteIpAddress 192.168.2.222 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**Folgen**_ 

   ```
   VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\diskspd.exe
   VERBOSE: The adapter Test-40G-2 is a physical adapter
   VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
   VERBOSE: QoS/DCB/PFC configuration is correct.
   VERBOSE: RDMA configuration is correct.
   VERBOSE: Checking if remote IP address, 192.168.2.222, is reachable.
   VERBOSE: Remote IP 192.168.2.222 is reachable.
   VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
   VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
   VERBOSE: 0 RDMA bytes written per second
   VERBOSE: 0 RDMA bytes sent per second
   VERBOSE: 485137693 RDMA bytes written per second
   VERBOSE: 35200268 RDMA bytes sent per second
   VERBOSE: 939044611 RDMA bytes written per second
   VERBOSE: 34880901 RDMA bytes sent per second
   VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
   VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.2.222
   ```

5. Testen Sie den RDMA-Datenverkehr vom lokalen zum Remote Computer.

    ```PowerShell
    Get-NetAdapter | ft –AutoSize
    ```

    _**Folgen**_ 

    ```
    Name  InterfaceDescriptionifIndex Status   MacAddress LinkSpeed
    ----  --------------------------- ------   ---------- ---------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  45 Up   00-15-5D-30-AA-0380 Gbps
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  41 Up   00-15-5D-30-AA-0280 Gbps
    ```

6. Führen Sie den RDMA-Datenverkehrs Test auf dem ersten virtuellen Adapter aus.    

   ```
   C:\TEST\Test-RDMA.PS1 -IfIndex 41 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**Folgen**_ 

   ```
   VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\diskspd.exe
   VERBOSE: The adapter vEthernet (SMB1) is a virtual adapter
   VERBOSE: Retrieving vSwitch bound to the virtual adapter
   VERBOSE: Found vSwitch: VMSTEST
   VERBOSE: Found the following physical adapter(s) bound to vSwitch: TEST-40G-1, TEST-40G-2
   VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
   VERBOSE: QoS/DCB/PFC configuration is correct.
   VERBOSE: RDMA configuration is correct.
   VERBOSE: Checking if remote IP address, 192.168.2.5, is reachable.
   VERBOSE: Remote IP 192.168.2.5 is reachable.
   VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
   VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
   VERBOSE: 0 RDMA bytes written per second
   VERBOSE: 0 RDMA bytes sent per second
   VERBOSE: 0 RDMA bytes written per second
   VERBOSE: 15250197 RDMA bytes sent per second
   VERBOSE: 896320913 RDMA bytes written per second
   VERBOSE: 33947559 RDMA bytes sent per second
   VERBOSE: 912160540 RDMA bytes written per second
   VERBOSE: 34091930 RDMA bytes sent per second
   VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
   VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.2.5
   ```

7. Führen Sie den RDMA-Datenverkehrs Test für den zweiten virtuellen Adapter aus.

   ```PowerShell
   C:\TEST\Test-RDMA.PS1 -IfIndex 45 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**Folgen**_ 

   ```
   VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\diskspd.exe
   VERBOSE: The adapter vEthernet (SMB2) is a virtual adapter
   VERBOSE: Retrieving vSwitch bound to the virtual adapter
   VERBOSE: Found vSwitch: VMSTEST
   VERBOSE: Found the following physical adapter(s) bound to vSwitch: TEST-40G-1, TEST-40G-2
   VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
   VERBOSE: QoS/DCB/PFC configuration is correct.
   VERBOSE: RDMA configuration is correct.
   VERBOSE: Checking if remote IP address, 192.168.2.5, is reachable.
   VERBOSE: Remote IP 192.168.2.5 is reachable.
   VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
   VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
   VERBOSE: 0 RDMA bytes written per second
   VERBOSE: 0 RDMA bytes sent per second
   VERBOSE: 385169487 RDMA bytes written per second
   VERBOSE: 33902277 RDMA bytes sent per second
   VERBOSE: 907354685 RDMA bytes written per second
   VERBOSE: 33923662 RDMA bytes sent per second
   VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
   VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.2.5
   ```

Die letzte Zeile in der Ausgabe "RDMA-Datenverkehrs Test erfolgreich: RDMA-Datenverkehr wurde an 192.168.2.5 gesendet. "zeigt, dass Sie die konvergierte NIC erfolgreich auf dem Adapter konfiguriert haben.

## <a name="related-topics"></a>Verwandte Themen 

- [Konvergierte NIC-Konfiguration mit einem einzelnen Netzwerk Adapter](cnic-single.md)
- [Konfiguration des physischen Switches für konvergierte NIC](cnic-app-switch-config.md)
- [Problembehandlung bei zusammen getauschten NIC](cnic-app-troubleshoot.md)
