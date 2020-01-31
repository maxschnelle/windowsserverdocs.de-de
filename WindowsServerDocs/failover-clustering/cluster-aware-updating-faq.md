---
ms.assetid: 6416d125-bcaf-433d-971a-2f0283bca2c2
title: 'Cluster fähiges aktualisieren: häufig gestellte Fragen'
ms.topic: article
ms.prod: windows-server
manager: dongill
ms.author: jgerend
author: JasonGerend
ms.date: 04/28/2017
description: Hier erhalten Sie Antworten auf häufig gestellte Fragen zum Cluster fähigen aktualisieren in Windows Server.
ms.openlocfilehash: 736b49222ae4c9e2a27229341f0d886bd3e0343c
ms.sourcegitcommit: 07c9d4ea72528401314e2789e3bc2e688fc96001
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2020
ms.locfileid: "76822133"
---
# <a name="cluster-aware-updating-frequently-asked-questions"></a>Clusterfähiges Aktualisieren: Häufig gestellte Fragen

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Das [Cluster fähige aktualisieren](cluster-aware-updating.md) \(Cau-\) ist ein Feature, das Software Updates auf allen Servern in einem Failovercluster auf eine Art und Weise koordiniert, die sich nicht mehr auf die Dienst Verfügbarkeit auswirkt als ein Geplantes Failover eines Cluster Knotens. Bei einigen Anwendungen mit Features für die kontinuierliche Verfügbarkeit \(z. b. Hyper\-V mit Live Migration oder ein SMB 3. x-Dateiserver mit SMB transparent Failover\), kann mit Cau die automatisierte Cluster Aktualisierung ohne Auswirkung auf die Dienst Verfügbarkeit koordiniert werden.

## <a name="does-cau-support-updating-storage-spaces-direct-clusters"></a>Unterstützt Cau das Aktualisieren von direkte Speicherplätze Clustern?  
Ja. Cau unterstützt das Aktualisieren von [direkte Speicherplätze](../storage/storage-spaces/storage-spaces-direct-overview.md) Clustern unabhängig vom Bereitstellungstyp: hyperkonvergiert oder konvergiert. Insbesondere wird durch die Orchestrierung von Cau sichergestellt, dass das Anhalten der einzelnen Cluster Knoten darauf wartet, dass der zugrunde liegende Cluster Speicherplatz fehlerfrei ist.

## <a name="does-cau-work-with-windowsserver-2008r2-or-windows7"></a>Kann CAU für Windows Server 2008 R2 oder Windows 7 verwendet werden?  
Nein Cau koordiniert den Cluster Aktualisierungs Vorgang nur auf Computern, auf denen Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10, Windows 8.1 oder Windows 8 ausgeführt wird. Auf dem zu Aktualisier Ende Failovercluster muss Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt werden.
  
## <a name="is-cau-limited-to-specific-clustered-applications"></a>Ist Cau auf bestimmte Cluster Anwendungen beschränkt?  
Nein CAU ist der Typ der Clusteranwendung unbekannt. Cau ist eine externe Cluster\-Update Lösung, die oberhalb der Clustering-APIs und PowerShell-Cmdlets angeordnet ist. Daher kann mit Cau die Aktualisierung für eine beliebige geclusterte Anwendung koordiniert werden, die in einem Windows Server-Failovercluster konfiguriert ist.  
  
> [!NOTE]  
> Derzeit werden die folgenden geclusterten Arbeits Auslastungen für Cau getestet und zertifiziert: SMB, Hyper\-V, DFS-Replikation, DFS-Namespaces, iSCSI und NFS.  
  
## <a name="does-cau-support-updates-from-microsoft-update-and-windows-update"></a>Unterstützt CAU Updates von Microsoft Update und Windows Update?  
Ja. Standardmäßig wird Cau mit einem Plug\-in konfiguriert, das den Windows Update-Agent \(WUA-APIs\) Hilfsprogramm-APIs auf den Cluster Knoten verwendet. Die WUA-Infrastruktur kann so konfiguriert werden, dass Sie auf Microsoft Update und Windows Update verweist oder \(WSUS-\) als Quelle für Updates Windows Server Update Services.  
  
