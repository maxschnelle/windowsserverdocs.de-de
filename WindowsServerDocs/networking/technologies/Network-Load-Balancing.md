---
title: Netzwerklastenausgleich
description: In diesem Thema, wir bieten Ihnen einen Überblick über den Netzwerklastenausgleich \(NLB\) -Feature in Windows Server 2016. Sie können NLB verwenden, um zwei oder mehr Servern als einzelnen virtuellen Cluster verwalten. NLB verbessert die Verfügbarkeit und Skalierbarkeit von Internet-serveranwendungen wie für Web-, FTP, firewall, Proxyserver, virtuelles privates Netzwerk \(VPN\), und andere unternehmenskritische\-wichtigen Servern.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-nlb
ms.topic: article
ms.assetid: 244a4b48-06e5-4796-8750-a50e4f88ac72
ms.author: pashort
author: shortpatti
ms.date: 09/13/2018
ms.openlocfilehash: d0cf1e1d6b1681a0f18908b08cd17572159e0462
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881751"
---
# <a name="network-load-balancing"></a>Netzwerklastenausgleich

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema, wir bieten Ihnen einen Überblick über den Netzwerklastenausgleich \(NLB\) -Feature in Windows Server 2016. Sie können NLB verwenden, um zwei oder mehr Servern als einzelnen virtuellen Cluster verwalten. NLB verbessert die Verfügbarkeit und Skalierbarkeit von Internet-serveranwendungen wie für Web-, FTP, firewall, Proxyserver, virtuelles privates Netzwerk \(VPN\), und andere unternehmenskritische\-wichtigen Servern.  

>[!NOTE]
>Windows Server 2016 enthält ein neuer Azure Inspirierte Software Load Balancer \(SLB\) als Komponente von der Software Defined Networking \(SDN\) Infrastruktur. Verwendung SLB anstelle von NLB bei Verwendung von SDN-nicht-Windows-Workloads verwenden, benötigen Sie ausgehenden NAT \(NAT\), oder Layer 3 benötigen \(L3\) oder nicht-TCP-basierte Lastenausgleich. Sie können weiterhin Verwendung von NLB mit Windows Server 2016 für nicht-SDN-Bereitstellungen. Weitere Informationen zu den SLB, finden Sie unter [Software Load Balancing (SLB) für SDN](../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md).

Der Netzwerklastenausgleich \(NLB\) Feature verteilt den Datenverkehr auf mehrere Server mithilfe von TCP\/IP-Netzwerkprotokolls. Durch die Kombination von zwei oder mehr Computern, die Anwendungen in einem einzelnen virtuellen Cluster ausgeführt werden, bietet NLB Zuverlässigkeit und Leistung für Webserver und andere unternehmenskritische\-wichtigen Servern.  
  
Die Server in einem NLB-Cluster werden als *Hosts*bezeichnet, und jeder Host führt eine separate Kopie der Serveranwendungen aus. Beim Netzwerklastenausgleich werden eingehende Clientanforderungen an die Hosts des Clusters verteilt. Sie können die Last konfigurieren, die von jedem Host behandelt werden soll. Sie können Hosts auch dynamisch dem Cluster hinzufügen, um erhöhte Lasten verarbeiten zu können. NLB kann auch den gesamten Datenverkehr zu einem einzelnen zugewiesenen Host weiterleiten. Dieser Host wird als *Standardhost* bezeichnet.  
  
Mit NLB können alle Computer eines Clusters mit derselben Gruppe von IP-Adressen adressiert werden. Dabei wird eine Gruppe von eindeutigen dedizierten IP-Adressen für jeden Host beibehalten. Last\--Anwendungen mit Lastenausgleich, wenn ein Host ausfällt oder offline geht, die Last wird automatisch neu verteilt, zwischen den Computern, die weiterhin ausgeführt werden. Wenn der offline geschaltete Computer wieder bereit ist, kann er erneut transparent mit dem Cluster verbunden werden und seinen Teil der Arbeitsauslastung wieder aufnehmen. Dadurch muss von den anderen Computern weniger Datenverkehr verarbeitet werden.  
  
