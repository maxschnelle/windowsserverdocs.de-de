---
ms.assetid: 2f4b6641-0ec2-4b1c-85fb-a1f1d16685c8
title: "Hochglanz-Aware Updating erweiterte Optionen und updateausführungsprofile"
ms.topic: article
ms.prod: storage-failover-clustering
manager: dongill
ms.author: jgerend
author: JasonGerend
ms.date: 6/7/2017
description: "So konfigurieren Sie erweiterte Optionen und updateausführungsprofile für clusterfähiges aktualisieren (CAU)"
ms.openlocfilehash: 5b6f035791a946ff96ff6a95a1f753ef505d54b4
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="cluster-aware-updating-advanced-options-and-updating-run-profiles"></a>Cluster-Aware Updating erweiterte Optionen und updateausführungsprofile

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server2016, Windows Server2012 R2, Windows Server 2012

In diesem Thema werden die updateausführungsoptionen, die für konfiguriert werden, können ein [Cluster-Aware Updating](cluster-aware-updating.md) aktualisieren (CAU) ausführen. Diese erweiterten Optionen können konfiguriert werden, wenn Sie Updates installieren oder Konfigurieren von selbstaktualisierungsoptionen die CAU-UI oder CAU Windows PowerShell-Cmdlets verwenden.

Die meisten Konfigurationseinstellungen können gespeichert werden, wenn eine XML-Datei Aktualisierungsausführungsprofil aufgerufen werden und bei späteren Updateausführungen wiederverwendet. Die Standardwerte für die updateausführungsoptionen, die von CAU bereitgestellten können auch in zahlreichen Clusterumgebungen verwendet werden.

Informationen zu weiteren Optionen, die Sie für jede Updateausführung angeben können und Updateausführungsprofile, finden Sie unter den folgenden Abschnitten weiter unten in diesem Thema:

Optionen, die Sie angeben, wenn Sie ein Update ausführen verwenden Profile Optionen für die Updateausführung anfordern, die in einem Profil für die Updateausführung festgelegt werden können

Die folgende Tabelle enthält Optionen, die Sie in einer CAU Profil für die Updateausführung festlegen können. 

> [!NOTE] 
> Um die Option PreUpdateScript oder PostUpdateScript festzulegen, stellen Sie sicher, dass Windows PowerShell und .NET Framework 4.6 oder 4.5 installiert sind und dass auf jedem Knoten im Cluster PowerShell-Remoting aktiviert ist. Weitere Informationen finden Sie unter Konfigurieren der Knoten für die Remoteverwaltung in [Anforderungen und Best Practices for Cluster-Aware Updating ](cluster-aware-updating-requirements.md).


