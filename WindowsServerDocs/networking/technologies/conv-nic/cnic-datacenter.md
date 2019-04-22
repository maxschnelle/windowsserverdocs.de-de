---
title: Zusammengeführte NIC Teaming-fähigen NIC-Konfiguration (Datencenter)
description: In diesem Thema bieten wir mit einer Anleitung zum Bereitstellen von Converged NIC in eine Teaming-fähigen NIC-Konfiguration mit Switch Embedded Teaming (SET).
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: f01546f8-c495-4055-8492-8806eee99862
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/17/2018
ms.openlocfilehash: 5f99600e24c62da9bdf674897dbadde9246b7bb7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821031"
---
# <a name="converged-nic-in-a-teamed-nic-configuration-datacenter"></a>Zusammengeführte NIC Teaming-fähigen NIC-Konfiguration (Datencenter)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema stellen wir Ihnen mit Anweisungen zum Bereitstellen von zusammengeführten NIC in einer NIC Teaming-fähigen-Konfiguration mit Switch Embedded Teaming \(festgelegt\). 

Die Beispielkonfiguration in diesem Thema wird beschrieben, zwei Hyper-V-Hosts **Hyper-V Host 1** und **Hyper-V-Host 2**. Beide Hosts verfügen über zwei Netzwerkadapter. Klicken Sie auf jedem Host ein Adapter mit dem Subnetz 192.168.1.x/24 verbunden ist, und ein Adapter mit dem 192.168.2.x/24 Subnetz verbunden ist.

![Hyper-V-Hosts](../../media/Converged-NIC/1-datacenter-test-conn.jpg)

## <a name="step-1-test-the-connectivity-between-source-and-destination"></a>Schritt 1 Testen der Konnektivität zwischen Quelle und Ziel

Stellen Sie sicher, dass die physischen NIC auf dem Zielhost verbinden kann.  Dieser Test zeigt die Verbindung mithilfe von Layer 3 \(L3\) - oder der IP-Schicht - als auch Schicht 2 \(L2\) virtuelle lokale Netzwerke \(VLAN\).

1. Anzeigen der Eigenschaften der ersten des Netzwerkadapters an.

   ```PowerShell
   Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize
   ```
  
   _**Ergebnisse:**_

   |Name|InterfaceDescription|ifIndex|Status|MacAddress|LinkSpeed|
   |-----|--------------------|-------|-----|----------|---------|
   |Test-40G-1|Mellanox ConnectX-3 Pro-Ethernet-Adapter|11|Nach oben|E4-1D-2D-07-43-D0|40 Gbit/s|
   ---
   
2. Zeigen Sie zusätzliche Eigenschaften für die erste Adapter, einschließlich der IP-Adresse. 

   ```PowerShell
   Get-NetIPAddress -InterfaceAlias "Test-40G-1"
   Get-NetIPAddress -InterfaceAlias "TEST-40G-1" | Where-Object {$_.AddressFamily -eq "IPv4"} | fl InterfaceAlias,IPAddress
   ```
   
   _**Ergebnisse:**_

   |Parameter|Wert|
   |---------|-----|
   |IPAddress| 192.168.1.3|
   |InterfaceIndex|11|
   |InterfaceAlias|Test-40G-1|
   |"AddressFamily"|IPv4|
   |Typ| Unicast|
   |PrefixLength|24|
   ---

3. Anzeigen der Eigenschaften der zweiten des Netzwerkadapters an.

   ```PowerShell
   Get-NetAdapter -Name "Test-40G-2" | ft -AutoSize
   ```
   
   _**Ergebnisse:**_

   |Name |InterfaceDescription |ifIndex |Status |MacAddress |LinkSpeed|
   |----|--------------------|-------|------|----------|---------|
   |TEST-40G-2 |Mellanox ConnectX-3 Pro Ethernet A... #2 |13 |Nach oben |E4-1D-2D-07-40-70 |40 Gbit/s|
   ---
   
4. Zeigen Sie zusätzliche Eigenschaften für die zweite Netzwerkkarte, einschließlich der IP-Adresse.

   ```PowerShell
   Get-NetIPAddress -InterfaceAlias "Test-40G-2"
   Get-NetIPAddress -InterfaceAlias "Test-40G-2" | Where-Object {$_.AddressFamily -eq "IPv4"} | fl InterfaceAlias,IPAddress
   ```
   
   _**Ergebnisse:**_

   |Parameter|Wert|
   |---------|-----|
   |IPAddress|192.168.2.3|
   |InterfaceIndex|13|
   |InterfaceAlias|TEST-40G-2|
   |"AddressFamily"|IPv4|
   |Typ|Unicast|
   |PrefixLength|24|
   ---

5. Stellen Sie sicher, dass diese anderen NIC-Team oder eine Gruppe Mitglied pNICs eine gültige IP-Adresse verfügt.<p>Verwenden von einem separaten Subnetz \(xxx.xxx. **2**.xxx Vs xxx.xxx. **1**.xxx\), um zu ermöglichen, von diesem Adapter an das Ziel gesendet. Andernfalls, wenn Sie beide pNICs im gleichen Subnetz finden, der Windows TCP/IP-Stapel Lastenausgleich zwischen den Schnittstellen und einfache Überprüfungen jedoch komplizierter.


## <a name="step-2-ensure-that-source-and-destination-can-communicate"></a>Schritt 2 Stellen Sie sicher, dass Quelle und Ziel kommunizieren kann

In diesem Schritt verwenden wir die **Test-NetConnection** Windows PowerShell-Befehl, doch wenn können Sie verwenden die **Ping** -Befehl, falls gewünscht. 

