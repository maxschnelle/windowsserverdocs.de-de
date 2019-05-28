---
title: Verwalten von Data Center Bridging (DCB)
description: Dieses Thema enthält Anweisungen zur Verwendung von Windows PowerShell-Befehle zum Verwalten von Data Center Bridging in Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 1575cc7c-62a7-4add-8f78-e5d93effe93f
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: daed746fe798ae253956d0977827d0e205bb8b3e
ms.sourcegitcommit: 21165734a0f37c4cd702c275e85c9e7c42d6b3cb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2019
ms.locfileid: "65034579"
---
# <a name="manage-data-center-bridging-dcb"></a>Verwalten von Data Center Bridging (DCB)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema enthält Anweisungen zur Verwendung von Windows PowerShell-Befehle zum Konfigurieren der Data Center Bridging \(DCB\) auf ein DCB\--kompatible Netzwerkkarte, die auf einem Computer installiert ist, die ausgeführt wird WindowsServer 2016 oder Windows 10.

## <a name="install-dcb-in-windows-server-2016-or-windows-10"></a>Installieren Sie DCB in WindowsServer 2016 oder Windows 10

Informationen zu den Voraussetzungen für die Verwendung und DCB installieren, finden Sie unter [installieren Sie Data Center Bridging (DCB) in Windows Server 2016 oder Windows 10](dcb-install.md).


## <a name="dcb-configurations"></a>DCB-Konfigurationen 

Vor Windows Server 2016 wurde die gesamte DCB-Konfiguration universell für alle Netzwerkadapter angewendet, die DCB unterstützt. 

Sie können in Windows Server 2016 DCB Konfigurationen anwenden, entweder auf die globale Richtlinie Store oder auf einzelne Richtlinie Store\(s\). Wenn einzelne Richtlinien angewendet werden, überschreiben sie alle globalen Richtlinieneinstellungen.

Die Konfigurationen der Zuweisung Datenverkehr-Klasse, die PCF und die Anwendung der Priorität auf Systemebene wird nicht auf Netzwerkadapter angewendet, bis Sie die folgenden Schritte ausführen.

1. Aktivieren Sie das Bit DCBX bereit, auf "false"

