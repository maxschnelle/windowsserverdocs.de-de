---
title: Übersicht über die clusterfähige Aktualisierung.
ms.topic: article
ms.prod: windows-server
ms.manager: dongill
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 08/06/2018
description: Das Cluster fähige aktualisieren (Cluster-Aware Update, Cau) automatisiert die Installation von Software Updates auf Clustern unter Windows Server.
ms.assetid: 3c2993b4-aa81-452b-a5c3-3724ad95d892
ms.openlocfilehash: e96223e0b4b44e87ade9dc8eb875f9aa7104f451
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361253"
---
# <a name="cluster-aware-updating-overview"></a>Übersicht über die clusterfähige Aktualisierung.

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Thema enthält eine Übersicht über den Cluster @ no__t-0aware Update \(CAU @ no__t-2, ein Feature, mit dem der Software Aktualisierungsprozess auf Cluster Servern bei gleichzeitiger Aufrechterhaltung der Verfügbarkeit automatisiert wird.

> [!NOTE]
> Wenn Sie [direkte Speicherplätze](../storage/storage-spaces/storage-spaces-direct-overview.md) Cluster aktualisieren, empfiehlt es sich, das Cluster fähige aktualisieren zu verwenden.
  
## <a name="BKMK_OVER"></a>Funktionsbeschreibung  
Das Cluster fähige aktualisieren ist ein automatisiertes Feature, mit dem Sie Server in einem [Failovercluster](failover-clustering-overview.md) mit geringem oder ohne Verfügbarkeit während des Aktualisierungs Vorgangs aktualisieren können. Während einer Update Ausführung führt das Cluster fähige aktualisieren transparent die folgenden Aufgaben aus:  

1. Versetzt jeden Knoten des Clusters in den Knoten Wartungsmodus.
2. Verschiebt die Cluster Rollen aus dem Knoten.
3. Installiert die Updates und alle abhängigen Updates.
4. Führt bei Bedarf einen Neustart durch.
5. Führt den Wartungsmodus des Knotens aus.
6. Stellt die Cluster Rollen auf dem Knoten wieder her.
7. Wechselt, um den nächsten Knoten zu aktualisieren.

Für viele Clusterrollen im Cluster löst der automatische Updateprozess ein geplantes Failover aus. Dadurch kann eine vorübergehende Dienstunterbrechung für angeschlossene Clients verursacht werden. Im Fall von fortlaufend verfügbaren Arbeits Auslastungen, wie z. b. Hyper @ no__t-0V mit Live Migration oder Dateiserver mit SMB transparent Failover, kann das Cluster fähige aktualisieren jedoch Cluster Aktualisierungen ohne Auswirkungen auf die Dienst Verfügbarkeit koordinieren.    
  
## <a name="practical-applications"></a>Praktische Anwendungsfälle  
  
-   Cau reduziert Dienst Ausfälle in geclusterten Diensten, verringert die Notwendigkeit von Problem Umgehungen für manuelles Aktualisieren und bewirkt, dass der End @ no__t-0to @ no__t-1End-Cluster Aktualisierungsprozess für den Administrator zuverlässiger ist. Wenn das Cau-Feature zusammen mit fortlaufend verfügbaren Cluster Arbeits Auslastungen verwendet wird, z. b. fortlaufend verfügbare Dateiserver \(-Dateiserver-Arbeitsauslastung mit SMB transparent Failover @ no__t-1 oder Hyper @ no__t-2V, können die Cluster Updates ausgeführt werden. mit keinerlei Auswirkung auf die Dienst Verfügbarkeit für Clients.  
  
-   CAU vereinfacht die unternehmensweite Übernahme von einheitlichen IT-Prozessen. Update Lauf Profile können für unterschiedliche Klassen von Failoverclustern erstellt und dann zentral auf einer Dateifreigabe verwaltet werden, um sicherzustellen, dass Aktualisierungen durch Cau-bereit Stellungen in der gesamten IT-Organisation einheitlich angewendet werden, auch wenn die Cluster von anderen verwaltet werden. Zeilen @ no__t-0von @ no__t-1business oder Administratoren.  
  
-   Mit CAU können Updateausführungen für regelmäßige tägliche, wöchentliche oder monatliche Intervalle zur Koordination von Clusteraktualisierungen mit anderen IT-Verwaltungsprozessen geplant werden.  
  
-   Cau stellt eine erweiterbare Architektur bereit, mit der die Cluster Software Inventur im @ no__t-fähigen Cluster-Cluster aktualisiert wird. Dies kann von Verlegern verwendet werden, um die Installation von Software Updates zu koordinieren, die nicht auf Windows Update oder Microsoft Update veröffentlicht werden oder nicht von Microsoft zur Verfügung stehen, z. b. Updates für nicht-no__t-0Microsoft-Gerätetreiber.  
  
-   Der Self @ no__t-0update-Modus von Cau ermöglicht einen "Cluster in einem Box"-Gerät \(Eine Reihe von gruppierten physischen Computern, die in der Regel in einem Chassis @ no__t-2 verpackt sind, um sich selbst zu aktualisieren. Normalerweise werden solche Geräte in Filialen mit minimalem lokalem IT-Support zur Verwaltung von Clustern bereitgestellt. Der Self @ no__t-0update-Modus bietet in diesen Bereitstellungs Szenarien einen großen nutzen.  
  
## <a name="important-functionality"></a>Wichtige Funktionalität  
Im folgenden finden Sie eine Beschreibung der wichtigen Funktionen für die Cluster fähige Aktualisierung:  
  
-   Eine Benutzeroberfläche \(ui @ no__t-1-das Fenster Cluster fähiges aktualisieren und eine Reihe von Cmdlets, mit denen Sie die Updates in der Vorschau anzeigen, anwenden, überwachen und Berichte überprüfen können.  
  
-   Eine End @ no__t-0to @ no__t-1End-Automatisierung des Cluster @ no__t-2Update-Vorgangs \(a-Update Ausführung @ no__t-4, orchestriert von einem oder mehreren updatekoordinatorcomputern  
  
-   Ein Standard-Plug-in für @ no__t-0in, das in den vorhandenen Windows Update-Agent \(wua @ no__t-2 und Windows Server Update Services \(wsus @ no__t-4-Infrastruktur in Windows Server integriert ist, um wichtige Microsoft-Updates anzuwenden.  
  
-   Ein zweites Plug @ no__t-0in, das zum Anwenden von Microsoft-Hotfixes verwendet werden kann und das zum Anwenden von nicht-no__t-1Microsoft-Updates angepasst werden kann  
  
-   Updateausführungsprofile, die Sie mit Einstellungen für Optionen zur Updateausführung konfigurieren, wie z. B. die maximale Anzahl an Versuchen, die eine Aktualisierung pro Knoten wiederholt wird. Updateausführungprofile ermöglichen eine schnelle Wiederverwendung derselben Einstellungen für verschiedene Updateausführungen und eine einfache Freigabe der Aktualisierungseinstellungen für andere Failovercluster.  
  
-   Eine erweiterbare Architektur, die neue Plug @ no__t-0in der Entwicklung unterstützt, um andere Node @ no__t-1Update-Tools im Cluster zu koordinieren, z. b. benutzerdefinierte Software Installationsprogramme, BIOS-Aktualisierungs Tools und Netzwerkadapter oder Hostbus Adapter \(hba @ no__t-3 Tools werden aktualisiert.  
  
Beim Cluster fähigen aktualisieren kann der gesamte Cluster Aktualisierungs Vorgang in zwei Modi koordiniert werden:  
  
-   **Self @ no__t-1aktualisierungs Modus** In diesem Modus wird die Cluster Rolle für Cluster fähiges aktualisieren als Arbeitsauslastung auf dem zu aktualisierenden Failovercluster konfiguriert, und es wird ein zugeordneter Aktualisierungs Zeitplan definiert. Der Cluster aktualisiert sich zu den geplanten Zeiten anhand eines standardmäßigen oder benutzerdefinierten Updateausführungsprofils selbst. Bei der Updateausführung startet der CAU-Updatekoordinatorprozess auf dem Knoten, der aktuell der Besitzer der Clusterrolle für CAU ist, und alle Clusterknoten werden nacheinander durch den Prozess aktualisiert. Von der CAU-Clusterrolle wird zum Aktualisieren des aktuellen Clusterknotens ein Failover zu einem anderen Clusterknoten ausgeführt, und ein neuer Updatekoordinatorprozess auf diesem Knoten übernimmt die Steuerung der Updateausführung. Im Self @ no__t-0update-Modus kann Cau den Failovercluster mithilfe eines vollautomatischen Aktualisierungsprozesses von End @ no__t-1TO @ no__t-2end aktualisieren. Ein Administrator kann auch Updates für @ no__t-0demand in diesem Modus oder einfach den Remote @ no__t-1Update-Ansatz verwenden, wenn gewünscht. Im Self @ no__t-0update-Modus kann ein Administrator Zusammenfassungs Informationen zu einer laufenden Update Ausführung erhalten, indem eine Verbindung mit dem Cluster hergestellt und das Windows PowerShell-Cmdlet **Get @ no__t-2caurun** ausgeführt wird.  
  
-   **Remote @ no__t-1Update-Modus** Bei diesem Modus wird ein Remote Computer, der als Update Koordinator bezeichnet wird, mit den Cau-Tools konfiguriert. Der Updatekoordinator gehört nicht dem Cluster an, der im Rahmen der Updateausführung aktualisiert wird. Der-Administrator löst auf dem Remote Computer mit einem standardmäßigen oder benutzerdefinierten Update Lauf Profil eine auf @ no__t-0demand-Aktualisierungs Lauf aus. Der Remote Modus "@ no__t-0update" ist nützlich für die Überwachung des Echtzeitstatus von @ no__t-1time während der Update Ausführung und für Cluster, die auf Server Core-Installationen ausgeführt werden.  
  
## <a name="hardware-and-software-requirements"></a>Hardware- und Softwareanforderungen  

Cau kann für alle Editionen von Windows Server, einschließlich Server Core-Installationen, verwendet werden. Ausführliche Informationen zu den Anforderungen finden Sie unter Anforderungen für das [Cluster fähige aktualisieren und bewährte Methoden](cluster-aware-updating-requirements.md).

### <a name="installing-cluster-aware-updating"></a>Installieren des Cluster fähigen Updates
Um Cau zu verwenden, installieren Sie das Failoverclustering-Feature in Windows Server, und erstellen Sie ein Failovercluster. Die Komponenten, die die CAU-Funktionalität unterstützen, werden automatisch auf jedem Clusterknoten installiert.

Zur Installation des Failoverclustering-Features können Sie die folgenden Tools verwenden:
- Assistent zum Hinzufügen von Rollen und Features im Server-Manager
- [Install-Windows Feature](https://docs.microsoft.com/powershell/module/servermanager/Install-WindowsFeature?view=winserver2012r2-ps&viewFallbackFrom=win10-ps) Windows PowerShell-Cmdlet
- Befehlszeilentool %%amp;quot;Abbildverwaltung für die Bereitstellung%%amp;quot; (Deployment Image Servicing and Management, DISM)

Weitere Informationen finden Sie unter [Installieren des Failoverclustering-Features](create-failover-cluster.md#install-the-failover-clustering-feature).

Sie müssen auch die Failoverclustering-Tools installieren, die Teil der Remoteserver-Verwaltungstools sind und standardmäßig installiert werden, wenn Sie das Failoverclustering-Feature in Server-Manager installieren. Die Failoverclustering-Tools umfassen die Cluster fähige Aktualisierungs Benutzeroberfläche und PowerShell-Cmdlets. 

Sie müssen die Failoverclusteringtools wie folgt installieren, um die verschiedenen CAU-Aktualisierungsmodi zu unterstützen:

- Installieren Sie die Failoverclustering-Tools auf den einzelnen Cluster Knoten, um Cau im Self @ no__t-Update-Modus zu verwenden.   
  
- Installieren Sie die failoverclusteringtools auf einem Computer, der über eine Netzwerkverbindung mit dem Failovercluster verfügt, um den Remote-@ no__t-0update Modus zu aktivieren.  
  
> [!NOTE]  
> -   Sie können die Failoverclustering-Tools unter Windows Server 2012 nicht verwenden, um das Cluster fähige Update auf einer neueren Version von Windows Server zu verwalten. 
> -   Die Installation der failoverclusteringtools auf den Cluster Knoten ist nicht erforderlich, um Cau nur im Remote-@ no__t-0update-Modus zu verwenden. Bestimmte CAU-Features sind dann jedoch nicht verfügbar. Weitere Informationen finden Sie unter [Anforderungen und Best Practices für clusterfähiges Aktualisieren\-](cluster-aware-updating-requirements.md).  
> -   Wenn Sie Cau nur im Self @ no__t-0update-Modus verwenden, kann der Computer, auf dem die Cau-Tools installiert werden und der die Aktualisierungen koordiniert, kein Mitglied des Failoverclusters sein.  
  
### <a name="enabling-self-updating-mode"></a>Aktivieren des selbst Aktualisierungs Modus
Um den selbst Aktualisierungs Modus zu aktivieren, müssen Sie dem Failovercluster die Cluster Rolle für Cluster fähiges aktualisieren hinzufügen. Verwenden Sie hierzu eine der folgenden Methoden:
- Wählen Sie in Server-Manager **Tools** > **Cluster fähiges aktualisieren**aus, und wählen Sie dann im Fenster Cluster fähiges aktualisieren die **Option selbst Aktualisierungs Optionen für Cluster konfigurieren**aus. 
- Führen Sie in einer PowerShell-Sitzung das Cmdlet [Add-cauclusterrole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Add-CauClusterRole?view=win10-ps) aus.  
  
Deinstallieren Sie zum Deinstallieren von Cau das Failoverclustering-Feature oder die failoverclusteringtools mithilfe von Server-Manager, dem Cmdlet [Uninstall-Windows Feature](https://docs.microsoft.com/powershell/module/servermanager/Uninstall-WindowsFeature?view=win10-ps) oder dem Befehl "-Ausdruck" @ no__t-1line-Tools.  
  
### <a name="additional-requirements-and-best-practices"></a>Weitere Anforderungen und Best Practices  

Sie können den Best Practices Analyzer für CAU ausführen, um die erfolgreiche Aktualisierung der Clusterknoten mit CAU sicherzustellen und weitere Informationen zum Konfigurieren der Failoverclusterumgebung für die Verwendung von CAU zu erhalten.  
  
Ausführliche Informationen zu den Anforderungen und bewährten Methoden für die Verwendung von Cau sowie Informationen zum Ausführen des Cau-Best Practices Analyzer finden Sie unter [Anforderungen und Best Practices für Cluster @ no__t-1aware Update](cluster-aware-updating-requirements.md).  
  
### <a name="starting-cluster-aware-updating"></a>Cluster fähiges aktualisieren wird gestartet  
  
##### <a name="to-start-cluster-aware-updating-from-server-manager"></a>So starten Sie das Cluster fähige Aktualisieren von Server-Manager  
  
1.  Starten Sie den Server-Manager.  
  
2.  Führen Sie eines der folgenden Verfahren aus:  
  
    -   Klicken Sie **im Menü Extras** auf **Cluster @ no__t-2aware Update**.  
  
    -   Wenn mindestens ein Cluster Knoten oder der Cluster zu Server-Manager hinzugefügt wird, klicken Sie auf der Seite **alle Server** mit der rechten Maustaste auf den Namen eines Knotens \(oder den Namen des Clusters @ no__t-3, und klicken Sie dann auf **Cluster aktualisieren**.  
  
## <a name="see-also"></a>Siehe auch  
Die folgenden Links enthalten weitere Informationen zur Verwendung des Cluster fähigen Updates.  
  
-   [Anforderungen und bewährte Methoden für Cluster @ no__t-1aware Update](cluster-aware-updating.md)  
  
-   [cluster @ no__t-1aware-Aktualisierung: Häufig gestellte Fragen](cluster-aware-updating-faq.md)  
  
-   [Erweiterte Optionen und Update Lauf Profile für Cau](cluster-aware-updating-options.md)  
  
-   [Funktionsweise von Cau-Plug @ no__t-1ins](cluster-aware-updating-plug-ins.md)  
  
-   [Cluster @ no__t-1aware Update-Cmdlets in Windows PowerShell](https://docs.microsoft.com/powershell/module/clusterawareupdating/?view=win10-ps&viewFallbackFrom=winserverr2-ps)  
  
-   [Cluster @ no__t-1aware Update Plugin @ no__t-2in-Referenz](https://docs.microsoft.com/previous-versions/windows/desktop/mscs/cluster-aware-update-plug-in-interfaces-and-classes)  
  

