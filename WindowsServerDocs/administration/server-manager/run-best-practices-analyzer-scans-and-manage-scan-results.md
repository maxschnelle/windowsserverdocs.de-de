---
title: Ausführen von Best Practices Analyzer-Scans und Verwalten von Überprüfung Results_1
description: Server-Manager
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-server-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 232f1c80-88ef-4a39-8014-14be788c2766
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 58fdf35e1d06fe7176b122155b2768094f2b01b4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838221"
---
# <a name="run-best-practices-analyzer-scans-and-manage-scan-results"></a>Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse

>Gilt für: Windows Server 2016

Bei der Verwaltung von Windows stellen *bewährte Methoden* Richtlinien dar, nach denen ein Server im normalen Betrieb optimal und gemäß den Vorschlägen von Experten konfiguriert werden kann. Beispielsweise ist es bei den meisten Serveranwendungen eine bewährte Methode, nur die Ports geöffnet zu lassen, die für die Kommunikation mit anderen Netzwerkcomputern erforderlich sind, und nicht verwendete Ports zu blockieren. Zwar sind selbst gravierende Verstöße gegen bewährte Methoden nicht unbedingt problematisch, doch weisen Verstöße auf Serverkonfigurationen hin, bei denen eine schlechte Leistung, mangelnde Zuverlässigkeit, unerwartete Konflikte, erhöhte Sicherheitsrisiken und andere potenzielle Probleme auftreten können.

Best Practices Analyzer (BPA) ist ein Serververwaltungstool, das in Windows Server 2012 R2, Windows Server 2012 und Windows Server 2008 R2 verfügbar ist. BPA können Administratoren, reduzieren Verstöße gegen bewährte Methoden, indem Sie Rollen, die auf verwalteten Servern, auf denen Windows Server 2012 oder Windows Server 2008 R2 installiert werden überprüft und Verstöße gegen bewährte Methoden für den Administrator.

Sie können Best Practices Analyzer (BPA)-Scans entweder im Server-Manager mithilfe der Benutzeroberfläche von BPA oder mithilfe von Cmdlets in Windows PowerShell ausführen. ab Windows Server 2012, können Sie eine oder mehrere Rollen gleichzeitig ausführen möchten, auf mehreren Servern überprüfen, ob Sie die Best Practices Analyzer-Kachel in der Server-Manager-Konsole oder Windows PowerShell-Cmdlets zum Ausführen von scans. Sie können in BPA auch festlegen, dass Scanergebnisse ausgeschlossen oder ignoriert werden, die Sie nicht anzeigen möchten.

Dieses Thema enthält die folgenden Abschnitte:

-   [BPA-Suche](#BKMK_find)

-   [Funktionsweise von BPA](#BKMK_how)

-   [Ausführen von Best Practices Analyzer-scans für Rollen](#BKMK_BPAscan)

-   [Verwalten der Überprüfungsergebnisse](#BKMK_manage)

## <a name="BKMK_find"></a>BPA-Suche
Finden Sie die Kachel "Best Practices Analyzer" auf Rolle und Gruppenseiten "Server" von Server-Manager, Windows Server 2012 R2 und Windows Server 2012, oder Sie können eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten zum Ausführen von Best Practices Analyzer-Cmdlets öffnen.

## <a name="BKMK_how"></a>Funktionsweise von BPA
BPA funktioniert, indem Sie messen die Übereinstimmung einer Rolle mit Regeln zu bewährten Methoden in acht unterschiedlichen Kategorien der Effektivität, Vertrauenswürdigkeit und Zuverlässigkeit. Die Bewertungsergebnisse werden in einem der drei Schweregrade zurückgegeben, die in der folgenden Tabelle beschrieben werden.

|Schweregrad|Beschreibung|
|---------|--------|
|Fehler|Fehlerergebnisse werden zurückgegeben, wenn eine Rolle den Bedingungen einer Regel für bewährte Methoden nicht entspricht und Funktionalitätsprobleme erwartet werden können.|
|Informationen|Informationsergebnisse werden zurückgegeben, wenn eine Rolle den Bedingungen einer Regel für bewährte Methoden entspricht.|
|Warnung|Warnungsergebnisse werden zurückgegeben, wenn die Ergebnisse der Nichtkompatibilität zu Problemen führen können, falls keine Änderungen vorgenommen werden. Die Anwendung ist zwar möglicherweise im aktuellen Betrieb kompatibel, entspricht den Bedingungen einer Regel jedoch nur, wenn ihre Konfiguration oder Richtlinieneinstellungen geändert werden. Beispielsweise kann beim Scan von Remotedesktopdienste eine Warnung angezeigt werden, wenn ein Lizenzserver für die Rolle nicht verfügbar ist. Denn selbst wenn zum Zeitpunkt des Scans keine Remoteverbindungen aktiv sind, bedeutet das Fehlen des Lizenzservers, dass neue Remoteverbindungen keine gültige Clientzugriffslizenzen erhalten.|

### <a name="rule-categories"></a>Regelkategorien
Die folgende Tabelle beschreibt die Kategorien der Regeln zu bewährten Methoden für die Rollen werden während der Best Practices Analyzer berechnet zu überprüfen.

|Kategoriename|Beschreibung|
|---------|--------|
|Sicherheit|Sicherheitsregeln werden angewendet, um eine relative Risiko von Bedrohungen, wie z. B. nicht autorisierte oder böswillige Benutzer, Verlust oder Diebstahl vertraulicher oder proprietärer Daten messen.|
|Leistung|Leistungsregeln werden angewendet, um zu messen die Fähigkeit einer Rolle Anforderungen zu verarbeiten und die vorgeschriebenen Aufgaben im Unternehmen innerhalb der Rolle Workload gegebenen Zeitpunkt auszuführen.|
|Konfiguration|Mit Konfigurationsregeln werden die Einstellungen einer Rolle identifiziert, die für eine optimale Leistung ggf. Änderungen erfordern. Konfigurationsregeln können Konflikte bei Einstellungen vermeiden, die Fehlermeldungen verursachen oder verhindern können, dass eine Rolle ihre zugewiesenen Aufgaben im Unternehmen erfüllt.|
|Richtlinie|Richtlinienregeln werden Gruppenrichtlinien oder Windows-registrierungseinstellungen identifiziert, die möglicherweise Änderungen für optimales und sicheres Ausführen einer Rolle angewendet.|
|Vorgang|Mit Vorgangsregeln werden mögliche Fehler einer Rolle beim Ausführen der vorgeschriebenen Aufgaben im Unternehmen identifiziert.|
|Vor der Bereitstellung|Regeln vor der Bereitstellung werden vor dem Bereitstellen einer installierten Rolle im Unternehmen angewendet. Damit können Administratoren auswerten, ob die bewährten Methoden erfüllt werden, bevor die Rolle in der Produktion verwendet wird.|
|Nach der Bereitstellung|Regeln nach der Bereitstellung werden angewendet, nachdem alle erforderlichen Dienste für eine Rolle gestartet wurden und die Rolle im Unternehmen ausgeführt wird.|
|Vorraussetzungen|Voraussetzungsregeln erläutern Konfigurationseinstellungen, Richtlinieneinstellungen und Features, die für eine Rolle erforderlich sind, bevor bestimmte Regeln aus anderen Kategorien von BPA angewendet werden können. Eine Voraussetzung in den Scanergebnissen gibt an, dass BPA aufgrund einer falschen Einstellung, eines fehlenden Programms, einer falsch aktivierten oder deaktivierten Richtlinie, einer Registrierungsschlüsseleinstellung oder sonstigen Konfiguration eine oder mehrere Regeln während des Scans nicht anwenden konnte. Die Kompatibilität oder Nichtkompatibilität mit Regeln wird somit nicht bewertet. Da eine Regel nicht angewendet werden konnte, ist sie nicht Bestandteil der Scanergebnisse.|

## <a name="BKMK_BPAscan"></a>Ausführen von Best Practices Analyzer-scans für Rollen
Sie können BPA-Scans für Rollen ausführen mithilfe der Benutzeroberfläche von BPA im Server-Manager oder mithilfe von Windows PowerShell-Cmdlets.

In Windows Server 2012 R2 und Windows Server 2012 einige Rollen Sie aufgefordert, weitere Parameter, wie die Namen bestimmter Server oder Freigaben, auf denen Teile der Rolle oder die IDs von Teilmodellen, ausgeführt werden, bevor ein BPA-Scan starten angeben. Verwenden Sie bei BPA-Scans für Modelle, bei denen Sie zusätzliche Parameter angeben müssen, die BPA-Cmdlets. Die grafische Benutzeroberfläche von BPA kann keine zusätzlichen Parameter wie Teilmodell-IDs annehmen. Beispielsweise stellt die Teilmodell-ID **FSRM** das Dateidienste-BPA-Teilmodell für den Ressourcen-Manager für Dateiserver dar, einen Rollendienst der Datei- und Speicherdienste. Um eine Überprüfung ausgeführt wird, nur auf den Rollendienst Ressourcen-Manager einen BPA-Scan mithilfe von Windows PowerShell-Cmdlets ausführen, und fügen Sie den Parameter `SubmodelId` dem Cmdlet.

Obwohl Sie zusätzliche Parameter an einen Scan, die Sie in der Benutzeroberfläche von BPA starten übergeben können, zeigt die BPA-Kachel im Server-Manager Ergebnisse für den letzten BPA-Scan, unabhängig davon, wie der Scan gestartet wurde.

-   [Überprüfen von Rollen mithilfe der Benutzeroberfläche von BPA](#BKMK_GUIscan)

-   [Überprüfen von Rollen mithilfe von Windows PowerShell-cmdlets](#BKMK_PSscan)

### <a name="BKMK_GUIscan"></a>Überprüfen von Rollen mithilfe der Benutzeroberfläche von BPA
Führen Sie die folgenden Schritte aus, um eine oder mehrere Rollen auf der grafischen Benutzeroberfläche von BPA zu überprüfen.

##### <a name="to-scan-roles-by-using-the-bpa-gui"></a>So überprüfen Sie Rollen mithilfe der grafischen Benutzeroberfläche von BPA

1.  Führen Sie einen der folgenden Server-Manager zu öffnen, sofern es nicht bereits geöffnet werden soll.

    -   Klicken Sie auf der Windows-Taskleiste auf die Schaltfläche "Server-Manager".

    -   Auf der **starten** Bildschirm, klicken Sie auf die Kachel Server-Manager.

2.  Öffnen Sie im Navigationsbereich eine Rollen- oder Gruppenseite.

    Beim Ausführen von BPA-Scans über eine Rollen- oder Gruppenseite werden alle Rollen überprüft, die auf Servern in dieser Gruppe installiert sind.

3.  Auf der **Aufgaben** im Menü der **Best Practices Analyzer** Kachel, klicken Sie auf **starten Sie die BPA-Scan**.

4.  Je nach Anzahl der Regeln, die für die von Ihnen ausgewählte Rolle oder Gruppe ausgewertet werden, kann es einige Minuten dauern, bis der BPA-Scan abgeschlossen ist.

### <a name="BKMK_PSscan"></a>Überprüfen von Rollen mithilfe von Windows PowerShell-cmdlets
Verwenden Sie die folgenden Verfahren, um eine oder mehrere Rollen mithilfe von Windows PowerShell-Cmdlets zu überprüfen.

> [!NOTE]
> Die Verfahren in diesem Abschnitt stellen nicht alle BPA-Cmdlets und -Parameter vor. Geben Sie für Weitere Informationen zu BPA-Vorgängen in Windows PowerShell, in der Windows PowerShell-Sitzung **Get-Help***BPACmdlet***-vollständige**, wobei *BPACmdlet* möglich die folgenden Werte. Sie erhalten auch BPA-Cmdlet-Hilfethemen für die [Windows Server TechCenter](https://go.microsoft.com/fwlink/p/?LinkId=240177).

-   **Get-BPAmodel**

-   **Invoke-BPAmodel**

-   **Get-BPAResult**

-   **Set-BPAResult**

#### <a name="BKMK_singlerole"></a>Überprüfen Sie eine einzelne Rolle mithilfe von Windows PowerShell-cmdlets

1.  Führen Sie eine der folgenden Windows PowerShell mit erhöhten Benutzerrechten ausführen.

    -   Zum Ausführen von Windows PowerShell als Administrator über die **starten** der rechten Maustaste auf die **Windows PowerShell** -Kachel in der **Apps** führt, und klicken Sie auf der app-Leiste auf **Als Administrator ausführen**.

    -   Führen Sie Windows PowerShell als Administrator über den Desktop Maustaste der **Windows PowerShell** der Taskleiste, und klicken Sie dann auf die Verknüpfung **als Administrator ausführen**.

2.  ab Windows PowerShell 3.0 können werden Cmdlet-Module automatisch in der Windows PowerShell-Sitzung beim ersten importiert, die ein Cmdlet im Modul verwendet wird. Das BPA-Cmdlet-Modul muss nicht importiert oder geladen werden.

3.  Suchen Sie die Modell-IDs aller Rollen, die für die BPA Scans können, indem Sie eingeben ausgeführt werden der **Get-Bpamodel** wie im folgenden Beispiel gezeigt.

    `Get-Bpamodel`

4.  Suchen Sie in den Ergebnissen aus Schritt 3 die Modell-IDs der Rollen, für die Sie einen BPA-Scan ausführen möchten.

5.  Geben Sie einen der folgenden Befehle ein, um den BPA-Scan für eine bestimmte Rolle zu starten. Trennen Sie die Modell-IDs bei mehreren Rollen durch Kommas.

    `Invoke-BPAmodel -modelId <modelID_from_Step3>`

    `Invoke-BPAmodel <modelID_from_Step3>`

    **Beispiel:**`Invoke-BPAmodel -modelId Microsoft/Windows/DNSServer,Microsoft/Windows/FileServices`

    > [!NOTE]
    > Die Modell-ID enthält den gesamten Pfad, der in der Spalte **Id** angezeigt wird, z. B. **Microsoft/Windows/Hyper-V**.

    Sie können auch einen Scan für eine bestimmte Rolle aus den Ergebnissen von Schritt 3 starten, indem Sie die Ergebnisse des `Get-BPAmodel` -Cmdlets an das `Invoke-BPAmodel` -Cmdlet weitergeben, wie im folgenden Beispiel gezeigt.

    `Get-BPAmodel <model_ID> | Invoke-BPAmodel`

    Dieses Cmdlet ausführen, ohne eine Modell-ID übergibt alle Modelle, die von zurückgegeben werden die `Get-BPAmodel` Cmdlets an das `Invoke-BPAmodel` -Cmdlet, Scans gestartet, auf alle Modelle, die auf Servern verfügbar sind, die dem Serverpool des Server-Manager hinzugefügt wurden.

#### <a name="BKMK_allroles"></a>So überprüfen Sie alle Rollen mithilfe von Windows PowerShell-cmdlets

1.  Öffnen Sie eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten, sofern nicht bereits geöffnet ist. Anweisungen finden Sie im vorherigen Verfahren.

2.  Leiten Sie alle Rollen, die für den BPA-Scan ausgeführt werden können, zum Starten von Scans an das `Invoke-BPAmodel` -Cmdlet weiter.

    `Get-BPAmodel | Invoke-BPAmodel`

3.  Wenn die Überprüfung abgeschlossen ist, gibt Windows PowerShell Ergebnisse ähnlich dem folgenden, für jede Rolle, die gescannt wurde.

    ```
    modelId                 :  Microsoft/Windows/FileServices
    SubmodelId              :
    Success                 :  True
    Scantime                :  1/01/2012  12:18:40 PM
    ScantimeUtcOffset       :  -08:00:00
    detail                  :  {server_name1, server_name2}

    ```

## <a name="BKMK_manage"></a>Verwalten der Überprüfungsergebnisse
Nachdem ein BPA-Scan auf der grafischen Benutzeroberfläche abgeschlossen wurde, können Sie Scanergebnisse in der BPA-Kachel anzeigen. Wenn Sie ein Ergebnis in der Kachel auswählen, werden in einem Vorschaubereich in der Kachel Ergebniseigenschaften angezeigt, und es wird angegeben, ob die Rolle mit der zugeordneten bewährten Methode kompatibel ist. Wenn ein Ergebnis nicht kompatibel ist, und Sie, wie Sie die in den Ergebniseigenschaften beschriebenen Probleme lösen wissen möchten, öffnen Sie Hyperlinks in Fehler- und warnungsergebniseigenschaften detaillierte lösungshilfethemen im Windows Server TechCenter.

> [!NOTE]
> BPA-Scanergebnisse werden nicht automatisch gespeichert oder archiviert. Beim Ausführen eines neuen Scans für ein Modell oder Teilmodell werden die Ergebnisse des letzten Scans überschrieben. Informationen zum Speichern der Ergebnisse von BPA-Scans, damit diese archiviert, gedruckt oder an andere gesendet werden können, finden Sie unter [So können Sie BPA-Ergebnisse aus Windows PowerShell-Sitzungen in verschiedenen Formaten anzeigen oder speichern](#BKMK_formats) in diesem Abschnitt.

### <a name="exclude-and-include-bpa-results"></a>Ausschließen und Einschließen von BPA-Ergebnissen
Wenn Sie nicht benötigen, um einige BPA-Ergebnisse, wie z. B. die Ergebnisse anzuzeigen, die häufig in Ihren BPA-Scans auftreten, aber keine Lösung erfordern, können Sie die Ergebnissen ausschließen, mithilfe der grafischen Benutzeroberfläche von BPA oder BPA-Cmdlets in Windows PowerShell. Sie können diese Ergebnisse jederzeit wieder einschließen.

> [!NOTE]
> Wenn Sie Ergebnisse ausschließen, werden sie auch nicht auf verwalteten Servern angezeigt. Andere Administratoren können ausgeschlossene Ergebnisse auf verwalteten Servern nicht anzeigen. Um Ergebnisse aus der Ansicht in eine lokale Server-Manager-Konsole auszuschließen, erstellen Sie eine benutzerdefinierte Abfrage, anstatt die **Ergebnis ausschließen** Befehl.

#### <a name="BKMK_exclude"></a>Ausschließen von Scanergebnissen
Die Einstellung **Ausschließen** ist persistent. Die von Ihnen ausgeschlossenen Ergebnisse bleiben bei künftigen Scans desselben Modells auf demselben Computer ausgeschlossen, sofern Sie sie nicht wieder einschließen.

Sie können Scanergebnisse mit dem `Set-BPAResult` -Cmdlet in Verbindung mit dem `Exclude` -Parameter ausschließen. Wie in der Best Practices Analyzer-Kachel im Server-Manager können Sie einzelne Ergebnisobjekte ausschließen, oder Sie können auch eine Reihe von Ergebnissen, deren Felder (Kategorie, Titel und Schweregrad, z. B.) entsprechen oder angegebene Werte enthalten, ausschließen. Beispielsweise können Sie aus einer Reihe von Scanergebnissen für ein Modell alle **Leistungsergebnisse** ausschließen.

> [!NOTE]
> Sie müssen mindestens einen BPA-Scan für ein Modell ausführen, bevor Sie die Verfahren in diesem Abschnitt verwenden können.

###### <a name="to-exclude-scan-results-by-using-the-gui"></a>So schließen Sie Scanergebnisse mithilfe der grafischen Benutzeroberfläche aus

1.  Öffnen Sie eine Rollen- oder Gruppenseite im Server-Manager.

2.  In der Kachel Best Practices Analyzer für die Rolle oder Servergruppe mit der Maustaste ein Ergebnis in der Liste aus, und klicken Sie dann auf **Ergebnis ausschließen**.

    Das Ergebnis wird nicht mehr in der Liste der Ergebnisse angezeigt.

3.  Führen Sie die integrierte Abfrage **Ausgeschlossene Ergebnisse** aus, um die ausgeschlossenen Ergebnisse auf der grafischen Benutzeroberfläche anzuzeigen. Klicken Sie auf **Gespeicherte Suchabfragen**, und klicken Sie dann auf **Ausgeschlossene Ergebnisse**.

    Beachten Sie, dass nach dem Ausführen der Abfrage **Ausgeschlossene Ergebnisse** der Untertitel der Kachel (eine Beschreibung der in der Liste angezeigten Ergebnisse) sich in **Ausgeschlossene Ergebnisse** ändert. Es werden nur ausgeschlossene Ergebnisse in der Liste angezeigt.

###### <a name="to-exclude-scan-results-by-using-windows-powershell-cmdlets"></a>So schließen Sie Scanergebnisse mithilfe von Windows PowerShell-Cmdlets aus

1.  Öffnen Sie eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten.

2.  Führen Sie den folgenden Befehl aus, um bestimmte Ergebnisse aus einem Modellscan auszuschließen.

    `Get-BPAResult -modelId <model ID> | Where { $_.<Field Name> -eq "Value"} | Set-BPAResult -Exclude $true`

    Der vorherige Befehl ruft Ergebniselemente von BPA-Scan für die Modell-ID, die durch dargestellt wird *Modell-ID*.

    Mit dem zweiten Abschnitt des Befehls werden die Ergebnisse des `Get-BPAResult`-Cmdlets gefiltert, sodass nur die Scanergebnisse abgerufen werden, bei denen der Wert für ein durch *Feldname* dargestelltes Ergebnisfeld mit dem Text in Anführungszeichen übereinstimmt.

    Mit dem letzten Abschnitt des Befehls, der auf den zweiten senkrechten Strich folgt, werden die vom vorherigen Cmdlet-Abschnitt gefilterten Ergebnisse ausgeschlossen.

    **Beispiel:**`Get-BPAResult -Microsoft/Windows/FileServices | Where { $_.Severity -eq "Information"} | Set-BPAResult -Exclude $true`

#### <a name="include-scan-results"></a>Einschließen von Scanergebnissen
Wenn Sie ausgeschlossene Scanergebnisse anzeigen möchten, können Sie diese Ergebnisse einschließen. Die Einstellung **Einschließen** ist persistent. Eingeschlossene Ergebnisse bleiben bei künftigen Scans desselben Modells auf demselben Computer eingeschlossen.

##### <a name="BKMK_gui"></a>So schließen Sie Überprüfungsergebnisse mithilfe der grafischen Benutzeroberfläche

1.  Öffnen Sie eine Rollen- oder Gruppenseite im Server-Manager.

2.  In der Kachel Best Practices Analyzer für die Rolle oder Servergruppe mit der Maustaste eines ausgeschlossenen Ergebnis in der **ausgeschlossene Ergebnisse** Abfragen der Liste aus, und klicken Sie dann auf **Ergebnis einschließen**.

    Das Ergebnis wird nicht mehr in der Liste der ausgeschlossenen Ergebnisse angezeigt. Löschen Sie die Abfrage, indem Sie auf **Alle löschen** klicken, um das eingeschlossene Ergebnis in die Liste aller eingeschlossenen Ergebnisse anzuzeigen.

##### <a name="BKMK_cmdlets"></a>So schließen Sie Überprüfungsergebnisse mithilfe der Windows PowerShell-cmdlets

1.  Öffnen Sie eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten.

2.  Geben Sie zum Einschließen bestimmter Ergebnisse aus einem Modellscan den folgenden Befehl ein, und drücken Sie dann die **EINGABETASTE**.

    `Get-BPAResult -modelId <model Id> | Where { $_.<Field Name> -eq "Value" } | Set-BPAResult -Exclude $false`

    Der vorherige Befehl ruft Ergebniselemente von BPA-Scan für das Modell durch dargestellt *Modell-Id*.

    Der zweite Teil des Befehls, der nach dem senkrechten Strich ( **|** ) filtert die Ergebnisse der **Get-BPAResult** Cmdlet zum Abrufen von nur die Überprüfungsergebnisse für die der Wert des Ergebnisses durch dargestellte Feld *Feldname*, mit dem Text in Anführungszeichen übereinstimmt.

    Mit dem letzten Abschnitt des Befehls, der auf den zweiten senkrechten Strich folgt, werden die Filterergebnisse des zweiten Cmdlet-Abschnitts eingeschlossen. Dabei wird der **-Exclude** -Parameter auf **false**festgelegt.

    **Beispiel:**`Get-BPAResult -Microsoft/Windows/FileServices | Where { $_.Severity -eq "Information"} | Set-BPAResult -Exclude $false`

### <a name="view-and-export-bpa-scan-results-in-windows-powershell"></a>Anzeigen und Exportieren von BPA-Scanergebnissen in Windows PowerShell
Zum Anzeigen und Verwalten der Scanergebnisse mithilfe von Windows PowerShell-Cmdlets, finden Sie unter den folgenden Verfahren. Bevor Sie eines der folgenden Verfahren verwenden können, müssen Sie mindestens einen BPA-Scan auf mindestens einem Modell oder Teilmodell ausführen.

#### <a name="BKMK_recentPS"></a>Zum Anzeigen der Ergebnisse des letzten Scans einer Rolle mithilfe von Windows PowerShell

1.  Öffnen Sie eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten.

2.  Rufen Sie die Ergebnisse des letzten Scans für eine angegebene Modell-ID ab. Geben Sie Folgendes ein, auf der das Modell, indem dargestellt wird *Modell-ID*, und drücken Sie dann die **EINGABETASTE**. Sie können Ergebnisse für mehrere Modell-IDs abrufen, indem Sie die Modell-IDs durch Kommas trennen.

    `Get-BPAResult <model ID>`

    **Beispiel:** `Get-BPAResult Microsoft/Windows/DNSServer,Microsoft/Windows/FileServices`

    Wenn Sie gescannt haben Teilmodell eines Modells, z. B. einen Rollendienst, erhalten Sie die Ergebnisse für nur dieses Teilmodell ab dazu die Teilmodell-ID im Cmdlet.

    **Beispiel:** `Get-BPAResult Microsoft/Windows/FileServices -SubmodelID FSRM`

#### <a name="BKMK_formats"></a>Anzeigen oder Speichern von BPA-Ergebnisse aus Windows PowerShell-Sitzungen in verschiedenen Formaten

-   Jedes BPA-Ergebnis ähnelt dem folgenden Code in Windows PowerShell.

    ```
    ResultNumber     :  14
    ResultId         :  1557706192
    modelId          :  Microsoft/Windows/FileServices
    SubmodelId       :  FSRM
    RuleId           :  16
    computerName     :  server_name1, server_name2
    Context          :  FileServices
    Source           :  server_name1
    Severity         :  Information
    Category         :  Configuration
    Title            :  Access Denied remediation requires remote management be enabled on this server
    Problem          :
    Impact           :
    Resolution       :
    compliance       :  The File Server Best Practices Analyzer scan has determined that you are in compliance with this best practice.
    help             :
    Excluded         :  False

    ```

    Führen Sie eine der folgenden Aktionen aus.

    -   Wenn Sie BPA-Ergebnisse in einer Tabelle formatieren möchten, führen Sie das folgende Cmdlet aus, und fügen Sie aus dem vorherigen Beispiel die Ergebniseigenschaften hinzu, die Sie anzeigen möchten.

        `Get-BPAResult model ID | format-Table -Property <property1,property2,property3...>`

        **Beispiel:**`Get-BPAResult Microsoft/Windows/FileServices | format-Table -Property modelId,SubmodelId,computerName,Source,Severity,Category,Title,Problem,Impact,Resolution,compliance,help`

    -   Wenn Sie BPA-Ergebnisse in einer auf der grafischen Benutzeroberfläche basierenden Rasteransicht mit einem Textzeichenfolgenfilter und Spaltenüberschriften formatieren möchten, auf die zum Sortieren von Ergebnissen geklickt werden kann, führen Sie das folgende Cmdlet aus.

        `Get-BPAResult <model ID> | OGV`

    -   BPA-Ergebnisse in eine HTML-Datei zu exportieren, die archiviert oder führen Sie das folgende Cmdlet an e-Mail-Empfänger gesendet werden können, in denen *Pfad* den Pfad und Dateinamen darstellt, die HTML-Ergebnisse gespeichert werden soll.

        `Get-BPAResult <model ID> | convertTo-Html | Set-Content <path>`

        **Beispiel:**`Get-BPAResult Microsoft/Windows/FileServices | convertTo-Html | Set-Content C:\BPAResults\FileServices.htm`

    -   So exportieren Sie BPA-Ergebnisse in eine Textdatei mit kommagetrennten Werten (CSV), führen Sie das folgende Cmdlet, in denen *Pfad* stellt den Pfad und den Text-Dateinamen, die CSV-Ergebnisse gespeichert werden soll. CSV-Ergebnisse können in Microsoft Excel oder andere Programme, die Daten in Tabellen oder Rastern anzeigen importiert werden.

        `Get-BPAResult <model ID> | Export-CSV <path>`

        **Beispiel:**`Get-BPAResult Microsoft/Windows/FileServices | Export-CSV C:\BPAResults\FileServices.txt`

## <a name="see-also"></a>Siehe auch
[Best Practices Analyzer für Inhalt mit Lösungen für Windows Server TechCenter](https://go.microsoft.com/fwlink/p/?LinkId=241597)
[filtern, Sortieren und Abfragen von Daten in Server-Manager-Kacheln](filter-sort-and-query-data-in-server-manager-tiles.md)
[Manage Multiple, remote Servers mit Server-Manager](manage-multiple-remote-servers-with-server-manager.md)
