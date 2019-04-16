---
title: "Cluster-Aware Updating (Übersicht)"
ms.topic: article
ms.prod: windows-server-threshold
ms.manager: dongill
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 3/23/2017
description: Cluster-Aware Updating, CAU automatisiert die Installation von Softwareupdates auf Clustern unter Windows Server.
ms.assetid: 3c2993b4-aa81-452b-a5c3-3724ad95d892
ms.openlocfilehash: 68336741accabd6e4cb0da5dbd708be707f68df6
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="cluster-aware-updating-overview"></a>Cluster-Aware Updating (Übersicht)

> Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server2016, Windows Server2012 R2, Windows Server 2012

Dieses Thema enthält eine Übersicht über \(CAU\) Cluster\-Aware Updating, ein Feature, das der softwareaktualisierungsprozess auf Clusterservern unter Aufrechterhaltung der Verfügbarkeit automatisiert.

> [!NOTE]
> Beim Aktualisieren von ["direkte Speicherplätze"](../storage/storage-spaces/storage-spaces-direct-overview.md) Clustern, empfehlen wir die Verwendung des clusterfähigen Aktualisierens.
  
## <a name="BKMK_OVER"></a>Featurebeschreibung  
Cluster-Aware Updating ist ein automatisiertes Feature zur Aktualisierung von Servern in einer [Failovercluster](failover-clustering-overview.md) mit wenig oder keinen verfügbarkeitseinbußen Verfügbarkeit während des Updates. Während einer Updateausführung Cluster-Aware Updating transparent die folgenden Aufgaben ausgeführt:  

1. Fügt jedem Knoten des Clusters in den Wartungsmodus Knoten.
2. Verschiebt die Clusterrollen aus dem Knoten.
3. Die Updates und aller abhängigen Updates installiert.
4. Ein Neustart durchgeführt, falls erforderlich.
5. Zeigt den Knoten aus dem Wartungsmodus.
6. Wiederherstellen der Clusterrollen auf dem Knoten an.
7. Wechselt zum nächsten Knoten zu aktualisieren.

Für viele Clusterrollen im Cluster löst der automatische Updateprozess ein geplantes Failover aus. Dies kann eine vorübergehende dienstunterbrechung für angeschlossene Clients verursachen. Allerdings bei fortlaufend verfügbaren Arbeitsauslastungen, z.B. Hyper\-V mit Livemigration oder Dateiserver mit SMB Transparent Failover Cluster-Aware Updating clusteraktualisierungen ohne Auswirkungen auf die dienstverfügbarkeit koordiniert werden.    
  
## <a name="practical-applications"></a>In der Praxis  
  
-   CAU reduziert Dienstausfälle in geclusterten Diensten, verringert den Bedarf an manuellen Problemumgehungen bei der Aktualisierung und macht die zur Implementierung-zu-Ende-Clusteraktualisierung Verlässlichkeit für den Administrator. Wenn das CAU-Feature verwendet wird, in Verbindung mit stets verfügbaren Arbeitsauslastungen, z.B. stets verfügbaren Dateiservern \ (dateiserverauslastung mit SMB Transparent Failover\) oder Hyper\-V, den Cluster Updates mit für Clients ohne Auswirkungen auf die dienstverfügbarkeit ausgeführt werden können.  
  
-   CAU vereinfacht die Übernahme von einheitlichen IT-Prozessen im Unternehmen. Updateausführungsprofile kann dann zentral auf einer Dateifreigabe, um sicherzustellen, dass Updates von CAU-Bereitstellungen in der gesamten IT-Organisation einheitlich angewendet, selbst wenn die Cluster von verschiedenen Lines\-Of\-Business oder Administratoren verwaltet werden für unterschiedliche Klassen von Failoverclustern erstellt und verwaltet werden.  
  
-   CAU kann Updateausführungen für regelmäßige tägliche, wöchentliche oder monatliche Intervalle können Koordination von clusteraktualisierungen mit anderen IT-Verwaltungsprozessen planen.  
  
