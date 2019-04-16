---
ms.assetid: 01988844-df02-4952-8535-c87aefd8a38a
title: Bereitstellen der automatischen Dateiklassifizierung (Demonstrationsschritte)
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 1c5c0fa221e0d7375216426f838ba37bee852984
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="deploy-automatic-file-classification-demonstration-steps"></a>Bereitstellen der automatischen Dateiklassifizierung (Demonstrationsschritte)

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

In diesem Thema wird erläutert, wie Ressourceneigenschaften in Active Directory aktivieren, Erstellen von Klassifizierungsregeln auf dem Dateiserver und die Ressourceneigenschaften für Dateien auf dem Dateiserver Werte zuweisen. In diesem Beispiel werden die folgenden Klassifizierungsregeln erstellt:  
  
-   Eine inhaltsklassifizierungsregel, die einen Satz von Dateien für die Zeichenfolge "Contoso vertraulich." durchsucht. Wenn die Zeichenfolge in einer Datei gefunden wird, wird die Ressourceneigenschaft "Impact" auf Hoch auf die Datei festgelegt.  
  
-   Eine inhaltsklassifizierungsregel, die eine Reihe von Dateien für einen regulären Ausdruck durchsucht, die eine Sozialversicherungsnummer mindestens 10 Mal in einer Datei entspricht. Wenn das Muster gefunden wird, wird die Datei mit persönlich identifizierbaren Informationen klassifiziert und persönlich identifizierbare Informationen Ressourceneigenschaft hoch festgelegt ist.  
  
**In diesem Dokument**  
  
-   [Schritt1: Erstellen von ressourceneigenschaftsdefinitionen](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step1)  
  
-   [Schritt2: Erstellen einer zeichenfolgeninhalts-Klassifizierungsregel](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step2)  
  
-   [Schritt3: Erstellen einer Klassifizierungsregel regulären Ausdruck](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step3)  
  
-   [Schritt4: Sicherstellen Sie, dass die Dateien klassifiziert sind](Deploy-Automatic-File-Classification--Demonstration-Steps-.md#BKMK_Step4)  
  
> [!NOTE]  
> Dieses Thema enthält Beispiel für Windows PowerShell-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).  
  
## <a name="BKMK_Step1"></a>Schritt1: Erstellen von ressourceneigenschaftsdefinitionen  
Die Ressourceneigenschaften Auswirkungen und persönlich identifizierbare Informationen sind aktiviert, sodass die Dateiklassifizierungsinfrastruktur diese Ressourceneigenschaften verwenden können, zum Kennzeichnen von Dateien, die auf einem freigegebenen Netzwerkordner gescannt werden.  
  
[Wiederholen Sie diesen Schrittmithilfe von Windows PowerShell](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1)  
  
#### <a name="to-create-resource-property-definitions"></a>Zum Erstellen Sie ressourceneigenschaftsdefinitionen  
  
1.  Melden Sie auf dem Domänencontroller sich an den Server als ein Mitglied der Sicherheitsgruppe "Domänen-Admins".  
  
2.  Active Directory-Verwaltungscenter zu öffnen. Klicken Sie im Server-Manager auf **Tools**, und klicken Sie dann auf **Active Directory-Verwaltungscenter**.  
  
3.  Erweitern Sie **dynamische Zugriffssteuerung**, und klicken Sie dann auf **Ressourceneigenschaften**.  
  
4.  Mit der rechten Maustaste **Auswirkungen**, und klicken Sie dann auf **aktivieren **.  
  
5.  Mit der rechten Maustaste **personenbezogene Informationen**, und klicken Sie dann auf **aktivieren **.  
  
