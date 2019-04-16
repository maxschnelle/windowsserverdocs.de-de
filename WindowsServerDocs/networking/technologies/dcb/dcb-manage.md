---
title: Verwalten von Data Center Bridging (DCB)
description: In diesem Thema erhalten Sie Anweisungen zur Verwendung von Windows PowerShell-Befehle zum Verwalten von Data Center Bridging in Windows Server2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 1575cc7c-62a7-4add-8f78-e5d93effe93f
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: dbe9e5e4af2ddd834b5b8f38e9ffd1b403e92793
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="manage-data-center-bridging-dcb"></a>Verwalten von Data Center Bridging (DCB)

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema erhalten Sie Anweisungen zur Verwendung von Windows PowerShell-Befehle zum Data Center Bridging \(DCB\) auf einem Netzwerkadapter DCB\-kompatiblen zu konfigurieren, die auf einem Computer installiert ist, auf denen Windows Server2016 oder Windows10 ausgeführt wird.

## <a name="install-dcb-in-windows-server-2016-or-windows-10"></a>Installieren Sie DCB wird in Windows Server 2016 oder Windows10.

Informationen zu Voraussetzungen für die Verwendung und DCB installieren, finden Sie unter [installieren Data Center Bridging (DCB) in Windows Server2016 oder Windows10](dcb-install.md).


## <a name="dcb-configurations"></a>DCB-Konfigurationen 

Vor Windows Server2016 wurde alle DCB-Konfiguration universell für alle Netzwerkadapter angewendet, die DCB unterstützt. 

In Windows Server2016 können Sie DCB-Konfigurationen Richtlinienspeicher Global oder einzelne Richtlinie Store\(s\) anwenden. Wenn einzelne Richtlinien angewendet werden sie alle globalen Einstellungen außer Kraft setzen.

Die Konfigurationen der Zuweisung Datenverkehr-Klasse, PCF und Anwendung der Priorität auf Systemebene ist nicht auf Netzwerkadapter angewendet, bis Sie die folgenden Schritteaus.

1. Aktivieren Sie das Bit DCBX bereit, auf "false"

