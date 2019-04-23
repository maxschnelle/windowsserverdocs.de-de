---
ms.assetid: d44d4430-41e2-483a-9685-92610cdef32a
title: Funktionsweise des clusterfähigen Aktualisierens-Plug-ins
ms.topic: article
ms.prod: windows-server-threshold
manager: dongill
ms.author: jgerend
author: JasonGerend
ms.date: 04/28/2017
ms.technology: storage-failover-clustering
description: So-Plug-ins verwenden, um Updates zu koordinieren, wenn der Cluster-Aware Updating in Windows Server verwenden, um die Installation von Updates auf einem Cluster.
ms.openlocfilehash: d09addb5e6787a8386d50570c0d27640646aa587
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854561"
---
# <a name="how-cluster-aware-updating-plug-ins-work"></a>Funktionsweise des clusterfähigen Aktualisierens-Plug-ins

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

[Cluster-Aware Updating](cluster-aware-updating.md) (aktualisieren CAU)-Plug-ins verwendet, um die Installation von Updates auf Knoten in einem Failovercluster zu koordinieren. Dieses Thema enthält Informationen zur Verwendung der integrierten\-in CAU-Plug\-ins oder anderen Plug-Ins\-ins, die Sie für clusterfähiges aktualisieren installieren.

## <a name="BKMK_INSTALL"></a>Installieren Sie ein Plug &\-in  
Schleichwerbung\-als den Standardwert anschließen\-ins, die mit dem clusterfähigen aktualisieren installiert sind \( **Microsoft.WindowsUpdatePlugin** und **Microsoft.HotfixPlugin** \)müssen separat installiert werden. Wenn für clusterfähiges aktualisieren, im Self-Service verwendet wird\-Updatemodus an, der Stecker\-in muss auf allen Clusterknoten installiert werden. Wenn für clusterfähiges aktualisieren, in Remotebüros verwendet wird\-Updatemodus an, der Stecker\-in muss auf dem Remotecomputer des Updatekoordinators installiert werden. Schleichwerbung\-in die Installation auf jedem Knoten Weitere Installationsanforderungen aufweisen kann.  
  
So installieren Sie ein Plug &\-, befolgen Sie die Anweisungen aus der Stecker\-im Publisher. So registrieren Sie manuell eine Plug &\-mit für clusterfähiges aktualisieren, führen Sie die [Register-CauPlugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin) Cmdlet auf jedem Computer, in dem der Stecker\-in installiert ist.  
  
## <a name="specify-a-plug-in-and-plug-in-arguments"></a>Geben Sie ein Plug &\-in, und schließen Sie\-in-Argumente  
  
### <a name="specify-a-cau-plug-in"></a>Geben Sie ein Plug-In für clusterfähiges aktualisieren\-in

In die CAU-UI, wählen Sie ein Plug &\-in in einem Dropdownmenü\-Liste der verfügbaren Plug-Ins\-ins, wenn Sie für clusterfähiges aktualisieren verwenden, um die folgenden Aktionen ausführen:  
  
-   Anwenden von Updates auf Cluster  
  
-   Updatevorschau für Cluster  
  
-   Konfigurieren von Self-Service-cluster\-Optionen aktualisieren  
  
Standardmäßig wählt clusterfähiges aktualisieren den Stecker\-in **Microsoft.WindowsUpdatePlugin**. Allerdings können Sie angeben, alle Plug &\-, installiert und für das clusterfähige aktualisieren registriert ist.

> [!TIP]  
> In die CAU-UI können Sie nur ein einzelnes Plug-in angeben\-in für clusterfähiges aktualisieren verwenden, um eine Vorschau anzuzeigen oder Updates während einer Updateausführung anwenden möchten. Mithilfe der CAU-PowerShell-Cmdlets zu verwenden, können Sie eine oder mehrere Plug-Ins angeben\-ins. Wenn Sie mehrere Arten von Updates für den Cluster installieren müssen, ist es in der Regel effizienter, mehrere Plug-Ins anzugeben\-ins in eine Updateausführung, anstatt eine separate Updateausführung für jedes Plug\-in. Dadurch sind z. B. meist weniger Knotenneustarts erforderlich.

Mithilfe der CAU-PowerShell-Cmdlets, die in der folgenden Tabelle aufgeführt sind, können Sie eine oder mehrere Plug-Ins angeben\-ins für eine Updateausführung oder die Überprüfung durch Übergeben der **– CauPluginName** Parameter. Sie können mehrere Plug-Ins angeben\-in Namen, indem diese durch Kommas trennen. Wenn Sie mehrere Plug-Ins angeben\-ins, Sie können auch steuern, wie der Stecker\-ins beeinflussen sich gegenseitig während einer Updateausführung, durch Angabe der  **\-RunPluginsSerially**,  **\- StopOnPluginFailure**, und **– SeparateReboots** Parameter. Weitere Informationen zur Verwendung mehrerer Plug-Ins\-ins, die verwendet werden die Links zur Cmdlet-Dokumentation in der folgenden Tabelle bereitgestellt.  
  
|Cmdlet|Beschreibung|  
|----------|---------------|  
|[Add-CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/add-cauclusterrole)|Fügt die Clusterrolle für clusterfähiges aktualisieren, die die Self-bietet\-Aktualisieren von Funktionalität mit dem angegebenen Cluster.|  
|[Invoke-CauRun](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-caurun)|Prüft Clusterknoten auf geeignete Updates und installiert diese Updates über eine Updateausführung auf dem angegebenen Cluster.|  
|[Invoke-CauScan](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-causcan)|Prüft Clusterknoten auf geeignete Updates und gibt eine Liste des ersten Updatesatzes zurück, der auf jeden Knoten des angegebenen Clusters angewendet werden würde.|  
|[Set-CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/set-cauclusterrole)|Legt Konfigurationseigenschaften für die Clusterrolle für clusterfähiges Aktualisieren auf dem angegebenen Cluster fest.|  
  
