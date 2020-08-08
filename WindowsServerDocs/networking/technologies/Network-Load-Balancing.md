---
title: Netzwerklastenausgleich
description: In diesem Thema erhalten Sie eine Übersicht über das NLB-Feature für den Netzwerk Lastenausgleich \( \) in Windows Server 2016. Sie können NLB verwenden, um zwei oder mehr Server als einzelnen virtuellen Cluster zu verwalten. Mit NLB wird die Verfügbarkeit und Skalierbarkeit von Internet Server Anwendungen verbessert, wie z. b. für Web-, FTP-, Firewall-, Proxy \( -, VPN \) -und andere Unternehmens \- kritische Server.
manager: dougkim
ms.topic: article
ms.assetid: 244a4b48-06e5-4796-8750-a50e4f88ac72
ms.author: lizross
author: eross-msft
ms.date: 09/13/2018
ms.openlocfilehash: 4417748504a0458396cd02e965547c2573f2c44f
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87990087"
---
# <a name="network-load-balancing"></a>Netzwerklastenausgleich

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erhalten Sie eine Übersicht über das NLB-Feature für den Netzwerk Lastenausgleich \( \) in Windows Server 2016. Sie können NLB verwenden, um zwei oder mehr Server als einzelnen virtuellen Cluster zu verwalten. Mit NLB wird die Verfügbarkeit und Skalierbarkeit von Internet Server Anwendungen verbessert, wie z. b. für Web-, FTP-, Firewall-, Proxy \( -, VPN \) -und andere Unternehmens \- kritische Server.

> [!NOTE]
> Windows Server 2016 enthält eine neue, von Azure inspirierte Software Load Balancer \( SLB \) als Komponente der Software Defined Networking \( Sdn \) Infrastructure. Verwenden Sie SLB anstelle von Netzwerk Lastenausgleich, wenn Sie Sdn verwenden, nicht-Windows-Workloads verwenden, ausgehende Netzwerkadressen Übersetzung benötigen \( \) oder Layer 3 \( L3 \) -oder nicht-TCP-basierten Lastenausgleich benötigen. Sie können NLB weiterhin mit Windows Server 2016 für nicht-Sdn-bereit Stellungen verwenden. Weitere Informationen zu SLB finden Sie unter [Software Lastenausgleich (Software Load Balancing, SLB) für Sdn](../sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn.md).

Mit dem \( NLB-Feature für den Netzwerk Lastenausgleich \) wird der Datenverkehr mithilfe des TCP \/ IP-Netzwerk Protokolls auf mehrere Server verteilt. Wenn Sie zwei oder mehr Computer, auf denen Anwendungen ausgeführt werden, in einem einzelnen virtuellen Cluster kombinieren, bietet NLB Zuverlässigkeit und Leistung für Webserver und andere Unternehmens \- kritische Server.

Die Server in einem NLB-Cluster werden als *Hosts* bezeichnet, und jeder Host führt eine separate Kopie der Serveranwendungen aus. Beim Netzwerklastenausgleich werden eingehende Clientanforderungen an die Hosts des Clusters verteilt. Sie können die Last konfigurieren, die von jedem Host behandelt werden soll. Sie können Hosts auch dynamisch dem Cluster hinzufügen, um erhöhte Lasten verarbeiten zu können. NLB kann auch den gesamten Datenverkehr zu einem einzelnen zugewiesenen Host weiterleiten. Dieser Host wird als *Standardhost* bezeichnet.

Mit NLB können alle Computer eines Clusters mit derselben Gruppe von IP-Adressen adressiert werden. Dabei wird eine Gruppe von eindeutigen dedizierten IP-Adressen für jeden Host beibehalten. Wenn bei Anwendungen mit Lastenausgleich \- ein Host ausfällt oder offline geschaltet wird, wird die Last automatisch auf die Computer verteilt, die noch ausgeführt werden. Wenn der offline geschaltete Computer wieder bereit ist, kann er erneut transparent mit dem Cluster verbunden werden und seinen Teil der Arbeitsauslastung wieder aufnehmen. Dadurch muss von den anderen Computern weniger Datenverkehr verarbeitet werden.

## <a name="practical-applications"></a>Praktische Anwendung
Der Netzwerk Lastenausgleich ist hilfreich, um sicherzustellen, dass Zustands lose Anwendungen, wie z. b. Webserver \( , die Internetinformationsdienste IIS ausführen \) , mit minimalen Ausfallzeiten verfügbar sind und dass Sie \( durch Hinzufügen zusätzlicher Server bei steigender Auslastung skalierbar sind \) . In den folgenden Abschnitten wird beschrieben, wie NLB eine hohe Verfügbarkeit, Skalierbarkeit und Verwaltbarkeit der geclusterten Server unterstützt, auf denen diese Anwendungen ausgeführt werden.

