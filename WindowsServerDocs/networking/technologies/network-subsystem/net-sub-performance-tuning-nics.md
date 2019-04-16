---
title: Leistung optimieren von Netzwerkadaptern
description: Dieses Thema ist Teil der Netzwerk-Subsystem-Leistungsoptimierung Anleitung für Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0b9b0f80-415c-4f5e-8377-c09b51d9c5dd
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1c6d36966ce6e2d407b6568e16946745256ee69b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="performance-tuning-network-adapters"></a>Leistung optimieren von Netzwerkadaptern

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema auf Netzwerkadapter für Leistung optimieren können, die auf Computern installiert sind, auf denen Windows Server 2016 ausgeführt werden.

Bestimmen der richtigen feineinstellungen für Ihren Netzwerkadapter hängt die folgenden Variablen:

- Der Netzwerkadapter und seiner festgelegten Features  

- Durch den Server ausgeführte Arbeitsauslastungstyp  

- Die Server-Hardware und Software-Ressourcen  

- Die Leistungsziele für den server  

Wenn Ihr Netzwerkadapter feinstellungsoptionen bereitstellt, können Sie die Netzwerkverwendung Durchsatz und Ressourcen zum Erreichen des maximalen Durchsatz auf Grundlage der oben beschriebenen Parameter optimieren.  

In den folgenden Abschnitten werden einige Ihrer feineinstellungsoptionen beschrieben.  

##  <a name="bkmk_offload"></a>Aktivieren von Auslagerungsfeatures

Aktivieren der Netzwerkadapter-auslagerungsfeatures ist für gewöhnlich nützlich. In manchen Fällen ist jedoch der Netzwerkadapter nicht leistungsfähig genug, um die Auslagerungsfunktionen mit hohem Durchsatz zu behandeln.

>[!IMPORTANT]
>Verwenden Sie nicht die auslagerungsfeatures **IPsec Task Offload** oder **TCP-Chimneyabladung**. Diese Technologien sind in Windows Server 2016 veraltet und möglicherweise beeinträchtigt, Server und die Leistung des Netzwerkes. Darüber hinaus können diese Technologien nicht von Microsoft in Zukunft unterstützt.

Aktivieren der segmentierungsauslagerung kann z. B. den maximalen tragfähigen Durchsatz auf einigen Netzwerkadaptern aufgrund begrenzter Hardwareressourcen reduzieren. Wenn der reduzierte Durchsatz zu einer Einschränkung nicht erwartet wird, sollten Sie Auslagerungsfunktionen, auch für diese Art der Netzwerkadapter aktivieren.

>[!NOTE]
> Einige Netzwerkadapter erforderlich auslagerungsfeatures unabhängig aktiviert werden, zum Senden und Empfangen von Pfade.

##  <a name="bkmk_rss_web"></a>Aktivieren von Side Scaling (RSS) für Webserver erhalten

RSS können webskalierbarkeit und Leistung verbessern, wenn weniger Netzwerkadapter als logische Prozessoren auf dem Server vorhanden sind. Wenn der gesamte Webdatenverkehr die RSS-fähige Netzwerkadapter durchlaufen wird, können eingehende webanforderungen aus unterschiedlichen Verbindungen gleichzeitig über unterschiedliche CPUs hinweg verarbeitet werden.

Es ist wichtig zu beachten, dass aufgrund der Logik in RSS und Hypertext Transfer-Protokoll \(HTTP\) für die Verteilung, die Leistung möglicherweise erheblich heruntergestuft, wenn ein nicht-RSS-fähiger Netzwerkadapter Webdatenverkehr auf einem Server akzeptiert, die eine oder mehrere RSS-fähige Netzwerkadapter verfügt. In diesem Fall verwenden Sie RSS-fähige Netzwerkadapter oder Deaktivieren von RSS auf den Eigenschaften des Netzwerkadapters **erweiterte Eigenschaften** Registerkarte. Um festzustellen, ob ein Netzwerkadapter RSS-fähig ist, können Sie die RSS-Informationen anzeigen, auf den Eigenschaften des Netzwerkadapters **erweiterte Eigenschaften** Registerkarte.

### <a name="rss-profiles-and-rss-queues"></a>RSS-Profile und RSS-Warteschlangen

Das Standardprofil für vordefinierte RSS ist statisch NUMA, das das Standardverhalten von früheren Versionen des Betriebssystems ändert. Um den ersten Schritten mit RSS-Profile können Sie überprüfen, die verfügbaren Profile, um zu verstehen, wann sie hilfreich sind und wie sie sich auf Ihre Netzwerkumgebung und Hardware angewendet.

