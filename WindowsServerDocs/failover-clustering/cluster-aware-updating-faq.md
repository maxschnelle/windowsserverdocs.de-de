---
ms.assetid: 6416d125-bcaf-433d-971a-2f0283bca2c2
title: "Cluster-Aware Updating - gestellte häufig Fragen"
ms.topic: article
ms.prod: storage-failover-clustering
manager: dongill
ms.author: jgerend
author: JasonGerend
ms.date: 4/28/2017
description: "Erhalten Sie Antworten auf häufig gestellte Fragen zur Cluster-Aware Updating in Windows Server."
ms.openlocfilehash: 8417ea8b6b76e16c3f4db3bac5062d90a8da3ff2
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="cluster-aware-updating-frequently-asked-questions"></a>Cluster-Aware Updating: Häufig gestellte Fragen

> Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server2016, Windows Server2012 R2, Windows Server 2012

[Cluster-Aware Updating](cluster-aware-updating.md) \(CAU\) ist ein Feature, das Softwareupdates auf allen Servern in einem Failovercluster auf eine Weise koordiniert, die die dienstverfügbarkeit mehr als ein geplantes Failover eines Clusterknotens auswirken nicht wird. Bei einigen Anwendungen mit stets Verfügbarkeitsfeatures \ z.B. (Hyper\-V mit Livemigration) oder ein SMB-3.x-Dateiserver mit SMB Transparent Failover\, kann CAU koordiniert, automatisierte Clusteraktualisierung ohne Auswirkungen auf die Verfügbarkeit des Diensts.

## <a name="does-cau-support-updating-storage-spaces-direct-clusters"></a>Unterstützt CAU Updates "direkte Speicherplätze"-Cluster?  
Ja. CAU unterstützt die Aktualisierung ["direkte Speicherplätze"](../storage/storage-spaces/storage-spaces-direct-overview.md) Cluster unabhängig von der Art der Bereitstellung: zusammengeführten oder zusammengefasst. CAU Orchestrierung wird insbesondere sichergestellt, dass jeder Clusterknoten anhalten auf die zugrunde liegenden Clusterspeicherplatzes fehlerfrei ist wartet.

## <a name="does-cau-work-with-windows-server-2008-r2-or-windows-7"></a>Kann CAU für Windows Server2008 R2 oder Windows7 werden verwendet?  
Nein. CAU koordiniert die Clusteraktualisierung nur auf Computern mit Windows Server2016, Windows Server2012 R2, Windows Server2012, Windows10, Windows8.1 oder Windows8. Im Failovercluster aktualisiert wird, muss Windows Server2016, Windows Server2012 R2 oder Windows Server2012 ausführen.
  
## <a name="is-cau-limited-to-specific-clustered-applications"></a>Ist CAU bestimmte Clusteranwendungen beschränkt?  
Nein. CAU ist in den Typ der Clusteranwendung unabhängig. CAU ist eine externe Cluster\ aktualisieren Lösung, die über die Cluster-APIs und PowerShell-Cmdlets gelagert ist. Daher kann CAU koordiniert Aktualisierung für eine beliebige geclusterte Anwendung, die in einem Windows Server-Failovercluster konfiguriert ist.  
  
> [!NOTE]  
> Derzeit die folgenden geclusterten Arbeitsauslastungen getestet und für CAU zertifiziert: SMB, Hyper\-V, DFS-Replikation, DFS-Namespaces, iSCSI und NFS.  
  
## <a name="does-cau-support-updates-from-microsoft-update-and-windows-update"></a>Unterstützt CAU Updates von Microsoft Update und Windows Update?  
Ja. Standardmäßig wird CAU mit einem Remoteverwaltungssoftware-in konfiguriert, die auf den Clusterknoten \(WUA\) Windows Update-Agent-Hilfsprogramm-APIs verwendet. Die WUA-Infrastruktur kann konfiguriert werden, um Microsoft Update und Windows Update oder Windows Server Update Services \(WSUS\) als Updatequelle verweist.  
  
