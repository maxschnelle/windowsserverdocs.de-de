---
title: Zusammengeführtes NIC-Konfiguration mit einem einzelnen Netzwerkadapter
description: Dieses Thema enthält Anweisungen zum Bereitstellen eines zusammengeführten NIC mit einem einzelnen Netzwerkadapter in Windows Server2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: eed5c184-fa55-43a8-a879-b1610ebc70ca
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d6663a966026afb301a4bad90a9573d16fc82875
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="converged-nic-configuration-with-a-single-network-adapter"></a>Zusammengeführtes NIC-Konfiguration mit einem einzelnen Netzwerkadapter

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Die folgenden Abschnitte enthalten Anweisungen zum Konfigurieren der zusammengeführten NIC mit einer NIC in Ihrem Hyper-V-Host.

Die Beispielkonfiguration in dieser Anleitung zeigt zwei Hyper-V-Hosts **Hyper-V-Host ein**, und **Hyper-V-Host B**.

## <a name="test-connectivity-between-source-and-destination"></a>Testen der Konnektivität zwischen Quell- und Zielserver

Dieser Abschnittenthält die erforderlichen Schrittezum Testen der Konnektivität zwischen Quell- und Zielserver Hyper-V-Hosts.

Die folgende Abbildungzeigt zwei Hyper-V-Hosts **Hyper-V-Host ein** und **Hyper-V-Host B**. 

Auf beiden Servern eine einzelne physische Netzwerkkarte (pNIC) installiert sein, und die NICs mit einem Anfang Rack \(ToR\) physischen Switch verbunden sind. Darüber hinaus die Server im gleichen Subnetz befinden sich 192.168.1.x/24.

![Hyper-V-Hosts](../../media/Converged-NIC/1-single-test-conn.jpg)


### <a name="test-nic-connectivity-to-the-hyper-v-virtual-switch"></a>Testen der Konnektivität der NIC mit dem virtuellen Hyper\-V-Switch

Verwenden Sie diesen Schritt, können Sie sicherstellen, dass die physische NIC, für die Sie später einen virtuellen Hyper\-V-Switch erstellen, auf dem Zielhost zugreifen kann. 

Bei diesem Test wird Konnektivität mit Layer 3-\(L3\) - oder die IP-Layer - als auch Schicht-2-\(L2\) veranschaulicht.

Die folgenden Windows PowerShell-Befehl können Sie die Eigenschaften des Netzwerkadapters abrufen.

    Get-NetAdapter
     
Folgendes sind die Ergebnisse dieses Befehls.

|Name|InterfaceDescription|ifIndex|Status|MacAddress|LinkSpeed|
|-----|--------------------|-------|-----|----------|---------|
|
|M1|Mellanox ConnectX-3 Pro...| 4| Nach-oben|7C-FE-90-93-8F-A1|40-Gbit/s|

Sie können einen der folgenden Befehle um zusätzliche Eigenschaften, z.B. die IP-Adresse zu erhalten.

    Get-NetAdapter M1 | fl *

Folgen bearbeitete Beispielergebnisse dieses Befehls.
    
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
    

### <a name="ensure-that-source-and-destination-can-communicate"></a>Stellen Sie sicher, dass Quell- und Zielserver kommunizieren können

Sie können diesen Schrittbidirektionale Kommunikation überprüfen \ (Ping von der Quelle zum Ziel und umgekehrt auf beide Systems\).  Im folgenden Beispiel der **Test NetConnection** Windows PowerShell-Befehl verwendet wird, aber bevorzugt, wenn Sie können die **Ping** Befehl. 

>[!NOTE]
>Wenn Sie sicher sind, dass die Hosts kommunizieren können, können Sie diesen Schrittüberspringen.

    Test-NetConnection 192.168.1.5

Folgendes sind die Ergebnisse dieses Befehls.

