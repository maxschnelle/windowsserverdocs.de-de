---
title: Optimieren der Leistung von Netzwerkkarten
description: Dieses Thema ist Teil des Handbuch zur Leistungsoptimierung des Netzwerk Subsystems für Windows Server 2016.
audience: Admin - CI ID 111485 - CSSTroubleshoot
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 0b9b0f80-415c-4f5e-8377-c09b51d9c5dd
manager: dcscontentpm
ms.author: v-tea
author: Teresa-Motiv
ms.date: 12/23/2019
ms.openlocfilehash: dec88eb81227b62cd0a0ca90810b2598b8f9fd52
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854743"
---
# <a name="performance-tuning-network-adapters"></a>Optimieren der Leistung von Netzwerkkarten

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (Semi-Annual Channel)

Verwenden Sie die Informationen in diesem Thema, um die Leistungs Netzwerkadapter für Computer zu optimieren, auf denen Windows Server 2016 und höhere Versionen ausgeführt werden. Wenn Ihre Netzwerkadapter Optimierungs Optionen bereitstellen, können Sie diese Optionen verwenden, um den Netzwerk Durchsatz und die Ressourcennutzung zu optimieren.

Die richtigen Optimierungs Einstellungen für die Netzwerkadapter hängen von den folgenden Variablen ab:

- Dem Netzwerkadapter und seiner festgelegten Features  
- Der Typ der Arbeitsauslastung, die der Server ausführt  
- Der Serverhardware- und Softwareressourcen  
- Von Ihren Leistungszielen in Bezug auf den Server  

In den folgenden Abschnitten werden einige Ihrer Feineinstellungsoptionen beschrieben.  

##  <a name="enabling-offload-features"></a><a name="bkmk_offload"></a>Aktivieren der Auslagerung-Funktionen

Das Aktivieren von Netzwerkadapter-Auslagerungsfeatures ist für gewöhnlich nützlich. Der Netzwerkadapter ist jedoch möglicherweise nicht leistungsfähig genug, um die Auslagerungs Funktionen mit hohem Durchsatz zu verarbeiten.

> [!IMPORTANT]
> Verwenden Sie nicht die Auslagerungs Features **IPSec Task Auslagerung** oder **TCP Chimney Auslagerung**. Diese Technologien sind in Windows Server 2016 veraltet und können sich negativ auf die Server-und Netzwerkleistung auswirken. Außerdem werden diese Technologien möglicherweise in Zukunft nicht von Microsoft unterstützt.

Nehmen wir beispielsweise an, dass ein Netzwerkadapter nur über begrenzte Hardware Ressourcen verfügt.
In diesem Fall kann der maximale dauerhafte Durchsatz des Adapters durch Aktivieren der Segmentierungs Auslagerung verringert werden. Wenn der reduzierte Durchsatz jedoch akzeptabel ist, sollten Sie die Funktionen zur Segmentierung der Segmentierung aktivieren.

> [!NOTE]  
> Bei einigen Netzwerkadaptern müssen Sie die Auslagerungs Features für die Sende-und Empfangs Pfade unabhängig voneinander aktivieren.

##  <a name="enabling-receive-side-scaling-rss-for-web-servers"></a><a name="bkmk_rss_web"></a>Aktivieren der Empfangs seitigen Skalierung (RSS) für Webserver

RSS kann die Webskalierbarkeit und Leistung verbessern, wenn weniger Netzwerkadapter als logische Prozessoren auf dem Server vorhanden sind. Wenn der gesamte Webdatenverkehr die RSS-fähigen Netzwerkadapter durchläuft, kann der Server eingehende Webanforderungen von verschiedenen Verbindungen gleichzeitig über verschiedene CPUs hinweg verarbeiten.