Wenn Sie kein Plug-In für clusterfähiges aktualisieren angeben\-Parameter mithilfe dieser Cmdlets, der Standardwert ist der Stecker\-in **Microsoft.WindowsUpdatePlugin**.  
  
### <a name="specify-cau-plug-in-arguments"></a>Geben Sie die Plug-In für clusterfähiges aktualisieren\-in-Argumente  
Wenn Sie die Optionen für die Updateausführung konfigurieren, können Sie angeben, eine oder mehrere *Namen\=Wert* Paare \(Argumente\) für die ausgewählten Plug\-an, zu verwenden. Auf der Benutzeroberfläche für clusterfähiges Aktualisieren können Sie z. B. wie folgt mehrere Argumente angeben:  
  
**Name1\=Value1;Name2\=Value2;Name3\=Value3**  
  
Diese *Namen\=Wert* Paare müssen für das Plug-in verwertbar sein\-, da Sie angeben. Für einige Plug-Ins\-ins die Argumente sind optional.  
  
Die Syntax von der CAU-Stecker\-gelten folgende allgemeine Regeln für in-Argumente:  
  
-   Mehrere *Namen\=Wert* -Paare werden durch Semikolons getrennt.  
  
-   Ein Leerzeichen enthaltender Wert wird in Anführungszeichen gestellt. Beispiel: **Name1\="Value with Spaces"**.  
  
-   Die genaue Syntax des *Wert* hängt von der Stecker\-in.  
  
An Plug-Ins\-in-Argumente mithilfe der CAU-PowerShell-Cmdlets, die Unterstützung der **– CauPluginParameters** Parameter, übergeben Sie einen Parameter des Formulars:  
  
**\-CauPluginArguments @{Name1\=Wert1; Name2\=Value2; Name3\=Wert3}**  
  
Sie können auch eine vordefinierte PowerShell-Hashtabelle verwenden. Angeben von Plug &\-in-Argumente für mehr als eine Plug\-, übergeben Sie mehrere Hashtabellen mit Argumenten, die durch Kommas voneinander getrennt. Übergeben den Stecker\-in Argumenten in der Stecker\-, damit im angegebenen **CauPluginName**.  
  
