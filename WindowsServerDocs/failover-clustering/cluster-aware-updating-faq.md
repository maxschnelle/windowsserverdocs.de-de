---
ms.assetid: 6416d125-bcaf-433d-971a-2f0283bca2c2
title: Clusterfähige Aktualisierung – gestellte häufig Fragen
ms.topic: article
ms.prod: windows-server-threshold
manager: dongill
ms.author: jgerend
author: JasonGerend
ms.date: 04/28/2017
description: Antworten auf häufig gestellte Fragen zur Cluster-Aware Updating in Windows Server.
ms.openlocfilehash: f9009811093823554f16295cc1205f1b99ead93f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882521"
---
# <a name="cluster-aware-updating-frequently-asked-questions"></a>Clusterfähiges aktualisieren: Häufig gestellte Fragen

> Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

[Cluster-Aware Updating](cluster-aware-updating.md) \(CAU\) ist ein Feature, das koordiniert die Software aktualisiert auf allen Servern in einem Failovercluster auf eine Weise, die die dienstverfügbarkeit auswirkt, nicht mehr als ein geplantes Failover eines Clusterknotens. Bei einigen Anwendungen mit stets Verfügbarkeitsfeatures \(wie z. B. Hyper\-V mit Livemigration oder SMB 3.x-Dateiserver mit SMB Transparent Failover\), kann durch CAU koordiniert automatisierte Clusteraktualisierung ohne Auswirkungen auf die dienstverfügbarkeit.

## <a name="does-cau-support-updating-storage-spaces-direct-clusters"></a>Unterstützt CAU die Aktualisierung "direkte Speicherplätze"-Cluster?  
Ja. Unterstützt CAU die Aktualisierung ["direkte Speicherplätze"](../storage/storage-spaces/storage-spaces-direct-overview.md) Cluster unabhängig von der Art der Bereitstellung: hyperkonvergenten oder konvergiert. Insbesondere wird CAU Orchestrierung wartet, das Anhalten der einzelnen Knoten für den zugrunde liegenden gruppierten Speicherplatz fehlerfrei sind.

## <a name="does-cau-work-with-windowsserver-2008r2-or-windows7"></a>Kann CAU für Windows Server 2008 R2 oder Windows 7 verwendet werden?  
Nein. CAU koordiniert die Clusteraktualisierung nur auf Computern mit Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10, Windows 8.1 oder Windows 8. Im Failovercluster aktualisiert wird, muss Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt.
  
## <a name="is-cau-limited-to-specific-clustered-applications"></a>Wird für clusterfähiges aktualisieren auf bestimmte Clusteranwendungen beschränkt?  
Nein. CAU ist der Typ der Clusteranwendung unbekannt. CAU ist ein externer Cluster\-aktualisieren die Lösung, die über die Cluster-APIs und PowerShell-Cmdlets gelagert ist. Daher kann durch CAU koordiniert Aktualisierung für eine beliebige geclusterte Anwendung, die in einem Windows Server-Failovercluster konfiguriert ist.  
  
> [!NOTE]  
> Derzeit werden die folgenden geclusterten arbeitsauslastungen getestet und zertifiziert für clusterfähiges aktualisieren: SMB, Hyper\-V, DFS-Replikation, DFS-Namespaces, iSCSI und NFS.  
  
## <a name="does-cau-support-updates-from-microsoft-update-and-windows-update"></a>Unterstützt CAU Updates von Microsoft Update und Windows Update?  
Ja. Standardmäßig wird CAU mit eine Plug & konfiguriert\-, verwendet der Windows Update-Agent \(WUA\) Dienstprogramm-APIs auf den Clusterknoten. Die WUA-Infrastruktur kann so konfiguriert werden, dass die auf Microsoft Update und Windows Update oder auf Windows Server Update Services verweisen \(WSUS\) als Quelle des Updates.  
  