1. Überprüfen Sie die bidirektionale Kommunikation.

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```
   
   _**Ergebnisse:**_

   |Parameter|Wert|
   |---------|-----|
   |ComputerName|192.168.1.5|
   |RemoteAddress|192.168.1.5|
   |InterfaceAlias|Test-40G-1|
   |SourceAddress|192.168.1.3|
   |PingSucceeded|False|
   |PingReplyDetails \(RTT\)|0 ms|
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
   
   _**Ergebnisse:**_

   |Parameter|Wert|
   |---------|-----|
   |ComputerName|192.168.1.5|
   |RemoteAddress|192.168.1.5|
   |InterfaceAlias|Test-40G-1|
   |SourceAddress|192.168.1.3|
   |PingSucceeded|False|
   |PingReplyDetails \(RTT\)|0 ms|
   ---
   
   
4. Überprüfen Sie die Verbindung für weitere NICs. Wiederholen Sie die vorherigen Schritte für alle nachfolgenden pNICs im Team NIC oder eine Gruppe enthalten.

   ```PowerShell    
   Test-NetConnection 192.168.2.5
   ```
   
   _**Ergebnisse:**_

   |Parameter|Wert|
   |---------|-----|
   |ComputerName|192.168.2.5|
   |RemoteAddress|192.168.2.5|
   |InterfaceAlias|Test-40G-2|
   |SourceAddress|192.168.2.3|
   |PingSucceeded|False|
   |PingReplyDetails \(RTT\)|0 ms|
   ---

## <a name="step-3-configure-the-vlan-ids-for-nics-installed-in-your-hyper-v-hosts"></a>Schritt 3 Konfigurieren Sie die VLAN-IDs für Netzwerkadapter, die in Hyper-V-Hosts installiert

Viele Netzwerkkonfigurationen Verwenden von VLANs, und wenn Sie VLANs in Ihrem Netzwerk verwenden möchten, müssen Sie den vorherigen Test wiederholen, mit VLANs konfiguriert.

Für diesen Schritt werden die NICs im **Zugriff** Modus. Wenn Sie jedoch einen virtuellen Hyper-V-Switch erstellen \(vSwitch\) weiter unten in diesem Handbuch werden die VLAN-Eigenschaften auf der Portebene vSwitch angewendet. 

Da mehrere VLANs von ein Switch gehostet werden kann, ist es erforderlich für die Top-of-Rack \(ToR\) physischen Switch mit den Port verfügen, die mit der Host im Modus "Trunk" konfiguriert verbunden ist.

>[!NOTE]
>Anweisungen zum Konfigurieren des Modus "Trunk" auf dem Switch finden Sie in der Dokumentation Ihres ToR-Switch.

Die folgende Abbildung zeigt zwei Hyper-V-Hosts mit zwei Netzwerkadaptern, die VLAN 101 und VLAN-102, die in den Eigenschaften des Netzwerkadapters konfiguriert haben.

![Konfigurieren Sie die virtuelle lokale Netzwerke](../../media/Converged-NIC/2-datacenter-configure-vlans.jpg)


>[!TIP]
>Gemäß der Institute of Electrical and Electronics Engineers \(IEEE\) networking Standards, Quality of Service \(QoS\) Eigenschaften in die physische NIC fungieren, auf dem 802. 1p-Header, die eingebettet ist in der 802. 1Q \(VLAN\) Header, die beim Konfigurieren der VLAN ID.

1. Konfigurieren Sie die VLAN-ID des ersten Netzwerkadapters, Test-40G-1.

   ```PowerShell    
   Set-NetAdapterAdvancedProperty -Name "Test-40G-1" -RegistryKeyword VlanID -RegistryValue "101"
   Get-NetAdapterAdvancedProperty -Name "Test-40G-1" | Where-Object {$_.RegistryKeyword -eq "VlanID"} | ft -AutoSize
   ```

   _**Ergebnisse:**_   

   |Name |DisplayName| DisplayValue| RegistryKeyword |RegistryValue|
   |----|-----------|------------|---------------|-------------|
   |TEST-40G-1|VLAN-ID|101|VlanID|{101}|
   ---

2. Starten Sie den Netzwerkadapter die VLAN ID. anwenden

   ```PowerShell
   Restart-NetAdapter -Name "Test-40G-1"
   ```
   
3. Sicherstellen, dass der Status ist **einrichten**.

   ```PowerShell
   Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize
   ```
   
   _**Ergebnisse:**_

   |Name|InterfaceDescription|ifIndex| Status|MacAddress|LinkSpeed|
   |----|--------------------|-------|------|----------| ---------|
   |Test-40G-1|Mellanox ConnectX-3 Pro-Ethernet-Ada...|11|Nach oben|E4-1D-2D-07-43-D0|40 Gbit/s|
   ---
    
4. Konfigurieren Sie die VLAN-ID, auf die zweite NIC und Test-40G-2.

   ```PowerShell    
   Set-NetAdapterAdvancedProperty -Name "Test-40G-2" -RegistryKeyword VlanID -RegistryValue "102"
   Get-NetAdapterAdvancedProperty -Name "Test-40G-2" | Where-Object {$_.RegistryKeyword -eq "VlanID"} | ft -AutoSize
   ``` 

   _**Ergebnisse:**_

   |Name |DisplayName| DisplayValue| RegistryKeyword |RegistryValue|
   |----|-----------|------------|---------------|-------------|
   |TEST-40G-2|VLAN-ID|102|VlanID|{102}|
   ---
   
5. Starten Sie den Netzwerkadapter die VLAN ID. anwenden

   ```PowerShell
   Restart-NetAdapter -Name "Test-40G-2" 
   ```
   
6. Sicherstellen, dass der Status ist **einrichten**.

   ```PowerShell
   Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize
   ```
   
   _**Ergebnisse:**_

   |Name|InterfaceDescription|ifIndex| Status|MacAddress|LinkSpeed|
   |----|--------------------|-------|------|----------| ---------|
   |Test-40G-2 |Mellanox ConnectX-3 Pro-Ethernet-Ada... |11 |Nach oben |E4-1D-2D-07-43-D1 |40 Gbit/s|
   ---

   >[!IMPORTANT]
   >Es kann einige Sekunden für das Gerät neu starten und im Netzwerk verfügbar sind, dauern. 
   
7. Überprüfen Sie die Verbindung für die erste NIC, Test-40G-1.<p>Bei einem Verbindungsfehler, überprüfen Sie den Switch VLAN-Konfiguration oder das Ziel Teilnahme im gleichen VLAN. 

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```

   _**Ergebnisse:**_   

   |Parameter|Wert|
   |---------|-----|
   |ComputerName|192.168.1.5|
   |RemoteAddress|192.168.1.5|
   |InterfaceAlias|Test-40G-1|
   |SourceAddress|192.168.1.5|
   |PingSucceeded|True|
   |PingReplyDetails \(RTT\)|0 ms|
   ---
   