### <a name="specify-optional-plug-in-arguments"></a>Geben Sie optional Plug\-in-Argumente  
Der Stecker\-ins das clusterfähige aktualisieren installierten \( **Microsoft.WindowsUpdatePlugin** und **Microsoft.HotfixPlugin** \) bieten zusätzliche Optionen, die Sie auswählen können. Die CAU-UI, diese werden auf einem **zusätzliche Optionen** Seite nach dem Konfigurieren der Optionen der Updateausführung für das Plug-in\-in. Wenn Sie die CAU-PowerShell-Cmdlets verwenden, werden diese Optionen als optionale Plug-in konfiguriert\-in-Argumente. Weitere Informationen finden Sie unter [Verwenden von "Microsoft.WindowsUpdatePlugin"](#BKMK_WUP) und [Verwenden von "Microsoft.HotfixPlugin"](#BKMK_HFP) weiter unten in diesem Thema.  
  
## <a name="manage-plug-ins-using-windows-powershell-cmdlets"></a>Verwalten von Plug-Ins\-ins, die mit Windows PowerShell-Cmdlets  
  
|Cmdlet|Beschreibung|  
|----------|---------------|  
|[Get-CauPlugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/get-cauplugin)|Ruft Informationen über eine oder mehrere softwareaktualisierungs-Plug &\-ins, die auf dem lokalen Computer registriert sind.|  
|[Register-CauPlugin]((https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin))|Registriert ein softwareaktualisierungs Aktualisieren von Plug-Ins\-in auf dem lokalen Computer.|  
|[Unregister-CauPlugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/unregister-cauplugin)|Entfernt ein softwareaktualisierungs-Plug &\-in aus der Liste der Plug &\-ins, die von CAU verwendet werden kann. **Hinweis**: Der Stecker\-ins, die mit dem clusterfähigen aktualisieren installiert sind \( **Microsoft.WindowsUpdatePlugin** und **Microsoft.HotfixPlugin** \) kann nicht aufgehoben werden.|  
  
## <a name="BKMK_WUP"></a>Verwenden von Microsoft.WindowsUpdatePlugin  

Der Standard-Stecker\-in für clusterfähiges aktualisieren, **Microsoft.WindowsUpdatePlugin**, führt die folgenden Aktionen aus:
- Das Plug-In steht in Kontakt mit dem Windows Update-Agent auf den einzelnen Knoten des Failoverclusters, um Updates für die Microsoft-Produkte anzuwenden, die auf den einzelnen Knoten ausgeführt werden.
- Installationen cluster Updates direkt von Windows Update oder Microsoft Update oder von einer auf\-lokale Windows Server Update Services \(WSUS\) Server.
- Installiert nur ausgewählte, die allgemeine Vertriebsversion \(GDR\) Updates. Standardmäßig wird der Stecker\-in wendet nur wichtige Softwareupdates. Es ist keine Konfiguration erforderlich. Die Standardkonfiguration lädt wichtige Updates von allgemeinen Vertriebsversionen auf die einzelnen Knoten herunter und installiert sie. 

> [!NOTE]
> Zum Anwenden von Updates, die als wichtige Softwareupdates, die standardmäßig ausgewählt sind \(Treiber aktualisiert z. B.\), Sie können einen optionalen Plug-in konfigurieren\-im Parameter. Weitere Informationen finden Sie unter [Konfigurieren der Abfragezeichenfolge für den Windows Update-Agent](#BKMK_QUERY).

### <a name="requirements"></a>Anforderungen

- Der Failovercluster und dem Remotecomputer des Updatekoordinators \(verwendet\) erfüllt die Anforderungen für clusterfähiges aktualisieren und die Konfiguration, die für die Remoteverwaltung in aufgeführten erforderlich ist [Anforderungen und Best Practices für clusterfähiges aktualisieren ](cluster-aware-updating-requirements.md).
- Lesen Sie die [Empfehlungen für die Anwendung von Microsoft-Updates](cluster-aware-updating-requirements.md#BKMK_BP_WUA), und nehmen Sie dann alle erforderlichen Änderungen an der Microsoft-Updatekonfiguration für die Failoverclusterknoten vor.
- Für optimale Ergebnisse wird empfohlen, dass Sie Best Practices Analyzer für CAU ausführen \(BPA\) um sicherzustellen, dass die Cluster- und updateumgebung ordnungsgemäß für die Anwendung von Updates über clusterfähiges aktualisieren konfiguriert sind. Weitere Informationen finden Sie unter [Testen der Updatebereitschaft für clusterfähiges Aktualisieren](cluster-aware-updating-requirements.md#BKMK_BPA).

> [!NOTE]
> Updates, die das Akzeptieren von Microsoft-Lizenzbedingungen oder andere Benutzerinteraktionen erfordern, werden ausgeschlossen und müssen manuell installiert werden.

### <a name="additional-options"></a>Zusätzliche Optionen

Optional können Sie angeben, werden die folgende Plug-Ins\-in-Argumenten zu erweitern oder beschränken den Satz von Updates, die angewendet werden, indem der Stecker\-in:
- So konfigurieren Sie die Plug &\-in anzuwendende empfohlene Updates zusätzlich zu wichtigen Updates auf jedem Knoten, in die CAU-UI auf die **zusätzliche Optionen** Seite die **bieten, die mir empfohlene updates identisch wie Ich erhalte, dass wichtige Updates** Kontrollkästchen.
<br>Konfigurieren Sie wahlweise die **'IncludeRecommendedUpdates'\='True'** anschließen\-in-Arguments.
- So konfigurieren Sie die Plug &\-in um die Typen von GDR-Updates zu filtern, die auf jedem Clusterknoten angewendet werden, geben Sie einen Windows Update-Agent Abfragezeichenfolge mit einem **QueryString** anschließen\-im Argument. Weitere Informationen finden Sie unter [Konfigurieren der Abfragezeichenfolge für den Windows Update-Agent](#BKMK_QUERY).

### <a name="BKMK_QUERY"></a>Konfigurieren der Windows Update-Agent-Abfragezeichenfolge  
Sie können konfigurieren, dass ein Plug-in\-im Argument für das standardmäßige Plug-in\-in **Microsoft.WindowsUpdatePlugin**, besteht aus einem Windows Update-Agent \(WUA\) Abfragezeichenfolge. Diese Anweisung verwendet die WUA-API, um eine oder mehrere Gruppen von Microsoft-Updates zu ermitteln, die auf Basis bestimmter Auswahlkriterien auf die einzelnen Knoten angewendet werden. Sie können mehrere Kriterien mithilfe einer logischen UND- oder ODER-Operation kombinieren. Die WUA-Abfragezeichenfolge angegeben ist, in einem Plug\-im Argument wie folgt:  
  
**QueryString\="Kriterium1\=Value1 und\/oder Kriterium2\=Value2 und\/oder..."**  
  
**Microsoft.WindowsUpdatePlugin** wählt z. B. wichtige Updates automatisch mithilfe des Standardarguments **QueryString** aus, das mit den Kriterien **IsInstalled**, **Type**, **IsHidden** und **IsAssigned** erzeugt wird:  
  
**QueryString\="IsInstalled\=0, und geben\="Software"und" IsHidden "\=0 und IsAssigned\=1"**  
  
Bei Angabe einer **QueryString** Argument dient anstelle des standardmäßigen **QueryString** für das Plug-in konfiguriert ist\-in.  
  
#### <a name="example-1"></a>Beispiel 1
  
So konfigurieren Sie eine **QueryString** Argument, das ein bestimmtes Update installiert wird, wie durch die ID *f6ce46c1\-971c\-43f9\-a2aa\-783df125f003*:  
  
**QueryString\="UpdateID\='f6ce46c1\-971c\-43f9\-a2aa\-783df125f003' and IsInstalled\=0"**  
  
> [!NOTE]  
> Im obige Beispiel gilt für das Anwenden von Softwareupdates mithilfe des Clusters\-bewusst-Assistenten aktualisieren. Wenn Sie ein bestimmtes Update durch Konfigurieren von Self-Service installieren möchten\-Optionen aktualisieren, mit die CAU-UI oder über die **hinzufügen\-CauClusterRole** oder **festgelegt\-CauClusterRole**PowerShell-Cmdlets müssen Sie den UpdateID-Wert mit zwei einzelnen formatieren\-Zeichen Zitat:  
>   
> **QueryString\="UpdateID\=''f6ce46c1\-971c\-43f9\-a2aa\-783df125f003'' and IsInstalled\=0"**  
  
#### <a name="example-2"></a>Beispiel 2
  
So konfigurieren Sie ein **QueryString**-Argument, das ausschließlich Treiber installiert  
  
**QueryString\="IsInstalled\=0, und geben\="Treiber"und" IsHidden "\=0"**  
  
Weitere Informationen zu Abfragezeichenfolgen für das standardmäßige Plug-in\-in **Microsoft.WindowsUpdatePlugin**, den Suchkriterien \(wie z. B. **IsInstalled**\), und die Syntax, die Sie in die Abfragezeichenfolgen einbeziehen können finden Sie im Abschnitt zu den Suchkriterien in der [Windows Update Agent (WUA) API-Referenz](https://go.microsoft.com/fwlink/p/?LinkId=223304).  
  
## <a name="BKMK_HFP"></a>Verwenden von Microsoft.HotfixPlugin  
Der Stecker\-in **Microsoft.HotfixPlugin** können verwendet werden, um das Anwenden von Microsoft beschränkt GDR \(LDR\) Updates \(auch Hotfixes genannt und früher als QFEsbezeichnet.\) , dass Sie zum Beheben der Probleme mit Software von Microsoft unabhängig herunterladen. Das plug-in installiert Updates aus einem Stammordner auf einer SMB-Dateifreigabe und können auch angepasst werden, um nicht anzuwenden\-Microsoft-Treiber, Firmware und BIOS-Updates.

> [!NOTE]
> Hotfixes stehen gelegentlich in zum Herunterladen von Microsoft Knowledge Base-Artikel, aber sie werden ebenfalls bereitgestellt, um Kunden auf\-Basis erforderlich.

### <a name="requirements"></a>Anforderungen

- Der Failovercluster und dem Remotecomputer des Updatekoordinators \(verwendet\) erfüllt die Anforderungen für clusterfähiges aktualisieren und die Konfiguration, die für die Remoteverwaltung in aufgeführten erforderlich ist [Anforderungen und Best Practices für clusterfähiges aktualisieren ](cluster-aware-updating-requirements.md).
- Lesen Sie hierzu [Empfehlungen zur Verwendung von Microsoft.HotfixPlugin](cluster-aware-updating-requirements.md#BKMK_BP_HF).
- Für optimale Ergebnisse wird empfohlen, dass Sie Best Practices Analyzer für CAU ausführen \(BPA\) Modell, um sicherzustellen, dass die Cluster- und updateumgebung ordnungsgemäß für die Anwendung von Updates über clusterfähiges aktualisieren konfiguriert sind. Weitere Informationen finden Sie unter [Testen der Updatebereitschaft für clusterfähiges Aktualisieren](cluster-aware-updating-requirements.md#BKMK_BPA).
- Rufen Sie die Updates vom Verleger, und kopieren Sie sie aus, oder Extrahieren Sie sie in einer Server Message Block \(SMB\) Dateifreigabe \(hotfixstammordner\) unterstützt, die mindestens SMB 2.0 und wird von allen des Clusters zugegriffen werden kann Knoten und dem Remotecomputer des Updatekoordinators \(Wenn für clusterfähiges aktualisieren, in Remotebüros verwendet wird\-Updatemodus\). Weitere Informationen finden Sie weiter unten in diesem Thema unter [Konfigurieren einer Hotfixstammordnerstruktur](#BKMK_HF_ROOT). 

    > [!NOTE]
    > Standardmäßig werden von diesem Plug-in\-in installiert Sie nur Hotfixes mit den folgenden Dateinamenerweiterungen: MSU, MSI und MSP.

- Kopieren Sie die Datei "defaulthotfixconfig.xml" \(die bereitgestellt wird, der **%SystemRoot%\\"System32"\\WindowsPowerShell\\v1. 0\\Module\\ ClusterAwareUpdating** Ordner auf einem Computer, auf dem die CAU-Tools installiert sind\) auf den hotfixstammordner, die Sie erstellt und unter dem Sie die Hotfixes extrahiert haben. Z. B. Kopieren Sie die Konfigurationsdatei  *\\ \\MyFileServer\\Hotfixes\\Stamm\\*. 

    > [!NOTE]
    > Für die Installation der meisten von Microsoft bereitgestellten Hotfixes und anderer Updates kann die standardmäßige Hotfixkonfigurationsdatei ohne Änderungen verwendet werden. Sie können die Konfigurationsdatei als erweiterte Aufgabe anpassen, wenn dies in Ihrem Szenario erforderlich ist. Die Konfigurationsdatei kann benutzerdefinierte Regeln enthalten, z. B. zum Behandeln von Hotfixdateien mit spezieller Erweiterung oder zum Definieren eines Verhaltens für bestimmte Beendigungsbedingungen. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Anpassen der Hotfixkonfigurationsdatei](#BKMK_CONFIG_FILE).

### <a name="configuration"></a>Konfiguration

Konfigurieren Sie die folgenden Einstellungen. Weitere Informationen finden Sie über die Links zu weiter unten in diesem Thema folgenden Abschnitten.
- Der Pfad zum freigegebenen Hotfixstammordner, der die anzuwendenden Updates und die Hotfixkonfigurationsdatei enthält. Sie können diesen Pfad eingeben, in die CAU-UI oder Konfigurieren der **HotfixRootFolderPath\=\<Pfad >** PowerShell Plug &\-in-Arguments. 

   > [!NOTE]
   > Sie können den hotfixstammordner als lokalen Pfad oder einen UNC-Pfad des Formulars angeben  *\\ \\ServerName\\Freigabe\\RootFolderName*. Eine Domäne\-basierend oder eigenständiger DFS-Namespace-Pfad verwendet werden kann. Allerdings der Stecker\-in Funktionen, die zugriffsüberprüfung Berechtigungen in der hotfixkonfigurationsdatei sind nicht kompatibel mit einem Pfad, den DFS-Namespace, also wenn Sie einen konfigurieren, Sie die Überprüfung auf Zugriffsberechtigungen mithilfe der CAU-UI oder durch Konfiguration deaktivieren müssen die **DisableAclChecks\='True'** anschließen\-in-Arguments.
- Einstellungen auf dem Server, der den hotfixstammordner zum Prüfen der notwendigen Berechtigungen zum Zugriff auf den Ordner, und Sicherstellen der Integrität der Daten auf das Sie über den SMB hostet freigegebenen Ordner \(SMB-Signatur oder SMB-Verschlüsselung\). Weitere Informationen finden Sie unter [Einschränken des Zugriffs auf den Hotfixstammordner](#BKMK_ACL).

### <a name="additional-options"></a>Zusätzliche Optionen

- Konfigurieren Sie optional die Plug &\-in also die SMB-Verschlüsselung wird erzwungen, wenn Daten von der hotfixdateifreigabe zugreifen. In die CAU-UI auf die **zusätzliche Optionen** Seite die **SMB-Verschlüsselung beim Zugriff auf den hotfixstammordner** aus, oder Konfigurieren der **RequireSMBEncryption\= 'True'** PowerShell Plug\-in-Arguments. 
  > [!IMPORTANT]
  > Sie müssen auf dem SMB-Server zusätzliche Konfigurationsschritte ausführen, um die SMB-Datenintegrität mithilfe der SMB-Signatur oder SMB-Verschlüsselung zu ermöglichen. Weitere Informationen finden Sie unter Schritt 4 in [Einschränken des Zugriffs auf den Hotfixstammordner](#BKMK_ACL). Wenn Sie die Option zum Erzwingen der Verwendung der SMB-Verschlüsselung auswählen und der Hotfixstammordner nicht für den Zugriff mit SMB-Verschlüsselung konfiguriert ist, tritt bei der Updateausführung ein Fehler auf.
- Deaktivieren Sie optional die Standardprüfungen auf ausreichende Berechtigungen für den Hotfixstammordner und die Hotfixkonfigurationsdatei. Wählen Sie die CAU-UI **Prüfung auf Administratorzugriff auf hotfixstammordner Stamm und Konfigurationsdatei deaktivieren**, oder konfigurieren Sie die **DisableAclChecks\='True'** anschließen\-in Argument.
- Konfigurieren (optional) die **HotfixInstallerTimeoutMinutes\= <Integer>**  Argument an, wie lange das Hotfix anschließen\-in wartet der hotfixinstallationsprozesses zurück. \(Der Standardwert ist 30 Minuten.\) Um ein Zeitlimit von zwei Stunden anzugeben, legen Sie z. B. **HotfixInstallerTimeoutMinutes\=120**.
- Konfigurieren Sie optional die **HotfixConfigFileName \= <name>**  anschließen\-im Argument, um einen Namen für die hotfixkonfigurationsdatei anzugeben, die sich im hotfixstammordner befindet. Wenn der Name nicht angegeben wird, lautet der Standardname "DefaultHotfixConfig.xml".
  
### <a name="BKMK_HF_ROOT"></a>Konfigurieren einer hotfixstammordnerstruktur

Schließen Sie den Hotfix\-in funktioniert, müssen die Hotfixes werden gespeichert in einen gut\-definierte Struktur in einer SMB-Dateifreigabe \(hotfixstammordner\), und Sie müssen konfigurieren, dass das Hotfix-Plug\-sich mit den Pfad zu der Hotfix-Stammordner mithilfe der CAU-UI oder der CAU-PowerShell-Cmdlets. Dieser Pfad wird an der Stecker übergeben\-in als die **HotfixRootFolderPath** Argument. Gemäß Ihrer Aktualisierungsanforderungen können Sie für den Hotfixstammordner eine von vielen Strukturen auswählen, wie in den folgenden Beispielen gezeigt. Dateien oder Ordner, die der Struktur nicht entsprechen, werden ignoriert.  
  
#### <a name="example-1---folder-structure-used-to-apply-hotfixes-to-all-cluster-nodes"></a>Beispiel 1: die Ordnerstruktur zum Anwenden von Hotfixes auf alle Clusterknoten
  
Um anzugeben, dass Hotfixes für alle Clusterknoten gelten, kopieren Sie sie in einen Ordner namens **CAUHotfix\_alle** unter dem hotfixstammordner. In diesem Beispiel die **HotfixRootFolderPath** anschließen\-im Argument nastaven NA hodnotu *\\ \\MyFileServer\\Hotfixes\\Stamm\\*. Die **CAUHotfix\_alle** Ordner enthält drei Updates mit den Erweiterungen MSU, MSI und MSP, die auf alle Clusterknoten angewendet werden. Die Namen der Updatedateien dienen nur zur Veranschaulichung.  
  
> [!NOTE]  
> In diesem und den folgenden Beispielen wird die Hotfixkonfigurationsdatei mit dem Standardnamen "DefaultHotfixConfig.xml" am erforderlichen Speicherort im Hotfixstammordner angezeigt.  
  
```
\\MyFileServer\Hotfixes\Root\   
   DefaultHotfixConfig.xml  
   CAUHotfix_All\   
      Update1.msu   
      Update2.msi   
      Update3.msp  
      ...  
```  
  
#### <a name="example-2---folder-structure-used-to-apply-certain-updates-only-to-a-specific-node"></a>Beispiel 2: Struktur des Ordners verwendet, um bestimmte Updates nur auf einen bestimmten Knoten angewendet
  
Um Hotfixes anzugeben, die nur auf einen bestimmten Knoten angewendet werden, verwenden Sie unter dem Hotfixstammordner einen Unterordner mit dem Namen dieses Knotens. Verwenden Sie den NetBIOS-Namen des Clusterknotens, z. B. *ContosoNode1*. Verschieben Sie dann die Updates, die nur für diesen Knoten gelten, in diesen Unterordner. Im folgenden Beispiel die **HotfixRootFolderPath** anschließen\-im Argument nastaven NA hodnotu  *\\ \\MyFileServer\\Hotfixes\\Stamm\\*. Aktualisierungen in der **CAUHotfix\_alle** Ordner wird auf allen Clusterknoten angewendet werden und *Node1\_bestimmte\_Update.msu* gelten nur für *ContosoNode1*.  
  
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
  
#### <a name="example-3---folder-structure-used-to-apply-updates-other-than-msu-msi-and-msp-files"></a>Beispiel 3: die Ordnerstruktur zum Anwenden von Updates als MSU, MSI und MSP-Dateien
  
Das Plug-In **Microsoft.HotfixPlugin** wendet standardmäßig nur Updates mit den Erweiterungen MSU, MSI oder MSP an. Bestimmte Updates können jedoch andere Erweiterungen aufweisen und somit andere Installationsbefehle erfordern. Möglicherweise müssen Sie ein Firmwareupdate mit der Erweiterung EXE auf einen Knoten in einem Cluster anwenden. Sie können den hotfixstammordner konfigurieren, mit einem Unterordner, der eine bestimmte, nicht angibt\-Standardtyp für die Updates installiert werden soll. Sie müssen auch eine entsprechende Ordnerinstallationsregel konfigurieren, die den Installationsbefehl im `<FolderRules>` -Element in der XML-Datei der Hotfixkonfiguration angibt.  
  
Im folgenden Beispiel die **HotfixRootFolderPath** anschließen\-im Argument nastaven NA hodnotu  *\\ \\MyFileServer\\Hotfixes\\Stamm\\*. Es werden verschiedene Updates auf alle Clusterknoten angewendet. Zusätzlich wird das Firmwareupdate *SpecialHotfix1.exe* mithilfe von *FolderRule1* auf *ContosoNode1* angewendet. Weitere Informationen zum Konfigurieren von *ContosoNode1* in der Hotfixkonfigurationsdatei finden Sie weiter unten in diesem Abschnitt unter [Anpassen der Hotfixkonfigurationsdatei](#BKMK_CONFIG_FILE) .  
  
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
Die Hotfixkonfigurationsdatei steuert, wie bestimmte Hotfixtypen von **Microsoft.HotfixPlugin** in einem Failovercluster installiert werden. Das XML-Schema für die Konfigurationsdatei wird in der Datei "HotfixConfigSchema.xsd" definiert, die sich im folgenden Ordner auf einem Computer befindet, auf dem die Tools für clusterfähiges Aktualisieren installiert sind:  
  
**%SystemRoot%\\"System32"\\WindowsPowerShell\\v1. 0\\Module\\ClusterAwareUpdating-Ordner**  
  
Kopieren Sie die Beispielkonfigurationsdatei "DefaultHotfixConfig.xml" aus diesem Speicherort in den Hotfixstammordner, und nehmen Sie die entsprechenden Änderungen für Ihr Szenario vor, um die Hotfixkonfigurationsdatei anzupassen:  
  
> [!IMPORTANT]  
> Für die Anwendung der meisten von Microsoft bereitgestellten Hotfixes und anderer Updates kann die standardmäßige Hotfixkonfigurationsdatei ohne Änderungen verwendet werden. Die Anpassung der Hotfixkonfigurationsdatei zählt nur in fortgeschrittenen Verwendungsszenarios zu den erforderlichen Aufgaben.  
  
Standardmäßig definiert die XML-Datei der Hotfixkonfiguration die Installationsregeln und Beendigungsbedingungen für die folgenden beiden Kategorien von Hotfixes:  
  
-   Der Hotfixdateien mit Erweiterungen, die der Stecker\-in können in der Standardeinstellung installieren \(MSU, MSI und MSP-Dateien\).  
  
    Diese sind als `<ExtensionRules>`-Elemente im `<DefaultRules>`-Element definiert. Für jeden standardmäßig unterstützten Dateityp gibt es ein `<Extension>` -Element. Die allgemeine XML-Struktur sieht wie folgt aus:  
  
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
  
    Wenn Sie bestimmte Updatetypen auf alle Clusterknoten in der Umgebung anwenden müssen, können Sie weitere `<Extension>` -Elemente definieren.  
  
-   Hotfix oder andere Updatedateien, die nicht MSI-, MSU- oder MSP-Dateien, z. B. nicht\-Microsoft-Treiber, Firmware und BIOS-Updates.  
  
    Jeder nicht\-Standarddateityp als konfiguriert ist, eine `<Folder>` Element in der `<FolderRules>` Element. Das Namensattribut des `<Folder>` -Elements muss mit dem Namen eines Ordners im Hotfixstammordner übereinstimmen, der Updates vom entsprechenden Typ enthalten wird. Der Ordner kann sein, der **CAUHotfix\_alle** Ordner oder in einem Knoten\-bestimmten Ordner. Wenn *FolderRule1* z. B. im Hotfixstammordner konfiguriert ist, konfigurieren Sie das folgende Element in der XML-Datei, damit es eine Installationsvorlage und Beendigungsbedingungen für die Updates in diesem Ordner definiert:  
  
    ```xml  
    <FolderRules>  
          <Folder name="FolderRule1">  
            <!-- Template and ExitConditions elements for installation of updates in FolderRule1 follow -->  
             ...  
          </Folder>  
          ...  
    </FolderRules>  
    ```  
  
In der folgenden Tabelle werden die `<Template>` -Attribute und mögliche `<ExitConditions>` -Unterelemente beschrieben.  
  
|`<Template>`-Attribut|Beschreibung|  
|--------------------------|---------------|  
|`path`|Der vollständige Pfad zum Installationsprogramm für den Dateityp, der im `<Extension name>` -Attribut definiert ist.<br /><br />Verwenden Sie `$update$`, um den Pfad zu einer Updatedatei in der Hotfix-Stammordnerstruktur anzugeben.|  
|`parameters`|Eine Zeichenfolge erforderlicher und optionaler Parameter für das Programm, das in `path`angegeben ist.<br /><br />Verwenden Sie `$update$`, um einen Parameter anzugeben, der dem Pfad zu einer Updatedatei in der Hotfix-Stammordnerstruktur entspricht.|  
  
|`<ExitConditions>`-Unterelement|Beschreibung|  
|---------------------------------|---------------|  
|`<Success>`|Definiert mindestens einen Beendigungscode, der auf die erfolgreiche Ausführung des angegebenen Updates hinweist. Dies ist ein erforderliches Unterelement.|  
|`<Success_RebootRequired>`|Definiert optional mindestens einen Beendigungscode, der darauf hinweist, dass das Update erfolgreich ausgeführt wurde und der Knoten neu gestartet werden muss. <br>**Hinweis**: Optional kann das `<Folder>`-Element das `alwaysReboot`-Attribut enthalten. Wenn dieses Attribut festgelegt ist, zeigt es an, dass wenn ein von dieser Regel installiertes Hotfix einen der Beendigungscodes zurückgibt, die in `<Success>`definiert sind, dieser als `<Success_RebootRequired>` -Beendigungsbedingung interpretiert wird.|  
|`<Fail_RebootRequired>`|Definiert optional mindestens einen Beendigungscode, der darauf hinweist, dass das Update nicht erfolgreich ausgeführt wurde und der Knoten neu gestartet werden muss.|  
|`<AlreadyInstalled>`|Definiert optional mindestens einen Beendigungscode, der darauf hinweist, dass das angegebene Update nicht angewendet wurde, da es bereits installiert ist.|  
|`<NotApplicable>`|Definiert optional mindestens einen Beendigungscode, der darauf hinweist, dass das angegebene Update nicht angewendet wurde, da es nicht für den Clusterknoten gilt.|  
  
> [!IMPORTANT]  
> Ein Beendigungscode, der in `<ExitConditions>` nicht explizit definiert ist, wird bei einem Fehler des Updates interpretiert und der Knoten wird nicht neu gestartet.  
  
### <a name="BKMK_ACL"></a>Beschränken des Zugriffs auf den hotfixstammordner  
Sie müssen verschiedene Schritte ausführen, um den SMB-Dateiserver und die -Dateifreigabe so zu konfigurieren, dass sie den Schutz der Dateien im Hotfixstammordner nur für den Zugriff im Kontext von **Microsoft.HotfixPlugin**unterstützen. Diese Schritte aktivieren verschiedene Features, die dabei helfen, mögliche Manipulationen an den Hotfixdateien zu verhindern, die möglicherweise den Failovercluster gefährden können.  
  
Die allgemeinen Schritte sehen wie folgt aus:  
  
1.  Identifizieren des Benutzerkontos, das für Updateausführungen verwendet wird, mithilfe des Steckers\-in  
  
2.  Konfigurieren dieses Benutzerkontos in den erforderlichen Gruppen auf einem SMB-Dateiserver  
  
3.  Konfigurieren der Berechtigungen für den Zugriff auf den Hotfixstammordner  
  
4.  Konfigurieren der Einstellungen für die SMB-Datenintegrität  
  
5.  Aktivieren der Windows-Firewall-Regel auf dem SMB-Server  
  
#### <a name="step-1-identify-the-user-account-that-is-used-for-updating-runs-by-using-the-hotfix-plug-in"></a>Schritt 1 Identifizieren des Benutzerkontos, das für Updateausführungen verwendet wird, mithilfe des Hotfix-Steckers\-in
  
Das Konto, das im Selbstaktualisierungsmodus, zum Prüfen der Sicherheitseinstellungen verwendet wird während einer Updateausführung mithilfe **Microsoft.HotfixPlugin** abhängig, ob für clusterfähiges aktualisieren, in Remotebüros verwendet wird\-aktualisieren Modus oder im Self-Service\-Updatemodus an, wie Die folgende:  
  
-   **Remote\-Updatemodus** das Konto, das über Administratorrechte, auf dem Cluster verfügt eine Vorschau anzeigen und Anwenden von Updates.  
  
-   **Self\-Updatemodus** der Namen des virtuellen Computerobjekts, das in Active Directory, für die CAU konfiguriert ist-Clusterrolle. Dies ist entweder der Name eines vorab bereitgestellten virtuellen Computerobjekts in Active Directory für die Clusterrolle für clusterfähiges Aktualisieren oder der Name, der von der Clusterrolle für clusterfähiges Aktualisieren generiert wird. Führen Sie zum Abrufen des Namens, wenn sie von CAU generiert werden, die **erhalten\-CauClusterRole** CAU-PowerShell-Cmdlet. In der Ausgabe ist **ResourceGroupName** der Name des generierten virtuellen Computerobjektkontos.  
  
#### <a name="step-2-configure-this-user-account-in-the-necessary-groups-on-an-smb-file-server"></a>Schritt 2 Konfigurieren dieses Benutzerkontos in den erforderlichen Gruppen auf einem SMB-Dateiserver
  
> [!IMPORTANT]  
> Sie müssen das für die Updateausführungen verwendete Konto als lokales Administratorkonto auf dem SMB-Server hinzufügen. Wenn dies aufgrund der Sicherheitsrichtlinien in Ihrer Organisation nicht zulässig ist, konfigurieren Sie dieses Konto auf dem SMB-Server mit den erforderlichen Berechtigungen, indem Sie das folgende Verfahren durchführen.  
  
##### <a name="to-configure-a-user-account-on-the-smb-server"></a>So konfigurieren Sie ein Benutzerkonto auf dem SMB-Server  
  
1.  Fügen Sie das für Updateausführungen verwendete Konto zur Gruppe "Distributed COM-Benutzer" sowie zu einer der folgenden Gruppen hinzu: Hauptbenutzer, Servervorgang oder Druck-Operator.  
  
2.  Starten Sie die WMI-Verwaltungskonsole auf dem SMB-Server, um die erforderlichen WMI-Berechtigungen für das Konto zu aktivieren. Starten Sie PowerShell, und geben Sie den folgenden Befehl aus:  
  
    ```  
    wmimgmt.msc  
    ```  
  
3.  Direkt in der Konsolenstruktur\-klicken Sie auf **WMI-Steuerung \(lokalen\)**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie auf **Sicherheit**, und erweitern Sie dann **Stamm**.  
  
5.  Klicken Sie auf **CIMV2**und dann auf **Sicherheit**.  
  
6.  Fügen Sie das für Updateausführungen verwendete Konto zur Liste **Gruppen- oder Benutzernamen** hinzu.  
  
7.  Erteilen Sie dem für Updateausführungen verwendeten Konto die Berechtigungen **Methoden ausführen** und **Remoteaktivierung** .  
  
#### <a name="step-3-configure-permissions-to-access-the-hotfix-root-folder"></a>Schritt 3 Konfigurieren der Berechtigungen für den Zugriff auf den Hotfixstammordner
  
Standardmäßig, wenn Sie versuchen, Updates zu installieren, der Hotfix anschließen\-in überprüft die Konfiguration der NTFS-Dateisystemberechtigungen für den Zugriff auf den hotfixstammordner. Wenn eine Updateausführung mit dem Hotfix-Plug nicht ordnungsgemäß, von die Berechtigungen für den Ordnerzugriff konfiguriert sind\-in schlägt möglicherweise fehl.  
  
Bei Verwendung die Standardkonfiguration der Hotfix-Stecker\-, stellen Sie sicher, dass die Berechtigungen für den Ordnerzugriff den folgenden Anforderungen erfüllen.  
  
-   Die Gruppe "Benutzer" verfügt über die Berechtigung "Lesen".  
  
-   Wenn der Stecker\-in Updates mit der Erweiterung .exe anwenden, die Gruppe der Benutzer verfügt über die Execute-Berechtigung.  
  
-   Nur für bestimmte Sicherheitsprinzipale dürfen \(sind jedoch nicht erforderlich\) schreiben oder die Berechtigung ändern. Die zulässigen Prinzipale sind die Gruppe der lokalen Administratoren, SYSTEM, ERSTELLER-BESITZER und TrustedInstaller. Anderen Konten oder Gruppen ist es nicht gestattet, die Berechtigung "Schreiben" oder "Ändern" für den Hotfixstammordner zu verwenden.  
  
Sie können optional deaktivieren, die oben aufgeführten Überprüfungen, die der Stecker\-führt Sie in der Standardeinstellung. Hierzu stehen Ihnen zwei Möglichkeiten zur Verfügung.  
  
-   Wenn Sie die CAU-PowerShell-Cmdlets verwenden, konfigurieren Sie die **DisableAclChecks\='True'** -Argument in der **CauPluginArguments** -Parameter für das Hotfix-Plug\-in.  
  
-   Wenn Sie die Benutzeroberfläche für clusterfähiges Aktualisieren verwenden, wählen Sie die Option **Prüfung auf Administratorzugriff auf Hotfixstammordner und Konfigurationsdatei deaktivieren** auf der Seite **Weitere Updateoptionen** aus, die zum Konfigurieren der Optionen von Updateausführungen verwendet wird.  
  
Es wird jedoch in vielen Umgebungen als bewährte Methode empfohlen, dass Sie diese Prüfungen mithilfe der Standardkonfiguration erzwingen.  
  
#### <a name="step-4-configure-settings-for-smb-data-integrity"></a>Schritt 4 Konfigurieren der Einstellungen für die SMB-Datenintegrität
  
Um die Integrität der Daten in die Verbindungen zwischen den Clusterknoten und SMB-Dateifreigabe zu überprüfen, schließen Sie der Hotfix\-in erfordert, dass Sie die Einstellungen für die SMB-Dateifreigabe für SMB-Signatur oder SMB-Verschlüsselung aktivieren. SMB-Verschlüsselung, die erhöhte Sicherheit und eine bessere Leistung in vielen Umgebungen bietet, ist ab Windows Server 2012 unterstützt. Sie können eine oder beide Einstellungen wie folgt aktivieren:  
  
-   Informationen zum Aktivieren der SMB-Signatur finden Sie unter dem Verfahren in der Microsoft Knowledge Base in [Artikel 887429](https://support.microsoft.com/kb/887429) .  
  
-   Führen Sie das folgende PowerShell-Cmdlet zum Aktivieren der SMB-Verschlüsselung für den freigegebenen SMB-Ordner auf dem SMB-Server:  
  
    ```PowerShell  
    Set-SmbShare <ShareName> -EncryptData $true  
    ```  
  
    Dabei gibt <*ShareName*> den Namen des freigegebenen SMB-Ordners an.  
  
Um die Verwendung der SMB-Verschlüsselung der Verbindungen zum SMB-Server zu erzwingen, wählen Sie optional die **SMB-Verschlüsselung beim Zugriff auf den hotfixstammordner** aus, in die CAU-UI, oder Konfigurieren der **RequireSMBEncryption \='True'** anschließen\-im Argument mit den CAU-PowerShell-Cmdlets.  
  
> [!IMPORTANT]  
> Wenn Sie die Option zum Erzwingen der Verwendung der SMB-Verschlüsselung auswählen und der Hotfixstammordner nicht für Verbindungen konfiguriert ist, die die SMB-Verschlüsselung verwenden, tritt bei der Updateausführung ein Fehler auf.  
  
#### <a name="step-5-enable-a-windows-firewall-rule-on-the-smb-server"></a>Schritt 5 Aktivieren der Windows-Firewall-Regel auf dem SMB-Server
  
Sie müssen die aktivieren die **Dateiserver-Remoteverwaltung \(SMB\-in\)**  Regel in der Windows-Firewall auf dem SMB-Dateiserver. Dies ist standardmäßig in Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 aktiviert.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Übersicht über das clusterfähige aktualisieren](cluster-aware-updating.md)
  
-   [Clusterfähige Aktualisierung Windows PowerShell-Cmdlets](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating)  
  
-   [Clusterfähiges aktualisieren die Referenz zu Plug-Ins](https://msdn.microsoft.com/library/hh418084.aspx)  
  