## <a name="does-cau-support-wsus-updates"></a>Unterstützt CAU WSUS-Updates?  
Ja. Standardmäßig wird Cau mit einem Plug\-in konfiguriert, das den Windows Update-Agent \(WUA-APIs\) Hilfsprogramm-APIs auf den Cluster Knoten verwendet. Die WUA-Infrastruktur kann so konfiguriert werden, dass Sie auf Microsoft Update und Windows Update oder auf eine lokale Windows Server Update Services \(WSUS-\) Server als Quelle für Updates verweist.  
  
## <a name="can-cau-apply-limited-distribution-release-updates"></a>Können von CAU Updates von Versionen mit eingeschränkter Verteilung angewendet werden?  
Ja. Eingeschränkte Verteilungs Releases \(LDR-\) Updates, auch Hotfixes genannt, werden nicht über Microsoft Update oder Windows Update veröffentlicht, sodass Sie nicht vom Windows Update-Agent heruntergeladen werden können \(WUA\) Plug\-, das standardmäßig von Cau verwendet wird.  
  
Cau enthält jedoch eine zweite Plug\-in, die Sie zum Anwenden von Hotfixupdates auswählen können. Diese Hotfix-Plug\-in können auch angepasst werden, um nicht\-Microsoft-Treiber, Firmware und BIOS-Updates anzuwenden.  
  
## <a name="can-i-use-cau-to-apply-cumulative-updates"></a>Kann ich CAU verwenden, um kumulative Updates anzuwenden?  
Ja. Wenn es sich bei den kumulativen Updates um Updates von Versionen mit allgemeiner Verteilung oder LDR-Updates handelt, können sie von CAU angewendet werden.  
  
## <a name="can-i-schedule-updates"></a>Kann ich Updates planen?  
Ja. CAU unterstützt die folgenden Aktualisierungsmodi, bei denen Updates jeweils geplant werden können:  
  
**Selbst\-Aktualisierung** Ermöglicht dem Cluster, sich selbst gemäß einem definierten Profil und einem regulären Zeitplan (z. b. während eines monatlichen Wartungs Fensters) zu aktualisieren. Sie können auch eine selbst\-Aktualisierung bei Bedarf jederzeit ausführen. Zum Aktivieren des selbst\-Aktualisierungs Modus müssen Sie dem Cluster die Cluster Rolle für Cluster fähiges aktualisieren hinzufügen. Die Self\-Update-Funktion von Cau wird wie jede andere gruppierte Arbeitsauslastung ausgeführt und kann problemlos mit den geplanten und ungeplanten Failover eines updatekoordinatorcomputers zusammenarbeiten.  
  
**Remote\-Aktualisierung** Hiermit können Sie jederzeit auf einem Computer mit Windows oder Windows Server eine Update Ausführung starten. Sie können eine Update Ausführung über das Cluster fähige Aktualisierungs Fenster oder mithilfe des PowerShell-Cmdlets **Aufruf\-caurun** starten. Remote\-Aktualisierung ist der Standard Aktualisierungs Modus für Cau. Mit der Aufgabenplanung können Sie das Cmdlet [Invoke-CauRun](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-caurun) nach einem gewünschten Zeitplan auf einem Remotecomputer ausführen, bei dem es sich nicht um einen der Clusterknoten handelt.  
  
## <a name="can-i-schedule-updates-to-apply-during-a-backup"></a>Können Updates geplant werden, die während einer Sicherung angewendet werden sollen?  
Ja. In diesem Zusammenhang werden von Cau keine Einschränkungen auferlegt. Das Durchführen von Software Updates auf einem Server \(mit den zugehörigen potenziellen Neustarts\) während der Ausführung einer Server Sicherung ist jedoch keine bewährte Vorgehensweise. Beachten Sie, dass von CAU nur Cluster-APIs verwendet werden, um Ressourcenfailover und -failbacks zu bestimmen. Daher ist CAU der Serversicherungsstatus nicht bekannt.  
  
