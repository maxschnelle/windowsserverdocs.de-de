---
ms.assetid: 01988844-df02-4952-8535-c87aefd8a38a
title: Bereitstellen der automatischen Dateiklassifizierung (Demonstrationsschritte)
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: cc89e97aacab3b764df7314beeab701df846048a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861253"
---
# <a name="deploy-automatic-file-classification-demonstration-steps"></a>Bereitstellen der automatischen Dateiklassifizierung (Demonstrationsschritte)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema wird erläutert, wie Ressourceneigenschaften in Active Directory aktiviert, Klassifizierungsregeln auf dem Dateiserver erstellt und anschließend Werte zu den Ressourceneigenschaften für Dateien auf dem Dateiserver zugewiesen werden. In diesem Beispiel werden die folgenden Klassifizierungsregeln erstellt:  
  
-   Eine Inhalts Klassifizierungs Regel, die einen Satz von Dateien nach der Zeichenfolge "" mit dem Kontexttyp "Confidential" durchsucht. Wenn die Zeichenfolge in der Datei gefunden wird, wird die Ressourceneigenschaft „Impact“ auf „High“ in der Datei festgelegt.  
  
-   Eine Inhaltsklassifizierungsregel, die eine Reihe von Dateien auf einen regulären Ausdruck hin durchsucht, der mit mindestens zehnmal mit einer Sozialversicherungsnummer in einer Datei übereinstimmt. Wenn das Muster gefunden wird, wird die Datei klassifiziert, dass sie über persönlich identifizierbare Informationen verfügt. Zudem wird die Ressourceneigenschaft „Personally Identifiable Information“ auf „High“ festgelegt.  
  
**In diesem Dokument**  
  
-   [Schritt 1: Erstellen von Ressourcen Eigenschafts Definitionen](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step1)  
  
-   [Schritt 2: Erstellen einer Zeichen folgen Inhalts-Klassifizierungs Regel](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step2)  
  
-   [Schritt 3: Erstellen einer Klassifizierungs Regel für reguläre Ausdrücke](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step3)  
  
-   [Schritt 4: überprüfen, ob die Dateien klassifiziert sind](Deploy-Automatic-File-Classification--Demonstration-Steps-.md#BKMK_Step4)  
  
> [!NOTE]  
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit deren Hilfe einige beschriebene Verfahren automatisiert werden können. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).  
  
## <a name="step-1-create-resource-property-definitions"></a><a name="BKMK_Step1"></a>Schritt 1: Erstellen von Ressourcen Eigenschafts Definitionen  
Die Ressourceneigenschaften „Impact“ und „Personally Identifiable Information“ sind aktiviert, sodass die Dateiklassifizierungsinfrastruktur diese Ressourceneigenschaften verwenden kann, um die Dateien zu kennzeichnen, die in einem freigegeben Netzwerkordner durchsucht werden.  
  
[Führen Sie diesen Schritt mithilfe von Windows PowerShell aus.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1)  
  
#### <a name="to-create-resource-property-definitions"></a>So erstellen Sie Ressourceneigenschaftsdefinitionen  
  
1.  Melden Sie sich auf dem Domänencontroller beim Server als Mitglied der Sicherheitsgruppe "Domänen-Admins" an.  
  
2.  Öffnen Sie das Active Directory-Verwaltungscenter. Klicken Sie im Server-Manager auf **Extras** und dann auf **Active Directory-Verwaltungscenter**.  
  
3.  Erweitern Sie **Dynamische Zugriffssteuerung**, und klicken Sie dann auf **Ressourceneigenschaften**.  
  
4.  Klicken Sie mit der rechten Maustaste auf **Auswirkung**, und klicken Sie dann auf **Aktivieren**.  
  
5.  Klicken Sie mit der rechten Maustaste auf **Personenbezogene Informationen**, und klicken Sie dann auf **Aktivieren**.  
  
