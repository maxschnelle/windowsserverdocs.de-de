---
ms.assetid: 2c76e81a-c2eb-439f-a89f-7d3d70790244
title: "Bereitstellen der Verschlüsselung von Office-Dateien (Demonstrationsschritte)"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 529000c60a80ee33fc2aa7d09370d8ac1e06311c
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="deploy-encryption-of-office-files-demonstration-steps"></a>Bereitstellen der Verschlüsselung von Office-Dateien (Demonstrationsschritte)

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Finanzabteilung von Contoso verfügt über eine Reihe von Dateiservern, die ihre Dokumente gespeichert. Diese Dokumente können allgemeinen Dokumentation zu werden oder sie können ein High Business Impact (HBI). Beispielsweise alle Dokumente, die vertrauliche Informationen enthält, von Contoso ein High Business Impact haben gilt. Contoso möchte sicherstellen, dass alle ihre Dokumente ein Mindestmaß an Schutz ist und ihre HBI-Dokumentation auf die richtigen Personen beschränkt ist. Um dies zu erreichen, prüft Contoso die Verwendung der Dateiklassifizierungsinfrastruktur (FCI) und der AD RMS, die in Windows Server2012 verfügbar ist. Mithilfe der FCI wird Contoso alle Dokumente auf dem Dateiserver, basierend auf den Inhalt zu klassifizieren und dann AD RMS verwenden, um die richtigen Benutzerrechterichtlinien anzuwenden.  
  
In diesem Szenario führen Sie die folgenden Schritteaus:  
  
|Aufgabe|Beschreibung|  
|--------|---------------|  
|[Aktivieren von Ressourceneigenschaften](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_1.1)|Aktivieren der **Auswirkungen** und **personenbezogene Informationen** Ressourceneigenschaften.|  
|[Erstellen von Klassifizierungsregeln](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_2)|Erstellen Sie die folgenden Klassifizierungsregeln: **HBI-Klassifizierungsregel** und **PII-Klassifizierungsregel **.|  
|[Verwenden von Dateiverwaltungsaufgaben zum automatischen Schützen von Dokumenten mit AD RMS](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_3)|Erstellen Sie eine Dateiverwaltungsaufgabe, die AD RMS automatisch verwendet, um Dokumente mit hoher persönlich identifizierbare Informationen (PII) zu schützen. Nur Mitglieder der Gruppe "FinanceAdmin" werden auf Dokumente zugreifen, die high PII enthalten.|  
|[Anzeigen der Ergebnisse](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_4)|Prüfen Sie die Klassifizierungen der Dokumente und beobachten Sie, wie sich diese ändern, wenn Sie den Inhalt des Dokuments ändern. Überprüfen Sie außerdem, wie das Dokument von AD RMS geschützt wird.|  
|[Überprüfen Sie die AD RMS-Schutz](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_5)|Stellen Sie sicher, dass das Dokument mit AD RMS geschützt ist.|  
|||  
  
## <a name="BKMK_1.1"></a>Schritt1: Aktivieren von Ressourceneigenschaften  
  
#### <a name="to-enable-resource-properties"></a>Aktivieren von Ressourceneigenschaften  
  
1.  Schließen Sie in Hyper-V-Manager auf Server "id_ad_dc1" her. Melden Sie sich an den Server mit "Contoso\Administrator" mit dem Kennwort **pass@word1**.  
  
2.  Öffnen Sie Active Directory Administrative Center, und klicken Sie dann auf **Strukturansicht **.  
  
3.  Erweitern Sie **dynamische ZUGRIFFSSTEUERUNG**, und wählen Sie **Ressourceneigenschaften **.  
  
4.  Führen Sie einen Bildlauf nach unten, um die **Auswirkungen** Eigenschaft in der **Anzeigenamen** Spalte. Mit der rechten Maustaste **Auswirkungen**, und klicken Sie dann auf **aktivieren **.  
  
5.  Führen Sie einen Bildlauf nach unten, um die **personenbezogene Informationen** Eigenschaft in der **Anzeigenamen** Spalte. Mit der rechten Maustaste **personenbezogene Informationen**, und klicken Sie dann auf **aktivieren **.  
  
6.  So veröffentlichen Sie die Ressourceneigenschaften in der **globalen Ressourcenliste**, klicken Sie im linken Bereich auf **Ressourceneigenschaftenlisten**, und doppelklicken Sie dann auf **globale Ressourceneigenschaftenliste **.  
  
