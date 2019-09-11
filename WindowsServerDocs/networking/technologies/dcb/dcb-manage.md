---
title: Verwalten von Data Center Bridging (DCB)
description: Dieses Thema enthält Anweisungen zur Verwendung von Windows PowerShell-Befehlen zum Verwalten von Data Center Bridging in Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 1575cc7c-62a7-4add-8f78-e5d93effe93f
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fd6e8e5dd0bb4103011269473c3e1091739c775e
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70869796"
---
# <a name="manage-data-center-bridging-dcb"></a>Verwalten von Data Center Bridging (DCB)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Dieses Thema enthält Anweisungen zur Verwendung von Windows PowerShell-Befehlen zum Konfigurieren von Data Center Bridging \(DCB\) auf einem DCB\--kompatiblen Netzwerkadapter, der auf einem Computer installiert ist, auf dem ausgeführt wird. Windows Server 2016 oder Windows 10.

## <a name="install-dcb-in-windows-server-2016-or-windows-10"></a>Installieren von DCB in Windows Server 2016 oder Windows 10

Informationen zu den Voraussetzungen für die Verwendung von und zur Installation von DCB finden Sie unter [Installieren von Data Center Bridging (DCB) in Windows Server 2016 oder Windows 10](dcb-install.md).


## <a name="dcb-configurations"></a>DCB-Konfigurationen 

Vor Windows Server 2016 wurden alle DCB-Konfigurationen universell auf alle Netzwerkadapter angewendet, von denen DCB unterstützt wurde. 

In Windows Server 2016 können Sie DCB-Konfigurationen entweder auf den globalen Richtlinien Speicher oder auf einzelne Richtlinien Speicher\(s\)anwenden. Wenn einzelne Richtlinien angewendet werden, überschreiben Sie alle globalen Richtlinien Einstellungen.

Die Konfigurationen der Datenverkehrs Klasse, PFC und Anwendungs Prioritäts Zuweisung auf Systemebene werden erst auf Netzwerkadapter angewendet, wenn Sie die folgenden Schritte ausführen.

1. Legen Sie das dcbx-Bit auf "false"