## <a name="does-cau-support-wsus-updates"></a>Unterstützt CAU WSUS-Updates?  
Ja. Standardmäßig wird CAU mit einem Remoteverwaltungssoftware-in konfiguriert, die auf den Clusterknoten \(WUA\) Windows Update-Agent-Hilfsprogramm-APIs verwendet. Die WUA-Infrastruktur kann konfiguriert werden, um Microsoft Update und Windows Update oder auf einem lokalen Windows Server Update Services \(WSUS\) Server als Updatequelle verweist.  
  
## <a name="can-cau-apply-limited-distribution-release-updates"></a>Kann CAU Updates von Versionen mit eingeschränkter Verteilung angewendet?  
Ja. Eingeschränkter Verteilung \(LDR\) von Updates auch als Hotfixes bezeichnet werden nicht über Microsoft Update oder Windows Update veröffentlicht, damit sie von der Windows Update-Agent-\(WUA\) plug\ heruntergeladen werden können – in diesem CAU wird standardmäßig verwendet.  
  
CAU bietet jedoch ein zweites Remoteverwaltungssoftware-in, dass Sie auswählen können, um das Hotfix-Updates anwenden. Dieses Hotfix Remoteverwaltungssoftware-in kann auch angepasst werden, um-Microsoft-Treiber, Firmware und BIOS-Updates anzuwenden.  
  
## <a name="can-i-use-cau-to-apply-cumulative-updates"></a>Kann ich CAU verwenden, um kumulative Updates anzuwenden?  
Ja. Wenn es sich bei den kumulativen Updates um Updates von Versionen mit allgemeiner Verteilung oder LDR-Updates handelt, kann CAU angewendet.  
  
## <a name="can-i-schedule-updates"></a>Kann ich Updates planen?  
Ja. CAU unterstützt die folgenden aktualisierungsmodi, die Updates geplant werden können:  
  
**Aktualisieren von deren Hilfe** ermöglicht dem Cluster, sich gemäß eines definierten Profils und regelmäßigen Zeitplans, z.B. während eines monatlichen Wartungszeitfensters zu aktualisieren. Sie können auch eine deren Hilfe-Updateausführung bei Bedarf jederzeit starten. Um deren Hilfe Remoteaktualisierungsmodus zu aktivieren, müssen Sie die Clusterrolle für clusterfähiges aktualisieren zum Cluster hinzufügen. Das Aktualisieren von deren Hilfe CAU-Feature wird wie jeder andere clusterarbeitsauslastung ausgeführt kann, und es problemlos mit der geplanten und ungeplanten Failover von eines updatekoordinatorcomputers.  
  
**Aktualisieren von Remote\** ermöglicht es Ihnen, eine Aktualisierungsausführung zu einem beliebigen Zeitpunkt von einem Computer unter Windows oder Windows Server starten. Sie können über das Fenster des clusterfähigen Aktualisierens oder über eine Updateausführung Starten der **Invoke-CauRun** PowerShell-Cmdlet. Remote\-Aktualisierung ist der standardaktualisierungsmodus für CAU. Sie können mithilfe der Aufgabenplanung Ausführen der [Invoke-CauRun](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-caurun) Cmdlet auf einem gewünschten Zeitplan auf einem Remotecomputer, der nicht einem Knoten eines Clusters ist.  
  
## <a name="can-i-schedule-updates-to-apply-during-a-backup"></a>Kann ich während einer Sicherung anzuwendenden Updates planen?  
Ja. CAU Hinsicht keine Einschränkungen in dieser. Allerdings Ausführen von Softwareupdates auf einem Server \ (mit den zugehörigen potenziellen Neustartanzahl\) während eine Sicherung wird Fortschritt ist keine bewährte IT-Methode. Achten Sie darauf, dass es sich bei CAU nur Cluster-APIs, um ressourcenfailover und -Failbacks zu bestimmen nutzt; Daher ist CAU der serversicherungsstatus nicht bekannt.  
  