## <a name="does-cau-support-wsus-updates"></a>Unterstützt CAU WSUS-Updates?  
Ja. Standardmäßig wird CAU mit eine Plug & konfiguriert\-, verwendet der Windows Update-Agent \(WUA\) Dienstprogramm-APIs auf den Clusterknoten. Die WUA-Infrastruktur kann so konfiguriert werden, dass die auf Microsoft Update und Windows Update oder auf einem lokalen Windows Server Update Services verweisen \(WSUS\) Server als Quelle des Updates.  
  
## <a name="can-cau-apply-limited-distribution-release-updates"></a>Können von CAU Updates von Versionen mit eingeschränkter Verteilung angewendet werden?  
Ja. Eingeschränkte GDR \(LDR\) Updates, so genannte Hotfixes werden nicht über Microsoft Update oder Windows Update veröffentlicht, damit sie nicht von der Windows Update-Agent heruntergeladen werden können \(WUA\) einbinden\-, da für clusterfähiges aktualisieren in der Standardeinstellung verwendet.  
  
CAU bietet jedoch eine zweite Plug\-, Sie wählen können, um die Hotfix-Updates anwenden. Dieser Hotfix-Plug\-in kann auch so angepasst werden nicht angewendet\-Microsoft-Treiber, Firmware und BIOS-Updates.  
  
## <a name="can-i-use-cau-to-apply-cumulative-updates"></a>Kann ich CAU verwenden, um kumulative Updates anzuwenden?  
Ja. Wenn es sich bei den kumulativen Updates um Updates von Versionen mit allgemeiner Verteilung oder LDR-Updates handelt, können sie von CAU angewendet werden.  
  
## <a name="can-i-schedule-updates"></a>Kann ich Updates planen?  
Ja. CAU unterstützt die folgenden Aktualisierungsmodi, bei denen Updates jeweils geplant werden können:  
  
**Self\-aktualisieren** kann der Cluster selbst gemäß eines definierten Profils und regelmäßigen Zeitplans, z. B. während eines monatlichen Wartungszeitfensters aktualisieren. Sie können auch ein selbstsigniertes starten\-aktualisiert bei Bedarf jederzeit ausführen. So aktivieren Sie Self-Service\-Updatemodus, müssen Sie die Clusterrolle für clusterfähiges Aktualisieren mit dem Cluster hinzufügen. Für clusterfähiges aktualisieren selbst\-aktualisieren die Funktion wie jede andere geclusterte Arbeitslast ausgeführt, und es funktioniert nahtlos mit der geplanten und ungeplanten Failover eines updatekoordinatorcomputers.  
  
**Remote\-aktualisieren** ermöglicht es Ihnen, eine Updateausführung zu einem beliebigen Zeitpunkt auf einem Computer unter Windows oder Windows Server zu starten. Sie können eine Aktualisierungsausführung über das Fenster des clusterfähigen Aktualisierens oder Starten der **Invoke\-CauRun** PowerShell-Cmdlet. Remote\-aktualisieren, ist der standardaktualisierungsmodus für CAU. Mit der Aufgabenplanung können Sie das Cmdlet [Invoke-CauRun](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-caurun) nach einem gewünschten Zeitplan auf einem Remotecomputer ausführen, bei dem es sich nicht um einen der Clusterknoten handelt.  
  
## <a name="can-i-schedule-updates-to-apply-during-a-backup"></a>Kann ich während einer Sicherung anzuwendenden Updates planen?  
Ja. CAU festlegen keine Einschränkungen in dieser Hinsicht. Ausführen von Softwareupdates jedoch auf einem Server \(die zugeordneten möglicherweise neu gestartet wird\) während eine Sicherung wird ausgeführt ist keine bewährte IT-Methode. Beachten Sie, dass von CAU nur Cluster-APIs verwendet werden, um Ressourcenfailover und -failbacks zu bestimmen. Daher ist CAU der Serversicherungsstatus nicht bekannt.  
  
