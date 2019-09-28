---
ms.assetid: 2f4b6641-0ec2-4b1c-85fb-a1f1d16685c8
title: Cluster fähiges aktualisieren erweiterter Optionen und Update Lauf profile
ms.topic: article
ms.prod: windows-server
manager: dongill
ms.author: jgerend
author: JasonGerend
ms.date: 08/06/2018
description: Konfigurieren erweiterter Optionen und Aktualisieren von Lauf Profilen für Cluster fähiges aktualisieren (Cau)
ms.openlocfilehash: 500eb4d9affe38fe5f22f3720893b7960190948e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361308"
---
# <a name="cluster-aware-updating-advanced-options-and-updating-run-profiles"></a>Cluster fähiges aktualisieren erweiterter Optionen und Update Lauf profile

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012.

In diesem Thema werden die Aktualisierungs Lauf Optionen beschrieben, die für das Update der [Cluster fähigen Aktualisierung (Cluster-Aware Update](cluster-aware-updating.md) , Cau) konfiguriert werden können. Diese erweiterten Optionen können konfiguriert werden, wenn Sie entweder die Benutzeroberfläche für Cluster fähiges aktualisieren oder die Windows PowerShell-Cmdlets für Cau verwenden, um Updates anzuwenden oder selbst Aktualisierungs Optionen zu konfigurieren.

Die meisten Konfigurationseinstellungen können als XML-Datei gespeichert werden; diese Datei wird als %%amp;quot;Profil für die Updateausführung%%amp;quot; bezeichnet und für weitere Updateausführungen wiederverwendet. Die von CAU bereitgestellten Standardwerte für die Updateausführungsoptionen können auch in zahlreichen Clusterumgebungen verwendet werden.

Informationen zu weiteren Optionen, die Sie für jede Updateausführung angeben können, sowie zu Profilen für die Updateausführung finden Sie in den folgenden Abschnitten in diesem Thema:

Optionen, die Sie beim Anfordern einer Update Laufzeit angeben, verwenden Optionen für die Update Lauf Profile, die in einem Profil für die Update Laufzeit festgelegt werden können.

Die folgende Tabelle enthält Optionen, die Sie in einem Profil für die CAU-Updateausführung festlegen können. 

> [!NOTE] 
> Stellen Sie zum Festlegen der Option preupdatescript oder postupdatescript sicher, dass Windows PowerShell und .NET Framework 4,6 oder 4,5 installiert sind und dass PowerShell-Remoting auf jedem Knoten im Cluster aktiviert ist. Weitere Informationen finden Sie unter Konfigurieren der Knoten für die Remote Verwaltung in [Anforderungen und bewährte Methoden für das Cluster fähige aktualisieren](cluster-aware-updating-requirements.md).


|Option|Standardwert|Details|  
|------------|-------------------|-------------|  
|**StopAfter**|Unbegrenzter Zeitraum|Die Zeit in Minuten, nach der die Updateausführung beendet wird, falls sie nicht abgeschlossen wurde. **Hinweis**:  Wenn Sie ein PowerShell-Skript vor oder nach dem Update angeben, muss der gesamte Prozess zum Ausführen von Skripts und zum Ausführen von Updates innerhalb des **stopafter** -Zeitlimits vollständig ausgeführt werden.|  
|**"Warnafter"**|Standardmäßig; keine Warnung|Die Zeit in Minuten, nach der eine Warnung angezeigt wird, falls die Updateausführung (einschließlich eines ggf. konfigurierten Skripts vor oder nach dem Update) noch nicht abgeschlossen wurde.|  
|**Maxretriespernode**|3|Die maximale Anzahl von Wiederholungen des Updateprozesses (einschließlich eines ggf. konfigurierten Skripts vor oder nach dem Update). Die maximale Anzahl ist 64.|  
|**Maxfailednodes**|Für die meisten Cluster eine ganze Zahl, die ca. ein Drittel der Anzahl der Clusterknoten beträgt|Maximale Anzahl von Knoten, an denen das Update fehlschlagen kann, entweder aufgrund von Knotenausfällen oder weil der Clusterdienst beendet wird. Tritt für einen weiteren Knoten ein Fehler auf, wird die Updateausführung beendet.<br /><br /> Der gültige Wertebereich ist 0 bis 1 weniger als die Anzahl von der Clusterknoten.|  
|**Requirements allnode sonline**|Keine|Gibt an, dass alle Knoten online und erreichbar sein müssen, bevor das Update gestartet wird.|  
|**Reboottimeoutminutes**|15|Die Zeit in Minuten, die bei CAU für den Neustart eines Knotens (sofern ein Neustart erforderlich ist) und das Starten aller Autostartdienst zulässig ist. Wenn der Neustart Vorgang nicht innerhalb dieses Zeitraums ausgeführt wird, wird die Update Ausführung für diesen Knoten als fehlgeschlagen markiert.|  
|**PreUpdateScript**|Keine|Der Pfad und der Dateiname für ein PowerShell-Skript, das auf jedem Knoten ausgeführt werden soll, bevor das Update gestartet und der Knoten in den Wartungsmodus versetzt wird. Die Dateinamenerweiterung muss **ps1**lauten, und die Gesamtlänge von Pfad und Dateiname darf nicht länger als 260 Zeichen sein. Es wird empfohlen, das Skript auf einem Datenträger im Clusterspeicher oder in einer hoch verfügbaren Dateifreigabe zu speichern, um sicherzustellen, dass alle Clusterknoten stets darauf zugreifen können. Wenn sich das Skript in einer Netzwerkdateifreigabe befindet, achten Sie darauf, die Dateifreigabe so zu konfigurieren, dass die Gruppe %%amp;quot;Jeder%%amp;quot; über die Leseberechtigung verfügt, und schränken Sie den Schreibzugriff ein, um eine Manipulationen an den Dateien durch nicht autorisierte Benutzer zu verhindern.<br /><br /> Vergewissern Sie sich bei Angabe eines Skripts vor dem Update, dass Einstellungen wie die Zeitlimits (beispielsweise **StopAfter**) so konfiguriert sind, dass das Skript erfolgreich ausgeführt werden kann. Diese Limits gelten für den gesamten Prozess (also sowohl für das Ausführen von Skripts als auch für das Installieren von Updates), nicht nur für das Installieren von Updates.|  
|**PostUpdateScript**|Keine|Der Pfad und der Dateiname für ein PowerShell-Skript, das nach Abschluss des Updates ausgeführt werden soll (nachdem der Knoten den Wartungsmodus verlassen hat). Die Dateinamenerweiterung muss **ps1** lauten, und die Gesamtlänge von Pfad und Dateiname darf nicht länger als 260 Zeichen sein. Es wird empfohlen, das Skript auf einem Datenträger im Clusterspeicher oder in einer hoch verfügbaren Dateifreigabe zu speichern, um sicherzustellen, dass alle Clusterknoten stets darauf zugreifen können. Wenn sich das Skript in einer Netzwerkdateifreigabe befindet, achten Sie darauf, die Dateifreigabe so zu konfigurieren, dass die Gruppe %%amp;quot;Jeder%%amp;quot; über die Leseberechtigung verfügt, und schränken Sie den Schreibzugriff ein, um eine Manipulationen an den Dateien durch nicht autorisierte Benutzer zu verhindern.<br /><br /> Vergewissern Sie sich bei Angabe eines Skripts nach dem Update, dass Einstellungen wie die Zeitlimits (beispielsweise **StopAfter**) so konfiguriert sind, dass das Skript erfolgreich ausgeführt werden kann. Diese Limits gelten für den gesamten Prozess (also sowohl für das Ausführen von Skripts als auch für das Installieren von Updates), nicht nur für das Installieren von Updates.|  
|**ConfigurationName**|Diese Einstellung betrifft nur die Ausführung von Skripts.<br /><br /> Wenn Sie ein Skript vor dem Update oder ein Skript nach dem Update angeben, aber keinen **ConfigurationName**angeben, wird die standardmäßige Sitzungs Konfiguration für PowerShell (Microsoft. PowerShell) verwendet.|Gibt die PowerShell-Sitzungs Konfiguration an, die die Sitzung definiert, in der Skripts (angegeben durch **preupdatescript** und **postupdatescript**) ausgeführt werden, und die Befehle einschränken können, die ausgeführt werden können.|  
|**CauPluginName**|**Microsoft. windowsupdateplugin**|Plug-In, mit dem Sie das clusterfähige Aktualisieren konfigurieren, um eine Updatevorschau anzuzeigen oder eine Updateausführung vorzunehmen. Weitere Informationen finden Sie unter [Funktionsweise von Plug-Ins für Cluster fähiges aktualisieren](cluster-aware-updating-plug-ins.md).|  
|**Caupluginarguments**|Keine|Ein Satz mit Paaren vom Typ *Name=Wert* (Argumenten) für das zu verwendende Update-Plug-In. Beispiel:<br /><br /> **Domäne = Domäne. local**<br /><br /> Diese Paare vom Typ *Name=Wert* müssen für das in **CauPluginName** angegebene Plug-In verwertbar sein.<br /><br /> Zum Angeben eines Arguments mithilfe der Benutzeroberfläche für CAU geben Sie den *Namen*, ein, drücken die TAB-TASTE und geben dann den entsprechenden *Wert* ein. Drücken Sie erneut die TAB-TASTE, um das nächste Argument anzugeben. Jedes Paar aus *Name* und *Wert* wird automatisch durch ein Gleichheitszeichen getrennt. Mehrere Paare werden jeweils automatisch durch ein Semikolon getrennt.<br /><br /> Für das standardmäßige **Microsoft. windowsupdateplugin** -Plug-in sind keine Argumente erforderlich. Sie können jedoch ein optionales Argument angeben, z. B. zum Festlegen einer standardmäßigen Windows Update-Agent-Abfragezeichenfolge zum Filtern der Updates, die durch das Plug-In übernommen werden. Verwenden Siefür einen Namen **QueryString**, und schließen Sie für einen *Wert*die gesamte Abfrage in Anführungszeichen ein.<br /><br /> Weitere Informationen finden Sie unter [Funktionsweise von Plug-Ins für Cluster fähiges aktualisieren](cluster-aware-updating-plug-ins.md).|  
  
##  <a name="BKMK_runtime"></a>Optionen, die Sie beim Anfordern einer Update Laufzeit angeben  
 Die folgende Tabelle enthält Optionen, die Sie beim Anfordern einer Updateausführung angeben können und bei denen es sich nicht um Optionen eines Profils für die Updateausführung handelt Informationen zu den Optionen, die Sie in einem Profil für die Updateausführung festlegen können, finden Sie in der vorherigen Tabelle.  
  
|Option|Standardwert|Details|  
|------------|-------------------|-------------|  
|**ClusterName**|Keine <br>**Hinweis**:  Diese Option muss nur festgelegt werden, wenn die CAU-Benutzeroberfläche für nicht an einem Failoverclusterknoten ausgeführt wird, oder wenn Sie auf einen anderen Failovercluster verweisen möchten, als jenen, auf dem die CAU-Benutzeroberfläche ausgeführt wird.|Der NetBIOS-Name des Clusters, auf dem die Updateausführung erfolgen soll.|  
|**Anmelde Informationen**|Aktuelle Kontoanmeldeinformationen|Die Administratoranmeldeinformationen für den Zielcluster, in dem die Updateausführung erfolgen soll. Möglicherweise verfügen Sie bereits über die erforderlichen Anmelde Informationen, wenn Sie die Cau-Benutzeroberfläche starten (oder eine PowerShell-Sitzung öffnen, wenn Sie die PowerShell-Cmdlets für Cau verwenden), von einem Konto, das über Administratorrechte und-Berechtigungen für den Cluster verfügt.|  
|**Node Order**|Standardmäßig wird bei CAU mit dem Knoten begonnen, der die kleinste Anzahl von Clusterrollen besitzt. Danach folgen die Knoten mit der jeweils nächsthöheren Anzahl.|Die Namen der Clusterknoten in der Reihenfolge, in der sie aktualisiert werden sollten (sofern möglich).|  
  
##  <a name="BKMK_profile"></a>Verwenden von Update Lauf Profilen  
 Jede Updateausführung kann einem bestimmten Profil für die Updateausführung zugeordnet werden. Das Standardprofil für die Profilerstellung wird im Ordner " *%windir%\Cluster* " gespeichert. Wenn Sie die Benutzeroberfläche für Cluster fähiges aktualisieren im Remote Aktualisierungs Modus verwenden, können Sie zum Zeitpunkt der Anwendung von Updates ein Profil für die Profilerstellung angeben, oder Sie können das Standardprofil für die Profilerstellung verwenden. Wenn Sie Cau im selbst Aktualisierungs Modus verwenden, können Sie die Einstellungen aus einem angegebenen Update Lauf Profil importieren, wenn Sie die selbst Aktualisierungs Optionen konfigurieren. In beiden Fällen können Sie bei Bedarf die angezeigten Werte für die Updateausführungsoptionen überschreiben. Die Updateausführungsoptionen können unter demselben oder einem anderen Dateinamen als Profil für die Updateausführung gespeichert werden. Wenn Sie das nächste Mal Updates übernehmen oder Selbstaktualisierungsoptionen konfigurieren, wählt CAU automatisch das zuvor ausgewählte Profil für die Updateausführung aus.  
  
 Sie können ein vorhandenes Update Testlauf-Profil ändern oder ein neues Profil erstellen, indem Sie auf der Cau-Benutzeroberfläche die Option **Update-Lauf Profil erstellen oder ändern** auswählen

