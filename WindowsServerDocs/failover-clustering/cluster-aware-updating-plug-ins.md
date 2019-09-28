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

Beim [Cluster fähigen aktualisieren (Cluster-Aware Update](cluster-aware-updating.md) , Cau) werden Plug-ins verwendet, um die Installation von Updates auf Knoten in einem Failovercluster zu koordinieren. Dieses Thema enthält Informationen zur Verwendung der erstellten @ no__t-0in Cau-Plug @ no__t-1ins oder anderen Plug @ no__t-2ins, die Sie für Cau installieren.

## <a name="BKMK_INSTALL"></a>Installieren eines Plug-ins @ no__t-1In  
Ein Plug @ no__t-0in einem anderen als die standardmäßigen Plug @ no__t-1ins, die mit Cau installiert werden \(**Microsoft. windowsupdateplugin** und **Microsoft. hotfixplugin**\) müssen separat installiert werden. Wenn Cau im Self @ no__t-0update-Modus verwendet wird, muss das Plug @ no__t-1In auf allen Cluster Knoten installiert werden. Wenn Cau im Remote Modus @ no__t-0update verwendet wird, muss das Plug @ no__t-1In auf dem Remote Computer mit dem Update Koordinator installiert sein. Bei einem Plug @ no__t-0in, das Sie installieren, sind möglicherweise zusätzliche Installationsanforderungen auf den einzelnen Knoten erforderlich.  
  
Um ein Plug @ no__t-0in zu installieren, befolgen Sie die Anweisungen des Plug @ no__t-1Auf dem Verleger. Wenn Sie ein Plug @ no__t-0in mit Cau manuell registrieren möchten, führen Sie das [Register-cauplugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin) -Cmdlet auf jedem Computer aus, auf dem Plug @ no__t-2in installiert ist.  
  
## <a name="specify-a-plug-in-and-plug-in-arguments"></a>Geben Sie einen Plug @ no__t-0in-und einen Plug @ no__t-1In-Argument an.  
  
### <a name="specify-a-cau-plug-in"></a>Geben Sie ein CAU-Plug @ no__t-0in an.

Wählen Sie auf der Benutzeroberfläche für Cluster fähiges aktualisieren aus einer Drop @ no__t-1down-Liste der verfügbaren Plug @ no__t-2ins ein Plug @ no__t-0in aus, wenn Sie mit Cau die folgenden Aktionen ausführen:  
  
-   Anwenden von Updates auf Cluster  
  
-   Updatevorschau für Cluster  
  
-   Konfigurieren von Self @ no__t-Update Optionen für Cluster  
  
Standardmäßig wählt Cau den Plug @ no__t-0in **Microsoft. windowsupdateplugin**aus. Allerdings können Sie ein beliebiges Plug @ no__t-0in angeben, das in Cau installiert und registriert ist.

> [!TIP]  
> In der Benutzeroberfläche für Cluster fähiges aktualisieren können Sie nur ein einzelnes Plug @ no__t-0in für das Cluster fähige aktualisieren angeben, das für die Vorschauversion oder für die Anwendung von Updates während einer Update Laufzeit verwendet werden soll. Mithilfe der PowerShell-Cmdlets für Cluster fähiges aktualisieren können Sie mindestens ein Plug @ no__t-0ins angeben. Wenn Sie mehrere Arten von Updates auf dem Cluster installieren müssen, ist es in der Regel effizienter, mehrere Plug @ no__t-0ins in einer Update Laufzeit anzugeben, anstatt für jeden Plug @ no__t-1In eine separate Update-Laufzeit zu verwenden. Dadurch sind z. B. meist weniger Knotenneustarts erforderlich.

Mithilfe der in der folgenden Tabelle aufgeführten PowerShell-Cmdlets für Cluster fähiges aktualisieren können Sie mindestens ein Plug @ no__t-0ins für eine Update-oder Scanvorgang angeben, indem Sie den **– caupluginname** -Parameter übergeben. Sie können mehrere Plug @ no__t-0in-Namen angeben, indem Sie Sie durch Kommas trennen. Wenn Sie mehrere Plug @ no__t-0ins angeben, können Sie auch steuern, wie sich die Plug @ no__t-1ins während einer Update Ausführung gegenseitig beeinflussen, indem Sie die **\-runpluginsseridal**, **\-stoponpluginfailure**und **– separaterestarts angeben.** Parameter. Weitere Informationen zur Verwendung mehrerer Plug-in-no__t-0ins finden Sie unter den Links, die für die Cmdlet-Dokumentation in der folgenden Tabelle bereitgestellt werden.  
  
|Cmdlet|Beschreibung|  
|----------|---------------|  
|[Add-cauclusterrole](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/add-cauclusterrole)|Fügt die Cluster Rolle für Cluster fähiges aktualisieren hinzu, die die Self @ no__t-0update-Funktionalität für den angegebenen Cluster bereitstellt.|  
|[Aufrufen: caurun](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/invoke-caurun)|Prüft Clusterknoten auf geeignete Updates und installiert diese Updates über eine Updateausführung auf dem angegebenen Cluster.|  
|[Aufrufen: kauscan](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/invoke-causcan)|Prüft Clusterknoten auf geeignete Updates und gibt eine Liste des ersten Updatesatzes zurück, der auf jeden Knoten des angegebenen Clusters angewendet werden würde.|  
|[Set-cauclusterrole](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/set-cauclusterrole)|Legt Konfigurationseigenschaften für die Clusterrolle für clusterfähiges Aktualisieren auf dem angegebenen Cluster fest.|  
  