## <a name="practical-applications"></a>Praktische Anwendungsfälle  
NLB ist hilfreich, um sicherzustellen, dass statusfreie Anwendungen, z. B. Webserver mit Internet Information Services \(IIS\), mit minimaler Downtime verfügbar sind und dass diese skalierbar sind \(durch Hinzufügen zusätzlicher Server als die Auslastung steigt\). In den folgenden Abschnitten wird beschrieben, wie NLB eine hohe Verfügbarkeit, Skalierbarkeit und Verwaltbarkeit der geclusterten Server unterstützt, auf denen diese Anwendungen ausgeführt werden.  
  
### <a name="high-availability"></a>Hohe Verfügbarkeit  
Ein System mit hoher Verfügbarkeit bietet zuverlässig einen akzeptablen Grad an Leistung mit minimaler Downtime. Um hochverfügbarkeit zu gewährleisten, NLB umfasst erstellt\-in Funktionen, die automatisch können:  
  
-   Erkennen und Wiederherstellen, wenn bei einem Clusterhost Fehler auftreten oder der Clusterhost offline geschaltet wird  
  
-   Ausgleichen der Netzwerklast, wenn Hosts hinzugefügt oder entfernt werden  
  
-   Wiederherstellen und Verteilen der Arbeitsauslastung innerhalb von 10 Sekunden  
  
### <a name="scalability"></a>Skalierbarkeit  
Die Skalierbarkeit ist ein Maß dafür, wie gut ein Computer, ein Dienst oder eine Anwendung an wachsende Leistungsanforderungen angepasst werden kann. In Bezug auf NLB-Cluster bedeutet Skalierbarkeit, dass dem vorhandenen Cluster schrittweise ein oder mehrere Systeme hinzugefügt werden können, wenn die Gesamtlast die Leistungsfähigkeit des Clusters überschreitet. Zur Unterstützung der Skalierbarkeit kann mit NLB Folgendes ausgeführt werden:  
  
-   Lastenausgleich von Anforderungen zum Laden in den NLB-Cluster für einzelne TCP\/IP-Dienste.  
  
-   Unterstützen von bis zu 32 Computern in einem einzigen Cluster  
  
-   Ausgleichen mehrerer serverlastanforderungen \(vom gleichen Client oder von verschiedenen Clients\) auf mehreren Hosts im Cluster.  
  
-   Hinzufügen von Hosts zum NLB-Cluster bei zunehmender Last ohne Ausfall des Clusters  
  
-   Entfernen von Hosts aus dem Cluster bei abnehmender Last  
  
-   Ermöglichen einer hohen Leistung und eines geringen Verwaltungsaufwands durch vollständige Pipelineimplementierung. Durch Pipelining können Anforderungen an den NLB-Cluster gesendet werden, ohne dass auf eine Antwort auf die vorher gesendete Anforderung gewartet werden muss.  
  
### <a name="manageability"></a>Verwaltbarkeit  
Zur Unterstützung der Verwaltbarkeit kann mit NLB Folgendes ausgeführt werden:  
  
-   Verwalten und konfigurieren Sie mehrere NLB-Cluster und die Clusterhosts über einen einzelnen Computer mithilfe von NLB-Manager oder das [Netzwerklastenausgleich (Network Load Balancing, NLB)-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/hh801274.aspx).
  
-   Festlegen des Lastausgleichsverhaltens für einen einzigen IP-Port oder eine Gruppe von Ports mit Portverwaltungsregeln  
  
-   Festlegen unterschiedlicher Portregeln für jede Website. Wenn Sie den gleichen Satz von Auslastung verwenden\-mit Lastenausgleich-Servern für mehrere Anwendungen oder Websites, Port-Regeln basieren auf der virtuellen IP-Zieladresse \(bei Verwendung virtueller Cluster\).  

-   Leiten Sie alle Clientanforderungen für einen einzelnen Host mit optionalen, einzelne\-Regeln zu hosten. NLB leitet Clientanforderungen an einen bestimmten Host weiter, auf dem bestimmte Anwendungen ausgeführt werden.  

-   Blockieren unerwünschter Netzwerkzugriffe auf bestimmte IP-Ports  