7.  Klicken Sie auf **hinzufügen**, und führen Sie einen Bildlauf nach unten, und klicken Sie auf **Auswirkungen** der Liste hinzuzufügen. Gleiches gilt für **personenbezogene Informationen **. Klicken Sie auf **OK** zweimal auf Fertig stellen.  
  
![Lösungshandbücher](media/Deploy-Encryption-of-Office-Files--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
Set-ADResourceProperty -Enabled:$true -Identity:"CN=Impact_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com"  
Set-ADResourceProperty -Enabled:$true -Identity:"CN=PII_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com" 
```  
  
## <a name="BKMK_2"></a>Schritt2: Erstellen von Klassifizierungsregeln  
Dieser Schrittwird erläutert, wie zum Erstellen der **weitreichenden** Klassifizierungsregel. Mit dieser Regel wird den Inhalt von Dokumenten durchsucht, und wenn die Zeichenfolge "Contoso vertraulich" gefunden wird, erfolgt die Klassifizierung des dieses Dokuments als High Business Impact. Diese Klassifizierung setzt alle zuvor zugewiesenen Klassifizierungen der Low Business Impact außer Kraft.  
  
Außerdem erstellen Sie eine **High PII** Regel. Mit dieser Regel wird den Inhalt von Dokumenten durchsucht, und wenn eine Sozialversicherungsnummer gefunden wird, werden Sie das Dokument als high PII klassifiziert.  
  
#### <a name="to-create-the-high-impact-classification-rule"></a>Zum Erstellen der Klassifizierungsregel aussagekräftige  
  
1.  Schließen Sie in Hyper-V-Manager auf Server "id_ad_file1" her. Melden Sie sich an den Server mit "Contoso\Administrator" mit dem Kennwort **pass@word1**.  
  
2.  Sie müssen die globalen Ressourceneigenschaften aus Active Directory aktualisieren. Öffnen Sie Windows PowerShell, und geben: `Update-FSRMClassificationPropertyDefinition`, und drücken Sie dann die EINGABETASTE. Schließen Sie WindowsPowerShell.  
  
3.  File Server Resource Manager zu öffnen. File Server Resource Manager zu öffnen, klicken Sie auf **starten**, Typ **Ressourcen-Manager für Dateiserver**, und klicken Sie dann auf **File Server Resource Manager**.  
  
4.  Erweitern Sie im linken Bereich des File Server Resource Manager **Klassifizierungsverwaltung**, und wählen Sie dann **Klassifizierungsregeln **.  
  
5.  In der **Aktionen** Bereich, klicken Sie auf **Klassifizierungsplan konfigurieren **. Auf der **automatische Klassifizierung** Registerkarte **festen Zeitplan aktivieren**wählen eine **Tag der Woche**, und wählen Sie dann die **fortlaufende Klassifizierung für neue Dateien zulassen** Kontrollkästchen. Klicken Sie auf **OK**.  
  
6.  In der **Aktionen** Bereich, klicken Sie auf **Klassifizierungsregel erstellen **. Daraufhin wird die **Klassifizierungsregel erstellen** Dialogfeld.  
  
7.  In der **Regelname** geben **High Business Impact **.  
  
8.  In der **Beschreibung** geben **bestimmt, ob das Dokument großen geschäftsrelevanten Einfluss basierend auf das Vorhandensein der Zeichenfolge "Contoso Confidential" verfügt.**  
  
9. Auf der **Bereich** auf **Ordnerverwaltungseigenschaften festlegen**Option **Verwendung Ordner**, klicken Sie auf **hinzufügen**, klicken Sie dann auf **Durchsuchen**, als Pfad "D:\Finance Documents", klicken Sie auf **OK**, und wählen Sie dann den Wert einer Eigenschaft namens **Gruppieren von Dateien**, und klicken Sie auf **schließen **. Wenn Management-Eigenschaften festgelegt sind, auf die **Regelbereich** wählen Registerkarte **Gruppendateien **.  
  
10. Klicken Sie auf die **Klassifizierung** Registerkarte.  Klicken Sie unter **Auswählen einer Methode für die Eigenschaft zuzuweisende**Option **Inhaltsklassifizierung** aus der Dropdownliste.  
  
11. Klicken Sie unter **zuzuweisende Eigenschaft auswählen**Option **Auswirkungen** aus der Dropdownliste.  
  
12. Klicken Sie unter **Geben Sie den Wert**Option **hohe** aus der Dropdownliste.  
  
13. Klicken Sie auf **konfigurieren** unter **Parameter **.  In der **Klassifizierungsparameter** Dialogfeld, in der **Ausdruckstyp** Liste **Zeichenfolge **. In der **Ausdruck** geben: **Contoso vertraulich**, und klicken Sie dann auf **OK **.  
  
14. Klicken Sie auf die **Evaluierungstyp** Registerkarte.  Klicken Sie auf **vorhandene Eigenschaftenwerte erneut auswerten**, klicken Sie auf **überschreiben**der vorhandene Wert, und klicken Sie dann auf **OK** beendet.  
  
![Lösungshandbücher](media/Deploy-Encryption-of-Office-Files--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
Update-FSRMClassificationPropertyDefinition  
$date = Get-Date  
$AutomaticClassificationScheduledTask = New-FsrmScheduledTask -Time $date -Weekly @(3, 2, 4, 5,1,6,0) -RunDuration 0;  
Set-FsrmClassification -Continuous -schedule $AutomaticClassificationScheduledTask  
New-FSRMClassificationRule -Name "High Business Impact" -Property "Impact_MS" -Description "Determines if the document has a high business impact based on the presence of the string 'Contoso Confidential'" -PropertyValue "3000" -Namespace @("D:\Finance Documents") -ClassificationMechanism "Content Classifier" -Parameters @("StringEx=Min=1;Expr=Contoso Confidential") -ReevaluateProperty Overwrite  
```  
  
#### <a name="to-create-the-high-pii-classification-rule"></a>Die High PII-Klassifizierungsregel erstellen  
  
1.  Schließen Sie in Hyper-V-Manager auf Server "id_ad_file1" her. Melden Sie sich an den Server mit "Contoso\Administrator" mit dem Kennwort **pass@word1**.  
  
2.  Öffnen Sie auf dem Desktop den Ordner mit dem Namen **reguläre Ausdrücke**, und öffnen Sie dann das Textdokument **RegEx-SSN **. Markieren und kopieren Sie die folgende reguläre Ausdruckszeichenfolge: **^ (? 000)([0-7]\d{2}|7([0-7]\d|7[012])) ([-]?) (?! 00) \d\d\3 (? 0000) \d {4} $**. Diese Zeichenfolge verwendet werden weiter unten in diesem Schrittbelassen sie Sie daher in der Zwischenablage.  
  
3.  File Server Resource Manager zu öffnen. File Server Resource Manager zu öffnen, klicken Sie auf **starten**, Typ **Ressourcen-Manager für Dateiserver**, und klicken Sie dann auf **File Server Resource Manager**.  
  
4.  Erweitern Sie im linken Bereich des File Server Resource Manager **Klassifizierungsverwaltung**, und wählen Sie dann **Klassifizierungsregeln **.  
  
5.  In der **Aktionen** Bereich, klicken Sie auf **Klassifizierungsplan konfigurieren **. Auf der **automatische Klassifizierung** Registerkarte **festen Zeitplan aktivieren**wählen eine **Tag der Woche**, und wählen Sie dann die **fortlaufende Klassifizierung für neue Dateien zulassen** Kontrollkästchen. Klicken Sie auf OK.  
  
6.  In der **Regelname** geben **High PII **. In der **Beschreibung** geben **fest, ob das Dokument ein High hat PII basierend auf dem Vorhandensein einer Sozialversicherungsnummer.**  
  
7.  Klicken Sie auf die **Bereich** Registerkarte die **Gruppendateien** Kontrollkästchen.  
  
8.  Klicken Sie auf die **Klassifizierung** Registerkarte.  Klicken Sie unter **Auswählen einer Methode für die Eigenschaft zuzuweisende**Option **Inhaltsklassifizierung** aus der Dropdownliste.  
  
9. Klicken Sie unter **zuzuweisende Eigenschaft auswählen**Option **personenbezogene Informationen** aus der Dropdownliste.  
  
10. Klicken Sie unter **Geben Sie den Wert**Option **hohe** aus der Dropdownliste.  
  
11. Klicken Sie auf **konfigurieren** unter **Parameter **.   
    In der **Klassifizierungsparameter**Fenster, in der **Ausdruckstyp** Liste **regulären Ausdruck **. In der **Ausdruck** Feld, fügen Sie den Text aus der Zwischenablage: **^ (? 000)([0-7]\d{2}|7([0-7]\d|7[012])) ([-]?) (?! 00) \d\d\3 (? 0000) \d {4} $**, und klicken Sie dann auf **OK **.  
  
    > [!NOTE]  
    > Dieser Ausdruck lässt ungültige Sozialversicherungsnummern. Dies ermöglicht es, in der Demonstration frei erfundene Sozialversicherungsnummern verwenden.  
  
12. Klicken Sie auf die **Evaluierungstyp** Registerkarte.  Wählen Sie **vorhandene Eigenschaftenwerte erneut auswerten**, **überschreiben**der vorhandene Wert, und klicken Sie dann auf **OK** beendet.  
  
![Lösungshandbücher](media/Deploy-Encryption-of-Office-Files--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
New-FSRMClassificationRule -Name "High PII" -Description "Determines if the document has a high PII based on the presence of a Social Security Number." -Property "PII_MS" -PropertyValue "5000" -Namespace @("D:\Finance Documents") -ClassificationMechanism "Content Classifier" -Parameters @("RegularExpressionEx=Min=1;Expr=^(?!000)([0-7]\d{2}|7([0-7]\d|7[012]))([ -]?)(?!00)\d\d\3(?!0000)\d{4}$") -ReevaluateProperty Overwrite  
```  
  
Sie verfügen jetzt über zwei Klassifizierungsregeln:  
  
-   High Businessimpact  
  
-   High PII  
  
## <a name="BKMK_3"></a>Schritt3: Verwenden von Dateiverwaltungsaufgaben zum automatischen Schützen von Dokumenten mit AD RMS  
Nun, dass Sie Dokumente basierend auf dem Inhalt automatisch klassifiziert Regeln erstellt haben, wird im nächste Schritteine Dateiverwaltungsaufgabe zu erstellen, die AD RMS verwendet, um bestimmte Dokumente basierend auf deren Klassifizierung automatisch zu schützen. In diesem Schritterstellen Sie eine Dateiverwaltungsaufgabe, die automatisch alle Dokumente mit einem high PII geschützt werden. Nur Mitglieder der Gruppe "FinanceAdmin" werden auf Dokumente zugreifen, die high PII enthalten.  
  
#### <a name="to-protect-documents-with-ad-rms"></a>So schützen Sie Dokumente mit AD RMS  
  
1.  Schließen Sie in Hyper-V-Manager auf Server "id_ad_file1" her. Melden Sie sich an den Server mit "Contoso\Administrator" mit dem Kennwort **pass@word1**.  
  
2.  File Server Resource Manager zu öffnen. File Server Resource Manager zu öffnen, klicken Sie auf **starten**, Typ **Ressourcen-Manager für Dateiserver**, und klicken Sie dann auf **File Server Resource Manager**.  
  
3.  Wählen Sie im linken Bereich **Dateiverwaltungsaufgaben **. In der **Aktionen** Bereich **Dateiverwaltungsaufgabe erstellen **.  
  
4.  In der **den Namen der Aufgabe:** geben **High PII **. In der **Beschreibung** geben **automatische RMS-Schutz für high PII-Dokumente **.  
  
5.  Klicken Sie auf die **Bereich** Registerkarte die **Gruppendateien** Kontrollkästchen.  
  
6.  Klicken Sie auf die **Aktion** Registerkarte. Klicken Sie unter **Typ**Option **RMS-Verschlüsselung **. Klicken Sie auf **Durchsuchen**, wählen Sie eine Vorlage aus, und wählen Sie dann die **nur Contoso-Finanzadmins** Vorlage.  
  
7.  Klicken Sie auf die **Bedingung** Registerkarte, und klicken Sie dann auf **hinzufügen **. Klicken Sie unter **Eigenschaft**Option **personenbezogene Informationen **. Klicken Sie unter **Operator**Option **gleich **. Klicken Sie unter **Wert**Option **hohe **. Klicken Sie auf **OK**.  
  
8.  Klicken Sie auf die **Zeitplan** Registerkarte. In der **Zeitplan** auf **wöchentlichen**, und wählen Sie dann **Sonntag **. Die Aufgabe einmal pro Woche ausführen wird sichergestellt, dass alle Dokumente erfasst werden, die aufgrund eines dienstausfalls oder andere störenden Ereignis verpasst wurden.  
  
9. In der **Betrieb** Abschnitt **Aufgabe für neue Dateien fortlaufend ausführen**, und klicken Sie dann auf **OK **. Sie verfügen jetzt über eine Dateiverwaltungsaufgabe, die mit dem Namen High PII.  
  
![Lösungshandbücher](media/Deploy-Encryption-of-Office-Files--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
$fmjRmsEncryption = New-FSRMFmjAction -Type 'Rms' -RmsTemplate 'Contoso Finance Admin Only'  
$fmjCondition1 = New-FSRMFmjCondition -Property 'PII_MS' -Condition 'Equal' -Value '5000'  
$date = get-date  
$schedule = New-FsrmScheduledTask -Time $date -Weekly @('Sunday')    
$fmj1=New-FSRMFileManagementJob -Name "High PII" -Description "Automatic RMS protection for high PII documents" -Namespace @('D:\Finance Documents') -Action $fmjRmsEncryption -Schedule $schedule -Continuous -Condition @($fmjCondition1)  
```  
  
## <a name="BKMK_4"></a>Schritt4: Anzeigen der Ergebnisse  
Es ist nun einen Blick auf die neuen automatische Klassifizierung und Regeln für AD RMS-Schutz in Aktion. In diesem Schrittwerden Sie untersuchen Sie die Klassifizierungen der Dokumente und beobachten, wie sich diese ändern, wenn Sie den Inhalt des Dokuments ändern.  
  
#### <a name="to-view-the-results"></a>Zum Anzeigen der Ergebnisse  
  
1.  Schließen Sie in Hyper-V-Manager auf Server "id_ad_file1" her. Melden Sie sich an den Server mit "Contoso\Administrator" mit dem Kennwort **pass@word1**.  
  
2.  Navigieren Sie in Windows-Explorer zu "D:\Finance Documents".  
  
3.  Mit der rechten Maustaste in des Dokuments "Finance Memo", und klicken Sie auf **Eigenschaften**. Klicken Sie auf die **Klassifizierung** Registerkarte, und beachten Sie, dass die Eigenschaft Auswirkungen derzeit keinen Wert aufweist. Klicken Sie auf **Abbrechen **.  
  
4.  Mit der rechten Maustaste die **Request for Approval to Hire Dokument**, und wählen Sie dann **Eigenschaften **.  
  
5.  Klicken Sie auf die **Klassifizierung** Registerkarte, und beachten Sie, dass **die Eigenschaft personenbezogene Informationen** derzeit hat keinen Wert. Klicken Sie auf **Abbrechen **.  
  
6.  Wechseln Sie auf "client1". Jeder Benutzer, der angemeldet ist melden, und melden Sie sich dann als "contoso\mreid" mit dem Kennwort **pass@word1**.  
  
7.  Öffnen Sie auf dem Desktop, die **Finanzdokumente** freigegebenen Ordner.  
  
8.  Öffnen der **"Finance Memo"** Dokument. Im unteren Bereich des Dokuments, sehen Sie das Wort **vertraulich **. Ändern sie die Zeichenfolge: **Contoso vertraulich **. Speichern Sie das Dokument, und schließen Sie es.  
  
9. Öffnen der **Request for Approval to Hire** Dokument. In der **Social Security#:** Geben Sie im Abschnitt: 777-77-7777. Speichern Sie das Dokument, und schließen Sie es.  
  
    > [!NOTE]  
    > Möglicherweise müssen Sie warten 30Sekunden für die Klassifizierung erfolgen kann.  
  
10. Wechseln Sie zu "id_ad_file1" her. Navigieren Sie in Windows-Explorer zu "D:\Finance Documents".  
  
11. Maustaste auf das Dokument "Finance Memo", und klicken Sie auf **Eigenschaften **. Klicken Sie auf die **Klassifizierung** Registerkarte. Beachten Sie, dass die **Auswirkungen** Eigenschaftensatz ist jetzt auf **hohe **. Klicken Sie auf **Abbrechen **.  
  
12. Mit der rechten Maustaste der Anforderung zur Genehmigung Hire Dokument und klicken Sie dann auf **Eigenschaften **.  
  
13. . Klicken Sie auf die **Klassifizierung** Registerkarte. Beachten Sie, dass die **personenbezogene Informationen** Eigenschaftensatz ist jetzt auf **hohe **. Klicken Sie auf **Abbrechen **.  
  
## <a name="BKMK_5"></a>Schritt5: Überprüfen der AD RMS-Schutzes  
  
#### <a name="to-verify-that-the-document-is-protected"></a>Um sicherzustellen, dass das Dokument geschützt ist  
  
1.  Wechseln Sie zu "id_ad_client1".  
  
2.  Öffnen der **Request for Approval to Hire** Dokument.  
  
3.  Klicken Sie auf **OK** auf das Dokument eine Verbindung mit dem AD RMS-Server herstellen kann.  
  
4.  Sie können jetzt sehen, dass das Dokument durch AD RMS geschützt ist, weil es eine Sozialversicherungsnummer enthält.  
  