8. Überprüfen Sie die Verbindung für die erste NIC, Test-40G-2.<p>Bei einem Verbindungsfehler, überprüfen Sie den Switch VLAN-Konfiguration oder das Ziel Teilnahme im gleichen VLAN.

   ```PowerShell    
   Test-NetConnection 192.168.2.5
   ```

   _**Ergebnisse:**_    

   |Parameter|Wert|
   |---------|-----|
   |ComputerName|192.168.2.5|
   |RemoteAddress|192.168.2.5|
   |InterfaceAlias|Test-40G-2|
   |SourceAddress|192.168.2.3|
   |PingSucceeded|True|
   |PingReplyDetails \(RTT\)|0 ms|
   ---
   
   >[!IMPORTANT]
   >Es ist nicht ungewöhnlich, dass eine **Test-NetConnection** oder Pingfehler auftreten, sofort nach dem Ausführen **Neustart-NetAdapter**.  Warten Sie den Netzwerkadapter vollständig initialisiert und versuchen Sie es dann erneut.
   >
   >Wenn die VLAN-101-Verbindungen funktionieren, aber nicht die VLAN-102-Verbindungen, das Problem möglicherweise, dass der Switch werden, um die Port-Datenverkehr auf die gewünschte VLAN zu ermöglichen konfiguriert muss. Sie können für diese überprüfen, indem vorübergehend die fehlerhaften-Adapter auf VLAN 101 festlegen, und wiederholen den Test der Netzwerkverbindung.

   
   Die folgende Abbildung zeigt die Hyper-V-Hosts nach dem Konfigurieren der VLANs erfolgreich.

   ![Konfigurieren von Quality of Service](../../media/Converged-NIC/3-datacenter-configure-qos.jpg)
   
   
## <a name="step-4-configure-quality-of-service-qos"></a>Schritt 4 Konfigurieren von Quality of Service \(QoS\)

>[!NOTE]
>Sie müssen alle der folgenden Schritte für DCB und QoS auf allen Hosts ausführen, die miteinander kommunizieren sollen.

1. Installieren der Data Center Bridging \(DCB\) auf jedem Hyper-V-Hosts.

   - **Optionale** für Netzwerkkonfigurationen, iWarp zu verwenden.
   - **Erforderliche** für Netzwerkkonfigurationen, mit denen RoCE \(eine beliebige Version\) für RDMA-Dienste.

   ```PowerShell
   Install-WindowsFeature Data-Center-Bridging
   ```

   _**Ergebnisse:**_

   |Erfolgreich |Neustart erforderlich |Exitcode|Ergebnis der Funktion|
   |------- |-------------- |--------- |-------------- |
   |True |Nein |Erfolgreich| {Data Center Bridging}|
   ---
   
2. Legen Sie die QoS-Richtlinien für SMB Direct an:

   - **Optionale** für Netzwerkkonfigurationen, iWarp zu verwenden.
   - **Erforderliche** für Netzwerkkonfigurationen, mit denen RoCE \(eine beliebige Version\) für RDMA-Dienste.
   
   Im unten stehenden Beispielbefehl ist der Wert "3" willkürlich. Sie können einen beliebigen Wert zwischen 1 und 7 verwenden, solange Sie konsistent den gleichen Wert in der Konfiguration von QoS-Richtlinien verwenden.

   ```PowerShell
   New-NetQosPolicy "SMB" -NetDirectPortMatchCondition 445 -PriorityValue8021Action 3
   ```
   
   _**Ergebnisse:**_

   |Parameter|Wert|
   |---------|-----|
   |Name |SMB|
   |Besitzer|Eine Gruppenrichtlinie \(Computer\)|
   |NetworkProfile|Alle|
   |Rangfolge|127|
   |JobObject|&nbsp;| 
   |NetDirectPort|445
   |PriorityValue|3
   ---

3. Legen Sie zusätzliche QoS-Richtlinien für den übrigen Datenverkehr für die Schnittstelle an.   

   ```PowerShell
   New-NetQosPolicy "DEFAULT" -Default -PriorityValue8021Action 0
   ```

   _**Ergebnisse:**_   

   |Parameter|Wert|
   |---------|-----|
   |Name | DEFAULT|
   |Besitzer|Eine Gruppenrichtlinie \(Computer\)|
   |NetworkProfile|Alle|
   |Rangfolge|127|
   |Vorlage| Standard|
   |JobObject| &nbsp;|
   |PriorityValue|0|
   ---
   
4. Aktivieren Sie **Priorität flusssteuerung** für SMB-Datenverkehr ist der nicht für iWarp erforderlich.

   ```PowerShell
   Enable-NetQosFlowControl -priority 3
   Get-NetQosFlowControl
   ```
   
   _**Ergebnisse:**_
   
   |Priority|Enabled|PolicySet|IfIndex|IfAlias|
   |---------|-----|--------- |-------| -------|
   |0 |False |Global|&nbsp;|&nbsp;|
   |1 |False |Global|&nbsp;|&nbsp;|
   |2 |False |Global|&nbsp;|&nbsp;|
   |3 |True |Global|&nbsp;|&nbsp;|
   |4 |False |Global|&nbsp;|&nbsp;|
   |5 |False |Global|&nbsp;|&nbsp;|
   |6 |False |Global|&nbsp;|&nbsp;|
   |7 |False |Global|&nbsp;|&nbsp;|
   ---
   
   >**WICHTIGE** , wenn die Ergebnisse dieser Ergebnisse nicht überein stimmen, da Elemente außer 3 einen Wert "true" aktiviert haben, müssen Sie deaktivieren **FlowControl** für diese Klassen.
   >
   >```PowerShell
   >Disable-NetQosFlowControl -priority 0,1,2,4,5,6,7
   >Get-NetQosFlowControl
   >```
   >Unter komplexere Konfigurationen die anderen Klassen flusssteuerung, unter Umständen jedoch diese Szenarien, würde den Rahmen dieses Handbuchs sind.