## <a name="can-cau-work-with-system-center-configuration-manager"></a>Werden CAU kann mit System Center Configuration Manager verwendet?  
CAU ist ein Tool, das Softwareupdates auf einem Clusterknoten koordiniert, und Configuration Manager werden auch serversoftwareupdates ausgeführt. Es ist wichtig, diese Tools so konfigurieren, dass sie keinen überlappende Abdeckung derselben Server in jeder Datacenter-Bereitstellung, einschließlich der Verwendung von anderen Windows Server Update Services-Server. Dadurch wird sichergestellt, dass die Absicht hinter der Verwendung von CAU nicht versehentlich aufgehoben wird, da Configuration Manager\ gesteuerte Aktualisierungen keine Clusterinformationen beinhalten.  
  
## <a name="do-i-need-administrative-credentials-to-run-cau"></a>Benötige ich Administratoranmeldeinformationen, um CAU auszuführen?  
Ja. Für das Ausführen der CAU-Tools für clusterfähiges aktualisieren administrative Anmeldeinformationen auf dem lokalen Server benötigt, oder es muss die **annehmen der Clientidentität nach Authentifizierung** Benutzer direkt auf dem lokalen Server oder Clientcomputer, auf dem es ausgeführt wird. Zum Koordinieren von Softwareupdates auf den Clusterknoten erfordert CAU jedoch clusteradministratoranmeldeinformationen auf jedem Knoten. Obwohl die CAU-UI ohne die Anmeldeinformationen gestartet werden können, werden aufgefordert, für die administrative Anmeldeinformationen für Cluster beim Herstellen einer zu einer Clusterinstanz Verbindung, um eine Vorschau oder Anwenden von Updates.  
  
## <a name="can-i-script-cau"></a>Kann ich CAU Skript?  
Ja. CAU enthält PowerShell-Cmdlets, die einen umfassenden Satz von Skriptoptionen anbieten. Dies sind dieselben Cmdlets, die die CAU-UI CAU-Aktionen aufgerufen.  

## <a name="what-happens-to-active-clustered-roles"></a>Was geschieht mit aktiven Clusterrollen?

Clusterrollen \ (ehemals Anwendungen und -Dienste\), die auf einem Knoten aktiv sind, führen Sie ein Failover auf andere Knoten vor der Aktualisierung der Software beginnen kann. CAU orchestriert diese Failover mithilfe des Wartungsmodus, der anhält und ihm ausgleicht den Knoten alle aktiven Clusterrollen. Wenn die Softwareupdates abgeschlossen sind, CAU fortgesetzt wird, den Knoten, und die Clusterrollen wird ein Failback auf den aktualisierten Knoten. Dadurch wird sichergestellt, dass die Verteilung von Clusterrollen im Vergleich zu Knoten bei den CAU-Aktualisierungsausführungen von einem Cluster gleich bleibt.  
  
## <a name="how-does-cau-select-target-nodes-for-clustered-roles"></a>Wie wird CAU die Zielknoten für Clusterrollen ausgewählt?

CAU wird, hängt davon ab, Cluster-APIs, um die Failover zu koordinieren. Die Cluster-API-Implementierung wählt die Knoten durch verwenden interner Metriken und intelligenter platzierungsheuristiken \ (z.B. Arbeitsauslastung Levels\) auf dem Zielknoten.  
  
## <a name="does-cau-load-balance-the-clustered-roles"></a>Lastenausgleich CAU die Clusterrollen?