2. Aktivieren Sie DCB auf den Netzwerkadaptern. Siehe [aktivieren und Anzeigen der DCB-Einstellungen auf Netzwerkadaptern](#bkmk_enabledcb).

>[!NOTE]
>Wenn Sie DCB von einem Switch über dcbx konfigurieren möchten, finden Sie weitere Informationen unter [dcbx-Einstellungen](#dcb-configuration-on-network-adapters).

Das dcbx-Bit ist in der DCB-Spezifikation beschrieben. Wenn das bereit zulegende Bit auf einem Gerät auf "true" festgelegt ist, ist das Gerät bereit, Konfigurationen von einem Remote Gerät über dcbx zu akzeptieren. Wenn das bereit zulegende Bit auf einem Gerät auf false festgelegt ist, lehnt das Gerät alle Konfigurations Versuche von Remote Geräten ab und erzwingt nur die lokalen Konfigurationen.

Wenn DCB in Windows Server 2016 nicht installiert ist, ist der Wert des bereit zustellenden Bits unerheblich, da das Betriebssystem über keine lokalen Einstellungen für Netzwerkadapter verfügt. Nachdem DCB installiert wurde, ist der Standardwert des bereit gestellenden Bits "true". Dieser Entwurf ermöglicht es Netzwerkadaptern, alle Konfigurationen beizubehalten, die Sie möglicherweise von ihren Remote Peers erhalten haben.

Wenn dcbx von einem Netzwerkadapter nicht unterstützt wird, werden keine Konfigurationen von einem Remote Gerät empfangen. Er empfängt Konfigurationen vom Betriebssystem, aber erst nach dem Festlegen des dcbx-Bits mit dem Wert "false".

## <a name="set-the-willing-bit"></a>Festlegen des bereit zulegenden Bits

Führen Sie den folgenden Befehl aus, um Betriebs Systemkonfigurationen der Datenverkehrs Klasse, der PFC-Zuweisung und der Anwendungs Prioritäts Zuweisung auf Netzwerkadaptern zu erzwingen oder um die Konfigurationen von Remote Geräten – zu überschreiben.

>[!NOTE]
>DCB Windows PowerShell-Befehlsnamen enthalten "QoS" anstelle von "DCB" in der namens Zeichenfolge. Dies liegt daran, dass QoS und DCB in Windows Server 2016 integriert sind, um eine nahtlose QoS-Verwaltung zu ermöglichen.

    
    Set-NetQosDcbxSetting -Willing $FALSE
    
    Confirm
    Are you sure you want to perform this action?
    Set-NetQosDcbxSetting -Willing $false
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"):
    

Verwenden Sie den folgenden Befehl, um den Status der Einstellung des bereit zustellenden Bits anzuzeigen:

    
    Get-NetQosDcbxSetting
    
    Willing PolicySetIfIndex IfAlias
    ------- ---------------- -------
    False   Global  
    

## <a name="dcb-configuration-on-network-adapters"></a>DCB-Konfiguration auf Netzwerkadaptern

Wenn Sie DCB auf einem Netzwerkadapter aktivieren, können Sie sehen, dass die Konfiguration von einem Switch an den Netzwerkadapter weitergegeben wurde.

DCB-Konfigurationen umfassen die folgenden Schritte.

1.  Konfigurieren Sie DCB-Einstellungen auf Systemebene, einschließlich:

    a. Verwaltung von Datenverkehrs Klassen
    
    b. Einstellungen für die Prioritäts Fluss Steuerung (PFC)
    
    c. Zuweisung von Anwendungs Priorität
    
    d. Dcbx-Einstellungen

2. Konfigurieren Sie DCB auf dem Netzwerkadapter.



##  <a name="dcb-traffic-class-management"></a>DCB-Traffic Class-Verwaltung

Im folgenden finden Sie Beispiel Befehle für Windows PowerShell für die Verwaltung von Datenverkehrs Klassen.

### <a name="create-a-traffic-class"></a>Erstellen einer Datenverkehrs Klasse

Sie können den Befehl **New-netqostrafficclass** verwenden, um eine Datenverkehrs Klasse zu erstellen.

    
    New-NetQosTrafficClass -Name SMB -Priority 4 -BandwidthPercentage 30 -Algorithm ETS
    
    Name Algorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ---- --------- ------------ -------- ---------------- -------
    SMB  ETS   30   4Global
      

Standardmäßig werden alle 802.1 p-Werte einer Standard-Datenverkehrs Klasse zugeordnet, die 100% der Bandbreite der physischen Verbindung aufweist. Der **New-netqostrafficclass-** Befehl erstellt eine neue Datenverkehrs Klasse, der jedes Paket zugeordnet ist, das mit dem 802.1 p-Prioritätswert 4 markiert ist. Der Übertragungs Auswahl Algorithmus \(TSA\) ist ETS und hat 30% der Bandbreite.

Sie können bis zu sieben neue Datenverkehrs Klassen erstellen. Die Standard-Datenverkehrs Klasse umfasst höchstens 8 Datenverkehrs Klassen im System. Ein DCB-fähiger Netzwerkadapter unterstützt jedoch möglicherweise nicht viele Datenverkehrs Klassen in der Hardware. Wenn Sie mehr Datenverkehrs Klassen erstellen, als auf einem Netzwerkadapter untergebracht werden können, und Sie DCB auf diesem Netzwerkadapter aktivieren, meldet der Mini Port-Treiber einen Fehler an das Betriebssystem. Der Fehler wird im Ereignisprotokoll protokolliert.

Die Summe der Bandbreiten Reservierungen für alle erstellten Datenverkehrs Klassen darf 99% der Bandbreite nicht überschreiten. Die Standard-Datenverkehrs Klasse hat immer mindestens 1% der Bandbreite, die für sich selbst reserviert ist.

### <a name="display-traffic-classes"></a>Anzeigen von Datenverkehrs Klassen

Sie können den Befehl **Get-netqostrafficclass** verwenden, um Datenverkehrs Klassen anzuzeigen.

    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   70   0-3,5-7  Global
    SMB ETS   30   4Global  
    
### <a name="modify-a-traffic-class"></a>Ändern einer Datenverkehrs Klasse

Sie können den Befehl **Set-netqostrafficclass** verwenden, um eine Datenverkehrs Klasse zu erstellen. 

    Set-NetQosTrafficClass -Name SMB -BandwidthPercentage 50

Sie können dann den Befehl **Get-netqostrafficclass** verwenden, um Einstellungen anzuzeigen.

    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   50   0-3,5-7  Global
    SMB ETS   50   4Global   
    

Nachdem Sie eine Datenverkehrs Klasse erstellt haben, können Sie Ihre Einstellungen unabhängig voneinander ändern. Folgende Einstellungen können Sie ändern:

1. Bandbreiten \(Zuordnung-bandwidthprozentsatz\)

2. TSA (\-Algorithmus\)

3. Prioritäts \(Zuordnung-Priorität\)

### <a name="remove-a-traffic-class"></a>Entfernen einer Datenverkehrs Klasse

Sie können den Befehl **Remove-netqostrafficclass** verwenden, um eine Datenverkehrs Klasse zu löschen.

>[!IMPORTANT]
>Die Standard-Datenverkehrs Klasse kann nicht entfernt werden.


    Remove-NetQosTrafficClass -Name SMB

Sie können dann den Befehl **Get-netqostrafficclass** verwenden, um Einstellungen anzuzeigen.
    
    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   100  0-7  Global
    

Nachdem Sie eine Datenverkehrs Klasse entfernt haben, wird der 802.1 p-Wert, der dieser Datenverkehrs Klasse zugeordnet ist, der Standard-Traffic-Klasse zugeordnet. Jede Bandbreite, die für eine Datenverkehrs Klasse reserviert war, wird beim Entfernen der Traffic-Klasse an die standardmäßige Zuordnung von Datenverkehrs Klassen zurückgegeben.

## <a name="per-network-interface-policies"></a>Netzwerkschnittstellen Richtlinien

Alle oben aufgeführten Beispiele legen globale Richtlinien fest. Im folgenden finden Sie Beispiele dafür, wie Sie pro-NIC-Richtlinien festlegen und erhalten können. 

Das Feld "policyset" ändert sich von Global in adapterspecific. Wenn adapterspecific-Richtlinien angezeigt werden, werden \(der Schnittstellen Index\) ifindex \(und der\) Schnittstellen Name ifalias ebenfalls angezeigt.

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

## <a name="priority-flow-control-settings"></a>Einstellungen für die Prioritäts Fluss Steuerung:

Im folgenden finden Sie Befehlsbeispiele für Einstellungen der Prioritäts Fluss Steuerung. Diese Einstellungen können auch für einzelne Adapter angegeben werden.

### <a name="enable-and-display-priority-flow-control-for-global-and-interface-specific-use-cases"></a>Aktivieren und Anzeigen der Prioritäts Fluss Steuerung für globale und Schnittstellen spezifische Anwendungsfälle

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


### <a name="disable-priority-flow-control-global-and-interface-specific"></a>Deaktivieren der Prioritäts Fluss Steuerung (Global und Interface Specific)

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

##  <a name="application-priority-assignment"></a>Zuweisung von Anwendungs Priorität

Im folgenden finden Sie Beispiele für die Prioritäts Zuweisung.

### <a name="create-qos-policy"></a>Erstellen einer QoS-Richtlinie

```
PS C:\> New-NetQosPolicy -Name "SMB Policy" -PriorityValue8021Action 4

Name           : SMB Policy
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
JobObject      :
PriorityValue  : 4

```

Mit dem vorherigen Befehl wird eine neue Richtlinie für SMB erstellt. – SMB ist ein Posteingangs Filter, der TCP-Port 445 (reserviert für SMB) entspricht. Wenn ein Paket an den TCP-Port 445 gesendet wird, wird es vom Betriebssystem mit dem 802.1 p-Wert 4 gekennzeichnet, bevor das Paket an einen Netzwerk-Mini Port-Treiber übermittelt wird.

Neben – SMB enthalten andere Standardfilter – iSCSI (übereinstimmender TCP-Port 3260),-NFS (übereinstimmender TCP-Port 2049),-Livemigration (übereinstimmender TCP-Port 6600),-FCoE (übereinstimmender EtherType 0x8906) und – networkdirect.

Networkdirect ist eine abstrakte Ebene, die auf jeder RDMA-Implementierung auf einem Netzwerkadapter erstellt wird. Auf – networkdirect muss ein direkter Netzwerkport folgen.

Zusätzlich zu den Standardfiltern können Sie den Datenverkehr nach dem ausführbaren Namen der Anwendung (wie im ersten Beispiel unten) oder nach IP-Adresse, Port oder Protokoll (wie im zweiten Beispiel dargestellt) klassifizieren:

**Name der ausführbaren Datei**

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


**Nach IP-Adressport oder-Protokoll**

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

### <a name="display-qos-policy"></a>Anzeigen der QoS-Richtlinie

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

### <a name="modify-qos-policy"></a>Ändern der QoS-Richtlinie

Die QoS-Richtlinien können wie unten dargestellt geändert werden.


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

### <a name="remove-qos-policy"></a>QoS-Richtlinie entfernen

```
PS C:\> Remove-NetQosPolicy -Name "Network Management"

Confirm
Are you sure you want to perform this action?
Remove-NetQosPolicy -Name "Network Management" -Store GPO:localhost
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): y  

```

## <a name="dcb-configuration-on-network-adapters"></a>DCB-Konfiguration auf Netzwerkadaptern

Die DCB-Konfiguration auf Netzwerkadaptern ist unabhängig von der DCB-Konfiguration auf der oben beschriebenen Systemebene. 

Unabhängig davon, ob DCB in Windows Server 2016 installiert ist, können Sie immer die folgenden Befehle ausführen. 

Wenn Sie DCB von einem Switch aus konfigurieren und dcbx für die Weitergabe der Konfigurationen an Netzwerkadapter einsetzen, können Sie nach der Aktivierung von DCB auf den Netzwerkadaptern prüfen, welche Konfigurationen auf den Netzwerkadaptern empfangen und erzwungen werden.

###  <a name="bkmk_enabledcb"></a>Aktivieren und Anzeigen von DCB-Einstellungen auf Netzwerkadaptern

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

### <a name="disable-dcb-on-network-adapters"></a>Deaktivieren von DCB auf Netzwerkadaptern

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

Es gibt DCB-Windows PowerShell-Befehle für Windows Server 2016 und Windows Server 2012 R2. Sie können alle Befehle für Windows Server 2012 R2 in Windows Server 2016 verwenden.

### <a name="windows-server-2016-windows-powershell-commands-for-dcb"></a>Windows Server 2016 Windows PowerShell-Befehle für DCB

Im folgenden Thema für Windows Server 2016 finden Sie Windows PowerShell-Cmdlet-Beschreibungen und Syntax für alle \(Data Center\) Bridging \(DCB\)Quality of Service QoS\--spezifischen Cmdlets. Die Cmdlets werden in alphabetischer Reihenfolge (basierend auf dem Verb am Anfang des Cmdlets) aufgeführt.

- [Dcbqos-Modul](https://technet.microsoft.com/itpro/powershell/windows/dcbqos/dcbqos)

### <a name="windows-server-2012-r2-windows-powershell-commands-for-dcb"></a>Windows Server 2012 R2 Windows PowerShell-Befehle für DCB

Im folgenden Thema für Windows Server 2012 R2 finden Sie Windows PowerShell-Cmdlet-Beschreibungen und Syntax für alle \(Data Center\) Bridging \(DCB\)Quality of Service QoS\--spezifischen Cmdlets. Die Cmdlets werden in alphabetischer Reihenfolge (basierend auf dem Verb am Anfang des Cmdlets) aufgeführt.

- [Cmdlets für Data Center Bridging (DCB) Quality of Service (QoS) in Windows PowerShell](https://technet.microsoft.com/library/hh967440.aspx)