Im folgenden finden Sie einige wichtige Hinweise zur Verwendung von Update Lauf Profilen:

* Bei einem Update Lauf Profil werden keine Cluster spezifischen Informationen, wie z. b. administrative Anmelde Informationen, gespeichert. Wenn Sie Cau im selbst Aktualisierungs Modus verwenden, speichert das Profil für die Update Ausführung auch keine Informationen zum selbst Aktualisierungs Zeitplan. Dies ermöglicht die Freigabe eines Profils für die Updateausführung in allen Failoverclustern in einer bestimmten Klasse.
* Wenn Sie selbst Aktualisierungs Optionen mithilfe eines Profils für die Update Laufzeit konfigurieren und das Profil später mit anderen Werten für die Update Lauf Optionen ändern, ändert sich die selbst Aktualisierungs Konfiguration nicht automatisch. Sie müssen die Selbstaktualisierungsoptionen erneut konfigurieren, damit die neuen Einstellungen für die Updateausführung übernommen werden.
* Der Run profile Editor unterstützt leider keine Dateipfade, die Leerzeichen enthalten, z. b. " *c:\Programme*". Um dieses Problem zu umgehen, speichern Sie Ihre Pre-und Post-Update Skripts in einem Pfad, der keine Leerzeichen enthält, oder verwenden Sie PowerShell ausschließlich zum Verwalten von Lauf Profilen, indem Sie beim Ausführen von " **aufrufen-caurun**" die Anführungszeichen

### <a name="windows-powershell-equivalent-commands"></a>Gleichwertige Windows PowerShell-Befehle
  
 Sie können die Einstellungen aus einem Profil für die Update Ausführung importieren, wenn Sie das Cmdlet " **Aufruf-caurun**", " **Add-cauclusterrole**" oder " **Set-cauclusterrole** " ausführen.  
  
 Im folgenden Beispiel wird ein Scan und eine vollständige Updateausführung auf dem Cluster *CONTOSO-FC1* durchgeführt. Dazu werden die in *C:\Windows\Cluster\DefaultParameters.xml* festgelegten Updateausführungsoptionen verwendet. Für die übrigen Cmdlet-Parameter werden Standardwerte verwendet.  
  
```powershell  
$MyRunProfile = Import-Clixml C:\Windows\Cluster\DefaultParameters.xml  
Invoke-CauRun –ClusterName CONTOSO-FC1 @MyRunProfile   
```  
  
 Durch die Verwendung eines Profils für die Updateausführung können Sie ein Failovercluster wiederholt mit einheitlichen Einstellungen für die Ausnahmenverwaltung, Zeitbindungen und weitere Betriebsparameter aktualisieren. Da diese Einstellungen in der Regel spezifisch für eine Klasse von Failoverclustern – z. B. %%amp;quot;Alle Microsoft SQL Server-Cluster%%amp;quot; oder %%amp;quot;Meine unternehmenswichtigen Cluster%%amp;quot; – sind, sollten Sie jedes Profil für die Updateausführung entsprechend der Klasse von Failoverclustern benennen, mit der es verwendet wird. Außerdem sollten Sie das Profil für die Updateausführung in einer Dateifreigabe verwalten, die für alle Failovercluster einer bestimmten Klasse in Ihrer IT-Organisation zugänglich ist.  
  
  
  
## <a name="see-also"></a>Siehe auch

-   [Clusterfähiges Aktualisieren](cluster-aware-updating.md)
  
-   [Cmdlets für Cluster fähiges aktualisieren in Windows PowerShell](https://docs.microsoft.com/powershell/module/clusterawareupdating/?view=win10-ps)