5. Aktivieren von QoS für die erste NIC, Test-40G-1.

   ```PowerShell
   Enable-NetAdapterQos -InterfaceAlias "Test-40G-1"
   Get-NetAdapterQos -Name "Test-40G-1"

   Name: TEST-40G-1 
   Enabled: True
   ```
   _**Funktionen**:_   

   |Parameter|Hardware|Aktuelle|
   |---------|--------|-------|
   |MacSecBypass|NotSupported|NotSupported|
   |DcbxSupport|Keine|Keine|
   |NumTCs(Max/ETS/PFC)|8/8/8|8/8/8|
   ---
 
   _**OperationalTrafficClasses**:_    

   |TC|TSA|Bandbreite|Prioritäten|
   |----|-----|--------|-------|
   |0| Strict|&nbsp;|0-7|
   ---

   _**OperationalFlowControl**:_  

   Priorität 3 aktiviert  

   _**OperationalClassifications**:_  

   |Protokoll|Porttyp /|Priority|
   |--------|---------|--------|
   |Standard|&nbsp;|0|
   |NetDirect| 445|3|
   ---
   
6. Aktivieren von QoS für die zweite NIC und Test-40G-2.

   ```PowerShell
   Enable-NetAdapterQos -InterfaceAlias "Test-40G-2"
   Get-NetAdapterQos -Name "Test-40G-2"

   Name: TEST-40G-2 
   Enabled: True 
   ```

   _**Funktionen**:_ 

   |Parameter|Hardware|Aktuelle|
   |---------|--------|-------|
   |MacSecBypass|NotSupported|NotSupported|
   |DcbxSupport|Keine|Keine|
   |NumTCs(Max/ETS/PFC)|8/8/8|8/8/8|
   ---

   _**OperationalTrafficClasses**:_  

   |TC|TSA|Bandbreite|Prioritäten|
   |----|-----|--------|-------|
   |0| Strict|&nbsp;|0-7|
   ---
   
    _**OperationalFlowControl**:_  

    Priorität 3 aktiviert  
   
   _**OperationalClassifications**:_  

   |Protokoll|Porttyp /|Priority|
   |--------|---------|--------|
   |Standard|&nbsp;|0|
   |NetDirect| 445|3|
   ---

   
7. Reservieren der Hälfte der Bandbreite für SMB Direct \(RDMA\)

   ```PowerShell
   New-NetQosTrafficClass "SMB" -priority 3 -bandwidthpercentage 50 -algorithm ETS
   ```
   
   _**Ergebnisse:**_  
   
   |Name|Algorithmus |Bandwidth(%)| Priority |PolicySet |IfIndex |IfAlias |
   |----|---------| ------------ |--------| ---------|------- |------- |
   |SMB | ETS     | 50 |3 |Global |&nbsp;|&nbsp;|   
   ---

8. Zeigen Sie die Reservierung bandbreiteneinstellungen an:   

   ```PowerShell
   Get-NetQosTrafficClass | ft -AutoSize
   ```
   
   _**Ergebnisse:**_  

   |Name|Algorithmus |Bandwidth(%)| Priority |PolicySet |IfIndex |IfAlias |
   |----|---------| ------------ |--------| ---------|------- |------- |
   |[Standard]| ETS|50 |0-2,4-7|  Global|&nbsp;|&nbsp;| 
   |SMB |ETS|50 |3 |Global|&nbsp;|&nbsp;| 
   ---
   
9. (Optional) Erstellen Sie zwei zusätzliche Klassen für den Mandanten IP-Datenverkehr. 

   >[!TIP]
   >Sie können die Werte für "IP1" und "IP2" weglassen.

   ```PowerShell
   New-NetQosTrafficClass "IP1" -Priority 1 -bandwidthpercentage 10 -algorithm ETS
   ```
   
   _**Ergebnisse:**_
   
   |Name|Algorithmus |Bandwidth(%)| Priority |PolicySet |IfIndex |IfAlias |
   |----|---------| ------------ |--------| ---------|------- |------- |
   |IP1 |ETS |10 |1 |Global|&nbsp;|&nbsp;|
   ---
   
   ```PowerShell
   New-NetQosTrafficClass "IP2" -Priority 2 -bandwidthpercentage 10 -algorithm ETS
   ```
   
   _**Ergebnisse:**_

   |Name|Algorithmus |Bandwidth(%)| Priority |PolicySet |IfIndex |IfAlias |
   |----|---------| ------------ |--------| ---------|------- |------- |
   |IP2 |ETS |10 |2 |Global|&nbsp;|&nbsp;|
   ---
   
10. Zeigen Sie die QoS-Klassen.

    ```PowerShell
    Get-NetQosTrafficClass | ft -AutoSize
    ```
    
    _**Ergebnisse:**_

    |Name|Algorithmus |Bandwidth(%)| Priority |PolicySet |IfIndex |IfAlias |
    |----|---------| ------------ |--------| ---------|------- |------- |
    |[Standard] |ETS |30 |0,4-7 |Global|&nbsp;|&nbsp;|
    |SMB |ETS |50 |3 |Global|&nbsp;|&nbsp;|
    |IP1 |ETS |10 |1 |Global|&nbsp;|&nbsp;|
    |IP2 |ETS |10 |2 |Global|&nbsp;|&nbsp;|
    ---
   
11. (Optional) Überschreiben Sie den Debugger an.<p>Standardmäßig wird für der angefügte Debugger NetQos blockiert. 

    ```PowerShell
    Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 –Force
    Get-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" | ft AllowFlowControlUnderDebugger
    ```

    _**Ergebnisse:**_  

    ```
    AllowFlowControlUnderDebugger
    -----------------------------
    1
    ```

## <a name="step-5-verify-the-rdma-configuration-mode-1"></a>Schritt 5 Überprüfen Sie die RDMA-Konfiguration \(Modus 1\) 

Sie möchten sicherstellen, dass das Fabric ordnungsgemäß konfiguriert ist, bevor Sie einen vSwitch erstellen und auf RDMA \(Modus 2\).

Die folgende Abbildung zeigt den aktuellen Zustand des Hyper-V-Hosts.

![Test RDMA](../../media/Converged-NIC/4-datacenter-test-rdma.jpg)


