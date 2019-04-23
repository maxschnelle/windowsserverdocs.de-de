---
title: Übersicht über die clusterfähige Aktualisierung.
ms.topic: article
ms.prod: windows-server-threshold
ms.manager: dongill
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 08/06/2018
description: Clusterfähiges aktualisieren (CAU) automatisiert die Installation von Softwareupdates in Windows Server-Clustern.
ms.assetid: 3c2993b4-aa81-452b-a5c3-3724ad95d892
ms.openlocfilehash: 77ccfe7dc9a769d602ff069d5f1d8e77522aa001
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827421"
---
# <a name="cluster-aware-updating-overview"></a>Übersicht über die clusterfähige Aktualisierung.

> Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Dieses Thema bietet einen Überblick über die Cluster\-Aware Updating \(CAU\), eine Funktion, die automatisiert der softwareaktualisierungsprozess auf gruppierten Servern unter Aufrechterhaltung der Verfügbarkeit.

> [!NOTE]
> Bei der Aktualisierung ["direkte Speicherplätze"](../storage/storage-spaces/storage-spaces-direct-overview.md) Cluster, es wird empfohlen, Cluster-Aware Updating.
  
## <a name="BKMK_OVER"></a>Featurebeschreibung  
Cluster-Aware Updating ist ein automatisiertes Feature, das Ihnen ermöglicht, das Aktualisieren von Servern in einer [Failovercluster](failover-clustering-overview.md) mit minimalen oder keinen verfügbarkeitseinbußen bei der Verfügbarkeit während des Updates. Während einer Updateausführung führt das Cluster-Aware Updating transparent die folgenden Aufgaben:  

1. Versetzen der einzelnen Knoten des Clusters in den knotenwartungsmodus.
2. Verschiebt die clusterrollen vom Knoten an.
3. Die Updates und alle abhängigen Aktualisierungen installiert.
4. Ein Neustart durchgeführt, falls erforderlich.
5. Stellt den Knoten aus dem Wartungsmodus.
6. Werden die clusterrollen auf dem Knoten wiederhergestellt.
7. Wechselt zum nächsten Knoten zu aktualisieren.

Für viele Clusterrollen im Cluster löst der automatische Updateprozess ein geplantes Failover aus. Dadurch kann eine vorübergehende Dienstunterbrechung für angeschlossene Clients verursacht werden. Allerdings bei fortlaufend verfügbaren arbeitsauslastungen, z. B. Hyper\-V live Migration oder Datei-Server mit SMB Transparent Failover Cluster-Aware Updating kann clusteraktualisierungen ohne Auswirkungen auf die dienstverfügbarkeit koordiniert werden.    
  
## <a name="practical-applications"></a>Praktische Anwendungsfälle  
  
-   CAU reduziert Dienstausfälle in geclusterten Diensten, verringert den Bedarf an manuellen problemumgehungen bei der Aktualisierung und macht Sie am Ende\-zu\-Ende-Clusteraktualisierung Verlässlichkeit für den Administrator. Wenn das CAU-Feature verwendet wird, zusammen mit laufend verfügbaren clusterarbeitsauslastungen, wie kontinuierlich verfügbare Dateiserver \(Dateiserver-arbeitsauslastung mit SMB Transparent Failover\) oder Hyper\-V, den Cluster clusteraktualisierungen ohne Auswirkungen auf die dienstverfügbarkeit für Clients können ausgeführt werden.  
  
-   CAU vereinfacht die unternehmensweite Übernahme von einheitlichen IT-Prozessen. Updateausführungsprofile kann dann zentral auf einer Dateifreigabe, um sicherzustellen, dass es sich bei Updates von CAU-Bereitstellungen in der gesamten IT-Organisation einheitlich angewendet, selbst wenn der Cluster von verschiedenen Zeilen verwaltet werden für unterschiedliche Klassen von Failoverclustern erstellt und verwaltet werden \-von\-Business oder Administratoren.  
  
-   Mit CAU können Updateausführungen für regelmäßige tägliche, wöchentliche oder monatliche Intervalle zur Koordination von Clusteraktualisierungen mit anderen IT-Verwaltungsprozessen geplant werden.  
  