2. Aktivieren Sie DCB für die Netzwerkadapter. Weitere Informationen finden Sie unter [aktivieren und Anzeigen von DCB-Einstellungen für Netzwerkadapter](#bkmk_enabledcb).

>[!NOTE]
>Wenn Sie von einem Switch über DCBX DCB konfigurieren möchten, finden Sie unter [DCBX-Einstellungen](#BKMK_DCBX_Settings)

Das DCBX bereit Bit ist in der DCB-Spezifikation beschrieben. Wenn das bereit Bit auf einem Gerät festgelegt ist, auf true festgelegt ist, das Gerät ist Konfigurationen von einem Remotegerät über DCBX akzeptiert. Wenn das bereit Bit auf einem Gerät auf "false" festgelegt ist, wird das Gerät Ablehnen aller Configuration Zugriffsversuche von Remotegeräten und nur die lokalen Konfigurationen zu erzwingen.

Wenn DCB nicht in Windows Server2016 installiert ist ist der Wert des bereit Bits nicht relevant, als Betriebssystems betroffen ist, da das Betriebssystem keine lokalen Einstellungen auf Netzwerkadapter angewendet wurde. Nach der Installation von DCB ist der Standardwert des bereit Bits "true". Dies ermöglicht die Netzwerkadapter für alle Konfigurationen behalten sie möglicherweise von ihren Remotepeers erhalten haben.

Wenn ein Netzwerkadapter DCBX unterstützt wird, erhält es nie Konfigurationen von einem Remotegerät. Er erhält Konfigurationen aus dem Betriebssystem, jedoch erst, nachdem Sie die DCBX bereit Bit auf "false" festgelegt ist.

## <a name="set-the-willing-bit"></a>Legen Sie das Bit bereit

Betriebssystemkonfigurationen Datenverkehrsklasse sowie PFC Anwendung Priorität Zuordnung für Netzwerkadapter zu erzwingen oder überschreiben Sie einfach die Konfigurationen von Remotegeräten \ – ggf. \ – Sie können den folgenden Befehl ausführen.

>[!NOTE]
>DCB Windows PowerShell-Befehlsnamen enthalten "QoS" anstelle von "DCB" in der Zeichenfolge. Dies liegt daran QoS und DCB integriert sind, in Windows Server2016 eine nahtlose QoS-Management-Oberfläche bereitzustellen.

    
    Set-NetQosDcbxSetting -Willing $FALSE
    
    Confirm
    Are you sure you want to perform this action?
    Set-NetQosDcbxSetting -Willing $false
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"):
    

Um den Zustand des bereit Bits Einstellung anzuzeigen, können Sie den folgenden Befehl verwenden:

    
    Get-NetQosDcbxSetting
    
    Willing PolicySetIfIndex IfAlias
    ------- ---------------- -------
    False   Global  
    

## <a name="dcb-configuration-on-network-adapters"></a>DCB-Konfiguration für Netzwerkadapter

Aktivieren DCB für einen Netzwerkadapter, können Sie die Konfiguration von einem Switch auf den Netzwerkadapter übermittelt finden Sie unter.

DCB-Konfigurationen umfassen die folgenden Schritteaus.

1.  Konfigurieren Sie DCB-Einstellungen auf Systemebene, einschließlich:

    ein. Datenverkehrsverwaltung-Klasse
    
    b. Prioritätseinstellungen Nachrichtenfluss-Steuerelement (PFC)
    
    c. Anwendung Priorität Zuweisung
    
    d. DCBX-Einstellungen

2. Konfigurieren Sie DCB für den Netzwerkadapter.



##  <a name="dcb-traffic-class-management"></a>Datenverkehrsklasse DCB-Verwaltung

Folgendes Beispiel Windows PowerShell-Befehle für die Datenverkehrsklasse Verwaltung sind.

### <a name="create-a-traffic-class"></a>Erstellen Sie eine Datenverkehrsklasse

Können die **New-NetQosTrafficClass** Befehl aus, um eine Datenverkehrsklasse zu erstellen.

    
    New-NetQosTrafficClass -Name SMB -Priority 4 -BandwidthPercentage 30 -Algorithm ETS
    
    Name Algorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ---- --------- ------------ -------- ---------------- -------
    SMB  ETS   30   4Global
      

Standardmäßig werden alle 802. 1p-Werte eine Datenverkehrsklasse standardmäßig zugeordnet, die über 100% der Bandbreite der physischen Verbindung. Die **New-NetQosTrafficClass** Befehl erstellt eine neue Datenverkehrsklasse, welche Pakete, die mit 802. 1p-Priorität gekennzeichnet ist 4-Wert zugeordnet ist. Die Übertragung Auswahl Algorithmus \(TSA\) ETS und 30% der Bandbreite.

Sie können bis zu 7 neue Klassen erstellen. Einschließlich der Standard-Datenverkehrsklasse darf höchstens 8 Datenverkehrsklassen des Systems. Ein DCB-fähiger Netzwerkadapter unterstützen jedoch nicht, dass viele Klassen in der Hardware des Datenverkehrs. Wenn Sie erstellen Weitere Datenverkehrsklassen als auf einem Netzwerkadapter verwendet werden kann, und Sie DCB auf Netzwerkadapter aktivieren, meldet der Miniporttreiber einen Fehler an das Betriebssystem. Der Fehler wird im Ereignisprotokoll protokolliert.

Die Summe der Bandbreite Reservierungen für alle erstellten Datenverkehrsklassen darf 99% der Bandbreite nicht überschreiten. Der Standard-Datenverkehrsklasse verfügt immer über mindestens 1Prozent der Bandbreite für sich selbst reserviert.

### <a name="display-traffic-classes"></a>Anzeigen von Klassen

Sie können die **Get-NetQosTrafficClass** Befehl, um Datenverkehrsklassen anzuzeigen.

    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   70   0-3,5-7  Global
    SMB ETS   30   4Global  
    
### <a name="modify-a-traffic-class"></a>Ändern Sie eine Datenverkehrsklasse

Sie können die **Set-NetQosTrafficClass** Befehl aus, um eine Datenverkehrsklasse erstellen. 

    Set-NetQosTrafficClass -Name SMB -BandwidthPercentage 50

Anschließend können Sie die **Get-NetQosTrafficClass** Befehl, um Einstellungen anzuzeigen.

    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   50   0-3,5-7  Global
    SMB ETS   50   4Global   
    

Nachdem Sie eine Datenverkehrsklasse erstellt haben, können Sie die Einstellungen ändern unabhängig. Die Einstellungen, die Sie ändern können, gehören:

1. Die Zuordnung \(-BandwidthPercentage\) Bandbreite

2. TSA (\-Algorithm\)

3. Die Zuordnung \(-Priority\) Priorität

### <a name="remove-a-traffic-class"></a>Entfernen Sie eine Datenverkehrsklasse

Sie können die **Remove-NetQosTrafficClass** Befehl aus, um eine Datenverkehrsklasse zu löschen.

>[!IMPORTANT]
>Der Standard-Datenverkehrsklasse nicht entfernt werden.


    Remove-NetQosTrafficClass -Name SMB

Anschließend können Sie die **Get-NetQosTrafficClass** Befehl, um Einstellungen anzuzeigen.
    
    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   100  0-7  Global
    

Wenn Sie eine Datenverkehrsklasse entfernen, zugeordnet der 802. 1p-Wert, dass der standardmäßige Datenverkehrsklasse Datenverkehrsklasse zugeordnet ist. Bei der Datenverkehrsklasse entfernt wird, wird die Reservierung des Standard-Datenverkehr Klasse Bandbreite, die für eine Datenverkehrsklasse reserviert wurde zurückgegeben.

## <a name="per-network-interface-policies"></a>Pro-Netzwerk-Richtlinien für die Benutzeroberfläche

Alle oben genannten Beispiele wird die globalen Richtlinien festlegen. Es folgen Beispiele für festlegen und Abrufen von pro-NIC-Richtlinien. 

Das Feld "PolicySet" wird von Global zu AdapterSpecific. Wenn AdapterSpecific Richtlinien angezeigt werden, werden auch die Schnittstellenindex \(ifIndex\) und Schnittstellennamen \(ifAlias\) angezeigt.

```
PS C:\> Get-NetQosTrafficClass

Name        Algorithm Bandwidth(%) Priority         PolicySet        IfIndex IfAlias
----        --------- ------------ --------         ---------        ------- -------
[Default]   ETS       100          0-7              Global


PS C:\> Get-NetQosTrafficClass -InterfaceAlias M1

Name        Algorithm Bandwidth(%) Priority         PolicySet        IfIndex IfAlias
----        --------- ------------ --------         ---------        ------- -------
[Default]   ETS       100          0-7              AdapterSpecific  4       M1


PS C:\> New-NetQosTrafficClass -Name SMBGlobal -BandwidthPercentage 30 -Priority 4 -Algorithm ETS

Name        Algorithm Bandwidth(%) Priority         PolicySet        IfIndex IfAlias
----        --------- ------------ --------         ---------        ------- -------
SMBGlobal   ETS       30           4                Global


PS C:\> New-NetQosTrafficClass -Name SMBforM1 -BandwidthPercentage 30 -Priority 4 -Algorithm ETS -Interfac


Name        Algorithm Bandwidth(%) Priority         PolicySet        IfIndex IfAlias
----        --------- ------------ --------         ---------        ------- -------
SMBforM1    ETS       30           4                AdapterSpecific  4       M1


PS C:\> Get-NetQosTrafficClass

Name        Algorithm Bandwidth(%) Priority         PolicySet        IfIndex IfAlias
----        --------- ------------ --------         ---------        ------- -------
[Default]   ETS       70           0-3,5-7          Global
SMBGlobal   ETS       30           4                Global


PS C:\> Get-NetQosTrafficClass -InterfaceAlias M1

Name        Algorithm Bandwidth(%) Priority         PolicySet        IfIndex IfAlias
----        --------- ------------ --------         ---------        ------- -------
[Default]   ETS       70           0-3,5-7          AdapterSpecific  4       M1
SMBforM1    ETS       30           4                AdapterSpecific  4       M1


```

## <a name="priority-flow-control-settings"></a>Flusssteuerung prioritätseinstellungen:

Folgen Befehlsbeispiele für die Einstellung der Priorität flusssteuerung. Diese Einstellungen können auch für einzelne Adapter angegeben werden.

### <a name="enable-and-display-priority-flow-control-for-global-and-interface-specific-use-cases"></a>Aktivieren und Anzeige Priorität flusssteuerung für globale und Schnittstelle bestimmte Anwendungsfälle

```
PS C:\> Enable-NetQosFlowControl -Priority 4
PS C:\> Enable-NetQosFlowControl -Priority 3 -InterfaceAlias M1
PS C:\> Get-NetQosFlowControl

Priority   Enabled    PolicySet        IfIndex IfAlias
--------   -------    ---------        ------- -------
0          False      Global
1          False      Global
2          False      Global
3          False      Global
4          True       Global
5          False      Global
6          False      Global
7          False      Global

PS C:\> Get-NetQosFlowControl -InterfaceAlias M1

Priority   Enabled    PolicySet        IfIndex IfAlias
--------   -------    ---------        ------- -------
0          False      AdapterSpecific  4       M1
1          False      AdapterSpecific  4       M1
2          False      AdapterSpecific  4       M1
3          True       AdapterSpecific  4       M1
4          False      AdapterSpecific  4       M1
5          False      AdapterSpecific  4       M1
6          False      AdapterSpecific  4       M1
7          False      AdapterSpecific  4       M1  

```


### <a name="disable-priority-flow-control-global-and-interface-specific"></a>Deaktivieren der Flusspriorisierung (globale spezifische Benutzeroberfläche)

```
PS C:\> Disable-NetQosFlowControl -Priority 4
PS C:\> Disable-NetQosFlowControl -Priority 3 -InterfaceAlias m1
PS C:\> Get-NetQosFlowControl

Priority   Enabled    PolicySet        IfIndex IfAlias
--------   -------    ---------        ------- -------
0          False      Global
1          False      Global
2          False      Global
3          False      Global
4          False      Global
5          False      Global
6          False      Global
7          False      Global


PS C:\> Get-NetQosFlowControl -InterfaceAlias M1

Priority   Enabled    PolicySet        IfIndex IfAlias
--------   -------    ---------        ------- -------
0          False      AdapterSpecific  4       M1
1          False      AdapterSpecific  4       M1
2          False      AdapterSpecific  4       M1
3          False      AdapterSpecific  4       M1
4          False      AdapterSpecific  4       M1
5          False      AdapterSpecific  4       M1
6          False      AdapterSpecific  4       M1
7          False      AdapterSpecific  4       M1  

```

##  <a name="application-priority-assignment"></a>Anwendung Priorität Zuweisung

Folgen einige Beispiele für Zuweisung Priorität.

### <a name="create-qos-policy"></a>QoS-Richtlinie erstellen

```
PS C:\> New-NetQosPolicy -Name "SMB Policy" -PriorityValue8021Action 4

Name           : SMB Policy
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
JobObject      :
PriorityValue  : 4

```

Der vorherige Befehl erstellt eine neue Richtlinie für SMB. SMB – ist ein Eingangsbox-Filter, der TCP-Port 445 (SMB-reserviert) entspricht. Wenn ein Paket an TCP-Port 445 gesendet wird, die sie vom Betriebssystem mit 802. 1p-Wert von 4 vor markiert wird das Paket an einen Netzwerk-Miniporttreiber übergeben.

Zusätzlich zu – SMB enthalten andere Standardfilter – iSCSI (übereinstimmenden TCP-Port 3260), - NFS (übereinstimmenden TCP-Port 2049), --Livemigration (übereinstimmenden TCP-Port 6600), - FCOE (Übereinstimmung EtherType 0x8906) und – NetworkDirect.

NetworkDirect ist eine abstrakte Ebene, die wir über keine RDMA-Implementierung auf einem Netzwerkadapter zu erstellen. – NetworkDirect muss von einem Network Direct Port folgen.

Zusätzlich zu den Standardfilter können Sie Datenverkehr klassifizieren, durch den Namen der ausführbaren Datei der Anwendung (wie im ersten Beispiel unten) oder IP-Adresse, Port und Protokoll (wie im zweiten Beispiel gezeigt):

**Durch den Namen der ausführbaren Datei**

```
PS C:\> New-NetQosPolicy -Name background -AppPathNameMatchCondition "C:\Program files (x86)\backup.exe" -PriorityValue8021Action 1

Name           : background
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
AppPathName    : C:\Program files (x86)\backup.exe
JobObject      :
PriorityValue  : 1

```


**Nach IP-Adressport oder Protokoll**

```
PS C:\> New-NetQosPolicy -Name "Network Management" -IPDstPrefixMatchCondition 10.240.1.0/24 -IPProtocolMatchCondition both -NetworkProfile all -PriorityValue8021Action 7

Name           : Network Management
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
JobObject      :
IPProtocol     : Both
IPDstPrefix    : 10.240.1.0/24
PriorityValue  : 7

```

### <a name="display-qos-policy"></a>Anzeigen von QoS-Richtlinie

```
PS C:\> Get-NetQosPolicy

Name           : background
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
AppPathName    : C:\Program files (x86)\backup.exe
JobObject      :
PriorityValue  : 1

Name           : Network Management
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
JobObject      :
IPProtocol     : Both
IPDstPrefix    : 10.240.1.0/24
PriorityValue  : 7

Name           : SMB Policy
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
JobObject      :
PriorityValue  : 4

```

### <a name="modify-qos-policy"></a>Ändern Sie die QoS-Richtlinie

Sie können die QoS-Richtlinien ändern, wie unten dargestellt.


```
PS C:\> Set-NetQosPolicy -Name "Network Management" -IPSrcPrefixMatchCondition 10.235.2.0/24 -IPProtocolMatchCondition both -PriorityValue8021Action 7
PS C:\> Get-NetQosPolicy

Name           : Network Management
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
JobObject      :
IPProtocol     : Both
IPSrcPrefix    : 10.235.2.0/24
IPDstPrefix    : 10.240.1.0/24
PriorityValue  : 7


```

### <a name="remove-qos-policy"></a>Entfernen Sie QoS-Richtlinie

```
PS C:\> Remove-NetQosPolicy -Name "Network Management"

Confirm
Are you sure you want to perform this action?
Remove-NetQosPolicy -Name "Network Management" -Store GPO:localhost
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): y  

```

## <a name="dcb-configuration-on-network-adapters"></a>DCB-Konfiguration für Netzwerkadapter

DCB-Konfiguration auf Netzwerkadapter ist unabhängig von der DCB-Konfiguration auf Systemebene, die oben beschriebenen. 

Unabhängig davon, ob DCB in Windows Server2016 installiert ist können Sie immer die folgenden Befehle ausführen. 

Wenn Sie DCB aus einem Switch konfigurieren und DCBX die Konfigurationen zu Netzwerkadaptern weitergegeben abhängig, können Sie überprüfen, welche Konfigurationen empfangen und auf die Netzwerkadapter von der Betriebssystem-Seite erzwungen werden, nachdem Sie DCB für die Netzwerkadapter aktivieren.

###  <a name="bkmk_enabledcb"></a>Aktivieren und Anzeigen von DCB-Einstellungen für Netzwerkadapter

```
PS C:\> Enable-NetAdapterQos M1
PS C:\> Get-NetAdapterQos

Name                       : M1
Enabled                    : True
Capabilities               :                       Hardware     Current
                                                   --------     -------
                             MacSecBypass        : NotSupported NotSupported
                             DcbxSupport         : None         None
                             NumTCs(Max/ETS/PFC) : 8/8/8        8/8/8

OperationalTrafficClasses  : TC TSA    Bandwidth Priorities
                             -- ---    --------- ----------
                              0 ETS    70%       0-3,5-7
                              1 ETS    30%       4

OperationalFlowControl     : All Priorities Disabled
OperationalClassifications : Protocol  Port/Type Priority
                             --------  --------- --------
                             Default             1


```

### <a name="disable-dcb-on-network-adapters"></a>Deaktivieren Sie DCB für Netzwerkadapter

```
PS C:\> Disable-NetAdapterQos M1
PS C:\> Get-NetAdapterQos M1

Name         : M1
Enabled      : False
Capabilities :                       Hardware     Current
                                     --------     -------
               MacSecBypass        : NotSupported NotSupported
               DcbxSupport         : None         None
               NumTCs(Max/ETS/PFC) : 8/8/8        0/0/0  

```
## <a name="bkmk_wps"></a>Windows PowerShell-Befehle für DCB

Es gibt DCB Windows PowerShell-Befehle für Windows Server2016 und Windows Server2012 R2. Sie können alle Befehle für Windows Server2012 R2 in Windows Server2016 verwenden.

### <a name="windows-server-2016-windows-powershell-commands-for-dcb"></a>Windows Server2016 Windows PowerShell-Befehle für DCB

Im folgende Thema für Windows Server2016 enthält Windows PowerShell-Cmdlet-Beschreibungen und Syntax für alle Data Center Bridging \(DCB\) Quality of Service \ \-specific-Cmdlets (QoS\). Es werden die Cmdlets in alphabetischer Reihenfolge basierend auf dem Verb am Anfang des Cmdlets.

- [DcbQoS-Modul](https://technet.microsoft.com/itpro/powershell/windows/dcbqos/dcbqos)

### <a name="windows-server-2012-r2-windows-powershell-commands-for-dcb"></a>Windows Server2012 R2 Windows PowerShell-Befehle für DCB

Im folgende Thema für Windows Server2012 R2 enthält Windows PowerShell-Cmdlet-Beschreibungen und Syntax für alle Data Center Bridging \(DCB\) Quality of Service \ \-specific-Cmdlets (QoS\). Es werden die Cmdlets in alphabetischer Reihenfolge basierend auf dem Verb am Anfang des Cmdlets.

- [Data Center Bridging (DCB) Quality of Service (QoS)-Cmdlets in WindowsPowerShell](https://technet.microsoft.com/library/hh967440.aspx)