![projektmappenanleitung für](media/Deploy-Automatic-File-Classification--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>entsprechende Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets führen dieselbe Funktion wie das vorherige Verfahren aus. Jedes Cmdlet sollte in einer eigenen Zeile eingegeben werden, obwohl sie hier aufgrund von Formateinschränkungen auf mehrere Zeilen umbrochen sein können.  
  
```  
Set-ADResourceProperty '"Enabled:$true '"Identity:'CN=Impact_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com'   
Set-ADResourceProperty '"Enabled:$true '"Identity:'CN=PII_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com'  
```  
  
## <a name="step-2-create-a-string-content-classification-rule"></a><a name="BKMK_Step2"></a>Schritt 2: Erstellen einer Zeichen folgen Inhalts-Klassifizierungs Regel  
Eine Zeichenfolgeninhalts-Klassifizierungsregeln durchsucht eine Datei auf eine bestimmte Zeichenfolge hin. Wenn die Zeichenfolge gefunden wird, kann der Wert einer Ressourceneigenschaft konfiguriert werden. In diesem Beispiel durchsuchen wir jede Datei in einem freigegebenen Netzwerkordner und suchen nach der Zeichenfolge "". Wenn die Zeichenfolge gefunden wird, wird die zugehörige Datei mit hoher Unternehmensauswirkung klassifiziert.  
  
[Führen Sie diesen Schritt mithilfe von Windows PowerShell aus.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep2)  
  
#### <a name="to-create-a-string-content-classification-rule"></a>So erstellen Sie eine Zeichenfolgeninhalts-Klassifizierungsregel  
  
1.  Melden Sie sich als Mitglied der Sicherheitsgruppe „Administratoren“ auf dem Dateiserver an.  
  
2.  Geben Sie an der PowerShell-Eingabeaufforderung **Update-FsrmClassificationPropertyDefinition** ein, und drücken Sie dann die EINGABETASTE. Dadurch werden die auf dem Domänencontroller erstellten Eigenschaftsdefinitionen mit dem Dateiserver synchronisiert.  
  
3.  Öffnen Sie den Ressourcen-Manager für Dateiserver. Klicken Sie in Server-Manager auf **Extras** und dann auf **Ressourcen-Manager für Dateiserver**.  
  
4.  Erweitern Sie **Klassifizierungsverwaltung**, klicken Sie mit der rechten Maustaste auf **Klassifizierungsregeln**, und klicken Sie dann auf **Klassifizierungsplan konfigurieren**.  
  
5.  Aktivieren Sie das Kontrollkästchen **Festen Zeitplan aktivieren** und das Kontrollkästchen **Fortlaufende Klassifizierung für neue Dateien zulassen**, wählen Sie einen Wochentag zum Ausführen der Klassifizierung, und klicken Sie dann auf **OK**.  
  
6.  Klicken Sie mit der rechten Maustaste auf **Klassifizierungsregeln**, und klicken Sie anschließend auf **Klassifizierungsregel erstellen**.  
  
7.  Geben Sie auf der Registerkarte **Allgemein** im Feld **Regelname** einen Regelnamen wie **Contoso Confidential** ein.  
  
8.  Klicken Sie auf der Registerkarte **Bereich** auf **Hinzufügen**, und wählen Sie die Ordner aus, die in dieser Regel einbezogen werden sollen, wie beispielsweise „D:\Finance Documents“.  
  
    > [!NOTE]  
    > Sie können auch einen dynamischen Namespace für den Bereich auswählen. Weitere Informationen zu dynamischen Namespaces für Klassifizierungsregeln finden Sie unter [What es New in File Server Ressourcen-Manager in Windows Server 2012 \[umgeleitet\]](assetId:///d53c603e-6217-4b98-8508-e8e492d16083).  
  
9. Konfigurieren Sie auf der Registerkarte **Klassifizierung** Folgendes:  
  
    -   Stellen Sie im Feld **Methode zum Zuweisen einer Eigenschaft für Dateien auswählen** sicher, dass **Inhaltsklassifizierung** ausgewählt ist.  
  
    -   Klicken Sie im Feld **Daten zuzuweisende Eigenschaft auswählen** auf **Auswirkung**.  
  
    -   Klicken Sie im Feld **Wert angeben** auf **Hoch**.  
  
10. Klicken Sie unter der Überschrift **Parameter** auf **Konfigurieren**.  
  
11. Wählen Sie in der Spalte **Ausdruckstyp** die Option **Zeichenfolge** aus.  
  
12. Geben Sie in der Spalte **Ausdruck** **Contoso Confidential** ein, und klicken Sie dann auf **OK**.  
  
13. Aktivieren Sie auf der Registerkarte **Evaluierungstyp** das Kontrollkästchen **Vorhandene Eigenschaftenwerte erneut auswerten**, klicken Sie auf **Vorhandenen Wert überschreiben**, und klicken Sie dann auf **OK**.  
  
![projektmappenanleitung für](media/Deploy-Automatic-File-Classification--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>entsprechende Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets führen dieselbe Funktion wie das vorherige Verfahren aus. Jedes Cmdlet sollte in einer eigenen Zeile eingegeben werden, obwohl sie hier aufgrund von Formateinschränkungen auf mehrere Zeilen umbrochen sein können.  
  
```  
$date = Get-Date  
$AutomaticClassificationScheduledTask = New-FsrmScheduledTask -Time $date -Weekly @(3, 2, 4, 5,1,6,0) -RunDuration 0;$AutomaticClassificationScheduledTask  
Set-FsrmClassification -Continuous -schedule $AutomaticClassificationScheduledTask  
New-FSRMClassificationRule -Name 'Contoso Confidential' -Property "Impact_MS" -PropertyValue "3000" -Namespace @('D:\Finance Documents') -ClassificationMechanism "Content Classifier" -Parameters @("StringEx=Min=1;Expr=Contoso Confidential") -ReevaluateProperty Overwrite  
```  
  
## <a name="step-3-create-a-regular-expression-content-classification-rule"></a><a name="BKMK_Step3"></a>Schritt 3: Erstellen einer Klassifizierungs Regel für reguläre Ausdrücke  
Eine Klassifizierungsregel für reguläre Ausdrücke durchsucht eine Datei auf ein Muster, das mit dem regulären Ausdruck übereinstimmt. Wenn eine Zeichenfolge gefunden wird, die mit dem gefundenen regulären Ausdruck übereinstimmt, kann der Wert einer Ressourceneigenschaft konfiguriert werden. In diesem Beispiel durchsuchen wir jede Datei in einem freigegebenen Netzwerkordner und suchen nach einer Zeichenfolge, die dem Muster einer Sozialversicherungsnummer (XXX-XX-XXXX) entspricht. Wenn die Zeichenfolge gefunden wird, wird die zugehörige Datei mit persönlich identifizierbaren Informationen klassifiziert.  
  
[Führen Sie diesen Schritt mithilfe von Windows PowerShell aus.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep3)  
  
#### <a name="to-create-a-regular-expression-content-classification-rule"></a>So erstellen Sie eine Klassifizierungsregel für Inhalte mit regulären Ausdrücken  
  
1.  Melden Sie sich als Mitglied der Sicherheitsgruppe "Administratoren" beim Dateiserver an.  
  
2.  Geben Sie an der PowerShell-Eingabeaufforderung **Update-FsrmClassificationPropertyDefinition** ein, und drücken Sie dann die EINGABETASTE. Dadurch werden die Eigenschaftsdefinitionen, die auf dem Domänencontroller erstellt wurden, mit dem Dateiserver synchronisiert.  
  
3.  Öffnen Sie den Ressourcen-Manager für Dateiserver. Klicken Sie in Server-Manager auf **Extras** und dann auf **Ressourcen-Manager für Dateiserver**.  
  
4.  Klicken Sie mit der rechten Maustaste auf **Klassifizierungsregeln**, und klicken Sie anschließend auf **Klassifizierungsregel erstellen**.  
  
5.  Geben Sie auf der Registerkarte **Allgemein** im Feld **Regelname** einen Namen für die Klassifizierungsregel wie „PII-Regel“ ein.  
  
6.  Klicken Sie auf der Registerkarte **Bereich** auf **Hinzufügen**, und wählen Sie dann die Ordner aus, die in dieser Regel einbezogen werden sollen, wie beispielsweise „D:\Finance Documents“.  
  
7.  Konfigurieren Sie auf der Registerkarte **Klassifizierung** Folgendes:  
  
    -   Stellen Sie im Feld **Methode zum Zuweisen einer Eigenschaft für Dateien auswählen** sicher, dass **Inhaltsklassifizierung** ausgewählt ist.  
  
    -   Klicken Sie im Feld **Daten zuzuweisende Eigenschaft auswählen** auf **Personenbezogene Informationen**.  
  
    -   Klicken Sie im Feld **Wert angeben** auf **Hoch**.  
  
8.  Klicken Sie unter der Überschrift **Parameter** auf **Konfigurieren**.  
  
9. Wählen Sie in der Spalte **Ausdruckstyp** die Option **Regulärer Ausdruck** aus.  
  
10. Geben Sie **Expression** in der Spalte Ausdruck **^ (?! 000) ([0-7] \d{2}| 7 ([0-7] \d | 7 [012])) ([-]?) (?! 00) \d\d\3 (?! 0000) \d{4}$**  
  
11. Geben Sie in die Spalte **Min. Anz. von Vorkommen** **10** ein, und klicken Sie dann auf **OK**.  
  
12. Aktivieren Sie auf der Registerkarte **Evaluierungstyp** das Kontrollkästchen **Vorhandene Eigenschaftenwerte erneut auswerten**, klicken Sie auf **Vorhandenen Wert überschreiben**, und klicken Sie dann auf **OK**.  
  
![projektmappenanleitung für](media/Deploy-Automatic-File-Classification--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>entsprechende Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets führen dieselbe Funktion wie das vorherige Verfahren aus. Jedes Cmdlet sollte in einer eigenen Zeile eingegeben werden, obwohl sie hier aufgrund von Formateinschränkungen auf mehrere Zeilen umbrochen sein können.  
  
```  
New-FSRMClassificationRule -Name "PII Rule" -Property "PII_MS" -PropertyValue "5000" -Namespace @('D:\Finance Documents') -ClassificationMechanism "Content Classifier" -Parameters @("RegularExpressionEx=Min=10;Expr=^(?!000)([0-7]\d{2}|7([0-7]\d|7[012]))([ -]?)(?!00)\d\d\3(?!0000)\d{4}$") -ReevaluateProperty Overwrite  
```  
  
## <a name="step-4-verify-that-the-files-are-classified-correctly"></a><a name="BKMK_Step4"></a>Schritt 4: überprüfen, ob die Dateien ordnungsgemäß klassifiziert sind  
Sie können sicherstellen, dass die Dateien richtig klassifiziert sind, indem Sie die Eigenschaften einer Datei anzeigen, die im in den Klassifizierungsregeln angegebenen Ordner erstellt wurde.  
  
#### <a name="to-verify-that-the-files-are-classified-correctly"></a>So stellen Sie die richtige Klassifizierung der Dateien sicher  
  
1.  Führen Sie auf dem Dateiserver die Klassifizierungsregeln mithilfe des Ressourcen-Managers für Dateiserver aus.  
  
    1.  Klicken Sie auf **Klassifizierungsverwaltung**, klicken Sie mit der rechten Maustaste auf **Klassifizierungsregen**, und klicken Sie dann auf **Klassifizierung mit allen Regeln jetzt ausführen**.  
  
    2.  Klicken Sie auf die Option **Warten, bis die Klassifizierung abgeschlossen ist**, und klicken Sie auf **OK**.  
  
    3.  Schließen Sie den Bericht für die automatische Klassifizierung.  
  
    4.  Verwenden Sie hierzu Windows PowerShell mit dem folgenden Befehl: **Start-fsrmclassification ' "RunDuration 0-Confirm: $false**  
  
2.  Wechseln Sie zum Ordner, der in den Klassifizierungsregeln angegeben wurde, wie beispielsweise „D:\Finance Documents“.  
  
3.  Klicken Sie mit der rechten Maustaste auf eine Datei in diesem Ordner, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie auf die Registerkarte **Klassifizierung**, und stellen Sie sicher, dass die Datei richtig klassifiziert wurde.  
  
## <a name="see-also"></a><a name="BKMK_Links"></a>Siehe auch  
  
-   [Szenario: erhalten von Einblicken in Ihre Daten mithilfe der Klassifizierung](Scenario--Get-Insight-into-Your-Data-by-Using-Classification.md)  
  
-   [Planen der automatischen Datei Klassifizierung](https://docs.microsoft.com/previous-versions/orphan-topics/ws.11/jj574209(v%3dws.11))  

  
-   [Dynamisches Access Control: Szenarioübersicht](Dynamic-Access-Control--Scenario-Overview.md)  
  