|Option|Standardwert|Detail|  
|------------|-------------------|-------------|  
|**StopAfter**|Unbegrenzte Zeit|Zeit in Minuten nach denen die Updateausführung beendet wird, wenn sie nicht abgeschlossen wurde. **Hinweis:** Wenn Sie eine vor dem Update oder ein PowerShell-Skript nach dem Update angeben, muss der gesamte Prozess der skriptausführung und der Ausführung der Updates innerhalb werden die **StopAfter** Zeitlimit.|  
|**WarnAfter**|Standardmäßig wird keine Warnung|Zeit in Minuten nach denen eine Warnung angezeigt wird, wenn die Updateausführung (einschließlich ein Skript vor oder nach der Update, falls konfiguriert) nicht abgeschlossen wurde.|  
|**MaxRetriesPerNode**|3|Maximale Anzahl der Fälle, in denen der Updateprozess (einschließlich ein Skript vor oder nach der Update, falls konfiguriert) pro Knoten wiederholt wird. Der Höchstwert beträgt 64.|  
|**MaxFailedNodes**|Für die meisten Cluster eine ganze Zahl, die CA. ein Drittel der Anzahl von Knoten im Cluster|Maximale Anzahl von Knoten, auf denen das Update fehlschlagen kann, entweder weil die Knoten ausfallen, oder der Clusterdienst beendet wird. Wenn Sie einen weiteren Knoten ein Fehler auftritt, wird die Updateausführung beendet.<br /><br /> Der gültige Wertebereich ist 0 bis 1 weniger als die Anzahl der Knoten im Cluster.|  
|**RequireAllNodesOnline**|Keine|Gibt an, dass alle Knoten online sein müssen und erreichbar vor dem Update beginnt.|  
|**RebootTimeoutMinutes**|15|Zeit in Minuten, die für clusterfähiges aktualisieren für den Neustart eines Knotens (falls ein Neustart erforderlich ist), und starten alle Autostart-Dienste ermöglichen. Wenn der Neustart nicht innerhalb dieses Zeitraums abgeschlossen wird, wird die Updateausführung für diesen Knoten als fehlerhaft gekennzeichnet.|  
|**PreUpdateScript**|Keine|Der Pfad und Dateiname für ein PowerShell-Skript auf jedem Knoten ausgeführt werden, bevor das Update gestartet und der Knoten in den Wartungsmodus versetzt wird. Die Erweiterung muss **. ps1**, und die Gesamtlänge der der Pfad und Dateiname darf maximal 260 Zeichen. Als bewährte Methode sollten das Skript gespeichert sein, auf einem Datenträger im Clusterspeicher oder auf einer hoch verfügbaren Netzwerkdateifreigabe, um sicherzustellen, dass sie immer für alle Clusterknoten zugänglich ist. Wenn das Skript auf einer Netzwerkdateifreigabe befindet, stellen Sie sicher, dass Sie die Dateifreigabe für die Berechtigung "Lesen" konfigurieren, für die jeder Gruppe, und schränken Sie Schreibzugriff auf, um zu verhindern, dass die Dateien durch nicht autorisierte Benutzer manipuliert.<br /><br /> Wenn Sie ein Skript vor dem Update angeben, stellen Sie sicher, dass Einstellungen wie die Zeitlimits (beispielsweise **StopAfter**) sind so konfiguriert, dass das Skript erfolgreich ausgeführt werden kann. Diese Grenzwerte umfassen den gesamten Prozess der skriptausführung und der Installation von Updates, nicht nur beim Installieren von Updates.|  
|**PostUpdateScript**|Keine|Der Pfad und Dateiname für ein PowerShell-Skript zum Ausführen von nach Abschluss des Updates (nachdem der Knoten den Wartungsmodus verlassen hat). Die Erweiterung muss **. ps1** und die Gesamtlänge der der Pfad und Dateiname darf maximal 260 Zeichen. Als bewährte Methode sollten das Skript gespeichert sein, auf einem Datenträger im Clusterspeicher oder auf einer hoch verfügbaren Netzwerkdateifreigabe, um sicherzustellen, dass sie immer für alle Clusterknoten zugänglich ist. Wenn das Skript auf einer Netzwerkdateifreigabe befindet, stellen Sie sicher, dass Sie die Dateifreigabe für die Berechtigung "Lesen" konfigurieren, für die jeder Gruppe, und schränken Sie Schreibzugriff auf, um zu verhindern, dass die Dateien durch nicht autorisierte Benutzer manipuliert.<br /><br /> Wenn Sie nach dem Update angeben, stellen Sie sicher, dass Einstellungen wie die Zeitlimits (beispielsweise **StopAfter**) sind so konfiguriert, dass das Skript erfolgreich ausgeführt werden kann. Diese Grenzwerte umfassen den gesamten Prozess der skriptausführung und der Installation von Updates, nicht nur beim Installieren von Updates.|  
|**ConfigurationName**|Diese Einstellung wirkt sich nur, wenn Sie Skripts ausführen.<br /><br /> Wenn Sie ein Skript vor oder nach dem Update angeben, aber Sie keine **ConfigurationName**, die Standard-Sitzung, die Konfiguration für PowerShell (Microsoft.PowerShell) verwendet wird.|Gibt die PowerShell-Sitzungskonfiguration, die definiert, die Sitzung in der Skripts (angegeben durch **PreUpdateScript** und **PostUpdateScript**) ausgeführt werden, und können die Befehle, die ausgeführt werden können.|  
|**CauPluginName**|**Microsoft.WindowsUpdatePlugin**|Plug-In, mit dem Sie konfigurieren Sie Cluster-Aware Updating verwenden, um eine Vorschau von Updates oder eine Updateausführung vorzunehmen. Weitere Informationen finden Sie unter [funktionieren wie Cluster-Aware Updating-Plug-Ins](cluster-aware-updating-plug-ins.md).|  
|**CauPluginArguments**|Keine|Eine Reihe von *Name = Wert* -Paare (Argumenten) für die Aktualisierung-Plug-In verwenden, z.B.:<br /><br /> **Domain=Domain.Local**<br /><br /> Diese *Name = Wert* Paare müssen an das Plug-In verwertbar sein, die Sie angeben, **CauPluginName**.<br /><br /> Geben Sie zum Angeben eines Arguments mithilfe der CAU-UI der *Namen*, drücken Sie die Tab-Taste, und geben Sie dann das entsprechende *Wert*. Drücken Sie die Tab-Taste erneut, um das nächste Argument anzugeben. Jede *Namen* und *Wert* werden automatisch mit einem Gleichheitszeichen (=) getrennt. Mehrere Paare werden automatisch durch Semikolons getrennt.<br /><br /> Für das standardmäßige **Microsoft.WindowsUpdatePlugin** -Plug-In, sind keine Argumente erforderlich. Sie können jedoch angeben, dass ein optionales Argument, z.B. zum Festlegen einer standardmäßigen Windows Update-Agent-Abfragezeichenfolge zum Filtern der Updates, die vom Plug-In angewendet werden. Für eine *Namen*, verwenden Sie **QueryString**, und für eine *Wert*, müssen Sie die vollständige Abfrage in Anführungszeichen einschließen.<br /><br /> Weitere Informationen finden Sie unter [funktionieren wie Cluster-Aware Updating-Plug-Ins](cluster-aware-updating-plug-ins.md).|  
  
