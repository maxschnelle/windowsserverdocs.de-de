---
title: Optimieren der Leistung von Netzwerkkarten
description: Dieses Thema ist Teil des Handbuch zur Leistungsoptimierung des Netzwerk Subsystems für Windows Server 2016.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 0b9b0f80-415c-4f5e-8377-c09b51d9c5dd
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e9c0ba73a1df874edc63001812d059a9e70f187f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405527"
---
# <a name="performance-tuning-network-adapters"></a>Optimieren der Leistung von Netzwerkkarten

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Sie können dieses Thema für die Leistungsoptimierung von Netzwerkadaptern verwenden, die auf Computern installiert sind, auf denen Windows Server 2016 ausgeführt wird.

Das Bestimmen der richtigen Feineinstellungen für Ihren Netzwerkadapter hängt von den folgenden Variablen ab:

- Dem Netzwerkadapter und seiner festgelegten Features  

- Der durch den Server ausgeführte Arbeitsauslastungstyp  

- Der Serverhardware- und Softwareressourcen  

- Von Ihren Leistungszielen in Bezug auf den Server  

Wenn Ihr Netzwerkadapter Feinstellungsoptionen bereitstellt, können Sie den Netzwerkdurchsatz und die Ressourcenverwendung optimieren, um einen maximalen Durchsatz auf Grundlage der oben beschriebenen Parameter zu erzielen.  

In den folgenden Abschnitten werden einige Ihrer Feineinstellungsoptionen beschrieben.  

##  <a name="bkmk_offload"></a>Aktivieren der Offload-Funktionen

Das Aktivieren von Netzwerkadapter-Auslagerungsfeatures ist für gewöhnlich nützlich. Manchmal ist der Netzwerkadapter jedoch nicht leistungsstark genug, um die Auslagerungsfunktionen mit hohem Durchsatz zu verarbeiten.

>[!IMPORTANT]
>Verwenden Sie nicht die Auslagerungs Features **IPSec Task Auslagerung** oder **TCP Chimney Auslagerung**. Diese Technologien sind in Windows Server 2016 veraltet und können sich negativ auf die Server-und Netzwerkleistung auswirken. Außerdem werden diese Technologien möglicherweise in Zukunft nicht von Microsoft unterstützt.

Beispielsweise kann das Aktivieren der Segmentierungsauslagerung aufgrund begrenzter Hardwareressourcen den maximal tragfähigen Durchsatz auf einigen Netzwerkadaptern reduzieren. Wenn der reduzierte Durchsatz jedoch nicht als eine Begrenzung erachtet wird, sollten Sie Auslagerungsfunktionen aktivieren, und zwar auch für diesen Netzwerkadaptertyp.

>[!NOTE]
> Für einige Netzwerkadapter ist es erforderlich, dass Auslagerungsfeatures für Sende- und Empfängerpfade unabhängig aktiviert werden.

##  <a name="bkmk_rss_web"></a>Aktivieren der Empfangs seitigen Skalierung (Receive Side Scaling, RSS) für Webserver

RSS kann die Webskalierbarkeit und Leistung verbessern, wenn weniger Netzwerkadapter als logische Prozessoren auf dem Server vorhanden sind. Wenn der gesamte Webdatenverkehr die RSS-fähigen Netzwerkadapter durchläuft, können eingehende Webanforderungen aus unterschiedlichen Verbindungen gleichzeitig über unterschiedliche CPUs hinweg verarbeitet werden.

Beachten Sie, dass die Leistung aufgrund der Logik in RSS und Hypertext Transfer Protocol \(http\) für die Lastenverteilung erheblich beeinträchtigt werden kann, wenn ein nicht RSS-fähiger Netzwerkadapter Webdatenverkehr auf einem Server akzeptiert, der über eine oder eine Weitere RSS-fähige Netzwerkadapter. In diesem Fall sollten Sie RSS-fähige Netzwerkadapter verwenden oder RSS in den Netzwerkadaptereigenschaften auf der Registerkarte **Erweiterte Eigenschaften** deaktivieren. Um zu bestimmen, ob ein Netzwerkadapter RSS-fähig ist, können Sie die RSS-Informationen in den Netzwerkadaptereigenschaften auf der Registerkarte **Erweiterte Eigenschaften** anzeigen.

### <a name="rss-profiles-and-rss-queues"></a>RSS-Profile und RSS-Warteschlangen

Das standardmäßige RSS-vordefinierte Profil ist NUMA static. Dadurch wird das Standardverhalten von früheren Versionen des Betriebssystems geändert. Für die ersten Schritte mit RSS-Profilen können Sie die verfügbaren Profile prüfen, um nachzuvollziehen, wann sie hilfreich sind und wie sie auf Ihre Netzwerkumgebung und Hardware angewendet werden.

Wenn Sie beispielsweise den Task-Manager öffnen und die logischen Prozessoren auf Ihrem Server anzeigen und sie anscheinend für den eingehenden Datenverkehr nicht ausreichend ausgelastet sind, können Sie versuchen, die Anzahl der RSS-Warteschlangen vom Standardwert 2 auf das Maximum zu erhöhen, das durch Ihren Netzwerkadapter unterstützt wird. Ihr Netzwerkadapter verfügt möglicherweise über Optionen zum Ändern der Anzahl der RSS-Warteschlangen als Bestandteil des Treibers.

