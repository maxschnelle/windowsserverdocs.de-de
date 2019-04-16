---
title: Zusammengeführtes NIC kombinierten NIC-Konfiguration
description: Dieses Thema enthält Anweisungen zum Konfigurieren der zusammengeführten NIC in einer Datacenter-Konfiguration in Windows Server2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: f01546f8-c495-4055-8492-8806eee99862
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1ac6c2915301b1cf64486f24c197ebbf22bb5e2e
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="converged-nic-teamed-nic-configuration"></a>Zusammengeführtes NIC kombinierten NIC-Konfiguration

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Die folgenden Abschnitte enthalten Anweisungen für die Bereitstellung von zusammengeführten NIC in einer zusammengeschlossen NIC-Konfiguration mit Switch Embedded Teaming \(SET\). Die Beispielkonfiguration in dieser Anleitung zeigt zwei Hyper-V-Hosts, Hyper-V-Host 1 und 2 für Hyper-V-Host.

## <a name="test-connectivity-between-source-and-destination"></a>Testen der Konnektivität zwischen Quell- und Zielserver

Dieser Abschnittenthält die erforderlichen Schrittezum Testen der Konnektivität zwischen Quell- und Ziel-Hyper-V-Hosts.

Die folgende Abbildungzeigt zwei Hyper-V-Hosts **Hyper-V-Host 1** und **Hyper-V-Host 2**. 

Beide Hyper-V-Hosts über zwei Netzwerkadapter verfügen. Klicken Sie auf jedem Host ein Adapter mit dem Subnetz 192.168.1.x/24 verbunden ist, und ein Adapter mit dem 192.168.2.x/24 Subnetz verbunden ist.

![Hyper-V-Hosts](../../media/Converged-NIC/1-datacenter-test-conn.jpg)

### <a name="test-nic-connectivity-to-the-hyper-v-virtual-switch"></a>Testen der Konnektivität der NIC mit dem virtuellen Hyper-V-Switch

Verwenden Sie diesen Schritt, können Sie sicherstellen, dass die physische NIC, für die Sie später einen virtuellen Hyper-V-Switch erstellen, auf dem Zielhost zugreifen kann. 

Dieser Test zeigt Konnektivität mit \(L3\) Layer 3 - oder der IP-Ebene - als auch die Layer-2-\(L2\) virtuelle lokale Netzwerke \(VLAN\).

Die folgenden Windows PowerShell-Befehl können Sie die Eigenschaften des Netzwerkadapters abrufen.

    Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize
     
Folgendes sind die Ergebnisse dieses Befehls.

|Name|InterfaceDescription|ifIndex|Status|MacAddress|LinkSpeed|
|-----|--------------------|-------|-----|----------|---------|
|
|Test-40G-1|Mellanox ConnectX-3 Pro-Ethernet-Adapter|11|Nach-oben|E4-1D-2D-07-43-D0|40-Gbit/s|

Sie können einen der folgenden Befehle um zusätzliche Eigenschaften, z.B. die IP-Adresse zu erhalten.

    Get-NetIPAddress -InterfaceAlias "Test-40G-1"

    Get-NetIPAddress -InterfaceAlias "TEST-40G-1" | Where-Object {$_.AddressFamily -eq "IPv4"} | fl InterfaceAlias,IPAddress
    
Folgendes Beispielergebnisse dieser Befehle sind.

|Parameter|Wert|
|---------|-----|
|
|IP-Adresse| 192.168.1.3|
|InterfaceIndex|11|
|InterfaceAlias|Test-40G-1|
|AddressFamily|IPv4|
|Typ| Unicast|
|PrefixLength|24|

### <a name="verify-that-nic-team-member-has-a-valid-ip-address"></a>Überprüfen Sie die Member der NIC-Team eine gültige IP-Adresse.

Können diesen Schrittzu überprüfen, ob andere NIC-Teams oder Switch Embedded Team \(SET\) Member physischen NICs \(pNICs\) verfügen auch über eine gültige IP-Adresse.

Dieser Schrittverwenden Sie in einem separaten Subnetz, \ (xxx.xxx.** 2**.xxx Vs xxx.xxx. **1**. Xxx\), um zu ermöglichen, von diesem Adapter an das Ziel gesendet. 

Andernfalls, wenn Sie beide pNICs im gleichen Subnetz finden, der Windows TCP/IP-Stapel Lastenausgleich zwischen den Schnittstellen und einfache Überprüfung jedoch komplizierter.

Die folgenden Windows PowerShell-Befehl können Sie die Eigenschaften des zweiten Netzwerkadapters abrufen.

    Get-NetAdapter -Name "Test-40G-2" | ft -AutoSize

Folgendes sind die Ergebnisse dieses Befehls.

|Name |InterfaceDescription |ifIndex |Status |MacAddress |LinkSpeed|
|----|--------------------|-------|------|----------|---------|
|
|TEST-40G-2 |Mellanox ConnectX-3 Pro Ethernet A... \ 2 |13 |Nach-oben |E4-1D-2D-07-40-70 |40-Gbit/s|

Sie können einen der folgenden Befehle um zusätzliche Eigenschaften, z.B. die IP-Adresse zu erhalten.

    Get-NetIPAddress -InterfaceAlias "Test-40G-2"

    Get-NetIPAddress -InterfaceAlias "Test-40G-2" | Where-Object {$\_.AddressFamily -eq "IPv4"} | fl InterfaceAlias,IPAddress

Folgendes Beispielergebnisse dieser Befehle sind.

|Parameter|Wert|
|---------|-----|
|
|IP-Adresse|192.168.2.3|
|InterfaceIndex|13|
|InterfaceAlias|TEST-40G-2|
|AddressFamily|IPv4|
|Typ|Unicast|
|PrefixLength|24|

### <a name="verify-that-additional-nics-have-valid-ip-addresses"></a>Überprüfen Sie, ob zusätzliche NICs gültige IP-Adressen

Dadurch können Sie sicherstellen, dass die andere NIC eine gültige IP-Adresse verfügt.

Dieser Schrittverwenden Sie in einem separaten Subnetz, \ (xxx.xxx.** 2**.xxx Vs xxx.xxx. **1**. Xxx\), um zu ermöglichen, von diesem Adapter an das Ziel gesendet. 

Andernfalls, wenn Sie beide pNICs im gleichen Subnetz finden, der Windows TCP/IP-Stapel Lastenausgleich zwischen den Schnittstellen und einfache Überprüfung jedoch komplizierter.

Die folgenden Windows PowerShell-Befehl können Sie die Eigenschaften des zweiten Netzwerkadapters abrufen.

    Get-NetAdapter -Name "Test-40G-2" | ft -AutoSize

Folgendes sind die Ergebnisse dieses Befehls.

|Name |InterfaceDescription |ifIndex |Status |MacAddress |LinkSpeed|
|----|--------------------|-------|------|----------|---------|
|
|TEST-40G-2 |Mellanox ConnectX-3 Pro Ethernet A... \ 2 |13 |Nach-oben |E4-1D-2D-07-40-70 |40-Gbit/s|

