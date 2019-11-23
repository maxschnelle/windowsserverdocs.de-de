---
ms.assetid: d44d4430-41e2-483a-9685-92610cdef32a
title: Funktionsweise von Plug-Ins für Cluster fähiges aktualisieren
ms.topic: article
ms.prod: windows-server
manager: dongill
ms.author: jgerend
author: JasonGerend
ms.date: 04/28/2017
ms.technology: storage-failover-clustering
description: Verwenden von Plug-ins zum Koordinieren von Updates bei Verwendung des Cluster fähigen Aktualisierens in Windows Server zum Installieren von Updates auf einem Cluster.
ms.openlocfilehash: f6c572a397530704dd91d9c67c5c1758ccc085c4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361288"
---
# <a name="how-cluster-aware-updating-plug-ins-work"></a>Funktionsweise von Plug-Ins für Cluster fähiges aktualisieren

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Beim [Cluster fähigen aktualisieren (Cluster-Aware Update](cluster-aware-updating.md) , Cau) werden Plug-ins verwendet, um die Installation von Updates auf Knoten in einem Failovercluster zu koordinieren. Dieses Thema enthält Informationen zur Verwendung der erstellten\-in Plug\-ins für Cluster fähiges aktualisieren oder in anderen Plug\-ins, die Sie für Cau installieren.

## <a name="BKMK_INSTALL"></a>Installieren eines Plug\-in  
Ein Plug\-in anderen als die Standard-Plug\-ins, die mit Cau \(**Microsoft. windowsupdateplugin** und **Microsoft. hotfixplugin** installiert werden\) müssen separat installiert werden. Wenn Cau im selbst\-Aktualisierungs Modus verwendet wird, muss das Plug\-in auf allen Cluster Knoten installiert werden. Wenn das Cluster fähige aktualisieren im Remote\--Aktualisierungs Modus verwendet wird, muss das Plug\-in auf dem Remote Computer für den Update Koordinator installiert sein. Bei einem Plug\-in, das Sie installieren, sind möglicherweise zusätzliche Installationsanforderungen auf den einzelnen Knoten erforderlich.  
  
Befolgen Sie zum Installieren eines Plug\-in die Anweisungen des Plug\-auf dem Verleger. Führen Sie das Cmdlet [Register-cauplugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin) auf jedem Computer aus, auf dem der Plug\-in installiert ist, um eine Plug\-in mit Cau manuell zu registrieren.  
  
## <a name="specify-a-plug-in-and-plug-in-arguments"></a>Geben Sie einen Plug\-in und einen Plug\-in Argumente an.  
  
### <a name="specify-a-cau-plug-in"></a>Cau-Plug\-in angeben

Wählen Sie auf der Benutzeroberfläche für Cluster fähiges aktualisieren aus einer\-Dropdown Liste mit verfügbaren Plug\-ins ein Plug\-aus, wenn Sie mit Cau die folgenden Aktionen ausführen:  
  
-   Anwenden von Updates auf Cluster  
  
-   Updatevorschau für Cluster  
  
-   Konfigurieren von selbst\-Aktualisierungs Optionen für Cluster  
  
Standardmäßig wählt Cau den Plug\-in **Microsoft. windowsupdateplugin**aus. Allerdings können Sie alle Plug\-in angeben, die installiert und bei Cau registriert sind.

> [!TIP]  
> In der Benutzeroberfläche für Cluster fähiges aktualisieren können Sie nur ein einzelnes Plug\-in angeben, das für das Cluster fähige aktualisieren verwendet wird, um eine Vorschau anzuzeigen oder Updates während einer Update Laufzeit anzuwenden. Mithilfe der PowerShell-Cmdlets für Cluster fähiges aktualisieren können Sie eine oder mehrere Plug\-ins angeben. Wenn Sie mehrere Arten von Updates auf dem Cluster installieren müssen, ist es in der Regel effizienter, mehrere Plug\-ins in einer Update Laufzeit anzugeben, anstatt für jede Plug\-in eine separate Update Laufzeit zu verwenden. Dadurch sind z. B. meist weniger Knotenneustarts erforderlich.

Mithilfe der in der folgenden Tabelle aufgeführten PowerShell-Cmdlets für Cluster fähiges aktualisieren können Sie eine oder mehrere Plug\-ins für eine Update-oder Scanvorgang angeben, indem Sie den **– caupluginname** -Parameter übergeben. Sie können mehrere Plug\-in Namen angeben, indem Sie Sie durch Kommas trennen. Wenn Sie mehrere Plug\-ins angeben, können Sie auch steuern, wie sich die Plug\-ins während einer Update Ausführung gegenseitig beeinflussen, indem Sie die Parameter **\-runpluginsseridal**, **\-stoponpluginfailure**und **– separatereboots** angeben. Weitere Informationen zur Verwendung mehrerer Plug\-ins finden Sie unter den Links, die für die Cmdlet-Dokumentation in der folgenden Tabelle bereitgestellt werden.  
  
|Cmdlet|Beschreibung|  
|----------|---------------|  
|[Add-cauclusterrole](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/add-cauclusterrole)|Fügt die Cluster Rolle für Cluster fähiges aktualisieren hinzu, die dem angegebenen Cluster die Funktion für die selbst\-Aktualisierung bereitstellt.|  
|[Aufrufen: caurun](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/invoke-caurun)|Prüft Clusterknoten auf geeignete Updates und installiert diese Updates über eine Updateausführung auf dem angegebenen Cluster.|  
|[Aufrufen: kauscan](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/invoke-causcan)|Prüft Clusterknoten auf geeignete Updates und gibt eine Liste des ersten Updatesatzes zurück, der auf jeden Knoten des angegebenen Clusters angewendet werden würde.|  
|[Set-cauclusterrole](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/set-cauclusterrole)|Legt Konfigurationseigenschaften für die Clusterrolle für clusterfähiges Aktualisieren auf dem angegebenen Cluster fest.|  
  