![Lösungshandbücher](media/Deploy-Automatic-File-Classification--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
Set-ADResourceProperty '"Enabled:$true '"Identity:'CN=Impact_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com'   
Set-ADResourceProperty '"Enabled:$true '"Identity:'CN=PII_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com'  
```  
  
## <a name="BKMK_Step2"></a>Schritt2: Erstellen einer zeichenfolgeninhalts-Klassifizierungsregel  
Eine zeichenfolgeninhalts-Klassifizierungsregel durchsucht eine Datei für eine bestimmte Zeichenfolge. Wenn die Zeichenfolge gefunden wird, kann der Wert einer Ressourceneigenschaft konfiguriert werden. In diesem Beispiel wird jede Datei auf einem freigegebenen Netzwerkordner durchsucht und suchen Sie nach der Zeichenfolge "Contoso vertraulich." Wenn die Zeichenfolge gefunden wird, wird die zugehörige Datei mit hoher unternehmensauswirkung klassifiziert.  
  
[Wiederholen Sie diesen Schrittmithilfe von Windows PowerShell](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep2)  
  
#### <a name="to-create-a-string-content-classification-rule"></a>Erstellen eine zeichenfolgeninhalts-Klassifizierungsregel  
  
1.  Melden Sie sich als Mitglied der Sicherheitsgruppe "Administratoren" auf dem Dateiserver an.  
  
2.  Geben Sie in der Windows PowerShell-Eingabeaufforderung **Update-FsrmClassificationPropertyDefinition** und drücken Sie dann die EINGABETASTE. Dadurch wird die Definitionen für Ressourceneigenschaften erstellt, auf dem Domänencontroller mit dem Dateiserver synchronisiert.  
  
3.  File Server Resource Manager zu öffnen. Klicken Sie im Server-Manager auf **Tools**, und klicken Sie dann auf **File Server Resource Manager**.  
  
4.  Erweitern Sie **Klassifizierungsverwaltung**, mit der rechten Maustaste **Klassifizierungsregeln**, und klicken Sie dann auf **Klassifizierungsplan konfigurieren**.  
  
5.  Wählen Sie die **festen Zeitplan aktivieren** Kontrollkästchen die **fortlaufende Klassifizierung für neue Dateien zulassen**, wählen Sie einen Wochentag zum Ausführen der Klassifizierung, und klicken Sie dann auf **OK**.  
  
6.  Mit der rechten Maustaste **Klassifizierungsregeln**, und klicken Sie dann auf **Klassifizierungsregel erstellen**.  
  
7.  Auf der **allgemeine** Registerkarte die **Regelname** geben einen Regelnamen wie z.B. **Contoso vertraulich**.  
  
8.  Auf der **Bereich** auf **hinzufügen**, und wählen Sie die Ordner, die in dieser Regel, z.B. "D:\Finance Documents" einbezogen werden sollen.  
  
    > [!NOTE]  
    > Sie können auch einen dynamischen Namespace für den Bereich auswählen. Weitere Informationen zu dynamischen Namespaces für Klassifizierungsregeln finden Sie unter [What's New in File Server Resource Manager in Windows Server2012 \[redirected\]](assetId:///d53c603e-6217-4b98-8508-e8e492d16083).  
  
9. Auf der **Klassifizierung** Registerkarte, konfigurieren Sie Folgendes:  
  
    -   In der **Auswählen einer Methode für eine Eigenschaft zuzuweisende** sicher, dass **Inhaltsklassifizierung** ausgewählt ist.  
  
    -   In der **zuzuweisende Eigenschaft auswählen** auf **Auswirkungen**.  
  
    -   In der **Geben Sie den Wert** auf **hohe**.  
  
10. Klicken Sie unter der **Parameter** Überschrift klicken Sie auf **konfigurieren**.  
  
11. In der **Ausdruckstyp** Spalte **Zeichenfolge**.  
  
12. In der **Ausdruck** Spalte, Typ **Contoso vertraulich**, und klicken Sie dann auf **OK**.  
  
13. Auf der **Evaluierungstyp** Registerkarte die **vorhandene Eigenschaftenwerte erneut auswerten** Kontrollkästchen, klicken Sie auf **den vorhandenen Wert überschreiben**, und klicken Sie dann auf **OK**.  
  
![Lösungshandbücher](media/Deploy-Automatic-File-Classification--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
$date = Get-Date  
$AutomaticClassificationScheduledTask = New-FsrmScheduledTask -Time $date -Weekly @(3, 2, 4, 5,1,6,0) -RunDuration 0;$AutomaticClassificationScheduledTask  
Set-FsrmClassification -Continuous -schedule $AutomaticClassificationScheduledTask  
New-FSRMClassificationRule -Name 'Contoso Confidential' -Property "Impact_MS" -PropertyValue "3000" -Namespace @('D:\Finance Documents') -ClassificationMechanism "Content Classifier" -Parameters @("StringEx=Min=1;Expr=Contoso Confidential") -ReevaluateProperty Overwrite  
```  
  
## <a name="BKMK_Step3"></a>Schritt3: Erstellen einer Klassifizierungsregel regulären Ausdruck  
Eine Klassifizierungsregel für reguläre Ausdrücke durchsucht eine Datei auf ein Muster, das dem regulären Ausdruck übereinstimmt. Wenn eine Zeichenfolge, die dem regulären Ausdruck übereinstimmt gefunden wird, kann der Wert einer Ressourceneigenschaft konfiguriert werden. In diesem Beispiel wird jede Datei auf einem freigegebenen Netzwerkordner durchsucht und Suchen nach einer Zeichenfolge, die das Muster einer Sozialversicherungsnummer (XXX-XX-XXXX) entspricht. Wenn das Muster gefunden wird, wird die zugehörige Datei mit persönlich identifizierbaren Informationen klassifiziert.  
  
[Wiederholen Sie diesen Schrittmithilfe von Windows PowerShell](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep3)  
  
#### <a name="to-create-a-regular-expression-content-classification-rule"></a>Zum Erstellen einer Klassifizierungsregel regulären Ausdruck  
  
1.  Melden Sie sich mit dem Dateiserver als Mitglied der Sicherheitsgruppe "Administratoren".  
  
2.  Geben Sie in der Windows PowerShell-Eingabeaufforderung **Update-FsrmClassificationPropertyDefinition**, und drücken Sie dann die EINGABETASTE. Dadurch werden die Eigenschaftsdefinitionen synchronisiert, die auf dem Domänencontroller, auf dem Dateiserver erstellt werden.  
  
3.  File Server Resource Manager zu öffnen. Klicken Sie im Server-Manager auf **Tools**, und klicken Sie dann auf **File Server Resource Manager**.  
  
4.  Mit der rechten Maustaste **Klassifizierungsregeln**, und klicken Sie dann auf **Klassifizierungsregel erstellen**.  
  
5.  Auf der **allgemeine** Registerkarte die **Regelname** geben einen Namen für die Klassifizierungsregel wie PII-Regel.  
  
6.  Auf der **Bereich** auf **hinzufügen**, und wählen Sie dann die Ordner, die in dieser Regel, z.B. "D:\Finance Documents" einbezogen werden sollen.  
  
7.  Auf der **Klassifizierung** Registerkarte, konfigurieren Sie Folgendes:  
  
    -   In der **Auswählen einer Methode für eine Eigenschaft zuzuweisende** sicher, dass **Inhaltsklassifizierung** ausgewählt ist.  
  
    -   In der **zuzuweisende Eigenschaft auswählen** auf **personenbezogene Informationen**.  
  
    -   In der **Geben Sie den Wert** auf **hohe**.  
  
8.  Klicken Sie unter der **Parameter** Überschrift klicken Sie auf **konfigurieren**.  
  
9. In der **Ausdruckstyp** Spalte **regulären Ausdruck**.  
  
10. In der **Ausdruck** Spalte, Typ **^ (? 000)([0-7]\d{2}|7([0-7]\d|7[012])) ([-]?) (?! 00) \d\d\3 (? 0000) \d {4} $**  
  
11. In der **mindestens Vorkommen** Spalte, Typ **10**, und klicken Sie dann auf **OK**.  
  
12. Auf der **Evaluierungstyp** Registerkarte die **vorhandene Eigenschaftenwerte erneut auswerten** Kontrollkästchen, klicken Sie auf **den vorhandenen Wert überschreiben**, und klicken Sie dann auf **OK**.  
  
![Lösungshandbücher](media/Deploy-Automatic-File-Classification--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
New-FSRMClassificationRule -Name "PII Rule" -Property "PII_MS" -PropertyValue "5000" -Namespace @('D:\Finance Documents') -ClassificationMechanism "Content Classifier" -Parameters @("RegularExpressionEx=Min=10;Expr=^(?!000)([0-7]\d{2}|7([0-7]\d|7[012]))([ -]?)(?!00)\d\d\3(?!0000)\d{4}$") -ReevaluateProperty Overwrite  
```  
  
## <a name="BKMK_Step4"></a>Schritt4: Stellen Sie sicher, dass die Dateien richtig klassifiziert sind  
Sie können überprüfen, ob die Dateien richtig klassifiziert sind, durch das Anzeigen der Eigenschaften einer Datei, die in den in den Klassifizierungsregeln angegebenen Ordner erstellt wurde.  
  
#### <a name="to-verify-that-the-files-are-classified-correctly"></a>Um sicherzustellen, dass die Dateien richtig klassifiziert sind  
  
1.  Führen Sie auf dem Dateiserver die Klassifizierungsregeln mithilfe von File Server Resource Manager.  
  
    1.  Klicken Sie auf **Klassifizierungsverwaltung**, mit der rechten Maustaste **Klassifizierungsregeln**, und klicken Sie dann auf **Klassifizierung mit allen Regeln jetzt ausführen**.  
  
    2.  Klicken Sie auf die **warten Sie, bis die Klassifizierung abgeschlossen** aus, und klicken Sie dann auf **OK**.  
  
    3.  Schließen Sie die automatische Klassifizierungsbericht.  
  
    4.  Hierzu können Sie mithilfe von Windows PowerShell mit dem folgenden Befehl: **Start-FSRMClassification ' "RunDuration 0 - bestätigen: $false**  
  
2.  Navigieren Sie zu dem Ordner, der in den Klassifizierungsregeln, z.B. "D:\Finance Documents" angegeben wurde.  
  
3.  Maustaste auf eine Datei in diesem Ordner, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie auf die **Klassifizierung** Registerkarte, und stellen Sie sicher, dass die Datei richtig klassifiziert wird.  
  
## <a name="BKMK_Links"></a>Siehe auch  
  
-   [Szenario: Erhalten von Einblicken in Ihre Daten mittels Klassifizierung](Scenario--Get-Insight-into-Your-Data-by-Using-Classification.md)  
  
-   [Planen der automatischen Dateiklassifizierung](assetId:///e3c3bb4b-3034-42b7-b391-8ef5f5851955)  
  
-   [Dynamische Zugriffssteuerung: Szenarioübersicht](Dynamic-Access-Control--Scenario-Overview.md)  
  