-   CAU bietet eine erweiterbare Architektur, um die Cluster-Softwareinventur Cluster\ unterstützende Weise aktualisieren. Dies kann vom Herausgeber verwendet werden, um die Installation von Softwareupdates, die nicht in Windows Update oder Microsoft Update veröffentlicht werden oder sind, nicht von Microsoft, z.B. Updates für-Microsoft-Gerätetreiber zu koordinieren.  
  
-   Aktualisieren von deren Hilfe CAU-Modus können Sie einen Cluster in einem Feld-Geräts \ (eine Gruppe von Cluster aus physischen Computern, üblicherweise in einem Chassis\) selbst aktualisieren. Normalerweise werden solche Geräte in Filialen mit minimalem lokalem IT-Support zur Verwaltung von Clustern bereitgestellt. Aktualisieren von deren Hilfe-Modus bietet hervorragende Leistung in diesen Szenarien.  
  
## <a name="important-functionality"></a>Wichtige Funktionen  
Im folgenden finden wichtige Cluster-Aware Updating Funktionen beschrieben:  
  
-   Eine Benutzeroberfläche \(UI\) - Fensters clusterfähiges aktualisieren – und einen Satz von Cmdlets, die Sie verwenden, um eine Vorschau anzeigen, anwenden und überwachen können, und melden die Updates  
  
-   Ein zur Implementierung-zu-Ende-Automatisierung des Vorgangs Cluster\ aktualisieren \ (ein Update ausführen), koordiniert durch einen oder mehrere Remoteupdatekoordinator Computer  
  
-   Remoteverwaltungssoftware im standardmäßig, die Integration in die bestehende Windows Update-Agent-\(WUA\) und Windows Server Update Services \(WSUS\)-Infrastruktur in Windows Server zum Anwenden wichtiger Microsoft-Updates  
  
-   Ein zweites Remoteverwaltungssoftware-in, zum Anwenden von Microsoft-Hotfixes verwendet werden kann und -Microsoft-Updates anwenden angepasst werden kann  
  
-   Updateausführungsprofile, die Sie mit den Einstellungen für die updateausführungsoptionen, wie z.B. die maximale Häufigkeit zu konfigurieren, die die Aktualisierung pro Knoten wiederholt wird. Updateausführungprofile ermöglichen Ihnen das schnelle Wiederverwendung derselben Einstellungen für Updateausführungen und einfache Freigabe der aktualisierungseinstellungen für andere Failovercluster.  
  
-   Eine erweiterbare Architektur, die Remoteverwaltungssoftware in Entwicklung neuen koordiniert werden andere Tools eine Aktualisierung über den Cluster, wie benutzerdefinierte softwareinstallationsprogramme, BIOS-Tools, aktualisieren und Netzwerk-Adapter oder Host Bus Adapter \(HBA\) aktualisieren Tools unterstützt.  
  
Cluster-Aware Updating, kann die gesamte Clusteraktualisierung auf zwei Arten erfolgen:  
  
-   **Deren Hilfe Remoteaktualisierungsmodus** in diesem Modus ist die Clusterrolle für clusterfähiges aktualisieren als Arbeitsauslastung auf, die zu aktualisierenden Failovercluster konfiguriert ist, und ein zugehöriger Aktualisierungszeitplan wird festgelegt. Der Cluster aktualisiert sich selbst am geplanten Zeiten anhand eines standardmäßigen oder benutzerdefinierten updateausführungsprofils. Während der Updateausführung die CAU-updatekoordinatorprozess auf dem Knoten, der aktuell die CAU-Clusterrolle besitzt gestartet wird, und werden nacheinander durch den Prozess Updates auf den einzelnen Knoten. Um die aktuellen Clusterknoten zu aktualisieren, die CAU-Clusterrolle ein Failover auf einen anderen Clusterknoten, und ein neuer updatekoordinatorprozess auf diesem Knoten übernimmt die Steuerung der Updateausführung aktualisieren. Im Modus mit deren Hilfe aktualisieren kann CAU den Failovercluster mit einem vollständig automatisierten, zur Implementierung-zu-Ende-Aktualisierungsprozess aktualisieren. Ein Administrator kann auch Trigger bedarfsgesteuerte in diesem Modus aktualisiert, oder einfach verwenden, die das Remote\ aktualisieren Ansatz, wenn gewünscht. Im Modus mit deren Hilfe aktualisieren, ein Administrator kann erhalten Zusammenfassungsinformationen zu einer Updateausführung in Bearbeitung eine Verbindung mit dem Cluster und Ausführen der **Get-CauRun** Windows PowerShell-Cmdlet.  
  