CAU lädt nicht den Lastenausgleich, die die Clusterknoten, aber es wird versucht, die Verteilung der Clusterrollen beizubehalten. Durch CAU beendet wird, einen Clusterknoten zu aktualisieren, versucht, ein auszuführen zurück zuvor gehosteten Clusterrollen auf diesen Knoten. CAU werden Cluster-APIs verwendet, um die Ressourcen an den Anfang des angehaltenen Vorgangs ein Failback basiert. Keine ungeplanten Failover und bevorzugten besitzereinstellungen, sollte die Verteilung der Clusterrollen daher unverändert bleiben.  
  
## <a name="how-does-cau-select-the-order-of-nodes-to-update"></a>Wie wird CAU die Reihenfolge zu aktualisierenden Knoten ausgewählt?  
Standardmäßig wählt clusterfähiges aktualisieren die Reihenfolge von Knoten zu aktualisierenden basierend auf der Ebene der Aktivität. Der Knoten, auf denen die wenigsten Clusterrollen gehostet werden, werden zuerst aktualisiert. Allerdings kann ein Administrator eine bestimmte Reihenfolge für das Aktualisieren der Knoten durch Angabe eines Parameters für die Updateausführung in die CAU-UI oder mithilfe der PowerShell-Cmdlets angeben.  
  
## <a name="what-happens-if-a-cluster-node-is-offline"></a>Was geschieht, wenn ein Knoten offline ist?

Der Administrator, der Aktualisierungsausführung initiiert kann den zulässigen Schwellenwert für die Anzahl der Knoten angeben, die offline sein können. Aus diesem Grund kann eine Updateausführung auf einem Cluster fortfahren, selbst wenn keiner die Clusterknoten online ist.  
  
## <a name="can-i-use-cau-to-update-only-a-single-node"></a>Kann ich CAU verwenden, um nur einen einzelnen Knoten aktualisieren?  
Nein. CAU ist ein Cluster\ Bereich aktualisieren Tool, sodass er nur zu aktualisierende Cluster auswählen kann. Wenn Sie einen einzelnen Knoten aktualisieren möchten, können Sie vorhandene serveraktualisierungstools für clusterfähiges aktualisieren.  
  
## <a name="can-cau-report-updates-that-are-initiated-from-outside-cau"></a>Kann CAU Updates melden, die außerhalb von CAU initiiert werden?  
Nein. CAU können nur Aktualisierungsausführungen gemeldet werden, die innerhalb von CAU initiiert werden. Allerdings wird eine nachfolgende CAU-Aktualisierungsausführung gestartet, werden Updates, die von CAU-Methoden installiert wurden entsprechend interpretiert, um die zusätzlichen Updates zu ermitteln, die auf jedem Clusterknoten erforderlich sein kann.  
  
## <a name="can-cau-support-my-unique-it-process-needs"></a>Können CAU-Unterstützung meinen individuellen IT-prozessanforderungen muss?  
Ja. CAU bietet die folgenden Dimensionen Maß an Flexibilität, entsprechend der Unternehmen, die Kunden individuellen IT-prozessanforderungen benötigt:  
  
**Skripts** eine Aktualisierungsausführung ein PowerShell-Skript registrierungseintragswert und ein PowerShell-Skript Post\ angeben können. Das Skript registrierungseintragswert-Update wird auf jedem Clusterknoten ausgeführt, bevor der Knoten angehalten wird. Das Skript Post\-Update wird auf jedem Clusterknoten ausgeführt, nachdem die knotenupdates installiert wurden.  
  
> [!NOTE]  
> .NET Framework 4.6 oder 4.5 und PowerShell muss auf jedem Clusterknoten, auf dem Sie die Skripts registrierungseintragswert- und Post\-Update ausführen möchten, installiert werden. Sie müssen auch die PowerShell-Remoting auf den Clusterknoten aktivieren. Ausführliche Informationen zu Systemanforderungen, finden Sie unter [Anforderungen und Best Practices for Cluster-Aware Updating](cluster-aware-updating-requirements.md).  
  