|Parameter|Wert|
|---------|-----|
|
|ComputerName|192.168.1.5|
|RemoteAddress|192.168.1.5|
|InterfaceAlias|M1|
|SourceAddress|192.168.1.3|
|PingSucceeded|"True"|
|PingReplyDetails \(RTT\)|0 ms|

In einigen Fällen müssen Sie die Windows-Firewall mit erweiterter Sicherheit erfolgreich Ausführen dieses Tests deaktivieren. Wenn Sie die Firewall deaktivieren, Bedenken Sie Sicherheit, und stellen Sie sicher, dass die Konfiguration Ihres Unternehmens die Sicherheit erfüllt.

Befehl im folgenden Beispiel können Sie alle Firewallprofile deaktivieren.

    Set-NetFirewallProfile -All -Enabled False
    
Nachdem Sie die Firewall deaktiviert haben, können Sie den folgenden Befehl, um die Verbindung zu testen.

    Test-NetConnection 192.168.1.5

Folgendes sind die Ergebnisse dieses Befehls.

|Parameter|Wert|
|---------|-----|
|
|ComputerName|192.168.1.5|
|RemoteAddress|192.168.1.5|
|InterfaceAlias|Test-40G-1|
|SourceAddress|192.168.1.3|
|PingSucceeded|"False"|
|PingReplyDetails \(RTT\)|0 ms|

## <a name="configure-vlans-optional"></a>Konfigurieren von VLANs \(Optional\)

Viele Netzwerkkonfigurationen stellen VLANs verwenden. Wenn Sie VLANs in Ihrem Netzwerk verwenden möchten, müssen Sie den vorherigen Tests mit VLANs konfiguriert wiederholen. \ (Wenn Sie RoCE für RDMA-Dienste verwenden möchten, müssen Sie VLANs aktivieren. \)

Für diesen Schrittwerden die NICs in **Zugriff** Modus. Bei der Erstellung einer virtuellen Hyper-V-Switch \(vSwitch\) weiter unten in diesem Handbuch werden jedoch die VLAN-Eigenschaften auf der Ebene der vSwitch-Port angewendet. 

Da ein Switch mehrere VLANs hosten kann, ist es erforderlich, für den Top of Rack \(ToR\) physischen Switch, den Port zu verfügen, den mit der Host im trunkmodus konfiguriert verbunden ist.

>[!NOTE]
>Anweisungen zum Konfigurieren der trunkmodus auf dem Switch finden Sie in der Dokumentation Ihres ToR-Switch.

Die folgende Abbildungzeigt zwei Hyper-V-Hosts mit einem physischen Netzwerkadapter, und jedes VLAN 101 kommunizieren konfiguriert.

![Konfigurieren Sie virtuelle lokale Netzwerke](../../media/Converged-NIC/2-single-configure-vlans.jpg)

### <a name="configure-the-vlan-id"></a>Konfigurieren Sie die VLAN-ID

Sie können diesen Schrittverwenden, so konfigurieren Sie die VLAN-IDs für Netzwerkkarten in Hyper-V-Hosts installiert.

#### <a name="configure-nic-m1"></a>Konfigurieren des NIC-M1

Konfigurieren Sie mit den folgenden Befehlen die VLAN-ID für die erste Netzwerkkarte, M1, und zeigen Sie dann die resultierende Konfiguration.

>[!IMPORTANT]
>Führen Sie mit diesem Befehl nicht aus, wenn Sie an den Host Remote über die Schnittstelle verbunden sind, da dadurch der Zugriff auf den Host führt.
    
    Set-NetAdapterAdvancedProperty -Name M1 -RegistryKeyword VlanID -RegistryValue "101"
    Get-NetAdapterAdvancedProperty -Name M1 | Where-Object {$_.RegistryKeyword -eq "VlanID"} 
    
Folgendes sind die Ergebnisse dieses Befehls.

|Name |"DisplayName"| DisplayValue| RegistryKeyword |RegistryValue|
|----|-----------|------------|---------------|-------------|
|
|M1|VLAN-ID|101|VLAN-ID|{101}|