2. Aktivieren Sie DCB für die Netzwerkadapter an. Finden Sie unter [aktivieren und Anzeigen von DCB-Einstellungen auf den Netzwerkadaptern](#bkmk_enabledcb).

>[!NOTE]
>Wenn Sie einen Switch über DCBX DCB konfigurieren möchten, finden Sie unter [DCBX Einstellungen](#dcb-configuration-on-network-adapters).

Das DCBX bereit Bit ist in der DCB-Spezifikation beschrieben. Wenn das Bit bereit, auf einem Gerät festgelegt ist, auf "true", das Gerät ist bereit, die Konfigurationen von einem Remotegerät über DCBX zu übernehmen. Wenn Bits auf einem Gerät bereit, die auf "false" festgelegt ist, wird das Gerät alle Versuche der Konfiguration von Remotegeräten ablehnen und nur die lokalen Konfigurationen zu erzwingen.

Wenn DCB nicht in Windows Server 2016 installiert ist ist der Wert des Bits bereit irrelevant, soweit es das Betriebssystem betrifft, da das Betriebssystem keine lokalen Einstellungen, die auf Netzwerkadapter angewendet wurde. Nach der Installation von DCB gilt der Standardwert des Bits bereit. Dieser Entwurf ermöglicht Netzwerkadaptern, um alle Konfigurationen zu halten, sie möglicherweise von ihren Remotepeers erhalten haben.

Wenn ein Netzwerkadapter DCBX unterstützt, erhält es nie Konfigurationen von einem Remotegerät. Konfigurationen auch vom Betriebssystem empfangen, aber erst nach der DCBX bereit Bit auf "false" festgelegt ist.

## <a name="set-the-willing-bit"></a>Legen Sie das Bit bereit

Zum Erzwingen von Betriebssystemkonfigurationen der Datenverkehrsklasse PCF und Priorität der anwendungszuweisung auf den Netzwerkadaptern, oder die Konfigurationen von Remotegeräten einfach überschreiben \ – sofern vorhanden \ – Sie können den folgenden Befehl ausführen.

>[!NOTE]
>DCB Windows PowerShell-Befehlsnamen enthalten "QoS" anstelle von "DCB" in der Zeichenfolge. Dies ist in Windows Server 2016 bieten eine nahtlose Benutzeroberfläche für die QoS-QoS und DCB integriert sind.

    
    Set-NetQosDcbxSetting -Willing $FALSE
    
    Confirm
    Are you sure you want to perform this action?
    Set-NetQosDcbxSetting -Willing $false
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"):
    

Um die Anzeige des Status des bereit Bits festlegen können Sie den folgenden Befehl aus:

    
    Get-NetQosDcbxSetting
    
    Willing PolicySetIfIndex IfAlias
    ------- ---------------- -------
    False   Global  
    

## <a name="dcb-configuration-on-network-adapters"></a>DCB-Konfiguration auf den Netzwerkadaptern

Aktivieren DCB für einen Netzwerkadapter, können Sie die Konfiguration von einem Switch auf den Netzwerkadapter übermittelt, finden Sie unter.

DCB-Konfigurationen enthalten die folgenden Schritte aus.

1.  Konfigurieren Sie DCB-Einstellungen auf Systemebene, darunter:

    a. Verwaltung des Datenverkehrs-Klasse
    
    b. Prioritätseinstellungen für Flow-Steuerelement (PCF)
    
    c. Priorität der Anwendungszuweisung
    
    d. DCBX-Einstellungen

2. Konfigurieren Sie DCB für den Netzwerkadapter an.



##  <a name="dcb-traffic-class-management"></a>Datenverkehrsklasse DCB-Verwaltung

Windows PowerShell-Beispielbefehle für die Verwaltung des Traffic Class "folgen".

### <a name="create-a-traffic-class"></a>Erstellen Sie eine Datenverkehrsklasse

Können Sie die **New-NetQosTrafficClass** Befehl aus, um eine Datenverkehrsklasse zu erstellen.

    
    New-NetQosTrafficClass -Name SMB -Priority 4 -BandwidthPercentage 30 -Algorithm ETS
    
    Name Algorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ---- --------- ------------ -------- ---------------- -------
    SMB  ETS   30   4Global
      

Standardmäßig werden alle 802. 1p-Werte auf eine Klasse standardmäßig Datenverkehr zugeordnet, die 100 % der Bandbreite der physischen Verknüpfung hat. Die **New-NetQosTrafficClass** Befehl erstellt eine neue Datenverkehrsklasse, auf welche jedes Paket, die mit der 802. 1p-Priorität gekennzeichnet ist 4 Wert zugeordnet ist. Die Übertragung Auswahlalgorithmus \(TSA\) ETS und 30 % der Bandbreite.

Sie können bis zu 7 neue Klassen erstellen. Einschließlich der standardmäßigen Datenverkehr-Klasse darf es nur maximal 8 Datenverkehrsklassen im System. Ein DCB-fähiger Netzwerkadapter unterstützen jedoch nicht, dass viele Klassen in der Hardware Datenverkehr. Wenn Sie weitere Klassen als auf einem Netzwerkadapter untergebracht werden kann und Sie DCB für diesen Netzwerkadapter aktivieren, meldet der Miniporttreiber einen Fehler für das Betriebssystem an. Der Fehler wird im Ereignisprotokoll protokolliert.

Die Summe aus der bandbreitenreservierungen für alle erstellten Datenverkehrsklassen darf 99 % der Bandbreite nicht überschreiten. Die Standardklasse für den Datenverkehr verfügt immer über mindestens 1 % an die Bandbreite, die für sich selbst reserviert.

### <a name="display-traffic-classes"></a>Anzeige Datenverkehrsklassen

Sie können die **Get-NetQosTrafficClass** Befehl zum Anzeigen von Klassen.

    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   70   0-3,5-7  Global
    SMB ETS   30   4Global  
    
### <a name="modify-a-traffic-class"></a>Ändern Sie eine Datenverkehrsklasse

Können Sie die **Set-NetQosTrafficClass** Befehl aus, um eine Datenverkehrsklasse zu erstellen. 

    Set-NetQosTrafficClass -Name SMB -BandwidthPercentage 50

Anschließend können Sie die **Get-NetQosTrafficClass** Befehl aus, um Einstellungen anzuzeigen.

    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   50   0-3,5-7  Global
    SMB ETS   50   4Global   
    

Nachdem Sie eine Datenverkehrsklasse erstellen, ändern Sie die Einstellungen unabhängig voneinander. Die Einstellungen, die Sie ändern können, lauten:

1. Bandbreitenzuordnung \(- BandwidthPercentage\)

2. TSA (\-Algorithmus\)

3. Priorität Zuordnung \(-Priorität\)

### <a name="remove-a-traffic-class"></a>Entfernen Sie eine Datenverkehrsklasse

Sie können die **Remove-NetQosTrafficClass** Befehl aus, um eine Datenverkehrsklasse löschen.

>[!IMPORTANT]
>Die Standardklasse für Datenverkehr kann nicht entfernt werden.


    Remove-NetQosTrafficClass -Name SMB

Anschließend können Sie die **Get-NetQosTrafficClass** Befehl aus, um Einstellungen anzuzeigen.
    
    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   100  0-7  Global
    

Wenn Sie eine Datenverkehrsklasse entfernen, zugeordnet der 802. 1p-Wert, dass die Standardklasse für Datenverkehr Datenverkehrsklasse zugeordnet ist. Bandbreite, die für eine Datenverkehrsklasse reserviert wurde wird an die standardzuweisung für Datenverkehr-Klasse zurückgegeben, wenn die Datenverkehrsklasse entfernt wird.

## <a name="per-network-interface-policies"></a>Pro-Network-Interface-Richtlinien

Globale Richtlinien für alle oben aufgeführten Beispiele festgelegt. Beispiele für wie festlegen und Abrufen von pro-NIC-Richtlinien. 

Das Feld "PolicySet" wird von Global zu AdapterSpecific. Wenn AdapterSpecific Richtlinien angezeigt werden, den Schnittstellenindex \(IfIndex\) und Schnittstellennamen \(IfAlias\) werden ebenfalls angezeigt.

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

Folgende werden Beispielbefehle für die Einstellungen für die flusssteuerung Priorität. Diese Einstellungen können auch für die einzelnen Adapter angegeben werden.

### <a name="enable-and-display-priority-flow-control-for-global-and-interface-specific-use-cases"></a>Aktivieren und anzeigen Priorität flusssteuerung für globale und Schnittstelle spezifischen Anwendungsfälle

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


### <a name="disable-priority-flow-control-global-and-interface-specific"></a>Deaktivieren der Flusspriorisierung (globale und spezifische Schnittstelle)

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

##  <a name="application-priority-assignment"></a>Priorität der anwendungszuweisung

Beispiele für Priorität Zuweisung.

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

Der vorherige Befehl erstellt eine neue Richtlinie für SMB. SMB – handelt es sich um ein Posteingang-Filter, der TCP-Port 445 (SMB-reserviert) übereinstimmt. Wenn ein Paket an TCP-Port 445, die es markiert wird vom Betriebssystem mit 802. 1p-Wert von 4 gesendet wird, bevor das Paket an einen Netzwerk-Miniporttreiber übergeben wird.

Zusätzlich zu SMB – enthalten andere Standardfilter – iSCSI (entsprechenden TCP-Port 3260) "," - NFS (entsprechenden TCP-Port 2049) "," --Livemigration (entsprechenden TCP-Port 6600) "," - oder FCOE (übereinstimmend EtherType 0x8906) "und" – NetworkDirect.

NetworkDirect ist eine abstrakte Ebene, die wir zur auf einem Netzwerkadapter RDMA-Implementierung zu erstellen. – NetworkDirect muss von einem Network Direct Port folgen.

Zusätzlich zu den Standard-filtern können Sie Datenverkehr von der ausführbaren Datei den Namen der Anwendung (wie das erste Beispiel unten) oder IP-Adresse, Port und Protokoll (wie im zweiten Beispiel gezeigt) klassifizieren:

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


**Nach IP-Adresse, Port oder Protokoll**

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

### <a name="remove-qos-policy"></a>Entfernen Sie die QoS-Richtlinie

```
PS C:\> Remove-NetQosPolicy -Name "Network Management"

Confirm
Are you sure you want to perform this action?
Remove-NetQosPolicy -Name "Network Management" -Store GPO:localhost
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): y  

```

## <a name="dcb-configuration-on-network-adapters"></a>DCB-Konfiguration auf den Netzwerkadaptern

DCB-Konfiguration für die Netzwerkadapter ist unabhängig von der DCB-Konfiguration auf der Systemebene, die oben beschriebenen. 

Unabhängig davon, ob DCB in Windows Server 2016 installiert ist können Sie immer die folgenden Befehle ausführen. 

Wenn Sie einen Switch DCB konfigurieren und basieren auf DCBX die Konfigurationen mit den Netzwerkadaptern weitergegeben werden, können Sie überprüfen, welche Konfigurationen empfangen und auf den Netzwerkadaptern, die aus der Betriebssystemebene erzwungen werden, nachdem Sie DCB für die Netzwerkadapter aktiviert werden.

###  <a name="bkmk_enabledcb"></a>Aktivieren und Anzeigen der DCB-Einstellungen für Netzwerkadapter

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

### <a name="disable-dcb-on-network-adapters"></a>Deaktivieren Sie DCB für die Netzwerkadapter

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

Es gibt DCB Windows PowerShell-Befehle für Windows Server 2016 und Windows Server 2012 R2. Sie können alle Befehle für Windows Server 2012 R2, Windows Server 2016 verwenden.

### <a name="windows-server-2016-windows-powershell-commands-for-dcb"></a>Windows Server 2016-Windows-PowerShell-Befehle für DCB

Im folgende Thema für Windows Server 2016 bietet Windows PowerShell-Cmdlet-Beschreibungen und Syntax für alle Data Center Bridging \(DCB\) Quality of Service \(QoS\)\--spezifische Cmdlets. Die Cmdlets werden in alphabetischer Reihenfolge (basierend auf dem Verb am Anfang des Cmdlets) aufgeführt.

- [DcbQoS-Modul](https://technet.microsoft.com/itpro/powershell/windows/dcbqos/dcbqos)

### <a name="windows-server-2012-r2-windows-powershell-commands-for-dcb"></a>Windows Server 2012 R2 Windows PowerShell-Befehle für DCB

Im folgende Thema für Windows Server 2012 R2 bietet Windows PowerShell-Cmdlet-Beschreibungen und Syntax für alle Data Center Bridging \(DCB\) Quality of Service \(QoS\)\--spezifische Cmdlets. Die Cmdlets werden in alphabetischer Reihenfolge (basierend auf dem Verb am Anfang des Cmdlets) aufgeführt.

- [Für Data Center Bridging (DCB) Quality of Service (QoS)-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/hh967440.aspx)