> [!IMPORTANT]  
> Vermeiden Sie die Verwendung von nicht-RSS-Netzwerkadaptern und RSS-fähigen Netzwerkadaptern auf demselben Server. Aufgrund der Lasten Verteilungs Logik in RSS und Hypertext Transfer Protocol (http) kann die Leistung erheblich beeinträchtigt werden, wenn ein nicht RSS-fähiger Netzwerkadapter Webdatenverkehr auf einem Server akzeptiert, der über mindestens einen RSS-fähigen Netzwerkadapter verfügt. In diesem Fall sollten Sie RSS-fähige Netzwerkadapter verwenden oder RSS in den Netzwerkadaptereigenschaften auf der Registerkarte **Erweiterte Eigenschaften** deaktivieren.
>  
> Um zu bestimmen, ob ein Netzwerkadapter RSS-fähig ist, können Sie die RSS-Informationen in den Netzwerkadaptereigenschaften auf der Registerkarte **Erweiterte Eigenschaften** anzeigen.

### <a name="rss-profiles-and-rss-queues"></a>RSS-Profile und RSS-Warteschlangen

Das standardmäßige RSS-vordefinierte Profil ist **numastatic**und unterscheidet sich von dem Standard, das in den vorherigen Versionen von Windows verwendet wurde. Bevor Sie RSS-Profile verwenden, überprüfen Sie die verfügbaren Profile, um zu verstehen, wann Sie von Vorteil sind und wie Sie auf Ihre Netzwerkumgebung und Hardware angewendet werden.

Wenn Sie z. b. den Task-Manager öffnen und die logischen Prozessoren auf dem Server überprüfen und für den Empfang von Datenverkehr unterausgelastet sind, können Sie versuchen, die Anzahl der RSS-Warteschlangen vom Standardwert von 2 auf den maximalen Wert zu erhöhen, den der Netzwerkadapter unterstützt. Ihr Netzwerkadapter verfügt möglicherweise über Optionen zum Ändern der Anzahl der RSS-Warteschlangen als Bestandteil des Treibers.

##  <a name="increasing-network-adapter-resources"></a><a name="bkmk_resources"></a>Erhöhen der Netzwerkadapter Ressourcen

Bei Netzwerkadaptern, die es Ihnen ermöglichen, Ressourcen wie Empfangs-und Sendepuffer manuell zu konfigurieren, sollten Sie die zugeordneten Ressourcen vergrößern.  

Einige Netzwerkadapter legen ihre Puffer zum Empfangen auf niedrige Werte fest, um vom Host zugeordneten Arbeitsspeicher zu sparen. Der geringe Wert hat verworfene Pakete und eine verringerte Leistung zur Folge. Daher sollten Sie in Szenarien, die „empfangsintensiv“ sind, die Anzahl des Pufferwerts für das Empfangen auf das Maximum festlegen.

> [!NOTE]  
> Wenn ein Netzwerkadapter keine manuelle Ressourcen Konfiguration verfügbar macht, werden die Ressourcen entweder dynamisch konfiguriert, oder die Ressourcen werden auf einen festgelegten Wert festgelegt, der nicht geändert werden kann.

### <a name="enabling-interrupt-moderation"></a>Aktivieren der interruptmoderation

Um die Unterbrechungs Moderation zu steuern, machen einige Netzwerkadapter unterschiedliche Unterbrechungs Moderations Stufen, unterschiedliche Puffer Sammel Parameter (manchmal separat für Sende-und Empfangs Puffer) oder beides verfügbar.

Sie sollten die Unterbrechungs Moderation für CPU-gebundene Workloads in Erwägung gezogen. Wenn Sie die Unterbrechungs Moderation verwenden, sollten Sie den Kompromiss zwischen den CPU-Einsparungen und der Latenz der Hosts im Vergleich zu den verstärkten CPU-Einsparungen durch den Host durch mehr Interrupts und weniger Latenz abwägen. Wenn der Netzwerkadapter keine unterbrechungs moderate ausführt, aber Puffer Zusammenstellung verfügbar macht, können Sie die Leistung verbessern, indem Sie die Anzahl der zusammengefügten Puffer erhöhen, um mehr Puffer pro Sende-oder Empfangsvorgang zuzulassen.

##  <a name="performance-tuning-for-low-latency-packet-processing"></a><a name="bkmk_low"></a>Leistungsoptimierung für die Paketverarbeitung mit geringer Latenz

