---
ms.assetid: d44d4430-41e2-483a-9685-92610cdef32a
title: Funktionsweise von Cluster-Aware Updating-Plug-Ins
ms.topic: article
ms.prod: windows-server-threshold
manager: dongill
ms.author: jgerend
author: JasonGerend
ms.date: 4/28/2017
ms.technology: storage-failover-clustering
description: Vorgehensweise beim-Plug-Ins verwenden, um Updates zu koordinieren, wenn Cluster-Aware Updating in Windows Server verwenden, um Updates auf einem Cluster zu installieren.
ms.openlocfilehash: eb606dfbe6596ecabd35e6ac36624fab2b4436b9
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="how-cluster-aware-updating-plug-ins-work"></a>Funktionsweise von Cluster-Aware Updating-Plug-Ins

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server2016, Windows Server2012 R2, Windows Server 2012

[Cluster-Aware Updating](cluster-aware-updating.md) (CAU) verwendet-Plug-Ins, um die Installation von Updates über alle Knoten eines Failoverclusters zu koordinieren. Dieses Thema enthält Informationen zur Verwendung der integrierten Remoteverwaltungssoftware clusterfähiges oder andere Remoteverwaltungssoftware-ins, die Sie für clusterfähiges aktualisieren installieren.

## <a name="BKMK_INSTALL"></a>Installieren Sie ein Remoteverwaltungssoftware in  
Ein Remoteverwaltungssoftware-in die standardmäßige Remoteverwaltungssoftware-ins, die mit dem clusterfähigen aktualisieren installiert sind \ (**Microsoft.WindowsUpdatePlugin** und **Microsoft.HotfixPlugin**\) müssen separat installiert werden. Wenn das clusterfähige aktualisieren im Remoteaktualisierungsmodus deren Hilfe verwendet wird, muss das Remoteverwaltungssoftware in auf allen Clusterknoten installiert werden. Wenn das clusterfähige aktualisieren im Remoteaktualisierungsmodus Remote\ verwendet wird, muss auf dem Remotecomputer des Updatekoordinators Remoteverwaltungssoftware-in installiert werden. Ein Remoteverwaltungssoftware in die Installation möglicherweise zusätzliche Installationsanforderungen auf jedem Knoten.  
  
Befolgen Sie die Anweisungen zum Installieren einer Remoteverwaltungssoftware in Remoteverwaltungssoftware in Herausgeber. Um manuell ein Remoteverwaltungssoftware in mit dem clusterfähigen aktualisieren zu registrieren, müssen die [Register-CauPlugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin) Cmdlet auf jedem Computer, auf dem das Remoteverwaltungssoftware-in installiert ist.  
  
## <a name="specify-a-plug-in-and-plug-in-arguments"></a>Geben Sie eine Remoteverwaltungssoftware-in und Remoteverwaltungssoftware in Argumente  
  
### <a name="specify-a-cau-plug-in"></a>Geben Sie ein CAU Remoteverwaltungssoftware in

In die CAU-UI wählen Sie ein Remoteverwaltungssoftware in aus einer Dropdownliste der verfügbaren Add-Ins Remoteverwaltungssoftware Drop\, wenn Sie CAU verwenden, um die folgenden Aktionen ausführen:  
  
-   Anwenden von Updates auf dem Cluster  
  
-   Updatevorschau für Cluster  
  
-   Konfigurieren Sie Cluster Aktualisieren von deren Hilfe Optionen  
  
Standardmäßig wählt clusterfähiges aktualisieren das Remoteverwaltungssoftware in **Microsoft.WindowsUpdatePlugin**. Sie können jedoch angeben einer Remoteverwaltungssoftware-in, installiert und für das clusterfähige aktualisieren registriert ist.

> [!TIP]  
> In der CAU-UI können Sie nur ein einzelnes Remoteverwaltungssoftware-in für clusterfähiges aktualisieren verwenden, um eine Vorschau oder Anwenden von Updates während einer Updateausführung angeben. Mithilfe der CAU-PowerShell-Cmdlets können Sie eine oder mehrere Remoteverwaltungssoftware Plug-Ins angeben. Wenn Sie mehrere Arten von Updates für den Cluster installieren müssen, ist es in der Regel effizienter, mehrere Remoteverwaltungssoftware-ins eine updateausführung anzugeben, anstatt eine separate Updateausführung für jeden Remoteverwaltungssoftware-in. Beispielsweise werden in der Regel weniger Knoten neu gestartet wird ausgeführt.

Mithilfe der CAU-PowerShell-Cmdlets, die in der folgenden Tabelle aufgeführt sind, können Sie eine oder mehrere Remoteverwaltungssoftware Plug-Ins für eine Updateausführung oder Prüfung angeben, durch Übergabe der **– CauPluginName** Parameter. Sie können mehrere Remoteverwaltungssoftware im Namen angeben, indem Sie diese durch Kommas trennen. Wenn Sie mehrere Remoteverwaltungssoftware Plug-Ins angeben, Sie können auch steuern, wie die Remoteverwaltungssoftware-ins jeweils anderen während einer Updateausführung durch Angabe beeinflussen die **\-RunPluginsSerially**, **\-StopOnPluginFailure**, und **– SeparateReboots** Parameter. Weitere Informationen zur Verwendung von mehreren Remoteverwaltungssoftware-ins verwenden Sie die Links in der Cmdlet-Dokumentation in der folgenden Tabelle.  
  
|Cmdlet|Beschreibung|  
|----------|---------------|  
|[Add-CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/add-cauclusterrole)|Fügt die Clusterrolle für clusterfähiges aktualisieren, die die Aktualisierung mit deren Hilfe Funktionen für den Cluster bereitstellt.|  
|[Invoke-CauRun](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-caurun)|Prüft Clusterknoten auf geeignete Updates und installiert diese Updates über eine Updateausführung auf dem angegebenen Cluster.|  
|[Invoke-CauScan](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-causcan)|Prüft Clusterknoten auf geeignete Updates und gibt eine Liste mit den ersten Satz der Updates, die für jeden Knoten des angegebenen Clusters angewendet werden würde.|  
|[Set-CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/set-cauclusterrole)|Legt Konfigurationseigenschaften für die Clusterrolle für clusterfähiges aktualisieren auf dem angegebenen Cluster fest.|  
  
