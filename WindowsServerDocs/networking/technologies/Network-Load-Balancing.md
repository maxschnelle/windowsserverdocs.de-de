---
title: Netzwerklastenausgleich
description: Dieses Thema enthält eine Übersicht über das Feature Netzwerklastenausgleich (Network Load Balancing, NLB) in Windows Server 2016 und enthält Links zu weiteren Anleitungen zum Erstellen, konfigurieren und Verwalten von NLB-Clustern.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-nlb
ms.topic: article
ms.assetid: 244a4b48-06e5-4796-8750-a50e4f88ac72
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b9fd39381316a8bcd06328e7aa75492ed99bc7f1
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="network-load-balancing"></a>Netzwerklastenausgleich

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Thema enthält eine Übersicht über das Feature Netzwerklastenausgleich \(NLB\) in Windows Server 2016 und enthält Links zu weiteren Anleitungen zum Erstellen, konfigurieren und Verwalten von NLB-Clustern.

NLB können Sie zwei oder mehr Servern als einzelnen virtuellen Cluster verwalten. NLB verbessert die Verfügbarkeit und Skalierbarkeit von Internet-serveranwendungen wie im Web, FTP verwendeten, firewall, Proxyserver, virtuelle Private Netzwerk-\(VPN\) und andere wichtige Mission\.   

>[!NOTE]
>Windows Server 2016 enthält ein neues Azure inspiriert Software Load Balancers \(SLB\) als Komponente der \(SDN\) Software Defined Networking-Infrastruktur. Verwendung SLB anstelle von NLB bei Verwendung von SDN, nicht-Windows-Arbeitslasten verwenden, benötigen Sie ausgehende Netzwerkadressübersetzung \(NAT\), oder Layer 3-\(L3\) oder nicht-TCP-basierte Lastenausgleich erforderlich. Sie können weiterhin NLB für nicht-SDN-Bereitstellungen mit Windows Server 2016 verwenden. Weitere Informationen zu SLB, finden Sie unter [Software Load Balancing (SLB) für SDN](../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md).

Das Feature Netzwerklastenausgleich \(NLB\) verteilt den Datenverkehr mithilfe des TCP/IP TCP/IP-Netzwerkprotokolls über mehrere Server. Durch die Kombination von zwei oder mehr Computer, auf denen eine Anwendung in einem einzelnen virtuellen Cluster ausgeführt werden, bietet NLB Zuverlässigkeit und Leistung für Webserver und andere wichtige Mission\ Server.  
  
Die Server in einem NLB-Cluster werden als bezeichnet *Hosts*, und jeder Host führt eine separate Kopie der serveranwendungen. Netzwerklastenausgleich werden eingehende Clientanforderungen auf die Hosts im Cluster verteilt. Sie können die Last konfigurieren, die von jedem Host behandelt werden sollen. Sie können auch dynamisch Hosts des Clusters um erhöhte Lasten verarbeiten hinzufügen. NLB kann auch der gesamte Datenverkehr zu einem einzelnen zugewiesenen Host, die aufgerufen wird, leiten die *Standardhost*.  
  
NLB kann alle Computer im Cluster mit den gleichen Satz von IP-Adressen adressiert werden, und es wird eine Gruppe von eindeutigen dedizierten IP-Adressen für jeden Host beibehalten. Für Anwendungen Load\ mit Lastenausgleich Wenn ein Host ausfällt oder offline geschaltet wird, wird die Last automatisch zwischen den Computern verteilt, die weiterhin ausgeführt werden. Wenn es bereit ist, kann die offline-Computer transparent treten Sie dem Cluster und erneuten seinen Anteil an die Arbeitslast, wodurch die anderen Computer im Cluster weniger Datenverkehr verarbeitet.  
  