Stellen Sie sicher, dass die VLAN-ID wirksam, die unabhängig von der Implementierung der Netzwerk-Adapter wird mithilfe des folgenden Befehls, um den Netzwerkadapter neu zu starten.

    Restart-NetAdapter -Name "M1"

Sie können den folgenden Befehl verwenden, um sicherzustellen, dass der Status des Netzwerkadapters **von** bevor Sie fortfahren.

    Get-NetAdapter -Name "M1"

Folgendes sind die Ergebnisse dieses Befehls.

|Name|InterfaceDescription|ifIndex| Status|MacAddress|LinkSpeed|
|----|--------------------|-------|------|----------| ---------|
|
|M1|Mellanox ConnectX-3 Pro Ethernet Ada...|4|Nach-oben|7C-FE-90-93-8F-A1|40-Gbit/s|

Stellen Sie sicher, dass Sie diesen Schritt, auf dem lokalen und den Zielserver durchführen. Wenn der Zielserver nicht mit der gleichen VLAN-ID wie der lokale Server konfiguriert ist, können nicht beide kommunizieren.

### <a name="verify-connectivity"></a>Überprüfen Sie die Konnektivität

In diesem Abschnittkönnen eine um Verbindung zu überprüfen, nachdem die Netzwerkadapter neu gestartet werden. Sie können die Konnektivität überprüfen, nach dem Anwenden des VLAN-Tags auf beiden Adaptern. Wenn die Verbindung ein Fehler auftritt, können Sie den Switch VLAN-Konfiguration oder das Ziel Teilnahme an demselben VLAN überprüfen. 

>[!IMPORTANT]
>Nachdem Sie die Schritteim vorherigen Abschnittausführen, kann es einige Sekunden für das Gerät neu starten und werden im Netzwerk verfügbar dauern.

#### <a name="verify-connectivity-for-nic-test-40g-1"></a>Überprüfen Sie die Konnektivität für NIC Test-40G-1

Um die Konnektivität für die erste Netzwerkkarte zu überprüfen, können Sie den folgenden Befehl ausführen.

    Test-NetConnection 192.168.1.5
    
## <a name="configure-data-center-bridging-dcb"></a>Konfigurieren von Data Center Bridging \(DCB\)

Der nächste Schrittist so konfigurieren Sie \(QoS\) DCB und Quality of Service, der erfordert, dass Sie zuerst das Feature "Windows Server2016" DCB installieren.

>[!NOTE]
>Sie müssen die folgenden Konfigurationsschritte DCB und QoS auf allen Servern ausführen, die miteinander kommunizieren sollen.

### <a name="install-data-center-bridging-dcb"></a>Installieren Sie Data Center Bridging \(DCB\)

Sie können diesen Schrittzum Installieren und aktivieren DCB verwenden. 

>[!IMPORTANT]
>- Installieren und Konfigurieren von DCB ist **optionale** für Netzwerkkonfigurationen, die iWarp für RDMA-Dienste verwenden.
>- Installieren und Konfigurieren von DCB ist **erforderlichen** für Netzwerkkonfigurationen, die RoCE \(any Version\) für RDMA-Dienste verwenden.


Sie können den folgenden Befehl verwenden, DCB auf allen Hyper-V-Hosts zu installieren. 

    Install-WindowsFeature Data-Center-Bridging

### <a name="set-the-qos-policies-for-smb-direct"></a>Legen Sie die QoS-Richtlinien für SMB Direct 

Sie können den folgenden Befehl verwenden, Konfigurieren von QoS-Richtlinien für SMB Direct.

>[!IMPORTANT]
>- Dieser Schrittist optional für Netzwerkkonfigurationen, die iWarp verwenden.
>- Dieser Schrittist erforderlich, damit Netzwerkkonfigurationen, die RoCE verwenden.
>- Im folgenden Beispielbefehl ist der Wert "3" beliebige. Sie können einen beliebigen Wert zwischen 1 und 7 verwenden, solange Sie denselben Wert in der Konfiguration von QoS-Richtlinien einheitlich verwendet.

    New-NetQosPolicy "SMB" -NetDirectPortMatchCondition 445 -PriorityValue8021Action 3

