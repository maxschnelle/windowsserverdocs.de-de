---
ms.assetid: 2c76e81a-c2eb-439f-a89f-7d3d70790244
title: Bereitstellen der Verschlüsselung von Office-Dateien (Demonstrationsschritte)
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 05da1b7df2e3242c9b68bd7858c824f91e81a563
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407102"
---
# <a name="deploy-encryption-of-office-files-demonstration-steps"></a>Bereitstellen der Verschlüsselung von Office-Dateien (Demonstrationsschritte)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die Finanzabteilung von "die Finanzabteilung von" ist eine Reihe von Dateiservern, auf denen Ihre Dokumente gespeichert werden. Diese Dokumente können von allgemeiner Natur oder aber unternehmenskritisch sein, d. h. großen geschäftsrelevanten Einfluss (High Business Impact, HBI) haben. So werden beispielsweise alle Dokumente mit vertraulichen Informationen von Contoso als HBI-Dokumente erachtet. Contoso möchte sicherstellen, dass die gesamte Firmendokumentation ein Mindestmaß an Schutz erhält und der Zugriff auf die HBI-Dokumente auf die richtigen (entsprechend berechtigten) Personen beschränkt ist. Zu diesem Zweck wird von "Configuration Manager" die Verwendung der Datei Klassifizierungs Infrastruktur (File Classification Infrastructure, FCI) und der AD RMS untersucht, die in Windows Server 2012 verfügbar ist. Mithilfe der FCI klassifiziert Contoso alle auf dem Dateiserver vorhandenen Dokumente basierend auf dem Inhalt und verwendet dann AD RMS, um die richtigen Benutzerrechterichtlinien anzuwenden.  
  
In diesem Szenario führen Sie die folgenden Schritte aus:  
  
|Aufgabe|Beschreibung|  
|--------|---------------|  
|[Aktivieren von Ressourcen Eigenschaften](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_1.1)|Aktivieren Sie die Ressourceneigenschaften **Auswirkung** und **Personenbezogene Informationen** (Personally Identifiable Information, PII).|  
|[Erstellen von Klassifizierungsregeln](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_2)|Erstellen Sie die folgenden Klassifizierungsregeln: **HBI-Klassifizierungsregel** und **PII-Klassifizierungsregel**.|  
|[Verwenden von Datei Verwaltungsaufgaben zum automatischen schützen von Dokumenten mit AD RMS](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_3)|Erstellen Sie eine Dateiverwaltungsaufgabe, die AD RMS automatisch verwendet, um Dokumente mit personenbezogenen Informationen (Personally Identifiable Information, PII) zu schützen. Nur Mitglieder der Gruppe "FinanzAdmin" haben Zugriff auf Dokumente mit High PII.|  
|[Anzeigen der Ergebnisse](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_4)|Prüfen Sie die Klassifizierungen der Dokumente, und beobachten Sie, wie sich diese ändern, wenn Sie den Inhalt des Dokuments ändern. Überprüfen Sie zudem, wie das Dokument von AD RMS geschützt wird.|  
|[Überprüfen des AD RMS Schutzes](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_5)|Überprüfen Sie, ob das Dokument mit AD RMS geschützt ist.|  
|||  
  
## <a name="BKMK_1.1"></a>Schritt 1: Aktivieren von Ressourceneigenschaften  
  
#### <a name="to-enable-resource-properties"></a>So aktivieren Sie Ressourceneigenschaften  
  
1. Stellen Sie in Hyper-V-Manager eine Verbindung mit dem Server "ID_AD_DC1" her. Melden Sie sich mit dem Kennwort <strong>pass@word1</strong>beim Server an.  
  
2. Öffnen Sie das Active Directory-Verwaltungscenter, und klicken Sie auf **Strukturansicht**.  
  
3. Erweitern Sie **DYNAMISCHE ZUGRIFFSTEUERUNG**, und wählen Sie **Ressourceneigenschaften**aus.  
  
4. Führen Sie in der Spalte **Anzeigename** einen Bildlauf zur Eigenschaft **Auswirkung** durch. Klicken Sie mit der rechten Maustaste auf **Auswirkung**, und klicken Sie dann auf **Aktivieren**.  
  