##  <a name="BKMK_runtime"></a>Optionen, die Sie angeben, wenn Sie Anfordern einer Updateausführung  
 Die folgende Tabelle enthält Optionen (mit Ausnahme der in einem Profil für die Updateausführung), die Sie beim Anfordern einer Updateausführung angeben können. Informationen zu den Optionen, die Sie in einem Profil für die Updateausführung festlegen können, finden Sie in der obigen Tabelle.  
  
|Option|Standardwert|Detail|  
|------------|-------------------|-------------|  
|**ClusterName**|Keine <br>**Hinweis:** diese Option muss festgelegt werden, nur, wenn die CAU-UI nicht, auf einem Knoten des Failoverclusters ausgeführt wird oder ein Failoverclusters, die sich von dem die CAU-UI ausgeführt wird verwiesen werden soll.|NetBIOS-Namen des Clusters, auf dem die Updateausführung erfolgen soll.|  
|**Anmeldeinformationen**|Aktuelle Kontoanmeldeinformationen|Administrative Anmeldeinformationen für das Ziel des Clusters auf dem die Updateausführung erfolgen soll. Möglicherweise bereits die erforderlichen Anmeldeinformationen müssen, wenn Sie die CAU-UI (oder eine PowerShell-Sitzung öffnen bei Verwendung der CAU-PowerShell-Cmdlets) von einem Konto, die über Administratorrechte und -Berechtigungen für den Cluster verfügt.|  
|**NodeOrder**|Standardmäßig wird bei CAU mit den Knoten, der die kleinste Anzahl von Clusterrollen besitzt, dann folgen die Knoten, der Zweitkleinste Anzahl, und So weiter.|Die Namen der Clusterknoten in der Reihenfolge, in diese (sofern möglich) aktualisiert werden sollen.|  
  