## <a name="can-cau-work-with-configuration-manager"></a>Kann Cau mit Configuration Manager arbeiten?  
Cau ist ein Tool, das Software Updates auf einem Cluster Knoten koordiniert und Configuration Manager auch Server Software Updates ausführt. Es ist wichtig, diese Tools so zu konfigurieren, dass Sie keine überlappende Abdeckung derselben Server in einer Daten Center Bereitstellung haben, einschließlich der Verwendung unterschiedlicher Windows Server Update Services Server. Dadurch wird sichergestellt, dass das Ziel für die Verwendung von Cau nicht versehentlich besiegt wird, da Configuration Manager\-gesteuerte Aktualisierung keine Cluster Informationen enthält.  
  
## <a name="do-i-need-administrative-credentials-to-run-cau"></a>Benötige ich Administratoranmeldeinformationen, um CAU auszuführen?  
Ja. Zum Ausführen der CAU-Tools sind Administratoranmeldeinformationen auf dem lokalen Server oder das Benutzerrecht **Annehmen der Clientidentität nach Authentifizierung** auf dem lokalen Server oder Clientcomputer erforderlich, auf dem CAU ausgeführt wird. Zum Koordinieren von Softwareupdates auf den Clusterknoten sind für CAU jedoch Clusteradministratoranmeldeinformationen auf allen Knoten erforderlich. Obwohl die Cau-Benutzeroberfläche ohne die Anmelde Informationen gestartet werden kann, werden Sie zur Eingabe der Anmelde Informationen für den Cluster Administrator aufgefordert, wenn eine Verbindung mit einer Cluster Instanz hergestellt wird, um eine Vorschau  
  
## <a name="can-i-script-cau"></a>Kann ich ein Skript für Cau erstellen?  
Ja. Cau verfügt über PowerShell-Cmdlets, die einen umfangreichen Satz von Skript Optionen bieten. Dies sind dieselben Cmdlets, die von der CAU-Benutzeroberfläche zum Ausführen von CAU-Aktionen aufgerufen werden.  

## <a name="what-happens-to-active-clustered-roles"></a>Was geschieht mit aktiven Cluster Rollen?

Cluster Rollen \(früher als Anwendungs-und Dienst\) bezeichnet, die auf einem Knoten aktiv sind, führen ein Failover auf andere Knoten aus, bevor die Software Aktualisierung beginnen kann. Diese Failover werden von CAU mithilfe des Wartungsmodus koordiniert, der den Knoten anhält und alle aktiven Clusterrollen auf ihm ausgleicht. Wenn die Softwareupdates abgeschlossen sind, wird der Knoten durch CAU fortgesetzt, und für die Clusterrollen wird ein Failback auf den aktualisierten Knoten ausgeführt. Dadurch wird sichergestellt, dass die Verteilung von Clusterrollen im Vergleich zu den Knoten bei den CAU-Aktualisierungsausführungen auf einem Cluster gleich bleibt.  
  
## <a name="how-does-cau-select-target-nodes-for-clustered-roles"></a>Wie werden Zielknoten für Cluster Rollen von Cau ausgewählt?

Von CAU werden Cluster-APIs verwendet, um die Failover zu koordinieren. Die Clustering-API-Implementierung wählt die Zielknoten aus, indem Sie sich auf interne Metriken und eine intelligente Platzierungs-Heuristik \(wie Arbeits Auslastungs Ebenen\) auf den Zielknoten.  
  
## <a name="does-cau-load-balance-the-clustered-roles"></a>Führt der Cau-Lastenausgleich für die Cluster Rollen aus?

Cau führt keinen Lastenausgleich für die gruppierten Knoten durch, sondern versucht, die Verteilung der Cluster Rollen beizubehalten. Wenn das Update eines Clusterknotens durch CAU beendet wird, wird für die zuvor auf dem jeweiligen Knoten gehosteten Clusterrollen ein Failback ausgeführt. Von CAU werden Cluster-APIs verwendet, um für die Ressourcen ein Failback zum Anfang des angehaltenen Vorgangs auszuführen. Wenn keine ungeplanten Failover und bevorzugten Besitzereinstellungen vorhanden sind, bleibt die Verteilung der Clusterrollen daher unverändert.  
  