5. Führen Sie in der Spalte **Anzeigename** einen Bildlauf zur Eigenschaft **Personenbezogene Informationen** durch. Klicken Sie mit der rechten Maustaste auf **Personenbezogene Informationen**, und klicken Sie dann auf **Aktivieren**.  
  
6. Wenn Sie die Ressourceneigenschaften in der **Globalen Ressourcenliste** veröffentlichen möchten, klicken Sie im linken Bereich auf **Ressourceneigenschaftenlisten**, und doppelklicken Sie dann auf **Globale Ressourceneigenschaftenliste**.  
  
7. Klicken Sie auf **Hinzufügen**, führen Sie einen Bildlauf zu **Auswirkung** durch, und klicken Sie dann darauf, um die Eigenschaft zur Liste hinzuzufügen. Führen Sie dieselben Aktionen für **Personenbezogene Informationen** aus. Klicken Sie abschließend zweimal auf **OK** .  
  
![solution Guides](media/Deploy-Encryption-of-Office-Files--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell äquivalente Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
Set-ADResourceProperty -Enabled:$true -Identity:"CN=Impact_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com"  
Set-ADResourceProperty -Enabled:$true -Identity:"CN=PII_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com" 
```  
  
## <a name="BKMK_2"></a>Schritt 2: Erstellen von Klassifizierungsregeln  
Hier erfahren Sie, wie die Klassifizierungsregel **High Impact** erstellt wird. Mit dieser Regel wird der Inhalt von Dokumenten durchsucht, und wenn die Zeichenfolge "" mit dem Wert "" von "" "," Diese Klassifizierung setzt alle zuvor zugewiesenen Klassifizierungen vom Typ LBI (Low Business Impact) außer Kraft.  
  
Außerdem erstellen Sie die Regel **High PII** . Mit dieser Regel wird der Inhalt von Dokumenten durchsucht, und wenn eine Sozialversicherungsnummer gefunden wird, erfolgt die Klassifizierung des Dokuments als High PII-Dokument.  
  
#### <a name="to-create-the-high-impact-classification-rule"></a>So erstellen Sie die Klassifizierungsregel "High Impact"  
  
1. Stellen Sie in Hyper-V-Manager eine Verbindung mit dem Server "ID_AD_FILE1" her. Melden Sie sich mit dem Kennwort <strong>pass@word1</strong>beim Server an.  
  
2. Sie müssen die globalen Ressourceneigenschaften aus Active Directory aktualisieren. Öffnen Sie Windows PowerShell, geben Sie `Update-FSRMClassificationPropertyDefinition`ein, und drücken Sie dann die EINGABETASTE. Schließen Sie Windows PowerShell.  
  
3. Öffnen Sie den Ressourcen-Manager für Dateiserver. Klicken Sie zum Öffnen des Ressourcen-Managers für Dateiserver auf **Start**, geben Sie **Ressourcen-Manager für Dateiserver**ein, und klicken Sie dann auf **Ressourcen-Manager für Dateiserver**.  
  
4. Erweitern Sie im linken Bereich des Ressourcen-Managers für Dateiserver die Struktur von **Klassifizierungsverwaltung**, und wählen Sie dann **Klassifizierungsregeln**aus.  
  
5. Klicken Sie im Bereich **Aktionen** auf **Klassifizierungsplan konfigurieren**. Wählen Sie auf der Registerkarte **Automatische Klassifizierung** die Option **Festen Zeitplan aktivieren** aus, wählen Sie einen **Wochentag** aus, und aktivieren Sie dann das Kontrollkästchen **Fortlaufende Klassifizierung für neue Dateien zulassen**. Klicken Sie auf **OK**.  
  
6. Klicken Sie im Bereich **Aktionen** auf **Klassifizierungsregel erstellen**. Das Dialogfeld **Klassifizierungsregel erstellen** wird geöffnet.  
  
7. Geben Sie im Feld **Regelname** die Zeichenfolge **High Business Impact** ein.  
  
8. Geben Sie im Feld **Beschreibung** **ein, um zu ermitteln, ob das Dokument aufgrund des Vorhandenseins der Zeichenfolge "kontoso Confidential" eine hohe geschäftliche Auswirkung hat** .  
  
9. Klicken Sie auf der Registerkarte **Bereich** auf **Ordnerverwaltungseigenschaften festlegen**. Wählen Sie **Ordnerverwendung**aus, klicken Sie auf **Hinzufügen**, und klicken Sie dann auf **Durchsuchen**. Navigieren Sie zum Pfad "D:\Finance Documents", klicken Sie auf **OK**, und wählen Sie dann einen Eigenschaftswert namens **Gruppendateien** aus, und klicken Sie auf **Schließen**. Nachdem Sie die Verwaltungseigenschaften festgelegt haben, können Sie auf der Registerkarte **Regelbereich** die Option **Gruppendateien**auswählen.  
  
10. Klicken Sie auf die Registerkarte **Klassifizierung**.  Wählen Sie unter Methode zum Zuweisen einer Eigenschaft für Dateien auswählenin der Dropdownliste den Eintrag **Inhaltsklassifizierung** aus.  
  
11. Wählen Sie unter **Daten zuzuweisende Eigenschaft auswählen** in der Dropdownliste den Eintrag **Auswirkung** aus.  
  
12. Wählen Sie unter **Wert angeben** in der Dropdownliste den Eintrag **Hoch** aus.  
  
13. Klicken Sie unter **Parameter** auf **Konfigurieren**.  Wählen Sie im Dialogfeld **Klassifizierungsparameter** in der Liste **Ausdruckstyp** die Option **Zeichenfolge**aus. Geben Sie im Feld **Ausdruck** Folgendes ein: Contoso Vertraulich. Klicken Sie dann auf **OK**.  
  
14. Klicken Sie auf die Registerkarte **Evaluierungstyp** .  Klicken Sie auf Vorhandene Eigenschaftenwerte erneut auswerten, auf **Vorhandenen Wert überschreiben**und dann auf **OK** , um den Vorgang abzuschließen.  
  
![solution Guides](media/Deploy-Encryption-of-Office-Files--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell äquivalente Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
Update-FSRMClassificationPropertyDefinition  
$date = Get-Date  
$AutomaticClassificationScheduledTask = New-FsrmScheduledTask -Time $date -Weekly @(3, 2, 4, 5,1,6,0) -RunDuration 0;  
Set-FsrmClassification -Continuous -schedule $AutomaticClassificationScheduledTask  
New-FSRMClassificationRule -Name "High Business Impact" -Property "Impact_MS" -Description "Determines if the document has a high business impact based on the presence of the string 'Contoso Confidential'" -PropertyValue "3000" -Namespace @("D:\Finance Documents") -ClassificationMechanism "Content Classifier" -Parameters @("StringEx=Min=1;Expr=Contoso Confidential") -ReevaluateProperty Overwrite  
```  
  
#### <a name="to-create-the-high-pii-classification-rule"></a>So erstellen Sie die Klassifizierungsregel "High PII"  
  
1. Stellen Sie in Hyper-V-Manager eine Verbindung mit dem Server "ID_AD_FILE1" her. Melden Sie sich mit dem Kennwort <strong>pass@word1</strong>beim Server an.  
  
2. Öffnen Sie auf dem Desktop den Ordner **Reguläre Ausdrücke**, und öffnen Sie dann das Textdokument **RegEx-SSN**. Markieren und kopieren Sie die folgende reguläre Ausdrucks Zeichenfolge: **^ (?! 000) ([0-7] \d @ no__t-1 | 7 ([0-7] \d | 7 [012])) ([-]?) (?! 00) \d\d\3 (?! 0000) \d @ no__t-2 $** . Diese Zeichenfolge wird im späteren Verlauf in diesem Schritt verwendet. Belassen Sie sie daher in der Zwischenablage.  
  
3. Öffnen Sie den Ressourcen-Manager für Dateiserver. Klicken Sie zum Öffnen des Ressourcen-Managers für Dateiserver auf **Start**, geben Sie **Ressourcen-Manager für Dateiserver**ein, und klicken Sie dann auf **Ressourcen-Manager für Dateiserver**.  
  
4. Erweitern Sie im linken Bereich des Ressourcen-Managers für Dateiserver die Struktur von **Klassifizierungsverwaltung**, und wählen Sie dann **Klassifizierungsregeln**aus.  
  
5. Klicken Sie im Bereich **Aktionen** auf **Klassifizierungsplan konfigurieren**. Wählen Sie auf der Registerkarte **Automatische Klassifizierung** die Option **Festen Zeitplan aktivieren** aus, wählen Sie einen **Wochentag** aus, und aktivieren Sie dann das Kontrollkästchen **Fortlaufende Klassifizierung für neue Dateien zulassen**. Klicken Sie auf „OK“.  
  
6. Geben Sie im Feld **Regelname** die Zeichenfolge **High PII**ein. Geben Sie im Feld **Beschreibung** Folgendes ein: **Ermittelt basierend auf dem Vorhandensein einer Sozialversicherungsnummer, ob das Dokument ein High PII-Dokument ist**  
  
7. Klicken Sie auf die Registerkarte **Bereich** , und aktivieren Sie das Kontrollkästchen **Gruppendateien** .  
  
8. Klicken Sie auf die Registerkarte **Klassifizierung**.  Wählen Sie unter Methode zum Zuweisen einer Eigenschaft für Dateien auswählenin der Dropdownliste den Eintrag **Inhaltsklassifizierung** aus.  
  
9. Wählen Sie unter **Daten zuzuweisende Eigenschaft auswählen** in der Dropdownliste den Eintrag **Personenbezogene Informationen** aus.  
  
10. Wählen Sie unter **Wert angeben** in der Dropdownliste den Eintrag **Hoch** aus.  
  
11. Klicken Sie unter **Parameter** auf **Konfigurieren**.   
    Klicken Sie im Bereich **Klassifizierungsparameter**in der Liste **Ausdruckstyp** die Option **Regulärer Ausdruck**. Fügen Sie im Feld **Ausdruck** den Text aus der Zwischenablage ein: **^ (?! 000) ([0-7] \d @ no__t-2 | 7 ([0-7] \d | 7 [012])) ([-]?) (?! 00) \d\d\3 (?! 0000) \d @ no__t-3 $** , und klicken Sie dann auf **OK**.  
  
    > [!NOTE]  
    > Dieser Ausdruck lässt ungültige Sozialversicherungsnummern zu. Dadurch können wir in der Demonstration frei erfundene Sozialversicherungsnummern verwenden.  
  
12. Klicken Sie auf die Registerkarte **Evaluierungstyp** .  Wählen Sie Vorhandene Eigenschaftenwerte erneut auswerten, **Vorhandenen Wert überschreiben**, und klicken Sie dann auf **OK** , um den Vorgang abzuschließen.  
  
![solution Guides](media/Deploy-Encryption-of-Office-Files--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell äquivalente Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
New-FSRMClassificationRule -Name "High PII" -Description "Determines if the document has a high PII based on the presence of a Social Security Number." -Property "PII_MS" -PropertyValue "5000" -Namespace @("D:\Finance Documents") -ClassificationMechanism "Content Classifier" -Parameters @("RegularExpressionEx=Min=1;Expr=^(?!000)([0-7]\d{2}|7([0-7]\d|7[012]))([ -]?)(?!00)\d\d\3(?!0000)\d{4}$") -ReevaluateProperty Overwrite  
```  
  
Sie verfügen jetzt über zwei Klassifizierungsregeln:  
  
-   High Business Impact  
  
-   High PII  
  
## <a name="BKMK_3"></a>Schritt 3: Verwenden von Datei Verwaltungsaufgaben zum automatischen schützen von Dokumenten mit AD RMS  
Nachdem Sie nun Regeln zum automatischen klassifizieren von Dokumenten basierend auf Inhalt erstellt haben, ist der nächste Schritt das Erstellen einer Datei Verwaltungsaufgabe, die AD RMS verwendet, um bestimmte Dokumente basierend auf deren Klassifizierung automatisch zu schützen. In diesem Schritt erstellen Sie eine Dateiverwaltungsaufgabe, die Dokumente mit personenbezogenen Informationen vom Typ "High PII" automatisch schützt. Nur Mitglieder der Gruppe "FinanzAdmin" haben Zugriff auf Dokumente mit High PII.  
  
#### <a name="to-protect-documents-with-ad-rms"></a>So schützen Sie Dokumente mit AD RMS  
  
1. Stellen Sie in Hyper-V-Manager eine Verbindung mit dem Server "ID_AD_FILE1" her. Melden Sie sich mit dem Kennwort <strong>pass@word1</strong>beim Server an.  
  
2. Öffnen Sie den Ressourcen-Manager für Dateiserver. Klicken Sie zum Öffnen des Ressourcen-Managers für Dateiserver auf **Start**, geben Sie **Ressourcen-Manager für Dateiserver**ein, und klicken Sie dann auf **Ressourcen-Manager für Dateiserver**.  
  
3. Wählen Sie im linken Bereich die Option **Dateiverwaltungsaufgaben** aus. Wählen Sie im Bereich **Aktionen** die Option **Dateiverwaltungsaufgabe erstellen**aus.  
  
4. Geben Sie im Feld **Aufgabenname** die Zeichenfolge **High PII**ein. Geben Sie im Feld **Beschreibung** Folgendes ein: **Automatischer RMS-Schutz für High PII-Dokumente**.  
  
5. Klicken Sie auf die Registerkarte **Bereich** , und aktivieren Sie das Kontrollkästchen **Gruppendateien** .  
  
6. Klicken Sie auf die Registerkarte **Aktion** . Wählen Sie unter Typdie Option **RMS-Verschlüsselung**aus. Klicken Sie auf **Durchsuchen**, um eine Vorlage auszuwählen, und wählen Sie dann die Vorlage **Nur Contoso-FinanzAdmins** aus.  
  
7. Klicken Sie auf die Registerkarte **Bedingung** , und klicken Sie dann auf **Hinzufügen**. Wählen Sie unter **Eigenschaft** die Option **Personenbezogene Informationen** aus. Wählen Sie unter **Operator**die Option **Gleich**aus. Wählen Sie unter **Wert** die Option **Hoch** aus. Klicken Sie auf **OK**.  
  
8. Klicken Sie auf die Registerkarte **Zeitplan** . Klicken Sie im Abschnitt Zeitplan auf **Wöchentlich**, und wählen Sie dann **Sonntag** aus. Wenn Sie die Aufgabe einmal pro Woche ausführen, können Sie sicherstellen, dass alle Dokumente erfasst werden, die möglicherweise aufgrund eines Dienstausfalls oder einer anderen Unterbrechung nicht berücksichtigt wurden.  
  
9. Wählen Sie im Abschnitt **Fortlaufende Ausführung** die Option **Für neue Dateien fortlaufend ausführen**aus, und klicken Sie dann auf **OK**. Sie verfügen jetzt über eine Dateiverwaltungsaufgabe mit dem Namen "High PII".  
  
![solution Guides](media/Deploy-Encryption-of-Office-Files--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell äquivalente Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
$fmjRmsEncryption = New-FSRMFmjAction -Type 'Rms' -RmsTemplate 'Contoso Finance Admin Only'  
$fmjCondition1 = New-FSRMFmjCondition -Property 'PII_MS' -Condition 'Equal' -Value '5000'  
$date = get-date  
$schedule = New-FsrmScheduledTask -Time $date -Weekly @('Sunday')    
$fmj1=New-FSRMFileManagementJob -Name "High PII" -Description "Automatic RMS protection for high PII documents" -Namespace @('D:\Finance Documents') -Action $fmjRmsEncryption -Schedule $schedule -Continuous -Condition @($fmjCondition1)  
```  
  
## <a name="BKMK_4"></a>Schritt 4: Anzeigen der Ergebnisse  
Es ist an der Zeit, sich die neuen Regeln für die automatische Klassifizierung und AD RMS Schutz in Aktion anzusehen. In diesem Schritt prüfen Sie die Klassifizierungen der Dokumente und beobachten, wie sich diese ändern, wenn Sie den Inhalt des Dokuments ändern.  
  
#### <a name="to-view-the-results"></a>So zeigen Sie die Ergebnisse an  
  
1. Stellen Sie in Hyper-V-Manager eine Verbindung mit dem Server "ID_AD_FILE1" her. Melden Sie sich mit dem Kennwort <strong>pass@word1</strong>beim Server an.  
  
2. Navigieren Sie in Windows-Explorer zum Ordner "D:\Finance Documents".  
  
3. Klicken Sie mit der rechten Maustaste auf das Dokument "Finance Memo", und klicken Sie auf **Eigenschaften**. Klicken Sie auf die Registerkarte **Klassifizierung** . Beachten Sie, dass der Eigenschaft "Auswirkung" aktuell kein Wert zugewiesen ist. Klicken Sie auf **Abbrechen**.  
  
4. Klicken Sie mit der rechten Maustaste auf das Dokument **Request for Approval to Hire**, und klicken Sie dann auf **Eigenschaften**.  
  
5. Klicken Sie auf die Registerkarte **Klassifizierung**. Beachten Sie, dass der Eigenschaft **Personenbezogene Informationen** aktuell kein Wert zugewiesen ist. Klicken Sie auf **Abbrechen**.  
  
6. Wechseln Sie zu "CLIENT1". Melden Sie alle angemeldeten Benutzer ab, und melden Sie sich dann als "condeso\mreid" mit dem Kennwort <strong>pass@word1</strong>an.  
  
7. Öffnen Sie auf dem Desktop den freigegebenen Ordner **Finance Documents** .  
  
8. Öffnen Sie das Dokument **Finance Memo**. Fast am Ende des Dokuments steht das Wort **Vertraulich**. Ändern Sie die Zeichenfolge wie folgt: **Contoso Vertraulich**. Speichern und schließen Sie das Dokument.  
  
9. Öffnen Sie das Dokument **Request for Approval to Hire** . Geben Sie im Abschnitt **Social Security#:** die folgende Sozialversicherungsnummer ein: 777-77-7777. Speichern und schließen Sie das Dokument.  
  
    > [!NOTE]  
    > Sie müssen möglicherweise 30 Sekunden warten, bis die Klassifizierung angezeigt wird.  
  
10. Wechseln Sie wieder zurück zu "ID_AD_FILE1". Navigieren Sie in Windows-Explorer zum Ordner "D:\Finance Documents".  
  
11. Klicken Sie mit der rechten Maustaste auf das Dokument "Finance Memo", und klicken Sie auf **Eigenschaften**. Klicken Sie auf die Registerkarte **Klassifizierung**. Beachten Sie, dass die Eigenschaft Auswirkung jetzt auf **Hoch** festgelegt ist. Klicken Sie auf **Abbrechen**.  
  
12. Klicken Sie mit der rechten Maustaste auf das Dokument "Request for Approval to Hire", und klicken Sie dann auf **Eigenschaften**.  
  
13. . Klicken Sie auf die Registerkarte **Klassifizierung**. Beachten Sie, dass die Eigenschaft Personenbezogene Informationen jetzt auf **Hoch** festgelegt ist. Klicken Sie auf **Abbrechen**.  
  
## <a name="BKMK_5"></a>Schritt 5: Überprüfen des Schutzes mit AD RMS  
  
#### <a name="to-verify-that-the-document-is-protected"></a>So überprüfen Sie, ob das Dokument geschützt ist  
  
1.  Wechseln Sie wieder zurück zu "ID_AD_CLIENT1".  
  
2.  Öffnen Sie das Dokument **Request for Approval to Hire** .  
  
3.  Klicken Sie auf **OK** , damit das Dokument eine Verbindung mit dem AD RMS-Server herstellen kann.  
  
4.  Sie können jetzt sehen, dass das Dokument durch AD RMS geschützt ist, weil es eine Sozialversicherungsnummer enthält.  
  