### <a name="high-availability"></a>Hochverfügbarkeit
Ein System mit hoher Verfügbarkeit bietet zuverlässig einen akzeptablen Grad an Leistung mit minimaler Downtime. Zum Bereitstellen von Hochverfügbarkeit umfasst NLB integrierte \- Features, die automatisch folgende Aktionen ausführen können:

-   Erkennen und Wiederherstellen, wenn bei einem Clusterhost Fehler auftreten oder der Clusterhost offline geschaltet wird

-   Ausgleichen der Netzwerklast, wenn Hosts hinzugefügt oder entfernt werden

-   Wiederherstellen und Verteilen der Arbeitsauslastung innerhalb von 10 Sekunden

### <a name="scalability"></a>Skalierbarkeit
Die Skalierbarkeit ist ein Maß dafür, wie gut ein Computer, ein Dienst oder eine Anwendung an wachsende Leistungsanforderungen angepasst werden kann. In Bezug auf NLB-Cluster bedeutet Skalierbarkeit, dass dem vorhandenen Cluster schrittweise ein oder mehrere Systeme hinzugefügt werden können, wenn die Gesamtlast die Leistungsfähigkeit des Clusters überschreitet. Zur Unterstützung der Skalierbarkeit kann mit NLB Folgendes ausgeführt werden:

-   Ausgleichen Sie Ladeanforderungen für einzelne TCP \/ -IP-Dienste über den NLB-Cluster.

-   Unterstützen von bis zu 32 Computern in einem einzigen Cluster

-   Ausgleichen mehrerer Server Ladeanforderungen \( vom gleichen Client oder von mehreren Clients \) über mehrere Hosts im Cluster.

-   Hinzufügen von Hosts zum NLB-Cluster bei zunehmender Last ohne Ausfall des Clusters

-   Entfernen von Hosts aus dem Cluster bei abnehmender Last

-   Ermöglichen einer hohen Leistung und eines geringen Verwaltungsaufwands durch vollständige Pipelineimplementierung. Durch Pipelining können Anforderungen an den NLB-Cluster gesendet werden, ohne dass auf eine Antwort auf die vorher gesendete Anforderung gewartet werden muss.

### <a name="manageability"></a>Verwaltbarkeit
Zur Unterstützung der Verwaltbarkeit kann mit NLB Folgendes ausgeführt werden:

-   Verwalten und konfigurieren Sie mehrere NLB-Cluster und die Cluster Hosts auf einem einzelnen Computer mithilfe des NLB-Managers oder der [Cmdlets für den Netzwerk Lastenausgleich (Network Load Balancing, NLB) in Windows PowerShell](/previous-versions/windows/powershell-scripting/hh801274(v=wps.630)).

-   Festlegen des Lastausgleichsverhaltens für einen einzigen IP-Port oder eine Gruppe von Ports mit Portverwaltungsregeln

-   Festlegen unterschiedlicher Portregeln für jede Website. Wenn Sie dieselbe Gruppe von Servern mit Lastenausgleich \- für mehrere Anwendungen oder Websites verwenden, basieren die Port Regeln auf der virtuellen Ziel-IP-Adresse, die \( Virtuelle Cluster verwendet \) .

-   Leiten Sie alle Client Anforderungen mithilfe optionaler, einzelner Host Regeln an einen einzelnen Host weiter \- . NLB leitet Clientanforderungen an einen bestimmten Host weiter, auf dem bestimmte Anwendungen ausgeführt werden.

-   Blockieren unerwünschter Netzwerkzugriffe auf bestimmte IP-Ports

-   Aktivieren \( Sie die IGMP-Unterstützung für das Internet Group Management-Protokoll \) auf den Cluster Hosts, um die Überflutung des Switchports zu steuern, \( bei der eingehende Netzwerkpakete an alle Ports auf dem Switch gesendet werden, \) Wenn

-   Remotes Starten, Anhalten und Steuern der NLB-Aktionen mit Befehlen oder Skripten von Windows PowerShell

-   Anzeigen des Windows-Ereignisprotokolls zur Überprüfung von NLB-Ereignissen. Alle Aktionen und Änderungen des Clusters werden von NLB im Ereignisprotokoll aufgeführt.

## <a name="important-functionality"></a>Wichtige Funktionalität

NLB wird als standardmäßige Windows Server-Netzwerktreiber Komponente installiert. Die Vorgänge sind für den TCP \/ -IP-Netzwerk Stapel transparent. In der folgenden Abbildung wird die Beziehung zwischen NLB und anderen Softwarekomponenten in einer typischen Konfiguration gezeigt.

![Netzwerk Lastenausgleich und andere Softwarekomponenten](../media/NLB/nlb.jpg)