## <a name="can-cau-work-with-system-center-configuration-manager"></a>Werden CAU kann mit System Center Configuration Manager verwendet?  
CAU ist ein Tool, das Softwareupdates auf einem Clusterknoten koordiniert, und Configuration Manager werden auch serversoftwareupdates ausgeführt. Es ist wichtig, diese Tools zu konfigurieren, sodass sie keine überlappende Abdeckung derselben Server in jeder Datacenter-Bereitstellung, einschließlich der Verwendung von unterschiedlichen Windows Server Update Services-Servern. Dadurch wird sichergestellt, dass die Absicht hinter der Verwendung von CAU nicht versehentlich aufgehoben wird, da Configuration Manager\-testgesteuerte aktualisiert nicht die Standortinformationen für den Cluster integrieren.  
  
## <a name="do-i-need-administrative-credentials-to-run-cau"></a>Benötige ich Administratoranmeldeinformationen, um CAU auszuführen?  
Ja. Zum Ausführen der CAU-Tools sind Administratoranmeldeinformationen auf dem lokalen Server oder das Benutzerrecht **Annehmen der Clientidentität nach Authentifizierung** auf dem lokalen Server oder Clientcomputer erforderlich, auf dem CAU ausgeführt wird. Zum Koordinieren von Softwareupdates auf den Clusterknoten sind für CAU jedoch Clusteradministratoranmeldeinformationen auf allen Knoten erforderlich. Auch wenn die CAU-UI ohne die Anmeldeinformationen gestartet werden kann, werden die clusteradministratoranmeldeinformationen Verbindung mit einer Clusterinstanz zum Anzeigen einer updatevorschau oder zum Anwenden von Updates.  
  
## <a name="can-i-script-cau"></a>Kann ich CAU Skript?  
Ja. CAU enthält PowerShell-Cmdlets, die einen umfangreichen Satz von Skriptoptionen zu bieten. Dies sind dieselben Cmdlets, die von der CAU-Benutzeroberfläche zum Ausführen von CAU-Aktionen aufgerufen werden.  

## <a name="what-happens-to-active-clustered-roles"></a>Was geschieht mit aktiven clusterrollen?

Gruppierte Rollen \(ehemals Anwendungen und Dienste\) , die auf einem Knoten aktiv sind, führen Sie ein Failover auf andere Knoten vor der Aktualisierung der Software beginnen kann. Diese Failover werden von CAU mithilfe des Wartungsmodus koordiniert, der den Knoten anhält und alle aktiven Clusterrollen auf ihm ausgleicht. Wenn die Softwareupdates abgeschlossen sind, wird der Knoten durch CAU fortgesetzt, und für die Clusterrollen wird ein Failback auf den aktualisierten Knoten ausgeführt. Dadurch wird sichergestellt, dass die Verteilung von Clusterrollen im Vergleich zu den Knoten bei den CAU-Aktualisierungsausführungen auf einem Cluster gleich bleibt.  
  
## <a name="how-does-cau-select-target-nodes-for-clustered-roles"></a>Wie wird CAU die Zielknoten für clusterrollen ausgewählt?

Von CAU werden Cluster-APIs verwendet, um die Failover zu koordinieren. Der clustering-API-Implementierung wählt die Knoten durch die Verwendung interner Metriken und intelligenter platzierungsheuristiken \(z. B. arbeitsauslastungsstufen\) alle Zielknoten.  
  
## <a name="does-cau-load-balance-the-clustered-roles"></a>Lastenausgleich CAU die clusterrollen?

CAU nicht den Lastenausgleich die gruppierten Knoten, aber es wird versucht, die Verteilung der clusterrollen beizubehalten. Wenn das Update eines Clusterknotens durch CAU beendet wird, wird für die zuvor auf dem jeweiligen Knoten gehosteten Clusterrollen ein Failback ausgeführt. Von CAU werden Cluster-APIs verwendet, um für die Ressourcen ein Failback zum Anfang des angehaltenen Vorgangs auszuführen. Wenn keine ungeplanten Failover und bevorzugten Besitzereinstellungen vorhanden sind, bleibt die Verteilung der Clusterrollen daher unverändert.  
  
