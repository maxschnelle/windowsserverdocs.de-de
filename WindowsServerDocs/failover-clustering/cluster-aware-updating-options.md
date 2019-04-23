---
ms.assetid: 2f4b6641-0ec2-4b1c-85fb-a1f1d16685c8
title: Erweiterte Optionen und updateausführungsprofile des clusterfähigen Aktualisierens
ms.topic: article
ms.prod: windows-server-threshold
manager: dongill
ms.author: jgerend
author: JasonGerend
ms.date: 08/06/2018
description: 'Vorgehensweise: Konfigurieren von erweiterten Optionen und updateausführungsprofile für clusterfähiges aktualisieren (CAU)'
ms.openlocfilehash: 5fac31ad35422e623b98caaabdd9eae183e2e5d8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830551"
---
# <a name="cluster-aware-updating-advanced-options-and-updating-run-profiles"></a>Erweiterte Optionen und updateausführungsprofile des clusterfähigen Aktualisierens

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

In diesem Thema wird beschrieben, Optionen der Updateausführung, die für die konfiguriert werden, können eine [Cluster-Aware Updating](cluster-aware-updating.md) (aktualisieren CAU) Updateausführung. Diese erweiterten Optionen können konfiguriert werden, wenn Sie Updates anwenden und selbstaktualisierungsoptionen konfigurieren die CAU-UI oder der CAU-Windows-PowerShell-Cmdlets verwenden.

Die meisten Konfigurationseinstellungen können als XML-Datei gespeichert werden; diese Datei wird als %%amp;quot;Profil für die Updateausführung%%amp;quot; bezeichnet und für weitere Updateausführungen wiederverwendet. Die von CAU bereitgestellten Standardwerte für die Updateausführungsoptionen können auch in zahlreichen Clusterumgebungen verwendet werden.

Informationen zu weiteren Optionen, die Sie für jede Updateausführung angeben können, sowie zu Profilen für die Updateausführung finden Sie in den folgenden Abschnitten in diesem Thema:

Optionen, die Sie angeben, wenn Sie eine Aktualisierung ausführen verwenden Profile Optionen für die Updateausführung anfordern, die in einem Profil für die Updateausführung festgelegt werden können

Die folgende Tabelle enthält Optionen, die Sie in einem Profil für die CAU-Updateausführung festlegen können. 

> [!NOTE] 
> Um die Option PreUpdateScript oder PostUpdateScript festzulegen, stellen Sie sicher, dass Windows PowerShell und .NET Framework 4.6 oder 4.5 installiert sind und dass PowerShell-Remoting auf jedem Knoten im Cluster aktiviert ist. Weitere Informationen finden Sie unter Konfigurieren Sie die Knoten für die Remoteverwaltung in [Anforderungen und Best Practices for Cluster-Aware Updating](cluster-aware-updating-requirements.md).