Sie können einen der folgenden Befehle um zusätzliche Eigenschaften, z.B. die IP-Adresse zu erhalten.
    
    Get-NetIPAddress -InterfaceAlias "Test-40G-2"

    Get-NetIPAddress -InterfaceAlias "Test-40G-2" | Where-Object {$_.AddressFamily -eq "IPv4"} | fl InterfaceAlias,IPAddress

Folgendes Beispielergebnisse dieser Befehle sind.

|Parameter|Wert|
|---------|-----|
|
|IP-Adresse|192.168.2.3|
|InterfaceIndex|13|
|InterfaceAlias|TEST-40G-2|
|AddressFamily|IPv4|
|Typ|Unicast|
|PrefixLength|24|

### <a name="ensure-that-source-and-destination-can-communicate"></a>Stellen Sie sicher, dass Quell- und Zielserver kommunizieren können

Sie können diesen Schrittbidirektionale Kommunikation überprüfen \ (Ping von der Quelle zum Ziel und umgekehrt auf beide Systems\).  Im folgenden Beispiel der **Test NetConnection** Windows PowerShell-Befehl verwendet wird, aber bevorzugt, wenn Sie können die **Ping** Befehl. 

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

### <a name="verify-connectivity-for-additional-nics"></a>Überprüfen Sie die Konnektivität für zusätzliche Netzwerkkarten

Mit diesem Schrittkönnen Sie die vorherigen Schrittefür alle nachfolgenden pNICs wiederholen, die im Team NIC oder einer Gruppe enthalten sind.

Den folgenden Befehl können Sie um die Verbindung testen.
    
    Test-NetConnection 192.168.2.5

Folgendes sind die Ergebnisse dieses Befehls.

|Parameter|Wert|
|---------|-----|
|
|ComputerName|192.168.2.5|
|RemoteAddress|192.168.2.5|
|InterfaceAlias|Test-40G-2|
|SourceAddress|192.168.2.3|
|PingSucceeded|"False"|
|PingReplyDetails \(RTT\)|0 ms|


## <a name="configure-vlans"></a>Konfigurieren von VLANs

Für diesen Schrittwerden die NICs in **Zugriff** Modus. Bei der Erstellung einer virtuellen Hyper-V-Switch \(vSwitch\) weiter unten in diesem Handbuch werden jedoch die VLAN-Eigenschaften auf der Ebene der vSwitch-Port angewendet. 

Da ein Switch mehrere VLANs hosten kann, ist es erforderlich, für den Top of Rack \(ToR\) physischen Switch der Port im trunkmodus konfiguriert haben.

Anweisungen zum Konfigurieren der trunkmodus auf dem Switch finden Sie in der Dokumentation Ihres ToR-Switch.

Die folgende Abbildungzeigt zwei Hyper-V-Hosts mit zwei Netzwerkadaptern jedes, die VLAN-101 und 102 VLAN in den Eigenschaften des Netzwerkadapters konfiguriert.

![Konfigurieren Sie virtuelle lokale Netzwerke](../../media/Converged-NIC/2-datacenter-configure-vlans.jpg)

### <a name="configure-the-vlan-ids-for-both-nics"></a>Konfigurieren Sie die VLAN-IDs für beide NICs

Sie können diesen Schrittverwenden, so konfigurieren Sie die VLAN-IDs für Netzwerkkarten in Hyper-V-Hosts installiert.

Gemäß den Institute of Electrical und Electronics Engineers \(IEEE\) Netzwerk Standards, Quality of Service \(QoS\) Eigenschaften in der physischen NIC wirken sich auf den 802. 1p-Header, die in der 802. 1Q eingebettet ist \(VLAN\) Header beim Konfigurieren der VLAN-ID.

#### <a name="configure-nic-test-40g-1"></a>Konfigurieren der NIC Test-40G-1

Konfigurieren Sie mit den folgenden Befehlen die VLAN-ID für die erste Netzwerkkarte, Test-40G-1, klicken Sie dann die resultierende Konfiguration anzuzeigen.

    
    Set-NetAdapterAdvancedProperty -Name "Test-40G-1" -RegistryKeyword VlanID -RegistryValue "101"
    Get-NetAdapterAdvancedProperty -Name "Test-40G-1" | Where-Object {$_.RegistryKeyword -eq "VlanID"} | ft -AutoSize
    
Folgendes sind die Ergebnisse dieses Befehls.

|Name |"DisplayName"| DisplayValue| RegistryKeyword |RegistryValue|
|----|-----------|------------|---------------|-------------|
|
|TEST-40G-1|VLAN-ID|101|VLAN-ID|{101}|


Stellen Sie sicher, dass die VLAN-ID wirksam, die unabhängig von der Implementierung der Netzwerk-Adapter wird mithilfe des folgenden Befehls, um den Netzwerkadapter neu zu starten.

    Restart-NetAdapter -Name "Test-40G-1"

Sie können den folgenden Befehl verwenden, um sicherzustellen, dass der Status des Netzwerkadapters **von** bevor Sie fortfahren.

    Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize

Folgendes sind die Ergebnisse dieses Befehls.

|Name|InterfaceDescription|ifIndex| Status|MacAddress|LinkSpeed|
|----|--------------------|-------|------|----------| ---------|
|
|Test-40G-1|Mellanox ConnectX-3 Pro Ethernet Ada...|11|Nach-oben|E4-1D-2D-07-43-D0|40-Gbit/s|

#### <a name="configure-nic-test-40g-2"></a>Konfigurieren der NIC Test-40G-2

Konfigurieren Sie mit den folgenden Befehlen die VLAN-ID für die zweite Netzwerkkarte, Test-40G-2, zeigen Sie dann die resultierende Konfiguration.

    
    Set-NetAdapterAdvancedProperty -Name "Test-40G-2" -RegistryKeyword VlanID -RegistryValue "102"
    Get-NetAdapterAdvancedProperty -Name "Test-40G-2" | Where-Object {$_.RegistryKeyword -eq "VlanID"} | ft -AutoSize
    

Folgendes sind die Ergebnisse dieses Befehls.

|Name |"DisplayName"| DisplayValue| RegistryKeyword |RegistryValue|
|----|-----------|------------|---------------|-------------|
|
|TEST-40G-2|VLAN-ID|102|VLAN-ID|{102}|

Stellen Sie sicher, dass die VLAN-ID wirksam, die unabhängig von der Implementierung der Netzwerk-Adapter wird mithilfe des folgenden Befehls, um den Netzwerkadapter neu zu starten.

`Restart-NetAdapter -Name "Test-40G-2"  `              

Sie können den folgenden Befehl verwenden, um sicherzustellen, dass der Status des Netzwerkadapters **von** bevor Sie fortfahren.

    Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize

Folgendes sind die Ergebnisse dieses Befehls.

|Name|InterfaceDescription|ifIndex| Status|MacAddress|LinkSpeed|
|----|--------------------|-------|------|----------| ---------|
|
|Test-40G-2 |Mellanox ConnectX-3 Pro Ethernet Ada... |11 |Nach-oben |E4-1D-2D-07-43-D1 |40-Gbit/s|


### <a name="verify-connectivity"></a>Überprüfen Sie die Konnektivität