## <a name="how-does-cau-select-the-order-of-nodes-to-update"></a>Wie wird von CAU die Reihenfolge der zu aktualisierenden Knoten ausgewählt?  
Standardmäßig wird die Reihenfolge der zu aktualisierenden Knoten von CAU basierend auf dem Aktivitätsgrad ausgewählt. Die Knoten, auf denen die wenigsten Clusterrollen gehostet werden, werden zuerst aktualisiert. Allerdings kann ein Administrator für das Aktualisieren der Knoten, durch Angabe eines Parameters für die Updateausführung in die CAU-UI oder mithilfe von PowerShell-Cmdlets eine bestimmte Reihenfolge angeben.  
  
## <a name="what-happens-if-a-cluster-node-is-offline"></a>Was geschieht, wenn ein Knoten offline ist?

Der Administrator, der die Aktualisierungsausführung initiiert, kann den zulässigen Schwellenwert für die Anzahl von Knoten angeben, die offline sein können. Daher kann eine Aktualisierungsausführung selbst dann auf einem Cluster fortgesetzt werden, wenn keiner der Clusterknoten online ist.  
  
## <a name="can-i-use-cau-to-update-only-a-single-node"></a>Kann ich CAU verwenden, um nur einen einzelnen Knoten zu aktualisieren?  
Nein. CAU ist ein Cluster\-Bereichsbezogene Tool aktualisieren, sodass er nur zu aktualisierende Cluster auswählen kann. Wenn Sie einen einzelnen Knoten aktualisieren möchten, können Sie vorhandene Serveraktualisierungstools außerhalb von CAU verwenden.  
  
## <a name="can-cau-report-updates-that-are-initiated-from-outside-cau"></a>Kann CAU Updates melden, die außerhalb von CAU initiiert werden?  
Nein. Von CAU können nur Aktualisierungsausführungen gemeldet werden, die innerhalb von CAU initiiert wurden. Aber wenn eine nachfolgende CAU-Aktualisierungsausführung gestartet wird, Updates, die durch nicht installiert wurden\-CAU-Methoden sind entsprechend interpretiert, um die zusätzlichen Updates zu bestimmen, die auf jedem Clusterknoten angewendet werden kann.  
  
## <a name="can-cau-support-my-unique-it-process-needs"></a>Können CAU-Unterstützung, die meinen individuellen IT-prozessanforderungen muss?  
Ja. CAU bietet die folgenden Dimensionen der Flexibilität, um den individuellen IT-Prozessanforderungen von Unternehmenskunden gerecht zu werden:  
  
**Skripts** eine Aktualisierungsausführung kann Geben Sie einen vorangestellten\-aktualisieren Sie PowerShell-Skript und Post\-PowerShell-Skript zu aktualisieren. Des präproduktionsclients\-Updateskript wird auf jedem Clusterknoten ausgeführt, bevor der Knoten angehalten wird. Der Beitrag\-Updateskript wird auf jedem Clusterknoten ausgeführt, nachdem die knotenupdates installiert wurden.  
  
> [!NOTE]  
> .NET Framework 4.6 "oder" 4.5 "und" PowerShell muss auf jedem Clusterknoten, die Sie auf Ausführen des präproduktionsclients installiert sein\-aktualisieren und buchen\-Skripts zu aktualisieren. Sie müssen auch die PowerShell-Remoting auf den Clusterknoten aktivieren. Ausführliche Informationen zu den Systemanforderungen finden Sie unter [Anforderungen und Best Practices for Cluster-Aware Updating](cluster-aware-updating-requirements.md).  
  