-   **Remote\ Remoteaktualisierungsmodus** bei diesem Modus wird ein Remotecomputer, der sogenannte Updatekoordinator, mit den CAU-Tools konfiguriert ist. Der Updatekoordinator ist kein Mitglied des Clusters, die während der Updateausführung aktualisiert wird. Vom Remotecomputer der Administrator löst bedarfsgesteuerte Updateausführung mithilfe eines standardmäßigen oder benutzerdefinierten updateausführungsprofils. Remote\ Remoteaktualisierungsmodus eignet sich für die Überwachung von Fortschritt Real\ Zeit während der Updateausführung und für den Cluster, die auf Server Core-Installationen ausgeführt werden.  
  
## <a name="hardware-and-software-requirements"></a>Hardware- und softwareanforderungen  

CAU kann für alle Editionen von Windows Server, einschließlich Server Core-Installationen verwendet werden. Informationen zu den detaillierten Anforderungen finden Sie unter [Cluster-Aware Updating Anforderungen und best Practices](cluster-aware-updating-requirements.md).

### <a name="installing-cluster-aware-updating"></a>Installieren die Cluster-Aware Updating
CAU verwenden, installieren das Feature Failoverclustering in Windows Server und einen Failovercluster erstellen. Die Komponenten, die CAU-Funktionalität unterstützen, werden automatisch auf jedem Clusterknoten installiert.

Um die Failover-Clusterunterstützung zu installieren, können Sie die folgenden Tools:
- Hinzufügen von Rollen und Features Assistenten im Server-Manager
- [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/server-manager/install-windowsfeature) Windows PowerShell-Cmdlet
- Befehlszeilentool Deployment Image Servicing and Management (DISM)