In diesem Abschnittkönnen eine um Verbindung zu überprüfen, nachdem die Netzwerkadapter neu gestartet werden. Sie können die Konnektivität überprüfen, nach dem Anwenden des VLAN-Tags auf beiden Adaptern. Wenn die Verbindung ein Fehler auftritt, können Sie den Switch VLAN-Konfiguration oder das Ziel Teilnahme an demselben VLAN überprüfen. 

>[!IMPORTANT]
>Nachdem Sie die Schritteim vorherigen Abschnittausführen, kann es einige Sekunden für das Gerät neu starten und werden im Netzwerk verfügbar dauern.

#### <a name="verify-connectivity-for-nic-test-40g-1"></a>Überprüfen Sie die Konnektivität für NIC Test-40G-1

Um die Konnektivität für die erste Netzwerkkarte zu überprüfen, können Sie den folgenden Befehl ausführen.

    Test-NetConnection 192.168.1.5
    
Folgendes sind die Ergebnisse dieses Befehls.

|Parameter|Wert|
|---------|-----|
|
|ComputerName|192.168.1.5|
|RemoteAddress|192.168.1.5|
|InterfaceAlias|Test-40G-1|
|SourceAddress|192.168.1.5|
|PingSucceeded|"True"|
|PingReplyDetails \(RTT\)|0 ms|

#### <a name="verify-connectivity-for-nic-test-40g-2"></a>Überprüfen Sie die Konnektivität für Test-40G-2 NIC

In diesem Abschnittkönnen zum Testen der Konnektivität für Test-40 G-2 NIC.

Verwenden Sie den folgenden Befehl zum Testen der Konnektivität für die zweite Netzwerkkarte.
    
    Test-NetConnection 192.168.2.5
    
Folgendes sind die Ergebnisse dieses Befehls.

|Parameter|Wert|
|---------|-----|
|
|ComputerName|192.168.2.5|
|RemoteAddress|192.168.2.5|
|InterfaceAlias|Test-40G-2|
|SourceAddress|192.168.2.3|
|PingSucceeded|"True"|
|PingReplyDetails \(RTT\)|0 ms|

Ein **Test NetConnection** Fehler oder Pingfehler, der auftritt, sofort nach dem durchführen **Neustart-NetAdapter** ist nicht ungewöhnlich, warten Sie daher für die Netzwerkkarte vollständig initialisiert werden kann, und versuchen Sie es dann erneut.

Wenn die VLAN-101-Verbindungen funktionieren, aber die VLAN-102-Verbindungen funktionieren nicht, kann das Problem, dass der Switch werden, um die gewünschte VLAN Port Datenverkehr ermöglichen konfiguriert muss. Sie können dies überprüfen, indem vorübergehend die fehlerhaften Adapter auf VLAN 101 und wiederholen den Test der Netzwerkverbindung.

## <a name="configure-quality-of-service-qos"></a>Konfigurieren von Quality of Service \(QoS\)

Der nächste Schrittbesteht \(QoS\) Quality of Service, erfordert die Installation von Windows Server2016-Feature Data Center Bridging \(DCB\) konfigurieren.

Die folgende Abbildungzeigt die Hyper-V-Hosts nach dem erfolgreichen VLANs im vorherigen Schrittkonfigurieren.

![Konfigurieren von Quality of Service](../../media/Converged-NIC/3-datacenter-configure-qos.jpg)

### <a name="install-data-center-bridging-dcb"></a>Installieren Sie Data Center Bridging \(DCB\)

Sie können diesen Schrittzum Installieren und aktivieren DCB verwenden. In den meisten Fällen dieser Schrittist optional für iWarp Implementierungen, aber es ist erforderlich, die Fabric-Verwaltungsaufgaben, wie z.B. Cross-Rack-Szenarien.

Sie können den folgenden Befehl verwenden, DCB auf allen Hyper-V-Hosts zu installieren. 

    Install-WindowsFeature Data-Center-Bridging

Folgendes sind die Ergebnisse dieses Befehls.

|Erfolg |Neustart erforderlich |Beendigungscode|Feature-Ergebnis|
|------- |-------------- |--------- |-------------- |
|
|"True" |Nein |Erfolg| {Data Center Bridging}|

### <a name="set-the-qos-policies-for-smb-direct"></a>Legen Sie die QoS-Richtlinien für SMB Direct 

Sie können den folgenden Befehl verwenden, Konfigurieren von QoS-Richtlinien für SMB Direct.

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

### <a name="set-policies-for-other-traffic-on-the-interface"></a>Festlegen von Richtlinien für den übrigen Datenverkehr für die Benutzeroberfläche 

Den folgenden Befehl können Sie zusätzliche QoS-Richtlinien festzulegen.

    New-NetQosPolicy "DEFAULT" -Default -PriorityValue8021Action 0
 
Folgendes sind die Ergebnisse dieses Befehls.

|Parameter|Wert|
|---------|-----|
|
|Name | STANDARDWERT|
|Besitzer|Group Policy \(Machine\)|
|NetworkProfile|Alle|
|Rangfolge|127|
|Vorlage| Standardwert|
|JobObject| &nbsp;|
|PriorityValue|0|

### <a name="turn-on-flow-control-for-smb"></a>Die flusssteuerung für SMB aktivieren 

Sie können die folgenden Befehle so aktivieren Sie die flusssteuerung für SMB und zum Anzeigen der Ergebnisse verwenden.

    Enable-NetQosFlowControl -priority 3
    Get-NetQosFlowControl

Folgendes sind die Ergebnisse dieses Befehls.

|Priorität|Aktiviert|PolicySet|IfIndex|IfAlias|
|---------|-----|--------- |-------| -------|
|
|0 |"False" |Globale|&nbsp;|&nbsp;|
|1 |"False" |Globale|&nbsp;|&nbsp;|
|2 |"False" |Globale|&nbsp;|&nbsp;|
|3 |"True" |Globale|&nbsp;|&nbsp;|
|4 |"False" |Globale|&nbsp;|&nbsp;|
|5 |"False" |Globale|&nbsp;|&nbsp;|
|6 |"False" |Globale|&nbsp;|&nbsp;|
|7 |"False" |Globale|&nbsp;|&nbsp;|

Wenn die Ergebnisse nicht diese Ergebnisse übereinstimmen, da Elemente als 3 aktiviert Wert True haben, müssen Sie im nächsten Schrittausführen. Wenn Ihre Ergebnisse diese Beispielergebnisse entsprechen, und nur die Position 3 aktiviert Wert "Wahr" zurückgegeben hat, müssen Sie nicht führen Sie den nächsten Schritt, und können nach unten zu überspringen **aktivieren QoS für das Ziel und Ziel-Netzwerkadapter**.

### <a name="ensure-flow-control-is-disabled-for-other-traffic-classes-optional"></a>Stellen Sie sicher, dass die flusssteuerung für andere Klassen \(Optional\) deaktiviert ist

Sie brauchen diesen Schrittdurchführen, wenn **FlowControl** für Datenverkehrsklassen 0,1,2,4,5,6 und 7 nicht aktiviert ist.

Wenn **FlowControl** ist bereits aktiviert, für sämtlicher Datenverkehr, der andere als 3 Klassen \ (0,1,2,4,5,6 und 7\), müssen Sie deaktivieren **FlowControl** für diese Klassen. 