##  <a name="BKMK_profile"></a>Verwenden von Profilen für die Updateausführung  
 Jede Updateausführung kann einem bestimmten Profil für die Updateausführung zugeordnet sein. Der Standard-Aktualisierungsausführungsprofil sich in befindet der *%windir%\Cluster* Ordner. Wenn Sie die CAU-UI im Remoteaktualisierungsmodus verwenden, können Profil angegeben, die Zeit, die Sie Updates installieren, oder Sie können das Standardprofil Updateausführung. Wenn Sie CAU im selbstaktualisierungsmodus verwenden, können Sie die Einstellungen von einem festgelegten Updateausführungsprofil importieren, wenn Sie die selbstaktualisierungsoptionen konfigurieren. In beiden Fällen können Sie gemäß Ihren Anforderungen die angezeigten Werte für die updateausführungsoptionen überschreiben. Wenn Sie möchten, können Sie die updateausführungsoptionen als Profil mit dem gleichen Dateinamen oder einen anderen Namen speichern. Updates übernehmen oder selbstaktualisierungsoptionen konfigurieren, CAU automatisch das nächste Mal wählt das Profil für die Updateausführung, die zuvor ausgewählt wurde.  
  
 Sie können ein vorhandenes Profil für die Updateausführung zu ändern oder ein neues erstellen, durch die Auswahl **erstellen oder Ändern von Profil für die Updateausführung** in die CAU-UI.

Hier sind einige wichtige Hinweise zur Verwendung von Updateausführungsprofile:

* Ein Profil für die Updateausführung speichern keine clusterspezifischen Informationen wie z.B. administrative Anmeldeinformationen. Wenn Sie CAU im selbstaktualisierungsmodus verwenden, speichern nicht das Profil für die Updateausführung auch die selbstaktualisierung Zeitplaninformationen. Dadurch möglich, ein Profil für die Updateausführung in allen Failoverclustern in einer angegebenen Klasse zu teilen.
* Wenn Sie selbstaktualisierungsoptionen mit einem Profil für die Updateausführung konfigurieren und das Profil mit verschiedenen Werten für die updateausführungsoptionen später ändern, ändert die Konfiguration die selbstaktualisierung nicht automatisch. Um die neuen Einstellungen für die Updateausführung anzuwenden, müssen Sie die selbstaktualisierungsoptionen erneut konfigurieren.
* Profil ausführen-Editor unterstützt leider keine Dateipfade mit Leerzeichen, z.B. *"C:\Program Files"*. Speichern Sie dieses Problem zu umgehen, die vor und Buchen von Update-Skripts in einem Pfad, die keine Leerzeichen enthalten oder mithilfe von PowerShell ausschließlich Ausführungsprofile, platzieren den Pfad in Anführungszeichen, bei der Ausführung verwalten **Invoke-CauRun**.

### <a name="windows-powershell-equivalent-commands"></a>Gleichwertige Windows PowerShell-Befehle
  
 Sie können die Einstellungen von Profil importieren, beim Ausführen der **Invoke-CauRun**, **Add-CauClusterRole**, oder **Set-CauClusterRole** Cmdlet.  
  
 Im folgenden Beispiel wird ein Scan und eine vollständige Updateausführung auf dem Cluster *CONTOSO-FC1*, mithilfe der Optionen der Updateausführung, die in angegebenen *C:\Windows\Cluster\DefaultParameters.xml*. Für die übrigen cmdletparameter werden Standardwerte verwendet.  
  
```powershell  
$MyRunProfile = Import-Clixml C:\Windows\Cluster\DefaultParameters.xml  
Invoke-CauRun –ClusterName CONTOSO-FC1 @MyRunProfile   
```  
  
 Verwenden Sie ein Profil für die Updateausführung, können Sie einen Failovercluster wiederholbare mit einheitlichen Einstellungen für die Verwaltung von Ausnahmen, zeitbindungen und weitere Betriebsparameter aktualisieren. Da diese Einstellungen in der Regel spezifisch für eine Klasse von Failoverclustern sind – z.B. "Alle Microsoft SQL Server-Cluster" oder "Meine unternehmenswichtigen Cluster%" – möglicherweise möchten Sie jedes Profil für die Updateausführung entsprechend der Klasse von Failoverclustern benennen mit verwendet wird. Darüber hinaus sollten Sie das Profil für die Updateausführung in einer Dateifreigabe verwalten, die für alle Failovercluster einer bestimmten Klasse in Ihrer IT-Organisation zugänglich ist.  
  
  
  
## <a name="see-also"></a>Siehe auch

-   [Cluster-Aware Updating](cluster-aware-updating.md)
  
-   [Cmdlets für clusterfähiges aktualisieren in WindowsPowerShell](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating)