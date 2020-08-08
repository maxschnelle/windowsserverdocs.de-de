---
title: Übersicht über die clusterfähige Aktualisierung.
description: Das Cluster fähige aktualisieren (Cluster-Aware Update, Cau) automatisiert die Installation von Software Updates auf Clustern unter Windows Server.
ms.topic: article
manager: lizross
author: JasonGerend
ms.author: jgerend
ms.date: 08/06/2018
ms.assetid: 3c2993b4-aa81-452b-a5c3-3724ad95d892
ms.openlocfilehash: defec4b34dfd0e2efa5724e499330c79b993bb60
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87990808"
---
# <a name="cluster-aware-updating-overview"></a>Übersicht über die clusterfähige Aktualisierung.

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Thema enthält eine Übersicht über das Cluster fähige \- Aktualisieren von \( Cau \) , ein Feature, mit dem der Software Aktualisierungsprozess auf Cluster Servern während der Aufrechterhaltung der Verfügbarkeit automatisiert wird.

> [!NOTE]
> Wenn Sie [direkte Speicherplätze](../storage/storage-spaces/storage-spaces-direct-overview.md) Cluster aktualisieren, empfiehlt es sich, das Cluster fähige aktualisieren zu verwenden.

## <a name="feature-description"></a><a name="BKMK_OVER"></a>Featurebeschreibung
Das Cluster fähige aktualisieren ist ein automatisiertes Feature, mit dem Sie Server in einem [Failovercluster](failover-clustering-overview.md) mit geringem oder ohne Verfügbarkeit während des Aktualisierungs Vorgangs aktualisieren können. Während einer Update Ausführung führt das Cluster fähige aktualisieren transparent die folgenden Aufgaben aus:

1. Versetzt jeden Knoten des Clusters in den Knoten Wartungsmodus.
2. Verschiebt die Cluster Rollen aus dem Knoten.
3. Installiert die Updates und alle abhängigen Updates.
4. Führt bei Bedarf einen Neustart durch.
5. Führt den Wartungsmodus des Knotens aus.
6. Stellt die Cluster Rollen auf dem Knoten wieder her.
7. Wechselt, um den nächsten Knoten zu aktualisieren.

Für viele Clusterrollen im Cluster löst der automatische Updateprozess ein geplantes Failover aus. Dadurch kann eine vorübergehende Dienstunterbrechung für angeschlossene Clients verursacht werden. Bei fortlaufend verfügbaren Arbeits Auslastungen, z. b. Hyper- \- V mit Live Migration oder Dateiserver mit SMB transparent Failover, kann das Cluster fähige aktualisieren jedoch Cluster Aktualisierungen ohne Auswirkungen auf die Dienst Verfügbarkeit koordinieren.

## <a name="practical-applications"></a>Praktische Anwendung

-   Cau reduziert Dienst Ausfälle in geclusterten Diensten, verringert die Notwendigkeit von Problem Umgehungen für manuelles Aktualisieren und macht den End- \- to- \- End-Cluster Aktualisierungsprozess für den Administrator zuverlässiger. Wenn das Cau-Feature in Verbindung mit fortlaufend verfügbaren Cluster Arbeits Auslastungen verwendet wird, z. b. fortlaufend verfügbare Datei \( Server-Arbeitsauslastung mit SMB transparent Failover \) oder Hyper- \- V, können die Cluster Aktualisierungen ohne Auswirkungen auf die Dienst Verfügbarkeit für Clients durchgeführt werden.

-   CAU vereinfacht die unternehmensweite Übernahme von einheitlichen IT-Prozessen. Update Lauf Profile können für unterschiedliche Klassen von Failoverclustern erstellt und dann zentral auf einer Dateifreigabe verwaltet werden, um sicherzustellen, dass Aktualisierungen durch Cau-bereit Stellungen in der gesamten IT-Organisation einheitlich angewendet werden, auch wenn die Cluster von verschiedenen \- \- Geschäftsbereichen oder Administratoren verwaltet werden.

-   Mit CAU können Updateausführungen für regelmäßige tägliche, wöchentliche oder monatliche Intervalle zur Koordination von Clusteraktualisierungen mit anderen IT-Verwaltungsprozessen geplant werden.