Weitere Informationen finden Sie unter [installieren oder Deinstallieren von Rollen, Rollendienste oder Features](https://technet.microsoft.com/library/hh831809(v=ws.11).aspx).

Sie müssen auch die Failoverclustering-Tools, installieren, die Teil der Remoteserver-Verwaltungstools und werden standardmäßig installiert, wenn Sie das Feature Failoverclustering in Server-Manager installieren. Das Failoverclustering-Tools enthalten, die Benutzeroberfläche des clusterfähigen Aktualisierens und PowerShell-Cmdlets. 

Sie müssen die Failoverclusteringtools wie folgt, um die verschiedenen CAU-aktualisierungsmodi unterstützen installieren:

- Um das clusterfähige aktualisieren im Remoteaktualisierungsmodus deren Hilfe verwenden, installieren Sie die Failoverclusteringtools auf den einzelnen Knoten.   
  
- Um Remote\ Remoteaktualisierungsmodus zu aktivieren, installieren Sie das Failoverclustering-Tools auf einem Computer, der über Netzwerkkonnektivität zum Failovercluster verfügt.  
  
> [!NOTE]  
> -   Die Failoverclustering-Tools können unter Windows Server2012 Sie Cluster-Aware Updating, die auf eine neuere Version von Windows Server verwalten. 
> -   Um die Verwendung von CAU nur im Modus Remote\ aktualisieren, ist die Installation der Failoverclusteringtools auf den Clusterknoten nicht erforderlich. Bestimmte Features für clusterfähiges aktualisieren können allerdings nicht verfügbar sein. Weitere Informationen finden Sie unter [Anforderungen und Best Practices for Cluster\-Aware Updating](cluster-aware-updating-requirements.md).  
> -   Es sei denn, Sie CAU nur im Modus mit deren Hilfe aktualisieren verwenden, kann nicht der Computer, auf dem die CAU-Tools installiert sind, und der die Aktualisierungen koordiniert, ein Mitglied des Failoverclusters sein.  
  
### <a name="enabling-self-updating-mode"></a>Selbstaktualisierungsmodus aktivieren
Um den selbstaktualisierungsmodus zu aktivieren, müssen Sie die Cluster-Aware Updating Clusterrolle für den Failovercluster hinzufügen. Verwenden Sie dazu eine der folgenden Methoden:
- Wählen Sie im Server-Manager **Tools** > **Cluster-Aware Updating**, wählen Sie dann im Fenster des clusterfähigen Aktualisierens **konfigurieren selbstaktualisierungsoptionen für Cluster**. 
- Führen Sie in einer PowerShell-Sitzung die [Add-CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/add-cauclusterrole) Cmdlet.  
  
CAU deinstallieren möchten, deinstallieren Sie die Failover-Clusterunterstützung oder die Failoverclusteringtools mithilfe des Server-Manager die [Uninstall-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/server-manager/uninstall-windowsfeature) -Cmdlet, oder der DISM-Befehlszeilenoption-Tools.  
  
### <a name="additional-requirements-and-best-practices"></a>Zusätzliche Anforderungen und best practices  

Um sicherzustellen, dass für clusterfähiges aktualisieren die Clusterknoten erfolgreich, und für Weitere Informationen zum Konfigurieren der Failoverclusterumgebung für cau aktualisieren kann, können Sie die Best Practices Analyzer für CAU ausführen.  
  
Detail zu den Anforderungen und best Practices für die Verwendung von CAU sowie Informationen zum Ausführen von Best Practices Analyzer für CAU finden Sie unter [Anforderungen und Best Practices for Cluster\-Aware Updating](cluster-aware-updating-requirements.md).  
  
### <a name="starting-cluster-aware-updating"></a>Starten Sie die Cluster-Aware Updating  
  
##### <a name="to-start-cluster-aware-updating-from-server-manager"></a>Cluster-Aware Updating über Server-Manager starten  
  
1.  Starten Sie Server-Manager.  
  
2.  Führen Sie einen der folgenden:  
  
    -   Auf der **Tools** Menü klicken Sie auf **Cluster\-Aware Updating**.  
  
    -   Wenn ein oder mehrere Knoten im Cluster oder der Cluster auf Server-Manager hinzugefügt wird die **alle Server** Seite, mit der rechten Maustaste auf den Namen eines Knotens \ (oder den Namen der Cluster\), und klicken Sie dann auf **Cluster aktualisieren**.  
  
## <a name="see-also"></a>Siehe auch  
Die folgenden Links bieten weitere Informationen zur Verwendung des clusterfähigen Aktualisierens.  
  
-   [Anforderungen und Best Practices for Cluster\-Aware Updating](cluster-aware-updating.md)  
  
-   [Cluster\-Aware Updating: Häufig gestellte Fragen](cluster-aware-updating-faq.md)  
  
-   [Erweiterte Optionen und Updateausführungsprofile für CAU](cluster-aware-updating-options.md)  
  
-   [Funktionsweise von CAU Remoteverwaltungssoftware-ins](cluster-aware-updating-plug-ins.md)  
  
-   [Cmdlets für Cluster\ unterstützende aktualisieren in WindowsPowerShell](https://go.microsoft.com/fwlink/p/?LinkId=237675)  
  
-   [Cluster\ unterstützende Remoteverwaltungssoftware im Verweis aktualisieren](https://msdn.microsoft.com/library/hh418084.aspx)  
  