## <a name="BKMK_APP"></a>In der Praxis  
NLB ist hilfreich, um sicherzustellen, dass statusfreie Anwendungen, beispielsweise Webserver, die unter Internetinformationsdienste \(IIS\) mit minimaler Downtime verfügbar sind, und skalierbar sind \ (durch Hinzufügen weiterer Server als die Load-Increases\). In den folgenden Abschnitten wird beschrieben, wie NLB unterstützt wird, eine hohe Verfügbarkeit, Skalierbarkeit und verwaltbarkeit der geclusterten Server, auf denen diese Anwendungen ausgeführt.  
  
### <a name="high-availability"></a>Hohe Verfügbarkeit  
Ein System mit hoher Verfügbarkeit bietet zuverlässig einen akzeptablen Grad an Leistung mit minimaler Downtime. Eine hohe Verfügbarkeit zu bieten, umfasst NLB integrierten Features, die automatisch können:  
  
-   Erkennen eines Clusterhosts, der ausfällt oder offline geschaltet, und klicken Sie dann wiederhergestellt werden.  
  
-   Ausgleichen der Netzwerklast, wenn Hosts hinzugefügt oder entfernt werden.  
  
-   Wiederherstellen und Verteilen der arbeitsauslastung innerhalb von 10 Sekunden.  
  
### <a name="scalability"></a>Skalierbarkeit  
Skalierbarkeit ist ein Maß dafür, wie gut ein Computer, den Dienst oder die Anwendung an wachsende leistungsanforderungen angepasst haben kann. NLB-Cluster ist Skalierbarkeit die Möglichkeit, ein oder mehrere Systeme inkrementell zu einem vorhandenen Cluster hinzufügen, wenn die Gesamtauslastung des Clusters seine Funktionen überschreitet. Zur Unterstützung der Skalierbarkeit, können Sie mit NLB Folgendes tun:  
  
-   Guthaben lastanforderungen des NLB-Clusters für einzelne TCP/IP TCP/IP-Dienste.  
  
-   Unterstützt bis zu 32 Computern in einem einzigen Cluster.  
  
-   Ausgleichen mehrerer serverlastanforderungen \ (vom gleichen Client oder von mehreren Clients\) auf mehreren Hosts im Cluster.  
  
-   Hinzufügen von Hosts zum NLB-Cluster zunehmender Last ohne Ausfall des Clusters fehlschlägt.  
  
-   Entfernen von Hosts aus dem Cluster bei abnehmender Last.  
  
-   Aktivieren Sie eine hohe Leistung und eines geringen Verwaltungsaufwands durch vollständige pipelineimplementierung. Durch Pipelining können Anforderungen an den NLB-Cluster gesendet werden, ohne dass eine Antwort auf eine vorherige Anforderung gewartet.  
  
### <a name="manageability"></a>Verwaltbarkeit  
Zur Unterstützung der Verwaltbarkeit können Sie mit NLB Folgendes tun:  
  
-   Verwalten und konfigurieren Sie mehrere NLB-Cluster und die Clusterhosts über einen einzelnen Computer mithilfe des NLB-Managers oder der [(Network Load Balancing, NLB)-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/hh801274.aspx).
  
-   Geben Sie den NLB-Verhalten für einen IP-Port oder eine Gruppe von Ports mit Portverwaltungsregeln.  
  
-   Definieren Sie verschiedene Portregeln für jede Website. Wenn Sie den gleichen Satz von Load\-Servern für mehrere Anwendungen oder Websites verwenden, basieren die Portregeln auf der virtuellen Ziel-IP-Adresse \(using virtual clusters\).  

-   Leiten Sie alle Clientanforderungen auf einen einzelnen Host mithilfe optionaler, Singlethread-Host-Regeln. NLB leitet Clientanforderungen an einen bestimmten Host, der bestimmte Anwendungen ausgeführt werden.  

-   Netzwerkzugriffe auf bestimmte IP-Ports zu blockieren.  

-   Aktivieren der Unterstützung von Internet Group Management Protocol \(IGMP\) auf den Clusterhosts zur Steuerung der Switchüberflutung \ (, werden eingehende Netzwerkpakete an alle Ports auf dem die Switch\ gesendet) im Multicastmodus fungierte.  