Wenn Sie mit diesen Cmdlets keine Cau-Plug\-in Parameter angeben, ist der Standardwert der Plug\-in **Microsoft. windowsupdateplugin**.  
  
### <a name="specify-cau-plug-in-arguments"></a>Cau-Plug\-in Argumenten angeben  
Wenn Sie die Optionen für die Aktualisierungs Laufzeit konfigurieren, können Sie einen oder mehrere *Name-\=-Wert* -Paare \(\) Argumente angeben, die für das ausgewählte Plug\-in verwendet werden sollen. Auf der Benutzeroberfläche für clusterfähiges Aktualisieren können Sie z. B. wie folgt mehrere Argumente angeben:  
  
**Name1\=value1; Name2\=Value2; Name3\=Wert3**  
  
Diese *Name\=Wert* -Paare müssen für den von Ihnen angegebenen Plug\-sinnvoll sein. Bei manchen Plug\-ins sind die Argumente optional.  
  
Die Syntax der Cau-Plug\-in-Argumente befolgt diese allgemeinen Regeln:  
  
-   Mehrere *Name-\=-Wert* -Paare werden durch Semikolons getrennt.  
  
-   Ein Wert, der Leerzeichen enthält, ist in Anführungszeichen eingeschlossen, z. b.: **Name1\="Wert mit Leerzeichen"** .  
  
-   Die genaue Syntax des *Werts* hängt von der Plug\-in ab.  
  
Zum Angeben von Plug\-in Argumenten mithilfe der Cau-PowerShell-Cmdlets, die den Parameter " **– caupluginparameters** " unterstützen, übergeben Sie einen Parameter in der Form:  
  
**\-caupluginarguments @ {Name1\=value1; Name2\=Value2; Name3\=Wert3}**  
  
Sie können auch eine vordefinierte PowerShell-Hash Tabelle verwenden. Um Plug\-in-Argumente für mehrere Plug\-in anzugeben, übergeben Sie mehrere Hash Tabellen mit Argumenten, die durch Kommas getrennt sind. Übergeben Sie die Plug\-in den Argumenten des Plug\-in der Reihenfolge, die in **caupluginname**angegeben ist.  
  