>[!NOTE]
>Unter komplexere Konfigurationen die andere Datenverkehrsklassen flusssteuerung, müssen möglicherweise jedoch außerhalb der Umfang dieser Anleitung diese Szenarien sind.

Sie können die folgenden Befehle auf SMB-flusssteuerung für Datenverkehrsklassen 0,1,2,4,5,6 und 7 zu deaktivieren, und klicken Sie zum Anzeigen der Ergebnisse verwenden.

    Disable-NetQosFlowControl -priority 0,1,2,4,5,6,7
    Get-NetQosFlowControl

Folgendes sind die Ergebnisse dieses Befehls.

|Priorität|Aktiviert|PolicySet|IfIndex|IfAlias|
|---------|-----|--------- |-------| -------|
|
|0 |"False" |Globale|&nbsp;|&nbsp;|
|1 |"False" |Globale|&nbsp;|&nbsp;|
|2 |"False" |Globale|&nbsp;|&nbsp;|
|3 |"True" |Globale|&nbsp;|&nbsp;|
|4 |"False" |Globale|&nbsp;|&nbsp;|
|5 |"False" |Globale|&nbsp;|&nbsp;|
|6 |"False" |Globale|&nbsp;|&nbsp;|
|7 |"False" |Globale|&nbsp;|&nbsp;|

### <a name="enable-qos-for-the-local-and-destination-network-adapters"></a>Aktivieren von QoS für die lokale und Ziel-Netzwerkadapter 

Mit diesem Schrittkönnen Sie QoS für die lokale und die Ziel-Netzwerkadapter aktivieren. Stellen Sie sicher, dass die Ausführung dieser Befehle auf beiden Hyper-V-Hosts.

#### <a name="enable-qos-for-nic-test-40g-1"></a>Aktivieren von QoS für NIC Test-40G-1

Sie können die folgenden Befehle zum Aktivieren von QoS und Anzeigen der Ergebnisse der Konfiguration.

    Enable-NetAdapterQos -InterfaceAlias "Test-40G-1"
    Get-NetAdapterQos -Name "Test-40G-1"

Folgendes sind die Ergebnisse dieses Befehls.

**Namen**: TEST-40G-1 **aktiviert**: True **Funktionen**:   

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
|0| Strict|&nbsp;|0-7|

**OperationalFlowControl**: Priorität 3 aktiviert **OperationalClassifications**:

|Protokoll|Porttyp /|Priorität|
|--------|---------|--------|
|
|Standardwert|&nbsp;|0|
|NetDirect| 445|3|

#### <a name="enable-qos-for-nic-test-40g-2"></a>Aktivieren von QoS für NIC Test-40G-2

Sie können die folgenden Befehle zum Aktivieren von QoS und Anzeigen der Ergebnisse der Konfiguration.

    Enable-NetAdapterQos -InterfaceAlias "Test-40G-2"
    Get-NetAdapterQos -Name "Test-40G-2"

 
Folgendes sind die Ergebnisse dieses Befehls.

**Namen**: TEST-40G-2 **aktiviert**: True **Funktionen**:   

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
|0| Strict|&nbsp;|0-7|

**OperationalFlowControl**: Priorität 3 aktiviert **OperationalClassifications**:

|Protokoll|Porttyp /|Priorität|
|--------|---------|--------|
|
|Standardwert|&nbsp;|0|
|NetDirect| 445|3|


### <a name="allocate-50-of-the-bandwidth-reservation-to-smb-direct-rdma"></a>Ordnen Sie 50% der Bandbreitenreservierung SMB Direct \(RDMA\)

Die folgenden Befehle können Sie die Hälfte der bandbreitenreservierung SMB Direct zuweisen möchten.

    New-NetQosTrafficClass "SMB" -priority 3 -bandwidthpercentage 50 -algorithm ETS

Folgendes sind die Ergebnisse dieses Befehls.

|Name|Algorithmus |Bandwidth(%)| Priorität |PolicySet |IfIndex |IfAlias |
|----|---------| ------------ |--------| ---------|------- |------- |
|
|SMB | ETS     | 50 |3 |Globale |&nbsp;|&nbsp;|                                      
 
Den folgenden Befehl können Sie Bandbreite Reservierungsinformationen anzuzeigen.

    Get-NetQosTrafficClass | ft -AutoSize

Folgendes sind die Ergebnisse dieses Befehls.
 
|Name|Algorithmus |Bandwidth(%)| Priorität |PolicySet |IfIndex |IfAlias |
|----|---------| ------------ |--------| ---------|------- |------- |
|
|[Standard]| ETS|50 |0-2,4-7|  Globale|&nbsp;|&nbsp;| 
SMB |ETS|50 |3 |Globale|&nbsp;|&nbsp;| 

### <a name="create-traffic-classes-for-tenant-ip-traffic-optional"></a>Erstellen von Klassen für Mandanten IP-Datenverkehr \(optional\)

Dadurch können Sie um zwei zusätzliche Klassen für Mandanten IP-Datenverkehr erstellen. 

Wenn Sie die folgenden Beispielbefehle ausführen, können Sie die Werte für "IP1" und "IP2" auslassen, falls gewünscht.

    New-NetQosTrafficClass "IP1" -Priority 1 -bandwidthpercentage 10 -algorithm ETS

Folgendes sind die Ergebnisse dieses Befehls.

|Name|Algorithmus |Bandwidth(%)| Priorität |PolicySet |IfIndex |IfAlias |
|----|---------| ------------ |--------| ---------|------- |------- |
|
|IP1 |ETS |10 |1 |Globale|&nbsp;|&nbsp;|


    New-NetQosTrafficClass "IP2" -Priority 2 -bandwidthpercentage 10 -algorithm ETS

Folgendes sind die Ergebnisse dieses Befehls.

|Name|Algorithmus |Bandwidth(%)| Priorität |PolicySet |IfIndex |IfAlias |
|----|---------| ------------ |--------| ---------|------- |------- |
|
|IP2 |ETS |10 |2 |Globale|&nbsp;|&nbsp;|

Den folgenden Befehl können Sie QoS-Datenverkehrsklassen anzeigen.

    Get-NetQosTrafficClass | ft -AutoSize

Folgendes sind die Ergebnisse dieses Befehls.

|Name|Algorithmus |Bandwidth(%)| Priorität |PolicySet |IfIndex |IfAlias |
|----|---------| ------------ |--------| ---------|------- |------- |
|
|[Standard] |ETS |30 |0,4-7 |Globale|&nbsp;|&nbsp;|
|SMB |ETS |50 |3 |Globale|&nbsp;|&nbsp;|
|IP1 |ETS |10 |1 |Globale|&nbsp;|&nbsp;|
|IP2 |ETS |10 |2 |Globale|&nbsp;|&nbsp;|

## <a name="configure-debugger-optional"></a>Konfigurieren der Debugger \(Optional\)

Dadurch können Sie um den Debugger konfigurieren.

In der Standardeinstellung blockiert der angefügte Debugger NetQos. Sie können die folgenden Befehle Debugger außer Kraft zu setzen und die Ergebnisse anzuzeigen.

    Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 –Force
    
    Get-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" | ft AllowFlowControlUnderDebugger

Folgendes sind die Ergebnisse dieses Befehls.

    AllowFlowControlUnderDebugger
    -----------------------------
    1

