---
title: Ausführen Best Practices Analyzer Scans und Verwalten der Scan Results_1
description: Server-Manager
ms.topic: article
ms.assetid: 232f1c80-88ef-4a39-8014-14be788c2766
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 8b8ef48e81daa9c673f42d43b2f95abadec619a8
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627799"
---
# <a name="run-best-practices-analyzer-scans-and-manage-scan-results"></a>Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse

>Gilt für: Windows Server 2016

Bei der Verwaltung von Windows stellen *bewährte Methoden* Richtlinien dar, nach denen ein Server im normalen Betrieb optimal und gemäß den Vorschlägen von Experten konfiguriert werden kann. Beispielsweise ist es bei den meisten Serveranwendungen eine bewährte Methode, nur die Ports geöffnet zu lassen, die für die Kommunikation mit anderen Netzwerkcomputern erforderlich sind, und nicht verwendete Ports zu blockieren. Zwar sind selbst gravierende Verstöße gegen bewährte Methoden nicht unbedingt problematisch, doch weisen Verstöße auf Serverkonfigurationen hin, bei denen eine schlechte Leistung, mangelnde Zuverlässigkeit, unerwartete Konflikte, erhöhte Sicherheitsrisiken und andere potenzielle Probleme auftreten können.

Best Practices Analyzer (BPA) ist ein Server Verwaltungs Tool, das in Windows Server 2012 R2, Windows Server 2012 und Windows Server 2008 R2 verfügbar ist. Mithilfe von BPA können Administratoren Verstöße gegen bewährte Methoden verringern, indem Sie die auf verwalteten Servern mit Windows Server 2012 oder Windows Server 2008 R2 installierten Rollen überprüfen und Verstöße gegen bewährte Methoden für den Administrator melden.

Sie können Best Practices Analyzer (BPA)-Scans entweder über Server-Manager, mithilfe der grafischen Benutzeroberfläche von BPA oder mithilfe von Cmdlets in Windows PowerShell ausführen. ab Windows Server 2012 können Sie eine oder mehrere Rollen gleichzeitig auf mehreren Servern Scannen, unabhängig davon, ob Sie die Best Practices Analyzer-Kachel in der Server-Manager-Konsole oder Windows PowerShell-Cmdlets zum Ausführen von Scans verwenden. Sie können in BPA auch festlegen, dass Scanergebnisse ausgeschlossen oder ignoriert werden, die Sie nicht anzeigen möchten.

Dieses Thema enthält folgende Abschnitte:

-   [BPA suchen](#BKMK_find)

-   [Funktionsweise von BPA](#BKMK_how)

-   [Ausführen von Best Practices Analyzer-Scans für Rollen](#BKMK_BPAscan)

-   [Verwalten von Scanergebnissen](#BKMK_manage)

## <a name="find-bpa"></a><a name=BKMK_find></a>BPA suchen
Die Best Practices Analyzer-Kachel finden Sie auf den Rollen-und Server Gruppen Seiten Server-Manager in Windows Server 2012 R2 und Windows Server 2012, oder Sie können eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten öffnen, um Best Practices Analyzer-Cmdlets auszuführen.

## <a name="how-bpa-works"></a><a name=BKMK_how></a>Funktionsweise von BPA
BPA misst die Konformität einer Rolle mit Best Practices-Regeln in acht verschiedenen Kategorien von Effektivität, Vertrauenswürdigkeit und Zuverlässigkeit. Die Bewertungsergebnisse werden in einem der drei Schweregrade zurückgegeben, die in der folgenden Tabelle beschrieben werden.

|Schweregrad|BESCHREIBUNG|
|---------|--------|
|Fehler|Fehlerergebnisse werden zurückgegeben, wenn eine Rolle den Bedingungen einer Regel für bewährte Methoden nicht entspricht und Funktionalitätsprobleme erwartet werden können.|
|Information|Informationsergebnisse werden zurückgegeben, wenn eine Rolle den Bedingungen einer Regel für bewährte Methoden entspricht.|
|Warnung|Warnungsergebnisse werden zurückgegeben, wenn die Ergebnisse der Nichtkompatibilität zu Problemen führen können, falls keine Änderungen vorgenommen werden. Die Anwendung ist zwar möglicherweise im aktuellen Betrieb kompatibel, entspricht den Bedingungen einer Regel jedoch nur, wenn ihre Konfiguration oder Richtlinieneinstellungen geändert werden. Beispielsweise kann beim Scan von Remotedesktopdienste eine Warnung angezeigt werden, wenn ein Lizenzserver für die Rolle nicht verfügbar ist. Denn selbst wenn zum Zeitpunkt des Scans keine Remoteverbindungen aktiv sind, bedeutet das Fehlen des Lizenzservers, dass neue Remoteverbindungen keine gültige Clientzugriffslizenzen erhalten.|

### <a name="rule-categories"></a>Regelkategorien
In der folgenden Tabelle werden die Kategorien der Best Practices-Regeln beschrieben, mit denen Rollen während eines Best Practices Analyzer Scans gemessen werden.

|Category Name|BESCHREIBUNG|
|---------|--------|
|Sicherheit|Sicherheitsregeln werden angewendet, um das relative Risiko einer Rolle für Bedrohungen wie nicht autorisierte oder böswillige Benutzer oder den Verlust oder Diebstahl vertraulicher oder proprietärer Daten zu messen.|
|Leistung|Leistungs Regeln werden angewendet, um die Fähigkeit einer Rolle zum Verarbeiten von Anforderungen und zum Ausführen der vorgeschriebenen Aufgaben im Unternehmen innerhalb der erwarteten Zeitspanne in der Arbeitsauslastung der Rolle zu messen.|
|Konfiguration|Mit Konfigurationsregeln werden die Einstellungen einer Rolle identifiziert, die für eine optimale Leistung ggf. Änderungen erfordern. Konfigurationsregeln können Konflikte bei Einstellungen vermeiden, die Fehlermeldungen verursachen oder verhindern können, dass eine Rolle ihre zugewiesenen Aufgaben im Unternehmen erfüllt.|
|Policy|Richtlinien Regeln werden angewendet, um Gruppenrichtlinie oder Windows-Registrierungs Einstellungen zu identifizieren, die möglicherweise geändert werden müssen, damit eine Rolle optimal und sicher funktioniert.|
|Vorgang|Mit Vorgangsregeln werden mögliche Fehler einer Rolle beim Ausführen der vorgeschriebenen Aufgaben im Unternehmen identifiziert.|
|Vor der Bereitstellung|Regeln vor der Bereitstellung werden vor dem Bereitstellen einer installierten Rolle im Unternehmen angewendet. Damit können Administratoren auswerten, ob die bewährten Methoden erfüllt werden, bevor die Rolle in der Produktion verwendet wird.|
|Nach der Bereitstellung|Regeln nach der Bereitstellung werden angewendet, nachdem alle erforderlichen Dienste für eine Rolle gestartet wurden und die Rolle im Unternehmen ausgeführt wird.|
|Voraussetzungen|Voraussetzungsregeln erläutern Konfigurationseinstellungen, Richtlinieneinstellungen und Features, die für eine Rolle erforderlich sind, bevor bestimmte Regeln aus anderen Kategorien von BPA angewendet werden können. Eine Voraussetzung in den Scanergebnissen gibt an, dass BPA aufgrund einer falschen Einstellung, eines fehlenden Programms, einer falsch aktivierten oder deaktivierten Richtlinie, einer Registrierungsschlüsseleinstellung oder sonstigen Konfiguration eine oder mehrere Regeln während des Scans nicht anwenden konnte. Die Kompatibilität oder Nichtkompatibilität mit Regeln wird somit nicht bewertet. Da eine Regel nicht angewendet werden konnte, ist sie nicht Bestandteil der Scanergebnisse.|

## <a name="performing-best-practices-analyzer-scans-on-roles"></a><a name=BKMK_BPAscan></a>Ausführen von Best Practices Analyzer-Scans für Rollen
Sie können BPA-Scans für Rollen ausführen, indem Sie entweder die BPA-GUI in Server-Manager oder Windows PowerShell-Cmdlets verwenden.

In Windows Server 2012 R2 und Windows Server 2012 werden Sie von einigen Rollen aufgefordert, zusätzliche Parameter anzugeben, z. b. die Namen bestimmter Server oder Freigaben, auf denen Teile der Rolle ausgeführt werden, oder die IDs von Teilmodellen, bevor ein BPA-Scan gestartet wird. Verwenden Sie bei BPA-Scans für Modelle, bei denen Sie zusätzliche Parameter angeben müssen, die BPA-Cmdlets. Die grafische Benutzeroberfläche von BPA kann keine zusätzlichen Parameter wie Teilmodell-IDs annehmen. Beispielsweise stellt die Teilmodell-ID **FSRM** das Dateidienste-BPA-Teilmodell für den Ressourcen-Manager für Dateiserver dar, einen Rollendienst der Datei- und Speicherdienste. Führen Sie einen BPA-Scan mithilfe von Windows PowerShell-Cmdlets aus, und fügen Sie dem Cmdlet den-Parameter hinzu, um nur einen Scanvorgang auf dem Datei Server Ressourcen-Manager Rollen Dienst auszuführen `SubmodelId` .

Obwohl Sie keine zusätzlichen Parameter an einen Scan übergeben können, den Sie auf der grafischen Benutzeroberfläche von BPA starten, zeigt die BPA-Kachel in Server-Manager Ergebnisse für den letzten BPA-Scan an, unabhängig davon, wie der Scanvorgang gestartet wurde.

-   [Überprüfen von Rollen mithilfe der grafischen Benutzeroberfläche von BPA](#BKMK_GUIscan)

-   [Überprüfen von Rollen mithilfe von Windows PowerShell-Cmdlets](#BKMK_PSscan)

### <a name="scanning-roles-by-using-the-bpa-gui"></a><a name=BKMK_GUIscan></a>Überprüfen von Rollen mithilfe der grafischen Benutzeroberfläche von BPA
Führen Sie die folgenden Schritte aus, um eine oder mehrere Rollen auf der grafischen Benutzeroberfläche von BPA zu überprüfen.

##### <a name="to-scan-roles-by-using-the-bpa-gui"></a>So überprüfen Sie Rollen mithilfe der grafischen Benutzeroberfläche von BPA

1.  Führen Sie eine der folgenden Aktionen aus, um Server-Manager zu öffnen, wenn es nicht bereits geöffnet ist.

    -   Klicken Sie in der Windows-Taskleiste auf die Schaltfläche Server-Manager.

    -   Klicken Sie auf dem **Start** Bildschirm auf die Kachel Server-Manager.

2.  Öffnen Sie im Navigationsbereich eine Rollen- oder Gruppenseite.

    Beim Ausführen von BPA-Scans über eine Rollen- oder Gruppenseite werden alle Rollen überprüft, die auf Servern in dieser Gruppe installiert sind.

3.  Klicken Sie im Menü **Aufgaben** der Kachel **Best Practices Analyzer** auf **BPA-Scan starten**.

4.  Je nach Anzahl der Regeln, die für die von Ihnen ausgewählte Rolle oder Gruppe ausgewertet werden, kann es einige Minuten dauern, bis der BPA-Scan abgeschlossen ist.

### <a name="scanning-roles-by-using-windows-powershell-cmdlets"></a><a name=BKMK_PSscan></a>Überprüfen von Rollen mithilfe von Windows PowerShell-Cmdlets
Verwenden Sie die folgenden Verfahren, um eine oder mehrere Rollen mithilfe von Windows PowerShell-Cmdlets zu scannen.

> [!NOTE]
> Die Verfahren in diesem Abschnitt stellen nicht alle BPA-Cmdlets und -Parameter vor. Weitere Informationen zu BPA-Vorgängen in Windows PowerShell erhalten Sie, wenn Sie in Ihrer Windows PowerShell **-Sitzung Get-Help***bpacmdlet***-Full**eingeben, wobei *bpacmdlet* einer der folgenden Werte sein kann. Sie finden auch Hilfe Themen zu BPA-Cmdlets im [Windows Server TechCenter](https://go.microsoft.com/fwlink/p/?LinkId=240177).

-   **Get-BPAModel**

-   **Aufrufen-BPAModel**

-   **Get-bparameesult**

-   **Set-bparameesult**

#### <a name="to-scan-a-single-role-by-using-windows-powershell-cmdlets"></a><a name=BKMK_singlerole></a>So überprüfen Sie eine einzelne Rolle mithilfe von Windows PowerShell-Cmdlets

1.  Führen Sie eine der folgenden Aktionen aus, um Windows PowerShell mit erhöhten Benutzerrechten auszuführen.

    -   Wenn Sie Windows PowerShell als Administrator über den **Start** Bildschirm ausführen möchten, klicken Sie in den **apps** -Ergebnissen mit der rechten Maustaste auf die Kachel **Windows PowerShell** , und klicken Sie dann auf der APP-Leiste auf **als Administrator ausführen**.

    -   Wenn Sie Windows PowerShell als Administrator über den Desktop ausführen möchten, klicken Sie in der Taskleiste mit der rechten Maustaste auf die Verknüpfung **Windows PowerShell** , und klicken Sie dann auf **als Administrator ausführen**.

2.  ab Windows PowerShell 3,0 werden Cmdlet-Module automatisch in Ihre Windows PowerShell-Sitzung importiert, wenn ein Cmdlet aus dem Modul zum ersten Mal verwendet wird. Das BPA-Cmdlet-Modul muss nicht importiert oder geladen werden.

3.  Suchen Sie die Modell-IDs aller Rollen, für die BPA-Scans ausgeführt werden können, indem Sie das Cmdlet **Get-BPAModel** eingeben, wie im folgenden Beispiel gezeigt.

    `Get-Bpamodel`

4.  Suchen Sie in den Ergebnissen aus Schritt 3 die Modell-IDs der Rollen, für die Sie einen BPA-Scan ausführen möchten.

5.  Geben Sie einen der folgenden Befehle ein, um den BPA-Scan für eine bestimmte Rolle zu starten. Trennen Sie die Modell-IDs bei mehreren Rollen durch Kommas.

    `Invoke-BPAmodel -modelId <modelID_from_Step3>`

    `Invoke-BPAmodel <modelID_from_Step3>`

    **Beispiel:** `Invoke-BPAmodel -modelId Microsoft/Windows/DNSServer,Microsoft/Windows/FileServices`

    > [!NOTE]
    > Die Modell-ID enthält den gesamten Pfad, der in der Spalte **Id** angezeigt wird, z. B. **Microsoft/Windows/Hyper-V**.

    Sie können auch einen Scan für eine bestimmte Rolle aus den Ergebnissen von Schritt 3 starten, indem Sie die Ergebnisse des `Get-BPAmodel` -Cmdlets an das `Invoke-BPAmodel` -Cmdlet weitergeben, wie im folgenden Beispiel gezeigt.

    `Get-BPAmodel <model_ID> | Invoke-BPAmodel`

    Wenn Sie dieses Cmdlet ausführen, ohne eine Modell-ID anzugeben, werden alle vom `Get-BPAmodel` Cmdlet zurückgegebenen Modelle an das `Invoke-BPAmodel` Cmdlet weitergeleitet, und es werden Scans für alle Modelle gestartet, die auf Servern verfügbar sind, die dem Server-Manager-Server Pool hinzugefügt wurden.

#### <a name="to-scan-all-roles-by-using-windows-powershell-cmdlets"></a><a name=BKMK_allroles></a>So überprüfen Sie alle Rollen mithilfe von Windows PowerShell-Cmdlets

1.  Öffnen Sie eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten, sofern nicht bereits eine geöffnet ist. Anweisungen finden Sie im vorherigen Verfahren.

2.  Leiten Sie alle Rollen, die für den BPA-Scan ausgeführt werden können, zum Starten von Scans an das `Invoke-BPAmodel` -Cmdlet weiter.

    `Get-BPAmodel | Invoke-BPAmodel`

3.  Nach Abschluss der Überprüfung gibt Windows PowerShell Ergebnisse ähnlich der folgenden für jede überprüfte Rolle zurück.

    ```
    modelId                 :  Microsoft/Windows/FileServices
    SubmodelId              :
    Success                 :  True
    Scantime                :  1/01/2012  12:18:40 PM
    ScantimeUtcOffset       :  -08:00:00
    detail                  :  {server_name1, server_name2}

    ```

## <a name="manage-scan-results"></a><a name=BKMK_manage></a>Verwalten von Scanergebnissen
Nachdem ein BPA-Scan auf der grafischen Benutzeroberfläche abgeschlossen wurde, können Sie Scanergebnisse in der BPA-Kachel anzeigen. Wenn Sie ein Ergebnis in der Kachel auswählen, werden in einem Vorschaubereich in der Kachel Ergebniseigenschaften angezeigt, und es wird angegeben, ob die Rolle mit der zugeordneten bewährten Methode kompatibel ist. Wenn ein Ergebnis nicht kompatibel ist und Sie wissen möchten, wie die in den Ergebnis Eigenschaften beschriebenen Probleme gelöst werden können, öffnen die Links unter Fehler-und Warnungs Ergebnis Eigenschaften detaillierte Lösungs Hilfe Themen im Windows Server TechCenter.

> [!NOTE]
> BPA-Scanergebnisse werden nicht automatisch gespeichert oder archiviert. Beim Ausführen eines neuen Scans für ein Modell oder Teilmodell werden die Ergebnisse des letzten Scans überschrieben. Informationen zum Speichern der Ergebnisse von BPA-Scans, damit diese archiviert, gedruckt oder an andere gesendet werden können, finden Sie unter [So können Sie BPA-Ergebnisse aus Windows PowerShell-Sitzungen in verschiedenen Formaten anzeigen oder speichern](#BKMK_formats) in diesem Abschnitt.

### <a name="exclude-and-include-bpa-results"></a>Ausschließen und Einschließen von BPA-Ergebnissen
Wenn keine BPA-Ergebnisse angezeigt werden müssen, z. b. Ergebnisse, die häufig in den BPA-Scans auftreten, aber keine Auflösung erfordern, können Sie die Ergebnisse ausschließen, indem Sie entweder die Benutzeroberfläche von BPA oder BPA-Cmdlets in Windows PowerShell verwenden. Sie können diese Ergebnisse jederzeit wieder einschließen.

> [!NOTE]
> Wenn Sie Ergebnisse ausschließen, werden sie auch nicht auf verwalteten Servern angezeigt. Andere Administratoren können ausgeschlossene Ergebnisse auf verwalteten Servern nicht anzeigen. Wenn Sie Ergebnisse nur in einer lokalen Server-Manager Konsole ausschließen möchten, erstellen Sie eine benutzerdefinierte Abfrage, anstatt den Befehl **Ergebnis ausschließen** zu verwenden.

#### <a name="exclude-scan-results"></a><a name=BKMK_exclude></a>Ausschließen von Scanergebnissen
Die Einstellung **Ausschließen** ist persistent. Die von Ihnen ausgeschlossenen Ergebnisse bleiben bei künftigen Scans desselben Modells auf demselben Computer ausgeschlossen, sofern Sie sie nicht wieder einschließen.

Sie können Scanergebnisse mit dem `Set-BPAResult` -Cmdlet in Verbindung mit dem `Exclude` -Parameter ausschließen. Wie in der Best Practices Analyzer Kachel in Server-Manager können Sie einzelne Ergebnis Objekte ausschließen. Sie können auch eine Reihe von Ergebnissen ausschließen, deren Felder (z. b. Kategorie, Titel oder Schweregrad) mit den angegebenen Werten übereinstimmen oder diese enthalten. Beispielsweise können Sie aus einer Reihe von Scanergebnissen für ein Modell alle **Leistungsergebnisse** ausschließen.

> [!NOTE]
> Sie müssen mindestens einen BPA-Scan für ein Modell ausführen, bevor Sie die Verfahren in diesem Abschnitt verwenden können.

###### <a name="to-exclude-scan-results-by-using-the-gui"></a>So schließen Sie Scanergebnisse mithilfe der grafischen Benutzeroberfläche aus

1.  Öffnen Sie eine Rollen-oder Server Gruppenseite in Server-Manager.

2.  Klicken Sie in der Kachel Best Practices Analyzer für die Rolle oder Server Gruppe mit der rechten Maustaste auf ein Ergebnis in der Liste, und klicken Sie dann auf **Ergebnis ausschließen**.

    Das Ergebnis wird nicht mehr in der Liste der Ergebnisse angezeigt.

3.  Führen Sie die integrierte Abfrage **Ausgeschlossene Ergebnisse** aus, um die ausgeschlossenen Ergebnisse auf der grafischen Benutzeroberfläche anzuzeigen. Klicken Sie auf **Gespeicherte Suchabfragen**, und klicken Sie dann auf **Ausgeschlossene Ergebnisse**.

    Beachten Sie, dass nach dem Ausführen der Abfrage **Ausgeschlossene Ergebnisse** der Untertitel der Kachel (eine Beschreibung der in der Liste angezeigten Ergebnisse) sich in **Ausgeschlossene Ergebnisse** ändert. Es werden nur ausgeschlossene Ergebnisse in der Liste angezeigt.

###### <a name="to-exclude-scan-results-by-using-windows-powershell-cmdlets"></a>So schließen Sie Scanergebnisse mithilfe von Windows PowerShell-Cmdlets aus

1.  Öffnen Sie eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten.

2.  Führen Sie den folgenden Befehl aus, um bestimmte Ergebnisse aus einem Modellscan auszuschließen.

    `Get-BPAResult -modelId <model ID> | Where { $_.<Field Name> -eq Value} | Set-BPAResult -Exclude $true`

    Mit dem vorangehenden Befehl werden Ergebnis Elemente des BPA-Scans für die Modell-ID abgerufen, die durch die *Modell-ID*dargestellt wird.

    Mit dem zweiten Abschnitt des Befehls werden die Ergebnisse des `Get-BPAResult`-Cmdlets gefiltert, sodass nur die Scanergebnisse abgerufen werden, bei denen der Wert für ein durch *Feldname* dargestelltes Ergebnisfeld mit dem Text in Anführungszeichen übereinstimmt.

    Mit dem letzten Abschnitt des Befehls, der auf den zweiten senkrechten Strich folgt, werden die vom vorherigen Cmdlet-Abschnitt gefilterten Ergebnisse ausgeschlossen.

    **Beispiel:** `Get-BPAResult -Microsoft/Windows/FileServices | Where { $_.Severity -eq Information} | Set-BPAResult -Exclude $true`

#### <a name="include-scan-results"></a>Einschließen von Scanergebnissen
Wenn Sie ausgeschlossene Scanergebnisse anzeigen möchten, können Sie diese Ergebnisse einschließen. Die Einstellung **Einschließen** ist persistent. Eingeschlossene Ergebnisse bleiben bei künftigen Scans desselben Modells auf demselben Computer eingeschlossen.

##### <a name="to-include-scan-results-by-using-the-gui"></a><a name=BKMK_gui></a>So schließen Sie Scanergebnisse mithilfe der grafischen Benutzeroberfläche ein

1.  Öffnen Sie eine Rollen-oder Server Gruppenseite in Server-Manager.

2.  Klicken Sie in der Kachel Best Practices Analyzer für die Rolle oder Server Gruppe mit der rechten Maustaste in der Abfrage Liste **ausgeschlossene Ergebnisse** auf ein ausgeschlossenes Ergebnis, und klicken Sie dann auf **Ergebnis einschließen**.

    Das Ergebnis wird nicht mehr in der Liste der ausgeschlossenen Ergebnisse angezeigt. Löschen Sie die Abfrage, indem Sie auf **Alle löschen** klicken, um das eingeschlossene Ergebnis in die Liste aller eingeschlossenen Ergebnisse anzuzeigen.

##### <a name="to-include-scan-results-by-using-windows-powershell-cmdlets"></a><a name=BKMK_cmdlets></a>So schließen Sie Scanergebnisse mithilfe von Windows PowerShell-Cmdlets ein

1.  Öffnen Sie eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten.

2.  Geben Sie zum Einschließen bestimmter Ergebnisse aus einem Modellscan den folgenden Befehl ein, und drücken Sie dann die **EINGABETASTE**.

    `Get-BPAResult -modelId <model Id> | Where { $_.<Field Name> -eq Value } | Set-BPAResult -Exclude $false`

    Der vorherige Befehl ruft BPA-Scanergebnis Elemente für das Modell ab, das durch die *Modell-ID*dargestellt wird.

    Mit dem zweiten Teil des Befehls nach dem ersten senkrechter Strich ( **|** ) werden die Ergebnisse des Cmdlets **Get-bparser** gefiltert, sodass nur die Scanergebnisse abgerufen werden, bei denen der Wert des durch *Feldname*dargestellten Ergebnis Felds mit dem Text in Anführungszeichen übereinstimmt.

    Mit dem letzten Abschnitt des Befehls, der auf den zweiten senkrechten Strich folgt, werden die Filterergebnisse des zweiten Cmdlet-Abschnitts eingeschlossen. Dabei wird der **-Exclude**-Parameter auf **false** festgelegt.

    **Beispiel:** `Get-BPAResult -Microsoft/Windows/FileServices | Where { $_.Severity -eq Information} | Set-BPAResult -Exclude $false`

### <a name="view-and-export-bpa-scan-results-in-windows-powershell"></a>Anzeigen und Exportieren von BPA-Scanergebnissen in Windows PowerShell
Informationen zum Anzeigen und Verwalten der Scanergebnisse mithilfe von Windows PowerShell-Cmdlets finden Sie in den folgenden Prozeduren. Bevor Sie eines der folgenden Verfahren verwenden können, müssen Sie mindestens einen BPA-Scan auf mindestens einem Modell oder Teilmodell ausführen.

#### <a name="to-view-results-of-the-most-recent-scan-of-a-role-by-using-windows-powershell"></a><a name=BKMK_recentPS></a>So zeigen Sie mithilfe von Windows PowerShell Ergebnisse des letzten Scans einer Rolle an

1.  Öffnen Sie eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten.

2.  Rufen Sie die Ergebnisse des letzten Scans für eine angegebene Modell-ID ab. Geben Sie Folgendes ein, in dem das Modell durch die *Modell-ID*dargestellt wird, und drücken Sie dann die **Eingabe**Taste. Sie können Ergebnisse für mehrere Modell-IDs abrufen, indem Sie die Modell-IDs durch Kommas trennen.

    `Get-BPAResult <model ID>`

    **Beispiel:** `Get-BPAResult Microsoft/Windows/DNSServer,Microsoft/Windows/FileServices`

    Wenn Sie ein Teil Modell eines Modells (z. b. einen Rollen Dienst) gescannt haben, können Sie nur die Ergebnisse für dieses Teil Modell Abfragen, indem Sie die Teil Modell-ID in das Cmdlet einschließen.

    **Beispiel:** `Get-BPAResult Microsoft/Windows/FileServices -SubmodelID FSRM`

#### <a name="to-view-or-save-bpa-results-from-windows-powershell-sessions-in-different-formats"></a><a name=BKMK_formats></a>So können Sie BPA-Ergebnisse aus Windows PowerShell-Sitzungen in verschiedenen Formaten anzeigen oder speichern

-   In Windows PowerShell ähnelt jedes BPA-Ergebnis dem folgenden.

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

    Führen Sie einen der folgenden Schritte aus:

    -   Wenn Sie BPA-Ergebnisse in einer Tabelle formatieren möchten, führen Sie das folgende Cmdlet aus, und fügen Sie aus dem vorherigen Beispiel die Ergebniseigenschaften hinzu, die Sie anzeigen möchten.

        `Get-BPAResult model ID | format-Table -Property <property1,property2,property3...>`

        **Beispiel:** `Get-BPAResult Microsoft/Windows/FileServices | format-Table -Property modelId,SubmodelId,computerName,Source,Severity,Category,Title,Problem,Impact,Resolution,compliance,help`

    -   Wenn Sie BPA-Ergebnisse in einer auf der grafischen Benutzeroberfläche basierenden Rasteransicht mit einem Textzeichenfolgenfilter und Spaltenüberschriften formatieren möchten, auf die zum Sortieren von Ergebnissen geklickt werden kann, führen Sie das folgende Cmdlet aus.

        `Get-BPAResult <model ID> | OGV`

    -   Um BPA-Ergebnisse in eine HTML-Datei zu exportieren, die archiviert oder an e-Mail-Empfänger gesendet werden kann, führen Sie das folgende Cmdlet aus, wobei *Pfad* den Pfad und den Dateinamen darstellt, in dem die HTML-Ergebnisse gespeichert werden sollen.

        `Get-BPAResult <model ID> | convertTo-Html | Set-Content <path>`

        **Beispiel:** `Get-BPAResult Microsoft/Windows/FileServices | convertTo-Html | Set-Content C:\BPAResults\FileServices.htm`

    -   Um BPA-Ergebnisse in eine CSV-Textdatei (Comma-Separated Values) zu exportieren, führen Sie das folgende Cmdlet aus, wobei *Pfad* den Pfad und den Namen der Textdatei darstellt, in der die CSV-Ergebnisse gespeichert werden sollen. CSV-Ergebnisse können in Microsoft Excel oder andere Programme importiert werden, die Daten in Tabellen oder Rastern anzeigen.

        `Get-BPAResult <model ID> | Export-CSV <path>`

        **Beispiel:** `Get-BPAResult Microsoft/Windows/FileServices | Export-CSV C:\BPAResults\FileServices.txt`

## <a name="see-also"></a>Weitere Informationen
[Best Practices Analyzer Auflösungs Inhalt im Windows Server TechCenter](https://go.microsoft.com/fwlink/p/?LinkId=241597) 
 [Filtern, Sortieren und Abfragen von Daten in Server-Manager Kacheln](filter-sort-and-query-data-in-server-manager-tiles.md) 
 [Verwalten mehrerer Remote Server mit Server-Manager](manage-multiple-remote-servers-with-server-manager.md)