##  <a name="bkmk_resources"></a>Erhöhen der Netzwerk Adapter Ressourcen

Für Netzwerkadapter, die die manuelle Konfiguration von Ressourcen gestatten wie Puffer zum Empfangen und Senden, sollten Sie die zugeordneten Ressourcen erhöhen. 

Einige Netzwerkadapter legen ihre Puffer zum Empfangen auf niedrige Werte fest, um vom Host zugeordneten Arbeitsspeicher zu sparen. Der geringe Wert hat verworfene Pakete und eine verringerte Leistung zur Folge. Daher sollten Sie in Szenarien, die „empfangsintensiv“ sind, die Anzahl des Pufferwerts für das Empfangen auf das Maximum festlegen.

>[!NOTE]
>Wenn ein Netzwerkadapter die manuelle Ressourcenkonfiguration nicht zur Verfügung stellt, konfiguriert er die Ressourcen entweder dynamisch, oder die Ressourcen sind auf einen festen Wert festgelegt, der nicht geändert werden kann.

### <a name="enabling-interrupt-moderation"></a>Aktivieren der Interruptüberprüfung

Zum Steuern der Interruptüberprüfung stellen einige Netzwerkadapter verschiedene Interruptüberprüfungsebenen, zusammengeführte Pufferparameter (manchmal getrennt für Puffer zum Senden und Empfangen) oder beide zur Verfügung.

Sie sollten die Interruptüberprüfung für CPU-gebundene Arbeitsauslastungen und den Kompromiss zwischen den CPU-Einsparungen und der Latenz mit den erhöhten Host-CPU-Einsparungen in Betracht ziehen, da hier mehr Unterbrechungen mit geringeren Latenzen vorliegen. Wenn der Netzwerkadapter keine Interruptüberprüfung ausführt, aber zusammengeführte Puffer verfügbar macht, ermöglicht Ihnen das Erhöhen der Anzahl zusammengeführter Puffer mehr Puffer zum Senden oder Empfangen, was die Leistung wiederum verbessert.

##  <a name="bkmk_low"></a>Leistungsoptimierung für die Paketverarbeitung mit geringer Latenz

Viele Netzwerkadapter bieten Optionen zum Optimieren der betriebssystembedingten Latenz. Latenz ist die Ablaufzeit, die zwischen der Netzwerktreiberverarbeitung eines eingehenden Pakets und dem Zurücksenden des Pakets durch den Netzwerktreiber vergeht. Diese Zeit wird für gewöhnlich in Mikrosekunden gemessen. Zum Vergleich wird die Übertragungszeit für Paket Übertragungen über lange Entfernungen normalerweise in Millisekunden \(in einer Größenordnung von größeren\)Größen gemessen. Diese Feineinstellung reduziert jedoch nicht die Zeit, die ein Paket übertragen wird.

Im Folgenden finden Sie einige Vorschläge zur Leistungsfeineinstellung für mikrosekundenbezogene Netzwerke.