## <a name="test-rdma-mode-1"></a>RDMA \(Mode 1\) testen

Dadurch können Sie sicherstellen, dass das Fabric ordnungsgemäß konfiguriert ist, vor dem Erstellen eines vSwitches und RDMA \(Mode 2\) wechselt.

Die folgende Abbildungzeigt den aktuellen Status des Hyper-V-Hosts.

![RDMA-Test](../../media/Converged-NIC/4-datacenter-test-rdma.jpg)

Um die RDMA-Konfiguration zu überprüfen, können Sie den folgenden Befehl ausführen.

    Get-NetAdapterRdma | ft -AutoSize

Folgendes sind die Ergebnisse dieses Befehls.

|Name |InterfaceDescription |Aktiviert|
|----|--------------------|-------|
|
|TEST-40G-1| VPI Mellanox ConnectX-4-Adapter 2 |"True"|
|TEST-40G-2| VPI Mellanox ConnectX-4-Adapter |"True"|


### <a name="determine-the-ifindex-value-of-your-target-adapter"></a>Bestimmen Sie den IfIndex-Wert, der den Ziel-Adapter

Den folgenden Befehl können Sie um den Wert IfIndex des Adapters Ziel zu ermitteln.

    Get-NetIPConfiguration -InterfaceAlias "TEST*" | ft InterfaceAlias,InterfaceIndex,IPv4Address

Folgendes sind die Ergebnisse dieses Befehls.

|InterfaceAlias |InterfaceIndex |IPv4Address|
|-------------- |-------------- |-----------|
|TEST-40G-1 |14 |{192.168.1.3}|
|TEST-40G-2 | 13 |{192.168.2.3}|

### <a name="download-diskspdexe-and-a-powershell-script"></a>Herunterladen von DiskSpd.exe und ein PowerShell-Skript

Um den Vorgang fortzusetzen, müssen Sie zunächst die folgenden Elemente herunterladen.