Folgendes sind die Ergebnisse dieses Befehls.

|Parameter|Wert|
|---------|-----|
|
|Name |SMB|
|Besitzer|Group Policy \(Machine\)|
|NetworkProfile|Alle|
|Rangfolge|127|
|JobObject|&nbsp;| 
|NetDirectPort|445
|PriorityValue|3

### <a name="for-roce-deployments-turn-on-priority-flow-control-for-smb-traffic"></a>Für RoCE Bereitstellungen aktivieren Priorität flusssteuerung für SMB-Datenverkehr 

Wenn Sie RoCE für Ihre RDMA-Dienste verwenden, können Sie die folgenden Befehle so aktivieren Sie die flusssteuerung für SMB und zum Anzeigen der Ergebnisse verwenden. Priorität Flow Control für RoCE ist erforderlich, aber es ist nicht erforderlich, wenn Sie die iWarp verwenden.

    Enable-NetQosFlowControl -priority 3
    Get-NetQosFlowControl

Folgendes Beispielergebnisse sind die **Get-NetQosFlowControl** Befehl.

|Priorität|Aktiviert|PolicySet|IfIndex|IfAlias|
|---------|-----|--------- |-------| -------|
|
|0 |"False" |Globale|&nbsp;|&nbsp;|
|1 |"False" |Globale|&nbsp;|&nbsp;|
|2 |"False" |Globale|&nbsp;|&nbsp;|
|3 |"True"  |Globale|&nbsp;|&nbsp;|
|4 |"False" |Globale|&nbsp;|&nbsp;|
|5 |"False" |Globale|&nbsp;|&nbsp;|
|6 |"False" |Globale|&nbsp;|&nbsp;|
|7 |"False" |Globale|&nbsp;|&nbsp;|

### <a name="enable-qos-for-the-local-and-destination-network-adapters"></a>Aktivieren von QoS für die lokale und Ziel-Netzwerkadapter
Mit diesem Schrittkönnen Sie DCB für bestimmte Netzwerkadapter aktivieren.

>[!IMPORTANT]
>-  Dieser Schrittist nicht für die Netzwerkkonfigurationen erforderlich, die iWarp verwenden.
>-  Dieser Schrittist erforderlich, damit Netzwerkkonfigurationen, die RoCE verwenden.




#### <a name="enable-qos-for-nic-m1"></a>QoS für NIC M1 aktivieren

Sie können die folgenden Befehle zum Aktivieren von QoS und Anzeigen der Ergebnisse der Konfiguration.

    Enable-NetAdapterQos -InterfaceAlias "M1"
    Get-NetAdapterQos -Name "M1"

Folgendes sind die Ergebnisse dieses Befehls.

**Namen**: M1 **aktiviert**: True **Funktionen**:   

|Parameter|Hardware|Aktuelle|
|---------|--------|-------|
|
|MacSecBypass|NotSupported|NotSupported|
|DcbxSupport|Keine|Keine|
|NumTCs(Max/ETS/PFC)|8/8/8|8/8/8|
 
**OperationalTrafficClasses**: 

|TC|TSA|Bandbreite|Prioritäten|
|----|-----|--------|-------|
|
|0| ETS|70%|0-2,4-7|
|1|ETS|30%|3

**OperationalFlowControl**: Priorität 3 aktiviert **OperationalClassifications**:

|Protokoll|Porttyp /|Priorität|
|--------|---------|--------|
|
|Standardwert|&nbsp;|0|
|NetDirect| 445|3|

### <a name="reserve-a-percentage-of-the-bandwidth-for-smb-direct-rdma"></a>Reservieren Sie einen Prozentsatz der Bandbreite für SMB Direct \(RDMA\)

