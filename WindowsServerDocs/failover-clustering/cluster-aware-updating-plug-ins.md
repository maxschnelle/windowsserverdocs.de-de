---
ms.assetid: d44d4430-41e2-483a-9685-92610cdef32a
title: Funktionsweise von Plug-Ins für Cluster fähiges aktualisieren
ms.topic: article
ms.prod: windows-server-threshold
manager: dongill
ms.author: jgerend
author: JasonGerend
ms.date: 04/28/2017
ms.technology: storage-failover-clustering
description: Verwenden von Plug-ins zum Koordinieren von Updates bei Verwendung des Cluster fähigen Aktualisierens in Windows Server zum Installieren von Updates auf einem Cluster.
ms.openlocfilehash: bd31a6056376b04fcb5a4a941b81a363548a2209
ms.sourcegitcommit: 6f968368c12b9dd699c197afb3a3d13c2211f85b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/26/2019
ms.locfileid: "68544510"
---
# <a name="how-cluster-aware-updating-plug-ins-work"></a>Funktionsweise von Plug-Ins für Cluster fähiges aktualisieren

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

[Cluster fähiges aktualisieren](cluster-aware-updating.md) (Cau) verwendet Plug-ins, um die Installation von Updates auf Knoten in einem Failovercluster zu koordinieren. Dieses Thema enthält Informationen zur Verwendung der integrierten\-Plug\--ins für Cluster fähiges aktualisieren oder\-anderer Plug-ins, die Sie für Cau installieren.

## <a name="BKMK_INSTALL"></a>Installieren eines Plug\--ins  
Ein anderes\-Plug-in als die Standard\--Plug-ins, die mit \(Cau **Microsoft. windowsupdateplugin** und **Microsoft. hotfixplugin** \) installiert werden, müssen separat installiert werden. Wenn Cau im selbst\-Aktualisierungs Modus verwendet wird, muss das Plug\--in auf allen Cluster Knoten installiert werden. Wenn das Cluster fähige aktualisieren im Remote\-Aktualisierungs Modus verwendet wird\-, muss das Plug-in auf dem Remote Computer für den Update Koordinator installiert sein. Bei einem\-Plug-in, das Sie installieren, sind möglicherweise zusätzliche Installationsanforderungen auf den einzelnen Knoten erforderlich.  
  
Befolgen Sie zum Installieren\-eines Plug-ins die Anweisungen des Plug\--in-Herausgebers. Wenn Sie ein Plug\--in mit Cau manuell registrieren möchten, führen Sie das [Register-cauplugin-](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin) Cmdlet auf\-jedem Computer aus, auf dem das Plug-in installiert ist.  
  
## <a name="specify-a-plug-in-and-plug-in-arguments"></a>Plug\--in-und Plug\--in-Argumente angeben  
  
### <a name="specify-a-cau-plug-in"></a>Angeben eines Plug\--ins für Cluster fähiges aktualisieren

In der Benutzeroberfläche für Cluster fähiges aktualisieren wählen Sie\-ein Plug-in\-aus einer Dropdown Liste\-der verfügbaren Plug-ins aus, wenn Sie mit Cau die folgenden Aktionen ausführen:  
  
-   Anwenden von Updates auf Cluster  
  
-   Updatevorschau für Cluster  
  
-   Konfigurieren von selbst\-Aktualisierungs Optionen für Cluster  
  
Standardmäßig wählt Cau den Plug\--in **Microsoft. windowsupdateplugin**aus. Sie können jedoch ein beliebiges Plug\--in angeben, das in Cau installiert und registriert ist.

> [!TIP]  
> Auf der Benutzeroberfläche für Cluster fähiges aktualisieren können Sie nur ein einzelnes\-Plug-in für Cluster fähiges aktualisieren angeben, das für die Vorschauversion oder die Anwendung von Updates während einer Update Laufzeit verwendet werden soll. Mithilfe der PowerShell-Cmdlets für Cluster fähiges aktualisieren können Sie ein oder mehrere Plug\--ins angeben. Wenn Sie mehrere Arten von Updates auf dem Cluster installieren müssen, ist es in der Regel effizienter, mehrere Plug\--ins in einer Update Laufzeit anzugeben, anstatt für jedes Plug\--in eine separate Update-Laufzeit zu verwenden. Dadurch sind z. B. meist weniger Knotenneustarts erforderlich.

Mithilfe der in der folgenden Tabelle aufgeführten PowerShell-Cmdlets für Cluster fähiges aktualisieren können Sie ein oder mehrere Plug\--ins für eine Update-oder Scanvorgang angeben, indem Sie den **– caupluginname** -Parameter übergeben. Sie können mehrere Plug\--in-Namen angeben, indem Sie Sie durch Kommas trennen. Wenn Sie mehrere\-Plug-ins angeben, können Sie auch steuern, wie sich die Plug\--ins während einer  **\-**  **\-** Update Ausführung gegenseitig beeinflussen, indem Sie runpluginsseridal, stoponpluginfailure, angeben. und **– separaterestarts** -Parameter. Weitere Informationen zur Verwendung mehrerer Plug\--ins finden Sie unter den Links, die für die Cmdlet-Dokumentation in der folgenden Tabelle bereitgestellt werden.  
  