Im folgenden finden Sie die primären Features von NLB.

- Keine Erfordernis von Hardwareänderungen für die Ausführung.

- Bereitstellung von NLB-Tools zur Konfiguration und Verwaltung mehrerer Cluster und aller Hosts von einem einzelnen Remote- oder lokalen Computer.

- Ermöglicht Clients den Zugriff auf den Cluster mit einem einzelnen, logischen Internet Namen und einer virtuellen IP-Adresse, die als Cluster-IP-Adresse bezeichnet wird \( . Sie behält die einzelnen Namen für jeden Computer bei \) . Mit Netzwerklastausgleich sind mehrere virtuelle IP-Adressen für mehrfach vernetzte Server möglich.

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

-   Wenn Sie den Unicastmodus verwenden, muss der Netzwerkadapter, der zum Verarbeiten von Datenverkehr zwischen Client und Cluster verwendet wird, das \- \- Ändern seiner Media Access Control MAC-Adresse unterstützen \( \) .

## <a name="software-requirements"></a>Softwareanforderungen
Im folgenden finden Sie die Softwareanforderungen für die Durchführung eines NLB-Clusters.

-   \/Auf dem Adapter, für den NLB auf jedem Host aktiviert ist, kann nur TCP IP verwendet werden. Fügen Sie diesem Adapter keine anderen Protokolle \( , z. b. IPX, hinzu \) .

-   Die IP-Adressen der Server in dem Cluster müssen statisch sein.

> [!NOTE]
> NLB unterstützt nicht das Dynamic Host Configuration-Protokoll \( DHCP \) . DHCP wird für jede zu konfigurierende Schnittstelle von NLB deaktiviert.

## <a name="installation-information"></a>Installationsinformationen
Sie können NLB installieren, indem Sie entweder Server-Manager oder die Windows PowerShell-Befehle für NLB verwenden.

Optional können Sie auch die Tools für Netzwerklastenausgleich für die Verwaltung eines lokalen oder Remote-NLB-Clusters installieren. Zu den Tools gehören der Netzwerk Lastenausgleich-Manager und die Windows PowerShell-Befehle für den NLB.

### <a name="installation-with-server-manager"></a>Installation mit Server-Manager

In Server-Manager können Sie den Assistenten zum Hinzufügen von Rollen und Features verwenden, um die Funktion für den **Netzwerk Lastenausgleich** hinzuzufügen. Nachdem Sie den Assistenten beendet haben, wird NLB installiert, und Sie müssen den Computer nicht neu starten.


### <a name="installation-with-windows-powershell"></a>Installation mit Windows PowerShell

Um NLB mithilfe von Windows PowerShell zu installieren, führen Sie den folgenden Befehl an einer Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten auf dem Computer aus, auf dem Sie NLB installieren möchten.

```powershell
Install-WindowsFeature NLB -IncludeManagementTools
```

Nach Abschluss der Installation ist kein Neustart des Computers erforderlich.

Weitere Informationen finden Sie unter [Install-WindowsFeature](/powershell/module/servermanager/install-windowsfeature?view=win10-ps).

### <a name="network-load-balancing-manager"></a>Netzwerk Lastenausgleich-Manager
Klicken Sie zum Öffnen des Netzwerklastenausgleich-Managers im Server-Manager auf **Extras**, und klicken Sie dann auf **Netzwerklastenausgleich-Manager**.

## <a name="additional-resources"></a>Weitere Ressourcen
In der folgenden Tabelle finden Sie Links zu weiteren Informationen zum NLB-Feature.

|Inhaltstyp|Referenzen|
|----------------|--------------|
|Bereitstellung|[Bereitstellungs Handbuch für den Netzwerk Lastenausgleich](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754833(v=ws.10)) &#124; [Konfigurieren des Netzwerk Lastenausgleichs mit Terminal Diensten](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771300(v=ws.10))|
|Operationen (Operations)|[Verwalten von Netzwerk Lastenausgleich-Clustern](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753954(v=ws.10)) &#124; [Festlegen von Netzwerk Lastenausgleich-Parametern](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731619(v=ws.10)) &#124; [Steuern von Hosts auf Netzwerk Lastenausgleich](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770870(v=ws.10))|
|Problembehandlung|[Problembehandlung für Netzwerk Lastenausgleichs-Cluster](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732592(v=ws.10)) &#124; [NLB-Cluster Ereignisse und-Fehler](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731678(v=ws.10))|
|Tools und Einstellungen|[Windows PowerShell-Cmdlets für den Netzwerklastenausgleich](https://go.microsoft.com/fwlink/p/?LinkId=238123)|
|Communityressourcen|[\(Clustering-Forum für Hochverfügbarkeit \)](https://go.microsoft.com/fwlink/p/?LinkId=230641)