|Option|Standardwert|Details|  
|------------|-------------------|-------------|  
|**StopAfter**|Unbegrenzter Zeitraum|Die Zeit in Minuten, nach der die Updateausführung beendet wird, falls sie nicht abgeschlossen wurde. **Hinweis**:  Wenn Sie vor oder ein PowerShell-Skript nach dem Update angeben, muss der gesamte Prozess der skriptausführung und der Ausführung der Updates innerhalb werden die **StopAfter** zeitliche Begrenzung.|  
|**WarnAfter**|Standardmäßig; keine Warnung|Die Zeit in Minuten, nach der eine Warnung angezeigt wird, falls die Updateausführung (einschließlich eines ggf. konfigurierten Skripts vor oder nach dem Update) noch nicht abgeschlossen wurde.|  
|**MaxRetriesPerNode**|3|Die maximale Anzahl von Wiederholungen des Updateprozesses (einschließlich eines ggf. konfigurierten Skripts vor oder nach dem Update). Die maximale Anzahl ist 64.|  
|**MaxFailedNodes**|Für die meisten Cluster eine ganze Zahl, die ca. ein Drittel der Anzahl der Clusterknoten beträgt|Maximale Anzahl von Knoten, an denen das Update fehlschlagen kann, entweder aufgrund von Knotenausfällen oder weil der Clusterdienst beendet wird. Tritt für einen weiteren Knoten ein Fehler auf, wird die Updateausführung beendet.<br /><br /> Der gültige Wertebereich ist 0 bis 1 weniger als die Anzahl von der Clusterknoten.|  
|**RequireAllNodesOnline**|Keine|Gibt an, dass alle Knoten online und erreichbar sein müssen, bevor das Update gestartet wird.|  
|**RebootTimeoutMinutes**|15|Die Zeit in Minuten, die bei CAU für den Neustart eines Knotens (sofern ein Neustart erforderlich ist) und das Starten aller Autostartdienst zulässig ist. Der Neustartvorgang innerhalb dieses Zeitraums abgeschlossen wird, wird die Updateausführung für diesen Knoten als fehlerhaft gekennzeichnet.|  
|**PreUpdateScript**|Keine|Der Pfad und Dateiname für ein PowerShell-Skript auf jedem Knoten ausgeführt werden soll, bevor das Update gestartet und der Knoten in den Wartungsmodus versetzt wird. Die Dateierweiterung muss **ps1**, und die Gesamtlänge von den Pfad und Dateiname darf maximal 260 Zeichen lang sein. Es wird empfohlen, das Skript auf einem Datenträger im Clusterspeicher oder in einer hoch verfügbaren Dateifreigabe zu speichern, um sicherzustellen, dass alle Clusterknoten stets darauf zugreifen können. Wenn sich das Skript in einer Netzwerkdateifreigabe befindet, achten Sie darauf, die Dateifreigabe so zu konfigurieren, dass die Gruppe %%amp;quot;Jeder%%amp;quot; über die Leseberechtigung verfügt, und schränken Sie den Schreibzugriff ein, um eine Manipulationen an den Dateien durch nicht autorisierte Benutzer zu verhindern.<br /><br /> Vergewissern Sie sich bei Angabe eines Skripts vor dem Update, dass Einstellungen wie die Zeitlimits (beispielsweise **StopAfter**) so konfiguriert sind, dass das Skript erfolgreich ausgeführt werden kann. Diese Limits gelten für den gesamten Prozess (also sowohl für das Ausführen von Skripts als auch für das Installieren von Updates), nicht nur für das Installieren von Updates.|  
|**PostUpdateScript**|Keine|Der Pfad und Dateiname für ein Powershellskript, führen Sie nach Abschluss des Updates (nach der Knoten den Wartungsmodus verlassen hat). Die Dateierweiterung muss **ps1** und die Gesamtlänge von den Pfad und Dateiname darf maximal 260 Zeichen lang sein. Es wird empfohlen, das Skript auf einem Datenträger im Clusterspeicher oder in einer hoch verfügbaren Dateifreigabe zu speichern, um sicherzustellen, dass alle Clusterknoten stets darauf zugreifen können. Wenn sich das Skript in einer Netzwerkdateifreigabe befindet, achten Sie darauf, die Dateifreigabe so zu konfigurieren, dass die Gruppe %%amp;quot;Jeder%%amp;quot; über die Leseberechtigung verfügt, und schränken Sie den Schreibzugriff ein, um eine Manipulationen an den Dateien durch nicht autorisierte Benutzer zu verhindern.<br /><br /> Vergewissern Sie sich bei Angabe eines Skripts nach dem Update, dass Einstellungen wie die Zeitlimits (beispielsweise **StopAfter**) so konfiguriert sind, dass das Skript erfolgreich ausgeführt werden kann. Diese Limits gelten für den gesamten Prozess (also sowohl für das Ausführen von Skripts als auch für das Installieren von Updates), nicht nur für das Installieren von Updates.|  
|**ConfigurationName**|Diese Einstellung betrifft nur die Ausführung von Skripts.<br /><br /> Wenn Sie ein Skript vor oder nach dem Update angeben, aber Sie nicht angeben einer **ConfigurationName**, die Standard-Sitzung, die Konfiguration für PowerShell (Microsoft.PowerShell) verwendet wird.|Gibt an, die PowerShell-Sitzungskonfiguration, die die Sitzung, in der Skripts definiert (angegeben durch **PreUpdateScript** und **PostUpdateScript**) ausgeführt werden, und können die Befehle, die ausgeführt werden können.|  
|**CauPluginName**|**Microsoft.WindowsUpdatePlugin**|Plug-In, mit dem Sie das clusterfähige Aktualisieren konfigurieren, um eine Updatevorschau anzuzeigen oder eine Updateausführung vorzunehmen. Weitere Informationen finden Sie unter [wie Cluster-Aware Updating-Plug-ins funktioniert](cluster-aware-updating-plug-ins.md).|  
|**CauPluginArguments**|Keine|Ein Satz mit Paaren vom Typ *Name=Wert* (Argumenten) für das zu verwendende Update-Plug-In. Beispiel:<br /><br /> **Domain=Domain.local**<br /><br /> Diese Paare vom Typ *Name=Wert* müssen für das in **CauPluginName** angegebene Plug-In verwertbar sein.<br /><br /> Zum Angeben eines Arguments mithilfe der Benutzeroberfläche für CAU geben Sie den *Namen*, ein, drücken die TAB-TASTE und geben dann den entsprechenden *Wert* ein. Drücken Sie erneut die TAB-TASTE, um das nächste Argument anzugeben. Jedes Paar aus *Name* und *Wert* wird automatisch durch ein Gleichheitszeichen getrennt. Mehrere Paare werden jeweils automatisch durch ein Semikolon getrennt.<br /><br /> Für den standardmäßigen **Microsoft.WindowsUpdatePlugin** -Plug-in, keine Argumente erforderlich sind. Sie können jedoch ein optionales Argument angeben, z. B. zum Festlegen einer standardmäßigen Windows Update-Agent-Abfragezeichenfolge zum Filtern der Updates, die durch das Plug-In übernommen werden. Für eine *Namen*, verwenden Sie **QueryString**, und für eine *Wert*, müssen Sie die vollständige Abfrage in Anführungszeichen einschließen.<br /><br /> Weitere Informationen finden Sie unter [wie Cluster-Aware Updating-Plug-ins funktioniert](cluster-aware-updating-plug-ins.md).|  
  