### <a name="specify-optional-plug-in-arguments"></a>Optionale Plug\-in Argumenten angeben  
Die Plug\-ins, die von Cau \(**Microsoft. windowsupdateplugin** und **Microsoft. hotfixplugin** installiert werden\) bieten zusätzliche Optionen, die Sie auswählen können. Diese werden auf der Benutzeroberfläche für Cluster fähiges aktualisieren auf der Seite **zusätzliche Optionen** angezeigt, nachdem Sie die Optionen für die Update Ausführung für das Plug\-in konfiguriert haben. Wenn Sie die PowerShell-Cmdlets für Cluster fähiges aktualisieren verwenden, werden diese Optionen als optionale Plug\-in-Argumente konfiguriert. Weitere Informationen finden Sie unter [Verwenden von "Microsoft.WindowsUpdatePlugin"](#BKMK_WUP) und [Verwenden von "Microsoft.HotfixPlugin"](#BKMK_HFP) weiter unten in diesem Thema.  
  
## <a name="manage-plug-ins-using-windows-powershell-cmdlets"></a>Verwalten von Plug\-ins mithilfe von Windows PowerShell-Cmdlets  
  
|Cmdlet|Beschreibung|  
|----------|---------------|  
|[Get-cauplugin](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/get-cauplugin)|Ruft Informationen zu einem oder mehreren Software Update-\-Plug-ins ab, die auf dem lokalen Computer registriert sind.|  
|[Register-cauplugin]((https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/register-cauplugin))|Registriert ein CAU-Plug\-für die Software Aktualisierung auf dem lokalen Computer.|  
|[Unregister-cauplugin](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/unregister-cauplugin)|Entfernt ein Software Update-\-Plug-in aus der Liste der Plug\-ins, die von Cau verwendet werden können. **Hinweis:** Die Registrierung der Plug\-ins, die mit Cau \(**Microsoft. windowsupdateplugin** und **Microsoft. hotfixplugin**\) installiert werden, kann nicht aufgehoben werden.|  
  
## <a name="BKMK_WUP"></a>Verwenden von "Microsoft. windowsupdateplugin"  

Die Standard-Plug\-in für Cau, **Microsoft. windowsupdateplugin**, führt die folgenden Aktionen aus:
- Das Plug-In steht in Kontakt mit dem Windows Update-Agent auf den einzelnen Knoten des Failoverclusters, um Updates für die Microsoft-Produkte anzuwenden, die auf den einzelnen Knoten ausgeführt werden.
- Von werden Cluster Updates direkt von Windows Update oder Microsoft Update oder von\-einem lokalen Windows Server Update Services \(WSUS-\) Server installiert.
- Installiert nur die ausgewählten, allgemeinen Verteilungs Releases \(DDR-\) Updates. Standardmäßig wendet das Plug\-in nur wichtige Software Updates an. Es ist keine Konfiguration erforderlich. Die Standardkonfiguration lädt wichtige Updates von allgemeinen Vertriebsversionen auf die einzelnen Knoten herunter und installiert sie. 

> [!NOTE]
> Wenn Sie andere Updates als die wichtigen Software Updates anwenden möchten, die standardmäßig ausgewählt sind \(z. b. Treiber Updates\), können Sie einen optionalen Plug\-in-Parameter konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren der Abfragezeichenfolge für den Windows Update-Agent](#BKMK_QUERY).

### <a name="requirements"></a>Anforderungen

- Der Computer mit dem Failovercluster und dem Remote Update Koordinator \(bei Verwendung\) die Anforderungen für Cau und die Konfiguration, die für die Remote Verwaltung erforderlich ist, gemäß den [Anforderungen und bewährten Methoden für Cau](cluster-aware-updating-requirements.md)erfüllen müssen.
- Lesen Sie die [Empfehlungen für die Anwendung von Microsoft-Updates](cluster-aware-updating-requirements.md#BKMK_BP_WUA), und nehmen Sie dann alle erforderlichen Änderungen an der Microsoft-Updatekonfiguration für die Failoverclusterknoten vor.
- Um optimale Ergebnisse zu erzielen, wird empfohlen, dass Sie das Cau-Best Practices Analyzer \(BPA\) ausführen, um sicherzustellen, dass die Cluster-und Update Umgebung ordnungsgemäß für die Anwendung von Updates mithilfe von Cau konfiguriert sind. Weitere Informationen finden Sie unter [Testen der Updatebereitschaft für clusterfähiges Aktualisieren](cluster-aware-updating-requirements.md#BKMK_BPA).

> [!NOTE]
> Updates, die das Akzeptieren von Microsoft-Lizenzbedingungen oder andere Benutzerinteraktionen erfordern, werden ausgeschlossen und müssen manuell installiert werden.

### <a name="additional-options"></a>Zusätzliche Optionen

Optional können Sie die folgenden Plug\-in-Argumente angeben, um den Satz der Updates zu vergrößern oder einzuschränken, die von der Plug\-in angewendet werden:
- Wenn Sie die Plug\-in zum Anwenden der empfohlenen Updates zusätzlich zu wichtigen Updates auf den einzelnen Knoten konfigurieren möchten, aktivieren Sie auf der Cau-Benutzeroberfläche auf der Seite **zusätzliche Optionen** das Kontrollkästchen **Empfohlene Updates auf die gleiche Weise wie wichtige Updates erhalten** .
<br>Alternativ dazu können Sie auch das Plug\- **' includerecommendedupdates '\=' true '** -Plug in-Argument konfigurieren.
- Um die Plug\-in zum Filtern der Typen von DDR-Updates zu konfigurieren, die auf die einzelnen Cluster Knoten angewendet werden, geben Sie eine Windows Update-Agent-Abfrage Zeichenfolge mit einem **QueryString** -Plug\-in-Argument an. Weitere Informationen finden Sie unter [Konfigurieren der Abfragezeichenfolge für den Windows Update-Agent](#BKMK_QUERY).

### <a name="BKMK_QUERY"></a>Konfigurieren der Abfrage Zeichenfolge für Windows Update-Agent  
Sie können ein Plug\-in-Argument für das Standard-Plug\-in, **Microsoft. windowsupdateplugin**, konfigurieren, das aus einem Windows Update-Agent \(WUA\) Abfrage Zeichenfolge besteht. Diese Anweisung verwendet die WUA-API, um eine oder mehrere Gruppen von Microsoft-Updates zu ermitteln, die auf Basis bestimmter Auswahlkriterien auf die einzelnen Knoten angewendet werden. Sie können mehrere Kriterien mithilfe einer logischen UND- oder ODER-Operation kombinieren. Die WUA-Abfrage Zeichenfolge wird wie folgt in einem Plug\-in-Argument angegeben:  
  
**QueryString\="Kriterium1\=value1 und\/oder Criterion2\=Value2 und\/oder..."**  
  
**Microsoft.WindowsUpdatePlugin** wählt z. B. wichtige Updates automatisch mithilfe des Standardarguments **QueryString** aus, das mit den Kriterien **IsInstalled**, **Type**, **IsHidden** und **IsAssigned** erzeugt wird:  
  
**QueryString\="isingestrandet\=0 und Typ\=" Software "und IsHidden\=0 und isassigned\=1"**  
  
Wenn Sie ein **QueryString** -Argument angeben, wird es anstelle des standardmäßigen **QueryString** -Arguments verwendet, das für das Plug\-in konfiguriert ist.  
  
#### <a name="example-1"></a>Beispiel 1
  
So konfigurieren Sie ein **QueryString** -Argument, das ein bestimmtes Update identifiziert, gemäß ID *f6ce46c1\-971c\-43f9\-a2aa\-783df125f003*:  
  
**QueryString\="UpdateId\=" f6ce46c1\-971c\-43F 9\-a2aa\-783df125.** \=  
  
> [!NOTE]  
> Das vorherige Beispiel gilt für die Anwendung von Updates mithilfe des Assistenten zum Aktualisieren von Cluster\-fähigen Updates. Wenn Sie ein bestimmtes Update installieren möchten, indem Sie die Optionen für die selbst\-Aktualisierung mithilfe der Cau-Benutzeroberfläche konfigurieren, oder indem Sie das PowerShell-Cmdlet **\-cauclusterrole hinzufügen** oder **\-cauclusterrole festlegen**, müssen Sie den UpdateId-Wert mit zwei einfachen\-Anführungszeichen formatieren:  
>   
> **QueryString\="UpdateId\=' ' f6ce46c1\-971c\-43F 9\-a2aa\-783df125-ID ' ' und isingestrandet\=0"**  
  
#### <a name="example-2"></a>Beispiel 2
  
So konfigurieren Sie ein **QueryString**-Argument, das ausschließlich Treiber installiert  
  
**QueryString\="isingestrandet\=0 und Type\=" Driver "und IsHidden\=0"**  
  
Weitere Informationen zu Abfrage Zeichenfolgen für die Standard-Plug\-in, **Microsoft. windowsupdateplugin**, die Suchkriterien \(wie z. b. " **isingestrandet**\)" und die Syntax, die Sie in die Abfrage Zeichenfolgen einschließen können, finden Sie im Abschnitt zu den Suchkriterien in der API-Referenz für den [Windows Update-Agent (WUA)](https://go.microsoft.com/fwlink/p/?LinkId=223304).  
  
## <a name="BKMK_HFP"></a>Verwenden von Microsoft. hotfixplugin  
Der Plug\-in **Microsoft. hotfixplugin** kann verwendet werden, um Microsoft Limited Distribution-Releases \(LDR-\) Updates \(auch Hotfixes genannt und früher als QFEs bezeichnet\), die Sie unabhängig herunterladen, um bestimmte Probleme von Microsoft-Software zu beheben. Das Plug-in installiert Updates aus einem Stamm Ordner auf einer SMB-Dateifreigabe und kann auch so angepasst werden, dass Sie nicht\-Microsoft-Treiber, Firmware und BIOS-Updates anwenden.

> [!NOTE]
> In Knowledge Base-Artikeln können Microsoft-Hotfixes gelegentlich von Microsoft heruntergeladen werden. Sie werden jedoch auch für Kunden auf der Basis von\-benötigt.

### <a name="requirements"></a>Anforderungen

- Der Computer mit dem Failovercluster und dem Remote Update Koordinator \(bei Verwendung\) die Anforderungen für Cau und die Konfiguration, die für die Remote Verwaltung erforderlich ist, gemäß den [Anforderungen und bewährten Methoden für Cau](cluster-aware-updating-requirements.md)erfüllen müssen.
- Lesen Sie hierzu [Empfehlungen zur Verwendung von Microsoft.HotfixPlugin](cluster-aware-updating-requirements.md#BKMK_BP_HF).
- Um optimale Ergebnisse zu erzielen, wird empfohlen, dass Sie das Cau-Best Practices Analyzer \(BPA-\) Modell ausführen, um sicherzustellen, dass die Cluster-und Update Umgebung ordnungsgemäß für die Anwendung von Updates mithilfe von Cau konfiguriert sind. Weitere Informationen finden Sie unter [Testen der Updatebereitschaft für clusterfähiges Aktualisieren](cluster-aware-updating-requirements.md#BKMK_BPA).
- Rufen Sie die Updates vom Verleger ab, kopieren Sie Sie, oder extrahieren Sie Sie auf einen Server Message Block \(SMB-\) Dateifreigabe \(hotfixstamm Ordner\) der mindestens SMB 2,0 unterstützt und auf den alle Cluster Knoten und den Remote Update Koordinator-Computer zugreifen können \(, wenn Cau im Remote\-Aktualisierungs Modus\)verwendet wird. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Konfigurieren einer Hotfixstammordnerstruktur](#BKMK_HF_ROOT). 

    > [!NOTE]
    > Standardmäßig werden von diesem Plug\-in nur Hotfixes mit den folgenden Dateinamen Erweiterungen installiert: MSU, MSI und MSP.

- Kopieren Sie die Datei "defaulthotfixconfig. xml" \(die im Ordner **% systemroot%\\System32\\WindowsPowerShell\\v 1.0\\modules\\clusterawareupdating** auf einem Computer bereitgestellt wird, auf dem die Cau-Tools installiert sind\) dem hotfixstamm Ordner, den Sie erstellt haben und in dem Sie die Hotfixes extrahiert haben. Kopieren Sie z. b. die Konfigurationsdatei in *\\\\myfileserver\\Hotfixes\\Stamm\\* . 

    > [!NOTE]
    > Für die Installation der meisten von Microsoft bereitgestellten Hotfixes und anderer Updates kann die standardmäßige Hotfixkonfigurationsdatei ohne Änderungen verwendet werden. Sie können die Konfigurationsdatei als erweiterte Aufgabe anpassen, wenn dies in Ihrem Szenario erforderlich ist. Die Konfigurationsdatei kann benutzerdefinierte Regeln enthalten, z. B. zum Behandeln von Hotfixdateien mit spezieller Erweiterung oder zum Definieren eines Verhaltens für bestimmte Beendigungsbedingungen. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Anpassen der Hotfixkonfigurationsdatei](#BKMK_CONFIG_FILE).

### <a name="configuration"></a>Konfiguration

Konfigurieren Sie die folgenden Einstellungen. Weitere Informationen finden Sie über die Links zu weiter unten in diesem Thema folgenden Abschnitten.
- Der Pfad zum freigegebenen Hotfixstammordner, der die anzuwendenden Updates und die Hotfixkonfigurationsdatei enthält. Sie können diesen Pfad über die Benutzeroberfläche für Cluster fähiges aktualisieren eingeben oder den **hotfixrootfolderpath-\=\<Pfad >** PowerShell-Plug\-in-Argument konfigurieren. 

   > [!NOTE]
   > Sie können den hotfixstamm Ordner als lokalen Ordner Pfad oder als UNC-Pfad der Form *\\\\Servername\\Freigabe\\rootfoldername*angeben. Es kann ein Domänen\-basierter oder eigenständiger DFS-Namespace Pfad verwendet werden. Die Plug\-in Funktionen, die die Zugriffsberechtigungen in der hotfixkonfigurationsdatei überprüfen, sind jedoch nicht mit einem DFS-Namespace Pfad kompatibel. Wenn Sie also eine konfigurieren, müssen Sie die Überprüfung auf Zugriffsberechtigungen über die Benutzeroberfläche für Cluster fähiges aktualisieren oder durch konfigurieren **\=der "true"** -Plug\-in-Argument deaktivieren.
- Einstellungen auf dem Server, der den hotfixstamm Ordner hostet, um die entsprechenden Berechtigungen für den Zugriff auf den Ordner zu überprüfen und die Integrität der Daten sicherzustellen, auf die über den freigegebenen SMB-Ordner zugegriffen wird \(SMB-Signatur oder SMB-\)Verschlüsselung Weitere Informationen finden Sie unter [Einschränken des Zugriffs auf den Hotfixstammordner](#BKMK_ACL).

### <a name="additional-options"></a>Zusätzliche Optionen

- Optional können Sie die Plug\-in so konfigurieren, dass die SMB-Verschlüsselung beim Zugriff auf Daten von der hotfixdateifreigabe erzwungen wird. Wählen Sie auf der Benutzeroberfläche für Cluster fähiges aktualisieren auf der Seite **zusätzliche Optionen** die Option **SMB-Verschlüsselung beim Zugriff auf hotfixstamm Ordner** anfordern aus, oder konfigurieren Sie das PowerShell-Plug\-in **"Requirements smbencryption"\="true"** . 
  > [!IMPORTANT]
  > Sie müssen auf dem SMB-Server zusätzliche Konfigurationsschritte ausführen, um die SMB-Datenintegrität mithilfe der SMB-Signatur oder SMB-Verschlüsselung zu ermöglichen. Weitere Informationen finden Sie unter Schritt 4 in [Einschränken des Zugriffs auf den Hotfixstammordner](#BKMK_ACL). Wenn Sie die Option zum Erzwingen der Verwendung der SMB-Verschlüsselung auswählen und der Hotfixstammordner nicht für den Zugriff mit SMB-Verschlüsselung konfiguriert ist, tritt bei der Updateausführung ein Fehler auf.
- Deaktivieren Sie optional die Standardprüfungen auf ausreichende Berechtigungen für den Hotfixstammordner und die Hotfixkonfigurationsdatei. Wählen Sie auf der Benutzeroberfläche für Cluster fähiges aktualisieren die Option **Prüfung auf Administrator Zugriff auf hotfixstamm Ordner und Konfigurationsdatei deaktivieren aus**, oder konfigurieren Sie die Option **disableaclchecks\="true"** Plug\-in-Argument.
- Konfigurieren Sie optional das Argument **hotfixinstallertimeoutminutes\=<Integer>** , um anzugeben, wie lange das Hotfix-Plug\-in wartet, bis der hotfixinstallationsprozess zurückgegeben wird. \(der Standardwert ist 30 Minuten. Wenn Sie z. b. einen Timeout Zeitraum von zwei Stunden angeben möchten, legen Sie **hotfixinstallertimeoutminutes\=120**fest.\)
- Optional können Sie die **hotfixconfigfilename-\= <name>** Plug\-in-Argument konfigurieren, um einen Namen für die hotfixkonfigurationsdatei anzugeben, die sich im hotfixstamm Ordner befindet. Wenn der Name nicht angegeben wird, lautet der Standardname "DefaultHotfixConfig.xml".
  
### <a name="BKMK_HF_ROOT"></a>Konfigurieren einer hotfixstamm Ordnerstruktur

Damit das Hotfix-\-Plug-in funktioniert, müssen die Hotfixes in einer ordnungsgemäß\-definierten Struktur in einer SMB-Dateifreigabe \(hotfixstamm Ordner\)gespeichert werden, und Sie müssen das Hotfix-\-Plug-in mit dem Pfad zum hotfixstamm Ordner konfigurieren, indem Sie die Cau-Benutzeroberfläche oder die PowerShell-Cmdlets für Cau verwenden. Dieser Pfad wird als **hotfixrootfolderpath** -Argument an das Plug\-in übermittelt. Gemäß Ihrer Aktualisierungsanforderungen können Sie für den Hotfixstammordner eine von vielen Strukturen auswählen, wie in den folgenden Beispielen gezeigt. Dateien oder Ordner, die der Struktur nicht entsprechen, werden ignoriert.  
  
#### <a name="example-1---folder-structure-used-to-apply-hotfixes-to-all-cluster-nodes"></a>Beispiel 1: Ordnerstruktur, die zum Anwenden von Hotfixes auf alle Cluster Knoten verwendet wird
  
Um anzugeben, dass Hotfixes für alle Cluster Knoten gelten, kopieren Sie Sie in einen Ordner mit dem Namen **cauhotfix\_alle** unter dem hotfixstamm Ordner. In diesem Beispiel ist das Plug\-in-Argument **hotfixrootfolderpath** auf *\\\\myfileserver\\Hotfixes\\root\\* festgelegt. Der **cauhotfix-\_Ordner alle** enthält drei Updates mit den Erweiterungen MSU, MSI und MSP, die auf alle Cluster Knoten angewendet werden. Die Namen der Updatedateien dienen nur zur Veranschaulichung.  
  
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
  
Um Hotfixes anzugeben, die nur auf einen bestimmten Knoten angewendet werden, verwenden Sie unter dem Hotfixstammordner einen Unterordner mit dem Namen dieses Knotens. Verwenden Sie den NetBIOS-Namen des Clusterknotens, z. B. *ContosoNode1*. Verschieben Sie dann die Updates, die nur für diesen Knoten gelten, in diesen Unterordner. Im folgenden Beispiel wird das\-Plug-in-Argument **hotfixrootfolderpath** auf *\\\\myfileserver\\Hotfixes\\root\\* festgelegt. Updates im **cauhotfix-\_alle** Ordner werden auf alle Cluster Knoten angewendet, und *Node1\_spezifische\_Update. msu* wird nur auf *ContosoNode1*angewendet.  
  
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
  
Das Plug-In **Microsoft.HotfixPlugin** wendet standardmäßig nur Updates mit den Erweiterungen MSU, MSI oder MSP an. Bestimmte Updates können jedoch andere Erweiterungen aufweisen und somit andere Installationsbefehle erfordern. Möglicherweise müssen Sie ein Firmwareupdate mit der Erweiterung EXE auf einen Knoten in einem Cluster anwenden. Sie können den hotfixstamm Ordner mit einem Unterordner konfigurieren, der angibt, dass ein bestimmter, nicht\-standardmäßiger Updatetyp installiert werden muss. Sie müssen auch eine entsprechende Ordnerinstallationsregel konfigurieren, die den Installationsbefehl im `<FolderRules>` -Element in der XML-Datei der Hotfixkonfiguration angibt.  
  
Im folgenden Beispiel wird das\-Plug-in-Argument **hotfixrootfolderpath** auf *\\\\myfileserver\\Hotfixes\\root\\* festgelegt. Es werden verschiedene Updates auf alle Clusterknoten angewendet. Zusätzlich wird das Firmwareupdate *SpecialHotfix1.exe* mithilfe von *FolderRule1* auf *ContosoNode1* angewendet. Weitere Informationen zum Konfigurieren von *ContosoNode1* in der Hotfixkonfigurationsdatei finden Sie weiter unten in diesem Abschnitt unter [Anpassen der Hotfixkonfigurationsdatei](#BKMK_CONFIG_FILE) .  
  
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
  
**% systemroot%\\System32\\WindowsPowerShell\\v 1.0\\Module\\clusterawareupdating-Ordner**  
  
Kopieren Sie die Beispielkonfigurationsdatei "DefaultHotfixConfig.xml" aus diesem Speicherort in den Hotfixstammordner, und nehmen Sie die entsprechenden Änderungen für Ihr Szenario vor, um die Hotfixkonfigurationsdatei anzupassen:  
  
> [!IMPORTANT]  
> Für die Anwendung der meisten von Microsoft bereitgestellten Hotfixes und anderer Updates kann die standardmäßige Hotfixkonfigurationsdatei ohne Änderungen verwendet werden. Die Anpassung der Hotfixkonfigurationsdatei zählt nur in fortgeschrittenen Verwendungsszenarios zu den erforderlichen Aufgaben.  
  
Standardmäßig definiert die XML-Datei der Hotfixkonfiguration die Installationsregeln und Beendigungsbedingungen für die folgenden beiden Kategorien von Hotfixes:  
  
-   Hotfixdateien mit Erweiterungen, die vom Plug\-in standardmäßig installiert werden können \(MSU-, MSI-und MSP-Dateien\).  
  
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
  
-   Hotfix oder andere Update Dateien, bei denen es sich nicht um MSI-, MSU-oder MSP-Dateien handelt, z. b. nicht\-Microsoft-Treiber, Firmware und BIOS-Updates.  
  
    Jeder nicht\-Standard Dateityp wird als `<Folder>`-Element im `<FolderRules>`-Element konfiguriert. Das Namensattribut des `<Folder>` -Elements muss mit dem Namen eines Ordners im Hotfixstammordner übereinstimmen, der Updates vom entsprechenden Typ enthalten wird. Der Ordner kann sich im **cauhotfix-\_alle** Ordner oder in einem Knoten\-bestimmten Ordner befinden. Wenn *FolderRule1* z. B. im Hotfixstammordner konfiguriert ist, konfigurieren Sie das folgende Element in der XML-Datei, damit es eine Installationsvorlage und Beendigungsbedingungen für die Updates in diesem Ordner definiert:  
  
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
|`<Success_RebootRequired>`|Definiert optional mindestens einen Beendigungscode, der darauf hinweist, dass das Update erfolgreich ausgeführt wurde und der Knoten neu gestartet werden muss. <br>**Hinweis:** Optional kann das `<Folder>`-Element das `alwaysReboot`-Attribut enthalten. Wenn dieses Attribut festgelegt ist, zeigt es an, dass wenn ein von dieser Regel installiertes Hotfix einen der Beendigungscodes zurückgibt, die in `<Success>`definiert sind, dieser als `<Success_RebootRequired>` -Beendigungsbedingung interpretiert wird.|  
|`<Fail_RebootRequired>`|Definiert optional mindestens einen Beendigungscode, der darauf hinweist, dass das Update nicht erfolgreich ausgeführt wurde und der Knoten neu gestartet werden muss.|  
|`<AlreadyInstalled>`|Definiert optional mindestens einen Beendigungscode, der darauf hinweist, dass das angegebene Update nicht angewendet wurde, da es bereits installiert ist.|  
|`<NotApplicable>`|Definiert optional mindestens einen Beendigungscode, der darauf hinweist, dass das angegebene Update nicht angewendet wurde, da es nicht für den Clusterknoten gilt.|  
  
> [!IMPORTANT]  
> Ein Beendigungscode, der in `<ExitConditions>` nicht explizit definiert ist, wird bei einem Fehler des Updates interpretiert und der Knoten wird nicht neu gestartet.  
  
### <a name="BKMK_ACL"></a>Einschränken des Zugriffs auf den hotfixstamm Ordner  
Sie müssen verschiedene Schritte ausführen, um den SMB-Dateiserver und die -Dateifreigabe so zu konfigurieren, dass sie den Schutz der Dateien im Hotfixstammordner nur für den Zugriff im Kontext von **Microsoft.HotfixPlugin**unterstützen. Diese Schritte aktivieren verschiedene Features, die dabei helfen, mögliche Manipulationen an den Hotfixdateien zu verhindern, die möglicherweise den Failovercluster gefährden können.  
  
Die allgemeinen Schritte sehen wie folgt aus:  
  
1.  Identifizieren Sie das Benutzerkonto, das für Update Ausführungen verwendet wird, indem Sie den Plug\-in  
  
2.  Konfigurieren dieses Benutzerkontos in den erforderlichen Gruppen auf einem SMB-Dateiserver  
  
3.  Konfigurieren der Berechtigungen für den Zugriff auf den Hotfixstammordner  
  
4.  Konfigurieren der Einstellungen für die SMB-Datenintegrität  
  
5.  Aktivieren der Windows-Firewall-Regel auf dem SMB-Server  
  
#### <a name="step-1-identify-the-user-account-that-is-used-for-updating-runs-by-using-the-hotfix-plug-in"></a>Schritt 1 Identifizieren Sie das Benutzerkonto, das für Update Ausführungen verwendet wird, indem Sie das Hotfix-Plug\-in verwenden.
  
Das Konto, das zum Überprüfen der Sicherheitseinstellungen beim Ausführen einer Update Ausführung mithilfe von **Microsoft. hotfixplugin** verwendet wird, hängt davon ab, ob das Cluster fähige aktualisieren im Remote-\-Aktualisierungs Modus oder im selbst\-Aktualisierungs Modus verwendet wird:  
  
-   **Remote\--Aktualisierungs Modus** Das Konto, das über Administratorrechte für den Cluster verfügt, um die Vorschau anzuzeigen und Updates anzuwenden.  
  
-   **Selbst\-Aktualisierungs Modus** Der Name des virtuellen Computer Objekts, das in Active Directory für die Cluster Rolle für Cluster fähiges aktualisieren konfiguriert ist. Dies ist entweder der Name eines vorab bereitgestellten virtuellen Computerobjekts in Active Directory für die Clusterrolle für clusterfähiges Aktualisieren oder der Name, der von der Clusterrolle für clusterfähiges Aktualisieren generiert wird. Wenn Sie den Namen abrufen möchten, wenn er von Cau generiert wurde, führen Sie das PowerShell-Cmdlet **Get\-cauclusterrole** Cau aus. In der Ausgabe ist **ResourceGroupName** der Name des generierten virtuellen Computerobjektkontos.  
  
#### <a name="step-2-configure-this-user-account-in-the-necessary-groups-on-an-smb-file-server"></a>Schritt 2 Konfigurieren dieses Benutzerkontos in den erforderlichen Gruppen auf einem SMB-Dateiserver
  
> [!IMPORTANT]  
> Sie müssen das für die Updateausführungen verwendete Konto als lokales Administratorkonto auf dem SMB-Server hinzufügen. Wenn dies aufgrund der Sicherheitsrichtlinien in Ihrer Organisation nicht zulässig ist, konfigurieren Sie dieses Konto auf dem SMB-Server mit den erforderlichen Berechtigungen, indem Sie das folgende Verfahren durchführen.  
  
##### <a name="to-configure-a-user-account-on-the-smb-server"></a>So konfigurieren Sie ein Benutzerkonto auf dem SMB-Server  
  
1.  Fügen Sie das für Updateausführungen verwendete Konto zur Gruppe „Distributed COM-Benutzer“ sowie zu einer der folgenden Gruppen hinzu: Hauptbenutzer, Servervorgang oder Druck-Operator.  
  
2.  Starten Sie die WMI-Verwaltungskonsole auf dem SMB-Server, um die erforderlichen WMI-Berechtigungen für das Konto zu aktivieren. Starten Sie PowerShell, und geben Sie dann den folgenden Befehl ein:  
  
    ```  
    wmimgmt.msc  
    ```  
  
3.  Klicken Sie in der Konsolen Struktur mit der rechten\-auf **WMI-Steuerung \(lokale\)** , und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie auf **Sicherheit**, und erweitern Sie dann **Stamm**.  
  
5.  Klicken Sie auf **CIMV2**und dann auf **Sicherheit**.  
  
6.  Fügen Sie das für Updateausführungen verwendete Konto zur Liste **Gruppen- oder Benutzernamen** hinzu.  
  
7.  Erteilen Sie dem für Updateausführungen verwendeten Konto die Berechtigungen **Methoden ausführen** und **Remoteaktivierung** .  
  
#### <a name="step-3-configure-permissions-to-access-the-hotfix-root-folder"></a>Schritt 3 Konfigurieren der Berechtigungen für den Zugriff auf den Hotfixstammordner
  
Wenn Sie versuchen, Updates anzuwenden, prüft das Hotfix-\-Plug-in in standardmäßig die Konfiguration der NTFS-Dateisystem Berechtigungen für den Zugriff auf den hotfixstamm Ordner. Wenn die Ordner Zugriffsberechtigungen nicht ordnungsgemäß konfiguriert sind, kann eine Update Ausführung mit dem Hotfix-Plug\-in fehlschlagen.  
  
Wenn Sie die Standardkonfiguration des Hotfix-Plug\-in verwenden, stellen Sie sicher, dass die Berechtigungen für den Ordner Zugriff den folgenden Anforderungen entsprechen.  
  
-   Die Gruppe "Benutzer" verfügt über die Berechtigung "Lesen".  
  
-   Wenn das Plug\-in Updates mit der Erweiterung exe anwendet, verfügt die Gruppe "Benutzer" über die Berechtigung "ausführen".  
  
-   Nur bestimmte Sicherheits Prinzipale sind \(zulässig, sind jedoch nicht erforderlich\) um die Berechtigung Schreiben oder ändern zu können. Die zulässigen Prinzipale sind die Gruppe der lokalen Administratoren, SYSTEM, ERSTELLER-BESITZER und TrustedInstaller. Anderen Konten oder Gruppen ist es nicht gestattet, die Berechtigung "Schreiben" oder "Ändern" für den Hotfixstammordner zu verwenden.  
  
Optional können Sie die obigen Prüfungen deaktivieren, die von der Plug\-in standardmäßig durchgeführt werden. Hierzu stehen Ihnen zwei Möglichkeiten zur Verfügung.  
  
-   Wenn Sie die PowerShell-Cmdlets für Cluster fähiges aktualisieren verwenden, konfigurieren Sie das-Argument **disableaclchecks\=' true '** im **caupluginarguments** -Parameter für das Hotfix-Plug\-in.  
  
-   Wenn Sie die Benutzeroberfläche für clusterfähiges Aktualisieren verwenden, wählen Sie die Option **Prüfung auf Administratorzugriff auf Hotfixstammordner und Konfigurationsdatei deaktivieren** auf der Seite **Weitere Updateoptionen** aus, die zum Konfigurieren der Optionen von Updateausführungen verwendet wird.  
  
Es wird jedoch in vielen Umgebungen als bewährte Methode empfohlen, dass Sie diese Prüfungen mithilfe der Standardkonfiguration erzwingen.  
  
#### <a name="step-4-configure-settings-for-smb-data-integrity"></a>Schritt 4 Konfigurieren der Einstellungen für die SMB-Datenintegrität
  
Zum Überprüfen der Datenintegrität in den Verbindungen zwischen den Cluster Knoten und der SMB-Dateifreigabe erfordert das Hotfix-Plug\-in, dass Sie die Einstellungen auf der SMB-Dateifreigabe für die SMB-Signatur oder SMB-Verschlüsselung aktivieren. Die SMB-Verschlüsselung, die in vielen Umgebungen eine höhere Sicherheit und bessere Leistung bietet, wird ab Windows Server 2012 unterstützt. Sie können eine oder beide Einstellungen wie folgt aktivieren:  
  
-   Informationen zum Aktivieren der SMB-Signatur finden Sie unter dem Verfahren in der Microsoft Knowledge Base in [Artikel 887429](https://support.microsoft.com/kb/887429) .  
  
-   Um die SMB-Verschlüsselung für den freigegebenen SMB-Ordner zu aktivieren, führen Sie das folgende PowerShell-Cmdlet auf dem SMB-Server aus:  
  
    ```PowerShell  
    Set-SmbShare <ShareName> -EncryptData $true  
    ```  
  
    Dabei gibt <*ShareName*> den Namen des freigegebenen SMB-Ordners an.  
  
Um optional die Verwendung der SMB-Verschlüsselung in den Verbindungen mit dem SMB-Server zu erzwingen, wählen Sie auf der Benutzeroberfläche für Cluster fähiges aktualisieren die Option **SMB-Verschlüsselung beim Zugriff auf hotfixstamm Ordner** anfordern aus, oder konfigurieren Sie die Option Requirements **smbencryption\="true"** Plug\-in-Argument mithilfe der Cau-PowerShell-Cmdlets.  
  
> [!IMPORTANT]  
> Wenn Sie die Option zum Erzwingen der Verwendung der SMB-Verschlüsselung auswählen und der Hotfixstammordner nicht für Verbindungen konfiguriert ist, die die SMB-Verschlüsselung verwenden, tritt bei der Updateausführung ein Fehler auf.  
  
#### <a name="step-5-enable-a-windows-firewall-rule-on-the-smb-server"></a>Schritt 5 Aktivieren der Windows-Firewall-Regel auf dem SMB-Server
  
Sie müssen die **Dateiserver-Remote Verwaltung \(SMB-\-in\)** Regel in der Windows-Firewall auf dem SMB-Dateiserver aktivieren. Dies ist in Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 standardmäßig aktiviert.  
  
## <a name="see-also"></a>Weitere Informationen  
  
-   [Übersicht über das Cluster fähige aktualisieren](cluster-aware-updating.md)
  
-   [Windows PowerShell-Cmdlets für Cluster fähiges aktualisieren](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating)  
  
-   [Plug-in-Referenz für Cluster fähiges aktualisieren](https://msdn.microsoft.com/library/hh418084.aspx)  
  