- Laden Sie das Dienstprogramm DiskSpd.exe und extrahieren Sie das Dienstprogramm in C:\TEST\[http://tinyurl.com/z68h3rc](http://tinyurl.com/z68h3rc)

- Das PowerShell-Skript Test-RDMA auf C:\TEST\ herunterladen[https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1)

### <a name="run-the-powershell-script"></a>Führen Sie das PowerShell-Skript

Wenn Sie die Test-Rdma. ps1 Windows PowerShell-Skript ausführen, können Sie den Wert IfIndex an das Skript, zusammen mit der IP-Adresse des Remote-Adapters auf demselben VLAN übergeben.

Befehl im folgenden Beispiel können Sie das Skript mit einer IfIndex von 14 auf dem Netzwerkadapter 192.168.1.5 auszuführen.
    
    C:\TEST\Test-RDMA.PS1 -IfIndex 14 -IsRoCE $true -RemoteIpAddress 192.168.1.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
    
    VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\\diskspd.exe
    VERBOSE: The adapter TEST-40G-1 is a physical adapter
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

### <a name="determine-the-ifindex-value-of-your-target-adapter"></a>Bestimmen Sie den IfIndex-Wert, der den Ziel-Adapter

Den folgenden Befehl können Sie um den Wert IfIndex des Adapters Ziel zu ermitteln.

    Get-NetIPConfiguration -InterfaceAlias "TEST*" | ft InterfaceAlias,InterfaceIndex,IPv4Address

Folgendes sind die Ergebnisse dieses Befehls.

|InterfaceAlias |InterfaceIndex |IPv4Address|
|-------------- |-------------- |-----------|
|TEST-40G-1 |14 |{192.168.1.3}|
|TEST-40G-2 | 13 |{192.168.2.3}|

Befehl im folgenden Beispiel können Sie das Skript mit einer IfIndex 13Jahren auf dem Netzwerkadapter 192.168.2.5 auszuführen.

    
    C:\TEST\Test-RDMA.PS1 -IfIndex 13 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
    VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\\diskspd.exe
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
    

## <a name="create-a-hyper-v-virtual-switch"></a>Erstellen eines virtuellen Hyper-V-Switch

In diesem Abschnittkönnen Sie um einen virtuellen Hyper-V-Switch \(vSwitch\) auf Ihren Hyper-V-Hosts erstellen.

Die folgende Abbildungzeigt die Hyper-V-Host 1 mit einem vSwitch.

![Erstellen eines virtuellen Hyper-V-Switch](../../media/Converged-NIC/5-datacenter-create-vswitch.jpg)

### <a name="create-a-vswitch-in-switch-embedded-teaming-set-mode"></a>Erstellen Sie einen vSwitch im \(SET\) Switch Embedded Teaming-Modus

Sie können Befehl im folgenden Beispiel erstellen Sie eine unabhängige Team Switch Satz mit dem Namen **VMSTEST** auf Hyper-V-Host 1. Sowohl der Netzwerkadapter auf diesem Computer, TEST-40G-1 "und" TEST-40G-2, werden an das SET-Team mit dem folgenden Befehl hinzugefügt.
    
    New-VMSwitch –Name "VMSTEST" –NetAdapterName "TEST-40G-1","TEST-40G-2" -EnableEmbeddedTeaming $true -AllowManagementOS $true
    
Folgendes sind die Ergebnisse dieses Befehls.

|Name |Extern |NetAdapterInterfaceDescription|
|---- |---------- |------------------------------|
|VMSTEST |Externe |Zusammengeschlossen-Schnittstelle|

Mit diesem Befehl können Sie den physischen Adapter-Teams in der Gruppe anzeigen.

    Get-VMSwitchTeam -Name "VMSTEST" | fl

Folgendes sind die Ergebnisse dieses Befehls.

**Namen**: VMSTEST **ID**: ad9bb542-dda2-4450-a00e-f96d44bdfbec **NetAdapterInterfaceDescription**: {Mellanox ConnectX-3 Pro-Ethernet-Adapter, Mellanox ConnectX-3 Pro-Ethernet-Adapter 2} **TeamingMode**: SwitchIndependent **LoadBalancingAlgorithm**: dynamische

#### <a name="display-two-views-of-the-host-vnic"></a>Anzeigen von zwei Ansichten des Host-vNIC

Sie können die folgenden zwei Befehle für zwei verschiedenen Ansichten des Host-vNIC verwenden.

Sie können diesen Befehl verwenden, um die Host-vNIC Eigenschaften anzuzeigen.

    Get-NetAdapter

Folgendes sind die Ergebnisse dieses Befehls.

| Namen | InterfaceDescription | IfIndex | Status | MacAddress | LinkSpeed | |------|---|---|---|---| | | vEthernet (VMSTEST) | Hyper-V virtuelle Ethernet-Adapter 2 | 28 | Sie | E4-1D-2D-07-40-71|80 Gbit/s |

Sie können diesen Befehl verwenden, um zusätzliche Eigenschaften die Host-vNIC anzuzeigen.

    Get-VMNetworkAdapter -ManagementOS

Folgendes sind die Ergebnisse dieses Befehls.

|Name |IsManagementOs |Name des virtuellen Computers |SwitchName |MacAddress |Status |IP-Adressen|
|----|--------------|------|----------|----------|------|-----------|
|
|VMSTEST|"True" |VMSTEST |E41D2D074071| {Ok}|&nbsp;|

#### <a name="test-the-network-connection-to-the-remote-vlan-101-adapter"></a>Testen Sie die Netzwerkverbindung mit dem Remote-VLAN-101-Adapter

Mit diesem Befehl können Sie um die Verbindung mit dem Remote-VLAN 101 Adapter testen.

`Test-NetConnection 192.168.1.5` 

Folgendes sind die Ergebnisse dieses Befehls.

    WARNING: Ping to 192.168.1.5 failed -- Status: DestinationHostUnreachable
    
    ComputerName   : 192.168.1.5
    RemoteAddress  : 192.168.1.5
    InterfaceAlias : vEthernet (CORP-External-Switch)
    SourceAddress  : 10.199.48.170
    PingSucceeded  : False
    PingReplyDetails (RTT) : 0 ms
    
### <a name="reconfigure-vlans"></a>Konfigurieren von VLANs

Sie können diesen Schrittdie ACCESS-VLAN-Einstellung aus der physischen NIC entfernen und die VLAN-ID mit der vSwitch festlegen.

Sie müssen die ACCESS-VLAN-Einstellung, um zu verhindern, dass beide automatische Kennzeichnung des ausgehenden Datenverkehrs mit der falschen VLAN-ID entfernen und von Filterung von eingehendem Datenverkehr die ACCESS-VLAN-ID übereinstimmt

Die folgenden Befehle können Sie die Einstellung VLAN Zugriff entfernen.
    
    Set-NetAdapterAdvancedProperty -Name "Test-40G-1" -RegistryKeyword VlanID -RegistryValue "0"
    Set-NetAdapterAdvancedProperty -Name "Test-40G-2" -RegistryKeyword VlanID -RegistryValue "0"
    

Sie können die folgenden Befehle die VLAN-ID vSwitch spezifische Windows PowerShell-Befehle festlegen und zum Anzeigen der Ergebnisse dieser Aktion verwenden.

    
    Set-VMNetworkAdapterVlan -VMNetworkAdapterName "VMSTEST" -VlanId "101" -Access -ManagementOS
    Get-VMNetworkAdapterVlan -ManagementOS -VMNetworkAdapterName "VMSTEST"
    

Folgendes sind die Ergebnisse dieses Befehls.

Name des virtuellen Computers VMNetworkAdapterName Modus VlanList
------ -------------------- ----   --------
       VMSTEST              Access 101     

Sie können den folgenden Befehl die Netzwerkverbindung testen und die Ergebnisse anzuzeigen.

    Test-NetConnection 192.168.1.5
    
    ComputerName   : 192.168.1.5
    RemoteAddress  : 192.168.1.5
    InterfaceAlias : vEthernet (VMSTEST)
    SourceAddress  : 192.168.1.3
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
    

Wenn die Ergebnisse ähneln sich nicht mit dem Beispiel und Ping-Befehl, mit der Meldung fehlschlägt "WARNING: Fehler beim Befehl Ping 192.168.1.5 – Status: DestinationHostUnreachable," bestätigen, dass "vEthernet (VMSTEST)" die richtige IP-Adresse verfügt, indem Sie den folgenden Befehl ausführen.

    
    Get-NetIPAddress -InterfaceAlias "vEthernet (VMSTEST)"
    

Wenn die IP-Adresse nicht festgelegt ist, können Sie den folgenden Befehl das Problem zu beheben und die Ergebnisse Ihrer Aktionen anzuzeigen.

    
    New-NetIPAddress -InterfaceAlias "vEthernet (VMSTEST)" -IPAddress 192.168.1.3 -PrefixLength 24
    
    IPAddress : 192.168.1.3
    InterfaceIndex: 37
    InterfaceAlias: vEthernet (VMSTEST)
    AddressFamily : IPv4
    Type  : Unicast
    PrefixLength  : 24
    PrefixOrigin  : Manual
    SuffixOrigin  : Manual
    AddressState  : Tentative
    ValidLifetime : Infinite ([TimeSpan]::MaxValue)
    PreferredLifetime : Infinite ([TimeSpan]::MaxValue)
    SkipAsSource  : False
    PolicyStore   : ActiveStore
    
#### <a name="rename-the-management-nic"></a>Benennen Sie die NIC-Verwaltung

Sie können mithilfe dieses Abschnitts die Verwaltungs-NIC umbenennen und später separate Instanzen von Host-vNIC für RDMA verwenden.

Sie können die folgenden Befehle zum Benennen Sie die Verwaltungs-NIC und Anzeigen von einigen NIC-Eigenschaften ausführen.

    Rename-VMNetworkAdapter -ManagementOS -Name “VMSTEST” -NewName “MGT”
    Get-VMNetworkAdapter -ManagementOS

Folgendes sind die Ergebnisse dieses Befehls.

|Name |IsManagementOs |Name des virtuellen Computers |SwitchName |MacAddress |Status |IP-Adressen
|----|--------------|------|----------|----------|------|-----------|
|
|CORP-External-Switch |"True" |&nbsp;|CORP-External-Switch |001B785768AA |{Ok}|&nbsp;|
|MANAGEMENT |"True" |&nbsp;|VMSTEST |E41D2D074071 |{Ok}|&nbsp;|

Sie können einige zusätzlichen NIC-Eigenschaften an den folgenden Befehl ausführen.

    Get-NetAdapter

Folgendes sind die Ergebnisse dieses Befehls.

|Name |InterfaceDescription |ifIndex |Status |MacAddress |LinkSpeed|
|----|--------------------|------|----------|---------|------|
|
|vEthernet (Management) |Virtuelle Hyper-V-Ethernet-Adapter 2 |28 |Nach-oben | E4-1D-2D-07-40-71 |80 Gbit/s|

## <a name="test-hyper-v-virtual-switch-rdma"></a>Testen von Hyper-V Virtual Switch RDMA

Die folgende Abbildungzeigt den aktuellen Status des Hyper-V-Hosts, einschließlich der vSwitch auf dem Hyper-V-Host 1.

![Testen Sie den virtuellen Hyper-V-Switch](../../media/Converged-NIC/6-datacenter-test-vswitch-rdma.jpg)

### <a name="set-priority-tagging-on-the-host-vnic-to-complement-the-previous-vlan-settings"></a>Festlegen der Priorität auf dem Host-vNIC-Kennzeichnung werden die vorherigen VLAN-Einstellungen

Sie können die folgenden Beispielbefehle verwenden, zum Festlegen der Priorität, die auf dem Host-vNIC-Kennzeichnung und Anzeigen der Ergebnisse Ihrer Aktionen.
    
    Set-VMNetworkAdapter -ManagementOS -Name "MGT" -IeeePriorityTag on
    Get-VMNetworkAdapter -ManagementOS -Name "MGT" | fl Name,IeeePriorityTag
    

    Name: MGT
    IeeePriorityTag : On
    
### <a name="create-two-host-vnics-for-rdma"></a>Erstellen Sie zwei Host-vNICs für RDMA

Sie können die folgenden Beispielbefehle verwenden, zwei Host-vNICs für RDMA erstellen, und verbinden Sie sie mit der vSwitch VMSTEST.
    
    Add-VMNetworkAdapter –SwitchName "VMSTEST" –Name SMB1 –ManagementOS
    Add-VMNetworkAdapter –SwitchName "VMSTEST" –Name SMB2 –ManagementOS
    
Befehl im folgenden Beispiel können Sie die Verwaltungs-NIC-Eigenschaften anzuzeigen.
    
    Get-VMNetworkAdapter -ManagementOS
    
Folgendes sind die Ergebnisse dieses Befehls.

|Name |IsManagementOs |Name des virtuellen Computers |SwitchName |MacAddress |Status |IP-Adressen|
|----|--------------|------|----------|----------|------|-----------|
|
|CORP-External-Switch |"True" |CORP-External-Switch |001B785768AA|{Ok} |&nbsp;| 
|Management |"True" |VMSTEST |E41D2D074071 |{Ok} |&nbsp;|
|SMB1 |"True" |VMSTEST |00155D30AA00 |{Ok} |&nbsp;|
|SMB2 |"True" |VMSTEST |00155D30AA01 |{Ok} |&nbsp;|

### <a name="assign-an-ip-address-to-the-smb-host-vnics"></a>Der SMB-Host-vNICs eine IP-Adresse zuweisen

Sie können in diesem Abschnittverwenden, die SMB-Host-vNICs vEthernet IP Addressrd zuweisen \(SMB1\) und vEthernet \(SMB2\).

Der TEST-40G-1 und TEST-40G-2 physischen Adapter haben immer noch eine VLAN Zugriff 101 und 102 konfiguriert. Aus diesem Grund die Adapter den Datenverkehr - tag- und Ping erfolgreich ist.

Zuvor Sie beide pNIC VLAN-IDs 0 (null) konfiguriert und dann VMSTEST vSwitch auf VLAN 101 festgelegt. Wurden Sie noch immer auf den Remote-VLAN-101-Adapter zu erreichen, mithilfe der Management-vNIC, aber es sind zurzeit keine Mitglieder VLAN 102.

Nun können Sie den folgenden Befehl werden beispielsweise die ACCESS-VLAN-Einstellung über die physische NIC, um zu verhindern, dass beide automatische Kennzeichnung des ausgehenden Datenverkehrs mit der falschen VLAN-ID und um zu verhindern, Filtern eingehende Datenverkehr zu entfernen entspricht, die die ACCESS-VLAN-Kennung nicht

Sie können mit dem Befehl im folgenden Beispiel um durch Hinzufügen einer neuen IP-Adresse vEthernet (SMB1) Schnittstellen zu Ziele und Anzeigen der Ergebnisse.

    
    New-NetIPAddress -InterfaceAlias "vEthernet (SMB1)" -IPAddress 192.168.2.111 -PrefixLength 24
    
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
    

Befehl im folgenden Beispiel können Sie testen, des Remote-VLAN 102 Adapters und Anzeigen der Ergebnisse.
    
    Test-NetConnection 192.168.2.5 
    
    ComputerName   : 192.168.2.5
    RemoteAddress  : 192.168.2.5
    InterfaceAlias : vEthernet (SMB1)
    SourceAddress  : 192.168.2.111
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
    
Sie können den folgenden Befehl werden beispielsweise eine neue IP-Adresse für die Schnittstelle vEthernet hinzufügen \(SMB2\), und die Ergebnisse anzuzeigen.
    
    New-NetIPAddress -InterfaceAlias "vEthernet (SMB2)" -IPAddress 192.168.2.222 -PrefixLength 24 
    
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
    
Sie müssen nicht erneut die Verbindung zu testen, da Kommunikation hergestellt wird.

### <a name="place-the-rdma-host-vnics-on-vlan-102"></a>Platzieren Sie die RDMA-Host-vNICs auf VLAN 102

In diesem Abschnittkönnen Sie die RDMA-Host-vNICs 102 VLAN zuweisen.

Da die "Management" Host-vNIC auf VLAN 101 befindet, können Sie die folgenden Beispielbefehle verwenden, die RDMA-Host-vNICs in die vorhandene VLAN 102 und Anzeigen der Ergebnisse Ihrer Aktionen.

    
    Set-VMNetworkAdapterVlan -VMNetworkAdapterName "SMB1" -VlanId "102" -Access -ManagementOS
    Set-VMNetworkAdapterVlan -VMNetworkAdapterName "SMB2" -VlanId "102" -Access -ManagementOS
    
    Get-VMNetworkAdapterVlan -ManagementOS
    
    VMName VMNetworkAdapterName Mode VlanList
    ------ -------------------- ---- --------
       SMB1 Access   102 
       Mgt  Access   101 
       SMB2 Access   102 
       CORP-External-Switch Untagged
    
### <a name="inspect-the-mapping-of-smb1-and-smb2-to-the-underlying-physical-nics"></a>Untersuchen Sie die Zuordnung von SMB1 und SMB2 mit den zugrunde liegenden physischen NICs

In diesem Abschnittkönnen, überprüfen die Zuordnung der SMB1 und SMB2 mit den zugrunde liegenden physischen NICs unter vSwitch Team festgelegt.  Die Zuordnung der Host-vNIC auf physische NICs ist zufällige und während der Erstellung und Zerstörung Neuverteilen.

In diesem Fall können Sie einen indirekte Mechanismus zum Überprüfen der aktuellen Zuordnung.

Die MAC-Adressen der SMB1 und SMB2 sind Member der NIC-Team TEST-40G-2 zugeordnet. Dies ist nicht ideal, da die Test-40G-1 verfügt nicht über eine zugehörige SMB-Host-vNIC, und verhindert, dass für die Nutzung von RDMA-Datenverkehr über den Link erst eine SMB-Host-vNIC zugeordnet ist.

Sie können die folgenden Beispielbefehle verwenden, zum Anzeigen dieser Informationen.

    
    Get-NetAdapterVPort (Preferred)
    
    Get-NetAdapterVmqQueue
    
    Name   QueueID MacAddressVlanID Processor VmFriendlyName
    ----   ------- ---------------- --------- --------------
    TEST-40G-1 1   E4-1D-2D-07-40-71 1010:17
    TEST-40G-2 1   00-15-5D-30-AA-00 1020:17
    TEST-40G-2 2   00-15-5D-30-AA-01 1020:17
    
    Get-VMNetworkAdapter -ManagementOS
    
    Name IsManagementOs VMName SwitchName   MacAddress   Status IPAddresses
    ---- -------------- ------ ----------   ----------   ------ -----------
    CORP-External-Switch True  CORP-External-Switch 001B785768AA {Ok}  
    Mgt  True  VMSTEST  E41D2D074071 {Ok}  
    SMB1 True  VMSTEST  00155D30AA00 {Ok}  
    SMB2 True  VMSTEST  00155D30AA01 {Ok}  
    

Die folgenden beiden Befehle sollte keine Informationen zurückgegeben werden, da Zuordnung noch nicht durchgeführt haben.
    
    Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName SMB1
    Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName SMB2
    
Die folgenden Beispielbefehle können SMB1 und SMB2 physischen NIC-Team Member getrennt, und klicken Sie zum Anzeigen der Ergebnisse Ihrer Aktionen zuordnen.

>[!IMPORTANT]
>Stellen Sie sicher, dass Sie führen Sie diesen Schritt, bevor Sie fortfahren, oder Ihre Implementierung schlägt fehl.
    
    Set-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName "SMB1" -PhysicalNetAdapterName "Test-40G-1"
    Set-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName "SMB2" -PhysicalNetAdapterName "Test-40G-2"
    
    Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST
    
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
    
### <a name="confirm-the-mac-associations"></a>Bestätigen Sie die MAC-Zuordnungen

Die folgenden Beispielbefehle können Sie um die MAC-Zuordnungen zu bestätigen, die Sie zuvor erstellt haben.
    
    Get-NetAdapterVmqQueue
    
    Name   QueueID MacAddressVlanID Processor VmFriendlyName
    ----   ------- ---------------- --------- --------------
    TEST-40G-1 1   E4-1D-2D-07-40-71 1010:17
    TEST-40G-1 2   00-15-5D-30-AA-00 1020:17
    TEST-40G-2 1   00-15-5D-30-AA-01 1020:17
    

Daran, dass sowohl Host-vNICs im gleichen Subnetz befinden und die gleichen VLAN-ID \(102\), können Sie Kommunikation mit dem Remotesystem überprüfen und Anzeigen der Ergebnisse Ihrer Aktionen.

>[!IMPORTANT]
>Führen Sie die folgenden Befehle auf dem Remotecomputer.

    
    Test-NetConnection 192.168.2.111
    
    
    ComputerName   : 192.168.2.111
    RemoteAddress  : 192.168.2.111
    InterfaceAlias : Test-40G-2
    SourceAddress  : 192.168.2.5
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
    
    Test-NetConnection 192.168.2.222
    
    ComputerName   : 192.168.2.222
    RemoteAddress  : 192.168.2.222
    InterfaceAlias : Test-40G-2
    SourceAddress  : 192.168.2.5
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms 
    
        
    Set-VMNetworkAdapter -ManagementOS -Name "SMB1" -IeeePriorityTag on
    Set-VMNetworkAdapter -ManagementOS -Name "SMB2" -IeeePriorityTag on
    Get-VMNetworkAdapter -ManagementOS -Name "SMB*" | fl Name,SwitchName,IeeePriorityTag,Status
    
    Name: SMB1
    SwitchName  : VMSTEST
    IeeePriorityTag : On
    Status  : {Ok}
    
    Name: SMB2
    SwitchName  : VMSTEST
    IeeePriorityTag : On
    Status  : {Ok}
    

    Get-NetAdapterRdma -Name "vEthernet*" | sort Name | ft -AutoSize
    
    Name  InterfaceDescription Enabled
    ----  -------------------- -------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  False  
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  False  
    vEthernet (MGT)   Hyper-V Virtual Ethernet Adapter #2  False   
    
    
    Enable-NetAdapterRdma -Name "vEthernet (SMB1)"
    Enable-NetAdapterRdma -Name "vEthernet (SMB2)"
    Get-NetAdapterRdma -Name "vEthernet*" | sort Name | fl *
    
    
    Name  InterfaceDescription Enabled
    ----  -------------------- -------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  True   
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  True  
    vEthernet (MGT)   Hyper-V Virtual Ethernet Adapter #2  False
      

### <a name="validate-rdma-functionality-from-the-remote-system"></a>Überprüfen Sie die RDMA-Funktionalität von Remote-System

In diesem Abschnittkönnen Sie die um RDMA-Funktionalität von Remote-System auf das lokale System, das mit einem vSwitch, zu überprüfen und Tests sowohl Adapter, die Mitglieder des vSwitch SET-Teams sind.

Da beide Host-vNICs \ (SMB1 und SMB2\) VLAN 102 zugewiesen sind, können Sie die VLAN-102-Adapter auf dem Remotesystem auswählen.  

Bei diesem Vorgang wird die NIC-Test-40G-2 RDMA auf SMB1 (192.168.2.111) und SMB2 (192.168.2.222).

Optional: Sie müssen möglicherweise die Firewall auf dem System deaktivieren.  Einzelheiten finden Sie in der Fabric-Richtlinie.

    
    Set-NetFirewallProfile -All -Enabled False
    
    Get-NetAdapterAdvancedProperty -Name "Test-40G-2"
    
    Name  DisplayNameDisplayValue   RegistryKeyword RegistryValue  
    ----  -----------------------   --------------- -------------  
    .
    .
    Test-40G-2VLAN ID102VlanID  {102} 
    
    Get-NetAdapter
    
    Name  InterfaceDescriptionifIndex Status   MacAddress LinkSpeed
    ----  --------------------------- ------   ---------- ---------
    Test-40G-2Mellanox ConnectX-3 Pro Ethernet A...#3   3 Up   E4-1D-2D-07-43-D140 Gbps
    
    
    Get-NetAdapterRdma
    
    Name  InterfaceDescription Enabled
    ----  -------------------- -------
    Test-40G-2Mellanox ConnectX-3 Pro Ethernet Adap... True   
    
    
    C:\TEST\Test-RDMA.PS1 -IfIndex 3 -IsRoCE $true -RemoteIpAddress 192.168.2.111 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
    VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\\diskspd.exe
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
    
    
    C:\TEST\Test-RDMA.PS1 -IfIndex 3 -IsRoCE $true -RemoteIpAddress 192.168.2.222 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
    VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\\diskspd.exe
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
    
### <a name="test-for-rdma-traffic-from-the-local-to-the-remote-computer"></a>Test für RDMA-Datenverkehr aus dem lokalen an den Remotecomputer

In diesem Abschnittkönnen Sie überprüfen, ob die RDMA-Datenverkehr vom lokalen Computer an den Remotecomputer gesendet wird.

Sie können die folgenden Beispielbefehle verwenden, zum Testen und Anzeigen der Datenfluss.

    
    Get-NetAdapter | ft –AutoSize
    
    Name  InterfaceDescriptionifIndex Status   MacAddress LinkSpeed
    ----  --------------------------- ------   ---------- ---------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  45 Up   00-15-5D-30-AA-0380 Gbps
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  41 Up   00-15-5D-30-AA-0280 Gbps
    
    
    C:\TEST\Test-RDMA.PS1 -IfIndex 41 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
    VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\\diskspd.exe
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
    
    
    C:\TEST\Test-RDMA.PS1 -IfIndex 45 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
    VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\\diskspd.exe
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
    
Die letzte Zeile in dieser Ausgabe "RDMA-Verkehr Test erfolgreich: RDMA-Datenverkehr an 192.168.2.5, gesendet wurde" gibt an, dass Sie erfolgreich zusammengeführten NIC auf dem Adapter konfiguriert haben.

## <a name="all-topics-in-this-guide"></a>Alle Themen in diesem Handbuch

Dieses Handbuch enthält die folgenden Themen.

- [Zusammengeführtes NIC-Konfiguration mit einem einzelnen Netzwerkadapter](cnic-single.md)
- [Zusammengeführtes NIC kombinierten NIC-Konfiguration](cnic-datacenter.md)
- [Physischen Switch-Konfiguration für die zusammengeführten NIC](cnic-app-switch-config.md)
- [Problembehandlung bei zusammengeführten NIC-Konfigurationen](cnic-app-troubleshoot.md)