Wenn Sie mithilfe dieser Cmdlets nicht Remoteverwaltungssoftware im Parameter für clusterfähiges aktualisieren angeben, wird standardmäßig das Remoteverwaltungssoftware in **Microsoft.WindowsUpdatePlugin**.  
  
### <a name="specify-cau-plug-in-arguments"></a>Geben Sie Remoteverwaltungssoftware in Argumente für clusterfähiges aktualisieren  
Wenn Sie die updateausführungsoptionen konfigurieren, können Sie angeben, eine oder mehrere *Tokentypen = Value* -Paaren \(arguments\) für den ausgewählten Remoteverwaltungssoftware-in verwenden. Beispielsweise können in der CAU-UI, Sie mehrere Argumente wie folgt angeben:  
  
**Name1\ = Wert1; Name2\ = Wert2; Name3\ = Wert3**  
  
Diese *Tokentypen = Value* Paare sinnvoll ist, Remoteverwaltungssoftware in werden müssen, die Sie angeben. Für einige Remoteverwaltungssoftware Plug-Ins sind diese Argumente optional.  
  
Die Syntax der Remoteverwaltungssoftware in Argumente für clusterfähiges aktualisieren folgt die folgenden allgemeinen Regeln:  
  
-   Mehrere *Tokentypen = Value* Paare werden durch Semikolons getrennt.  
  
-   Ein Wert, der Leerzeichen ist umgeben von Anführungszeichen, z.B.: **Name1\ = "Value with Spaces"**.  
  
-   Die genaue Syntax *Wert* hängt von der Remoteverwaltungssoftware-in.  
  
So geben Remoteverwaltungssoftware Argumenten mithilfe der CAU-PowerShell-Cmdlets, die Unterstützung der **– CauPluginParameters** Parameter, übergeben Sie einen Parameter des Formulars:  
  
**\-CauPluginArguments @{Name1\ = Wert1; Name2\ = Wert2; Name3\ = Wert3}**  
  
Sie können auch eine vordefinierte PowerShell-Hashtabelle verwenden. Zum Angeben der Remoteverwaltungssoftware Argumenten für mehr als einen Remoteverwaltungssoftware in mehrere Hashtabellen mit Argumenten, übergeben, die durch Kommas getrennt werden. Übergeben Sie die Argumente Remoteverwaltungssoftware-in in der Remoteverwaltungssoftware-in im angegebenen Reihenfolge **CauPluginName**.  
  
