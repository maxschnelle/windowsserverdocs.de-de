---
title: Remotezugriff auf den direkten Speicher (RDMA) und Switch Embedded Teaming (SET)
description: Dieses Thema enthält Informationen zum Konfigurieren von-Schnittstellen (Remote Direct Memory Access, RDMA) mit Hyper-V in Windows Server 2016 sowie Informationen zu Switch Embedded Teaming (SET).
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: 68c35b64-4d24-42be-90c9-184f2b5f19be
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c945144194ac86623bfa8ce60a306f0202df0874
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881661"
---
# <a name="remote-direct-memory-access-rdma-and-switch-embedded-teaming-set"></a>Remote Direct Memory Access \(RDMA\) und Switch Embedded Teaming \(festlegen\)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema enthält Informationen zum Konfigurieren von Remote Direct Memory Access \(RDMA\) Schnittstellen mit Hyper-V in Windows Server 2016 verwenden darüber hinaus, um Informationen zu Switch Embedded Teaming \(festgelegt\).  

> [!NOTE]
> Zusätzlich zu diesem Thema wird Folgendes Switch Embedded Teaming verfügbar. 
> - TechNet Gallery herunterladen: [Windows Server 2016-NIC und Switch Embedded Teaming-Benutzerhandbuch](https://gallery.technet.microsoft.com/Windows-Server-2016-839cb607?redir=0)

## <a name="bkmk_rdma"></a>Konfigurieren von RDMA-Schnittstellen mit Hyper-V  

In Windows Server 2012 R2 verwenden sowohl "RDMA" und "Hyper-V auf dem gleichen Computer wie den Netzwerkadaptern, die angeben, dass die RDMA-Dienste nicht mit einem virtuellen Hyper-V-Switch gebunden werden können. Dies erhöht die Anzahl der physischen Netzwerkadapter, die erforderlich sind, auf dem Hyper-V-Host installiert werden.

>[!TIP]
>In Windows Server vor Windows Server 2016-Editionen ist es nicht möglich, so konfigurieren Sie RDMA auf den Netzwerkadaptern, die auf einem NIC-Team oder mit einem virtuellen Hyper-V-Switch gebunden sind. In Windows Server 2016 können Sie RDMA auf den Netzwerkadaptern aktivieren, die mit einem virtuellen Hyper-V-Switch mit oder ohne festgelegte gebunden sind.

In Windows Server 2016 können Sie weniger Netzwerkadapter verwenden, bei der Verwendung von RDMA mit oder ohne festgelegte.

Die folgende Abbildung veranschaulicht die Architektur softwareänderungen zwischen Windows Server 2012 R2 und Windows Server 2016.

![Änderungen an der Architektur](../media/RDMA-and-SET/rdma_over.jpg)

Die folgenden Abschnitte enthalten Anweisungen für die Verwendung von Windows PowerShell-Befehle zum Aktivieren der Data Center Bridging (DCB) erstellen einen virtuellen Hyper-V-Switch mit einer virtuellen RDMA-Netzwerkkarte \(vNIC\), und erstellen Sie einen virtuellen Hyper-V-Switch mit SET und RDMA-vNICs.

### <a name="enable-data-center-bridging-dcb"></a>Aktivieren von Data Center Bridging \(DCB\)

Vor der Verwendung von jedem RDMA over Converged Ethernet \(RoCE\) Version von RDMA, müssen Sie DCB aktivieren.  Zwar nicht erforderlich für Wide Area RDMA Internetprotokoll \(iWARP\) Netzwerken testen festgestellt, dass alle RDMA Ethernet-basierten Technologien besser mit DCB funktioniert. Aus diesem Grund sollten Sie DCB verwenden, auch für iWARP RDMA-Bereitstellungen.

Die folgenden Windows PowerShell-Beispielbefehle veranschaulichen das Aktivieren und konfigurieren DCB für SMB Direct.

Aktivieren Sie DCB

    Install-WindowsFeature Data-Center-Bridging

Legen Sie eine Richtlinie für SMB Direct an:

    New-NetQosPolicy "SMB" -NetDirectPortMatchCondition 445 -PriorityValue8021Action 3

Aktivieren Sie die flusssteuerung für SMB:

    Enable-NetQosFlowControl  -Priority 3

Stellen Sie sicher, dass die flusssteuerung für den übrigen Datenverkehr deaktiviert ist:

    Disable-NetQosFlowControl  -Priority 0,1,2,4,5,6,7

Richtlinie wird auf die Zieladapter anwenden:

    Enable-NetAdapterQos  -Name "SLOT 2"

Weisen Sie SMB Direct 30 % der minimalen Bandbreite:

`New-NetQosTrafficClass "SMB"  -Priority 3  -BandwidthPercentage 30  -Algorithm ETS`  

Wenn Sie einen Kerneldebugger im System installiert haben, müssen Sie den Debugger, um QoS festgelegt werden, mithilfe des folgenden Befehls ermöglichen konfigurieren.

Überschreiben den Debugger – in der Standardeinstellung blockiert des Debuggers NetQos:
 
    Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 -Force

### <a name="create-a-hyper-v-virtual-switch-with-an-rdma-vnic"></a>Erstellen Sie einen virtuellen Hyper-V-Switch mit einer RDMA vNIC

Wenn SET nicht für die Bereitstellung erforderlich ist, können Sie die folgenden Windows PowerShell-Befehle, um einen virtuellen Hyper-V-Switch mit einer RDMA vNIC zu erstellen.

> [!NOTE]
> Verwenden SET-Teams mit RDMA-fähigen physischen NICs bietet mehr RDMA-Ressourcen für die vNICs zu nutzen.

    New-VMSwitch -Name RDMAswitch -NetAdapterName "SLOT 2"

Fügen Sie Host-vNICs hinzu, und stellen sie RDMA kann:

    Add-VMNetworkAdapter -SwitchName RDMAswitch -Name SMB_1
    Enable-NetAdapterRDMA "vEthernet (SMB_1)" "SLOT 2"

Überprüfen Sie die RDMA-Funktionen:

    Get-NetAdapterRdma

###  <a name="bkmk_set-rdma"></a>Erstellen Sie einen virtuellen Hyper-V-Switch mit SET und RDMA-vNICs

Zum Verwenden von RDMA hosten Capabilies auf Hyper-V virtuelle Netzwerkadapter \(vNICs\) auf einem virtuellen Hyper-V-Switch, der werden Teamvorgänge RDMA unterstützt, können Sie diese Beispiel-Windows PowerShell-Befehle.

    New-VMSwitch -Name SETswitch -NetAdapterName "SLOT 2","SLOT 3" -EnableEmbeddedTeaming $true

Fügen Sie Host-vNICs hinzu:

    Add-VMNetworkAdapter -SwitchName SETswitch -Name SMB_1 -managementOS
    Add-VMNetworkAdapter -SwitchName SETswitch -Name SMB_2 -managementOS

Viele Switches wird nicht übergeben nicht markierten Datenverkehr für VLAN-Klasseninformationen zum Datenverkehr, also stellen Sie sicher, dass die Host-Adapter für RDMA auf VLANs befinden. Dieses Beispiel weist zwei SMB_ * virtuellen Host-Adapter auf VLAN-42.
    
    Set-VMNetworkAdapterIsolation -ManagementOS -VMNetworkAdapterName SMB_1  -IsolationMode VLAN -DefaultIsolationID 42
    Set-VMNetworkAdapterIsolation -ManagementOS -VMNetworkAdapterName SMB_2  -IsolationMode VLAN -DefaultIsolationID 42
    

Aktivieren Sie RDMA auf dem Host-vNICs:

    Enable-NetAdapterRDMA "vEthernet (SMB_1)","vEthernet (SMB_2)" "SLOT 2", "SLOT 3"

Überprüfen Sie die RDMA-Funktionen; Stellen Sie sicher, dass die Funktionen einen Wert ungleich sind:

    Get-NetAdapterRdma | fl *


## <a name="bkmk_sswitchembedded"></a>Switch Embedded Teaming (SET)  

Dieser Abschnitt enthält eine Übersicht über der Switch Embedded Teaming (SET) in Windows Server 2016, und enthält die folgenden Abschnitte.

- [Übersicht über](#bkmk_over)

- [SET-Verfügbarkeit](#bkmk_avail)

- [Unterstützte und nicht unterstützten Netzwerkkarten für Gruppe](#bkmk_nics)

- [Legen Sie die Kompatibilität mit Windows Server Networking-Technologien](#bkmk_compat)

- [SET-Modi und Einstellungen](#bkmk_modes)

- [Gruppe und Warteschlangen für virtuelle Computer (Vmq)](#bkmk_vmq)

- [Gruppe und Hyper-V-Netzwerkvirtualisierung (HNV)](#bkmk_hnv)

- [Festlegen und Live-Migration](#bkmk_live)

- [Verwendung der MAC-Adresse in gesendeten Paketen](#bkmk_mac)

- [Verwalten von einem SET-team](#bkmk_manage)

## <a name="bkmk_over"></a>Übersicht über

Ist eine alternative Lösung NIC-Teamvorgang, mit denen Sie in Umgebungen, die Hyper-V und der Software Defined Networking enthalten \(SDN\) -Stapel in Windows Server 2016. SET integriert einige Funktionen mit NIC-Teamvorgang in den virtuellen Hyper-V-Switch.

Satz ermöglicht Ihnen, zwischen einem und acht physische Ethernet-Netzwerkadapter in ein oder mehrere softwarebasierte virtuelle Netzwerkadapter zu gruppieren. Diese virtuellen Netzwerkadapter bieten schnelle Leistung und Fehlertoleranz bei Ausfall eines Netzwerkadapters.

SET-Member-Netzwerkadapter müssen alle in dem gleichen physischen Hyper-V-Host in einem Team platziert werden installiert.

> [!NOTE]
> Die Verwendung von SET wird nur im virtuellen Hyper-V-Switch unter Windows Server 2016 unterstützt. Sie können keine Gruppe in Windows Server 2012 R2 bereitstellen.

Sie können Ihre Teaming-fähigen Netzwerkkarten auf demselben physischen Switch oder mit verschiedenen physischen Switches verbinden. Wenn Sie Netzwerkkarten mit verschiedenen Switches verbunden sind, müssen beide Schalter im gleichen Subnetz sein.

Die folgende Abbildung zeigt die SET-Architektur.

![SET-Architektur](../media/RDMA-and-SET/set_architecture.jpg)

Da SET in den virtuellen Hyper-V-Switch integriert ist, sind Sie nicht, Satz innerhalb eines virtuellen Computers (VM) verwenden. Sie können jedoch die NIC-Teamvorgang auf virtuellen Computern verwenden.

Weitere Informationen finden Sie unter [NIC-Teamvorgang auf virtuellen Computern (VMs)](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nict-vms).

Darüber hinaus macht teamschnittstellen von SET-Architektur nicht verfügbar. Stattdessen müssen Sie virtuelle Hyper-V-Switchports konfigurieren.

## <a name="bkmk_avail"></a>SET-Verfügbarkeit

SET ist verfügbar in allen Versionen von Windows Server 2016, die Hyper-V und den SDN-Stapel enthalten. Darüber hinaus können Sie Windows PowerShell-Befehle und Herstellen von Remotedesktopverbindungen von Remotecomputern verwalten, die ein Clientbetriebssystem ausgeführt werden, auf denen die Tools unterstützt werden.

## <a name="bkmk_nics"></a>Unterstützten Netzwerkkarten für Gruppe

Können Sie eine beliebige Ethernet-NIC, die die Qualifikation für Windows-Hardware und das Logo vergangen ist \(WHQL\) in einem SET-Team in Windows Server 2016 zu testen. SET ist erforderlich, dass alle Netzwerkadapter, die Mitglieder eines Teams Satz sind identisch sein müssen, \(z. B. gleichen Hersteller, demselben Modell, gleichen Firmware und Treiber\). Zwischen einer und acht Netzwerkadapter in einem Team unterstützt.
  
## <a name="bkmk_compat"></a>Legen Sie die Kompatibilität mit Windows Server Networking-Technologien

SET ist mit den folgenden netzwerktechnologien in Windows Server 2016 kompatibel.

- Datacenter bridging \(DCB\)
  
- Hyper-V-Netzwerkvirtualisierung – NV-GRE und VxLAN werden sowohl in Windows Server 2016 unterstützt.  
- Empfangsseitige Prüfsumme abladungen \(IPv4, IPv6 und TCP-\) – diese werden unterstützt, wenn keines der Teammitglieder der Gruppe diese unterstützt.

- Remote Direct Memory Access \(RDMA\)

- Virtualisierung mit einzelstamm e/a \(SR-IOV\)

- Übertragen clientseitigen Prüfsumme abladungen \(IPv4, IPv6 und TCP-\) – diese werden unterstützt, wenn alle der Gruppe Teammitglieder diese unterstützt.

- VM-Warteschlangen \(VMQ\)

- Virtuelle empfangsseitige Skalierung \(RSS\)

Satz ist nicht mit den folgenden netzwerktechnologien in Windows Server 2016 kompatibel.

- 802.1 X Authentifizierung. 802.1 x Extensible Authentication Protocol \(EAP\) Pakete werden automatisch gelöscht, indem Hyper\-V-Switch unter Szenarien.
 
- IPsec-Aufgabenverlagerung \(IPsecTO\). Dies ist eine veraltete Technologie, die von den meisten Netzwerkadapter unterstützt wird, und, in dem sie vorhanden ist, ist es standardmäßig deaktiviert.

- Verwenden von QoS \(pacer.exe\) im systemeigenen Betriebssystem oder Host. Diese QoS-Szenarios sind nicht Hyper\-V-Szenarien, damit die Technologien nicht überschneiden. Darüber hinaus QoS ist verfügbar, aber nicht standardmäßig aktiviert – müssen Sie absichtlich QoS aktivieren.

- Empfangen von Side coalescing \(RSC\). RSC wird automatisch deaktiviert, indem Hyper\-V-Switches.

- Empfangsseitige Skalierung \(RSS\). Da Hyper-V die Warteschlangen für VMQ und VMMQ verwendet wird, ist RSS immer deaktiviert, wenn Sie einen virtuellen Switch erstellen.

- TCP-Chimney-Abladung. Diese Technologie ist standardmäßig deaktiviert.

- VM-QoS \(VM-QoS-\). VM-QoS ist verfügbar, aber standardmäßig deaktiviert. Wenn Sie VM-QoS in einer SET-Umgebung konfigurieren, werden die QoS-Einstellungen zu unvorhersehbaren Ergebnissen führen.

## <a name="bkmk_modes"></a>SET-Modi und Einstellungen

Im Gegensatz zu den NIC-Teamvorgang bei der Erstellung einer SET-Team, können nicht konfigurieren Sie ein Teamname. Darüber hinaus mit einem standby-Adapter wird in der NIC-Teamvorgang unterstützt, aber in der Gruppe wird nicht unterstützt. Wenn Sie eine Gruppe bereitstellen, alle Netzwerkadapter sind aktiv, und keine sind im Standbymodus befindet.

Eine andere Hauptunterschied zwischen der NIC-Teamvorgang und ist, dass es sich bei NIC-Teamvorgang stellt drei verschiedene teaming-Modi, während SET nur unterstützt **Switchunabhängig** Modus. Switchunabhängig-Modus oder den Optionen, die Mitglieder des Teams festlegen verbunden sind, nicht davon, ob das SET-Team-fähig sind, und bestimmen nicht die Verteilung des Netzwerkdatenverkehrs TEAMMITGLIEDER – stattdessen das SET-Team eingehenden Netzwerk verteilt Datenverkehr in der Gruppe Teammitglieder.

Wenn Sie ein neues Team für die Gruppe erstellen, müssen Sie die folgenden Eigenschaften für die Team konfigurieren.

- Mitgliederadapter

- Lastenausgleichsmodus

### <a name="member-adapters"></a>Mitgliederadapter

Wenn Sie ein SET-Team erstellen, müssen Sie bis zu acht identische Netzwerkadapter angeben, die mit dem virtuellen Hyper-V-Switch als Satz Team mitgliederadapter gebunden sind.

### <a name="load-balancing-mode"></a>-Lademodus für Lastenausgleich

Die Optionen für die Gruppe team des Lastenausgleichs-Verteilungsmodus sind **Hyper-V-Port** und **dynamische**.

**Hyper-V-Port**

VMs werden mit einem Port auf dem virtuellen Hyper-V-Switch verbunden. Bei Verwendung der Hyper-V-Port im Modus für SET-Teams werden Port des virtuellen Hyper-V-Switches und die zugeordnete MAC-Adresse verwendet, um den Netzwerkdatenverkehr zwischen der Gruppe Teammitglieder unterteilen.

> [!NOTE]
> Bei Verwendung von SET in Verbindung mit Packetdirect, den teamvorgangsmodus **Switchunabhängig** und der Modus für den Lastenausgleich **Hyper-V-Port** erforderlich sind.

Da der benachbarte Switch immer eine bestimmte MAC-Adresse auf einem bestimmten Port erkennt, verteilt der Switch die eingehende Last (der Datenverkehr vom Switch zum Host) an den Port auf dem sich die MAC-Adresse befindet. Dies ist besonders nützlich, wenn Warteschlangen für virtuelle Computer (Vmq) verwendet werden, weil eine Warteschlange für die bestimmten Netzwerkschnittstellenkarte platziert werden kann, in denen der Datenverkehr erwartet wird, auf das eintreffen.

Allerdings verfügt der Host nur wenige virtuelle Computer, in diesem Modus präzise genug, um eine ausgewogene Verteilung zu erreichen möglicherweise nicht. In diesem Modus wird immer einen einzelnen virtuellen Computer (d. h. der Datenverkehr von einem einzigen Switch-Port) auf die Bandbreite beschränkt, die auf einer einzelnen Schnittstelle verfügbar ist.

**Dynamic**

Dieser Lastenausgleich Load-Modus bietet die folgenden Vorteile.

- Ausgehende lädt werden auf Grundlage des Hashs der TCP-Ports und IP-Adressen verteilt.  Im dynamischen Modus verteilt neu außerdem lädt in Echtzeit, damit eine angegebene ausgehenden Datenfluss zwischen Teammitgliedern Satz hin und her wechseln kann.

- Eingehende Laden werden in die gleiche Weise wie der Hyper-V-portmodus verteilt.

Die ausgehende lädt in diesem Modus werden dynamisch basierend auf dem Konzept von Flowlets ausgeglichen. Genau wie der menschliche Stimme natürliche datenbrüche an den Enden der Wörter und Sätze verfügt, müssen TCP-Flüsse (TCP-kommunikationsstreams) auch vorkommende unterbrochen. Der Teil einer TCP-Datenflusses zwischen zwei solchen Unterbrechungen wird als eine Flowlet bezeichnet.

Wenn der dynamischen Modus-Algorithmus erkennt, dass eine Grenze Flowlet gefunden wurde, z. B. wenn eine Unterbrechung einer ausreichenden Länge in den TCP-Fluss - aufgetreten - verteilt der Algorithmus automatisch den Fluss auf ein anderes Teammitglied bei Bedarf neu.  Unter Umständen ungewöhnlichen kann der Algorithmus in regelmäßigen Abständen Flows ausgleichen, die keine Flowlets enthalten. Aus diesem Grund kann die Affinität zwischen TCP-Flow-Teammitglied zu einem beliebigen Zeitpunkt ändern, wie der dynamische Lastenausgleich Algorithmus funktioniert, um die arbeitsauslastung Mitglied des Teams verteilen.

## <a name="bkmk_vmq"></a>Gruppe und Warteschlangen für virtuelle Computer (Vmq)

VMQ und legen Sie gut zusammen funktionieren, und aktivieren Sie VMQ, wenn Sie Hyper-V "und" SET verwenden.

> [!NOTE]
> Legen Sie immer zeigt die Teammitglieder der Gesamtanzahl der Warteschlangen, die für alle Satz verfügbar sind. In der NIC-Teamvorgang wird dies Summe des Warteschlangen Modus bezeichnet.

Die meisten Netzwerkadapter verfügen, Warteschlangen, die für die beiden empfangsseitige Skalierung verwendet werden können \(RSS\) oder VMQ, aber nicht beides gleichzeitig.
  
Einige VMQ-Einstellungen Einstellungen für die RSS-Warteschlangen zu sein scheinen, aber es gibt Einstellungen für die generische Warteschlangen, die sowohl RSS als auch VMQ-verwendet abhängig von der Funktion aktuell verwendet wird. Jede NIC verfügt, in der erweiterten Eigenschaften, Werte für `*RssBaseProcNumber` und `*MaxRssProcessors`.

Im folgenden werden einige VMQ-Einstellungen, die eine bessere Systemleistung bereitstellen.

- Im Idealfall jede NIC aufweisen sollte die `*RssBaseProcNumber` auf eine gerade Zahl festgelegt wird, größer als oder gleich zwei (2). Grund hierfür ist der erste physischen Prozessor, Core 0 \(logischen Prozessoren, 0 und 1\), in der Regel werden die meisten das System verarbeitet, damit die netzwerkverarbeitung von diesen physischen Prozessor hardwareappliances gelenkt werden soll. 

>[!NOTE]
>Einige Feld Computerarchitekturen. keine zwei logische Prozessoren pro physischen Prozessor, sodass für diese Computer der Basis-Prozessor größer als oder gleich 1 sein sollte. Im Zweifelsfall wird davon ausgegangen Sie, dass dem Host ein Prozessor mit 2 logischen pro physischen Prozessor-Architektur verwendet.

- Die Teammitglieder Prozessoren werden sollte, sofern es ist praktisch, nicht überlappenden. Z. B. in einem 4-Core-Host \(8 logische Prozessoren\) mit einem Team von 2 NICs von 10 Gbit/s, können Sie die erste Bedingung, base 2-Prozessor zu verwenden und mit 4 Kernen festlegen; die zweite auf Basis 6-Prozessor und 2 Kerne fest.

## <a name="bkmk_hnv"></a>Gruppe und Hyper-V-Netzwerkvirtualisierung \(HNV\)

Satz ist vollständig kompatibel mit Hyper-V-Netzwerkvirtualisierung unter Windows Server 2016. Das hnv-Management-System bietet Informationen zu den SET-Treiber, der können festlegen, um die Last des Netzwerkdatenverkehrs auf eine Weise zu verteilen, die für den hnv-Datenverkehr optimiert ist.
  
## <a name="bkmk_live"></a>Festlegen und Live-Migration

Live-Migration wird in Windows Server 2016 unterstützt.

## <a name="bkmk_mac"></a>Verwendung der MAC-Adresse in gesendeten Paketen

Beim Konfigurieren eines SET-Teams mit dynamischen lastverteilung, die Pakete aus einer einzelnen Quelle \(wie z. B. eine einzelne VM\) gleichzeitig auf mehrere Teammitglieder verteilt sind. 

Ersetzt die Quell-MAC-Adresse mit einer anderen MAC-Adresse für die Frames, die auf Teammitglieder kategorisierter Teammitglieds übertragen werden, um zu verhindern, dass die Switches erste verwechselt, und um zu verhindern, dass MAC Flügelschlagen Alarme, festzulegen. Aus diesem Grund jedes Teammitglied verwendet eine andere MAC-Adresse und MAC-Adresskonflikte werden verhindert, es sei denn, und bis der Fehler auftritt.

Wenn ein Fehler auf die primäre NIC erkannt wird, festgelegtem teaming-Programme beginnt mit der MAC-Adresse des virtuellen Computers auf dem Teammitglied, das ausgewählt wird das temporäre kategorisierter Teammitglied \(z. B. dasjenige, das nun mit dem Switch als des virtuellen Computers angezeigt wird Schnittstelle\).

Diese Änderung gilt nur für Datenverkehr, der wollte, war zu sendende kategorisierter Teammitglied des virtuellen Computers, mit der VMs-MAC-Adresse als die Quell-MAC-Adresse verwendet werden. Anderer Datenverkehr wird weiterhin mit den Quell-MAC-Adresse gesendet werden, die sie vor dem Ausfall verwendet haben, würden.

Folgendes sind aufgeführt, die beschreiben, SET-teaming-MAC-Adresse ersatzverhaltens, basierend auf wie das Team konfiguriert ist:

- Im Switch unabhängigen Modus mit Hyper-V-Port-Verteilung

    - Jede VmSwitch-Port ist an ein anderes Teammitglied zugeordnet.
  
    - Jedes Paket wird auf dem Teammitglied gesendet, der der Port zugeordnet ist  
  
    - Es erfolgt kein Quell-MAC-Ersatz  
  
- Im Modus für Switchunabhängig mit dynamische Verteilung
  
    - Jede VmSwitch-Port ist an ein anderes Teammitglied zugeordnet.  
  
    - Alle ARP/NS-Pakete werden auf dem Teammitglied gesendet, die der Port zugeordnet ist  
  
    - Pakete, die auf dem Teammitglied, das das kategorisierter Teammitglied gesendet haben kein Quell-MAC-Adresse ersetzen durchgeführt  
  
    - Pakete, die auf ein anderes Teammitglied kategorisierter Teammitglieds gesendet werden Quelle MAC-Adresse ersetzen durchgeführt haben.  
  
## <a name="bkmk_manage"></a>Verwalten von einem SET-team

Es wird empfohlen, die Verwendung von System Center Virtual Machine Manager- \(VMM\) zum Verwalten von teams, Sie jedoch auch Windows PowerShell verwenden können, verwalten. Die folgenden Abschnitte enthalten, dass die Windows PowerShell-Befehle, die Sie verwenden können, zu verwalten.

Informationen zum Erstellen einer team mithilfe von VMM, finden Sie im Abschnitt "Einrichten von einem logischen Switch" in das Thema der System Center VMM-Bibliothek [logische Switches erstellen](https://docs.microsoft.com/system-center/vmm/network-switch).
  
### <a name="create-a-set-team"></a>Erstellen Sie ein SET-team

Sie müssen ein SET-Team erstellen, zur gleichen Zeit, die Sie den virtuellen Hyper-V-Switch erstellen die **New-VMSwitch** Windows PowerShell-Befehl.

Wenn Sie den virtuellen Hyper-V-Switch erstellen, müssen Sie die neue einschließen **EnableEmbeddedTeaming** Parameter in die Befehlssyntax. Im folgenden Beispiel ein Hyper-V-Switch mit dem Namen **TeamedvSwitch** mit embedded teaming und bei zwei ursprünglichen Teams Elemente erstellt wird.
  
```  
New-VMSwitch -Name TeamedvSwitch -NetAdapterName "NIC 1","NIC 2" -EnableEmbeddedTeaming $true  
```  
  
Die **EnableEmbeddedTeaming** Parameter wird davon ausgegangen, dass von Windows PowerShell bei der das Argument für **NetAdapterName** ist ein Array von NICs anstelle einer NIC. Daher können Sie den vorherigen Befehl wie folgt überarbeiten.

```  
New-VMSwitch -Name TeamedvSwitch -NetAdapterName "NIC 1","NIC 2"  
```  

Wenn Sie erstellen möchten wechseln eine SET-fähigen mit einem einzelnen Teammitglied, damit Sie ein anderes Teammitglied hinzufügen können, zu einem späteren Zeitpunkt, müssen Sie den EnableEmbeddedTeaming-Parameter verwenden.

```  
New-VMSwitch -Name TeamedvSwitch -NetAdapterName "NIC 1" -EnableEmbeddedTeaming $true  
```  

### <a name="adding-or-removing-a-set-team-member"></a>Hinzufügen oder entfernen ein SET-Teammitglied

Die **Set-VMSwitchTeam** -Befehl enthält den **NetAdapterName** Option. Um die Mitglieder des Teams in einem SET-Team zu ändern, geben Sie die gewünschte Liste der Teammitglieder, nachdem die **NetAdapterName** Option. Wenn **TeamedvSwitch** ursprünglich erstellt wurde mit NIC-1 und 2 der NIC, und klicken Sie dann Befehl im folgenden Beispiel löscht die Gruppe Mitglied des Teams "NIC-2" und fügt die neuen SET-Teammitglied "NIC 3".
  
```  
Set-VMSwitchTeam -Name TeamedvSwitch -NetAdapterName "NIC 1","NIC 3"  
```  

### <a name="removing-a-set-team"></a>Entfernen ein SET-team

Sie können ein Team für die Gruppe entfernen, nur durch das Entfernen von den virtuellen Hyper-V-Switch, die das Team für die Gruppe enthält.  Verwenden Sie das Thema [Remove-VMSwitch](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/remove-vmswitch) Informationen zu den virtuellen Hyper-V-Switch zu entfernen. Im folgenden Beispiel wird einem virtuellen Switch namens **SETvSwitch**.

```  
Remove-VMSwitch "SETvSwitch"  
```  

### <a name="changing-the-load-distribution-algorithm-for-a-set-team"></a>Ändern die Load-Verteilungsalgorithmus für ein SET-team

Die **Set-VMSwitchTeam** Cmdlet verfügt über eine **LoadBalancingAlgorithm** Option. Diese Option akzeptiert einen von zwei möglichen Werten: **HyperVPort** oder **dynamische**. Verwenden Sie diese Option, um festzulegen, oder ändern die Last Verteilungsalgorithmus für ein Switch-embedded-Team. 

Im folgenden Beispiel, mit dem Namen der VMSwitchTeam **TeamedvSwitch** verwendet die **dynamische** Lastenausgleichsalgorithmus.  
```  
Set-VMSwitchTeam -Name TeamedvSwitch -LoadBalancingAlgorithm Dynamic  
```  
### <a name="affinitizing-virtual-interfaces-to-physical-team-members"></a>Zuordnen von virtuelle Schnittstellen für physischen Teammitglieder

Satz ermöglicht Ihnen die Erstellung eine Affinität zwischen einer virtuellen Schnittstelle \(z. B. virtuelle Hyper-V-Switch Port\) und eine physische Netzwerkkarte auf dem Team. 

Z. B. bei der Erstellung zwei host-vNICs für SMB\-direkt, wie im Abschnitt [erstellen Sie einen virtuellen Hyper-V-Switch mit SET und RDMA-vNICs](#bkmk_set-rdma), können Sie sicherstellen, dass zwei vNICs verschiedene Teammitglieder verwenden. 

Das Skript in diesem Abschnitt hinzugefügt haben, können Sie die folgenden Windows PowerShell-Befehle.

    Set-VMNetworkAdapterTeamMapping -VMNetworkAdapterName SMB_1 –ManagementOS –PhysicalNetAdapterName “SLOT 2”
    Set-VMNetworkAdapterTeamMapping -VMNetworkAdapterName SMB_2 –ManagementOS –PhysicalNetAdapterName “SLOT 3”

In diesem Thema wird ausführlicher im Abschnitt 4.2.5 untersucht die [Windows Server 2016-NIC und Switch Embedded Teaming-Benutzerhandbuch](https://gallery.technet.microsoft.com/Windows-Server-2016-839cb607?redir=0).