**Erweiterte updateausführungsoptionen** der Administrator kann darüber hinaus eine Reihe erweiterter updateausführungsoptionen wie z.B. die maximale Häufigkeit, mit der der Updatevorgang auf jedem Knoten wiederholt wird angeben. Diese Optionen können mithilfe der CAU-UI oder der CAU-PowerShell-Cmdlets angegeben werden. Diese benutzerdefinierten Einstellungen können in einem Profil für die Updateausführung gespeichert und bei späteren Updateausführungen wiederverwendet werden.  
  
**Öffentliche Remoteverwaltungssoftware-in-Architektur** CAU bietet Features zum Registrieren, Aufheben der Registrierung, und wählen Sie Remoteverwaltungssoftware-ins cau bietet zwei Standard-Remoteverwaltungssoftware-ins: eines koordiniert die Windows Update-Agent-\(WUA\) APIs auf jedem Clusterknoten; die zweite wendet Hotfixes an, die manuell in eine Dateifreigabe kopiert werden, die die Clusterknoten zugegriffen werden kann. Wenn ein Unternehmen individuelle Anforderungen, die mit diesen beiden Remoteverwaltungssoftware Plug-Ins nicht erfüllt werden können hat, kann Unternehmen ein neues CAU Remoteverwaltungssoftware eingehend gemäß der öffentlichen API-Spezifikation erstellen. Weitere Informationen finden Sie unter [Cluster\-Aware Updating Remoteverwaltungssoftware im Verweis](http://msdn.microsoft.com/library/hh418084(VS.85).aspx).  
  
Informationen zum Konfigurieren und Anpassen von CAU Remoteverwaltungssoftware Plug-Ins unterstützen verschiedene Szenarien, Aktualisieren finden Sie [Funktionsweise Remoteverwaltungssoftware ins](assetId:///847b571b-12b3-473c-953f-75a5a1f51333).  
  
## <a name="how-can-i-export-the-cau-preview-and-update-results"></a>Wie kann ich exportieren die CAU-Vorschau und aktualisieren Ergebnisse zu?  
CAU bietet Exportoptionen über die Befehlszeilenschnittstelle und die Benutzeroberfläche.  
  
**Schnittstelle Befehlszeilenoptionen:**  
  
-   Vorschauergebnisse mithilfe des PowerShell-Cmdlets **Invoke-CauScan | ConvertTo-XML-**. Ausgabe: XML  
  
-   Berichtsergebnisse mithilfe des PowerShell-Cmdlets **Invoke-CauRun | ConvertTo-XML-**. Ausgabe: XML  
  
-   Berichtsergebnisse mithilfe des PowerShell-Cmdlets **Get-CauReport | Export\-CauReport**. Ausgabe: HTML, CSV  
  
**UI-Optionen:**  
  
-   Kopieren Sie die Berichtsergebnisse aus dem **Updatevorschau** Bildschirm. Ausgabe: CSV  
  
-   Kopieren Sie die Berichtsergebnisse aus dem **Bericht** Bildschirm. Ausgabe: CSV  
  
-   Exportieren Sie die Berichtsergebnisse aus dem **Bericht** Bildschirm. Ausgabe: HTML  
  
## <a name="how-do-i-install-cau"></a>Wie installiere ich CAU?  
Eine CAU-Installation ist nahtlos in das Feature Failoverclustering integriert. CAU wird wie folgt installiert:  
  
-   Wenn Failoverclustering auf einem Clusterknoten installiert ist, wird der \(WMI\) CAU-WMI-Anbieter automatisch installiert.  
  
-   Wenn das Feature Failoverclustering-Tools auf einem Server oder Clientcomputer installiert ist, werden die clusterfähige Aktualisierung UI und PowerShell-Cmdlets automatisch installiert.
  
## <a name="does-cau-need-components-running-on-the-cluster-nodes-that-are-being-updated"></a>Benötigt CAU Komponenten auf den Clusterknoten, die aktualisiert werden?  
CAU ist einen Dienst, der auf den Clusterknoten ausgeführt erforderlich. CAU benötigt jedoch eine Softwarekomponente \ (der WMI-Provider\) auf den Clusterknoten installiert. Diese Komponente wird mit dem Feature Failoverclustering installiert.  
  
Um deren Hilfe Remoteaktualisierungsmodus zu aktivieren, muss die CAU-Clusterrolle auch dem Cluster hinzugefügt werden.  
  
## <a name="what-is-the-difference-between-using-cau-and-vmm"></a>Was ist der Unterschied zwischen der Verwendung von CAU und VMM?  
  
-   System Center Virtual Machine Manager \(VMM\) konzentriert sich nur Hyper\-V-Cluster, aktualisieren, während CAU jeder Art von unterstützter Failovercluster, einschließlich Hyper\-V-Cluster aktualisiert werden kann.  
  
-   VMM erfordert zusätzliche Lizenzen, während CAU für alle Windows Server lizenziert ist. Die CAU-Features, Tools und UI werden mit Failoverclusteringkomponenten installiert.  
  
-   Wenn Sie bereits eine System Center-Lizenz besitzen, können Sie weiterhin mit VMM Hyper\-V-Cluster zu aktualisieren, da es sich um eine integrierte Verwaltungs- und softwareaktualisierungserfahrung bietet.  
  
-   CAU wird nur auf Clustern unterstützt, auf denen Windows Server2016, Windows Server2012 R2 und Windows Server2012 ausgeführt werden. VMM unterstützt auch Hyper\-V-Cluster auf Computern unter Windows Server2008 R2 und Windows Server2008.  
  
## <a name="can-i-use-remote-updating-on-a-cluster-that-is-configured-for-self-updating"></a>Kann ich verwenden Remote\ aktualisieren in einem Cluster, der so konfiguriert ist, für deren Hilfe aktualisieren?  
Ja. Ein Failovercluster in einer Konfiguration mit deren Hilfe aktualisieren kann über Remote\ aktualisieren bedarfsgesteuerte, aktualisiert werden, wie Sie eine Windows Update-Überprüfung zu einem beliebigen Zeitpunkt auf dem Computer erzwingen können, auch wenn Windows Update konfiguriert ist, dass Updates automatisch installiert. Allerdings müssen Sie sicherstellen, dass eine Updateausführung nicht bereits ausgeführt wird.  
  
## <a name="can-i-reuse-my-cluster-update-settings-across-clusters"></a>Kann ich meine clusteraktualisierungseinstellung für mehrere Cluster wiederverwenden?  
Ja. CAU unterstützt eine Reihe von updateausführungsoptionen, die bestimmen, wie die Updateausführung verhält sich, wenn den Cluster aktualisiert. Diese Optionen können als Aktualisierungsausführungsprofil gespeichert werden, und für beliebige Cluster wiederverwendet werden. Es wird empfohlen, dass Sie speichern und Ihre Einstellungen auf Failoverclustern, die ähnlichen aktualisierungsanforderungen wiederzuverwenden. Sie können z.B. ein "Business\ erforderliche SQL Server-Cluster Aktualisierungsausführungsprofil" für alle Microsoft SQL Server-Cluster, die Business\ kritischen Dienste unterstützen erstellen.  
  
## <a name="where-is-the-cau-plug-in-specification"></a>Wo finde ich die CAU-Remoteverwaltungssoftware-in-Spezifikation?  
  
-   [Cluster\ unterstützende Remoteverwaltungssoftware im Verweis aktualisieren](http://msdn.microsoft.com/library/hh418084(VS.85).aspx)  
  
-   [Cluster-Aware Updating Remoteverwaltungssoftware-in-Beispiel](http://code.msdn.microsoft.com/windowsdesktop/Cluster-Aware-Updating-6a8854c9)  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Übersicht über das Cluster\ unterstützende aktualisieren](cluster-aware-updating.md)  
  