-   Starten, beenden und NLB-Aktionen mithilfe von Windows PowerShell-Befehle oder Skripts remote steuern.  

-   Zeigen Sie das Windows-Ereignisprotokoll, um NLB-Ereignisse zu überprüfen. NLB werden alle Aktionen und Änderungen der Cluster im Ereignisprotokoll protokolliert.  

## <a name="important-functionality"></a>Wichtige Funktionen  
 
NLB wird als eine standardmäßige Windows Server-Netzwerktreiberkomponente installiert. Die Vorgänge sind für den TCP/IP TCP/IP-Netzwerkstapel transparent. Die folgende Abbildung zeigt die Beziehung zwischen NLB und anderen Softwarekomponenten in einer typischen Konfiguration.  
  
![Netzwerklastenausgleich und andere Softwarekomponenten](../media/NLB/nlb.jpg)  
  
Im folgenden werden die wichtigsten Features von NLB.  
  
- Erfordert keine Änderung der Hardware ausgeführt.  
  
- Bietet Tools für den Netzwerklastenausgleich zur Konfiguration und Verwaltung mehrerer Cluster und alle Hosts von einem einzelnen Remote- oder lokalen Computer.  
  
- Ermöglicht Clients den Zugriff auf den Cluster mit einem einzelnen, logischen Internetnamen und virtuelle IP-Adresse, der als die Cluster-IP-Adresse bekannt ist \ (individuelle Namen für die einzelnen Computer\ werden beibehalten). NLB kann mehrere virtuelle IP-Adressen für mehrfach vernetzte Server.  
  
> [!NOTE]  
> Wenn Sie virtuelle Computer als virtuelle Cluster bereitstellen, ist NLB Server mehrfach vernetzt sein, damit mehrere virtuelle IP-Adressen können nicht erforderlich.  
  
- Können NLB an mehrere Netzwerkadapter gebunden werden soll, dem Sie mehrere unabhängige Cluster auf jedem Host konfigurieren kann. Unterstützung für mehrere Netzwerkadapter unterscheidet sich von virtuellen Clustern, in diesem virtuelle Clustern mehrere Cluster auf einem einzelnen Netzwerkadapter konfigurieren können.  
  
- Erfordert keine Änderungen für serveranwendungen, so, dass sie in einem NLB-Cluster ausgeführt werden können.  
  
- Kann konfiguriert werden, um automatisch hinzugefügt, dass ein Host dem Cluster, wenn dieser Clusterhost ausfällt und anschließend wieder online geschaltet. Der hinzugefügte Host kann die Verarbeitung von neuen serveranforderungen von Clients gestartet.  
  
-   Können Sie Computer für vorbeugende Wartungsmaßnahmen offline ohne des clusterbetriebs auf den anderen Hosts dauern.  
  
## <a name="BKMK_HARD"></a>Hardwareanforderungen  
Im folgenden werden die hardwareanforderungen zur Ausführung eines NLB-Clusters.  
  
-   Alle Hosts im Cluster müssen sich im gleichen Subnetz befinden.  
  
-   Es besteht keine Einschränkung hinsichtlich der Anzahl der Netzwerkadapter auf jedem Host, und verschiedene Hosts können eine unterschiedliche Anzahl an Netzwerkadaptern aufweisen.  
  
-   In den einzelnen Clustern müssen alle Netzwerkadapter entweder Multicast- oder Unicastadressen sein. NLB bietet keine Unterstützung für eine gemischte Umgebung mit Multicast- und in einem einzigen Cluster.  
  
-   Wenn Sie die Unicast-Modus verwenden, muss der Netzwerkadapter, der verwendet wird, um die Client-zu-Cluster-Datenverkehr behandeln Ändern seiner Mac-\(MAC\) Adresse unterstützen.  
  
## <a name="BKMK_SOFT"></a>Anforderungen der Clientsoftware  
Im folgenden werden die softwareanforderungen zum Ausführen eines NLB-Clusters.  
  