|Cmdlet|Beschreibung|  
|----------|---------------|  
|[Add-cauclusterrole](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/add-cauclusterrole)|Fügt die Cluster Rolle für Cluster fähiges aktualisieren hinzu, die\-dem angegebenen Cluster die selbst Aktualisierungs Funktion bereitstellt.|  
|[Aufrufen: caurun](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/invoke-caurun)|Prüft Clusterknoten auf geeignete Updates und installiert diese Updates über eine Updateausführung auf dem angegebenen Cluster.|  
|[Aufrufen: kauscan](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/invoke-causcan)|Prüft Clusterknoten auf geeignete Updates und gibt eine Liste des ersten Updatesatzes zurück, der auf jeden Knoten des angegebenen Clusters angewendet werden würde.|  
|[Set-cauclusterrole](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/set-cauclusterrole)|Legt Konfigurationseigenschaften für die Clusterrolle für clusterfähiges Aktualisieren auf dem angegebenen Cluster fest.|  
  
Wenn Sie mithilfe dieser Cmdlets keinen Plug\--in-Parameter für Cluster fähiges aktualisieren angeben, ist der Standardwert\-der Plug-in **Microsoft. windowsupdateplugin**.  
  
### <a name="specify-cau-plug-in-arguments"></a>Cau-Plug\--in-Argumente angeben  
Wenn Sie die Optionen\) für die Aktualisierungs Laufzeit konfigurieren, können Sie ein oder mehrere *Name\=-Wert* -Paare \(angeben\-, die für das ausgewählte Plug-in verwendet werden sollen. Auf der Benutzeroberfläche für clusterfähiges Aktualisieren können Sie z. B. wie folgt mehrere Argumente angeben:  
  
**Name1\=value1; Name2\=Value2; Name3\=Wert3**  
  
Diese *Name\=-Wert* -Paare müssen für das von\-Ihnen angegebene Plug-in sinnvoll sein. Für einige Plug\--ins sind die Argumente optional.  
  
Die Syntax der Plug\--in-Argumente für Cau befolgt diese allgemeinen Regeln:  
  
-   Mehrere *Name\=-Wert* -Paare werden durch Semikolons getrennt.  
  
-   Ein Leerzeichen enthaltender Wert wird in Anführungszeichen gestellt. Beispiel: **Name1\="Wert mit Leerzeichen"** .  
  
-   Die genaue Syntax des *Werts* hängt vom Plug\--in ab.  
  
Zum Angeben von\-Plug-in-Argumenten mithilfe der Cau-PowerShell-Cmdlets, die den Parameter **– caupluginparameters** unterstützen, übergeben Sie einen Parameter in der Form:  
  
**\-Caupluginarguments @ {Name1\=value1; Name2\=Value2; Name3\=Wert3}**  
  
Sie können auch eine vordefinierte PowerShell-Hash Tabelle verwenden. Um Plug\--in-Argumente für mehr als ein\-Plug-in anzugeben, übergeben Sie mehrere Hash Tabellen mit Argumenten, die durch Kommas getrennt sind. Übergeben Sie die\-Plug-in-Argumente\-in der Plug-in-Reihenfolge, die in **caupluginname**angegeben ist.  
  
### <a name="specify-optional-plug-in-arguments"></a>Angeben Optionaler\-Plug-in-Argumente  
Die Plug\--ins, die von \(Cau **Microsoft. windowsupdateplugin** und **Microsoft. hotfixplugin** \) installiert werden, bieten zusätzliche Optionen, die Sie auswählen können. Diese werden auf der Benutzeroberfläche für Cluster fähiges aktualisieren auf der Seite **zusätzliche Optionen** angezeigt, nachdem Sie die Optionen für\-die Update Ausführung für das Plug-in konfiguriert haben. Wenn Sie die PowerShell-Cmdlets für Cluster fähiges aktualisieren verwenden, werden diese Optionen als optionale\-Plug-in-Argumente konfiguriert. Weitere Informationen finden Sie unter [Verwenden von "Microsoft.WindowsUpdatePlugin"](#BKMK_WUP) und [Verwenden von "Microsoft.HotfixPlugin"](#BKMK_HFP) weiter unten in diesem Thema.  
  
## <a name="manage-plug-ins-using-windows-powershell-cmdlets"></a>Verwalten von\-Plug-Ins mithilfe von Windows PowerShell-Cmdlets  
  
|Cmdlet|Beschreibung|  
|----------|---------------|  
|[Get-cauplugin](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/get-cauplugin)|Ruft Informationen zu einem oder mehreren Software Update-Plug\--ins ab, die auf dem lokalen Computer registriert sind.|  
|[Register-cauplugin]((https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/register-cauplugin))|Registriert ein Plug\--in für Cau-Software Updates auf dem lokalen Computer.|  
|[Unregister-cauplugin](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/unregister-cauplugin)|Entfernt ein Software Update-\-Plug-in aus der Liste\-der Plug-ins, die von Cau verwendet werden können. **Hinweis**: Die Registrierung\-der Plug-ins, die mit \(Cau **Microsoft. windowsupdateplugin** und **Microsoft. hotfixplugin** \) installiert werden, kann nicht aufgehoben werden.|  
  
## <a name="BKMK_WUP"></a>Verwenden von "Microsoft. windowsupdateplugin"  

Das Standard-\-Plug-in für Cau, **Microsoft. windowsupdateplugin**, führt die folgenden Aktionen aus:
- Das Plug-In steht in Kontakt mit dem Windows Update-Agent auf den einzelnen Knoten des Failoverclusters, um Updates für die Microsoft-Produkte anzuwenden, die auf den einzelnen Knoten ausgeführt werden.
- Installiert Cluster Updates direkt von Windows Update oder Microsoft Update oder von einem\-lokalen Windows Server Update Services \(WSUS\) -Server.
- Installiert nur die ausgewählten, allgemeinen \(\) Updates der releasereleaseversion. Standardmäßig wendet das Plug\--in nur wichtige Software Updates an. Es ist keine Konfiguration erforderlich. Die Standardkonfiguration lädt wichtige Updates von allgemeinen Vertriebsversionen auf die einzelnen Knoten herunter und installiert sie. 

> [!NOTE]
> Wenn Sie andere Updates als die wichtigen Software Updates anwenden möchten, die Standard \(mäßig ausgewählt werden, z\). b. Treiber Updates, können\-Sie einen optionalen Plug-in-Parameter konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren der Abfragezeichenfolge für den Windows Update-Agent](#BKMK_QUERY).

### <a name="requirements"></a>Anforderungen

- Der Failovercluster und der Remote Update \(Coordinator-\) Computer müssen die Anforderungen für Cau und die Konfiguration erfüllen, die für die Remote Verwaltung in den [Anforderungen und bewährten Methoden für Cau](cluster-aware-updating-requirements.md)erforderlich ist.
- Lesen Sie die [Empfehlungen für die Anwendung von Microsoft-Updates](cluster-aware-updating-requirements.md#BKMK_BP_WUA), und nehmen Sie dann alle erforderlichen Änderungen an der Microsoft-Updatekonfiguration für die Failoverclusterknoten vor.
- Um optimale Ergebnisse zu erzielen, wird empfohlen, dass Sie das Cluster \(fähige aktualisieren\) (Cau Best Practices Analyzer BPA) ausführen, um sicherzustellen, dass die Cluster-und Update Umgebung ordnungsgemäß für die Anwendung von Updates über Cau Weitere Informationen finden Sie unter [Testen der Updatebereitschaft für clusterfähiges Aktualisieren](cluster-aware-updating-requirements.md#BKMK_BPA).

> [!NOTE]
> Updates, die das Akzeptieren von Microsoft-Lizenzbedingungen oder andere Benutzerinteraktionen erfordern, werden ausgeschlossen und müssen manuell installiert werden.

### <a name="additional-options"></a>Zusätzliche Optionen

Optional können Sie die folgenden Plug\--in-Argumente angeben, um die vom Plug\--in angewendeten Updates zu vergrößern oder einzuschränken:
- Um das Plug\--in so zu konfigurieren, dass zusätzlich zu wichtigen Updates auf den einzelnen Knoten Empfohlene Updates angewendet werden, wählen Sie auf der Benutzeroberfläche für Cluster fähiges aktualisieren auf der Seite **zusätzliche Optionen** die **empfohlenen Updates auf die gleiche Weise aus wie wichtige Updates** . Kontrollkästchen.
<br>Alternativ können Sie das Plug\--in-Argument **' includerecommendedupdates '\=(true** ) konfigurieren.
- Um das Plug\--in so zu konfigurieren, dass die Typen von DDR-Updates gefiltert werden, die auf die einzelnen Cluster Knoten angewendet werden, geben Sie eine Abfrage\-Zeichenfolge für den Windows Update-Agent mit einem **QueryString** - Weitere Informationen finden Sie unter [Konfigurieren der Abfragezeichenfolge für den Windows Update-Agent](#BKMK_QUERY).

### <a name="BKMK_QUERY"></a>Konfigurieren der Abfrage Zeichenfolge für Windows Update-Agent  
Sie können ein Plug\--in-Argument für das Standard-Plug\--in, **Microsoft. windowsupdateplugin**, konfigurieren, das \(aus einer\) Abfrage Zeichenfolge für den Windows Update-Agent WUA besteht. Diese Anweisung verwendet die WUA-API, um eine oder mehrere Gruppen von Microsoft-Updates zu ermitteln, die auf Basis bestimmter Auswahlkriterien auf die einzelnen Knoten angewendet werden. Sie können mehrere Kriterien mithilfe einer logischen UND- oder ODER-Operation kombinieren. Die WUA-Abfrage Zeichenfolge wird wie\-folgt in einem Plug-in-Argument angegeben:  
  
**QueryString\="Kriterium1\=value1 and\/or Criterion2\=Value2 and\/or..."**  
  
**Microsoft.WindowsUpdatePlugin** wählt z. B. wichtige Updates automatisch mithilfe des Standardarguments **QueryString** aus, das mit den Kriterien **IsInstalled**, **Type**, **IsHidden** und **IsAssigned** erzeugt wird:  
  
**QueryString\="isinstemmt\=0 und\=Type ' Software ' and IsHidden\=0 and isassigned\=1"**  
  
Wenn Sie ein **QueryString** -Argument angeben, wird es anstelle des standardmäßigen **QueryString** -Arguments verwendet, das für das\-Plug-in konfiguriert ist.  
  
#### <a name="example-1"></a>Beispiel 1
  
So konfigurieren Sie **ein QueryString** -Argument, das ein bestimmtes Update installiert, gemäß ID *\-f6ce46c1\-\-971c 43f9 a2aa\-783df125f003*:  
  
**QueryString\="UpdateId\=' f6ce46c1\-971c\-43F 9\-a2aa\-783df125f 003 ' und isinstemstem0\="**  
  
> [!NOTE]  
> Das vorherige Beispiel gilt für die Anwendung von Updates mithilfe des Assistenten\-zum Aktualisieren von Cluster fähigen Updates. Wenn Sie ein bestimmtes Update durch Konfigurieren von selbst\-Aktualisierungs Optionen über die Benutzeroberfläche für Cluster fähiges aktualisieren oder über das PowerShell-Cmdlet " **Add\-cauclusterrole** " oder " **Set\-cauclusterrole**" installieren möchten, müssen Sie das Cmdlet UpdateId-Wert mit zwei\-einfachen Anführungszeichen:  
>   
> **QueryString\="UpdateId\=" "f6ce46c1\-971c\-43F 9\-a2aa\-783df125-ID" "und isinstemstemter\=0"**  
  
#### <a name="example-2"></a>Beispiel 2
  
So konfigurieren Sie ein **QueryString**-Argument, das ausschließlich Treiber installiert  
  
**QueryString\="isinstemmt\=0 und\=Typ" Driver "und IsHidden\=0"**  
  
Weitere Informationen zu Abfrage Zeichenfolgen für das Standard\--Plug-in, **Microsoft. windowsupdateplugin**, \(zu den Suchkriterien, wie z. b. **isindefault**\), und zur Syntax, die Sie in die Abfrage einschließen können. zu Zeichen folgen finden Sie im Abschnitt zu den Suchkriterien in der API-Referenz für den [Windows Update-Agent (WUA)](https://go.microsoft.com/fwlink/p/?LinkId=223304).  
  
## <a name="BKMK_HFP"></a>Verwenden von Microsoft. hotfixplugin  
Mit dem\-Plug-in " **Microsoft. hotfixplugin** " können Microsoft Limited Distribution Release \(-LDR \(\) -Updates angewendet werden, die auch als Hotfixes\) bezeichnet werden und früher als QFEs bezeichnet wurden. Download unabhängig, um bestimmte Probleme mit Microsoft-Software zu beheben. Das Plug-in installiert Updates aus einem Stamm Ordner auf einer SMB-Dateifreigabe und kann auch so angepasst werden,\-dass Sie nicht von Microsoft stammenden Treiber, Firmware und BIOS-Updates anwenden.

> [!NOTE]
> In Knowledge Base-Artikeln können Hotfixes manchmal von Microsoft heruntergeladen werden, Sie werden jedoch auch nach\-Bedarf für Kunden bereitgestellt.

### <a name="requirements"></a>Anforderungen

- Der Failovercluster und der Remote Update \(Coordinator-\) Computer müssen die Anforderungen für Cau und die Konfiguration erfüllen, die für die Remote Verwaltung in den [Anforderungen und bewährten Methoden für Cau](cluster-aware-updating-requirements.md)erforderlich ist.
- Lesen Sie hierzu [Empfehlungen zur Verwendung von Microsoft.HotfixPlugin](cluster-aware-updating-requirements.md#BKMK_BP_HF).
- Um optimale Ergebnisse zu erzielen, empfiehlt es sich, das BPA \(\) -Modell von Cau Best Practices Analyzer auszuführen, um sicherzustellen, dass die Cluster-und Update Umgebung ordnungsgemäß für die Anwendung von Updates mithilfe von Cau konfiguriert sind. Weitere Informationen finden Sie unter [Testen der Updatebereitschaft für clusterfähiges Aktualisieren](cluster-aware-updating-requirements.md#BKMK_BPA).
- Rufen Sie die Updates vom Verleger ab, kopieren Sie Sie, oder extrahieren Sie Sie auf einen \(SMB\) -Datei \(Freigabe-hotfixstamm Ordner\) , der mindestens SMB 2,0 unterstützt und auf den alle Cluster zugreifen können. Knoten und der Remote Update Koordinator- \(Computer, wenn das Cluster fähige aktualisieren\-im Remote\)Aktualisierungs Modus verwendet wird. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Konfigurieren einer Hotfixstammordnerstruktur](#BKMK_HF_ROOT). 

    > [!NOTE]
    > Standardmäßig werden von diesem\-Plug-in nur Hotfixes mit den folgenden Dateinamen Erweiterungen installiert: MSU, MSI und MSP.

- Kopieren Sie die \(Datei "defaulthotfixconfig. xml", die im Ordner " **%\\SystemRoot% System32\\\\WindowsPowerShell\\\\v 1.0 modules clusterawareupdating** " bereitgestellt wird. auf einem Computer, auf dem die Cau-\) Tools in dem hotfixstamm Ordner installiert werden, den Sie erstellt haben und in dem Sie die Hotfixes extrahiert haben. Kopieren Sie die Konfigurationsdatei z. b. in  *\\ \\den\\Ordner myfileserver\\Hotfixes root\\* . 

    > [!NOTE]
    > Für die Installation der meisten von Microsoft bereitgestellten Hotfixes und anderer Updates kann die standardmäßige Hotfixkonfigurationsdatei ohne Änderungen verwendet werden. Sie können die Konfigurationsdatei als erweiterte Aufgabe anpassen, wenn dies in Ihrem Szenario erforderlich ist. Die Konfigurationsdatei kann benutzerdefinierte Regeln enthalten, z. B. zum Behandeln von Hotfixdateien mit spezieller Erweiterung oder zum Definieren eines Verhaltens für bestimmte Beendigungsbedingungen. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Anpassen der Hotfixkonfigurationsdatei](#BKMK_CONFIG_FILE).

### <a name="configuration"></a>Konfiguration

Konfigurieren Sie die folgenden Einstellungen. Weitere Informationen finden Sie über die Links zu weiter unten in diesem Thema folgenden Abschnitten.
- Der Pfad zum freigegebenen Hotfixstammordner, der die anzuwendenden Updates und die Hotfixkonfigurationsdatei enthält. Sie können diesen Pfad über die Benutzeroberfläche für Cluster fähiges aktualisieren eingeben oder den **Pfad "\=hotfixrootfolderpath\<" >** PowerShell-Plug\--in-Argument konfigurieren. 

   > [!NOTE]
   > Sie können den hotfixstamm Ordner als lokalen Ordner Pfad oder als UNC-Pfad der Form  *\\ \\Server\\Name Freigabe\\rootfoldername*angeben. Es kann\-ein Domänen basierter oder eigenständiger DFS-Namespace Pfad verwendet werden. Die Plug\--in-Features, mit denen die Zugriffsberechtigungen in der hotfixkonfigurationsdatei überprüft werden, sind jedoch nicht mit einem DFS-Namespace Pfad kompatibel. Wenn Sie also eine konfigurieren, müssen Sie die Überprüfung der Zugriffsberechtigungen über die Benutzeroberfläche für Cluster fähiges aktualisieren oder durch Konfigurieren des **Disableaclchecks\=' true '** -\-Plug-in-Argument.
- Einstellungen auf dem Server, der den hotfixstamm Ordner hostet, um die entsprechenden Berechtigungen für den Zugriff auf den Ordner zu überprüfen und die Integrität der Daten sicher \(zustellen, auf die über\)SMB-Signaturen oder SMB-Verschlüsselung im SMB-Ordner zugegriffen wird Weitere Informationen finden Sie unter [Einschränken des Zugriffs auf den Hotfixstammordner](#BKMK_ACL).

### <a name="additional-options"></a>Zusätzliche Optionen

- Konfigurieren Sie optional das Plug\--in, damit die SMB-Verschlüsselung beim Zugriff auf Daten von der hotfixdateifreigabe erzwungen wird. Wählen Sie auf der Benutzeroberfläche für Cluster fähiges aktualisieren auf der Seite **zusätzliche Optionen** die Option **SMB-Verschlüsselung beim Zugriff auf hotfixstamm Ordner** anfordern aus, oder konfigurieren Sie das\- **\=** PowerShell-Plug-in-Argument "true". 
  > [!IMPORTANT]
  > Sie müssen auf dem SMB-Server zusätzliche Konfigurationsschritte ausführen, um die SMB-Datenintegrität mithilfe der SMB-Signatur oder SMB-Verschlüsselung zu ermöglichen. Weitere Informationen finden Sie unter Schritt 4 in [Einschränken des Zugriffs auf den Hotfixstammordner](#BKMK_ACL). Wenn Sie die Option zum Erzwingen der Verwendung der SMB-Verschlüsselung auswählen und der Hotfixstammordner nicht für den Zugriff mit SMB-Verschlüsselung konfiguriert ist, tritt bei der Updateausführung ein Fehler auf.
- Deaktivieren Sie optional die Standardprüfungen auf ausreichende Berechtigungen für den Hotfixstammordner und die Hotfixkonfigurationsdatei. Wählen Sie auf der Benutzeroberfläche für Cluster fähiges aktualisieren die Option **Prüfung auf Administrator Zugriff auf hotfixstamm Ordner und Konfigurationsdatei deaktivieren aus**, oder konfigurieren Sie das Plug\--in-Argument **disableaclchecks\=' true '** .
- Konfigurieren Sie optional das **hotfixinstallertimeoutminutes\= <Integer>**  -Argument, um anzugeben, wie lange das\-Hotfix-Plug-in auf die Rückgabe des hotfixinstallations Prozesses wartet. \(Der Standardwert ist 30 Minuten.\) Wenn Sie z. b. einen Timeout Zeitraum von zwei Stunden angeben möchten, legen Sie **\=hotfixinstallertimeoutminutes 120**fest.
- Konfigurieren Sie optional dasPlug\--in-Argument **hotfixconfigfilename \= <name>**  , um einen Namen für die hotfixkonfigurationsdatei anzugeben, die sich im hotfixstamm Ordner befindet. Wenn der Name nicht angegeben wird, lautet der Standardname "DefaultHotfixConfig.xml".
  
### <a name="BKMK_HF_ROOT"></a>Konfigurieren einer hotfixstamm Ordnerstruktur

Damit das Hotfix-\-Plug-in funktioniert, müssen Hotfixes in einer klar\-definierten Struktur in einem SMB-Dateifreigabe \(-hotfixstamm\)Ordner gespeichert werden, und Sie müssen das Hotfix-Plug\--in mit dem Pfad zum hotfixstamm Ordner über die Benutzeroberfläche für Cluster fähiges aktualisieren oder über die PowerShell-Cmdlets für Cluster fähiges aktualisieren. Dieser Pfad wird als\- **hotfixrootfolderpath** -Argument an das Plug-in übermittelt. Gemäß Ihrer Aktualisierungsanforderungen können Sie für den Hotfixstammordner eine von vielen Strukturen auswählen, wie in den folgenden Beispielen gezeigt. Dateien oder Ordner, die der Struktur nicht entsprechen, werden ignoriert.  
  
#### <a name="example-1---folder-structure-used-to-apply-hotfixes-to-all-cluster-nodes"></a>Beispiel 1: Ordnerstruktur, die zum Anwenden von Hotfixes auf alle Cluster Knoten verwendet wird
  
Um anzugeben, dass Hotfixes für alle Cluster Knoten gelten, kopieren Sie Sie in einen Ordner mit dem Namen **cauhotfix\_all** unter dem hotfixstamm Ordner. In diesem Beispiel wird\-das Plug-in-Argument **hotfixrootfolderpath** auf  *\\ \\myfileserver\\Hotfixes\\root\\* festgelegt. Der Ordner **cauhotfix\_all** enthält drei Updates mit den Erweiterungen MSU, MSI und MSP, die auf alle Cluster Knoten angewendet werden. Die Namen der Updatedateien dienen nur zur Veranschaulichung.  
  
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
  
#### <a name="example-2---folder-structure-used-to-apply-certain-updates-only-to-a-specific-node"></a>Beispiel 2: Ordnerstruktur, die verwendet wird, um bestimmte Updates nur auf einen bestimmten Knoten anzuwenden
  
Um Hotfixes anzugeben, die nur auf einen bestimmten Knoten angewendet werden, verwenden Sie unter dem Hotfixstammordner einen Unterordner mit dem Namen dieses Knotens. Verwenden Sie den NetBIOS-Namen des Clusterknotens, z. B. *ContosoNode1*. Verschieben Sie dann die Updates, die nur für diesen Knoten gelten, in diesen Unterordner. Im folgenden Beispiel wird\-das Plug-in-Argument **hotfixrootfolderpath** auf  *\\ \\\\myfileserver\\Hotfixes root\\* festgelegt. Updates im **cauhotfix\_all** -Ordner werden auf alle Cluster Knoten angewendet, und *\_Node1 Specific\_Update. msu* wird nur auf *ContosoNode1*angewendet.  
  
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
  
#### <a name="example-3---folder-structure-used-to-apply-updates-other-than-msu-msi-and-msp-files"></a>Beispiel für eine drei-Ordner-Struktur, die zum Anwenden von anderen Updates als MSU-, MSI-und MSP-Dateien verwendet wird
  
Das Plug-In **Microsoft.HotfixPlugin** wendet standardmäßig nur Updates mit den Erweiterungen MSU, MSI oder MSP an. Bestimmte Updates können jedoch andere Erweiterungen aufweisen und somit andere Installationsbefehle erfordern. Möglicherweise müssen Sie ein Firmwareupdate mit der Erweiterung EXE auf einen Knoten in einem Cluster anwenden. Sie können den hotfixstamm Ordner mit einem Unterordner konfigurieren, der angibt, dass ein\-bestimmter, nicht standardmäßiger Updatetyp installiert werden muss. Sie müssen auch eine entsprechende Ordnerinstallationsregel konfigurieren, die den Installationsbefehl im `<FolderRules>` -Element in der XML-Datei der Hotfixkonfiguration angibt.  
  
Im folgenden Beispiel wird\-das Plug-in-Argument **hotfixrootfolderpath** auf  *\\ \\\\myfileserver\\Hotfixes root\\* festgelegt. Es werden verschiedene Updates auf alle Clusterknoten angewendet. Zusätzlich wird das Firmwareupdate *SpecialHotfix1.exe* mithilfe von *FolderRule1* auf *ContosoNode1* angewendet. Weitere Informationen zum Konfigurieren von *ContosoNode1* in der Hotfixkonfigurationsdatei finden Sie weiter unten in diesem Abschnitt unter [Anpassen der Hotfixkonfigurationsdatei](#BKMK_CONFIG_FILE) .  
  
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
  
**Ordner "% SystemRoot\\%\\System32 WindowsPowerShell\\\\v\\1.0 modules clusterawareupdating"**  
  
Kopieren Sie die Beispielkonfigurationsdatei "DefaultHotfixConfig.xml" aus diesem Speicherort in den Hotfixstammordner, und nehmen Sie die entsprechenden Änderungen für Ihr Szenario vor, um die Hotfixkonfigurationsdatei anzupassen:  
  
> [!IMPORTANT]  
> Für die Anwendung der meisten von Microsoft bereitgestellten Hotfixes und anderer Updates kann die standardmäßige Hotfixkonfigurationsdatei ohne Änderungen verwendet werden. Die Anpassung der Hotfixkonfigurationsdatei zählt nur in fortgeschrittenen Verwendungsszenarios zu den erforderlichen Aufgaben.  
  
Standardmäßig definiert die XML-Datei der Hotfixkonfiguration die Installationsregeln und Beendigungsbedingungen für die folgenden beiden Kategorien von Hotfixes:  
  
-   Hotfixdateien mit Erweiterungen, die vom\-Plug-in standardmäßig \(installiert werden können. msu-, MSI-und MSP-Dateien\).  
  
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
  
-   Hotfix oder andere Update Dateien, bei denen es sich nicht um MSI-, MSU-oder MSP-Dateien handelt,\-z. b. nicht von Microsoft stammende Treiber, Firmware und BIOS-Updates.  
  
    Jeder nicht\-standardmäßige Dateityp wird `<Folder>` als-Element im `<FolderRules>` -Element konfiguriert. Das Namensattribut des `<Folder>` -Elements muss mit dem Namen eines Ordners im Hotfixstammordner übereinstimmen, der Updates vom entsprechenden Typ enthalten wird. Der Ordner kann sich im Ordner " **cauhotfix\_all** " oder in einem\-Knoten spezifischen Ordner befinden. Wenn *FolderRule1* z. B. im Hotfixstammordner konfiguriert ist, konfigurieren Sie das folgende Element in der XML-Datei, damit es eine Installationsvorlage und Beendigungsbedingungen für die Updates in diesem Ordner definiert:  
  
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
  
### <a name="BKMK_ACL"></a>Einschränken des Zugriffs auf den hotfixstamm Ordner  
Sie müssen verschiedene Schritte ausführen, um den SMB-Dateiserver und die -Dateifreigabe so zu konfigurieren, dass sie den Schutz der Dateien im Hotfixstammordner nur für den Zugriff im Kontext von **Microsoft.HotfixPlugin**unterstützen. Diese Schritte aktivieren verschiedene Features, die dabei helfen, mögliche Manipulationen an den Hotfixdateien zu verhindern, die möglicherweise den Failovercluster gefährden können.  
  
Die allgemeinen Schritte sehen wie folgt aus:  
  
1.  Identifizieren Sie das Benutzerkonto, das für Update Ausführungen mithilfe des Plug\--ins verwendet wird.  
  
2.  Konfigurieren dieses Benutzerkontos in den erforderlichen Gruppen auf einem SMB-Dateiserver  
  
3.  Konfigurieren der Berechtigungen für den Zugriff auf den Hotfixstammordner  
  
4.  Konfigurieren der Einstellungen für die SMB-Datenintegrität  
  
5.  Aktivieren der Windows-Firewall-Regel auf dem SMB-Server  
  
#### <a name="step-1-identify-the-user-account-that-is-used-for-updating-runs-by-using-the-hotfix-plug-in"></a>Schritt 1 Identifizieren Sie das Benutzerkonto, das für Update Ausführungen verwendet wird, indem Sie das\-Hotfix-Plug-in verwenden.
  
Das Konto, das in Cau zum Überprüfen der Sicherheitseinstellungen beim Ausführen einer Update Ausführung mithilfe von **Microsoft. hotfixplugin** verwendet wird, hängt davon ab,\-ob das Cluster fähige\-aktualisieren im Remote Aktualisierungs Modus oder im selbst Aktualisierungs Modus verwendet wird:  
  
-   **Remote\-Aktualisierungs Modus** das Konto, das über Administratorrechte für den Cluster verfügt, um die Vorschau anzuzeigen und Updates anzuwenden.  
  
-   **Selbst\-Aktualisierungs Modus** der Name des virtuellen Computer Objekts, das in Active Directory für die Cluster Rolle für Cluster fähiges aktualisieren konfiguriert ist. Dies ist entweder der Name eines vorab bereitgestellten virtuellen Computerobjekts in Active Directory für die Clusterrolle für clusterfähiges Aktualisieren oder der Name, der von der Clusterrolle für clusterfähiges Aktualisieren generiert wird. Wenn Sie den Namen abrufen möchten, wenn er von Cau generiert wurde, führen Sie das PowerShell-Cmdlet **get\-cauclusterrole** Cau aus. In der Ausgabe ist **ResourceGroupName** der Name des generierten virtuellen Computerobjektkontos.  
  
#### <a name="step-2-configure-this-user-account-in-the-necessary-groups-on-an-smb-file-server"></a>Schritt 2 Konfigurieren dieses Benutzerkontos in den erforderlichen Gruppen auf einem SMB-Dateiserver
  
> [!IMPORTANT]  
> Sie müssen das für die Updateausführungen verwendete Konto als lokales Administratorkonto auf dem SMB-Server hinzufügen. Wenn dies aufgrund der Sicherheitsrichtlinien in Ihrer Organisation nicht zulässig ist, konfigurieren Sie dieses Konto auf dem SMB-Server mit den erforderlichen Berechtigungen, indem Sie das folgende Verfahren durchführen.  
  
##### <a name="to-configure-a-user-account-on-the-smb-server"></a>So konfigurieren Sie ein Benutzerkonto auf dem SMB-Server  
  
1.  Fügen Sie das für Updateausführungen verwendete Konto zur Gruppe "Distributed COM-Benutzer" sowie zu einer der folgenden Gruppen hinzu: Hauptbenutzer, Servervorgang oder Druck-Operator.  
  
2.  Starten Sie die WMI-Verwaltungskonsole auf dem SMB-Server, um die erforderlichen WMI-Berechtigungen für das Konto zu aktivieren. Starten Sie PowerShell, und geben Sie dann den folgenden Befehl ein:  
  
    ```  
    wmimgmt.msc  
    ```  
  
3.  Klicken Sie in der Konsolen Struktur\-mit der rechten Maustaste auf **WMI- \(Steuerung lokal\)** , und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie auf **Sicherheit**, und erweitern Sie dann **Stamm**.  
  
5.  Klicken Sie auf **CIMV2**und dann auf **Sicherheit**.  
  
6.  Fügen Sie das für Updateausführungen verwendete Konto zur Liste **Gruppen- oder Benutzernamen** hinzu.  
  
7.  Erteilen Sie dem für Updateausführungen verwendeten Konto die Berechtigungen **Methoden ausführen** und **Remoteaktivierung** .  
  
#### <a name="step-3-configure-permissions-to-access-the-hotfix-root-folder"></a>Schritt 3 Konfigurieren der Berechtigungen für den Zugriff auf den Hotfixstammordner
  
Wenn Sie versuchen, Updates anzuwenden, prüft das Hotfix-Plug\--in standardmäßig die Konfiguration der NTFS-Dateisystem Berechtigungen für den Zugriff auf den hotfixstamm Ordner. Wenn die Ordner Zugriffsberechtigungen nicht ordnungsgemäß konfiguriert sind, kann eine Update Ausführung mit dem Hotfix-Plug\--in fehlschlagen.  
  
Wenn Sie die Standardkonfiguration des Hotfix-Plug\--ins verwenden, stellen Sie sicher, dass die Berechtigungen für den Ordner Zugriff den folgenden Anforderungen entsprechen.  
  
-   Die Gruppe "Benutzer" verfügt über die Berechtigung "Lesen".  
  
-   Wenn das Plug\--in Updates mit der Erweiterung ". exe" anwendet, verfügt die Gruppe "Benutzer" über die Berechtigung "ausführen".  
  
-   Nur bestimmte Sicherheits Prinzipale sind zulässig \(\) , aber Sie müssen nicht über die Berechtigung Schreiben oder ändern verfügen. Die zulässigen Prinzipale sind die Gruppe der lokalen Administratoren, SYSTEM, ERSTELLER-BESITZER und TrustedInstaller. Anderen Konten oder Gruppen ist es nicht gestattet, die Berechtigung "Schreiben" oder "Ändern" für den Hotfixstammordner zu verwenden.  
  
Optional können Sie die obigen Prüfungen deaktivieren, die vom Plug\--in standardmäßig durchgeführt werden. Hierzu stehen Ihnen zwei Möglichkeiten zur Verfügung.  
  
-   Wenn Sie die PowerShell-Cmdlets für Cluster fähiges aktualisieren verwenden, konfigurieren Sie das **disableaclchecks\=' true '** -Argument im **caupluginarguments** -Parameter für\-das Hotfix-Plug-in.  
  
-   Wenn Sie die Benutzeroberfläche für clusterfähiges Aktualisieren verwenden, wählen Sie die Option **Prüfung auf Administratorzugriff auf Hotfixstammordner und Konfigurationsdatei deaktivieren** auf der Seite **Weitere Updateoptionen** aus, die zum Konfigurieren der Optionen von Updateausführungen verwendet wird.  
  
Es wird jedoch in vielen Umgebungen als bewährte Methode empfohlen, dass Sie diese Prüfungen mithilfe der Standardkonfiguration erzwingen.  
  
#### <a name="step-4-configure-settings-for-smb-data-integrity"></a>Schritt 4 Konfigurieren der Einstellungen für die SMB-Datenintegrität
  
Zum Überprüfen der Datenintegrität in den Verbindungen zwischen den Cluster Knoten und der SMB-Dateifreigabe erfordert das Hotfix-Plug\--in, dass Sie die Einstellungen auf der SMB-Dateifreigabe für die SMB-Signatur oder SMB-Verschlüsselung aktivieren. Die SMB-Verschlüsselung, die in vielen Umgebungen eine höhere Sicherheit und bessere Leistung bietet, wird ab Windows Server 2012 unterstützt. Sie können eine oder beide Einstellungen wie folgt aktivieren:  
  
-   Informationen zum Aktivieren der SMB-Signatur finden Sie unter dem Verfahren in der Microsoft Knowledge Base in [Artikel 887429](https://support.microsoft.com/kb/887429) .  
  
-   Um die SMB-Verschlüsselung für den freigegebenen SMB-Ordner zu aktivieren, führen Sie das folgende PowerShell-Cmdlet auf dem SMB-Server aus:  
  
    ```PowerShell  
    Set-SmbShare <ShareName> -EncryptData $true  
    ```  
  
    Dabei gibt <*ShareName*> den Namen des freigegebenen SMB-Ordners an.  
  
Um optional die Verwendung der SMB-Verschlüsselung in den Verbindungen mit dem SMB-Server zu erzwingen, wählen Sie auf der Benutzeroberfläche für Cluster fähiges aktualisieren die Option **SMB-Verschlüsselung beim Zugriff auf hotfixstamm Ordner** anfordern aus, oder konfigurieren Sie den **\="true"** -Plug-in. \-in Argument mithilfe der Cau-PowerShell-Cmdlets.  
  
> [!IMPORTANT]  
> Wenn Sie die Option zum Erzwingen der Verwendung der SMB-Verschlüsselung auswählen und der Hotfixstammordner nicht für Verbindungen konfiguriert ist, die die SMB-Verschlüsselung verwenden, tritt bei der Updateausführung ein Fehler auf.  
  
#### <a name="step-5-enable-a-windows-firewall-rule-on-the-smb-server"></a>Schritt 5 Aktivieren der Windows-Firewall-Regel auf dem SMB-Server
  
Sie müssen die **Datei \(Server-Remoteverwaltungs-\) SMB\-in** der Regel in der Windows-Firewall auf dem SMB-Dateiserver aktivieren. Dies ist in Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 standardmäßig aktiviert.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Übersicht über das Cluster fähige aktualisieren](cluster-aware-updating.md)
  
-   [Windows PowerShell-Cmdlets für Cluster fähiges aktualisieren](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating)  
  
-   [Plug-in-Referenz für Cluster fähiges aktualisieren](https://msdn.microsoft.com/library/hh418084.aspx)  
  