-   CAU bietet eine erweiterbare Architektur zum Aktualisieren der Cluster die Softwareinventur in einem Cluster\-clusterfähiger knotenaktualisierungstools. Dies kann verwendet werden, von Herausgebern, koordinieren die Installation von Softwareupdates, die nicht mit Windows Update oder Microsoft Update veröffentlicht werden oder sich nicht von Microsoft, z. B. Updates für, nicht\-Microsoft-Gerätetreiber.  
  
-   CAU Self-Service\-Updatemodus an ein Gerät "-Clusters in einem Feld" ermöglicht \(einen Satz von Cluster aus physischen Computern, üblicherweise in einem einzelnen Gehäuse\) sich selbst zu aktualisieren. Normalerweise werden solche Geräte in Filialen mit minimalem lokalem IT-Support zur Verwaltung von Clustern bereitgestellt. Self\-Updatemodus bietet hervorragende Leistung in diesen Bereitstellungsszenarios.  
  
## <a name="important-functionality"></a>Wichtige Funktionalität  
Im folgenden finden eine Beschreibung der wichtige Cluster-Aware Updating-Funktionen:  
  
-   Eine Benutzeroberfläche \(UI\) -Fenster clusterfähiges aktualisieren – und eine Reihe von Cmdlets, die Sie verwenden, um eine Vorschau anzeigen, anwenden und überwachen können, und Berichte zu den Updates  
  
-   Ein Ende\-zu\-Enden der Automatisierung des Clusters\-Vorgang aktualisiert \(einer Updateausführung\), von einem oder mehreren Remoteupdatekoordinator Computern koordiniert  
  
-   Eine Standard-Plug\-in, das den vorhandenen Windows Update Agent integriert \(WUA\) und Windows Server Update Services \(WSUS\) -Infrastruktur in Windows Server anwenden wichtiger Microsoft Updates  
  
-   Eine zweite Plug\-in dieser können verwendet werden, um Microsoft-Hotfixes angewendet, und nicht anzuwendende angepasst werden kann\-Microsoft-Updates  
  
-   Updateausführungsprofile, die Sie mit Einstellungen für Optionen zur Updateausführung konfigurieren, wie z. B. die maximale Anzahl an Versuchen, die eine Aktualisierung pro Knoten wiederholt wird. Updateausführungprofile ermöglichen eine schnelle Wiederverwendung derselben Einstellungen für verschiedene Updateausführungen und eine einfache Freigabe der Aktualisierungseinstellungen für andere Failovercluster.  
  
-   Eine erweiterbare Architektur, die neue Plug-Ins unterstützt\-in der Entwicklung zum Koordinieren von anderen Knoten\-im Cluster, wie benutzerdefinierte softwareinstallationsprogramme, BIOS aktualisieren von Tools und Netzwerkadapter oder Hostbusadapter toolsaktualisieren\( HBA\) Tools werden aktualisiert.  
  
Cluster-Aware Updating, kann die gesamte Clusteraktualisierung in zwei Modi koordiniert werden:  
  
-   **Self\-Updatemodus** bei diesem Modus wird die Clusterrolle für clusterfähiges aktualisieren als einer arbeitsauslastung auf, die zu aktualisierenden Failovercluster konfiguriert ist, und ein zugehöriger Aktualisierungszeitplan wird festgelegt. Der Cluster aktualisiert sich zu den geplanten Zeiten anhand eines standardmäßigen oder benutzerdefinierten Updateausführungsprofils selbst. Bei der Updateausführung startet der CAU-Updatekoordinatorprozess auf dem Knoten, der aktuell der Besitzer der Clusterrolle für CAU ist, und alle Clusterknoten werden nacheinander durch den Prozess aktualisiert. Von der CAU-Clusterrolle wird zum Aktualisieren des aktuellen Clusterknotens ein Failover zu einem anderen Clusterknoten ausgeführt, und ein neuer Updatekoordinatorprozess auf diesem Knoten übernimmt die Steuerung der Updateausführung. In Self-Service\-Updatemodus an, für clusterfähiges aktualisieren können aktualisieren Sie den Failovercluster mit einem vollständig automatisierten, Ende\-zu\-End-Prozess zu aktualisieren. Ein Administrator kann auch Auslösen von Updates auf\-in diesem Modus erfordern, oder verwenden Sie einfach die Remote\-Ansatz wird bei Bedarf aktualisiert. In Self-Service\-Updatemodus an, ein Administrator erhalten zusammenfassende Informationen zu einer Updateausführung wird ausgeführt durch Herstellen einer Verbindung mit dem Cluster und Ausführen der **erhalten\-CauRun** Windows PowerShell-Cmdlet.  
  