## <a name="how-does-cau-select-the-order-of-nodes-to-update"></a>Wie wird von CAU die Reihenfolge der zu aktualisierenden Knoten ausgewählt?  
Standardmäßig wird die Reihenfolge der zu aktualisierenden Knoten von CAU basierend auf dem Aktivitätsgrad ausgewählt. Die Knoten, auf denen die wenigsten Clusterrollen gehostet werden, werden zuerst aktualisiert. Ein Administrator kann jedoch eine bestimmte Reihenfolge für die Aktualisierung der Knoten angeben, indem er auf der Cau-Benutzeroberfläche einen Parameter für die Aktualisierungs Laufzeit oder mithilfe der PowerShell-Cmdlets angibt.  
  
## <a name="what-happens-if-a-cluster-node-is-offline"></a>Was geschieht, wenn ein Cluster Knoten offline ist?

Der Administrator, der die Aktualisierungsausführung initiiert, kann den zulässigen Schwellenwert für die Anzahl von Knoten angeben, die offline sein können. Daher kann eine Aktualisierungsausführung selbst dann auf einem Cluster fortgesetzt werden, wenn keiner der Clusterknoten online ist.  
  
## <a name="can-i-use-cau-to-update-only-a-single-node"></a>Kann ich Cau verwenden, um nur einen einzelnen Knoten zu aktualisieren?  
Nein Cau ist ein Cluster\-Tool für das Bereichs bezogene Update, sodass Sie nur zu Aktualisier Ende Cluster auswählen können. Wenn Sie einen einzelnen Knoten aktualisieren möchten, können Sie vorhandene Serveraktualisierungstools außerhalb von CAU verwenden.  
  
## <a name="can-cau-report-updates-that-are-initiated-from-outside-cau"></a>Können von Cau Updates gemeldet werden, die außerhalb von Cau initiiert wurden?  
Nein Von CAU können nur Aktualisierungsausführungen gemeldet werden, die innerhalb von CAU initiiert wurden. Wenn jedoch eine nachfolgende Cau-Aktualisierungs Laufzeit gestartet wird, werden Updates, die über nicht\-Cau-Methoden installiert wurden, entsprechend berücksichtigt, um die zusätzlichen Updates zu bestimmen, die möglicherweise für die einzelnen Cluster Knoten gelten.  
  
## <a name="can-cau-support-my-unique-it-process-needs"></a>Kann Cau meine individuellen Anforderungen an IT-Prozesse unterstützen?  
Ja. CAU bietet die folgenden Dimensionen der Flexibilität, um den individuellen IT-Prozessanforderungen von Unternehmenskunden gerecht zu werden:  
  
**Skripts** Bei einer Update-Lauf Zeit kann ein PowerShell-Skript vor\-Update und ein PowerShell-Skript nach\-Aktualisierung angegeben werden. Das Skript Pre\-Update wird auf jedem Cluster Knoten ausgeführt, bevor der Knoten angehalten wird. Nachdem die Knoten Updates installiert wurden, wird das Skript nach\-Aktualisierung auf jedem Cluster Knoten ausgeführt.  
  
> [!NOTE]  
> .NET Framework 4,6 oder 4,5 und PowerShell müssen auf jedem Cluster Knoten installiert sein, auf dem Sie das Pre\-Update ausführen und\-Update Skripts ausführen möchten. Außerdem müssen Sie PowerShell-Remoting auf den Cluster Knoten aktivieren. Ausführliche Informationen zu den Systemanforderungen finden Sie unter [Anforderungen und bewährte Methoden für das Cluster fähige aktualisieren](cluster-aware-updating-requirements.md).  
  