-   Nur TCP\IP kann auf dem Adapter verwendet werden, für die NLB auf jedem Host aktiviert ist. Fügen Sie keine weiteren Protokolle nicht \ (z. B. IPX\) zu diesem Adapter.  
  
-   Die IP-Adressen der Server im Cluster müssen statisch sein.  
  
> [!NOTE]  
> NLB bietet keine Unterstützung für Dynamic Host Configuration-Protokoll \(DHCP\). NLB deaktiviert DHCP auf jede Schnittstelle, die konfiguriert werden.  
  
## <a name="BKMK_INSTALL"></a>Informationen zur Installation  
Sie können NLB mithilfe von Server-Manager oder Windows PowerShell-Befehle für den Netzwerklastenausgleich installieren.

Optional können Sie die Tools für den Netzwerklastenausgleich zum Verwalten von einem lokalen oder Remotecomputer NLB-Cluster installieren. Die Tools beinhalten den Netzwerklastenausgleich-Manager und NLB Windows PowerShell-Befehle.

### <a name="installation-with-server-manager"></a>Installation mit Server-Manager

Im Server-Manager können das Hinzufügen von Rollen und Features Assistenten zum Hinzufügen der **Network Load Balancing** Feature. Beim Ausführen des Assistenten NLB installiert ist, und Sie müssen nicht auf den Computer neu starten.


### <a name="installation-with-windows-powershell"></a>Installation mit WindowsPowerShell  

Um NLB mithilfe von Windows PowerShell zu installieren, führen Sie den folgenden Befehl an einer Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten auf dem Computer, der Sie NLB installieren möchten.

    
    Install-WindowsFeature NLB -IncludeManagementTools
    
Nach Abschluss der Installation ist kein Neustart des Computers erforderlich.

Weitere Informationen finden Sie unter [Install-WindowsFeature](https://technet.microsoft.com/library/jj205467.aspx).

### <a name="network-load-balancing-manager"></a>Netzwerklastenausgleich-Manager
Klicken Sie zum Öffnen des Netzwerklastenausgleich-Managers im Server-Manager **Tools**, und klicken Sie dann auf **des Netzwerklastenausgleich-Managers**.
  
## <a name="BKMK_LINKS"></a>Zusätzliche Ressourcen  
Die folgende Tabelle enthält Links zu weiteren Informationen zum NLB-Feature.  
  
|Inhaltstyp|Verweise|  
|----------------|--------------|  
|Bereitstellung|[Für den Netzwerklastenausgleich-Bereitstellungshandbuch](https://technet.microsoft.com/library/cc754833(WS.10).aspx) & #124; [Konfigurieren des Netzwerklastenausgleichs mit Terminaldiensten](https://technet.microsoft.com/library/cc771300(v=WS.10).aspx)|  
|Vorgänge|[Verwalten von Netzwerklastenausgleich-Clustern](https://technet.microsoft.com/library/cc753954(WS.10).aspx) & #124; [Festlegen von Parametern für den Netzwerklastenausgleich](https://technet.microsoft.com/library/cc731619(WS.10).aspx) & #124; [Steuern von Hosts in Netzwerklastenausgleich-Cluster](https://technet.microsoft.com/library/cc770870(WS.10).aspx)|  
|Problembehandlung|[Problembehandlung für Netzwerklastenausgleich-Clustern](https://technet.microsoft.com/library/cc732592(WS.10).aspx) & #124; [NLB-Clusterereignisse und-Fehler](https://technet.microsoft.com/library/cc731678(WS.10).aspx)|
|Tools und Einstellungen|[Network Load Balancing Windows PowerShell-cmdlets](https://go.microsoft.com/fwlink/p/?LinkId=238123)|
|Community-Ressourcen|[Forum für hohe Verfügbarkeit \(Clustering\)](https://go.microsoft.com/fwlink/p/?LinkId=230641)