### <a name="specify-optional-plug-in-arguments"></a>Geben Sie optional Remoteverwaltungssoftware-Argumente  
Remoteverwaltungssoftware-ins clusterfähigen aktualisieren installiert \ (**Microsoft.WindowsUpdatePlugin** und **Microsoft.HotfixPlugin**\) bieten zusätzliche Optionen, die Sie auswählen können. In der CAU-UI, diese werden auf einer **zusätzliche Optionen** Seite, nachdem Sie Optionen für die Remoteverwaltungssoftware-Updateausführung konfiguriert. Wenn Sie die CAU-PowerShell-Cmdlets verwenden, werden diese Optionen als optionale Remoteverwaltungssoftware-Argumente konfiguriert. Weitere Informationen finden Sie unter [mithilfe von "Microsoft.windowsupdateplugin"](#BKMK_WUP) und [mithilfe von "Microsoft.hotfixplugin"](#BKMK_HFP) weiter unten in diesem Thema.  
  
## <a name="manage-plug-ins-using-windows-powershell-cmdlets"></a>Remoteverwaltungssoftware-ins verwalten mithilfe von Windows PowerShell-Cmdlets  
  
|Cmdlet|Beschreibung|  
|----------|---------------|  
|[Get-CauPlugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/get-cauplugin)|Ruft Informationen über ein oder mehrere Softwareupdates aktualisieren Remoteverwaltungssoftware Plug-Ins, die auf dem lokalen Computer registriert sind.|  
|[Register-CauPlugin]((https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin))|Registriert ein softwareaktualisierungs Remoteverwaltungssoftware-in auf dem lokalen Computer aktualisieren.|  
|[Unregister-CauPlugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/unregister-cauplugin)|Entfernt ein softwareaktualisierungs Remoteverwaltungssoftware-in aus der Liste der Remoteverwaltungssoftware-ins, die von CAU verwendet werden kann. **Hinweis:** Remoteverwaltungssoftware-ins, die mit dem clusterfähigen aktualisieren installiert sind \ (**Microsoft.WindowsUpdatePlugin** und **Microsoft.HotfixPlugin**\) kann nicht aufgehoben werden.|  
  
## <a name="BKMK_WUP"></a>Mithilfe von "Microsoft.windowsupdateplugin"  

Die standardmäßige Remoteverwaltungssoftware-in für CAU, **Microsoft.WindowsUpdatePlugin**, führt die folgenden Aktionen aus:
- Kommuniziert mit der Windows Update-Agent auf jedem Knoten des Failoverclusters zum Anwenden von Updates, die für die Microsoft-Produkte erforderlich sind, die auf jedem Knoten ausgeführt werden.
- Es installiert clusteraktualisierungen direkt über Windows Update oder Microsoft Update oder von einem lokalen On\ \(WSUS\) Windows Server Update Services-Server.
- Es installiert nur ausgewählte allgemeiner Verteilung veröffentlichen \(GDR\)-Updates. Standardmäßig gilt die Remoteverwaltungssoftware in nur wichtige Softwareupdates. Es ist keine Konfiguration erforderlich. Die Standardkonfiguration heruntergeladen und installiert wichtige GDR-Updates auf jedem Knoten. 

> [!NOTE]
> Zum Anwenden von Updates als wichtige Softwareupdates, die standardmäßig aktiviert sind \ (z.B. Treiber Updates\), können Sie einen optionalen Parameter Remoteverwaltungssoftware-in konfigurieren. Weitere Informationen finden Sie unter [konfigurieren die Windows Update-Agent-Abfragezeichenfolge](#BKMK_QUERY).

### <a name="requirements"></a>Anforderungen

- Der Failovercluster und remote Remoteupdatekoordinator Computer \(if used\) müssen die Anforderungen für CAU erfüllt und die Konfiguration, die für die Remoteverwaltung erforderlich ist aufgeführt, [Anforderungen und Best Practices für clusterfähiges aktualisieren](cluster-aware-updating-requirements.md).
- Überprüfung [Empfehlungen zum Anwenden von Microsoft-Updates](cluster-aware-updating-requirements.md#BKMK_BP_WUA), und ändern Sie die Microsoft Update-Konfiguration für die Failoverclusterknoten vor.
- Für optimale Ergebnisse empfehlen wir die Ausführung der Best Practices Analyzer für CAU \(BPA\) um sicherzustellen, dass die Cluster- und updateumgebung ordnungsgemäß für die Anwendung von Updates über clusterfähiges aktualisieren konfiguriert sind. Weitere Informationen finden Sie unter [Test CAU updating Readiness](cluster-aware-updating-requirements.md#BKMK_BPA).

> [!NOTE]
> Updates, die das Akzeptieren von Microsoft-Lizenzbedingungen oder andere Benutzerinteraktionen erfordern, werden ausgeschlossen und müssen manuell installiert werden.

### <a name="additional-options"></a>Weitere Optionen

Optional können Sie die folgenden Remoteverwaltungssoftware in Argumente zum Erweitern oder Einschränken der Updates, die angewendet werden, indem das Remoteverwaltungssoftware in angeben:
- So konfigurieren Sie das Remoteverwaltungssoftware-in für die Anwendung von empfohlenen Updates zusätzlich zu wichtigen Updates auf den einzelnen Knoten in der CAU-UI auf die **zusätzliche Optionen** Seite auf die **empfohlene Updates die gleiche Weise wie wichtige Updates bereitstellen** Kontrollkästchen.
<br>Konfigurieren Sie wahlweise die **'IncludeRecommendedUpdates' \ = 'True'** Remoteverwaltungssoftware im Argument.
- Zum Konfigurieren von dem Remoteverwaltungssoftware-in können Sie die Typen von GDR-Updates zu filtern, die auf jedem Clusterknoten angewendet werden, geben Sie eine Windows Update-Agent Abfrage mithilfe einer **QueryString** Remoteverwaltungssoftware im Argument. Weitere Informationen finden Sie unter [konfigurieren die Windows Update-Agent-Abfragezeichenfolge](#BKMK_QUERY).

### <a name="BKMK_QUERY"></a>Konfigurieren der Windows Update-Agent-Abfragezeichenfolge  
Sie können ein Argument Remoteverwaltungssoftware-in für das standardmäßige Remoteverwaltungssoftware-in konfigurieren **Microsoft.WindowsUpdatePlugin**, die aus einer Abfragezeichenfolge für den Windows Update-Agent \(WUA\) besteht. Diese Anweisung verwendet die WUA-API, um eine oder mehrere Gruppen von Microsoft-Updates auf jedem Knoten, basierend auf bestimmten Kriterien angewendet zu identifizieren. Sie können mehrere Kriterien mithilfe einer logischen und oder oder kombinieren. Die WUA-Abfragezeichenfolge wird wie folgt in einem Remoteverwaltungssoftware im Argument angegeben:  
  
**QueryString\ = "Criterion1\ = Wert1 And\ / oder Criterion2\ = Wert2 And\ / oder..."**  
  
Beispielsweise **Microsoft.WindowsUpdatePlugin** wählt automatisch wichtige Updates unter Verwendung eines **QueryString** Argument, das erstellt wird, mit der **IsInstalled**, **Typ**, **IsHidden**, und **IsAssigned** Kriterien:  
  
**QueryString\ = "IsInstalled\ = 0 und Type\ = 'Software' und IsHidden\ = 0 und IsAssigned\ = 1"**  
  
Bei Angabe einer **QueryString** Argument, wird es anstelle des standardmäßigen verwendet **QueryString** für das Remoteverwaltungssoftware-in konfiguriert ist.  
  
#### <a name="example-1"></a>Beispiel 1
  
So konfigurieren Sie eine **QueryString** Argument, das ein bestimmtes Update installiert, wie durch die ID *f6ce46c1\-971c\-43f9\-a2aa\-783df125f003*:  
  
**QueryString\ = "UpdateID\ = 'f6ce46c1\-971c\-43f9\-a2aa\-783df125f003' und IsInstalled\ = 0"**  
  
> [!NOTE]  
> Im obigen Beispiel ist für die Anwendung von Updates mithilfe des Assistenten zum Cluster\ unterstützende aktualisieren gültig. Wenn Sie ein bestimmtes Update durch Konfigurieren von Optionen mit der CAU-UI deren Hilfe aktualisieren oder mithilfe von installieren möchten die **Add-CauClusterRole** oder **Set-CauClusterRole**PowerShell-Cmdlets müssen Sie den UpdateID-Wert mit zwei Singlethread-Anführungszeichen formatieren:  
>   
> **QueryString\ = "UpdateID\ ='' f6ce46c1\-971c\-43f9\-a2aa\-783df125f003'' und IsInstalled\ = 0"**  
  
#### <a name="example-2"></a>Beispiel 2
  
So konfigurieren Sie eine **QueryString** Argument, das ausschließlich Treiber installiert:  
  
**QueryString\ = "IsInstalled\ = 0 und Type\ = 'Treiber' und IsHidden\ = 0"**  
  
Weitere Informationen zu Abfragezeichenfolgen für das standardmäßige Remoteverwaltungssoftware-in **Microsoft.WindowsUpdatePlugin**, den Suchkriterien \ (z.B. **IsInstalled**\), und die Syntax, die Sie in die Abfragezeichenfolgen einbeziehen können finden Sie im Abschnittzu den Suchkriterien in der [Windows Update Agent (WUA)-API-Referenz](http://go.microsoft.com/fwlink/p/?LinkId=223304).  
  
## <a name="BKMK_HFP"></a>Verwenden von "Microsoft.hotfixplugin"  
Das Remoteverwaltungssoftware in **Microsoft.HotfixPlugin** kann zum Anwenden von Microsoft eingeschränkte Verteilung von Updates von \(LDR\) \ (auch als Hotfixes bezeichnet und früher QFEs\ genannt), dass Sie unabhängig herunterladen, um bestimmte Microsoft-Software-Probleme zu beheben. Das Plug-In Updates aus einem Stammordner für SMB-Dateifreigabe installiert und kann auch angepasst werden, um-Microsoft-Treiber, Firmware und BIOS-Updates anzuwenden.

> [!NOTE]
> Hotfixes stehen gelegentlich in Knowledge Base-Artikeln von Microsoft heruntergeladen, aber sie werden auch bereitgestellt, um Kunden auf der Grundlage As\ erforderlich.

### <a name="requirements"></a>Anforderungen

- Der Failovercluster und remote Remoteupdatekoordinator Computer \(if used\) müssen die Anforderungen für CAU erfüllt und die Konfiguration, die für die Remoteverwaltung erforderlich ist aufgeführt, [Anforderungen und Best Practices für clusterfähiges aktualisieren](cluster-aware-updating-requirements.md).
- Überprüfung [Empfehlungen zur Verwendung von Microsoft.HotfixPlugin](cluster-aware-updating-requirements.md#BKMK_BP_HF).
- Für optimale Ergebnisse empfehlen wir die Ausführung der Best Practices Analyzer für CAU \(BPA\)-Modell, um sicherzustellen, dass die Cluster- und updateumgebung ordnungsgemäß für die Anwendung von Updates über clusterfähiges aktualisieren konfiguriert sind. Weitere Informationen finden Sie unter [Test CAU updating Readiness](cluster-aware-updating-requirements.md#BKMK_BPA).
- Rufen Sie die Updates vom Herausgeber und kopieren oder Extrahieren Sie sie in einer Dateifreigabe Server Message Block \(SMB\) \ (Hotfix Stamm Folder\) unterstützt, die mindestens SMB 2.0 und kann von allen Clusterknoten und dem Remotecomputer des Updatekoordinators \ (Wenn Sie CAU im Arbeitsplatz\ Remote\ aktualisieren verwendet wird). Weitere Informationen finden Sie unter [Konfigurieren einer hotfixstammordnerstruktur](#BKMK_HF_ROOT) weiter unten in diesem Thema. 

    > [!NOTE]
    > In der Standardeinstellung diesem Remoteverwaltungssoftware-in installiert nur Hotfixes mit den folgenden Dateinamenerweiterungen: MSU, MSI und MSP.

- Kopieren Sie die Datei DefaultHotfixConfig.xml \ (die finden Sie unter der **%systemroot%\\System32\\WindowsPowerShell\\v1.0\\Modules\\ClusterAwareUpdating** Ordner auf einem Computer, in dem die CAU-Tools Installed\) auf den hotfixstammordner, die Sie erstellt und unter dem Sie die Hotfixes extrahiert haben. Kopieren Sie die Konfigurationsdatei z.B. *\\\MyFileServer\\Hotfixes\\Root\\*. 

    > [!NOTE]
    > Um die meisten Hotfixes von Microsoft und anderen Updates bereitgestellten zu installieren, kann die standardmäßige hotfixkonfigurationsdatei ohne Änderung verwendet werden. Wenn Ihr Szenario erfordert, können Sie die Konfigurationsdatei als erweiterte Aufgabe anpassen. Die Konfigurationsdatei kann benutzerdefinierte Regeln enthalten, zum Behandeln von Hotfixdateien mit der spezifische Erweiterung oder zum Definieren eines Verhaltens für bestimmte beendigungsbedingungen. Weitere Informationen finden Sie unter [Anpassen der hotfixkonfigurationsdatei](#BKMK_CONFIG_FILE) weiter unten in diesem Thema.

### <a name="configuration"></a>Konfiguration

Konfigurieren Sie die folgenden Einstellungen. Weitere Informationen finden Sie unter den Links zu Abschnitten weiter unten in diesem Thema.
- Der Pfad zum freigegebenen hotfixstammordner, der enthält die Updates anwenden und enthält die hotfixkonfigurationsdatei. Sie können diesen Pfad über die CAU-UI eingeben oder konfigurieren Sie die **HotfixRootFolderPath\ = \ < Pfad >** Remoteverwaltungssoftware in PowerShell-Argument. 

   > [!NOTE]
   > Sie können den hotfixstammordner als lokalen Pfad oder einen UNC-Pfad des Formulars angeben *\\\ServerName\\Share\\RootFolderName*. Ein Domäne\-basierte oder eigenständiger DFS-Namespace-Pfad kann verwendet werden. Allerdings die Remoteverwaltungssoftware-in-Funktionen zur Überprüfung der Zugriffsberechtigungen in der hotfixkonfigurationsdatei sind nicht kompatibel mit einem Pfad DFS-Namespace, sodass, wenn Sie einen konfigurieren, müssen Sie das Kontrollkästchen für deaktivieren Zugriffsberechtigungen mithilfe der CAU-UI oder durch Konfigurieren der **DisableAclChecks\ = 'True'** Remoteverwaltungssoftware im Argument.
- Einstellungen auf dem Server, der den hotfixstammordner So überprüfen Sie für die entsprechenden Berechtigungen für den Zugriff auf den Ordner und Sicherstellen der Integrität der Daten aus den SMB zugegriffen hostet freigegebenen Ordner \ (SMB-Signatur oder SMB-Encryption\). Weitere Informationen finden Sie unter [Einschränken des Zugriffs auf den hotfixstammordner](#BKMK_ACL).

### <a name="additional-options"></a>Weitere Optionen

- Konfigurieren Sie optional das Remoteverwaltungssoftware in, sodass SMB-Verschlüsselung beim Zugriff auf Daten von der hotfixdateifreigabe erzwungen wird. In der CAU-UI auf die **zusätzliche Optionen** Seite auf die **SMB-Verschlüsselung beim Zugriff auf den hotfixstammordner** aus, oder Konfigurieren der **RequireSMBEncryption\ = 'True'** Remoteverwaltungssoftware in PowerShell-Argument. 
  > [!IMPORTANT]
  > Sie müssen zusätzliche Konfigurationsschritte ausführen, auf dem SMB-Server SMB-Datenintegrität für SMB-Signatur oder SMB-Verschlüsselung zu aktivieren. Weitere Informationen finden Sie unter Schritt4 in [Einschränken des Zugriffs auf den hotfixstammordner](#BKMK_ACL). Wenn Sie die Option zum Erzwingen der Verwendung der SMB-Verschlüsselung und der hotfixstammordner nicht konfiguriert für den Zugriff mithilfe von SMB-Verschlüsselung, die Updateausführung schlägt fehl.
- Deaktivieren Sie optional die Standardprüfungen auf ausreichende Berechtigungen für den hotfixstammordner und die hotfixkonfigurationsdatei. Wählen Sie die CAU-UI **Prüfung auf Administratorzugriff auf hotfixstammordner Stamm und Konfigurationsdatei deaktivieren**, oder konfigurieren Sie die **DisableAclChecks\ = 'True'** Remoteverwaltungssoftware im Argument.
- Konfigurieren Sie optional die **HotfixInstallerTimeoutMinutes\ =<Integer>** Argument, um anzugeben, wie lange das Hotfix Remoteverwaltungssoftware in hotfixinstallationsprozesses zurückzugebenden wartet. \ (Der Standardwert ist 30Minuten. \) um ein Zeitlimit von zwei Stunden anzugeben, legen Sie z.B. **HotfixInstallerTimeoutMinutes\ = 120**.
- Konfigurieren Sie optional die **HotfixConfigFileName \ = <name>**Remoteverwaltungssoftware in-Argument, um einen Namen für die hotfixkonfigurationsdatei anzugeben, die sich im hotfixstammordner befindet. Wenn nicht angegeben ist, wird der Standardname DefaultHotfixConfig.xml verwendet.
  
### <a name="BKMK_HF_ROOT"></a>Konfigurieren einer hotfixstammordnerstruktur

Für das Hotfix Remoteverwaltungssoftware-in funktioniert, müssen die Hotfixes werden gespeichert in einer überlegt definierten Struktur in einer SMB-Dateifreigabe \ (Hotfix Stamm Folder\), und Sie den Hotfix Remoteverwaltungssoftware im durch den Pfad zum hotfixstammordner über die CAU-UI oder der CAU-PowerShell-Cmdlets konfigurieren. Dieser Pfad wird für das Remoteverwaltungssoftware als übergeben der **HotfixRootFolderPath** Argument. Sie können eine von vielen Strukturen für den hotfixstammordner gemäß Ihrer aktualisierungsanforderungen auswählen, wie in den folgenden Beispielen gezeigt. Dateien oder Ordner, die in der Struktur nicht entsprechen, werden ignoriert.  
  
#### <a name="example-1---folder-structure-used-to-apply-hotfixes-to-all-cluster-nodes"></a>Beispiel 1: Ordnerstruktur zum Anwenden von Hotfixes auf alle Clusterknoten
  
Um anzugeben, dass Hotfixes für alle Clusterknoten gelten, kopieren Sie sie in einen Ordner namens **CAUHotfix\_All** unter dem hotfixstammordner. In diesem Beispiel die **HotfixRootFolderPath** Remoteverwaltungssoftware im Argument festgelegt ist *\\\MyFileServer\\Hotfixes\\Root\\*. Die **CAUHotfix\_All** Ordner enthält drei Updates mit den Erweiterungen MSU, MSI und MSP, die für alle Clusterknoten angewendet werden. Die Namen der Updatedateien sind nur zur Veranschaulichung.  
  
> [!NOTE]  
> In diesem und den folgenden Beispielen wird die hotfixkonfigurationsdatei mit dem Standardnamen DefaultHotfixConfig.xml in die erforderlichen Speicherort im hotfixstammordner angezeigt.  
  
```
\\MyFileServer\Hotfixes\Root\   
   DefaultHotfixConfig.xml  
   CAUHotfix_All\   
      Update1.msu   
      Update2.msi   
      Update3.msp  
      ...  
```  
  
#### <a name="example-2---folder-structure-used-to-apply-certain-updates-only-to-a-specific-node"></a>Beispiel 2 – Ordnerstruktur zum Anwenden bestimmter Updates nur für einen bestimmten Knoten
  
Um Hotfixes anzugeben, die nur für einen bestimmten Knoten gelten, verwenden Sie einen Unterordner unter dem hotfixstammordner mit dem Namen des Knotens. Verwenden Sie den NetBIOS-Namen des Clusterknotens, z.B. *ContosoNode1*. Verschieben Sie dann die Updates, die nur für diesen Knoten, um diesen Unterordner gelten. Im folgenden Beispiel der **HotfixRootFolderPath** Remoteverwaltungssoftware im Argument festgelegt ist *\\\MyFileServer\\Hotfixes\\Root\\*. Aktualisiert die **CAUHotfix\_All** Ordner auf allen Clusterknoten angewendet werden und *Node1\_Specific\_Update.msu* ausgeglichen werden nur für *ContosoNode1*.  
  
```
\\MyFileServer\Hotfixes\Root\   
   DefaultHotfixConfig.xml  
   CAUHotfix_All\   
      Update1.msu   
      Update2.msi   
      Update3.msp  
      ...  
   ContosoNode1\   
      Node1_Specific_Update.msu   
      ...  
```  
  
#### <a name="example-3---folder-structure-used-to-apply-updates-other-than-msu-msi-and-msp-files"></a>Beispiel 3 – Ordnerstruktur zum Anwenden von Updates als MSU, MSI und MSP-Dateien
  
In der Standardeinstellung **Microsoft.HotfixPlugin** nur auf Updates mit der Erweiterung MSU, MSI oder MSP angewendet. Bestimmte Updates können jedoch andere Erweiterungen aufweisen und somit andere Installationsbefehle erfordern. Beispielsweise müssen Sie ein Firmwareupdate mit der Erweiterung .exe auf einen Knoten in einem Cluster anwenden. Sie können den hotfixstammordner mit einem Unterordner, der angibt, einen bestimmten konfigurieren, die nicht standardmäßige Updatetyp installiert werden soll. Außerdem müssen Sie eine entsprechende ordnerinstallationsregel, die den Installationsbefehl gibt Konfigurieren der `<FolderRules>`Element in der Hotfix-XML-Konfigurationsdatei.  
  
Im folgenden Beispiel der **HotfixRootFolderPath** Remoteverwaltungssoftware im Argument festgelegt ist *\\\MyFileServer\\Hotfixes\\Root\\*. Mehrere Updates werden auf alle Knoten des Clusters, und eine Aktualisierung der Firmware angewendet *SpecialHotfix1.exe* ausgeglichen werden *ContosoNode1* mit *FolderRule1*. Informationen zum Konfigurieren von *FolderRule1* in der hotfixkonfigurationsdatei finden Sie unter [Anpassen der hotfixkonfigurationsdatei](#BKMK_CONFIG_FILE) weiter unten in diesem Thema.  
  
```
\\MyFileServer\Hotfixes\Root\   
   DefaultHotfixConfig.xml  
   CAUHotfix_All\   
      Update1.msu   
      Update2.msi   
      Update3.msp  
      ...  
  
   ContosoNode1\   
      FolderRule1\  
          SpecialHotfix1.exe  
      ...  
```

### <a name="BKMK_CONFIG_FILE"></a>Anpassen der hotfixkonfigurationsdatei  
Die hotfixkonfigurationsdatei Steuerelemente wie Datei **Microsoft.HotfixPlugin** bestimmte hotfixtypen in einem Failovercluster installiert. Das XML-Schema für die Konfigurationsdatei wird in HotfixConfigSchema.xsd, definiert, die in den folgenden Ordner auf einem Computer befindet, auf dem die CAU-Tools installiert werden:  
  
**%systemroot%\\System32\\WindowsPowerShell\\v1.0\\Modules\\ClusterAwareUpdating Ordner**  
  
Anpassen der hotfixkonfigurationsdatei, kopieren die Beispielkonfigurationsdatei DefaultHotfixConfig.xml von diesem Speicherort auf den hotfixstammordner, und stellen Sie die entsprechenden Änderungen für Ihr Szenario.  
  
> [!IMPORTANT]  
> Wenn die meisten Hotfixes von Microsoft und anderen Updates bereitgestellten anwenden möchten, kann die standardmäßige hotfixkonfigurationsdatei ohne Änderung verwendet werden. Anpassung der hotfixkonfigurationsdatei ist nur in fortgeschrittenen Verwendungsszenarios.  
  
Standardmäßig definiert die XML-hotfixkonfigurationsdatei Installationsregeln und beendigungsbedingungen für die folgenden beiden Kategorien von Hotfixes:  
  
-   Hotfixdateien mit Erweiterungen, die das Remoteverwaltungssoftware in standardmäßig installiert werden können \ (MSU, MSI und MSP-c:\programme\).  
  
    Diese sind definiert als `<ExtensionRules>`Elemente in der `<DefaultRules>`Element. Es gibt einen `<Extension>` -Element für jeden standardmäßig unterstützten Dateitypen. Die allgemeine XML-Struktur lautet wie folgt:  
  
    ```xml  
    <DefaultRules>  
        <ExtensionRules>  
          <Extension name="MSI">  
            <!-- Template and ExitConditions elements for installation of .msi files follow -->  
             ...  
          </Extension>  
          <Extension name="MSU">  
            <!-- Template and ExitConditions elements for installation of .msu files follow -->  
             ...  
          </Extension>  
          <Extension name="MSP">  
            <!-- Template and ExitConditions elements for installation of .msp files follow -->  
             ...  
          </Extension>  
             ...  
       </ExtensionRules>  
    </DefaultRules>  
    ```  
  
    Wenn Sie bestimmte Updatetypen auf alle Clusterknoten in Ihrer Umgebung anwenden müssen, können Sie zusätzliche definieren `<Extension>`Elemente.  
  
-   Hotfix oder andere Updatedateien, die nicht um MSI-, MSU- oder MSP-Dateien sind, z.B.-Microsoft-Treiber, Firmware und BIOS-Updates.  
  
    Jeder nicht standardmäßige Dateityp wird als konfiguriert eine `<Folder>`Element in der `<FolderRules>`Element. Das Namensattribut des der `<Folder>`Element muss identisch mit dem Namen eines Ordners im hotfixstammordner, die Updates vom entsprechenden Typ enthalten sein. Der Ordner kann sich der **CAUHotfix\_All** Ordner oder in einem Ordner eine spezifische. Wenn beispielsweise *FolderRule1* ist in den hotfixstammordner konfiguriert ist, konfigurieren Sie das folgende Element in der XML-Datei definieren eine Installationsvorlage und beendigungsbedingungen für die Updates in diesem Ordner:  
  
    ```xml  
    <FolderRules>  
          <Folder name="FolderRule1">  
            <!-- Template and ExitConditions elements for installation of updates in FolderRule1 follow -->  
             ...  
          </Folder>  
          ...  
    </FolderRules>  
    ```  
  
Die folgenden Tabellen beschreiben die `<Template>` -Attribute und mögliche `<ExitConditions>`Unterelemente.  
  
|`<Template>` Attribut|Beschreibung|  
|--------------------------|---------------|  
|`path`|Den vollständigen Pfad zum Installationsprogramm für den Dateityp, der in definiert ist die `<Extension name>`Attribut.<br /><br />Verwenden Sie zum Angeben des Pfads zu einer Updatedatei in der Hotfix-stammordnerstruktur `$update$`.|  
|`parameters`|Eine Zeichenfolge erforderlicher und optionaler Parameter für das Programm, das in angegebenen `path`.<br /><br />Verwenden, um einen Parameter anzugeben, die den Pfad zu einer Updatedatei in der Hotfix-stammordnerstruktur `$update$`.|  
  
|`<ExitConditions>` Unterelement|Beschreibung|  
|---------------------------------|---------------|  
|`<Success>`|Definiert mindestens einen Beendigungscode, die angeben, das Update erfolgreich war. Hierbei handelt es sich um ein erforderliches Unterelement.|  
|`<Success_RebootRequired>`|Definiert optional mindestens einen Beendigungscode, die angeben, das Update erfolgreich war, und der Knoten muss neu gestartet. <br>**Hinweis:** optional die `<Folder>` -Element enthalten kann die `alwaysReboot`Attribut. Wenn dieses Attribut festgelegt ist, es gibt an, dass wenn ein von dieser Regel installiertes Hotfix gibt einen der Beendigungscodes, die in definiert ist `<Success>`, darüber hinaus eine `<Success_RebootRequired>`Bedingung zu beenden.|  
|`<Fail_RebootRequired>`|Definiert optional mindestens einen Beendigungscode, die angeben, die angegebene Aktualisierung fehlgeschlagen ist und der Knoten muss neu gestartet.|  
|`<AlreadyInstalled>`|Definiert optional mindestens einen Beendigungscode, die darauf hinweisen, dass das Update nicht angewendet wurde, da es bereits installiert ist.|  
|`<NotApplicable>`|Definiert optional mindestens einen Beendigungscode, die darauf, dass das Update nicht angewendet wurde hinweisen, da es sich nicht auf den Clusterknoten.|  
  
> [!IMPORTANT]  
> Ein Beendigungscode, die in nicht explizit definiert ist `<ExitConditions>`interpretiert wird, wie die Aktualisierung fehlgeschlagen ist und der Knoten nicht neu gestartet.  
  
### <a name="BKMK_ACL"></a>Einschränken des Zugriffs auf den hotfixstammordner  
Sie müssen verschiedene Schrittezum Konfigurieren von SMB-Server und Datei-Dateifreigabe zum Sichern der Hotfixdateien Root-Ordner und die-Dateifreigabe für den Zugriff nur im Kontext des ausführen **Microsoft.HotfixPlugin **. Diese Schritteaktivieren verschiedene Features, die verhindern, dass mögliche Manipulationen an den Hotfixdateien in einer Weise, die den Failovercluster gefährden können.  
  
Die allgemeinen Schrittesehen wie folgt aus:  
  
1.  Identifizieren des Benutzerkontos, das für Updateausführungen verwendet wird, mit dem Remoteverwaltungssoftware in  
  
2.  Konfigurieren Sie dieses Benutzerkontos in den erforderlichen Gruppen auf dem SMB-Dateiserver  
  
3.  Konfigurieren der Berechtigungen für den Zugriff auf den hotfixstammordner  
  
4.  Konfigurieren Sie Einstellungen für SMB-Datenintegrität  
  
5.  Aktivieren Sie eine Windows-Firewall-Regel auf dem SMB-Server  
  
#### <a name="step-1-identify-the-user-account-that-is-used-for-updating-runs-by-using-the-hotfix-plug-in"></a>Schritt1. Identifizieren des Benutzerkontos, das für Updateausführungen verwendet wird, mit dem Hotfix Remoteverwaltungssoftware in
  
Das Konto, das in für clusterfähiges aktualisieren, zum Prüfen der Sicherheitseinstellungen verwendet wird während einer Updateausführung mithilfe **Microsoft.HotfixPlugin** abhängig, ob CAU wie folgt im Remote\ aktualisieren oder Aktualisieren von deren Hilfe Modus verwendet wird:  
  
-   **Remote\ Remoteaktualisierungsmodus** das Konto, das über Administratorrechte verfügt, auf dem Cluster, um eine Vorschau anzeigen oder Updates anzuwenden.  
  
-   **Deren Hilfe Remoteaktualisierungsmodus** der Namen des virtuellen Computerobjekts, das in Active Directory, für die CAU konfiguriert ist-Clusterrolle. Dies ist der Name des einer vorab bereitgestellten virtuellen Computerobjekts in Active Directory für die Clusterrolle für clusterfähiges aktualisieren oder den Namen, der für die Clusterrolle clusterfähigen Aktualisierens generiert wurde. Führen Sie zum Abrufen des Namens, wenn er durch CAU generiert wird, die **Get-CauClusterRole** CAU-PowerShell-Cmdlet. In der Ausgabe **ResourceGroupName** ist der Name des generierten virtuellen computerobjektkontos.  
  
#### <a name="step-2-configure-this-user-account-in-the-necessary-groups-on-an-smb-file-server"></a>Schritt2. Konfigurieren Sie dieses Benutzerkontos in den erforderlichen Gruppen auf dem SMB-Dateiserver
  
> [!IMPORTANT]  
> Sie müssen das Konto hinzufügen, das für Updateausführungen als ein lokales Administratorkonto auf dem SMB-Server verwendet wird. Wenn dies aufgrund der Sicherheitsrichtlinien in Ihrer Organisation nicht zulässig ist, konfigurieren Sie dieses Konto mit den erforderlichen Berechtigungen auf dem SMB-Server mithilfe des folgenden Verfahrens.  
  
##### <a name="to-configure-a-user-account-on-the-smb-server"></a>So konfigurieren Sie ein Benutzerkonto auf dem SMB-Server  
  
1.  Fügen Sie das Konto, das für Updateausführungen, um die Gruppe "Distributed COM-Benutzer" und eine der folgenden Gruppen verwendet wird hinzu: Hauptbenutzer, Servervorgang oder Druck-Operator.  
  
2.  Um die erforderlichen WMI-Berechtigungen für das Konto zu aktivieren, starten Sie die WMI-Verwaltungskonsole auf dem SMB-Server. Starten Sie PowerShell, und geben Sie den folgenden Befehl aus:  
  
    ```  
    wmimgmt.msc  
    ```  
  
3.  In der Konsolenstruktur mit der rechten Maustaste auf **WMI-Steuerung \(Local\)**, und klicken Sie dann auf **Eigenschaften **.  
  
4.  Klicken Sie auf **Security**, und erweitern Sie dann **Root **.  
  
5.  Klicken Sie auf **CIMV2**, und klicken Sie dann auf **Security **.  
  
6.  Fügen Sie das Konto, das für Updateausführungen verwendet wird die **Gruppen- oder Benutzernamen** Liste.  
  
7.  Gewähren der **Methoden ausführen** und **Remoteaktivierung** Berechtigungen für das Konto, das für Updateausführungen verwendet wird.  
  
#### <a name="step-3-configure-permissions-to-access-the-hotfix-root-folder"></a>Schritt3. Konfigurieren der Berechtigungen für den Zugriff auf den hotfixstammordner
  
Beim Versuch, Updates anzuwenden, überprüft der Hotfix Remoteverwaltungssoftware in die Konfiguration der NTFS-Berechtigungen für den Zugriff auf den hotfixstammordner. Wenn die Ordnerzugriffsberechtigungen nicht ordnungsgemäß konfiguriert sind, kann die Updateausführung mit dem Hotfix Remoteverwaltungssoftware in fehlschlagen.  
  
Wenn Sie die Standardkonfiguration des Hotfix Remoteverwaltungssoftware in verwenden, stellen Sie sicher, dass die Zugriffsberechtigungen für Ordner die folgenden Anforderungen erfüllen.  
  
-   Die Gruppe "Benutzer" verfügt über die Berechtigung Lesen.  
  
-   Wenn das Remoteverwaltungssoftware in Updates mit der Erweiterung .exe angewendet wird, hat die Gruppe "Benutzer" Ausführungsberechtigung.  
  
-   Dürfen nur bestimmten Sicherheitsprinzipalen \ (jedoch nicht Required\) über die Berechtigung zu schreiben. Die zulässigen Prinzipale sind die lokale Administratoren Gruppenrichtlinien, SYSTEM, Ersteller-Besitzer und TrustedInstaller. Andere Konten oder Gruppen dürfen nicht über die Berechtigung auf den hotfixstammordner zu schreiben.  
  
Optional können Sie die vorherigen Prüfungen deaktiviert, die das Remoteverwaltungssoftware in standardmäßig ausführt. Hierzu können Sie auf zwei Arten:  
  
-   Wenn Sie die CAU-PowerShell-Cmdlets verwenden, konfigurieren Sie die **DisableAclChecks\ = 'True'** Argument in der **CauPluginArguments** Parameter für das Hotfix Remoteverwaltungssoftware-in.  
  
-   Wenn Sie die CAU-UI verwenden, wählen Sie die **Prüfung auf Administratorzugriff auf hotfixstammordner Stamm und Konfigurationsdatei deaktivieren** Option auf der **Weitere Updateoptionen** Seite des Assistenten, mit dem updateausführungsoptionen konfiguriert.  
  
Als bewährte Methode in vielen Umgebungen wird jedoch empfohlen, dass Sie die Standardkonfiguration verwenden, um diese Kontrollen zu erzwingen.  
  
#### <a name="step-4-configure-settings-for-smb-data-integrity"></a>Schritt4. Konfigurieren Sie Einstellungen für SMB-Datenintegrität
  
Zum Überprüfen der Integrität der Daten in die Verbindungen zwischen den Clusterknoten und SMB-Dateifreigabe erfordert das Hotfix Remoteverwaltungssoftware-in, Einstellungen für die SMB-Dateifreigabe für SMB-Signatur oder SMB-Verschlüsselung zu aktivieren. SMB-Verschlüsselung, die eine höhere Sicherheit und eine bessere Leistung in vielen Umgebungen bereitstellt, wird ab Windows Server2012 unterstützt. Sie können eine oder beide der folgenden Einstellungen wie folgt aktivieren:  
  
-   Zum Aktivieren der SMB-Signatur finden Sie unter dem Verfahren in den [Artikel 887429](http://support.microsoft.com/kb/887429) in der Microsoft Knowledge Base.  
  
-   Führen Sie das folgende PowerShell-Cmdlet zum Aktivieren der SMB-Verschlüsselung für den freigegebenen SMB-Ordner auf dem SMB-Server:  
  
    ```PowerShell  
    Set-SmbShare <ShareName> -EncryptData $true  
    ```  
  
    Wobei <*Freigabename*> ist der Name des freigegebenen SMB-Ordners.  
  
Um die Verwendung der SMB-Verschlüsselung der Verbindungen zum SMB-Server zu erzwingen, wählen Sie optional die **SMB-Verschlüsselung beim Zugriff auf den hotfixstammordner** in die CAU-UI aus, oder Konfigurieren der **RequireSMBEncryption\ = 'True'** Remoteverwaltungssoftware im Argument mithilfe der CAU-PowerShell-Cmdlets.  
  
> [!IMPORTANT]  
> Wenn Sie die Option zum Erzwingen der Verwendung der SMB-Verschlüsselung und der hotfixstammordner nicht für Verbindungen, die SMB-Verschlüsselung konfiguriert, die Updateausführung schlägt fehl.  
  
#### <a name="step-5-enable-a-windows-firewall-rule-on-the-smb-server"></a>Schritt5. Aktivieren Sie eine Windows-Firewall-Regel auf dem SMB-Server
  
Sie müssen die Aktivieren der **Dateiserver-Remoteverwaltung \(SMB\-in\)** Regel in der Windows-Firewall auf dem SMB-Dateiserver. Dies ist standardmäßig in Windows Server2016, Windows Server2012 R2 und Windows Server2012 aktiviert.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Übersicht über das clusterfähige aktualisieren](cluster-aware-updating.md)
  
-   [Cluster-Aware aktualisieren Windows PowerShell-Cmdlets](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating)  
  
-   [Clusterfähiges aktualisieren Plug-In-Referenz](http://msdn.microsoft.com/library/hh418084.aspx)  
  