Wenn Sie mit diesen Cmdlets keinen Cau-Plug @ no__t-0in-Parameter angeben, ist der Standardwert Plug @ no__t-1In **Microsoft. windowsupdateplugin**.  
  
### <a name="specify-cau-plug-in-arguments"></a>Cau-Plug @ no__t-0in-Argumente angeben  
Wenn Sie die Optionen für die Aktualisierungs Laufzeit konfigurieren, können Sie einen oder mehrere *Namen @ no__t-1value* -Paare \(arguments @ no__t-3 angeben, die für das ausgewählte Plug @ no__t-4in verwendet werden sollen. Auf der Benutzeroberfläche für clusterfähiges Aktualisieren können Sie z. B. wie folgt mehrere Argumente angeben:  
  
**Name1 @ no__t-1value1; Name2 @ no__t-2value2; Name3 @ no__t-3value3**  
  
Diese *Namen @ no__t-1value-* Paare müssen für das von Ihnen angegebene Plug @ no__t-2in sinnvoll sein. Bei manchen Plug @ no__t-0ins sind die Argumente optional.  
  
Die Syntax der Cau-Plug @ no__t-0in-Argumente befolgt diese allgemeinen Regeln:  
  
-   Multiple *Name @ no__t-1value-* Paare werden durch Semikolons getrennt.  
  
-   Ein Leerzeichen enthaltender Wert wird in Anführungszeichen gestellt. Beispiel: **Name1 @ no__t-1 "Wert mit Leerzeichen"** .  
  
-   Die genaue Syntax des *Werts* hängt von dem Plug @ no__t-1In ab.  
  
Zum Angeben von Plug @ no__t-0in-Argumenten mithilfe der Cau-PowerShell-Cmdlets, die den Parameter **– caupluginparameters** unterstützen, übergeben Sie einen Parameter in der Form:  
  
**\-caupluginarguments @ {Name1 @ no__t-2value1; Name2 @ no__t-3value2; Name3 @ no__t-4value3}**  
  
Sie können auch eine vordefinierte PowerShell-Hash Tabelle verwenden. Um Plug @ no__t-0in-Argumente für mehr als ein Plug @ no__t-1In anzugeben, übergeben Sie mehrere Hash Tabellen mit Argumenten, die durch Kommas getrennt sind. Übergeben Sie die Plug @ no__t-0in-Argumente im Plug @ no__t-1In der Reihenfolge, die in **caupluginname**angegeben ist.  
  
### <a name="specify-optional-plug-in-arguments"></a>Optionale Plug @ no__t-0in-Argumente angeben  
Die Plug-in-no__t-0ins, die von Cau installiert werden \(**Microsoft. windowsupdateplugin** und **Microsoft. hotfixplugin**\) bieten zusätzliche Optionen, die Sie auswählen können. Diese werden auf der Benutzeroberfläche für Cluster fähiges aktualisieren auf der Seite **zusätzliche Optionen** angezeigt, nachdem Sie die Optionen für die Update Ausführung für das Plug @ no__t-1In konfiguriert haben. Wenn Sie die PowerShell-Cmdlets für Cluster fähiges aktualisieren verwenden, werden diese Optionen als optionale Plug @ no__t-0in-Argumente konfiguriert. Weitere Informationen finden Sie unter [Verwenden von "Microsoft.WindowsUpdatePlugin"](#BKMK_WUP) und [Verwenden von "Microsoft.HotfixPlugin"](#BKMK_HFP) weiter unten in diesem Thema.  
  
## <a name="manage-plug-ins-using-windows-powershell-cmdlets"></a>Verwalten von Plug-in-no__t-0ins mithilfe von Windows PowerShell-Cmdlets  
  
|Cmdlet|Beschreibung|  
|----------|---------------|  
|[Get-cauplugin](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/get-cauplugin)|Ruft Informationen zu mindestens einem softwareupdateaktualisierungs-Plug-in no__t-0ins ab, die auf dem lokalen Computer registriert sind.|  
|[Register-cauplugin]((https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/register-cauplugin))|Registriert ein CAU-Softwareupdateverteilungs-Plug @ no__t-0in auf dem lokalen Computer.|  
|[Unregister-cauplugin](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/unregister-cauplugin)|Entfernt ein Software Update-Plug @ no__t-0in aus der Liste der Plug @ no__t-1ins, die von Cau verwendet werden können. **Hinweis**: Bei den mit Cau \(**Microsoft. windowsupdateplugin** und **Microsoft. hotfixplugin**\) installierten Plug @ no__t-0ins kann die Registrierung nicht aufgehoben werden.|  
  
## <a name="BKMK_WUP"></a>Verwenden von "Microsoft. windowsupdateplugin"  

Das Standard-Plug @ no__t-0in für Cau, **Microsoft. windowsupdateplugin**, führt die folgenden Aktionen aus:
- Das Plug-In steht in Kontakt mit dem Windows Update-Agent auf den einzelnen Knoten des Failoverclusters, um Updates für die Microsoft-Produkte anzuwenden, die auf den einzelnen Knoten ausgeführt werden.
- Installiert Cluster Updates direkt von Windows Update oder Microsoft Update bzw. von einem auf @ no__t-0lokal Windows Server Update Services \(wsus @ no__t-2 Server.
- Installiert nur die ausgewählte allgemeine Verteilungs Version \(ddr @ no__t-1 Updates. Standardmäßig wendet das Plug @ no__t-0in nur wichtige Software Updates an. Es ist keine Konfiguration erforderlich. Die Standardkonfiguration lädt wichtige Updates von allgemeinen Vertriebsversionen auf die einzelnen Knoten herunter und installiert sie. 

> [!NOTE]
> Wenn Sie andere Updates als die wichtigen Software Updates anwenden möchten, die standardmäßig ausgewählt sind @no__t z. b. Treiber Updates @ no__t-1, können Sie einen optionalen Parameter "Plug @ no__t-2in" konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren der Abfragezeichenfolge für den Windows Update-Agent](#BKMK_QUERY).

### <a name="requirements"></a>Anforderungen

- Der Failovercluster und der Remote Update Koordinator-Computer \(if used @ no__t-1 müssen die Anforderungen für Cau und die Konfiguration erfüllen, die für die Remote Verwaltung in [Anforderungen und bewährten Methoden für Cau](cluster-aware-updating-requirements.md)erforderlich ist.
- Lesen Sie die [Empfehlungen für die Anwendung von Microsoft-Updates](cluster-aware-updating-requirements.md#BKMK_BP_WUA), und nehmen Sie dann alle erforderlichen Änderungen an der Microsoft-Updatekonfiguration für die Failoverclusterknoten vor.
- Um optimale Ergebnisse zu erzielen, empfiehlt es sich, das Cau-Best Practices Analyzer \(bpa @ no__t-1 auszuführen, um sicherzustellen, dass die Cluster-und Update Umgebung ordnungsgemäß für die Anwendung von Updates mithilfe von Cau konfiguriert sind. Weitere Informationen finden Sie unter [Testen der Updatebereitschaft für clusterfähiges Aktualisieren](cluster-aware-updating-requirements.md#BKMK_BPA).

> [!NOTE]
> Updates, die das Akzeptieren von Microsoft-Lizenzbedingungen oder andere Benutzerinteraktionen erfordern, werden ausgeschlossen und müssen manuell installiert werden.

### <a name="additional-options"></a>Zusätzliche Optionen

Optional können Sie die folgenden Plug-in-no__t-0in-Argumente angeben, um den Satz der Updates zu vergrößern oder einzuschränken, die von Plug @ no__t-1In angewendet werden:
- Wählen Sie auf der Benutzeroberfläche für Cluster fähiges aktualisieren auf der Seite zusätzliche Optionen auf der Seite **zusätzliche Optionen die Option** **Empfohlene Updates auf die gleiche Weise wie wichtige Updates** überprüfen aus, um das Plug @ no__t-0in zum Anwenden empfohlener Updates zu konfigurieren. Chens.
<br>Alternativ dazu können Sie das Argument **"includerecommendedupdates" \= ' true '** Plug @ no__t-2in-Argument konfigurieren.
- Um das Plug @ no__t-0in so zu konfigurieren, dass es die Typen von DDR-Updates filtert, die auf die einzelnen Cluster Knoten angewendet werden, geben Sie eine Abfrage Zeichenfolge für den Windows Update-Agent mithilfe eines **QueryString** -Plug @ no__t-2in Weitere Informationen finden Sie unter [Konfigurieren der Abfragezeichenfolge für den Windows Update-Agent](#BKMK_QUERY).

### <a name="BKMK_QUERY"></a>Konfigurieren der Abfrage Zeichenfolge für Windows Update-Agent  
Sie können ein Plug @ no__t-0in-Argument für das Standard-Plug @ no__t-1In, **Microsoft. windowsupdateplugin**, konfigurieren, das aus einem Windows Update-Agent \(wua @ no__t-4-Abfrage Zeichenfolge besteht. Diese Anweisung verwendet die WUA-API, um eine oder mehrere Gruppen von Microsoft-Updates zu ermitteln, die auf Basis bestimmter Auswahlkriterien auf die einzelnen Knoten angewendet werden. Sie können mehrere Kriterien mithilfe einer logischen UND- oder ODER-Operation kombinieren. Die WUA-Abfrage Zeichenfolge wird wie folgt in einem Plug @ no__t-0in-Argument angegeben:  
  
**QueryString @ no__t-1 "Kriterium1 @ no__t-2value1 und @ no__t-3or Criterion2 @ no__t-4value2 und @ no__t-5or..."**  
  
**Microsoft.WindowsUpdatePlugin** wählt z. B. wichtige Updates automatisch mithilfe des Standardarguments **QueryString** aus, das mit den Kriterien **IsInstalled**, **Type**, **IsHidden** und **IsAssigned** erzeugt wird:  
  
**QueryString @ no__t-1 "isingestrandet @ no__t-20 und Type @ no__t-3' Software ' and IsHidden @ no__t-40 and isassigned @ no__t-51"**  
  
Wenn Sie ein **QueryString** -Argument angeben, wird es anstelle des standardmäßigen **QueryString** -Arguments verwendet, das für das Plug @ no__t-2in konfiguriert ist.  
  
#### <a name="example-1"></a>Beispiel 1
  
So konfigurieren Sie ein **QueryString** -Argument, das ein bestimmtes Update installiert, wie durch ID *f6ce46c1 @ no__t-2971c @ no__t-343f9 @ no__t-4a2aa @ no__t-5783df125f003*:  
  
**QueryString @ no__t-1 "UpdateId @ no__t-2' f & 6ce46c1 @ no__t-3971c @ no__t-443f @ no__t-5a2aa @ no__t-6783df125-ID" und isingestrandet @ no__t-70 "**  
  
> [!NOTE]  
> Das vorherige Beispiel gilt für die Anwendung von Updates mithilfe des Cluster-Assistenten zum Aktualisieren von @ no__t 0aware. Wenn Sie ein bestimmtes Update durch Konfigurieren von Self @ no__t-0update-Optionen über die Benutzeroberfläche für Cluster fähiges aktualisieren oder mithilfe des PowerShell-Cmdlets **Add @ no__t-2cauclusterrole** oder **Set @ no__t-4cauclusterrole**installieren möchten, müssen Sie den UpdateId-Wert mit zwei Werten formatieren. Single @ no__t-5anführungs Zeichen:  
>   
> **QueryString @ no__t-1 "UpdateId @ no__t-2or ' f 6ce46c1 @ no__t-3971c @ no__t-443f @ no__t-5a2aa @ no__t-6783df125" "und isinstemstemter @ no__t-70"**  
  
#### <a name="example-2"></a>Beispiel 2
  
So konfigurieren Sie ein **QueryString**-Argument, das ausschließlich Treiber installiert  
  
**QueryString @ no__t-1 "isingestrandet @ no__t-20 und Type @ no__t-3' Driver ' and IsHidden @ no__t-40"**  
  
Weitere Informationen zu Abfrage Zeichenfolgen für das Standard-Plug @ no__t-0in, **Microsoft. windowsupdateplugin**, die Suchkriterien \(WIE z. b. **isingestrandet**\) und die Syntax, die Sie in die Abfrage Zeichenfolgen einschließen können, finden Sie im Abschnitt. Informationen zu Suchkriterien in der API-Referenz für den [Windows Update-Agent (WUA)](https://go.microsoft.com/fwlink/p/?LinkId=223304).  
  
## <a name="BKMK_HFP"></a>Verwenden von Microsoft. hotfixplugin  
Der Plug @ no__t-0in **Microsoft. hotfixplugin** kann verwendet werden, um die Microsoft Limited Distribution Release \(ldr @ no__t-3 Updates \(Auch als Hotfixes bezeichnet und ehemals QFEs @ no__t-5 zu verwenden, die Sie unabhängig von der Adresse herunterladen. bestimmte Microsoft-Software Probleme. Das Plug-in installiert Updates aus einem Stamm Ordner auf einer SMB-Dateifreigabe und kann auch so angepasst werden, dass Sie nicht-@ no__t-0Microsoft-Treiber, Firmware und BIOS-Updates anwendet.

> [!NOTE]
> In Knowledge Base-Artikeln können Hotfixes gelegentlich von Microsoft heruntergeladen werden. Sie werden jedoch auch für Kunden auf der Basis von "@ no__t-0benötigter" bereitgestellt.

### <a name="requirements"></a>Anforderungen

- Der Failovercluster und der Remote Update Koordinator-Computer \(if used @ no__t-1 müssen die Anforderungen für Cau und die Konfiguration erfüllen, die für die Remote Verwaltung in [Anforderungen und bewährten Methoden für Cau](cluster-aware-updating-requirements.md)erforderlich ist.
- Lesen Sie hierzu [Empfehlungen zur Verwendung von Microsoft.HotfixPlugin](cluster-aware-updating-requirements.md#BKMK_BP_HF).
- Um optimale Ergebnisse zu erzielen, empfiehlt es sich, das Modell Cau Best Practices Analyzer \(bpa @ no__t-1 auszuführen, um sicherzustellen, dass die Cluster-und Update Umgebung ordnungsgemäß für die Anwendung von Updates mithilfe von Cau konfiguriert sind. Weitere Informationen finden Sie unter [Testen der Updatebereitschaft für clusterfähiges Aktualisieren](cluster-aware-updating-requirements.md#BKMK_BPA).
- Rufen Sie die Updates vom Verleger ab, kopieren Sie Sie, oder extrahieren Sie Sie auf einen Server Message Block \(smb @ no__t-1 Dateifreigabe \(hotfix Stamm Ordner @ no__t-3, der mindestens SMB 2,0 unterstützt und auf die alle Cluster Knoten und das Remote Update zugreifen können. Der koordinatorcomputer \(if Cau wird im Remote @ no__t-5update Mode @ no__t-6 verwendet. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Konfigurieren einer Hotfixstammordnerstruktur](#BKMK_HF_ROOT). 

    > [!NOTE]
    > Standardmäßig werden von diesem Plug @ no__t-0in nur Hotfixes mit den folgenden Dateinamen Erweiterungen installiert: MSU, MSI und MSP.

- Kopieren Sie die Datei "defaulthotfixconfig. xml" \(, die im Ordner " **% systemroot% \\system32 @ no__t-3windowspowershell @ no__t-4V 1.0 @ no__t-5modules @ no__t-6clusterawareupdating** " auf einem Computer bereitgestellt wird, auf dem die Cau-Tools installiert @ no__t-7 in den hotfixstamm Ordner, den Sie erstellt haben und in dem Sie die Hotfixes extrahiert haben. Kopieren Sie z. b. die Konfigurationsdatei in *\\ @ no__t-2myfileserver @ no__t-3hotfixes @ no__t-4root @ no__t-5*. 

    > [!NOTE]
    > Für die Installation der meisten von Microsoft bereitgestellten Hotfixes und anderer Updates kann die standardmäßige Hotfixkonfigurationsdatei ohne Änderungen verwendet werden. Sie können die Konfigurationsdatei als erweiterte Aufgabe anpassen, wenn dies in Ihrem Szenario erforderlich ist. Die Konfigurationsdatei kann benutzerdefinierte Regeln enthalten, z. B. zum Behandeln von Hotfixdateien mit spezieller Erweiterung oder zum Definieren eines Verhaltens für bestimmte Beendigungsbedingungen. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Anpassen der Hotfixkonfigurationsdatei](#BKMK_CONFIG_FILE).

### <a name="configuration"></a>Konfiguration

Konfigurieren Sie die folgenden Einstellungen. Weitere Informationen finden Sie über die Links zu weiter unten in diesem Thema folgenden Abschnitten.
- Der Pfad zum freigegebenen Hotfixstammordner, der die anzuwendenden Updates und die Hotfixkonfigurationsdatei enthält. Sie können diesen Pfad auf der Cau-Benutzeroberfläche eingeben oder den **hotfixrootfolderpath @ no__t-1 @ no__t-2path >** PowerShell-Plug @ no__t-3in-Argument konfigurieren. 

   > [!NOTE]
   > Sie können den hotfixstamm Ordner als lokalen Ordner Pfad oder als UNC-Pfad in der Form *\\ @ no__t-2servername @ no__t-3share @ no__t-4rootfoldername*angeben. Ein Domänen basierter oder eigenständiger DFS-Namespace Pfad kann verwendet werden. Die Plug @ no__t-0in-Funktionen, die die Zugriffsberechtigungen in der hotfixkonfigurationsdatei überprüfen, sind jedoch nicht mit einem DFS-Namespace Pfad kompatibel. Wenn Sie also eine konfigurieren, müssen Sie die Überprüfung der Zugriffsberechtigungen über die Benutzeroberfläche für Cluster fähiges aktualisieren oder durch Konfigurieren des  **Disableaclchecks @ no__t-2' true '** Plug @ no__t-3in-Argument.
- Einstellungen auf dem Server, der den hotfixstamm Ordner hostet, um entsprechende Berechtigungen für den Zugriff auf den Ordner zu überprüfen und die Integrität der Daten sicherzustellen, auf die über den freigegebenen SMB-Ordner zugegriffen wird \(smb-Signatur oder SMB-Verschlüsselung @ no__t-1 Weitere Informationen finden Sie unter [Einschränken des Zugriffs auf den Hotfixstammordner](#BKMK_ACL).

### <a name="additional-options"></a>Zusätzliche Optionen

- Optional können Sie den Plug @ no__t-0in so konfigurieren, dass die SMB-Verschlüsselung beim Zugriff auf Daten von der hotfixdateifreigabe erzwungen wird. Wählen Sie auf der Benutzeroberfläche für Cluster fähiges aktualisieren auf der Seite **zusätzliche Optionen** die Option **SMB-Verschlüsselung beim Zugriff auf hotfixstamm Ordner** anfordern aus, oder konfigurieren Sie das PowerShell-Plug @ no__t-4in-Argument **"Requirements smbencryption @ no__t-3' true"** . 
  > [!IMPORTANT]
  > Sie müssen auf dem SMB-Server zusätzliche Konfigurationsschritte ausführen, um die SMB-Datenintegrität mithilfe der SMB-Signatur oder SMB-Verschlüsselung zu ermöglichen. Weitere Informationen finden Sie unter Schritt 4 in [Einschränken des Zugriffs auf den Hotfixstammordner](#BKMK_ACL). Wenn Sie die Option zum Erzwingen der Verwendung der SMB-Verschlüsselung auswählen und der Hotfixstammordner nicht für den Zugriff mit SMB-Verschlüsselung konfiguriert ist, tritt bei der Updateausführung ein Fehler auf.
- Deaktivieren Sie optional die Standardprüfungen auf ausreichende Berechtigungen für den Hotfixstammordner und die Hotfixkonfigurationsdatei. Wählen Sie auf der Benutzeroberfläche für Cluster fähiges aktualisieren die Option **Prüfung auf Administrator Zugriff auf hotfixstamm Ordner und Konfigurationsdatei deaktivieren aus**, oder konfigurieren Sie das Argument **disableaclchecks @ no__t-2' true '** Plug @ no__t-3in.
- Konfigurieren Sie optional das Argument **hotfixinstallertimeoutminutes @ no__t-1 @ no__t-2** , um anzugeben, wie lange das Hotfix-Plug-in von no__t-3in wartet, bis der hotfixinstallationsprozess zurückgegeben wird. \(der Standardwert ist 30 Minuten. \) Wenn Sie z. b. einen Timeout Zeitraum von zwei Stunden angeben möchten, legen Sie **hotfixinstallertimeoutminutes @ no__t-1120**fest.
- Konfigurieren Sie optional das Argument **hotfixconfigfilename \= <name>** Plug @ no__t-3in, um einen Namen für die hotfixkonfigurationsdatei anzugeben, die sich im hotfixstamm Ordner befindet. Wenn der Name nicht angegeben wird, lautet der Standardname "DefaultHotfixConfig.xml".
  
### <a name="BKMK_HF_ROOT"></a>Konfigurieren einer hotfixstamm Ordnerstruktur

Damit das Hotfix-Plug-in "no__t-0in" funktioniert, müssen die Hotfixes in einer "Well @ no__t-1"-Struktur in einer SMB-Dateifreigabe \(hotfix-Stamm Ordner @ no__t-3 gespeichert werden, und Sie müssen das Hotfix-Plug-in mit dem Pfad zum hotfixstamm Ordner über die Benutzeroberfläche von Cau oder die Cau-PowerShell-Cmdlets. Dieser Pfad wird als **hotfixrootfolderpath** -Argument an das Plug @ no__t-0in-Argument übermittelt. Gemäß Ihrer Aktualisierungsanforderungen können Sie für den Hotfixstammordner eine von vielen Strukturen auswählen, wie in den folgenden Beispielen gezeigt. Dateien oder Ordner, die der Struktur nicht entsprechen, werden ignoriert.  
  
#### <a name="example-1---folder-structure-used-to-apply-hotfixes-to-all-cluster-nodes"></a>Beispiel 1: Ordnerstruktur, die zum Anwenden von Hotfixes auf alle Cluster Knoten verwendet wird
  
Um anzugeben, dass Hotfixes für alle Cluster Knoten gelten, kopieren Sie Sie in einen Ordner mit dem Namen **cauhotfix @ no__t-1All** unter dem hotfixstamm Ordner. In diesem Beispiel ist das **hotfixrootfolderpath** -Plug @ no__t-1In-Argument auf *\\ @ no__t-4myfileserver @ no__t-5hotfixes @ no__t-6root @ no__t-7*festgelegt. Der Ordner **cauhotfix @ no__t-1All** enthält drei Updates mit den Erweiterungen MSU, MSI und MSP, die auf alle Cluster Knoten angewendet werden. Die Namen der Updatedateien dienen nur zur Veranschaulichung.  
  
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
  
Um Hotfixes anzugeben, die nur auf einen bestimmten Knoten angewendet werden, verwenden Sie unter dem Hotfixstammordner einen Unterordner mit dem Namen dieses Knotens. Verwenden Sie den NetBIOS-Namen des Clusterknotens, z. B. *ContosoNode1*. Verschieben Sie dann die Updates, die nur für diesen Knoten gelten, in diesen Unterordner. Im folgenden Beispiel wird das **hotfixrootfolderpath** -Plug @ no__t-1In-Argument auf *\\ @ no__t-4myfileserver @ no__t-5hotfixes @ no__t-6root @ no__t-7*festgelegt. Updates im Ordner **cauhotfix @ no__t-1All** werden auf alle Cluster Knoten angewendet, und *Node1 @ no__t-3Specific\_Update.msu* wird nur auf *ContosoNode1*angewendet.  
  
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
  
Das Plug-In **Microsoft.HotfixPlugin** wendet standardmäßig nur Updates mit den Erweiterungen MSU, MSI oder MSP an. Bestimmte Updates können jedoch andere Erweiterungen aufweisen und somit andere Installationsbefehle erfordern. Möglicherweise müssen Sie ein Firmwareupdate mit der Erweiterung EXE auf einen Knoten in einem Cluster anwenden. Sie können den hotfixstamm Ordner mit einem Unterordner konfigurieren, der angibt, dass ein bestimmter, nicht @ no__t-0default-Updatetyp installiert werden muss. Sie müssen auch eine entsprechende Ordnerinstallationsregel konfigurieren, die den Installationsbefehl im `<FolderRules>` -Element in der XML-Datei der Hotfixkonfiguration angibt.  
  
Im folgenden Beispiel wird das **hotfixrootfolderpath** -Plug @ no__t-1In-Argument auf *\\ @ no__t-4myfileserver @ no__t-5hotfixes @ no__t-6root @ no__t-7*festgelegt. Es werden verschiedene Updates auf alle Clusterknoten angewendet. Zusätzlich wird das Firmwareupdate *SpecialHotfix1.exe* mithilfe von *FolderRule1* auf *ContosoNode1* angewendet. Weitere Informationen zum Konfigurieren von *ContosoNode1* in der Hotfixkonfigurationsdatei finden Sie weiter unten in diesem Abschnitt unter [Anpassen der Hotfixkonfigurationsdatei](#BKMK_CONFIG_FILE) .  
  
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
  
**% systemroot% \\system32 @ no__t-2windowspowershell @ no__t-3V 1.0 @ no__t-4modules @ no__t-5clusterawareupdating-Ordner**  
  
Kopieren Sie die Beispielkonfigurationsdatei "DefaultHotfixConfig.xml" aus diesem Speicherort in den Hotfixstammordner, und nehmen Sie die entsprechenden Änderungen für Ihr Szenario vor, um die Hotfixkonfigurationsdatei anzupassen:  
  
> [!IMPORTANT]  
> Für die Anwendung der meisten von Microsoft bereitgestellten Hotfixes und anderer Updates kann die standardmäßige Hotfixkonfigurationsdatei ohne Änderungen verwendet werden. Die Anpassung der Hotfixkonfigurationsdatei zählt nur in fortgeschrittenen Verwendungsszenarios zu den erforderlichen Aufgaben.  
  
Standardmäßig definiert die XML-Datei der Hotfixkonfiguration die Installationsregeln und Beendigungsbedingungen für die folgenden beiden Kategorien von Hotfixes:  
  
-   Hotfixdateien mit Erweiterungen, die vom Plug-in-no__t-0in standardmäßig installiert werden können @no__t -1. msu,. msi und. msp-Dateien @ no__t-2.  
  
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
  
-   Hotfix oder andere Update Dateien, bei denen es sich nicht um MSI-, MSU-oder MSP-Dateien handelt, z. b. nicht @ no__t-0Microsoft-Treiber, Firmware und BIOS-Updates.  
  
    Jeder nicht-@ no__t-0default-Dateityp wird als `<Folder>`-Element im `<FolderRules>`-Element konfiguriert. Das Namensattribut des `<Folder>` -Elements muss mit dem Namen eines Ordners im Hotfixstammordner übereinstimmen, der Updates vom entsprechenden Typ enthalten wird. Der Ordner kann sich im Ordner **cauhotfix @ no__t-1All** oder im Ordner @ no__t-2specific befinden. Wenn *FolderRule1* z. B. im Hotfixstammordner konfiguriert ist, konfigurieren Sie das folgende Element in der XML-Datei, damit es eine Installationsvorlage und Beendigungsbedingungen für die Updates in diesem Ordner definiert:  
  
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
  
1.  Identifizieren Sie das Benutzerkonto, das für Update Ausführungen verwendet wird, indem Sie Plug @ no__t-0in verwenden.  
  
2.  Konfigurieren dieses Benutzerkontos in den erforderlichen Gruppen auf einem SMB-Dateiserver  
  
3.  Konfigurieren der Berechtigungen für den Zugriff auf den Hotfixstammordner  
  
4.  Konfigurieren der Einstellungen für die SMB-Datenintegrität  
  
5.  Aktivieren der Windows-Firewall-Regel auf dem SMB-Server  
  
#### <a name="step-1-identify-the-user-account-that-is-used-for-updating-runs-by-using-the-hotfix-plug-in"></a>Schritt 1 Identifizieren Sie das Benutzerkonto, das für Update Ausführungen verwendet wird, mithilfe des Hotfix-Plug-ins @ no__t-0in
  
Das Konto, das zum Überprüfen der Sicherheitseinstellungen beim Ausführen einer Update Ausführung mithilfe von **Microsoft. hotfixplugin** verwendet wird, hängt davon ab, ob das Cluster fähige aktualisieren im Remote @ no__t-1Update-Modus oder im Self @ no__t-2Update-Modus verwendet wird:  
  
-   **Remote @ no__t-1Update-Modus** Das Konto, das über Administratorrechte für den Cluster verfügt, um die Vorschau anzuzeigen und Updates anzuwenden.  
  
-   **Self @ no__t-1aktualisierungs Modus** Der Name des virtuellen Computer Objekts, das in Active Directory für die Cluster Rolle für Cluster fähiges aktualisieren konfiguriert ist. Dies ist entweder der Name eines vorab bereitgestellten virtuellen Computerobjekts in Active Directory für die Clusterrolle für clusterfähiges Aktualisieren oder der Name, der von der Clusterrolle für clusterfähiges Aktualisieren generiert wird. Wenn Sie den Namen abrufen möchten, wenn er von Cau generiert wird, führen Sie das PowerShell-Cmdlet **Get @ no__t-1cauclusterrole** Cau aus. In der Ausgabe ist **ResourceGroupName** der Name des generierten virtuellen Computerobjektkontos.  
  
#### <a name="step-2-configure-this-user-account-in-the-necessary-groups-on-an-smb-file-server"></a>Schritt 2 Konfigurieren dieses Benutzerkontos in den erforderlichen Gruppen auf einem SMB-Dateiserver
  
> [!IMPORTANT]  
> Sie müssen das für die Updateausführungen verwendete Konto als lokales Administratorkonto auf dem SMB-Server hinzufügen. Wenn dies aufgrund der Sicherheitsrichtlinien in Ihrer Organisation nicht zulässig ist, konfigurieren Sie dieses Konto auf dem SMB-Server mit den erforderlichen Berechtigungen, indem Sie das folgende Verfahren durchführen.  
  
##### <a name="to-configure-a-user-account-on-the-smb-server"></a>So konfigurieren Sie ein Benutzerkonto auf dem SMB-Server  
  
1.  Fügen Sie das für Updateausführungen verwendete Konto zur Gruppe "Distributed COM-Benutzer" sowie zu einer der folgenden Gruppen hinzu: Hauptbenutzer, Servervorgang oder Druck-Operator.  
  
2.  Starten Sie die WMI-Verwaltungskonsole auf dem SMB-Server, um die erforderlichen WMI-Berechtigungen für das Konto zu aktivieren. Starten Sie PowerShell, und geben Sie dann den folgenden Befehl ein:  
  
    ```  
    wmimgmt.msc  
    ```  
  
3.  Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf no__t- **WMI-Steuerung \(local @ no__t-3**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie auf **Sicherheit**, und erweitern Sie dann **Stamm**.  
  
5.  Klicken Sie auf **CIMV2**und dann auf **Sicherheit**.  
  
6.  Fügen Sie das für Updateausführungen verwendete Konto zur Liste **Gruppen- oder Benutzernamen** hinzu.  
  
7.  Erteilen Sie dem für Updateausführungen verwendeten Konto die Berechtigungen **Methoden ausführen** und **Remoteaktivierung** .  
  
#### <a name="step-3-configure-permissions-to-access-the-hotfix-root-folder"></a>Schritt 3 Konfigurieren der Berechtigungen für den Zugriff auf den Hotfixstammordner
  
Wenn Sie versuchen, Updates anzuwenden, prüft das Hotfix-Plug-in @ no__t-0in standardmäßig die Konfiguration der NTFS-Dateisystem Berechtigungen für den Zugriff auf den hotfixstamm Ordner. Wenn die Ordner Zugriffsberechtigungen nicht ordnungsgemäß konfiguriert sind, kann eine Update Ausführung mit dem Hotfix-Plug-in no__t-0in fehlschlagen.  
  
Wenn Sie die Standardkonfiguration des Hotfix-Plug-ins @ no__t-0in verwenden, stellen Sie sicher, dass die Berechtigungen für den Ordner Zugriff den folgenden Anforderungen entsprechen.  
  
-   Die Gruppe "Benutzer" verfügt über die Berechtigung "Lesen".  
  
-   Wenn das Plug @ no__t-0in Updates mit der Erweiterung exe anwendet, verfügt die Gruppe "Benutzer" über die Berechtigung "ausführen".  
  
-   Nur bestimmte Sicherheits Prinzipale sind \(zulässig, sind jedoch nicht erforderlich @ no__t-1, damit Sie über die Berechtigung Schreiben oder ändern verfügen. Die zulässigen Prinzipale sind die Gruppe der lokalen Administratoren, SYSTEM, ERSTELLER-BESITZER und TrustedInstaller. Anderen Konten oder Gruppen ist es nicht gestattet, die Berechtigung "Schreiben" oder "Ändern" für den Hotfixstammordner zu verwenden.  
  
Optional können Sie die obigen Prüfungen deaktivieren, die von Plug @ no__t-0in standardmäßig durchgeführt werden. Hierzu stehen Ihnen zwei Möglichkeiten zur Verfügung.  
  
-   Wenn Sie die PowerShell-Cmdlets für Cluster fähiges aktualisieren verwenden, konfigurieren Sie das Argument **disableaclchecks @ no__t-1' true '** im **caupluginarguments** -Parameter für das Hotfix-Plug @ no__t-3in.  
  
-   Wenn Sie die Benutzeroberfläche für clusterfähiges Aktualisieren verwenden, wählen Sie die Option **Prüfung auf Administratorzugriff auf Hotfixstammordner und Konfigurationsdatei deaktivieren** auf der Seite **Weitere Updateoptionen** aus, die zum Konfigurieren der Optionen von Updateausführungen verwendet wird.  
  
Es wird jedoch in vielen Umgebungen als bewährte Methode empfohlen, dass Sie diese Prüfungen mithilfe der Standardkonfiguration erzwingen.  
  
#### <a name="step-4-configure-settings-for-smb-data-integrity"></a>Schritt 4 Konfigurieren der Einstellungen für die SMB-Datenintegrität
  
Zum Überprüfen der Datenintegrität in den Verbindungen zwischen den Cluster Knoten und der SMB-Dateifreigabe erfordert das Hotfix-Plug-in @ no__t-0in, dass Sie die Einstellungen auf der SMB-Dateifreigabe für die SMB-Signatur oder SMB-Verschlüsselung aktivieren. Die SMB-Verschlüsselung, die in vielen Umgebungen eine höhere Sicherheit und bessere Leistung bietet, wird ab Windows Server 2012 unterstützt. Sie können eine oder beide Einstellungen wie folgt aktivieren:  
  
-   Informationen zum Aktivieren der SMB-Signatur finden Sie unter dem Verfahren in der Microsoft Knowledge Base in [Artikel 887429](https://support.microsoft.com/kb/887429) .  
  
-   Um die SMB-Verschlüsselung für den freigegebenen SMB-Ordner zu aktivieren, führen Sie das folgende PowerShell-Cmdlet auf dem SMB-Server aus:  
  
    ```PowerShell  
    Set-SmbShare <ShareName> -EncryptData $true  
    ```  
  
    Dabei gibt <*ShareName*> den Namen des freigegebenen SMB-Ordners an.  
  
Um optional die Verwendung der SMB-Verschlüsselung in den Verbindungen mit dem SMB-Server zu erzwingen, wählen Sie auf der Benutzeroberfläche für Cluster fähiges aktualisieren die Option **SMB-Verschlüsselung beim Zugriff auf hotfixstamm Ordner** anfordern aus, oder konfigurieren Sie die Option Requirements **smbencryption @ no__t-2' true '** Plug @ no__. t-3in-Argument mithilfe der Cau-PowerShell-Cmdlets.  
  
> [!IMPORTANT]  
> Wenn Sie die Option zum Erzwingen der Verwendung der SMB-Verschlüsselung auswählen und der Hotfixstammordner nicht für Verbindungen konfiguriert ist, die die SMB-Verschlüsselung verwenden, tritt bei der Updateausführung ein Fehler auf.  
  
#### <a name="step-5-enable-a-windows-firewall-rule-on-the-smb-server"></a>Schritt 5 Aktivieren der Windows-Firewall-Regel auf dem SMB-Server
  
Sie müssen die Regel **Datei Server-Remote Verwaltung \(SMB @ no__t-2in @ no__t-3** in der Windows-Firewall auf dem SMB-Dateiserver aktivieren. Dies ist in Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 standardmäßig aktiviert.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Übersicht über das Cluster fähige aktualisieren](cluster-aware-updating.md)
  
-   [Windows PowerShell-Cmdlets für Cluster fähiges aktualisieren](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating)  
  
-   [Plug-in-Referenz für Cluster fähiges aktualisieren](https://msdn.microsoft.com/library/hh418084.aspx)  
  
