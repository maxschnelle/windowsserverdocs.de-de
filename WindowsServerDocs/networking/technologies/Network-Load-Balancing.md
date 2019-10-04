---
title: Netzwerklastenausgleich
description: In diesem Thema erhalten Sie eine Übersicht über den Netzwerk Lastenausgleich \(nlb @ no__t-1-Feature in Windows Server 2016. Sie können NLB verwenden, um zwei oder mehr Server als einzelnen virtuellen Cluster zu verwalten. Mit NLB wird die Verfügbarkeit und Skalierbarkeit von Internet Server Anwendungen, wie z. b. den Web-, FTP-, Firewall-, Proxy-, virtuellen privaten Netzwerk \(vpn @ no__t-1 und anderen no__t-Servern (Mission @-) verbessert.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-nlb
ms.topic: article
ms.assetid: 244a4b48-06e5-4796-8750-a50e4f88ac72
ms.author: pashort
author: shortpatti
ms.date: 09/13/2018
ms.openlocfilehash: 4d79b6f29fbe64633bf04604ad586aff3dd86edf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405844"
---
# <a name="network-load-balancing"></a>Netzwerklastenausgleich

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erhalten Sie eine Übersicht über den Netzwerk Lastenausgleich \(nlb @ no__t-1-Feature in Windows Server 2016. Sie können NLB verwenden, um zwei oder mehr Server als einzelnen virtuellen Cluster zu verwalten. Mit NLB wird die Verfügbarkeit und Skalierbarkeit von Internet Server Anwendungen, wie z. b. den Web-, FTP-, Firewall-, Proxy-, virtuellen privaten Netzwerk \(vpn @ no__t-1 und anderen no__t-Servern (Mission @-) verbessert.  

> [!NOTE]
> Windows Server 2016 enthält eine neue von Azure inspirierte Software Load Balancer \(slb @ no__t-1 als Komponente der Software Defined Networking \(sdn @ no__t-3 Infrastructure. Verwenden Sie SLB anstelle von Netzwerk Lastenausgleich, wenn Sie Sdn verwenden, nicht-Windows-Workloads verwenden, die ausgehende Netzwerk Adressübersetzung \(nat @ no__t-1 benötigen, oder Sie benötigen Layer 3 \(l3 @ no__t-3 oder einen nicht-TCP-basierten Lastenausgleich. Sie können NLB weiterhin mit Windows Server 2016 für nicht-Sdn-bereit Stellungen verwenden. Weitere Informationen zu SLB finden Sie unter [Software Lastenausgleich (Software Load Balancing, SLB) für Sdn](../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md).

Der Netzwerk Lastenausgleich \(nlb @ no__t-1-Feature verteilt den Datenverkehr mithilfe des TCP @ no__t-2IP-Netzwerk Protokolls auf mehrere Server. Wenn Sie zwei oder mehr Computer, auf denen Anwendungen ausgeführt werden, in einem einzelnen virtuellen Cluster kombinieren, bietet NLB Zuverlässigkeit und Leistung für Webserver und andere unternehmenskritische Server (no__t).  
  
Die Server in einem NLB-Cluster werden als *Hosts*bezeichnet, und jeder Host führt eine separate Kopie der Serveranwendungen aus. Beim Netzwerklastenausgleich werden eingehende Clientanforderungen an die Hosts des Clusters verteilt. Sie können die Last konfigurieren, die von jedem Host behandelt werden soll. Sie können Hosts auch dynamisch dem Cluster hinzufügen, um erhöhte Lasten verarbeiten zu können. NLB kann auch den gesamten Datenverkehr zu einem einzelnen zugewiesenen Host weiterleiten. Dieser Host wird als *Standardhost* bezeichnet.  
  
Mit NLB können alle Computer eines Clusters mit derselben Gruppe von IP-Adressen adressiert werden. Dabei wird eine Gruppe von eindeutigen dedizierten IP-Adressen für jeden Host beibehalten. Wenn ein Host ausfällt oder offline geschaltet wird, wird die Last automatisch auf die Computer verteilt, die noch ausgeführt werden, wenn ein Host ausfällt oder offline geschaltet wird. Wenn der offline geschaltete Computer wieder bereit ist, kann er erneut transparent mit dem Cluster verbunden werden und seinen Teil der Arbeitsauslastung wieder aufnehmen. Dadurch muss von den anderen Computern weniger Datenverkehr verarbeitet werden.  
  
## <a name="practical-applications"></a>Praktische Anwendungsfälle  
Der Netzwerk Lastenausgleich ist hilfreich, um sicherzustellen, dass Zustands lose Anwendungen, wie z. b. Webserver, die Internetinformationsdienste \(iis @ no__t-1 ausführen, mit minimalen Ausfallzeiten verfügbar sind, und dass Sie durch Hinzufügen zusätzlicher Server als Last skali@no__t Erbar sind. erhöht @ no__t-3. In den folgenden Abschnitten wird beschrieben, wie NLB eine hohe Verfügbarkeit, Skalierbarkeit und Verwaltbarkeit der geclusterten Server unterstützt, auf denen diese Anwendungen ausgeführt werden.  
  
### <a name="high-availability"></a>Hohe Verfügbarkeit  
Ein System mit hoher Verfügbarkeit bietet zuverlässig einen akzeptablen Grad an Leistung mit minimaler Downtime. Um Hochverfügbarkeit zu gewährleisten, umfasst NLB integrierte @ no__t-0in-Funktionen, die automatisch folgende Aktionen ausführen können:  
  
-   Erkennen und Wiederherstellen, wenn bei einem Clusterhost Fehler auftreten oder der Clusterhost offline geschaltet wird  
  
-   Ausgleichen der Netzwerklast, wenn Hosts hinzugefügt oder entfernt werden  
  
-   Wiederherstellen und Verteilen der Arbeitsauslastung innerhalb von 10 Sekunden  
  
### <a name="scalability"></a>Skalierbarkeit  
Die Skalierbarkeit ist ein Maß dafür, wie gut ein Computer, ein Dienst oder eine Anwendung an wachsende Leistungsanforderungen angepasst werden kann. In Bezug auf NLB-Cluster bedeutet Skalierbarkeit, dass dem vorhandenen Cluster schrittweise ein oder mehrere Systeme hinzugefügt werden können, wenn die Gesamtlast die Leistungsfähigkeit des Clusters überschreitet. Zur Unterstützung der Skalierbarkeit kann mit NLB Folgendes ausgeführt werden:  
  
-   Ausgleichen Sie Ladeanforderungen für einzelne TCP @ no__t-0ip-Dienste über den NLB-Cluster.  
  
-   Unterstützen von bis zu 32 Computern in einem einzigen Cluster  
  
-   Lastenausgleich mehrerer Server Ladeanforderungen \(vom gleichen Client oder von mehreren Clients @ no__t-1 über mehrere Hosts im Cluster.  
  
-   Hinzufügen von Hosts zum NLB-Cluster bei zunehmender Last ohne Ausfall des Clusters  
  
-   Entfernen von Hosts aus dem Cluster bei abnehmender Last  
  
-   Ermöglichen einer hohen Leistung und eines geringen Verwaltungsaufwands durch vollständige Pipelineimplementierung. Durch Pipelining können Anforderungen an den NLB-Cluster gesendet werden, ohne dass auf eine Antwort auf die vorher gesendete Anforderung gewartet werden muss.  
  
### <a name="manageability"></a>Verwaltbarkeit  
Zur Unterstützung der Verwaltbarkeit kann mit NLB Folgendes ausgeführt werden:  
  
-   Verwalten und konfigurieren Sie mehrere NLB-Cluster und die Cluster Hosts auf einem einzelnen Computer mithilfe des NLB-Managers oder der [Cmdlets für den Netzwerk Lastenausgleich (Network Load Balancing, NLB) in Windows PowerShell](https://technet.microsoft.com/library/hh801274.aspx).
  
-   Festlegen des Lastausgleichsverhaltens für einen einzigen IP-Port oder eine Gruppe von Ports mit Portverwaltungsregeln  
  
-   Festlegen unterschiedlicher Portregeln für jede Website. Wenn Sie für mehrere Anwendungen oder Websites denselben Load @ no__t-Balanced-Server verwenden, basieren die Port Regeln auf der virtuellen Ziel-IP-Adresse \(Mithilfe der virtuellen Cluster @ no__t-2.  

-   Leiten Sie alle Client Anforderungen mithilfe optionaler, einzelner @ no__t-0host-Regeln an einen einzelnen Host weiter. NLB leitet Clientanforderungen an einen bestimmten Host weiter, auf dem bestimmte Anwendungen ausgeführt werden.  

-   Blockieren unerwünschter Netzwerkzugriffe auf bestimmte IP-Ports  

-   Aktivieren Sie das Internet Group Management Protocol \(igmp @ no__t-1-Unterstützung auf den Cluster Hosts, um die Überflutung von Switchports \( zu steuern, wobei eingehende Netzwerkpakete an alle Ports auf dem Switch @ no__t-3 gesendet werden, wenn der Multicast Modus ausgeführt wird.  

-   Remotes Starten, Anhalten und Steuern der NLB-Aktionen mit Befehlen oder Skripten von Windows PowerShell  

-   Anzeigen des Windows-Ereignisprotokolls zur Überprüfung von NLB-Ereignissen. Alle Aktionen und Änderungen des Clusters werden von NLB im Ereignisprotokoll aufgeführt.  

## <a name="important-functionality"></a>Wichtige Funktionalität  
 
NLB wird als standardmäßige Windows Server-Netzwerktreiber Komponente installiert. Die Vorgänge sind für den TCP @ no__t-0ip-Netzwerk Stapel transparent. In der folgenden Abbildung wird die Beziehung zwischen NLB und anderen Softwarekomponenten in einer typischen Konfiguration gezeigt.  
  
![Netzwerk Lastenausgleich und andere Softwarekomponenten](../media/NLB/nlb.jpg)  
  
Im folgenden finden Sie die primären Features von NLB.  
  
- Keine Erfordernis von Hardwareänderungen für die Ausführung.  
  
- Bereitstellung von NLB-Tools zur Konfiguration und Verwaltung mehrerer Cluster und aller Hosts von einem einzelnen Remote- oder lokalen Computer.  
  
- Ermöglicht Clients den Zugriff auf den Cluster mit einem einzelnen, logischen Internet Namen und einer virtuellen IP-Adresse, die als Cluster-IP-Adresse bezeichnet wird \(Sie behält die einzelnen Namen für jeden Computer @ no__t-1 bei. Mit Netzwerklastausgleich sind mehrere virtuelle IP-Adressen für mehrfach vernetzte Server möglich.  
  
> [!NOTE]  
> Wenn Sie virtuelle Computer als virtuelle Cluster bereitstellen, müssen Server nicht mehrfach vernetzt werden, um mehrere virtuelle IP-Adressen zu haben.  
  
- Möglichkeit, dass NLB an mehrere Netzwerkadapter gebunden wird. Dadurch können Sie mehrere unabhängige Cluster auf den einzelnen Hosts konfigurieren. Die Unterstützung für mehrere Netzwerkadapter unterscheidet sich von der für virtuelle Cluster, da Sie bei virtuellen Clustern mehrere Cluster auf einem einzigen Netzwerkadapter konfigurieren können.  
  
- Keine Notwendigkeit von Änderungen der Serveranwendungen für die Ausführung in einem NLB-Cluster.  
  
- Möglichkeit der Konfiguration zum automatischen Hinzufügen eines Hosts zu dem Cluster, wenn dieser Clusterhost ausfällt und anschließend wieder online geschaltet wird. Der hinzugefügte Host kann mit der Verarbeitung von neuen Serveranforderungen von Clients beginnen.  
  
-   Möglichkeit der Offlineschaltung von Computern für vorbeugende Wartungsmaßnahmen ohne Beeinträchtigung des Clusterbetriebs auf den anderen Hosts.  
  
## <a name="hardware-requirements"></a>Hardwareanforderungen  
Im folgenden sind die Hardwareanforderungen zum Ausführen eines NLB-Clusters aufgeführt.  
  
-   Alle Hosts in dem Cluster müssen sich in demselben Subnetz befinden.  
  
-   Die Anzahl der Netzwerkadapter für jeden Host ist nicht eingeschränkt. Verschiedene Hosts können eine unterschiedliche Anzahl an Netzwerkadaptern aufweisen.  
  
-   In den einzelnen Clustern müssen alle Netzwerkadapter entweder Multicast- oder Unicastadressen aufweisen. NLB bietet keine Unterstützung für eine Umgebung, in der sowohl Multicast- als auch Unicastadressen in einem einzigen Cluster verwendet werden.  
  
-   Wenn Sie den Unicastmodus verwenden, muss der Netzwerkadapter, der zum Verarbeiten von Client @ no__t-0to @ no__t-1cluster-Datenverkehr verwendet wird, das Ändern seiner Media Access Control \(mac @ no__t-3-Adresse unterstützen.  
  
## <a name="software-requirements"></a>Softwareanforderungen  
Im folgenden finden Sie die Softwareanforderungen für die Durchführung eines NLB-Clusters.  
  
-   Auf dem Adapter, für den NLB auf jedem Host aktiviert ist, kann nur TCP @ no__t-0ip verwendet werden. Fügen Sie diesem Adapter keine weiteren Protokolle \(z. b. IPX @ no__t-1 hinzu.  
  
-   Die IP-Adressen der Server in dem Cluster müssen statisch sein.  
  
> [!NOTE]  
> NLB unterstützt nicht das Dynamic Host Configuration-Protokoll \(dhcp @ no__t-1. DHCP wird für jede zu konfigurierende Schnittstelle von NLB deaktiviert.  
  
## <a name="installation-information"></a>Installationsinformationen  
Sie können NLB installieren, indem Sie entweder Server-Manager oder die Windows PowerShell-Befehle für NLB verwenden.

Optional können Sie auch die Tools für Netzwerklastenausgleich für die Verwaltung eines lokalen oder Remote-NLB-Clusters installieren. Zu den Tools gehören der Netzwerk Lastenausgleich-Manager und die Windows PowerShell-Befehle für den NLB.

### <a name="installation-with-server-manager"></a>Installation mit Server-Manager

In Server-Manager können Sie den Assistenten zum Hinzufügen von Rollen und Features verwenden, um die Funktion für den **Netzwerk Lastenausgleich** hinzuzufügen. Nachdem Sie den Assistenten beendet haben, wird NLB installiert, und Sie müssen den Computer nicht neu starten.


### <a name="installation-with-windows-powershell"></a>Installation mit Windows PowerShell  

Um NLB mithilfe von Windows PowerShell zu installieren, führen Sie den folgenden Befehl an einer Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten auf dem Computer aus, auf dem Sie NLB installieren möchten.

    
    Install-WindowsFeature NLB -IncludeManagementTools
    
Nach Abschluss der Installation ist kein Neustart des Computers erforderlich.

Weitere Informationen finden Sie unter [install-Windows Feature](https://docs.microsoft.com/powershell/module/servermanager/install-windowsfeature?view=win10-ps).

### <a name="network-load-balancing-manager"></a>Netzwerk Lastenausgleich-Manager
Klicken Sie zum Öffnen des Netzwerklastenausgleich-Managers im Server-Manager auf **Extras**, und klicken Sie dann auf **Netzwerklastenausgleich-Manager**.
  
## <a name="additional-resources"></a>Zusätzliche Ressourcen  
In der folgenden Tabelle finden Sie Links zu weiteren Informationen zum NLB-Feature.  
  
|Inhaltstyp|Verweise|  
|----------------|--------------|  
|Bereitstellung|[Bereitstellungs Handbuch](https://technet.microsoft.com/library/cc754833(WS.10).aspx) &#124; für den Netzwerk Lastenausgleich [Konfigurieren des Netzwerk Lastenausgleichs mit Terminal Diensten](https://technet.microsoft.com/library/cc771300(v=WS.10).aspx)|  
|Vorgänge|[Verwalten von Netzwerk Lastenausgleich-Clustern](https://technet.microsoft.com/library/cc753954(WS.10).aspx) &#124; [Festlegen von Parametern](https://technet.microsoft.com/library/cc731619(WS.10).aspx) &#124; für den Netzwerk Lastenausgleich [Steuern von Hosts auf](https://technet.microsoft.com/library/cc770870(WS.10).aspx) NLB|  
|Problembehandlung|Problembehandlung für [NLB-Cluster Ereignisse und-Fehler](https://technet.microsoft.com/library/cc731678(WS.10).aspx) in [Netzwerk Lastenausgleich](https://technet.microsoft.com/library/cc732592(WS.10).aspx) &#124;|
|Tools und Einstellungen|[Windows PowerShell-Cmdlets für den Netzwerk Lastenausgleich](https://go.microsoft.com/fwlink/p/?LinkId=238123)|
|Communityressourcen|[Hochverfügbarkeit \(clustering @ no__t-2 Forum](https://go.microsoft.com/fwlink/p/?LinkId=230641)