Viele Netzwerkadapter bieten Optionen zum Optimieren der betriebssystembedingten Latenz. Latenz ist die Ablaufzeit, die zwischen der Netzwerktreiberverarbeitung eines eingehenden Pakets und dem Zurücksenden des Pakets durch den Netzwerktreiber vergeht. Diese Zeit wird für gewöhnlich in Mikrosekunden gemessen. Zum Vergleich wird die Übertragungszeit für Paketübertragungen über lange Distanzen hinweg normalerweise in Millisekunden (aufgrund der größeren Größe) gemessen. Diese Feineinstellung reduziert jedoch nicht die Zeit, die ein Paket übertragen wird.

Im Folgenden finden Sie einige Vorschläge zur Leistungsfeineinstellung für mikrosekundenbezogene Netzwerke.

- Legen Sie das Computer-BIOS auf **High Performance** mit deaktivierten C-Status fest. Beachten Sie jedoch, dass dies system- und BIOS-abhängig ist, und einige Systeme bieten eine höhere Leistung, wenn das Betriebssystem die Energieverwaltung steuert. Sie können Ihre Energie Verwaltungs Einstellungen über **Einstellungen** oder mithilfe des Befehls **powercfg** überprüfen und anpassen. Weitere Informationen finden Sie unter [powercfg-Befehlszeilenoptionen](https://docs.microsoft.com/windows-hardware/design/device-experiences/powercfg-command-line-options).

- Legen Sie das Energieverwaltungsprofil des Betriebssystems auf **Höchstleistung** fest.  
   > [!NOTE]  
   > Diese Einstellung funktioniert nicht ordnungsgemäß, wenn das System-BIOS festgelegt wurde, um die Betriebssystem Steuerung der Energie Verwaltung zu deaktivieren.

- Aktivieren statischer Offloads. Aktivieren Sie beispielsweise die UDP-Prüfsummen, TCP-Prüfsummen und die LSO-Einstellungen (Large Offload).

- Aktivieren Sie RSS, wenn der Datenverkehr mit mehreren Daten gestreamt wird, z. b. beim Empfang von Multicast Datenverkehr mit hohem Volumen.

- Deaktivieren Sie die Einstellung **Interruptüberprüfung** für Netzwerkkartentreiber, für die die geringstmögliche Latenz erforderlich ist. Beachten Sie, dass diese Konfiguration mehr CPU-Zeit und einen Kompromiss darstellt.

- Verarbeiten Sie Netzwerkadapterunterbrechungen und DPCs auf einem Kernprozessor, der CPU-Cache gemeinsam mit dem Kern verwendet, der durch das Programm verwendet wird (Benutzerthread), welches das Paket verarbeitet. Die CPU-Affinitätsfeineinstellung kann zum Lenken eines Vorgangs zu bestimmten logischen Prozessoren in Verbindung mit der RSS-Konfiguration verwendet werden. Das Verwenden des gleichen Kerns für den Interrupt, DPC und Benutzermodusthread zieht eine schlechte Leistung und eine erhöhte Last nach sich, da ISR, DPC und der Thread den Kern für sich beanspruchen.

##  <a name="system-management-interrupts"></a><a name="bkmk_smi"></a>System Verwaltungs Interrupts

Viele Hardwaresysteme verwenden System Verwaltungs Interrupts (SMI) für eine Vielzahl von Wartungsfunktionen, wie z. b. das Melden von Fehlerkorrektur Code (ECC), die Beibehaltung der Legacy-USB-Kompatibilität, das Steuern des Lüfters und das Verwalten von BIOS-gesteuerter Leistung. Einstellungen.

Beim SMI handelt es sich um den Unterbrechung mit der höchsten Priorität auf dem System, und die CPU wird in den Verwaltungsmodus versetzt. Dieser Modus entfernt alle anderen Aktivitäten vorzeitig, während SMI eine Interrupt Service Routine ausführt, die in der Regel im BIOS enthalten ist.

Leider kann dieses Verhalten zu Latenz Spitzen von 100 Mikrosekunden oder mehr führen.

Wenn Sie die geringe Latenz erzielen müssen, sollten Sie eine BIOS-Version Ihres Hardwareanbieters beziehen, die die SMIs auf den kleinsten möglichen Grad reduziert. Diese BIOS-Versionen werden häufig als "BIOS mit niedriger Latenz" oder "SMI-freies BIOS" bezeichnet. In einigen Fällen ist es für eine Hardwareplattform nicht möglich, die gesamte SMI-Aktivität zu beenden, da sie zum Steuern wichtiger Funktionen (beispielsweise für die Lüfter) verwendet werden.

> [!NOTE]  
> Das Betriebssystem kann keine smis steuern, da der logische Prozessor in einem speziellen Wartungsmodus ausgeführt wird, der das Betriebssystem Eingriff verhindert.

##  <a name="performance-tuning-tcp"></a><a name="bkmk_tcp"></a>Leistungsoptimierung für TCP

 Sie können die folgenden Elemente verwenden, um die TCP-Leistung zu optimieren.

###  <a name="tcp-receive-window-autotuning"></a><a name="bkmk_tcp_params"></a>Automatische Optimierung des TCP-Empfangs Fensters

In Windows Vista, Windows Server 2008 und höheren Versionen von Windows verwendet der Windows-Netzwerk Stapel eine Funktion mit dem Namen " *TCP-Empfangs Fenster-Automatische* Optimierung", um die TCP-Empfangs Fenstergröße auszuhandeln. Diese Funktion kann eine definierte Empfangs Fenstergröße für jede TCP-Kommunikation während des TCP-Handshakes aushandeln.

In früheren Versionen von Windows verwendete der Windows-Netzwerk Stapel ein Empfangs Fenster mit fester Größe (65.535 Bytes), das den gesamten möglichen Durchsatz für Verbindungen beschränkte. Durch den gesamten erreichbaren Durchsatz von TCP-Verbindungen können Netzwerk Verwendungs Szenarien eingeschränkt werden. Die automatische Optimierung des TCP-Empfangs Fensters ermöglicht es diesen Szenarien, das Netzwerk vollständig zu verwenden.

Bei einem TCP-Empfangs Fenster mit einer bestimmten Größe können Sie mithilfe der folgenden Gleichung den gesamten Durchsatz einer einzelnen Verbindung berechnen.

> *Gesamtanzahl erreichbarer Durchsatz in Bytes* = *TCP-Empfangs Fenstergröße in Byte* \* (1/ *Verbindungs Latenz in Sekunden*)

Bei einer Verbindung mit einer Latenz von 10 MS beträgt der gesamte erreichbare Durchsatz z. b. nur 51 Mbit/s. Dieser Wert eignet sich für eine große Unternehmensnetzwerk Infrastruktur. Wenn Sie das Empfangs Fenster mithilfe der automatische Optimierung anpassen, kann die Verbindung jedoch die vollständige Zeilen Rate einer Verbindung mit 1 Gbit/s erreichen.  

Einige Anwendungen definieren die Größe des TCP-Empfangs Fensters. Wenn die Größe des Empfangs Fensters von der Anwendung nicht definiert wird, bestimmt die Verbindungsgeschwindigkeit die Größe wie folgt:

- Weniger als 1 Megabit pro Sekunde (Mbit/s): 8 Kilobyte (KB)
- 1 Mbit/s bis 100 Mbit/s: 17 KB
- 100 Mbit/s bis 10 Gigabit pro Sekunde (Gbit/s): 64 KB
- 10 Gbit/s oder schneller: 128 KB

Auf einem Computer, auf dem ein 1-Gbit/s-Netzwerkadapter installiert ist, sollte die Fenstergröße z. b. 64 KB betragen.

Diese Funktion nutzt auch andere Features, um die Netzwerkleistung zu verbessern. Zu diesen Features gehören die restlichen TCP-Optionen, die in [RFC 1323](https://tools.ietf.org/html/rfc1323)definiert sind. Mithilfe dieser Features können Windows-basierte Computer TCP-Empfangs Fenstergrößen aushandeln, die kleiner sind, aber abhängig von der Konfiguration mit einem definierten Wert skaliert werden. Dieses Verhalten ist für Netzwerkgeräte einfacher zu handhaben.

> [!NOTE]  
> Möglicherweise tritt ein Problem auf, bei dem das Netzwerkgerät nicht mit der **TCP-Fenster Skalierungs Option**kompatibel ist, wie in [RFC 1323](https://tools.ietf.org/html/rfc1323) definiert. Daher wird der Skalierungsfaktor nicht unterstützt. In diesen Fällen kann die [Netzwerk Konnektivität in KB 934430 nicht ausgeführt werden, wenn Sie versuchen, Windows Vista hinter einem Firewallgerät zu verwenden,](https://support.microsoft.com/help/934430/network-connectivity-fails-when-you-try-to-use-windows-vista-behind-a) oder wenden Sie sich an das Support Team Ihres Netzwerkgeräte Anbieters.  

#### <a name="review-and-configure-tcp-receive-window-autotuning-level"></a>Überprüfen und Konfigurieren der automatische Optimierungs Ebene für das TCP-Empfangs Fenster

Sie können entweder Netsh-Befehle oder Windows PowerShell-Cmdlets verwenden, um die automatische Optimierungs Ebene des TCP-Empfangs Fensters zu überprüfen oder zu ändern.

> [!NOTE]  
> Anders als bei Windows-Versionen, die vor dem Update von Windows 10 oder Windows Server 2019 verwendet wurden, können Sie die Registrierung nicht mehr verwenden, um die TCP-Empfangs Fenstergröße zu konfigurieren. Weitere Informationen zu den veralteten Einstellungen finden Sie unter als [veraltet markierte TCP-Parameter](#deprecated-tcp-parameters).

> [!NOTE]  
> Ausführliche Informationen zu den verfügbaren automatische Optimierungs Ebenen finden Sie unter [Automatische Optimierungs Ebenen](#autotuning-levels).

**So verwenden Sie netsh, um die automatische Optimierungs Ebene zu überprüfen oder zu ändern**

Um die aktuellen Einstellungen zu überprüfen, öffnen Sie ein Eingabe Aufforderungs Fenster, und führen Sie den folgenden Befehl aus:

```cmd
netsh interface tcp show global
```

Die Ausgabe dieses Befehls sollte etwa wie folgt aussehen:

```
Querying active state...

TCP Global Parameters  
-----
Receive-Side Scaling State : enabled
Chimney Offload State : disabled
Receive Window Auto-Tuning Level : normal
Add-On Congestion Control Provider : default
ECN Capability : disabled
RFC 1323 Timestamps : disabled
Initial RTO : 3000
Receive Segment Coalescing State : enabled
Non Sack Rtt Resiliency : disabled
Max SYN Retransmissions : 2
Fast Open : enabled
Fast Open Fallback : enabled
Pacing Profile : off
```

Um die Einstellung zu ändern, führen Sie den folgenden Befehl an der Eingabeaufforderung aus:

```cmd
netsh interface tcp set global autotuninglevel=<Value>
```

> [!NOTE]  
> Im vorherigen Befehl > \<*Wert*den neuen Wert für die automatische Optimierungs Ebene dar.

Weitere Informationen zu diesem Befehl finden Sie unter [Netsh Commands for Interface Transmission Control Protocol](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731258(v=ws.10)).

**So verwenden Sie PowerShell, um die automatische Optimierungs Ebene zu überprüfen oder zu ändern**

Öffnen Sie ein PowerShell-Fenster, und führen Sie das folgende Cmdlet aus, um die aktuellen Einstellungen zu überprüfen.

```PowerShell
Get-NetTCPSetting | Select SettingName,AutoTuningLevelLocal
```

Die Ausgabe dieses Cmdlets sollte in etwa wie folgt aussehen.

```
SettingName           AutoTuningLevelLocal
-----------          --------------------
Automatic
InternetCustom       Normal
DatacenterCustom     Normal
Compat               Normal
Datacenter           Normal
Internet             Normal
```

Um die Einstellung zu ändern, führen Sie das folgende Cmdlet an der PowerShell-Eingabeaufforderung aus.

```PowerShell
Set-NetTCPSetting -AutoTuningLevelLocal <Value>
```

> [!NOTE]  
> Im vorherigen Befehl > \<*Wert*den neuen Wert für die automatische Optimierungs Ebene dar.

Weitere Informationen zu diesen Cmdlets finden Sie in den folgenden Artikeln:

- [Get-nettcpsetting](https://docs.microsoft.com/powershell/module/nettcpip/get-nettcpsetting?view=win10-ps)
- [Set-nettcpsetting](https://docs.microsoft.com/powershell/module/nettcpip/set-nettcpsetting?view=win10-ps)

#### <a name="autotuning-levels"></a>Automatische Optimierungs Stufen

Sie können die automatische Optimierung des Empfangs Fensters auf eine beliebige von fünf Ebenen festlegen. Der Standardwert ist " **Normal**". In der folgenden Tabelle werden die Ebenen beschrieben.

|Level |Hexadezimalwert |Comments |
| --- | --- | --- |
|Normal (Standardeinstellung) |0x8 (Skalierungsfaktor 8) |Legen Sie fest, dass das TCP-Empfangs Fenster für fast alle Szenarien erweitert werden soll. |
|Deaktiviert |Kein Skalierungsfaktor verfügbar |Legen Sie das TCP-Empfangs Fenster auf den Standardwert fest. |
|Restricted (Eingeschränkter Zugriff) |0x4 (Skalierungsfaktor 4) |Legen Sie fest, dass das TCP-Empfangs Fenster über den Standardwert hinaus vergrößert wird, aber begrenzen Sie dieses Wachstum in einigen Szenarien. |
|Stark eingeschränkt |0x2 (Skalierungsfaktor von 2) |Legen Sie fest, dass das TCP-Empfangs Fenster über den Standardwert hinaus wächst, aber dies ist sehr konservativ. |
|Eller |0xe (Skalierungsfaktor 14) |Legen Sie fest, dass das TCP-Empfangs Fenster erweitert wird, um extrem Szenarios aufzunehmen |

Wenn Sie eine Anwendung verwenden, um Netzwerkpakete zu erfassen, sollte die Anwendung Daten, die den folgenden ähneln, für verschiedene Einstellungen für die automatische Einstellungen der Fenster-Optimierung melden.

- Automatische Optimierungs Ebene: **Normal (Standardstatus)**

   ```
   Frame: Number = 492, Captured Frame Length = 66, MediaType = ETHERNET
   + Ethernet: Etype = Internet IP (IPv4),DestinationAddress:[D8-FE-E3-65-F3-FD],SourceAddress:[C8-5B-76-7D-FA-7F]
   + Ipv4: Src = 192.169.0.5, Dest = 192.169.0.4, Next Protocol = TCP, Packet ID = 2667, Total IP Length = 52
   - Tcp: [Bad CheckSum]Flags=......S., SrcPort=60975, DstPort=Microsoft-DS(445), PayloadLen=0, Seq=4075590425, Ack=0, Win=64240 ( Negotiating scale factor 0x8 ) = 64240
   SrcPort: 60975
   DstPort: Microsoft-DS(445)
   SequenceNumber: 4075590425 (0xF2EC9319)
   AcknowledgementNumber: 0 (0x0)
   + DataOffset: 128 (0x80)
   + Flags: ......S. ---------------------------------------------------------> SYN Flag set
   Window: 64240 ( Negotiating scale factor 0x8 ) = 64240 ---------> TCP Receive Window set as 64K as per NIC Link bitrate. Note it shows the 0x8 Scale Factor.
   Checksum: 0x8182, Bad
   UrgentPointer: 0 (0x0)
   - TCPOptions:
   + MaxSegmentSize: 1
   + NoOption:
   + WindowsScaleFactor: ShiftCount: 8 -----------------------------> Scale factor, defined by AutoTuningLevel
   + NoOption:
   + NoOption:
   + SACKPermitted:
   ```

- Stufe "Automatische Optimierung": **deaktiviert**

   ```
   Frame: Number = 353, Captured Frame Length = 62, MediaType = ETHERNET
   + Ethernet: Etype = Internet IP (IPv4),DestinationAddress:[D8-FE-E3-65-F3-FD],SourceAddress:[C8-5B-76-7D-FA-7F]
   + Ipv4: Src = 192.169.0.5, Dest = 192.169.0.4, Next Protocol = TCP, Packet ID = 2576, Total IP Length = 48
   - Tcp: [Bad CheckSum]Flags=......S., SrcPort=60956, DstPort=Microsoft-DS(445), PayloadLen=0, Seq=2315885330, Ack=0, Win=64240 ( ) = 64240
   SrcPort: 60956
   DstPort: Microsoft-DS(445)
   SequenceNumber: 2315885330 (0x8A099B12)
   AcknowledgementNumber: 0 (0x0)
   + DataOffset: 112 (0x70)
   + Flags: ......S. ---------------------------------------------------------> SYN Flag set
   Window: 64240 ( ) = 64240 ----------------------------------------> TCP Receive Window set as 64K as per NIC Link bitrate. Note there is no Scale Factor defined. In this case, Scale factor is not being sent as a TCP Option, so it will not be used by Windows.
   Checksum: 0x817E, Bad
   UrgentPointer: 0 (0x0)
   - TCPOptions:
   + MaxSegmentSize: 1
   + NoOption:
   + NoOption:
   + SACKPermitted:
   ```

- Stufe "Automatische Optimierung": **eingeschränkt**

   ```
   Frame: Number = 3, Captured Frame Length = 66, MediaType = ETHERNET
   + Ethernet: Etype = Internet IP (IPv4),DestinationAddress:[D8-FE-E3-65-F3-FD],SourceAddress:[C8-5B-76-7D-FA-7F]
   + Ipv4: Src = 192.169.0.5, Dest = 192.169.0.4, Next Protocol = TCP, Packet ID = 2319, Total IP Length = 52
   - Tcp: [Bad CheckSum]Flags=......S., SrcPort=60890, DstPort=Microsoft-DS(445), PayloadLen=0, Seq=1966088568, Ack=0, Win=64240 ( Negotiating scale factor 0x4 ) = 64240
   SrcPort: 60890
   DstPort: Microsoft-DS(445)
   SequenceNumber: 1966088568 (0x75302178)
   AcknowledgementNumber: 0 (0x0)
   + DataOffset: 128 (0x80)
   + Flags: ......S. ---------------------------------------------------------> SYN Flag set
   Window: 64240 ( Negotiating scale factor 0x4 ) = 64240 ---------> TCP Receive Window set as 64K as per NIC Link bitrate. Note it shows the 0x4 Scale Factor.
   Checksum: 0x8182, Bad
   UrgentPointer: 0 (0x0)
   - TCPOptions:
   + MaxSegmentSize: 1
   + NoOption:
   + WindowsScaleFactor: ShiftCount: 4 -------------------------------> Scale factor, defined by AutoTuningLevel.
   + NoOption:
   + NoOption:
   + SACKPermitted:
   ```

- Ebene der automatische Optimierung: **stark eingeschränkt**

   ```
   Frame: Number = 115, Captured Frame Length = 66, MediaType = ETHERNET
   + Ethernet: Etype = Internet IP (IPv4),DestinationAddress:[D8-FE-E3-65-F3-FD],SourceAddress:[C8-5B-76-7D-FA-7F]
   + Ipv4: Src = 192.169.0.5, Dest = 192.169.0.4, Next Protocol = TCP, Packet ID = 2388, Total IP Length = 52
   - Tcp: [Bad CheckSum]Flags=......S., SrcPort=60903, DstPort=Microsoft-DS(445), PayloadLen=0, Seq=1463725706, Ack=0, Win=64240 ( Negotiating scale factor 0x2 ) = 64240
   SrcPort: 60903
   DstPort: Microsoft-DS(445)
   SequenceNumber: 1463725706 (0x573EAE8A)
   AcknowledgementNumber: 0 (0x0)
   + DataOffset: 128 (0x80)
   + Flags: ......S. ---------------------------------------------------------> SYN Flag set
   Window: 64240 ( Negotiating scale factor 0x2 ) = 64240 ---------> TCP Receive Window set as 64K as per NIC Link bitrate. Note it shows the 0x2 Scale Factor.
   Checksum: 0x8182, Bad
   UrgentPointer: 0 (0x0)
   - TCPOptions:
   + MaxSegmentSize: 1
   + NoOption:
   + WindowsScaleFactor: ShiftCount: 2 ------------------------------> Scale factor, defined by AutoTuningLevel
   + NoOption:
   + NoOption:
   + SACKPermitted:
   ```

- Stufe "Automatische Optimierung": **experimentell**

   ```
   Frame: Number = 238, Captured Frame Length = 66, MediaType = ETHERNET
   + Ethernet: Etype = Internet IP (IPv4),DestinationAddress:[D8-FE-E3-65-F3-FD],SourceAddress:[C8-5B-76-7D-FA-7F]
   + Ipv4: Src = 192.169.0.5, Dest = 192.169.0.4, Next Protocol = TCP, Packet ID = 2490, Total IP Length = 52
   - Tcp: [Bad CheckSum]Flags=......S., SrcPort=60933, DstPort=Microsoft-DS(445), PayloadLen=0, Seq=2095111365, Ack=0, Win=64240 ( Negotiating scale factor 0xe ) = 64240
   SrcPort: 60933
   DstPort: Microsoft-DS(445)
   SequenceNumber: 2095111365 (0x7CE0DCC5)
   AcknowledgementNumber: 0 (0x0)
   + DataOffset: 128 (0x80)
   + Flags: ......S. ---------------------------------------------------------> SYN Flag set
   Window: 64240 ( Negotiating scale factor 0xe ) = 64240 ---------> TCP Receive Window set as 64K as per NIC Link bitrate. Note it shows the 0xe Scale Factor.
   Checksum: 0x8182, Bad
   UrgentPointer: 0 (0x0)
   - TCPOptions:
   + MaxSegmentSize: 1
   + NoOption:
   + WindowsScaleFactor: ShiftCount: 14 -----------------------------> Scale factor, defined by AutoTuningLevel
   + NoOption:
   + NoOption:
   + SACKPermitted:
   ```

#### <a name="deprecated-tcp-parameters"></a>Als veraltet markierte TCP-Parameter

Die folgenden Registrierungs Einstellungen von Windows Server 2003 werden nicht mehr unterstützt und in späteren Versionen ignoriert.

- **TcpWindowSize**
- **Numtcbtablepartitions**  
- **Maxhashtablesize**  

Alle diese Einstellungen befinden sich im folgenden Registrierungs Unterschlüssel:

> **HKEY_LOCAL_MACHINE \system\currentcontrolset\services\tcpip\parameters**  

###  <a name="windows-filtering-platform"></a><a name="bkmk_wfp"></a>Windows-Filter Plattform

Windows Vista und Windows Server 2008 haben die Windows-Filter Plattform (WFP) eingeführt. WFP stellt APIs für unabhängige Microsoft-Softwarehersteller (ISVs) zur Verfügung, um Paketverarbeitungs Filter zu erstellen. Zu Beispielen zählen Firewall- und Antivirensoftware.

> [!NOTE]  
> Ein schlecht geschriebener WFP-Filter kann die Netzwerkleistung eines Servers erheblich verringern. Weitere Informationen finden Sie im Windows dev Center [unter Portieren von Paketen für die Paketverarbeitung und Apps auf WFP](https://docs.microsoft.com/windows-hardware/drivers/network/porting-packet-processing-drivers-and-apps-to-wfp) .

Links zu allen Themen in diesem Handbuch finden Sie unter [Network Subsystem Performance Tuning](net-sub-performance-top.md).