##  <a name="BKMK_runtime"></a> Optionen, die Sie angeben, wenn Sie Anfordern einer Updateausführung  
 Die folgende Tabelle enthält Optionen, die Sie beim Anfordern einer Updateausführung angeben können und bei denen es sich nicht um Optionen eines Profils für die Updateausführung handelt Informationen zu den Optionen, die Sie in einem Profil für die Updateausführung festlegen können, finden Sie in der vorherigen Tabelle.  
  
|Option|Standardwert|Details|  
|------------|-------------------|-------------|  
|**ClusterName**|Keine <br>**Hinweis**:  Diese Option muss nur festgelegt werden, wenn die CAU-Benutzeroberfläche für nicht an einem Failoverclusterknoten ausgeführt wird, oder wenn Sie auf einen anderen Failovercluster verweisen möchten, als jenen, auf dem die CAU-Benutzeroberfläche ausgeführt wird.|Der NetBIOS-Name des Clusters, auf dem die Updateausführung erfolgen soll.|  
|**Anmeldeinformationen**|Aktuelle Kontoanmeldeinformationen|Die Administratoranmeldeinformationen für den Zielcluster, in dem die Updateausführung erfolgen soll. Bereits die erforderlichen Anmeldeinformationen möglicherweise, wenn Sie die CAU-UI starten (oder eine PowerShell-Sitzung, öffnen Wenn Sie die CAU-PowerShell-Cmdlets verwenden) aus einem Konto, die auf dem Cluster über Administratorrechte und-Berechtigungen verfügt.|  
|**NodeOrder**|Standardmäßig wird bei CAU mit dem Knoten begonnen, der die kleinste Anzahl von Clusterrollen besitzt. Danach folgen die Knoten mit der jeweils nächsthöheren Anzahl.|Die Namen der Clusterknoten in der Reihenfolge, in der sie aktualisiert werden sollten (sofern möglich).|  
  