-   **Remote\-Updatemodus** bei diesem Modus wird ein Remotecomputer, der sogenannte Updatekoordinator, mit den CAU-Tools konfiguriert ist. Der Updatekoordinator gehört nicht dem Cluster an, der im Rahmen der Updateausführung aktualisiert wird. Vom Remotecomputer, der Administrator löst ein auf\-mithilfe einer standardmäßigen oder benutzerdefinierten updateausführungsprofils fordern Updateausführung. Remote\-Updatemodus eignet sich für die Überwachung von realen\-Mal ausgeführt, während der Updateausführung und für Cluster, die auf Server Core-Installationen ausgeführt werden.  
  
## <a name="hardware-and-software-requirements"></a>Hardware- und Softwareanforderungen  

CAU kann für alle Editionen von Windows Server, einschließlich Server Core-Installationen verwendet werden. Ausführliche Informationen finden Sie unter [Cluster-Aware Updating Anforderungen und best Practices](cluster-aware-updating-requirements.md).

### <a name="installing-cluster-aware-updating"></a>Installieren des clusterfähigen Aktualisierens
Um für clusterfähiges aktualisieren verwenden, installieren Sie das Feature Failoverclustering in Windows Server, und Erstellen eines Failoverclusters. Die Komponenten, die die CAU-Funktionalität unterstützen, werden automatisch auf jedem Clusterknoten installiert.

Zur Installation des Failoverclustering-Features können Sie die folgenden Tools verwenden:
- Assistent zum Hinzufügen von Rollen und Features im Server-Manager
- [Install-WindowsFeature](https://docs.microsoft.com/powershell/module/servermanager/Install-WindowsFeature?view=winserver2012r2-ps&viewFallbackFrom=win10-ps) Windows PowerShell-Cmdlet
- Befehlszeilentool %%amp;quot;Abbildverwaltung für die Bereitstellung%%amp;quot; (Deployment Image Servicing and Management, DISM)

Weitere Informationen finden Sie unter [installieren Sie das Feature "Failoverclustering"](create-failover-cluster.md#install-the-failover-clustering-feature).

Sie müssen auch die Failoverclustering-Tools, installieren, die Teil der Remoteserver-Verwaltungstools werden standardmäßig installiert, wenn Sie das Feature "Failoverclustering" im Server-Manager installieren. Das Failoverclustering-Tools enthalten die Cluster-Aware Updating-Benutzeroberfläche und PowerShell-Cmdlets. 

Sie müssen die Failoverclusteringtools wie folgt installieren, um die verschiedenen CAU-Aktualisierungsmodi zu unterstützen:

- Verwendung von CAU in Self-Service\-Updatemodus an, die Failoverclustering-Tools auf jedem Clusterknoten installieren.   
  
- So aktivieren Sie remote\-Updatemodus an, die Failoverclustering-Tools auf einem Computer installieren, die über eine Netzwerkverbindung zum Failovercluster verfügt.  
  
> [!NOTE]  
> -   Sie können nicht die Failoverclustering-Tools unter Windows Server 2012 verwenden, zum Verwalten von Cluster-Aware Updating auf einer neueren Version von Windows Server. 
> -   Verwendung von CAU nur in Remote\-Updatemodus, Installation der Failoverclusteringtools auf den Clusterknoten ist nicht erforderlich. Bestimmte CAU-Features sind dann jedoch nicht verfügbar. Weitere Informationen finden Sie unter [Anforderungen und Best Practices für Cluster\-Aware Updating](cluster-aware-updating-requirements.md).  
> -   Wenn Sie CAU nur im Self-Service mit\-Updatemodus an, der Computer, auf dem die CAU-Tools installiert sind, und der die Aktualisierungen koordiniert, kann nicht Mitglied des Failoverclusters.  
  
### <a name="enabling-self-updating-mode"></a>Selbstaktualisierungsmodus aktivieren
Um den selbstaktualisierungsmodus zu aktivieren, müssen Sie die Cluster-Aware Updating Clusterrolle mit dem Failovercluster hinzufügen. Zu diesem Zweck verwenden Sie eine der folgenden Methoden:
- Wählen Sie im Server-Manager **Tools** > **Cluster-Aware Updating**, wählen Sie dann im Fenster des clusterfähigen Aktualisierens **selbstaktualisierungsoptionen fürKonfigurieren-Cluster**. 
- Führen Sie in einer PowerShell-Sitzung die [Add-CauClusterRole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Add-CauClusterRole?view=win10-ps) Cmdlet.  
  
CAU deinstallieren möchten, deinstallieren Sie das Feature "Failoverclustering" oder die Failoverclusteringtools mithilfe des Server-Manager die [Uninstall-WindowsFeature](https://docs.microsoft.com/powershell/module/servermanager/Uninstall-WindowsFeature?view=win10-ps) -Cmdlet, oder der DISM-Befehl\-Zeile Tools.  
  
### <a name="additional-requirements-and-best-practices"></a>Weitere Anforderungen und Best Practices  

Sie können den Best Practices Analyzer für CAU ausführen, um die erfolgreiche Aktualisierung der Clusterknoten mit CAU sicherzustellen und weitere Informationen zum Konfigurieren der Failoverclusterumgebung für die Verwendung von CAU zu erhalten.  
  
Details zu den Anforderungen und best Practices für die Verwendung von CAU sowie Informationen zum Ausführen von Best Practices Analyzer für CAU finden Sie [Anforderungen und Best Practices für Cluster\-Aware Updating](cluster-aware-updating-requirements.md).  
  
### <a name="starting-cluster-aware-updating"></a>Starten des clusterfähigen Aktualisierens  
  
##### <a name="to-start-cluster-aware-updating-from-server-manager"></a>Cluster-Aware Updating im Server-Manager gestartet werden.  
  
1.  Starten Sie den Server-Manager.  
  
2.  Führen Sie eine der folgenden Aktionen aus:  
  
    -   Auf der **Tools** Menü klicken Sie auf **Cluster\-Aware Updating**.  
  
    -   Wenn mindestens ein Clusterknoten oder dem Cluster Server-Manager hinzugefügt wird die **alle Server** Seite rechts\-klicken Sie auf den Namen eines Knotens \(oder den Namen des Clusters\), und klicken Sie dann auf  **Aktualisieren der Cluster**.  
  
## <a name="see-also"></a>Siehe auch  
Die folgenden Links bieten weitere Informationen zur Verwendung des clusterfähigen Aktualisierens.  
  
-   [Anforderungen und Best Practices für Cluster\-clusterfähiges aktualisieren](cluster-aware-updating.md)  
  
-   [Cluster\-clusterfähiges aktualisieren: Häufig gestellte Fragen](cluster-aware-updating-faq.md)  
  
-   [Erweiterte Optionen und Updateausführungsprofile für CAU](cluster-aware-updating-options.md)  
  
-   [Stecken Sie CAU wie\-ins Arbeit](cluster-aware-updating-plug-ins.md)  
  
-   [Cluster\-clusterfähige Aktualisierung-Cmdlets in Windows PowerShell](https://docs.microsoft.com/powershell/module/clusterawareupdating/?view=win10-ps&viewFallbackFrom=winserverr2-ps)  
  
-   [Cluster\-clusterfähige Aktualisierung Plug\-Referenz](https://docs.microsoft.com/previous-versions/windows/desktop/mscs/cluster-aware-update-plug-in-interfaces-and-classes)  
  