-   Cau stellt eine erweiterbare Architektur bereit, mit der die Cluster Software Inventur in einer Cluster fähigen Weise aktualisiert werden können \- . Dies kann von Verlegern verwendet werden, um die Installation von Software Updates zu koordinieren, die nicht auf Windows Update oder Microsoft Update veröffentlicht werden oder nicht von Microsoft zur Verfügung stehen, z. b. Updates für nicht von \- Microsoft stammende Gerätetreiber.

-   \-Der selbst Aktualisierungs Modus von Cau ermöglicht einem Cluster in einem Box-Gerät \( eine Reihe von gruppierten physischen Computern, die in der Regel in einem Chassis verpackt werden, \) um sich selbst zu aktualisieren. Normalerweise werden solche Geräte in Filialen mit minimalem lokalem IT-Support zur Verwaltung von Clustern bereitgestellt. \-Der selbst Aktualisierungs Modus bietet in diesen Bereitstellungs Szenarien einen großen nutzen.

## <a name="important-functionality"></a>Wichtige Funktionalität
Im folgenden finden Sie eine Beschreibung der wichtigen Funktionen für die Cluster fähige Aktualisierung:

-   Eine Benutzeroberfläche \( , \) das Cluster fähige Aktualisierungs Fenster und eine Reihe von Cmdlets, die Sie verwenden können, um die Aktualisierungen anzuzeigen, zu überwachen, zu überwachen und zu berichten.

-   Eine End- \- to- \- End-Automatisierung des Cluster \- Aktualisierungs Vorgangs \( eine Update Ausführung \) , die von einem oder mehreren updatekoordinatorcomputern orchestriert wird

-   Ein Standard \- -Plug-in, das in den vorhandenen Windows Update \( -Agent WUA \) und Windows Server Update Services \( WSUS- \) Infrastruktur in Windows Server integriert wird, um wichtige Microsoft-Updates anzuwenden.

-   Ein zweites Plug \- -in, das zum Anwenden von Microsoft-Hotfixes verwendet werden kann und das zum Anwenden von nicht-Microsoft-Updates angepasst werden kann \-

-   Updateausführungsprofile, die Sie mit Einstellungen für Optionen zur Updateausführung konfigurieren, wie z. B. die maximale Anzahl an Versuchen, die eine Aktualisierung pro Knoten wiederholt wird. Updateausführungprofile ermöglichen eine schnelle Wiederverwendung derselben Einstellungen für verschiedene Updateausführungen und eine einfache Freigabe der Aktualisierungseinstellungen für andere Failovercluster.

-   Eine erweiterbare Architektur, die neue Plug-in-Entwicklungen unterstützt, \- um andere Knoten \- Aktualisierungs Tools im Cluster zu koordinieren, wie z. b. benutzerdefinierte Software Installationsprogramme, Tools für die BIOS-Aktualisierung und Netzwerkadapter-oder Hostbus Adapter- \( HBA \)

Das Feature des clusterfähigen Aktualisierens kann die gesamte Clusteraktualisierung in zwei Modi koordinieren:

-   **Selbst \- Aktualisierungs Modus** in diesem Modus wird die Cluster Rolle für Cluster fähiges aktualisieren als Arbeitsauslastung auf dem zu aktualisierenden Failovercluster konfiguriert, und ein zugeordneter Aktualisierungs Zeitplan wird definiert. Der Cluster aktualisiert sich zu den geplanten Zeiten anhand eines standardmäßigen oder benutzerdefinierten Updateausführungsprofils selbst. Bei der Updateausführung startet der CAU-Updatekoordinatorprozess auf dem Knoten, der aktuell der Besitzer der Clusterrolle für CAU ist, und alle Clusterknoten werden nacheinander durch den Prozess aktualisiert. Von der CAU-Clusterrolle wird zum Aktualisieren des aktuellen Clusterknotens ein Failover zu einem anderen Clusterknoten ausgeführt, und ein neuer Updatekoordinatorprozess auf diesem Knoten übernimmt die Steuerung der Updateausführung. Im selbst \- Aktualisierungs Modus kann mit Cau der Failovercluster mit einem vollständig automatisierten, End- \- to- \- End-Aktualisierungsprozess aktualisiert werden. Ein Administrator kann auch Updates \- Bedarfs gesteuert in diesem Modus oder bei Bedarf einfach den Ansatz für die Remote \- Aktualisierung verwenden. Im selbst \- Aktualisierungs Modus kann ein Administrator Zusammenfassungs Informationen zu einer laufenden Update Ausführung erhalten, indem er eine Verbindung mit dem Cluster herstellt und das Windows PowerShell-Cmdlet **get \- caurun** ausführen.

-   Der **Remote \- Aktualisierungs Modus** für diesen Modus wird ein Remote Computer, der als Update Koordinator bezeichnet wird, mit den Cau-Tools konfiguriert. Der Updatekoordinator gehört nicht dem Cluster an, der im Rahmen der Updateausführung aktualisiert wird. Vom Remote Computer aus löst der Administrator \- mithilfe eines standardmäßigen oder benutzerdefinierten Update Lauf Profils eine Bedarfs gesteuerte Update Laufzeit aus. \-Der Remote Aktualisierungs Modus ist nützlich für \- die Überwachung des Echt Zeit Fortschritts während der Update Ausführung und für Cluster, die auf Server Core-Installationen ausgeführt werden.

## <a name="hardware-and-software-requirements"></a>Hardware- und Softwareanforderungen

Cau kann für alle Editionen von Windows Server, einschließlich Server Core-Installationen, verwendet werden. Ausführliche Informationen zu den Anforderungen finden Sie unter Anforderungen für das [Cluster fähige aktualisieren und bewährte Methoden](cluster-aware-updating-requirements.md).

### <a name="installing-cluster-aware-updating"></a>Installieren des Cluster fähigen Updates
Um Cau zu verwenden, installieren Sie das Failoverclustering-Feature in Windows Server, und erstellen Sie ein Failovercluster. Die Komponenten, die die CAU-Funktionalität unterstützen, werden automatisch auf jedem Clusterknoten installiert.

Zur Installation des Failoverclustering-Features können Sie die folgenden Tools verwenden:
- Assistent zum Hinzufügen von Rollen und Features im Server-Manager
- [Install-Windows Feature](/powershell/module/servermanager/Install-WindowsFeature?view=winserver2012r2-ps&viewFallbackFrom=win10-ps)   Windows PowerShell-Cmdlet
- Befehlszeilentool %%amp;quot;Abbildverwaltung für die Bereitstellung%%amp;quot; (Deployment Image Servicing and Management, DISM)

Weitere Informationen finden Sie unter [Installieren des Failoverclustering-Features](create-failover-cluster.md#install-the-failover-clustering-feature).

Sie müssen auch die Failoverclustering-Tools installieren, die Teil der Remoteserver-Verwaltungstools sind und standardmäßig installiert werden, wenn Sie das Failoverclustering-Feature in Server-Manager installieren. Die Failoverclustering-Tools umfassen die Cluster fähige Aktualisierungs Benutzeroberfläche und PowerShell-Cmdlets.

Sie müssen die Failoverclusteringtools wie folgt installieren, um die verschiedenen CAU-Aktualisierungsmodi zu unterstützen:

- Wenn Sie Cau im selbst \- Aktualisierungs Modus verwenden möchten, installieren Sie die Failoverclustering-Tools auf jedem Cluster Knoten.

- Installieren Sie zum Aktivieren \- des Remote Aktualisierungs Modus die Failoverclustering-Tools auf einem Computer, der über eine Netzwerkverbindung mit dem Failovercluster verfügt.

> [!NOTE]
> -   Sie können die Failoverclustering-Tools unter Windows Server 2012 nicht verwenden, um das Cluster fähige Update auf einer neueren Version von Windows Server zu verwalten.
> -   Wenn Sie Cau nur im Remote \- Aktualisierungs Modus verwenden möchten, ist die Installation der failoverclusteringtools auf den Cluster Knoten nicht erforderlich. Bestimmte CAU-Features sind dann jedoch nicht verfügbar. Weitere Informationen finden Sie unter [Anforderungen und bewährte Methoden für die Cluster fähige \- Aktualisierung](cluster-aware-updating-requirements.md).
> -   Wenn Sie Cau nur im selbst \- Aktualisierungs Modus verwenden, kann der Computer, auf dem die Cau-Tools installiert werden und der die Aktualisierungen koordiniert, kein Mitglied des Failoverclusters sein.

### <a name="enabling-self-updating-mode"></a>Aktivieren des selbst Aktualisierungs Modus
Um den selbst Aktualisierungs Modus zu aktivieren, müssen Sie dem Failovercluster die Cluster Rolle für Cluster fähiges aktualisieren hinzufügen. Verwenden Sie hierzu eine der folgenden Methoden:
- Wählen Sie unter Server-Manager **Tools**  >  die Option Tools**Cluster fähiges aktualisieren**aus, und wählen Sie dann im Fenster Cluster fähiges aktualisieren die **Option selbst Aktualisierungs Optionen für Cluster konfigurieren**aus.
- Führen Sie in einer PowerShell-Sitzung das Cmdlet [Add-cauclusterrole](/powershell/module/clusterawareupdating/Add-CauClusterRole?view=win10-ps) aus.

Deinstallieren Sie zum Deinstallieren von Cau das Failoverclustering-Feature oder die failoverclusteringtools mithilfe von Server-Manager, dem Cmdlet " [Uninstall-Windows Feature](/powershell/module/servermanager/Uninstall-WindowsFeature?view=win10-ps) " oder den Befehls \- Zeilen Tools der Befehlszeilen Programme.

### <a name="additional-requirements-and-best-practices"></a>Weitere Anforderungen und Best Practices

Sie können den Best Practices Analyzer für CAU ausführen, um die erfolgreiche Aktualisierung der Clusterknoten mit CAU sicherzustellen und weitere Informationen zum Konfigurieren der Failoverclusterumgebung für die Verwendung von CAU zu erhalten.

Ausführliche Informationen zu den Anforderungen und bewährten Methoden für die Verwendung von Cau sowie Informationen zum Ausführen des Cau-Best Practices Analyzer finden Sie unter [Anforderungen und bewährte Methoden für die Cluster fähige \- Aktualisierung](cluster-aware-updating-requirements.md).

### <a name="starting-cluster-aware-updating"></a>Cluster fähiges aktualisieren wird gestartet

##### <a name="to-start-cluster-aware-updating-from-server-manager"></a>So starten Sie das Cluster fähige Aktualisieren von Server-Manager

1.  Starten Sie den Server-Manager.

2.  Führen Sie eines der folgenden Verfahren aus:

    -   Klicken Sie **im Menü Extras** auf **Cluster fähiges \- Aktualisieren**.

    -   Wenn mindestens ein Cluster Knoten oder der Cluster zu Server-Manager hinzugefügt wird, klicken Sie auf der Seite **alle Server** mit \- der rechten Maustaste auf den Namen eines Knotens \( oder den Namen des Clusters \) , und klicken Sie dann auf **Cluster aktualisieren**.

## <a name="additional-references"></a>Weitere Verweise
Die folgenden Links enthalten weitere Informationen zur Verwendung des Cluster fähigen Updates.

-   [Anforderungen und bewährte Methoden für die Cluster fähige \- Aktualisierung](cluster-aware-updating.md)

-   [Cluster fähiges \- Aktualisieren: häufig gestellte Fragen](cluster-aware-updating-faq.md)

-   [Erweiterte Optionen und Updateausführungsprofile für CAU](cluster-aware-updating-options.md)

-   [Funktionsweise von Cau-Plug- \- ins](cluster-aware-updating-plug-ins.md)

-   [\-Cmdlets für Cluster fähiges aktualisieren in Windows PowerShell](/powershell/module/clusterawareupdating/?view=win10-ps&viewFallbackFrom=winserverr2-ps)

-   [\-Referenz zu Plug- \- ins für Cluster fähiges aktualisieren](/previous-versions/windows/desktop/mscs/cluster-aware-update-plug-in-interfaces-and-classes)