##  <a name="BKMK_profile"></a> Verwenden von Profilen für die Updateausführung  
 Jede Updateausführung kann einem bestimmten Profil für die Updateausführung zugeordnet werden. Der Standard-Aktualisierungsausführungsprofil sich in befindet der *%windir%\cluster* Ordner. Wenn Sie die CAU-UI im remoteaktualisierungsmodus verwenden, können ein Profil für die Updateausführung zum Zeitpunkt angeben, dass Sie Updates anwenden oder das Standardprofil Updateausführung können. Wenn Sie CAU im selbstaktualisierungsmodus verwenden, können Sie die Einstellungen aus einem festgelegten Updateausführungsprofil importieren, wenn Sie die selbstaktualisierungsoptionen konfigurieren. In beiden Fällen können Sie bei Bedarf die angezeigten Werte für die Updateausführungsoptionen überschreiben. Die Updateausführungsoptionen können unter demselben oder einem anderen Dateinamen als Profil für die Updateausführung gespeichert werden. Wenn Sie das nächste Mal Updates übernehmen oder Selbstaktualisierungsoptionen konfigurieren, wählt CAU automatisch das zuvor ausgewählte Profil für die Updateausführung aus.  
  
 Sie können ein vorhandenes Profil für die Updateausführung zu ändern oder erstellen Sie einen neuen durch Auswahl **erstellen oder Ändern von Profil für die Updateausführung** in die CAU-UI.

Hier sind einige wichtige Hinweise zur Verwendung von Ausführungsprofile aktualisieren:

* Ein Profil für die Updateausführung speichern keine clusterspezifischen Informationen wie z. B. administrative Anmeldeinformationen. Wenn Sie CAU im selbstaktualisierungsmodus verwenden, speichert das Profil für die Updateausführung nicht auch die selbstaktualisierung Zeitplaninformationen. Dies ermöglicht die Freigabe eines Profils für die Updateausführung in allen Failoverclustern in einer bestimmten Klasse.
* Wenn Sie selbstaktualisierungsoptionen mithilfe von einem Profil für die Updateausführung konfigurieren und später, das Profil mit unterschiedlichen Werten für die updateausführungsoptionen ändern, nicht die Konfiguration die selbstaktualisierung automatisch geändert. Sie müssen die Selbstaktualisierungsoptionen erneut konfigurieren, damit die neuen Einstellungen für die Updateausführung übernommen werden.
* Der ausführen-Editor unterstützt leider keine Dateipfade, die Leerzeichen, z. B. enthalten *C:\Program Files*. Dieses Problem zu umgehen, speichern Sie Ihre vor und veröffentlichen Sie die Aktualisierung von Skripts in einen Pfad, der keine Leerzeichen enthalten, oder mithilfe von PowerShell ausschließlich zur Verwaltung von Ausführungsprofile, platzieren den Pfad in Anführungszeichen, bei der Ausführung **Invoke-CauRun**.

### <a name="windows-powershell-equivalent-commands"></a>Gleichwertige Windows PowerShell-Befehle
  
 Sie können die Einstellungen aus einem Profil für die Updateausführung importieren, beim Ausführen der **Invoke-CauRun**, **Add-CauClusterRole**, oder **Set-CauClusterRole** Cmdlet.  
  
 Im folgenden Beispiel wird ein Scan und eine vollständige Updateausführung auf dem Cluster *CONTOSO-FC1* durchgeführt. Dazu werden die in *C:\Windows\Cluster\DefaultParameters.xml* festgelegten Updateausführungsoptionen verwendet. Für die übrigen Cmdlet-Parameter werden Standardwerte verwendet.  
  
```powershell  
$MyRunProfile = Import-Clixml C:\Windows\Cluster\DefaultParameters.xml  
Invoke-CauRun –ClusterName CONTOSO-FC1 @MyRunProfile   
```  
  
 Durch die Verwendung eines Profils für die Updateausführung können Sie ein Failovercluster wiederholt mit einheitlichen Einstellungen für die Ausnahmenverwaltung, Zeitbindungen und weitere Betriebsparameter aktualisieren. Da diese Einstellungen in der Regel spezifisch für eine Klasse von Failoverclustern – z. B. %%amp;quot;Alle Microsoft SQL Server-Cluster%%amp;quot; oder %%amp;quot;Meine unternehmenswichtigen Cluster%%amp;quot; – sind, sollten Sie jedes Profil für die Updateausführung entsprechend der Klasse von Failoverclustern benennen, mit der es verwendet wird. Außerdem sollten Sie das Profil für die Updateausführung in einer Dateifreigabe verwalten, die für alle Failovercluster einer bestimmten Klasse in Ihrer IT-Organisation zugänglich ist.  
  
  
  
## <a name="see-also"></a>Siehe auch

-   [Clusterfähiges aktualisieren](cluster-aware-updating.md)
  
-   [Cmdlets für clusterfähiges aktualisieren in Windows PowerShell](https://docs.microsoft.com/powershell/module/clusterawareupdating/?view=win10-ps)