Beispielsweise können Wenn Sie Task-Manager öffnen, und überprüfen Sie die logischen Prozessoren auf dem Server, und sie anscheinend für den eingehenden Datenverkehr nicht ausreichend ausgelastet sind, Sie erhöhen Sie die Anzahl der RSS-Warteschlangen vom Standardwert 2 auf das Maximum, das durch Ihren Netzwerkadapter unterstützt wird. Der Netzwerkadapter möglicherweise Optionen, um die Anzahl der RSS-Warteschlangen als Bestandteil des Treibers ändern.

##  <a name="bkmk_resources"></a>Netzwerkadapterressourcen

Für Netzwerkadapter, die manuelle Konfiguration von Ressourcen ermöglichen, z. B. empfangen und Senden von Puffern, sollten Sie die zugeordneten Ressourcen erhöhen. 

Manche Netzwerkadapter festgelegt ihre Empfangspuffer niedrig zugeordneten Arbeitsspeicher zu sparen vom Host. Der geringe Wert hat Verworfene Pakete und Leistungseinbußen. Daher wird empfohlen Receive-Intensive Szenarien, die pufferwerts auf das Maximum zu erhöhen.

>[!NOTE]
>Wenn ein Netzwerkadapter die manuelle Ressourcenkonfiguration nicht verfügbar macht, entweder dynamisch konfiguriert die Ressourcen, oder die Ressourcen festgelegt auf einen festen Wert, der nicht geändert werden kann.

### <a name="enabling-interrupt-moderation"></a>Aktivieren der Interruptüberprüfung

Zum Steuern der interruptüberprüfung einige Netzwerkadapter verschiedene Interrupt Moderation Ebenen verfügbar zu machen, Pufferparameter (manchmal getrennt für senden und Empfangen von Puffern), oder beides.

Sie sollten interruptüberprüfung für CPU-gebundene arbeitsauslastungen und einen Kompromiss zwischen der CPU-einsparungen und der Latenz mit den erhöhten Host-CPU-einsparungen berücksichtigen, da hier mehr Unterbrechungen und weniger Wartezeit. Wenn der Netzwerkadapter keine interruptüberprüfung Puffer Zusammenfügung macht, erhöhen, jedoch wird die Anzahl der zusammengeführter Puffer kann weitere Puffer zum Senden oder empfangen, die Leistung wiederum verbessert.

##  <a name="bkmk_low"></a>Feineinstellen der Verarbeitung von Paketen mit geringer Latenz

Viele Netzwerkadapter bieten Optionen zum Optimieren der betriebssystembedingten Latenz. Latenz ist die Zeit zwischen den Netzwerktreiber eines eingehenden Pakets und der Netzwerktreiber Senden des Pakets zurück. Diese Zeit wird in der Regel in Mikrosekunden gemessen. Zum Vergleich wird die Übertragungszeit für paketübertragungen über lange Distanzen hinweg normalerweise in Millisekunden gemessen \ (eine Größenordnung Larger\). Diese Einstellung wird nicht die Zeit verringern, die ein Paket während der Übertragung verbringt.

Im folgenden werden einige Vorschläge für mikrosekundenbezogene Netzwerke für die Optimierung.

- Legen Sie das BIOS des Computers auf **mit hoher Leistung**, mit deaktivierten C-Status. Beachten Sie jedoch, dass dies System- und BIOS-abhängig ist, und einige Systeme eine höhere Leistung bieten, wenn die energieverwaltung das Betriebssystem steuert. Sie können überprüfen, und passen Sie Ihre energieverwaltungseinstellungen **Einstellungen** oder mithilfe der **Powercfg** Befehl. Weitere Informationen finden Sie unter [Powercfg-Befehlszeilenoptionen](https://technet.microsoft.com/library/cc748940.aspx)

- Legen Sie das energieverwaltungsprofil des Betriebssystems auf **Höchstleistung**. Beachten Sie, dass dies nicht ordnungsgemäß ausgeführt werden, wenn das System-BIOS festgelegt wurde, die betriebssystemsteuerung der energieverwaltung zu deaktivieren.

- Aktivieren Sie die statischen Auslagerungen, z. B. Prüfsummen für UDP, TCP Checksums, und senden Large Offload (LSO).

- Aktivieren Sie RSS, wenn der Datenverkehr mehrfach gestreamt, ist, wie z. B. mit hohem Volumen Multicast erhalten.

-   Deaktivieren der **Interruptüberprüfung** für Netzwerkkartentreiber, für die die geringstmögliche Latenz erforderlich. Beachten Sie, dass dies mehr CPU-Zeit verwenden kann und ein Kompromiss darstellt.

- Behandeln Sie netzwerkadapterunterbrechungen und DPCs auf einem kernprozessor, die CPU-Cache für den Kern freigegeben, die von der Anwendung (Benutzerthread) verwendet wird, die das Paket behandelt werden. CPU-affinitätsfeineinstellung kann verwendet werden, um einen Prozess zu bestimmten logischen Prozessoren in Verbindung mit RSS-Konfiguration zu leiten. Mit den gleichen grundlegenden für den Interrupt, DPC und der Benutzer den Modus Thread ist das schlechter Leistung zunehmender Last, da die ISR, DPC und der Thread für die Verwendung der wichtigsten konkurrieren.

##  <a name="bkmk_smi"></a>Systemverwaltungsunterbrechungen

Viele Hardwaresysteme verwenden System Management Interrupts \(SMI\) für eine Vielzahl von Verwaltungsoptionen, dazu zählen die berichterstellung Korrektur Code \(ECC\) Arbeitsspeicherfehler, legacy-USB-Kompatibilität, lüftungssteuerung und BIOS-gesteuerte energieverwaltung. 

Der SMI ist die höchste Priorität Interrupt auf dem System und platziert die CPU in einen Verwaltungsmodus, der alle anderen Aktivitäten zuvorkommt, während sie eine Interrupt-dienstroutine, die in der Regel im BIOS enthalten ausgeführt wird.

Leider kann diese Latenzspitzenwerte von 100 Mikrosekunden oder mehrere führen. 

Wenn Sie die niedrigste Latenz erzielen müssen, sollten Sie eine BIOS-Version Ihres Hardwareanbieters anfordern, die SMIs auf die möglichen Grad reduziert. Diese werden häufig als "BIOS mit geringer Latenz" oder SMI-freies BIOS."bezeichnet In einigen Fällen ist es nicht möglich, dass eine Hardwareplattform SMI-Aktivität zu beenden, da es zum Steuern wichtiger Funktionen (z. B. Lüfter) verwendet wird.

>[!NOTE]
>Das Betriebssystem kann keine Kontrolle über die SMIs ausüben, da der logische Prozessor in einem speziellen Wartungsmodus betriebssystemintervention verhindert ausgeführt wird.

##  <a name="bkmk_tcp"></a>TCP-leistungsfeineinstellung

 Sie können die Leistung optimieren TCP mithilfe der folgenden Elemente.

###  <a name="bkmk_tcp_params"></a>TCP Auto-Empfangsfensters

Vor Windows Server2008 verwendete der Netzwerkstapel ein fester Größe empfangsseitige Fenster (65.535 Bytes), das den gesamten potenziellen Durchsatz für Verbindungen begrenzte. Ist eine der wichtigsten Änderungen an TCP-Stapel TCP Auto-Empfangsfensters. 

Sie können den Gesamtdurchsatz einer einzelnen Verbindung berechnen, wenn Sie eine feste Größe TCP-Empfangsfensters als verwenden:

**Gesamt erzielbarer Durchsatz in Byte = TCP Größe in Bytes erhalten \ * (1/Verbindungslatenz in Sekunden)**

Beispielsweise ist der gesamte erzielbare Durchsatz nur 51 MBit/s bei einer Verbindung mit Latenz von 10 ms \ (ein angemessener Wert für eine große Unternehmensnetzwerk Infrastructure\). 

Mit der automatischen Optimierung, jedoch die Fenster ist anpassbar, und es kann wachsen, um die Anforderungen des sendenden zu erfüllen. Es ist möglich, dass eine Verbindung mit einem vollständige Leitungsrate einer 1 Gbit/s-Verbindung zu erzielen. Netzwerkverwendungsszenarien, die in der Vergangenheit durch den insgesamt erzielbaren Durchsatz von TCP-Verbindungen möglicherweise begrenzt wurden, können nun vollständig im Netzwerk verwenden.

#### <a name="deprecated-tcp-parameters"></a>Veraltete TCP-Parameter

Die folgenden registrierungseinstellungen von Windows Server 2003 werden nicht mehr unterstützt und in späteren Versionen ignoriert werden.

All diese Einstellungen wurden die folgenden Registrierungsschlüssel:

    ```  
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Tcpip\Parameters  
    ```  

- TcpWindowSize

- NumTcbTablePartitions  

- MaxHashTableSize  



###  <a name="bkmk_wfp"></a>Windows-Filterplattform

Die Windows Filtering Platform (WFP), die in Windows Vista und Windows Server 2008 eingeführt wurde bietet APIs zu nicht-Microsoft unabhängige Softwareanbieter (ISVs) zum Erstellen von paketverarbeitungsfiltern. Beispiele: Firewall- und Antivirensoftware.

>[!NOTE]
>Ein schlecht geschriebener WFP-Filter kann die netzwerkleistung eines Servers erheblich verringern. Weitere Informationen finden Sie unter [Portieren Paket erforderliche Treiber und Apps zu Windows-Dateischutz](https://msdn.microsoft.com/windows/hardware/gg463267.aspx) im Windows Dev Center.


Links zu allen Themen in diesem Handbuch finden Sie [Optimieren der Leistung mit Subsystem](net-sub-performance-top.md).