**Erweiterte updateausführungsoptionen** der Administrator kann darüber hinaus angeben, eine Reihe erweiterter updateausführungsoptionen wie z. B. die maximale Anzahl von Wiederholungen, die der Updatevorgang auf jedem Knoten wiederholt wird. Diese Optionen können mithilfe der CAU-UI oder der CAU-PowerShell-Cmdlets angegeben werden. Diese benutzerdefinierten Einstellungen können in einem Profil für die Updateausführung gespeichert und bei späteren Updateausführungen wiederverwendet werden.  
  
**Öffentliche Plug-in\-in Architektur** CAU bietet Features zum Registrieren, Aufheben der Registrierung, und wählen Sie anschließen\-ins. Cau bietet zwei Standard-Plug &\-ins: eines koordiniert der Windows Update-Agent \(WUA\) APIs auf jedem Clusterknoten installieren; das zweite wendet Hotfixes, die manuell in eine Dateifreigabe kopiert werden, die an die Clusterknoten zugegriffen werden kann. Wenn ein Unternehmen individuelle Anforderungen hat, die mit diesen nicht erfüllt werden können, die zwei anschließen\-ins, die Unternehmen kann erstellen ein neues CAU-Plug\-entsprechend in der öffentlichen API-Spezifikation. Weitere Informationen finden Sie unter [Cluster\-bewusst Aktualisieren von Plug-Ins\-Referenz](https://msdn.microsoft.com/library/hh418084(VS.85).aspx).  
  
Schließen Sie Informationen zum Konfigurieren und Anpassen von CAU\-ins zur Unterstützung der verschiedenen Szenarien aktualisieren finden Sie unter [wie anschließen\-ins funktionieren](assetId:///847b571b-12b3-473c-953f-75a5a1f51333).  
  
## <a name="how-can-i-export-the-cau-preview-and-update-results"></a>Wie kann ich die CAU-Vorschau- und -Aktualisierungsergebnisse exportieren?  
CAU bietet Exportoptionen über den Befehl\-Befehlszeilenschnittstelle (CLI) und über die Benutzeroberfläche.  
  
**Befehl\-Schnittstelle Befehlszeilenoptionen:**  
  
-   Vorschauergebnisse mithilfe des PowerShell-Cmdlets **Invoke\-CauScan | ConvertTo\-Xml**. Ausgabe: XML  
  
-   Berichtsergebnisse mithilfe des PowerShell-Cmdlets **Invoke\-CauRun | ConvertTo\-Xml**. Ausgabe: XML  
  
-   Berichtsergebnisse mithilfe des PowerShell-Cmdlets **erhalten\-CauReport | Exportieren Sie\-CauReport**. Ausgabe: HTML, CSV  
  
**Optionen der Benutzeroberfläche:**  
  
-   Kopieren Sie die Berichtsergebnisse aus dem Bildschirm **Vorschau der Updates anzeigen**. Ausgabe: CSV  
  
-   Kopieren Sie die Berichtsergebnisse aus dem Bildschirm **Bericht generieren** . Ausgabe: CSV  
  
-   Exportieren Sie die Berichtsergebnisse aus dem Bildschirm **Bericht generieren** . Ausgabe: HTML  
  
## <a name="how-do-i-install-cau"></a>Wie installiere ich CAU?  
Eine CAU-Installation ist nahtlos in das Feature "Failoverclustering" integriert. CAU wird wie folgt installiert:  
  
-   Wenn Failoverclustering installiert ist, auf einem Clusterknoten, die CAU-Windows-Verwaltungsinstrumentierung \(WMI\) Anbieter wird automatisch installiert.  
  
-   Wenn das Feature Failoverclustering-Tools auf einem Server oder Clientcomputer installiert ist, werden die Benutzeroberfläche für clusterfähiges aktualisieren und PowerShell-Cmdlets automatisch installiert.
  
## <a name="does-cau-need-components-running-on-the-cluster-nodes-that-are-being-updated"></a>Ist für clusterfähiges aktualisieren erforderlich Komponenten auf den Clusterknoten, die aktualisiert werden?  
CAU benötigt keinen Dienst, der auf den Clusterknoten. CAU benötigt jedoch eine Softwarekomponente \(der WMI-Anbieter\) auf den Clusterknoten installiert. Diese Komponente wird mit dem Feature Failoverclustering installiert.  
  
So aktivieren Sie Self-Service\-Updatemodus an, die Clusterrolle für clusterfähiges aktualisieren muss außerdem werden dem Cluster hinzugefügt.  
  
## <a name="what-is-the-difference-between-using-cau-and-vmm"></a>Was ist der Unterschied zwischen der Verwendung von CAU und VMM?  
  
-   System Center Virtual Machine Manager- \(VMM\) konzentriert sich auf Update nur Hyper\-V-Cluster, während CAU kann jede Art von unterstützter Failovercluster, einschließlich Hyper aktualisieren\-V-Cluster.  
  
-   VMM erfordert zusätzliche Lizenzen, während CAU für alle Windows Server lizenziert ist. Die CAU-Features, -Tools und -Benutzeroberfläche werden mit Failoverclusteringkomponenten installiert.  
  
-   Wenn Sie bereits System Center-Lizenz besitzen, Sie können weiterhin mit VMM Hyper aktualisieren\-V-Cluster, da es sich um eine integrierte Verwaltungs- und softwareaktualisierungserfahrung bietet.  
  
-   CAU wird nur auf Clustern unterstützt, auf denen Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 ausgeführt werden. VMM unterstützt auch Hyper\-V-Cluster auf Computern unter Windows Server 2008 R2 und Windows Server 2008.  
  
## <a name="can-i-use-remote-updating-on-a-cluster-that-is-configured-for-self-updating"></a>Kann ich verwenden remote\-aktualisieren, die in einem Cluster, die für Self-Service konfiguriert ist\-aktualisieren?  
Ja. Eines Failoverclusters in einem selbstaktivierten\-Aktualisieren der Konfiguration kann aktualisiert werden, über Remote\-aktualisieren auf\-erfordern, wie Sie eine Windows Update-Überprüfung zu einem beliebigen Zeitpunkt auf dem Computer erzwingen können, selbst wenn Windows Update konfiguriert ist Updates automatisch installiert. Sie müssen jedoch sicherstellen, dass gerade keine Aktualisierungsausführung erfolgt.  
  
## <a name="can-i-reuse-my-cluster-update-settings-across-clusters"></a>Kann ich meine Clusteraktualisierungseinstellung für mehrere Cluster wiederverwenden?  
Ja. Von CAU werden einige Aktualisierungsausführungsoptionen unterstützt, mit denen das Verhalten der Aktualisierungsausführung beim Aktualisieren des Clusters bestimmt wird. Diese Optionen können als Aktualisierungsausführungsprofil gespeichert und für beliebige Cluster wiederverwendet werden. Es wird empfohlen, Ihre Einstellungen für Failovercluster mit ähnlichen Aktualisierungsanforderungen zu speichern und wiederzuverwenden. Sie können z. B. Erstellen einer "Business\-kritische SQL Server-Cluster aktualisieren ausführen-Profil" für alle Microsoft SQL Server-Cluster, die Unterstützung von Business\-wichtige Dienste.  
  
## <a name="where-is-the-cau-plug-in-specification"></a>Wobei die Plug-Ins für clusterfähiges aktualisieren ist\-in Spezifikation?  
  
-   [Cluster\-clusterfähige Aktualisierung Plug\-Referenz](https://msdn.microsoft.com/library/hh418084(VS.85).aspx)  
  
-   [Cluster-Aware Updating Plug &\-im Beispiel](https://code.msdn.microsoft.com/windowsdesktop/Cluster-Aware-Updating-6a8854c9)  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Cluster\-clusterfähige Aktualisierung – Übersicht](cluster-aware-updating.md)  
  