-   Internet Group Management Protocol aktivieren \(IGMP\) Unterstützung für die Clusterhosts zur Steuerung der Switchüberflutung \(, an die eingehende Netzwerkpakete an alle Ports auf dem Switch gesendet werden\) während des Betriebs in Multicast-Modus.  

-   Remotes Starten, Anhalten und Steuern der NLB-Aktionen mit Befehlen oder Skripten von Windows PowerShell  

-   Anzeigen des Windows-Ereignisprotokolls zur Überprüfung von NLB-Ereignissen. Alle Aktionen und Änderungen des Clusters werden von NLB im Ereignisprotokoll aufgeführt.  

## <a name="important-functionality"></a>Wichtige Funktionalität  
 
NLB ist als eine standardmäßige Windows Server-Netzwerktreiberkomponente installiert. Vorgänge sind für die TCP transparent\/IP-Netzwerkstapel. Die folgende Abbildung zeigt die Beziehung zwischen NLB und anderen Softwarekomponenten in einer typischen Konfiguration.  
  
![Netzwerklastenausgleich und andere Softwarekomponenten](../media/NLB/nlb.jpg)  
  
Im folgenden werden die wichtigsten Features des NLB.  
  
- Keine Erfordernis von Hardwareänderungen für die Ausführung.  
  
- Bereitstellung von NLB-Tools zur Konfiguration und Verwaltung mehrerer Cluster und aller Hosts von einem einzelnen Remote- oder lokalen Computer.  
  
- Ermöglicht Clients, auf den Cluster zugreifen, mithilfe eines einzigen, logischen Internetnamen und virtuelle IP-Adresse, bekannt als die IP-Clusteradresse \(individuelle Namen für jeden Computer bleiben\). Mit Netzwerklastausgleich sind mehrere virtuelle IP-Adressen für mehrfach vernetzte Server möglich.  
  
> [!NOTE]  
> Wenn Sie virtuelle Computer als virtuelle Cluster bereitstellen, erfordert NLB keine Server mehrfach vernetzt sein, um mehrere virtuelle IP-Adressen erhalten können.  
  
- Möglichkeit, dass NLB an mehrere Netzwerkadapter gebunden wird. Dadurch können Sie mehrere unabhängige Cluster auf den einzelnen Hosts konfigurieren. Die Unterstützung für mehrere Netzwerkadapter unterscheidet sich von der für virtuelle Cluster, da Sie bei virtuellen Clustern mehrere Cluster auf einem einzigen Netzwerkadapter konfigurieren können.  
  
- Keine Notwendigkeit von Änderungen der Serveranwendungen für die Ausführung in einem NLB-Cluster.  
  
- Möglichkeit der Konfiguration zum automatischen Hinzufügen eines Hosts zu dem Cluster, wenn dieser Clusterhost ausfällt und anschließend wieder online geschaltet wird. Der hinzugefügte Host kann mit der Verarbeitung von neuen Serveranforderungen von Clients beginnen.  
  
-   Möglichkeit der Offlineschaltung von Computern für vorbeugende Wartungsmaßnahmen ohne Beeinträchtigung des Clusterbetriebs auf den anderen Hosts.  
  
## <a name="hardware-requirements"></a>Hardwareanforderungen  
Es folgen die hardwareanforderungen zur Ausführung eines NLB-Clusters.  
  
-   Alle Hosts in dem Cluster müssen sich in demselben Subnetz befinden.  
  
-   Die Anzahl der Netzwerkadapter für jeden Host ist nicht eingeschränkt. Verschiedene Hosts können eine unterschiedliche Anzahl an Netzwerkadaptern aufweisen.  
  
-   In den einzelnen Clustern müssen alle Netzwerkadapter entweder Multicast- oder Unicastadressen aufweisen. NLB bietet keine Unterstützung für eine Umgebung, in der sowohl Multicast- als auch Unicastadressen in einem einzigen Cluster verwendet werden.  
  
-   Bei Verwendung von Unicast-Modus, den Netzwerkadapter, die verwendet wird, behandelt der Client\-zu\-Clusterdatenverkehr muss ändern die Media-Zugriffssteuerung unterstützt \(MAC\) Adresse.  
  