- Legen Sie das Computer-BIOS auf **High Performance** mit deaktivierten C-Status fest. Beachten Sie jedoch, dass dies system- und BIOS-abhängig ist, und einige Systeme bieten eine höhere Leistung, wenn das Betriebssystem die Energieverwaltung steuert. Sie können Ihre Energie Verwaltungs Einstellungen über **Einstellungen** oder mithilfe des Befehls **powercfg** überprüfen und anpassen. Weitere Informationen finden Sie unter [powercfg-Befehlszeilenoptionen](https://technet.microsoft.com/library/cc748940.aspx) .

- Legen Sie das Energieverwaltungsprofil des Betriebssystems auf **Höchstleistung** fest. Beachten Sie, dass dies nicht richtig funktioniert, wenn das System-BIOS festgelegt wurde, die Betriebssystemsteuerung der Energieverwaltung zu deaktivieren.

- Aktivieren Sie „Enable Static Offloads“, beispielsweise „UDP Checksums“, „TCP Checksums“ und „Send Large Offload (LSO)“.

- Aktivieren Sie RSS, wenn der Datenverkehr mehrfach gestreamt wird, wie dies bei umfangreichem Multicast-Empfangsdatenverkehr der Fall ist.

-   Deaktivieren Sie die Einstellung **Interruptüberprüfung** für Netzwerkkartentreiber, für die die geringstmögliche Latenz erforderlich ist. Beachten Sie, dass dies mehr CPU-Zeit in Anspruch nehmen kann und eher einen Kompromiss darstellt.

- Verarbeiten Sie Netzwerkadapterunterbrechungen und DPCs auf einem Kernprozessor, der CPU-Cache gemeinsam mit dem Kern verwendet, der durch das Programm verwendet wird (Benutzerthread), welches das Paket verarbeitet. Die CPU-Affinitätsfeineinstellung kann zum Lenken eines Vorgangs zu bestimmten logischen Prozessoren in Verbindung mit der RSS-Konfiguration verwendet werden. Das Verwenden des gleichen Kerns für den Interrupt, DPC und Benutzermodusthread zieht eine schlechte Leistung und eine erhöhte Last nach sich, da ISR, DPC und der Thread den Kern für sich beanspruchen.

##  <a name="bkmk_smi"></a>System Verwaltungs Interrupts

Viele Hardwaresysteme verwenden die \(System Management Interrupts SMI\) für eine Vielzahl von Wartungsfunktionen, einschließlich der Berichterstattung über Fehler\) Korrektur Code \(ECC-Speicherfehler, ältere USB-Kompatibilität, Lüfter Kontrolle und die BIOS-gesteuerte Energie Verwaltung. 

Beim SMI handelt es sich um den Interrupt mit der höchsten Priorität auf dem System. Sie platziert die CPU in einen Verwaltungsmodus, was allen anderen Aktivitäten zuvorkommt, während sie eine Interrupt-Dienstroutine, die für gewöhnlich im BIOS enthalten ist, ausführt.

Dies kann unglücklicherweise Latenzspitzenwerte von 100 Mikrosekunden und mehr zur Folge haben. 

Wenn Sie die geringe Latenz erzielen müssen, sollten Sie eine BIOS-Version Ihres Hardwareanbieters beziehen, die die SMIs auf den kleinsten möglichen Grad reduziert. Diese werden häufig als BIOS mit geringer Latenz oder SMI-freies BIOS bezeichnet. In einigen Fällen ist es für eine Hardwareplattform nicht möglich, die gesamte SMI-Aktivität zu beenden, da sie zum Steuern wichtiger Funktionen (beispielsweise für die Lüfter) verwendet werden.

>[!NOTE]
>Das Betriebssystem kann keine Kontrolle über die SMIs ausüben, da der logische Prozessor in einem speziellen Wartungsmodus ausgeführt wird, was eine Betriebssystemintervention verhindert.

##  <a name="bkmk_tcp"></a>Leistungsoptimierung für TCP

 Sie können die TCP-Leistung mithilfe der folgenden Elemente abstimmen.

###  <a name="bkmk_tcp_params"></a>Automatische Optimierung des TCP-Empfangs Fensters

Vor Windows Server 2008 verwendete der Netzwerk Stapel ein Empfangs seitiges Fenster mit fester Größe (65.535 Bytes), das den gesamten möglichen Durchsatz für Verbindungen beschränkte. Eine der wichtigsten Änderungen am TCP-Stapel betrifft die automatische Optimierung des TCP-Empfangsfensters. 

Sie können den Gesamtdurchsatz einer einzelnen Verbindung berechnen, wenn Sie ein TCP-Empfangs Fenster mit fester Größe wie folgt verwenden:

**Erreichbarer Durchsatz Gesamt in Bytes = TCP-Empfangs Fenstergröße \* in Byte (1/Verbindungs Latenz in Sekunden)**

Der gesamte erreichbare Durchsatz beträgt z. b. nur 51 Mbit/s bei einer Verbindung \(mit einer Latenz von 10 MS und einem angemessenen\)Wert für eine große Unternehmensnetzwerk Infrastruktur. 

Mit der automatischen Optimierung kann das Fenster auf der Empfängerseite jedoch angepasst werden, und es kann wachsen, um die Anforderungen des Sendenden zu erfüllen. Es ist möglich, dass eine Verbindung eine vollständige Zeilen Rate einer 1 Gbit/s-Verbindung erreicht. Netzwerkverwendungsszenarien, die in der Vergangenheit durch den insgesamt erzielbaren Durchsatz von TCP-Verbindungen möglicherweise begrenzt wurden, können das Netzwerk nun vollständig nutzen.

#### <a name="deprecated-tcp-parameters"></a>Als veraltet markierte TCP-Parameter

Die folgenden Registrierungs Einstellungen von Windows Server 2003 werden nicht mehr unterstützt und in späteren Versionen ignoriert.

Alle diese Einstellungen verfügten über den folgenden Registrierungs Speicherort:

    ```  
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Tcpip\Parameters  
    ```  

- TcpWindowSize

- NumTcbTablePartitions  

- MaxHashTableSize  



###  <a name="bkmk_wfp"></a>Windows-Filter Plattform

Die Windows-Filter Plattform (WFP), die in Windows Vista und Windows Server 2008 eingeführt wurde, stellt APIs für unabhängige Microsoft-Softwarehersteller (ISVs) zur Verfügung, um Paketverarbeitungs Filter zu erstellen. Zu Beispielen zählen Firewall- und Antivirensoftware.

>[!NOTE]
>Ein schlecht geschriebener WFP-Filter kann die Netzwerkleistung eines Servers erheblich verringern. Weitere Informationen finden Sie im Windows dev Center [unter Portieren von Paketen für die Paketverarbeitung und Apps auf WFP](https://msdn.microsoft.com/windows/hardware/gg463267.aspx) .


Links zu allen Themen in diesem Handbuch finden Sie unter [Network Subsystem Performance Tuning](net-sub-performance-top.md).