Den folgenden Befehl können Sie einen Prozentsatz der Bandbreite für SMB Direct reserviert werden muss.  

In diesem Beispiel wird eine bandbreitenreservierung 30% verwendet. Sie sollten einen Wert auswählen, der darstellt, was Sie erwarten, dass Ihre Speicherdatenverkehr erforderlich ist. Der Wert der **- Bandwidthpercentage** Parameter muss ein Vielfaches von 10% sein.

    New-NetQosTrafficClass "SMB" -Priority 3 -BandwidthPercentage 30 -Algorithm ETS

Folgendes sind die Ergebnisse dieses Befehls.

|Name|Algorithmus |Bandwidth(%)| Priorität |PolicySet |IfIndex |IfAlias |
|----|---------| ------------ |--------| ---------|------- |------- |
|
|SMB | ETS     | 30 |3 |Globale |&nbsp;|&nbsp;|                                      
 
Den folgenden Befehl können Sie Bandbreite Reservierungsinformationen anzuzeigen.

    Get-NetQosTrafficClass

Folgendes sind die Ergebnisse dieses Befehls.
 
|Name|Algorithmus |Bandwidth(%)| Priorität |PolicySet |IfIndex |IfAlias |
|----|---------| ------------ |--------| ---------|------- |------- |
|
|[Standard]|ETS|70 |0-2,4-7| Globale|&nbsp;|&nbsp;| 
|SMB      |ETS|30 |3 |Globale|&nbsp;|&nbsp;| 

## <a name="remove-debugger-conflict-mellanox-adapter-only"></a>Entfernen Sie die Debugger-Konflikt \(Mellanox Adapter only\)

Wenn Sie einen Adapter aus Mellanox verwenden, die Sie diesen Schrittkonfigurieren Sie den Debugger ausführen müssen. Standardmäßig blockiert ein Mellanox-Adapter verwendet wird, der angefügte Debugger NetQos. Den folgenden Befehl können Sie um den Debugger außer Kraft setzen.

    
    Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 –Force
    

## <a name="test-rdma-native-host"></a>Test RDMA (systemeigene Host)

Dadurch können Sie sicherstellen, dass das Fabric ordnungsgemäß konfiguriert ist, vor dem Erstellen eines vSwitches und RDMA \(Converged NIC\) wechselt.

Die folgende Abbildungzeigt den aktuellen Status des Hyper-V-Hosts.

![RDMA-Test](../../media/Converged-NIC/4-single-test-rdma.jpg)

Um die RDMA-Konfiguration zu überprüfen, können Sie den folgenden Befehl ausführen.

    Get-NetAdapterRdma

Folgendes sind die Ergebnisse dieses Befehls.

|Name |InterfaceDescription |Aktiviert|
|----|--------------------|-------|
|
|M1| Mellanox ConnectX-3 Pro-Ethernet-Adapter |"True"|

### <a name="download-diskspdexe-and-a-powershell-script"></a>Herunterladen von DiskSpd.exe und ein PowerShell-Skript

Um den Vorgang fortzusetzen, müssen Sie zunächst die folgenden Elemente herunterladen.