## <a name="software-requirements"></a>Softwareanforderungen  
Im folgenden werden die softwareanforderungen zum NLB-Cluster ausführen.  
  
-   Nur TCP\/IP-Adresse kann verwendet werden, auf dem Adapter für die auf jedem Host NLB aktiviert ist. Fügen Sie keine andere Protokolle \(z. B. IPX\) an diesen Adapter.  
  
-   Die IP-Adressen der Server in dem Cluster müssen statisch sein.  
  
> [!NOTE]  
> NLB bietet keine Unterstützung für Dynamic Host Configuration Protocol \(DHCP\). DHCP wird für jede zu konfigurierende Schnittstelle von NLB deaktiviert.  
  
## <a name="installation-information"></a>Informationen zur Installation  
Sie können NLB installieren, mithilfe von Server-Manager oder die Windows PowerShell-Befehle für den Netzwerklastenausgleich.

Optional können Sie auch die Tools für Netzwerklastenausgleich für die Verwaltung eines lokalen oder Remote-NLB-Clusters installieren. Die Tools beinhalten den Netzwerklastenausgleich-Manager "und" die NLB-Windows-PowerShell-Befehle.

### <a name="installation-with-server-manager"></a>Installation mit Server-Manager

Im Server-Manager können Hinzufügen von Rollen und Features-Assistenten zum Hinzufügen der **Netzwerklastenausgleich** Feature. Wenn Sie den Assistenten abgeschlossen haben, NLB installiert ist, und Sie müssen nicht den Computer neu starten.


### <a name="installation-with-windows-powershell"></a>Installation mit Windows PowerShell  

Um NLB mithilfe von Windows PowerShell zu installieren, führen Sie den folgenden Befehl an einer Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten auf dem Computer, in dem Sie NLB installieren möchten.

    
    Install-WindowsFeature NLB -IncludeManagementTools
    
Nachdem die Installation abgeschlossen ist, ist kein Neustart des Computers erforderlich.

Weitere Informationen finden Sie unter [Install-WindowsFeature](https://docs.microsoft.com/powershell/module/servermanager/install-windowsfeature?view=win10-ps).

### <a name="network-load-balancing-manager"></a>Netzwerklastenausgleich-Manager
Klicken Sie zum Öffnen des Netzwerklastenausgleich-Managers im Server-Manager auf **Extras**, und klicken Sie dann auf **Netzwerklastenausgleich-Manager**.
  
## <a name="additional-resources"></a>Zusätzliche Ressourcen  
Die folgende Tabelle enthält Links zu weiteren Informationen zum NLB-Feature.  
  
|Inhaltstyp|Verweise|  
|----------------|--------------|  
|Bereitstellung|[Für den Netzwerklastenausgleich-Bereitstellungshandbuch](https://technet.microsoft.com/library/cc754833(WS.10).aspx) &#124; [Konfigurieren des Netzwerklastenausgleichs mit Terminaldiensten](https://technet.microsoft.com/library/cc771300(v=WS.10).aspx)|  
|Vorgänge|[Verwalten von Netzwerklastenausgleich-Cluster](https://technet.microsoft.com/library/cc753954(WS.10).aspx) &#124; [Festlegen von Parametern für den Netzwerklastenausgleich](https://technet.microsoft.com/library/cc731619(WS.10).aspx) &#124; [Steuern von Hosts in Netzwerklastenausgleich-Cluster](https://technet.microsoft.com/library/cc770870(WS.10).aspx)|  
|Problembehandlung|[Problembehandlung für Netzwerklastenausgleich-Cluster](https://technet.microsoft.com/library/cc732592(WS.10).aspx) &#124; [NLB-Clusterereignisse und-Fehler](https://technet.microsoft.com/library/cc731678(WS.10).aspx)|
|Tools und Einstellungen|[Network Load Balancing Windows PowerShell-cmdlets](https://go.microsoft.com/fwlink/p/?LinkId=238123)|
|Communityressourcen|[Hohe Verfügbarkeit \(Clustering\) Forum](https://go.microsoft.com/fwlink/p/?LinkId=230641)