**Erweiterte Aktualisierungs Lauf Optionen** Der Administrator kann zusätzlich einen umfangreichen Satz von erweiterten Optionen für die Aktualisierungs Laufzeit angeben, z. b. die maximale Anzahl von Wiederholungs versuchen für den Update Vorgang auf jedem Knoten. Diese Optionen können entweder über die Cau-Benutzeroberfläche oder über die PowerShell-Cmdlets für Cau angegeben werden. Diese benutzerdefinierten Einstellungen können in einem Profil für die Updateausführung gespeichert und bei späteren Updateausführungen wiederverwendet werden.  
  
**Öffentliches Plug\-in der Architektur** Cau enthält Features zum Registrieren, Aufheben der Registrierung und Auswählen von Plug\-ins. Cau wird mit zwei Standard-Plug\-ins ausgeliefert: eine koordiniert den Windows Update Agent \(WUA-\)-APIs auf jedem Cluster Knoten. die zweite Anwendung wendet Hotfixes an, die manuell in eine Dateifreigabe kopiert werden, auf die die Cluster Knoten zugreifen können. Wenn ein Unternehmen besondere Anforderungen hat, die mit diesen beiden Plug\-ins nicht erfüllt werden können, kann das Unternehmen gemäß der öffentlichen API-Spezifikation ein neues Cau-Plug\-in erstellen. Weitere Informationen finden Sie [unter Referenz für Cluster\-fähiges Aktualisieren von Plug\-](https://msdn.microsoft.com/library/hh418084(VS.85).aspx).  
  
Informationen zum Konfigurieren und Anpassen von Plug\-ins für Cluster fähiges aktualisieren, um unterschiedliche Aktualisierungs Szenarien zu unterstützen, finden Sie unter [Funktionsweise von Plug\-ins](assetId:///847b571b-12b3-473c-953f-75a5a1f51333).  
  
## <a name="how-can-i-export-the-cau-preview-and-update-results"></a>Wie kann ich die CAU-Vorschau- und -Aktualisierungsergebnisse exportieren?  
Cau bietet Exportoptionen über die Befehls\--Zeilen Schnittstelle und über die Benutzeroberfläche.  
  
**Optionen für Befehls\-Zeilen Schnittstelle:**  
  
-   Vorschau Ergebnisse mit dem PowerShell-Cmdlet- **Aufruf\-causcan | ConvertTo\-XML**. Ausgabe: XML  
  
-   Melden Sie Ergebnisse mit dem PowerShell-Cmdlet **-Aufruf\-caurun | ConvertTo\-XML**. Ausgabe: XML  
  
-   Berichts Ergebnisse mithilfe des PowerShell-Cmdlets **Get\-caureport | Exportieren Sie\-caureport**. Ausgabe: HTML, CSV  
  
**Benutzeroberflächen Optionen:**  
  
-   Kopieren Sie die Berichtsergebnisse aus dem Bildschirm **Vorschau der Updates anzeigen** . Ausgabe: CSV  
  
-   Kopieren Sie die Berichtsergebnisse aus dem Bildschirm **Bericht generieren** . Ausgabe: CSV  
  
-   Exportieren Sie die Berichtsergebnisse aus dem Bildschirm **Bericht generieren** . Ausgabe: HTML  
  
## <a name="how-do-i-install-cau"></a>Wie installiere ich CAU?  
Eine CAU-Installation ist nahtlos in das Feature "Failoverclustering" integriert. CAU wird wie folgt installiert:  
  
-   Wenn das Failoverclustering auf einem Cluster Knoten installiert ist, wird das Cau-Windows-Verwaltungsinstrumentation \(WMI-\)-Anbieter automatisch installiert.  
  
-   Wenn das Feature Failoverclustering-Tools auf einem Server oder Client Computer installiert ist, werden die Benutzeroberfläche für das Cluster fähige aktualisieren und die PowerShell-Cmdlets automatisch installiert.
  
## <a name="does-cau-need-components-running-on-the-cluster-nodes-that-are-being-updated"></a>Muss für Cau Komponenten auf den Cluster Knoten ausgeführt werden, die aktualisiert werden?  
Für Cau muss kein Dienst auf den Cluster Knoten ausgeführt werden. Für Cau muss jedoch eine Softwarekomponente \(der WMI-Anbieter\) auf den Cluster Knoten installiert sein. Diese Komponente wird mit dem Feature Failoverclustering installiert.  
  
Zum Aktivieren des selbst\-Aktualisierungs Modus muss die Cluster Rolle für Cluster fähiges aktualisieren ebenfalls dem Cluster hinzugefügt werden.  
  
## <a name="what-is-the-difference-between-using-cau-and-vmm"></a>Worin besteht der Unterschied zwischen der Verwendung von Cau und VMM?  
  
-   System Center Virtual Machine Manager \(VMM-\) ist darauf ausgerichtet, nur Hyper\-V-Cluster zu aktualisieren, während mit Cau beliebige Typen unterstützter Failovercluster, einschließlich Hyper\-v-Cluster, aktualisiert werden können.  
  
-   VMM erfordert zusätzliche Lizenzen, während Cau für alle Windows Server lizenziert ist. Die CAU-Features, -Tools und -Benutzeroberfläche werden mit Failoverclusteringkomponenten installiert.  
  
-   Wenn Sie bereits eine System Center-Lizenz besitzen, können Sie VMM weiterhin verwenden, um Hyper\-V-Cluster zu aktualisieren, da es eine integrierte Verwaltungs-und Software Aktualisierungs Funktion bietet.  
  
-   Cau wird nur auf Clustern unterstützt, auf denen Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 ausgeführt werden. VMM unterstützt auch Hyper\-V-Cluster auf Computern, auf denen Windows Server 2008 R2 und Windows Server 2008 ausgeführt werden.  
  
## <a name="can-i-use-remote-updating-on-a-cluster-that-is-configured-for-self-updating"></a>Kann ich die Remote\-Aktualisierung auf einem Cluster verwenden, der für die selbst\-Aktualisierung konfiguriert ist?  
Ja. Ein Failovercluster in einer selbst\-Aktualisierungs Konfiguration kann mithilfe von Remote\-aktualisieren bei\-Bedarf aktualisiert werden, so wie Sie eine Windows Update Überprüfung jederzeit auf dem Computer erzwingen können, auch wenn Windows Update für die automatische Installation von Updates konfiguriert ist. Sie müssen jedoch sicherstellen, dass gerade keine Aktualisierungsausführung erfolgt.  
  
## <a name="can-i-reuse-my-cluster-update-settings-across-clusters"></a>Kann ich meine Clusteraktualisierungseinstellung für mehrere Cluster wiederverwenden?  
Ja. Von CAU werden einige Aktualisierungsausführungsoptionen unterstützt, mit denen das Verhalten der Aktualisierungsausführung beim Aktualisieren des Clusters bestimmt wird. Diese Optionen können als Aktualisierungsausführungsprofil gespeichert und für beliebige Cluster wiederverwendet werden. Es wird empfohlen, Ihre Einstellungen für Failovercluster mit ähnlichen Aktualisierungsanforderungen zu speichern und wiederzuverwenden. Beispielsweise können Sie für alle Microsoft SQL Server Cluster, die Geschäfts\-kritische Dienste unterstützen, das Profil "Geschäfts\-kritische SQL Server Cluster Update-Profilerstellung" erstellen.  
  
## <a name="where-is-the-cau-plug-in-specification"></a>Wo ist der Cau-Plug\-in der Spezifikation?  
  
-   [Cluster\-fähiges Aktualisieren von Plug\-als Referenz](https://msdn.microsoft.com/library/hh418084(VS.85).aspx)  
  
-   [Plug-in für Cluster fähiges aktualisieren (Plug\-in Beispiel](https://code.msdn.microsoft.com/windowsdesktop/Cluster-Aware-Updating-6a8854c9)  
  
## <a name="see-also"></a>Weitere Informationen:  
  
-   [Clusterfähige Aktualisierung – Übersicht](cluster-aware-updating.md)  
  