- Laden Sie das Dienstprogramm DiskSpd.exe und extrahieren Sie das Dienstprogramm in C:\TEST\ [Diskspd-Dienstprogramm: ein stabiles Speicher testen Tool (ersetzende SQLIO)](https://gallery.technet.microsoft.com/DiskSpd-a-robust-storage-6cd2f223)

- Das PowerShell-Skript Test-RDMA auf C:\TEST\ herunterladen[https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1)

### <a name="determine-the-ifindex-value-of-your-target-adapter"></a>Bestimmen Sie den IfIndex-Wert, der den Ziel-Adapter

Den folgenden Befehl können Sie um den Wert IfIndex des Adapters Ziel zu ermitteln. Sie können diesen Wert in den nachfolgenden Schrittenbei der Ausführung des Skripts, die Sie heruntergeladen haben.

    Get-NetIPConfiguration -InterfaceAlias "M*" | ft InterfaceAlias,InterfaceIndex,IPv4Address

Folgendes sind die Ergebnisse dieses Befehls.

|InterfaceAlias |InterfaceIndex |IPv4Address|
|-------------- |-------------- |-----------|
|
|M2 |14 |{192.168.1.5}|

### <a name="run-the-powershell-script"></a>Führen Sie das PowerShell-Skript

Wenn Sie die Test-Rdma. ps1 Windows PowerShell-Skript ausführen, können Sie den Wert IfIndex an das Skript, zusammen mit der IP-Adresse des Remote-Adapters auf demselben VLAN übergeben.

Befehl im folgenden Beispiel können Sie das Skript mit einer IfIndex von 14 auf dem Netzwerkadapter 192.168.1.5 auszuführen.
    
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
    

>[!NOTE]
>Wenn die RDMA-Datenverkehr für den Fall RoCE insbesondere fehlschlägt, finden Sie in Ihrer Konfiguration ToR-Switch richtigen PCF/ETS-Einstellungen, die die Einstellungen übereinstimmen sollte. Siehe AbschnittQoS in diesem Dokument für das Verweisen auf Werte.

## <a name="remove-the-access-vlan-setting"></a>Entfernen Sie die Einstellung Zugriff VLAN

Vorbereitung für die Erstellung des Hyper-V-Switches müssen Sie die VLAN-Einstellungen entfernen, denen Sie zuvor installiert.  Sie können den folgenden Befehl verwenden, so entfernen Sie die VLAN-Einstellung Zugriff von der physischen NIC. Dadurch wird verhindert, dass die NIC Auto-Tagging den ausgehenden Datenverkehr mit der falschen VLAN-ID und auch verhindert, dass es Filterung /-Ausgang-Datenverkehr, der den Zugriff VLAN-ID übereinstimmt

    
    Set-NetAdapterAdvancedProperty -Name M1 -RegistryKeyword VlanID -RegistryValue "0"
    

Befehl im folgenden Beispiel können Sie die VLAN-ID-Einstellung zu bestätigen und zeigen Sie die Ergebnisse, die zeigen, dass der VLAN-ID-Wert 0 (null) ist.

    
    Get-NetAdapterAdvancedProperty -name m1 | Where-Object {$_.RegistryKeyword -eq 'VlanID'} 
    


## <a name="create-a-hyper-v-virtual-switch"></a>Erstellen eines virtuellen Hyper-V-Switch

In diesem Abschnittkönnen Sie um einen virtuellen Hyper-V-Switch \(vSwitch\) auf Ihren Hyper-V-Hosts erstellen.

Die folgende Abbildungzeigt die Hyper-V-Host 1 mit einem vSwitch.

![Erstellen eines virtuellen Hyper-V-Switch](../../media/Converged-NIC/5-single-create-vswitch.jpg)


### <a name="create-an-external-hyper-v-virtual-switch"></a>Erstellen eines externen virtuellen Hyper-V-Switches

In diesem Abschnittkönnen Sie einen externen vSwitch in Hyper-V von Hyper-V-Host a erstellen

Befehl im folgenden Beispiel können Sie einen Switch mit dem Namen VMSTEST erstellen.

>[!NOTE]
>Der Parameter **AllowManagementOS** in den folgenden Befehl erstellt eine Host-vNIC, die die MAC-Adresse und die IP-Adresse die physische NIC erbt.

    New-VMSwitch -Name VMSTEST -NetAdapterName "M1" -AllowManagementOS $true

Folgendes sind die Ergebnisse dieses Befehls.

|Name |Extern |NetAdapterInterfaceDescription|
|---- |---------- |------------------------------|
|VMSTEST |Externe |Mellanox ConnectX-3 Pro-Ethernet-Adapter|

Sie können den folgenden Befehl verwenden, zum Anzeigen der Eigenschaften des Netzwerkadapters.

    Get-NetAdapter | ft -AutoSize

Folgendes sind die Ergebnisse dieses Befehls.

|Name |InterfaceDescription | ifIndex |Status |MacAddress |LinkSpeed|
|---- |-------------------- |-------| ------|----------|---------|
|
|vEthernet \(VMSTEST\) |Virtuelle Hyper-V-Ethernet-Adapter 2|27 |Nach-oben |E4-1D-2D-07-40-71 |40-Gbit/s|


Sie können eine Host-vNIC auf zweierlei Weise verwalten. Eine Methode ist die **NetAdapter** anzeigen, die ausgeführt wird, basierend auf der "vEthernet \(VMSTEST\)" Namen.

Die andere Methode ist die **VMNetworkAdapter** Ansicht, die das Präfix "vEthernet" löscht und einfach den Namen Vmswitch verwendet.

Die **VMNetworkAdapter** zeigt einige Netzwerkadapter-Eigenschaften, die nicht mit angezeigt werden die **NetAdapter** Befehl.

Sie können den folgenden Befehl zum Anzeigen der Ergebnisse von der **VMNetworkAdapter** Methode.

    Get-VMNetworkAdapter –ManagementOS | ft -AutoSize

Folgendes sind die Ergebnisse dieses Befehls.

|Name |IsManagementOs |Name des virtuellen Computers |SwitchName |MacAddress |Status |IP-Adressen|
|----|-------------- |------ |----------|----------|------ |-----------|
|
|CORP-External-Switch |"True" |CORP-External-Switch| 001B785768AA |{Ok} |&nbsp;|
|VMSTEST |"True" |VMSTEST | E41D2D074071| {Ok} | &nbsp;| 

### <a name="test-the-connection"></a>Testen der Verbindung

Befehl im folgenden Beispiel können Sie die Verbindung zu testen und die Ergebnisse anzuzeigen.
    
    Test-NetConnection 192.168.1.5

    ComputerName   : 192.168.1.5
    RemoteAddress  : 192.168.1.5
    InterfaceAlias : vEthernet (CORP-External-Switch)
    SourceAddress  : 192.168.1.3
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
    
Sie können die folgenden Beispielbefehle zuweisen und Anzeigen von VLAN-netzwerkadaptereinstellungen verwenden.
    
    Set-VMNetworkAdapterVlan -VMNetworkAdapterName "VMSTEST" -VlanId "101" -Access -ManagementOS
    Get-VMNetworkAdapterVlan -ManagementOS -VMNetworkAdapterName "VMSTEST"
    

|Name des virtuellen Computers |VMNetworkAdapterName |Modus |VlanList|
|------ |-------------------- |---- |--------|
|
|&nbsp;|VMSTEST |Zugriff |101     
 
### <a name="test-the-connection"></a>Testen der Verbindung

Denken Sie daran, dass die Änderung ein paar Sekunden abgeschlossen werden, bevor Sie die anderen Adapter ping können dauern kann.

Befehl im folgenden Beispiel können Sie die Verbindung zu testen und die Ergebnisse anzuzeigen.
    
    Test-NetConnection 192.168.1.5
     
    ComputerName   : 192.168.1.5
    RemoteAddress  : 192.168.1.5
    InterfaceAlias : vEthernet (VMSTEST)
    SourceAddress  : 192.168.1.3
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
    

## <a name="test-hyper-v-virtual-switch-rdma-mode-2"></a>Testen von Hyper-V Virtual Switch RDMA (2-Modus)

Die folgende Abbildungzeigt den aktuellen Status des Hyper-V-Hosts, einschließlich der vSwitch auf dem Hyper-V-Host 1.

![Testen Sie den virtuellen Hyper-V-Switch](../../media/Converged-NIC/6-single-test-vswitch-rdma.jpg)


### <a name="set-priority-tagging-on-the-host-vnic"></a>Festlegen der Priorität, die auf dem Host-vNIC-Kennzeichnung

Sie können die folgenden Beispielbefehle verwenden, zum Festlegen der Priorität, die auf dem Host-vNIC-Kennzeichnung und Anzeigen der Ergebnisse Ihrer Aktionen.
    
    Set-VMNetworkAdapter -ManagementOS -Name "VMSTEST" -IeeePriorityTag on
    Get-VMNetworkAdapter -ManagementOS -Name "VMSTEST" | fl Name,IeeePriorityTag
    
    Name: VMSTEST
    IeeePriorityTag : On
    
Befehl im folgenden Beispiel können Sie den Netzwerkadapter RDMA-Informationen anzeigen. In den Ergebnissen Wenn der Parameter **aktiviert** weist den Wert **False**, bedeutet dies, dass RDMA nicht aktiviert ist.
    
    Get-NetAdapterRdma
    
|Name |InterfaceDescription |Aktiviert |
|---- |-------------------- |-------|
|
|vEthernet \(VMSTEST\)| Virtuelle Hyper-V-Ethernet-Adapter 2|"False"|

### <a name="enable-rdma-on-the-host-vnic"></a>Aktivieren Sie RDMA auf dem Host-vNIC

Sie können die folgenden Beispielbefehle verwenden, zum Anzeigen der Eigenschaften des Netzwerkadapters, aktivieren Sie RDMA für den Adapter, und zeigen Sie den Netzwerkadapter RDMA-Informationen.
    
    Get-NetAdapter
    
|Name |InterfaceDescription |ifIndex |Status |MacAddress |LinkSpeed|
|----|--------------------|-------|------|----------|---------|
|
|vEthernet (VMSTEST)|Virtuelle Hyper-V-Ethernet-Adapter 2|27|Nach-oben|E4-1D-2D-07-40-71|40-Gbit/s|

    Enable-NetAdapterRdma -Name "vEthernet (VMSTEST)"
    Get-NetAdapterRdma -Name "vEthernet (VMSTEST)"

In den folgenden Ergebnissen Wenn der Parameter **aktiviert** weist den Wert **"true"**, bedeutet dies, dass RDMA aktiviert ist.

|Name |InterfaceDescription |Aktiviert |
|---- |-------------------- |-------|
|
|vEthernet \(VMSTEST\)| Virtuelle Hyper-V-Ethernet-Adapter 2|"True"|


    
    Get-NetAdapter 
    

|Name |InterfaceDescription |ifIndex |Status |MacAddress |LinkSpeed|
|----|--------------------|-------|------|----------|---------|
|
|vEthernet (VMSTEST)|Virtuelle Hyper-V-Ethernet-Adapter 2|27|Nach-oben|E4-1D-2D-07-40-71|40-Gbit/s|

### <a name="perform-rdma-traffic-test-by-using-the-script"></a>Führen Sie RDMA Verkehr Test mithilfe des Skripts

Sie können den folgenden Befehl verwenden, führen Sie das Skript aus, die, das Sie heruntergeladen haben, und zeigen Sie die Ergebnisse.
    
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
    
Die letzte Zeile in dieser Ausgabe "RDMA-Verkehr Test erfolgreich: RDMA-Datenverkehr an 192.168.1.5, gesendet wurde" gibt an, dass Sie erfolgreich zusammengeführten NIC auf dem Adapter konfiguriert haben.

## <a name="all-topics-in-this-guide"></a>Alle Themen in diesem Handbuch

Dieses Handbuch enthält die folgenden Themen.

- [Zusammengeführtes NIC-Konfiguration mit einem einzelnen Netzwerkadapter](cnic-single.md)
- [Zusammengeführtes NIC kombinierten NIC-Konfiguration](cnic-datacenter.md)
- [Physischen Switch-Konfiguration für die zusammengeführten NIC](cnic-app-switch-config.md)
- [Problembehandlung bei zusammengeführten NIC-Konfigurationen](cnic-app-troubleshoot.md)