1. Überprüfen Sie die RDMA-Konfiguration.

   ```PowerShell
   Get-NetAdapterRdma | ft -AutoSize
   ```
   
   _**Ergebnisse:**_

   |Name |InterfaceDescription |Enabled|
   |----|--------------------|-------|
   |TEST-40G-1| Mellanox ConnectX-4-VPI Adapter #2 |True|
   |TEST-40G-2| Mellanox ConnectX-4-VPI-Adapter |True|
   ---

2. Bestimmen der **IfIndex** Wert Ihrer Zieladapter.<p>Sie verwenden diesen Wert in den nachfolgenden Schritten aus, wenn Sie das Skript ausführen, die, das Sie herunterladen.   

   ```PowerShell
   Get-NetIPConfiguration -InterfaceAlias "TEST*" | ft InterfaceAlias,InterfaceIndex,IPv4Address
   ```
   
   _**Ergebnisse:**_

   |InterfaceAlias |InterfaceIndex |IPv4-Adresse|
   |-------------- |-------------- |-----------|
   |TEST-40G-1 |14 |{192.168.1.3}|
   |TEST-40G-2 | 13 |{192.168.2.3}|
   ---
   
3. Herunterladen der [DiskSpd.exe Hilfsprogramm](https://aka.ms/diskspd) und extrahieren Sie es in C:\TEST\.

4. Herunterladen der [Test-RDMA-PowerShell-Skript](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1) in einem Testordner auf dem lokalen Laufwerk, z. B. C:\TEST\.

5. Führen Sie die **Test-Rdma.ps1** PowerShell-Skript für den IfIndex-Wert an das Skript, mit der IP-Adresse des ersten remote-Adapters in demselben VLAN zu übergeben.<p>In diesem Beispiel leitet das Skript die **IfIndex** Wert 14 Remotenetzwerk Adapter IP-Adresse 192.168.1.5 erstellt.
   
   ```PowerShell
   C:\TEST\Test-RDMA.PS1 -IfIndex 14 -IsRoCE $true -RemoteIpAddress 192.168.1.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**Ergebnisse:**_ 
   
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
   >Wenn der RDMA-Datenverkehr für den Fall RoCE insbesondere ein Fehler auftritt, finden Sie in Ihrer Konfiguration der ToR-Switch geeigneten PCF/ETS-Konfigurationseinstellungen, die die Einstellungen für den Host übereinstimmen sollten. Finden Sie in den QoS-Abschnitt in diesem Dokument Referenzwerte.

6. Führen Sie die **Test-Rdma.ps1** PowerShell-Skript für den IfIndex-Wert an das Skript, mit der IP-Adresse des zweiten Adapters remote auf demselben VLAN zu übergeben.<p>In diesem Beispiel leitet das Skript die **IfIndex** Wert 13 in der remote-IP-Netzwerkadapteradresse 192.168.2.5.

   ```PowerShell
   C:\TEST\Test-RDMA.PS1 -IfIndex 13 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**Ergebnisse:**_ 
   
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

## <a name="step-6-create-a-hyper-v-vswitch-on-your-hyper-v-hosts"></a>Schritt 6 Erstellen Sie einen Hyper-V-Switchs auf den Hyper-V-hosts


Die folgende Abbildung zeigt die Hyper-V Host 1 mit einem vSwitch.

![Erstellen eines virtuellen Hyper-V-Switch](../../media/Converged-NIC/5-datacenter-create-vswitch.jpg)

1. Erstellen Sie einen vSwitch im Modus für Hyper-V-Host 1 festlegen.

   ```PowerShell
   New-VMSwitch –Name "VMSTEST" –NetAdapterName "TEST-40G-1","TEST-40G-2" -EnableEmbeddedTeaming $true -AllowManagementOS $true
   ```
   
   _**Ergebnis:**_

   |Name |SwitchType |NetAdapterInterfaceDescription|
   |---- |---------- |------------------------------|
   |VMSTEST |Extern |Team-Schnittstelle|
   ---
   
2. Zeigen Sie den physischen Adapter-Teams im Satz ein.

   ```PowerShell
   Get-VMSwitchTeam -Name "VMSTEST" | fl
   ```
   
   _**Ergebnisse:**_  
   
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
   
   _**Ergebnisse:**_

   |Name |InterfaceDescription |ifIndex |Status |MacAddress |LinkSpeed|
   |---- |--------------------|-------|------|----------|---------|
   |vEthernet (VMSTEST)|Virtuelle Hyper-V-Ethernet-Adapter #2 |28 |Nach oben|E4-1D-2D-07-40-71|80 Gbit/s|
   ---
   
4. Zeigen Sie zusätzliche Eigenschaften für die Host-vNIC. 

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS
   ```
   
   _**Ergebnisse:**_

   |Name |IsManagementOs |VMName |SwitchName |MacAddress |Status |IP-Adressen|
   |----|--------------|------|----------|----------|------|-----------|
   |VMSTEST|True |VMSTEST |E41D2D074071| {Ok}|&nbsp;|
   ---
   

5. Testen Sie die Netzwerkverbindung mit dem remote-VLAN-101-Adapter.

   ```PowerShell
   Test-NetConnection 192.168.1.5 
   ```
   
   _**Ergebnisse:**_  
   
   ```
   WARNING: Ping to 192.168.1.5 failed -- Status: DestinationHostUnreachable
    
   ComputerName   : 192.168.1.5
   RemoteAddress  : 192.168.1.5
   InterfaceAlias : vEthernet (CORP-External-Switch)
   SourceAddress  : 10.199.48.170
   PingSucceeded  : False
   PingReplyDetails (RTT) : 0 ms
   ```
   
## <a name="step-7-remove-the-access-vlan-setting"></a>Schritt 7 Entfernen Sie die Access-VLAN-Einstellung

In diesem Schritt entfernen Sie die ACCESS-VLAN-Einstellung, die physische NIC und die VLAN-ID mithilfe der vSwitch festlegen.

Sie müssen die ACCESS-VLAN-Einstellung, um zu verhindern, dass beide automatische Kennzeichnung des ausgehende Datenverkehrs durch die falsche VLAN-ID entfernen und Filtern der eingehenden Datenverkehr, die nicht mit der ZUGRIFFS-VLAN-ID übereinstimmen

1. Entfernen Sie die Einstellung ein.
    
   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name "Test-40G-1" -RegistryKeyword VlanID -RegistryValue "0"
   Set-NetAdapterAdvancedProperty -Name "Test-40G-2" -RegistryKeyword VlanID -RegistryValue "0"
   ```

2. Legen Sie die VLAN-ID.

   ```PowerShell
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "VMSTEST" -VlanId "101" -Access -ManagementOS
   Get-VMNetworkAdapterVlan -ManagementOS -VMNetworkAdapterName "VMSTEST"
   ```
   
   _**Ergebnisse:**_  
   
   ```
   VMName VMNetworkAdapterName Mode   VlanList
   ------ -------------------- ----   --------
          VMSTEST              Access 101     
   ```
   
   
3. Testen Sie die Netzwerkverbindung.

   ```PowerShell
   Test-NetConnection 192.168.1.5
   ```
   
   _**Ergebnisse:**_   
   
   ```
   ComputerName   : 192.168.1.5
   RemoteAddress  : 192.168.1.5
   InterfaceAlias : vEthernet (VMSTEST)
   SourceAddress  : 192.168.1.3
   PingSucceeded  : True
   PingReplyDetails (RTT) : 0 ms
   ```

   >**WICHTIGE** Wenn die Ergebnisse nicht mit den Beispielergebnissen vergleichbar sind und Ping, mit der Meldung fehlschlägt "Warnung: Fehler bei der Ping an 192.168.1.5 erstellt – Status: DestinationHostUnreachable,"bestätigen, dass die"vEthernet (VMSTEST)"die richtige IP-Adresse verfügt.
   >
   >```PowerShell
   >Get-NetIPAddress -InterfaceAlias "vEthernet (VMSTEST)"
   >```
   >
   >Wenn die IP-Adresse nicht festgelegt ist, korrigieren Sie das Problem.
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
   

4. Benennen Sie die Verwaltungs-NIC

   ```PowerShell
   Rename-VMNetworkAdapter -ManagementOS -Name “VMSTEST” -NewName “MGT”
   Get-VMNetworkAdapter -ManagementOS
   ```
   
   _**Ergebnisse:**_ 
   
   |Name |IsManagementOs |VMName |SwitchName |MacAddress |Status |IP-Adressen
   |----|--------------|------|----------|----------|------|-----------|
   |CORP-External-Switch |True |&nbsp;|CORP-External-Switch |001B785768AA |{Ok}|&nbsp;|
   |MGT |True |&nbsp;|VMSTEST |E41D2D074071 |{Ok}|&nbsp;|
   ---
   
5. Zeigt zusätzliche NIC-Eigenschaften.

   ```PowerShell
   Get-NetAdapter
   ```
   
   _**Ergebnisse:**_

   |Name |InterfaceDescription |ifIndex |Status |MacAddress |LinkSpeed|
   |----|--------------------|------|----------|---------|------|
   |vEthernet (MGT) |Virtuelle Hyper-V-Ethernet-Adapter #2 |28 |Nach oben | E4-1D-2D-07-40-71 |80 Gbit/s|
   ---
   
## <a name="step-8-test-hyper-v-vswitch-rdma"></a>Schritt 8. Testen von Hyper-V-Switchs RDMA

Die folgende Abbildung zeigt den aktuellen Zustand des Hyper-V-Hosts, einschließlich der vSwitch auf dem Hyper-V Host 1.

![Testen Sie den virtuellen Hyper-V-Switch](../../media/Converged-NIC/6-datacenter-test-vswitch-rdma.jpg)

1. Festlegen der Priorität für die Host-vNIC die vorherigen VLAN-Einstellungen als Ergänzung zu kennzeichnen.

   ```PowerShell    
   Set-VMNetworkAdapter -ManagementOS -Name "MGT" -IeeePriorityTag on
   Get-VMNetworkAdapter -ManagementOS -Name "MGT" | fl Name,IeeePriorityTag
   ```
   
   _**Ergebnisse:**_  
      
   Name: MGT  
   IeeePriorityTag:  Ein  
    
2. Erstellen Sie zwei Host-vNICs für RDMA und verbinden Sie sie mit der vSwitch VMSTEST.

   ```PowerShell    
   Add-VMNetworkAdapter –SwitchName "VMSTEST" –Name SMB1 –ManagementOS
   Add-VMNetworkAdapter –SwitchName "VMSTEST" –Name SMB2 –ManagementOS
   ```
   
3. Anzeigen der Verwaltungs-NIC-Eigenschaften.

   ```PowerShell    
   Get-VMNetworkAdapter -ManagementOS
   ```
   
   _**Ergebnisse:**_ 

   |Name |IsManagementOs |VMName |SwitchName |MacAddress |Status |IP-Adressen|
   |----|--------------|------|----------|----------|------|-----------|
   |CORP-External-Switch |True |CORP-External-Switch |001B785768AA|{Ok} |&nbsp;| 
   |Mgt |True |VMSTEST |E41D2D074071 |{Ok} |&nbsp;|
   |SMB1 |True |VMSTEST |00155D30AA00 |{Ok} |&nbsp;|
   |SMB2 |True |VMSTEST |00155D30AA01 |{Ok} |&nbsp;|
   ---
   
## <a name="step-9-assign-an-ip-address-to-the-smb-host-vnics-vethernet-smb1-and-vethernet-smb2"></a>Schritt 9: Zuweisen eine IP-Adresse, die SMB-Host-vNICs vEthernet \(SMB1\) und vEthernet \(SMB2\)

Der TEST-40G-1 und TEST-40G-2 physischen Adaptern haben immer noch ein VLAN Zugriff von 101 und 102 konfiguriert. Aus diesem Grund die Adapter Markieren des Datenverkehrs - Angestellte und Ping erfolgreich ist. Zuvor Sie beide pNIC VLAN-IDs 0 (null) konfiguriert und dann die VMSTEST vSwitch auf VLAN 101 festgelegt. Anschließend konnten Sie trotzdem den remote-VLAN-101-Adapter mithilfe der vNIC MGT pingen, aber derzeit keine VLAN-102-Elemente vorhanden sind.



1. Entfernen Sie die ACCESS-VLAN-Einstellung über die physische NIC, um zu verhindern, dass sie sowohl automatische Kennzeichnung des ausgehende Datenverkehrs durch die falsche VLAN-ID und um zu verhindern, Filtern eingehenden Datenverkehr, der mit der ZUGRIFFS-VLAN-ID übereinstimmt

   ```PowerShell    
   New-NetIPAddress -InterfaceAlias "vEthernet (SMB1)" -IPAddress 192.168.2.111 -PrefixLength 24
   ```

   _**Ergebnisse:**_  

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

2. Testen Sie den remote-VLAN-102-Adapter.
    
   ```PowerShell
   Test-NetConnection 192.168.2.5 
   ```
   
   _**Ergebnisse:**_  
   
   ```
   ComputerName   : 192.168.2.5
   RemoteAddress  : 192.168.2.5
   InterfaceAlias : vEthernet (SMB1)
   SourceAddress  : 192.168.2.111
   PingSucceeded  : True
   PingReplyDetails (RTT) : 0 ms
   ```
    
3. Hinzufügen einer neuen IP-Adresse für die Schnittstelle vEthernet \(SMB2\).

   ```PowerShell
   New-NetIPAddress -InterfaceAlias "vEthernet (SMB2)" -IPAddress 192.168.2.222 -PrefixLength 24 
   ```
   
   _**Ergebnisse:**_ 
   
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


5. Platzieren Sie die RDMA-Host-vNICs, auf die bereits vorhandene VLAN-102.

   ```PowerShell
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "SMB1" -VlanId "102" -Access -ManagementOS
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "SMB2" -VlanId "102" -Access -ManagementOS
    
   Get-VMNetworkAdapterVlan -ManagementOS
   ```

   _**Ergebnisse:**_ 

   ```   
   VMName VMNetworkAdapterName Mode VlanList
   ------ -------------------- ---- --------
      SMB1 Access   102 
      Mgt  Access   101 
      SMB2 Access   102 
      CORP-External-Switch Untagged
   ```
   
6. Überprüfen Sie die Zuordnung der SMB1 und SMB2 an die zugrunde liegenden physischen NICs unter vSwitches Team festlegen.<p>Die Zuordnung des Host-vNIC auf physische NICs ist zufällig und unterliegen den Ausgleich während der Erstellung und Zerstörung. In diesem Fall können Sie eine indirekte Methode zum Überprüfen der aktuellen Zuordnung. Die MAC-Adressen der SMB1 und SMB2 werden der NIC-Team-Member-TEST-40G-2 zugeordnet. Dies ist nicht ideal, da der Test-40G-1 verfügt nicht über eine zugeordnete SMB-Host-vNIC, und lässt nicht für die Auslastung des Datenverkehrs von RDMA über den Link erst eine SMB-Host-vNIC, die dieser zugeordnet ist.

   ```PowerShell    
   Get-NetAdapterVPort (Preferred)
    
   Get-NetAdapterVmqQueue
   ```
   
   _**Ergebnisse:**_ 
   
   ```
   Name   QueueID MacAddressVlanID Processor VmFriendlyName
   ----   ------- ---------------- --------- --------------
   TEST-40G-1 1   E4-1D-2D-07-40-71 1010:17
   TEST-40G-2 1   00-15-5D-30-AA-00 1020:17
   TEST-40G-2 2   00-15-5D-30-AA-01 1020:17
   ```

7. Zeigen Sie die VM-Eigenschaften des Netzwerkadapters an.

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS
   ```
   
   _**Ergebnisse:**_ 
   
   ```
   Name IsManagementOs VMName SwitchName   MacAddress   Status IPAddresses
   ---- -------------- ------ ----------   ----------   ------ -----------
   CORP-External-Switch True  CORP-External-Switch 001B785768AA {Ok}  
   Mgt  True  VMSTEST  E41D2D074071 {Ok}  
   SMB1 True  VMSTEST  00155D30AA00 {Ok}  
   SMB2 True  VMSTEST  00155D30AA01 {Ok}  
   ```

8. Zeigen Sie die Netzwerkzuordnung des Adapter-Team.<p>Die Ergebnisse sollten keine Informationen zurück, da Sie noch keine Zuordnung ausgeführt haben.
    
   ```PowerShell
   Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName SMB1
   Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName SMB2
   ```
   
   
9. Ordnen Sie SMB1 und SMB2, um die Mitglieder der physischen NIC-Teams zu trennen, und klicken Sie zum Anzeigen der Ergebnisse Ihrer Aktionen.

   >[!IMPORTANT]
   >Stellen Sie sicher, dass bei dieses Schritts, bevor Sie fortfahren Abschluss, oder die Implementierung ein Fehler auftritt.
    
   ```PowerShell
   Set-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName "SMB1" -PhysicalNetAdapterName "Test-40G-1"
   Set-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName "SMB2" -PhysicalNetAdapterName "Test-40G-2"
    
   Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST
   ```

   _**Ergebnisse:**_ 
   
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
   
10. Vergewissern Sie sich die MAC-Zuordnungen, die zuvor erstellt haben.

    ```PowerShell    
    Get-NetAdapterVmqQueue
    ```

    _**Ergebnisse:**_ 
   
    ```   
    Name   QueueID MacAddressVlanID Processor VmFriendlyName
    ----   ------- ---------------- --------- --------------
    TEST-40G-1 1   E4-1D-2D-07-40-71 1010:17
    TEST-40G-1 2   00-15-5D-30-AA-00 1020:17
    TEST-40G-2 1   00-15-5D-30-AA-01 1020:17
    ```


11. Testen Sie die Verbindung vom Remotesystem aus, da beide NICs des Hosts im gleichen Subnetz befinden und die gleiche VLAN-ID haben \(102\).

    ```PowerShell 
    Test-NetConnection 192.168.2.111
    ```

    _**Ergebnisse:**_   

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

    _**Ergebnisse:**_   

    ```
    ComputerName   : 192.168.2.222
    RemoteAddress  : 192.168.2.222
    InterfaceAlias : Test-40G-2
    SourceAddress  : 192.168.2.5
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms 
    ```
12. Festlegen Sie der Name, Name des Netzwerkswitchs und prioritätstags.   

    ```PowerShell
    Set-VMNetworkAdapter -ManagementOS -Name "SMB1" -IeeePriorityTag on
    Set-VMNetworkAdapter -ManagementOS -Name "SMB2" -IeeePriorityTag on
    Get-VMNetworkAdapter -ManagementOS -Name "SMB*" | fl Name,SwitchName,IeeePriorityTag,Status
    ```

    _**Ergebnisse:**_   
    
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

13. Zeigen Sie die vEthernet-Eigenschaften des Netzwerkadapters an.
    
    ```PowerShell
    Get-NetAdapterRdma -Name "vEthernet*" | sort Name | ft -AutoSize
    ```

    _**Ergebnisse:**_   

    ```
    Name  InterfaceDescription Enabled
    ----  -------------------- -------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  False  
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  False  
    vEthernet (MGT)   Hyper-V Virtual Ethernet Adapter #2  False   
    ```

14. Aktivieren Sie die vEthernet-Netzwerkadaptern.  
    
    ```PowerShell
    Enable-NetAdapterRdma -Name "vEthernet (SMB1)"
    Enable-NetAdapterRdma -Name "vEthernet (SMB2)"
    Get-NetAdapterRdma -Name "vEthernet*" | sort Name | fl *
    ```

    _**Ergebnisse:**_   
    
    ```
    Name  InterfaceDescription Enabled
    ----  -------------------- -------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  True   
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  True  
    vEthernet (MGT)   Hyper-V Virtual Ethernet Adapter #2  False
    ```

## <a name="step-10-validate-the-rdma-functionality"></a>Schritt 10 fort. Überprüfen Sie die RDMA-Funktionalität.

Möchten Sie die RDMA-Funktionalität vom Remotesystem auf dem lokalen System zu überprüfen, bei denen einen vSwitch, um beide Mitglieder des Teams Satz vSwitch verfügt.<p>Da beide Host-vNICs \(SMB1 und SMB2\) zugewiesen sind, VLAN-102, können Sie die VLAN-102-Adapter auf dem remoten System auswählen. <p>In diesem Beispiel wird der NIC-Test-40G-2 RDMA auf SMB1 (192.168.2.111) und SMB2 (192.168.2.222).

>[!TIP]
>Sie müssen möglicherweise die Firewall auf diesem System deaktivieren.  Einzelheiten finden Sie in der Fabric-Richtlinie.
>
>```PowerShell
>Set-NetFirewallProfile -All -Enabled False
>    
>Get-NetAdapterAdvancedProperty -Name "Test-40G-2"
>```
>
>_**Ergebnisse:**_ 
>   
>```
>Name  DisplayNameDisplayValue   RegistryKeyword RegistryValue  
>----  -----------------------   --------------- -------------  
> .
> .
>Test-40G-2VLAN ID102VlanID  {102} 
>```
    
1. Anzeigen von den Eigenschaften des Netzwerkadapters.

   ```PowerShell
   Get-NetAdapter
   ```
    
   _**Ergebnisse:**_ 
    
   ```
   Name  InterfaceDescriptionifIndex Status   MacAddress LinkSpeed
   ----  --------------------------- ------   ---------- ---------
   Test-40G-2Mellanox ConnectX-3 Pro Ethernet A...#3   3 Up   E4-1D-2D-07-43-D140 Gbps
   ```
   
2. Zeigen Sie den Netzwerkadapter RDMA-Informationen.

   ```PowerShell
   Get-NetAdapterRdma
   ```
    
   _**Ergebnisse:**_  
    
   ```
   Name  InterfaceDescription Enabled
   ----  -------------------- -------
   Test-40G-2Mellanox ConnectX-3 Pro Ethernet Adap... True   
   ```

3. Führen Sie den Test der RDMA-Datenverkehr auf den ersten physischen Adapter aus.

   ```PowerShell 
   C:\TEST\Test-RDMA.PS1 -IfIndex 3 -IsRoCE $true -RemoteIpAddress 192.168.2.111 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```
    
   _**Ergebnisse:**_ 
    
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

4. Führen Sie den Test der RDMA-Datenverkehr, auf den zweiten physischen Adapter aus.

   ```PowerShell
   C:\TEST\Test-RDMA.PS1 -IfIndex 3 -IsRoCE $true -RemoteIpAddress 192.168.2.222 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```
    
   _**Ergebnisse:**_ 
    
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
    
5. Test für RDMA-Datenverkehr vom lokalen an den Remotecomputer.

    ```PowerShell
    Get-NetAdapter | ft –AutoSize
    ```
    
    _**Ergebnisse:**_ 
    
    ```
    Name  InterfaceDescriptionifIndex Status   MacAddress LinkSpeed
    ----  --------------------------- ------   ---------- ---------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  45 Up   00-15-5D-30-AA-0380 Gbps
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  41 Up   00-15-5D-30-AA-0280 Gbps
    ```

6. Führen Sie den Test der RDMA-Datenverkehr auf dem ersten virtuellen Adapter.    
    
   ```
   C:\TEST\Test-RDMA.PS1 -IfIndex 41 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```
    
   _**Ergebnisse:**_ 
    
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

7. Führen Sie den Test der RDMA-Datenverkehr auf den zweiten virtuellen Adapter an.

   ```PowerShell
   C:\TEST\Test-RDMA.PS1 -IfIndex 45 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```
    
   _**Ergebnisse:**_ 
    
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
    
Die letzte Zeile in dieser Ausgabe ist "RDMA-Datenverkehr Test erfolgreich: RDMA-Datenverkehr wurde an 192.168.2.5, gesendet"zeigt, dass Sie erfolgreich Converged NIC auf dem Adapter konfiguriert haben.

## <a name="related-topics"></a>Verwandte Themen 

- [Zusammengeführte NIC-Konfiguration mit einem einzelnen Netzwerkadapter](cnic-single.md)
- [Konfiguration der physischen Switch für zusammengeführte NIC](cnic-app-switch-config.md)
- [Problembehandlung bei Converged NIC-Konfigurationen](cnic-app-troubleshoot.md)
