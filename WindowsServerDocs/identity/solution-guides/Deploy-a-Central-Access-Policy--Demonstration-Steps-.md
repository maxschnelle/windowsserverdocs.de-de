---
ms.assetid: 8738c03d-6ae8-49a7-8b0c-bef7eab81057
title: Bereitstellen einer zentralen Zugriffsrichtlinie (Demonstrationsschritte)
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 16973b32407985ffc3f66bf5ac579384a756b5d0
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="deploy-a-central-access-policy-demonstration-steps"></a>Bereitstellen einer zentralen Zugriffsrichtlinie (Demonstrationsschritte)

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

In diesem Szenario wird der Finance-Abteilung Sicherheitsvorgänge mit der zentralen Informationssicherheit an einer zentralen Zugriffsrichtlinie erforderlich, damit sie auf Dateiservern archivierte Finanzinformationen schützen können. Die archivierten Finanzinformationen jedes Land kann durch alle finanzmitarbeiter aus demselben Land als schreibgeschützt zugegriffen werden. Eine zentrale finanzadministratorgruppe kann die Finanzinformationen aus allen Ländern zugreifen.  
  
Bereitstellen einer zentralen Zugriffsrichtlinie beinhaltet die folgenden Phasen:  
  
|Phase|Beschreibung  
|---------|---------------  
|[Plan: Identifizieren der richtliniennotwendigkeit und der für die Bereitstellung erforderlichen Konfiguration](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md#BKMK_1.2)|Identifizieren Sie die Notwendigkeit einer Richtlinie und der für die Bereitstellung erforderlichen Konfiguration. 
|[Implementieren: Konfigurieren der Komponenten und Richtlinie](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md#BKMK_1.3)|Konfigurieren der Komponenten und Richtlinie.  
|[Bereitstellen der zentralen Zugriffsrichtlinie](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md#BKMK_1.4)|Bereitstellen Sie diese Richtlinie.  
|[Verwalten Sie ändern und Staging der Richtlinie](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md#BKMK_1.5)|Richtlinienänderungen und Staging. 
  
## <a name="BKMK_1.1"></a>Einrichten einer Testumgebung  
Bevor Sie beginnen, müssen Sie Labor zum Testen dieses Szenarios einrichten. Die Schrittezum Einrichten des Labors werden detailliert erläutert [AnhangB: Setting Up the Test Environment ](Appendix-B--Setting-Up-the-Test-Environment.md).  
  
## <a name="BKMK_1.2"></a>Plan: Identifizieren der richtliniennotwendigkeit und der für die Bereitstellung erforderlichen Konfiguration  
Dieser Abschnittenthält die Reihe allgemeiner Schritte, die in der Planungsphase Ihrer Bereitstellung unterstützen.  
  
||Schritt|Beispiel|  
|-|--------|-----------|  
|1.1|Unternehmen bestimmt, dass eine zentrale Zugriffsrichtlinie erforderlich ist|Um Finanzinformationen zu schützen, die auf Dateiservern gespeichert sind, die Finanzabteilung Abteilung Sicherheitsvorgänge mit der zentralen Informationssicherheit an einer zentralen Zugriffsrichtlinie erforderlich.|  
|1.2|Ausdrücken der Zugriffsrichtlinie|Finanzdokumente sollten nur von Mitgliedern der Finanzabteilung gelesen werden. Mitglieder der Finanzabteilung sollten nur auf Dokumente in ihrem eigenen Land zugreifen. Nur Finanzadministratoren sollten Schreibzugriff haben. Für Mitglieder der Gruppe "FinanceException" wird eine Ausnahme zugelassen. Diese Gruppe verfügt über Lesezugriff.|  
|1.3|Ausdrücken der Zugriffsrichtlinie in Windows Server2012-Konstrukten|Werbung:<br /><br />-"Resource.Department" enthält "Finance"<br /><br />Regeln:<br /><br />– Kann User.Country=Resource.Country und User.department = "Resource.Department"<br />-Vollzugriff User.MemberOf(FinanceAdmin)<br /><br />Ausnahme:<br /><br />Lesen memberOf(FinanceException) zulassen|  
|1.4|Bestimmen Sie, die für die Richtlinie erforderlichen Dateieigenschaften|Dateien kennzeichnen mit:<br /><br />-Abteilung<br />-Land|  
|1.5|Bestimmen Sie die Anspruchstypen und für die Richtlinie erforderlichen Gruppen|Anspruchstypen:<br /><br />-Land<br />-Abteilung<br /><br />Gruppen:<br /><br />-FinanceAdmin<br />-"Financeexception"|  
|1.6|Bestimmen Sie den Server, auf denen diese Richtlinie anwenden|Wenden Sie die Richtlinie auf alle finanzdateiserver an.|  
  
## <a name="BKMK_1.3"></a>Implementieren: Konfigurieren der Komponenten und Richtlinie  
Dieser Abschnittenthält ein Beispiel, das eine zentrale Zugriffsrichtlinie für Finanzdokumente bereitgestellt wird.  
  
|Nein|Schritt|Beispiel|  
|------|--------|-----------|  
|2.1|Erstellen von Anspruchstypen|Erstellen Sie die folgenden Anspruchstypen:<br /><br />-Abteilung<br />-Land|  
|2.2|Erstellen von Ressourceneigenschaften|Erstellen Sie und aktivieren Sie die folgenden Eigenschaften:<br /><br />-Abteilung<br />-Land|  
|2.3|Konfigurieren einer zentralen Zugriffsregel|Erstellen Sie eine Regel für Finanzdokumente, die die im vorherigen Abschnittbestimmte Richtlinie enthält.|  
|2.4|Konfigurieren einer zentralen Zugriffsrichtlinie (CAP)|Erstellen Sie eine CAP Finance Policy aufgerufen, und fügen Sie dieser zentralen Zugriffsrichtlinie die Regel für Finanzdokumente hinzu.|  
|2.5|Zentrale Zugriffsrichtlinie auf den Dateiservern abzielen|Veröffentlichen der Finance-CAP-Richtlinie auf den Dateiservern.|  
|2.6|Aktivieren Sie KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos Armoring.|Aktivieren Sie KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos Armoring für contoso.com.|  
  
Im folgenden Verfahren erstellen Sie zwei Anspruchstypen: Land "und" Department.  
  
#### <a name="to-create-claim-types"></a>Zum Erstellen von Anspruchstypen  
  
1.  Öffnen Sie Server "DC1" im Hyper-V-Manager, und melden sich als "Contoso\administrator" mit dem Kennwort **pass@word1**.  
  
2.  Active Directory-Verwaltungscenter zu öffnen.  
  
3.  Klicken Sie auf die **strukturansichtssymbol**, erweitern Sie **dynamische Zugriffssteuerung**, und wählen Sie dann **Anspruchstypen **.  
  
    Mit der rechten Maustaste **Anspruchstypen**, klicken Sie auf **neu**, und klicken Sie dann auf **Anspruchstyp **.  
  
    > [!TIP]  
    > Sie können auch Öffnen einer **Anspruchstyp erstellen:** Fenster aus der **Aufgaben** Bereich. Auf der **Aufgaben** Bereich, klicken Sie auf **neu**, und klicken Sie dann auf **Anspruchstyp **.  
  
4.  In der **Quellattribut** aus, führen Sie einen Bildlauf nach unten durch die Liste der Attribute, und auf **Abteilung **. Dies sollte Auffüllen der **Anzeigenamen** Feld **Abteilung **. Klicken Sie auf **OK**.  
  
5.  In **Aufgaben** Bereich, klicken Sie auf **neu**, und klicken Sie dann auf **Anspruchstyp**.  
  
6.  In der **Quellattribut** aufzulisten, führen Sie einen Bildlauf nach unten durch die Liste der Attribute und klicken Sie dann auf die **c** Attribut (Ländername). In der **Anzeigenamen** geben **Land**.  
  
7.  In der **vorgeschlagene Werte** Abschnitt **die folgenden Werte werden vorgeschlagen:**, und klicken Sie dann auf **hinzufügen**.  
  
8.  In der **Wert** und **Anzeigenamen** Felder, Typ **US**, und klicken Sie dann auf **OK**.  
  
9. Wiederholen Sie den obigen Schritt. In der **vorgeschlagenen Wert hinzufügen**, geben Sie im Dialogfeld **JP** in die **Wert** und **Anzeigenamen** Felder, und klicken Sie dann auf **OK**.  
  
![Lösungshandbücher](media/Deploy-a-Central-Access-Policy--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
 
    New-ADClaimType country -SourceAttribute c -SuggestedValues:@((New-Object Microsoft.ActiveDirectory.Management.ADSuggestedValueEntry("US","US","")), (New-Object Microsoft.ActiveDirectory.Management.ADSuggestedValueEntry("JP","JP","")))  
    New-ADClaimType department -SourceAttribute department  
      
 
  
> [!TIP]  
> Können die Windows PowerShell-Verlaufsanzeige im Active Directory-Verwaltungscenter auf um Windows PowerShell-Cmdlets nach jeder Prozedur zu durchsuchen, die Sie im Active Directory-Verwaltungscenter ausführen. Weitere Informationen finden Sie unter [Windows PowerShell History Viewer](https://technet.microsoft.com/library/hh831702)  
  
Im nächste Schrittwerden Ressourceneigenschaften erstellt. Im folgenden Verfahren erstellen Sie eine Ressourceneigenschaft, die die Liste der globalen Ressourceneigenschaften auf dem Domänencontroller automatisch hinzugefügt wird, damit sie für den Dateiserver verfügbar ist.  
  
#### <a name="to-create-and-enable-pre-created-resource-properties"></a>So erstellen und aktivieren vorab erstellte Ressourceneigenschaften  
  
1.  Klicken Sie im linken Bereich des Active Directory-Verwaltungscenters auf **Strukturansicht**. Erweitern Sie **dynamische Zugriffssteuerung**, und wählen Sie dann **Ressourceneigenschaften**.  
  
2.  Mit der rechten Maustaste **Ressourceneigenschaften**, klicken Sie auf **neu**, und klicken Sie dann auf **Referenzressourceneigenschaft**.  
  
    > [!TIP]  
    > Sie können auch eine Ressourceneigenschaft aus der **Aufgaben** Bereich. Klicken Sie auf **neu**, und klicken Sie dann auf **Referenzressourceneigenschaft**.  
  
3.  In **wählen Sie ein Anspruchstyp zum Freigeben wird vorgeschlagen Werte Liste**, klicken Sie auf **Land**.  
  
4.  In der **Anzeigenamen** geben **Land**, und klicken Sie dann auf **OK**.  
  
5.  Doppelklicken Sie auf die **Ressourceneigenschaften** aufzulisten, führen Sie einen Bildlauf nach unten, um die **Abteilung** Ressourceneigenschaft. Mit der rechten Maustaste, und klicken Sie dann auf **aktivieren**. Dadurch kann die integrierte **Abteilung** Ressourceneigenschaft.  
  
6.  In der **Ressourceneigenschaften** Liste im Navigationsbereich des Active Directory-Verwaltungscenter, Sie haben nun zwei aktivierte Ressourceneigenschaften:  
  
    -   Land  
  
    -   Abteilung  
  
![Lösungshandbücher](media/Deploy-a-Central-Access-Policy--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
New-ADResourceProperty Country -IsSecured $true -ResourcePropertyValueType MS-DS-MultivaluedChoice -SharesValuesWith country  
Set-ADResourceProperty Department_MS -Enabled $true  
Add-ADResourcePropertyListMember "Global Resource Property List" -Members Country  
Add-ADResourcePropertyListMember "Global Resource Property List" -Members Department_MS  
  
```  
  
Der nächste Schrittist die Erstellung zentrale Zugriffsregeln, die definieren, wer auf Ressourcen zugreifen können. In diesem Szenario lauten die Geschäftsregeln:  
  
-   Finanzdokumente können nur von Mitgliedern der Finanzabteilung gelesen werden.  
  
-   Mitglieder der Finanzabteilung können nur auf Dokumente in ihrem eigenen Land zugreifen.  
  
-   Nur Finanzadministratoren können über Schreibzugriff verfügen.  
  
-   Wir können eine Ausnahme für Mitglieder der Gruppe "FinanceException". Diese Gruppe verfügt über Lesezugriff.  
  
-   Der Administrator auch der Dokumentbesitzer haben weiterhin Vollzugriff.  
  
Oder zum Ausdrücken der Regeln mit Windows Server2012-Konstrukten:  
  
Werbung: "Resource.Department" enthält "Finance"  
  
Regeln:  
  
-   Lesen User.Country=Resource.Country und User.department zulassen = "Resource.Department"  
  
-   Vollzugriff User.MemberOf(FinanceAdmin)  
  
-   Lesen User.MemberOf(FinanceException) zulassen  
  
#### <a name="to-create-a-central-access-rule"></a>Erstellen Sie eine zentrale Zugriffsregel  
  
1.  Klicken Sie im linken Bereich des Active Directory-Verwaltungscenter auf **Strukturansicht**Option **dynamische Zugriffssteuerung**, und klicken Sie dann auf **zentrale Zugriffsregeln**.  
  
2.  Mit der rechten Maustaste **zentrale Zugriffsregeln**, klicken Sie auf **neu**, und klicken Sie dann auf **zentrale Zugriffsregel**.  
  
3.  In den **Namen** geben **Finance Documents Rule**.  
  
4.  In der **Zielressourcen** auf **bearbeiten**, und in der **zentrale Zugriffsregel** Dialogfeld klicken Sie auf **eine Bedingung hinzufügen,**. Fügen Sie die folgende Bedingung hinzu:   
    [**Ressource**] [**Abteilung**] [**Gleich**] [**Value**] [**Finanzen**], und klicken Sie dann auf **OK**.  
  
5.  In der **Berechtigungen** Abschnitt **folgende Berechtigungen als aktuelle Berechtigungen verwenden**, klicken Sie auf **bearbeiten**, und in der **Advanced Security Settings for Berechtigungen** Dialogfeld auf **hinzufügen**.  
  
    > [!NOTE]  
    > **Verwenden Sie die folgenden Berechtigungen als vorgesehene Berechtigungen** Option können Sie die Richtlinie in Staging erstellen. Weitere Informationen hierzu finden Sie in der verwalten: Ändern und Phase im Richtlinienabschnitt "in diesem Thema.  
  
6.  In der **Berechtigungseintrag für Berechtigungen** Dialogfeld, klicken Sie auf **Prinzipal auswählen**, Typ **authentifizierte Benutzer**, und klicken Sie dann auf **OK**.  
  
7.  In der **Berechtigungseintrag für Berechtigungen** Dialogfeld, klicken Sie auf **eine Bedingung hinzufügen,**, und fügen Sie die folgenden Bedingungen hinzu:   
    [**User**] [**Land**] [**Any of**] [**Ressource**] [**Land**]   
     Klicken Sie auf **fügen Sie eine Bedingung**.   
     [**And**]   
    Klicken Sie auf [**Benutzer**] [**Abteilung**] [**eines**] [**Ressource**] [**Abteilung**]. Legen Sie die **Berechtigungen** auf **lesen**.  
  
8.  Klicken Sie auf **OK**, und klicken Sie dann auf **hinzufügen**. Klicken Sie auf **Prinzipal auswählen**, Typ **FinanceAdmin**, und klicken Sie dann auf **OK**.  
  
9. Wählen Sie die **ändern, lesen und ausführen, lesen, schreiben** Berechtigungen, und klicken Sie dann auf **OK**.  
  
10. Klicken Sie auf **hinzufügen**, klicken Sie auf **Prinzipal auswählen**, Typ **FinanceException**, und klicken Sie dann auf **OK**. Wählen Sie die Berechtigungen werden **lesen** und **Lese- und Ausführungsberechtigungen**.  
  
11. Klicken Sie auf **OK** dreimal ab, und kehren Sie zu Active Directory-Verwaltungscenter zurück.  
  
    ![Lösungshandbücher](media/Deploy-a-Central-Access-Policy--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
    Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
 
    $countryClaimType = Get-ADClaimType Land  
    $departmentClaimType = Get-ADClaimType Abteilung  
    $countryResourceProperty = Get-ADResourceProperty Land  
    $departmentResourceProperty = Get-ADResourceProperty Abteilung  
    $currentAcl = "O:SYG:SYD:AR(A;; FA;; O W) (A; FA;; BA) (A; 0 x1200a9;; S-1-5-21-1787166779-1215870801-2157059049-1113) (A; 0 x1301bf;; S-1-5-21-1787166779-1215870801-2157059049-1112) (A; FA;; SY) (XA; 0 x1200a9;; AU;((@USER." + $countryClaimType.Name + "Any_of @RESOURCE." + $countryResourceProperty.Name + ") & & (@USER." + $departmentClaimType.Name + "Any_of @RESOURCE." + $departmentResourceProperty.Name + ")))"  
    $resourceCondition = "(@RESOURCE." + $departmentResourceProperty.Name + "enthält {`"Finance`"}) "  
    New-ADCentralAccessRule "Finance Documents Rule" - CurrentAcl $currentAcl - ResourceCondition $resourceCondition  

  
> [!IMPORTANT]  
> Im obigen Cmdlet-Beispiel werden die Sicherheits-IDs (SIDs) für die Gruppe "financeadmin" und der Benutzer wird zur Erstellungszeit bestimmt und unterscheiden sich in Ihrem Beispiel. Beispielsweise die bereitgestellten SID-Wert (S-1-5-21-1787166779-1215870801-2157059049-1113) für die FinanceAdmins muss durch die tatsächliche Sicherheits-ID für die Gruppe "FinanceAdmin" ersetzt werden, die Sie in Ihrer Bereitstellung erstellen müssen. Sie können Windows PowerShell verwenden, suchen Sie nach der SID-Wert dieser Gruppe, den Wert einer Variablen zuweisen und verwenden Sie die Variable hier. Weitere Informationen finden Sie unter [Windows PowerShell-Tipp: Verwenden von SIDs](https://go.microsoft.com/fwlink/?LinkId=253545).  
  
Sie verfügen jetzt über eine zentrale Zugriffsregel, die Personen Zugriff auf Dokumente aus demselben Land und derselben Abteilung ermöglicht. Die Regel ermöglicht der Gruppe "FinanceAdmin", die Dokumente zu bearbeiten, und ermöglicht der Gruppe "FinanceException", um die Dokumente zu lesen. Diese Regel zielt nur auf Dokumente als Finance klassifiziert.  
  
#### <a name="to-add-a-central-access-rule-to-a-central-access-policy"></a>Eine zentrale Zugriffsrichtlinie einer zentralen Zugriffsregel hinzu  
  
1.  Klicken Sie im linken Bereich des Active Directory-Verwaltungscenter auf **dynamische Zugriffssteuerung**, und klicken Sie dann auf **zentrale Zugriffsrichtlinien**.  
  
2.  In der **Aufgaben** Bereich, klicken Sie auf **neu**, und klicken Sie dann auf **zentrale Zugriffsrichtlinie**.  
  
3.  In **zentrale Zugriffsrichtlinie erstellen:**, Typ **Finance Policy** in den **Namen** Feld.  
  
4.  In **Member zentrale Zugriffsregeln**, klicken Sie auf **hinzufügen**.  
  
5.  Doppelklicken Sie auf die **Finance Documents Rule** mit dem sie die **folgende zentrale Zugriffsregeln hinzufügen** aus, und klicken Sie dann auf **OK**.  
  
6.  Klicken Sie auf **OK** beendet. Sie verfügen jetzt über eine zentrale Zugriffsrichtlinie namens Finance Policy.  
  
    ![Lösungshandbücher](media/Deploy-a-Central-Access-Policy--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
    Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
    ```  
    New-ADCentralAccessPolicy "Finance Policy" Add-ADCentralAccessPolicyMember   
    -Identity "Finance Policy"   
    -Member "Finance Documents Rule"  
  
    ```  
  
#### <a name="to-apply-the-central-access-policy-across-file-servers-by-using-group-policy"></a>Die zentrale Zugriffsrichtlinie dateiserverübergreifend anwenden, mithilfe von Gruppenrichtlinien  
  
1.  Auf der **starten** Bildschirm, in der **Suche** geben **die Gruppenrichtlinien-Verwaltungskonsole**. Doppelklicken Sie auf **Gruppenrichtlinienverwaltung**.  
  
    > [!TIP]  
    > Wenn die **Verwaltungstools anzeigen** Einstellung deaktiviert ist, die **Verwaltung** Ordner und dessen Inhalt werden nicht angezeigt, dem **Einstellungen** Ergebnisse.  
  
    > [!TIP]  
    > In Ihrer Produktionsumgebung sollten Sie erstellen eine Datei Server Organisationseinheit (OU) und alle Ihre Dateiserver dieser Organisationseinheit hinzufügen, möchten Sie diese Richtlinie anwenden. Sie können dann eine Gruppenrichtlinie erstellen und dieser Richtlinie diese Organisationseinheit hinzufügen.  
  
2.  In diesem Schrittbearbeiten Sie das Gruppenrichtlinienobjekt, das Sie erstellt, in haben [Erstellen des Domänencontrollers](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_Build) Abschnittin der Umgebung für die zentrale Zugriffsrichtlinie enthalten, die Sie erstellt haben. In der Gruppenrichtlinienverwaltungs-Editor, wechseln Sie zu, und wählen Sie die Organisationseinheit, in der Domäne (in diesem Beispiel contoso.com): **Gruppenrichtlinienverwaltung**, **Gesamtstruktur: contoso.com**, **Domänen**, **contoso.com**, **Contoso**, **FileServerOU **.  
  
3.  Mit der rechten Maustaste **flexibleAccessGPO**, und klicken Sie dann auf **bearbeiten **.  
  
4.  Wechseln Sie in der Gruppenrichtlinienverwaltungs-Editor-Fenster zu **Computerkonfiguration**, erweitern Sie **Richtlinien**, erweitern Sie **Windows-Einstellungen**, und klicken Sie auf **Sicherheitseinstellungen **.  
  
5.  Erweitern Sie **Dateisystem**, mit der rechten Maustaste **zentrale Zugriffsrichtlinie**, und klicken Sie dann auf **zentrale Zugriffsrichtlinien verwalten**.  
  
6.  In der **Konfiguration der zentralen Zugriffsrichtlinien** Dialogfeld fügen **Finance Policy**, und klicken Sie dann auf **OK **.  
  
7.  Führen Sie einen Bildlauf nach unten zu **erweiterte Überwachungsrichtlinienkonfiguration**, und erweitern Sie ihn.  
  
8.  Erweitern Sie **Überwachungsrichtlinien**, und wählen Sie **Objektzugriff **.  
  
9. Doppelklicken Sie auf **Staging zentraler Zugriffsrichtlinien Überwachen **. Wählen Sie alle drei Kontrollkästchen, und klicken Sie dann auf **OK **. Dieser Schrittkann das System Überwachungsereignisse im Zusammenhang mit zentralen Zugriffs-Staging-Richtlinien erhalten.  
  
10. Doppelklicken Sie auf **Dateisystemeigenschaften Überwachen **. Wählen Sie alle drei Kontrollkästchen und klicken Sie dann **OK **.  
  
11. Schließen Sie den Gruppenrichtlinienverwaltungs-Editor. Sie haben nun der Gruppenrichtlinie die zentrale Zugriffsrichtlinie hinzugefügt.  
  
Für eine Domäne Domänencontroller Ansprüche oder gerätautorisierungsdaten bereitstellen müssen die Domänencontroller für die Unterstützung der dynamischen Zugriffssteuerung konfiguriert werden.  
  
#### <a name="to-enable-support-for-claims-and-compound-authentication-for-contosocom"></a>So aktivieren Sie die Unterstützung für Ansprüche und Verbundauthentifizierung für die contoso.com  
  
1.  Öffnen Sie die Gruppenrichtlinien-Verwaltungskonsole, klicken Sie auf **contoso.com**, und klicken Sie dann auf **Domänencontroller **.  
  
2.  Mit der rechten Maustaste **Standarddomänencontroller-Richtlinie**, und klicken Sie dann auf **bearbeiten **.  
  
3.  Doppelklicken Sie in der Gruppenrichtlinienverwaltungs-Editor-Fenster auf **Computerkonfiguration**, doppelklicken Sie auf **Richtlinien**, doppelklicken Sie auf **Administrative Vorlagen**, doppelklicken Sie auf **System**, und doppelklicken Sie dann auf **KDC**.  
  
4.  Doppelklicken Sie auf **KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos Armoring **. In der **KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos Armoring** Dialogfeld klicken Sie auf **aktiviert**, und wählen Sie **unterstützte** aus der **Optionen** Dropdownliste. (Sie müssen zum Aktivieren dieser Einstellung Benutzeransprüche in zentralen Zugriffsrichtlinien verwenden.)  
  
5.  Schließen **Gruppenrichtlinienverwaltung**.  
  
6.  Öffnen Sie ein Eingabeaufforderungsfenster, und geben `gpupdate /force`.  
  
## <a name="BKMK_1.4"></a>Bereitstellen der zentralen Zugriffsrichtlinie  
  
||Schritt|Beispiel|  
|-|--------|-----------|  
|3.1|Weisen Sie der Caps zu den entsprechenden freigegebenen Ordnern auf dem Dateiserver.|Weisen Sie die zentrale Zugriffsrichtlinie zu den entsprechenden freigegebenen Ordner auf dem Dateiserver.|  
|3.2|Stellen Sie sicher, dass der Zugriff richtig konfiguriert ist.|Überprüfen Sie den Zugriff für Benutzer aus anderen Ländern und Abteilungen.|  
  
In diesem Schrittweisen Sie die zentrale Zugriffsrichtlinie auf einem Dateiserver. Sie melden Sie sich an einen Dateiserver, der die zentrale Zugriffsrichtlinie empfängt, dass Sie die vorherigen Schrittenerstellt haben und die Richtlinie in einen freigegebenen Ordner zuweisen.  
  
#### <a name="to-assign-a-central-access-policy-to-a-file-server"></a>Ein Dateiserver eine zentrale Zugriffsrichtlinie zuweisen  
  
1.  Schließen Sie in Hyper-V-Manager auf Server "file1". Melden Sie sich bei dem Server mithilfe von "Contoso\Administrator" mit dem Kennwort:**pass@word1**.  
  
2.  Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten und Typ: **Gpupdate/force**. Dadurch wird sichergestellt, dass Ihre gruppenrichtlinienänderungen auf Ihrem Server wirksam.  
  
3.  Sie müssen auch die globalen Ressourceneigenschaften aus Active Directory zu aktualisieren. Öffnen einer Windows PowerShell-Fenster mit erhöhten Rechten, und geben `Update-FSRMClassificationpropertyDefinition`. Drücken Sie die EINGABETASTE, und schließen Sie Windows PowerShell.  
  
    > [!TIP]  
    > Sie können auch die globalen Ressourceneigenschaften durch Anmelden bei der Dateiserver aktualisieren. Um die globalen Ressourceneigenschaften vom Dateiserver zu aktualisieren, führen Sie folgende Schritte  
    >   
    > 1.  Melden Sie sich die Datei Server FILE1 als Contoso\administrator mit dem Kennwort **pass@word1**.  
    > 2.  File Server Resource Manager zu öffnen. File Server Resource Manager zu öffnen, klicken Sie auf **starten**, Typ **Ressourcen-Manager für Dateiserver**, und klicken Sie dann auf **File Server Resource Manager**.  
    > 3.  Klicken Sie im der Resource Manager für Dateiserver, auf **Dateiklassifizierungsverwaltung**, mit der rechten Maustaste **Klassifizierungseigenschaften**, und klicken Sie dann auf **aktualisieren **.  
  
4.  Öffnen Sie Windows Explorer, und klicken Sie im linken Bereich auf Laufwerk "d" mit der rechten Maustaste die **Finanzdokumente** Ordner, und klicken Sie dann auf **Eigenschaften **.  
  
5.  Klicken Sie auf die **Klassifizierung** auf **Land**, und wählen Sie dann **US** in die **Wert** Feld.  
  
6.  Klicken Sie auf **Abteilung**, und wählen Sie dann **Finanzen** in die **Wert** ein, und klicken Sie dann auf **übernehmen **.  
  
    > [!NOTE]  
    > Denken Sie daran, dass die zentrale Zugriffsrichtlinie für die Zieldateien für die Finanzabteilung konfiguriert wurde. Die vorherigen Schrittemarkieren Sie alle Dokumente im Ordner mit den Attributen Land "und" Department.  
  
7.  Klicken Sie auf die **Security** Registerkarte, und klicken Sie dann auf **erweitert**. Klicken Sie auf die **zentrale Richtlinie** Registerkarte.  
  
8.  Klicken Sie auf **ändern**Option **Finance Policy** aus der Dropdownmenü, und klicken Sie dann auf **übernehmen **. Sehen Sie die **Finance Documents Rule** in der Richtlinie aufgelistet. Erweitern Sie das Element, um alle Berechtigungen anzeigen, die Sie festlegen, wenn Sie die Regel in Active Directory erstellt.  
  
9. Klicken Sie auf **OK** zurückkehren zu Windows-Explorer.  
  
Im nächsten Schrittstellen Sie sicher, dass der Zugriff richtig konfiguriert ist.  Benutzerkonten müssen die entsprechenden Abteilung-Attribut festgelegt sein (Legen Sie dies mithilfe von Active Directory Administrative Center). Die einfachste Möglichkeit zum Anzeigen der effektiven Ergebnisse der neuen Richtlinie ist die Verwendung der **effektiver Zugriff** Registerkarte in Windows Explorer. Die **effektiver Zugriff** auf der Registerkarte werden die Zugriffsrechte für ein bestimmtes Benutzerkonto.  
  
#### <a name="to-examine-the-access-for-various-users"></a>Überprüfen Sie den Zugriff für verschiedene Benutzer  
  
1.  Schließen Sie in Hyper-V-Manager auf Server "file1". Melden Sie sich an den Server mit "Contoso\Administrator" an. Navigieren Sie zu D:\ in Windows-Explorer. Mit der rechten Maustaste die **Finanzdokumente** Ordner, und klicken Sie dann auf **Eigenschaften **.  
  
2.  Klicken Sie auf die **Security** auf **erweitert**, und klicken Sie dann auf die **effektiver Zugriff** Registerkarte.  
  
3.  Klicken Sie zum Überprüfen der Berechtigungen für einen Benutzer auf **wählen Sie einen Benutzer**, geben Sie den Namen des Benutzers ein, und klicken Sie dann auf **effektiven Zugriff anzeigen** um die effektiven Zugriffsrechte anzuzeigen. Zum Beispiel:  
  
    -   Myriam Delesalle (MDelesalle) ist in der Finanzabteilung und sollte Lesezugriff für den Ordner haben.  
  
    -   Miles Reid (MReid) ist ein Mitglied der Gruppe "FinanceAdmin" und sollte Zugriff ändern für den Ordner haben.  
  
    -   Esther Valle (EValle) ist nicht in der Finanzabteilung. Sie ist jedoch ein Mitglied der Gruppe "FinanceException" und sollte über Lesezugriff verfügen.  
  
    -   Maira Wenzel (MWenzel) ist nicht in der Finanzabteilung und ist nicht Mitglied der Gruppe "FinanceAdmin" oder "FinanceException". Sie sollten nicht Zugriff auf den Ordner haben.  
  
    Beachten Sie, die die letzte Spalte namens **Zugriff eingeschränkt durch** im Fenster effektiven Zugriff. Diese Spalte verrät Ihnen, welche Gates Berechtigungen der Person begegnen können. In diesem Fall ermöglicht die Freigabe- und NTFS-Berechtigungen allen Benutzern Vollzugriff. Die zentrale Zugriffsrichtlinie schränkt jedoch den Zugriff basierend auf den Regeln, die Sie zuvor konfiguriert.  
  
## <a name="BKMK_1.5"></a>Verwalten Sie ändern und Staging der Richtlinie  
  
||||  
|-|-|-|  
|Anzahl|Schritt|Beispiel|  
|4.1|Konfigurieren von Geräteansprüchen für Clients|Legen Sie die Gruppenrichtlinieneinstellung zum Aktivieren von Geräteansprüchen|  
|4.2|Aktivieren Sie einen Anspruch für Geräte.|Aktivieren Sie den landanspruchstyp für Geräte.|  
|4.3|Hinzufügen einer staging-Richtlinie auf den vorhandenen zentralen Zugriffsrichtlinie, den Sie ändern möchten.|Ändern Sie die Finance Documents Rule zum Hinzufügen einer staging-Richtlinie.|  
|4.4|Die Ergebnisse der staging-Richtlinie anzeigen.|Suchen Sie nach Velles Berechtigungen.|  
  
#### <a name="to-set-up-group-policy-setting-to-enable-claims-for-devices"></a>Informationen zum Einrichten von Gruppenrichtlinien-Einstellung zum Aktivieren der Ansprüche für Geräte  
  
1.  Melden Sie sich bei DC1 Öffnen der Gruppenrichtlinien-Verwaltungskonsole auf **contoso.com**, klicken Sie auf **Default Domain Policy**mit der rechten Maustaste auf, und wählen Sie **bearbeiten **.  
  
2.  Wechseln Sie in der Gruppenrichtlinienverwaltungs-Editor-Fenster zu **Computerkonfiguration**, **Richtlinien**, **Administrative Vorlagen**, **System**, **Kerberos **.  
  
3.  Wählen Sie **Kerberos-Clientunterstützung für Ansprüche, Verbundauthentifizierung und Kerberos Armoring**, und klicken Sie auf **aktivieren **.  
  
#### <a name="to-enable-a-claim-for-devices"></a>So aktivieren Sie einen Anspruch für Geräte  
  
1.  Öffnen Sie Server "DC1" im Hyper-V-Manager, und melden sich als "Contoso\Administrator" mit dem Kennwort **pass@word1**.  
  
2.  Von der **Tools** Menü Öffnen von Active Directory Administrative Center.  
  
3.  Klicken Sie auf **Strukturansicht**, erweitern Sie **dynamische Zugriffssteuerung**, doppelklicken Sie auf **Anspruchstypen**, und doppelklicken Sie auf die **Land** geltend machen.  
  
4.  In **Ansprüche von diesem Typ können für die folgenden Klassen ausgegeben werden**, wählen die **Computer** Kontrollkästchen. Klicken Sie auf **OK**.   
    Beide **Benutzer** und **Computer** Kontrollkästchen sollten nun aktiviert sein. Der Anspruch Land kann jetzt mit Geräten zusätzlich zu Benutzern verwendet werden.  
  
Im nächste Schrittwird eine staging-Richtlinienregel erstellen. Staging-Richtlinien können verwendet werden, um die Auswirkungen eines neuen Richtlinieneintrags überwachen, bevor Sie ihn aktivieren. In den folgenden Schrittaus Sie erstellen einen staging-Richtlinieneintrag und überwachen die Auswirkung auf Ihre freigegebenen Ordner.  
  
#### <a name="to-create-a-staging-policy-rule-and-add-it-to-the-central-access-policy"></a>Erstellen eine staging-Richtlinienregel und die zentrale Zugriffsrichtlinie hinzufügen  
  
1.  Öffnen Sie Server "DC1" im Hyper-V-Manager, und melden sich als "Contoso\Administrator" mit dem Kennwort **pass@word1**.  
  
2.  Active Directory-Verwaltungscenter zu öffnen.  
  
3.  Klicken Sie auf **Strukturansicht**, erweitern Sie **dynamische Zugriffssteuerung**, und wählen Sie **zentrale Zugriffsregeln **.  
  
4.  Mit der rechten Maustaste **Finance Documents Rule**, und klicken Sie dann auf **Eigenschaften **.  
  
5.  In der **vorgesehene Berechtigungen** Abschnittder **staging-Konfiguration aktivieren Berechtigung** Kontrollkästchen, klicken Sie auf **bearbeiten**, und klicken Sie dann auf **hinzufügen **. In der **Berechtigungseintrag für vorgesehene Berechtigungen** Fenster, klicken Sie auf die **Prinzipal auswählen** verknüpfen, geben Sie **authentifizierte Benutzer**, und klicken Sie dann auf **OK **.  
  
6.  Klicken Sie auf die **fügen Sie eine Bedingung** verknüpfen, und fügen Sie die folgende Bedingung hinzu:   
     [**User**] [**Land**] [**Any of**] [**Ressource**] [**Land**].  
  
7.  Klicken Sie auf **fügen Sie eine Bedingung** erneut, und fügen Sie die folgende Bedingung hinzu:  
    [**And**]   
     [**Gerät**] [**Land**] [**Any of**] [**Ressource**] [**Land**]  
  
8.  Klicken Sie auf **fügen Sie eine Bedingung** erneut, und fügen Sie die folgende Bedingung hinzu.  
    [Und]   
     [**User**] [**Group**] [**Mitglied einer**] [**Wert**] \ (**FinanceException**)  
  
9. Klicken Sie zum Festlegen der FinanceException Gruppe, klicken Sie auf **Elemente hinzufügen** und in der **Benutzer, Computer, Dienstkonto oder Gruppe** geben **FinanceException **.  
  
10. Klicken Sie auf **Berechtigungen**Option **Vollzugriff**, und klicken Sie auf **OK **.  
  
11. Wählen Sie in den erweiterten Sicherheitseinstellungen für vorgesehene Berechtigungen Fenster, **FinanceException**, und klicken Sie auf **entfernen **.  
  
12. Klicken Sie auf **OK** zweimal auf Fertig stellen.  
  
![Lösungshandbücher](media/Deploy-a-Central-Access-Policy--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
Set-ADCentralAccessRule  
-Identity: "CN=FinanceDocumentsRule,CN=CentralAccessRules,CN=ClaimsConfiguration,CN=Configuration,DC=Contoso.com"  
-ProposedAcl: "O:SYG:SYD:AR(A;;FA;;;BA)(A;;FA;;;SY)(A;;0x1301bf;;;S-1-21=1426421603-1057776020-1604)"  
-Server: "WIN-2R92NN8VKFP.Contoso.com"  
  
```  
  
> [!NOTE]  
> Im obigen Cmdlet-Beispiel zeigt den Server-Wert den Server in der Testumgebung. Windows PowerShell History Viewer können Sie um Windows PowerShell-Cmdlets nach jeder Prozedur zu durchsuchen, die Sie im Active Directory-Verwaltungscenter ausführen. Weitere Informationen finden Sie unter [Windows PowerShell History Viewer](https://technet.microsoft.com/library/hh831702)  
  
In diesem Satz vorgesehener Berechtigungen sind Mitglieder der Gruppe "FinanceException" besitzen vollständigen Zugriff auf Dateien von ihrem eigenen Land beim Zugriff über ein Gerät aus demselben Land wie das Dokument. Überwachungseinträge stehen im Dateiserver-Sicherheitsprotokoll aufgezeichnet, wenn ein Mitarbeiter der Finanzabteilung versucht, auf Dateien zugreifen. Sicherheitseinstellungen werden jedoch nicht erzwungen, bis die Richtlinie vom Staging höher gestuft wird.  
  
In den nächsten Verfahren fort überprüfen Sie die Ergebnisse der staging-Richtlinie. Sie Zugriff auf den freigegebenen Ordner mit einem Benutzernamen, der über Berechtigungen auf Grundlage der aktuellen Regel verfügt. Esther Valle (EValle) ist ein Mitglied von "financeexception", und er derzeit über die Leseberechtigung. Gemäß unserer staging-Richtlinie sollte EValle keinerlei Rechte besitzen.  
  
#### <a name="to-verify-the-results-of-the-staging-policy"></a>So überprüfen Sie die Ergebnisse der staging-Richtlinie  
  
1.  Mit der Datei Server FILE1 im Hyper-V-Manager, und melden in als "Contoso\administrator" mit dem Kennwort verbinden **pass@word1**.  
  
2.  Öffnen Sie ein Eingabeaufforderungsfenster, und geben **Gpupdate/force **. Dadurch wird sichergestellt, dass Ihre gruppenrichtlinienänderungen auf Ihrem Server wirksam werden.  
  
3.  Schließen Sie in Hyper-V-Manager auf Server "client1". Melden Sie sich der Benutzer, der aktuell angemeldet ist. Starten Sie den virtuellen Computer "client1" neu. Klicken Sie dann melden Sie sich bei dem Computer mit Contoso\EValle pass@word1.  
  
4.  Doppelklicken Sie auf die Desktopverknüpfung zu \\\FILE1\Finance Dokumente. EValle sollte weiterhin auf die Dateien zugreifen. Wechseln Sie zu "file1".  
  
5.  Öffnen **Ereignisanzeige** über die Verknüpfung auf dem Desktop. Erweitern Sie **Windows-Protokolle**, und wählen Sie dann **Security **. Öffnen Sie die Einträge mit **Event ID 4818**unter der **Staging zentraler Zugriffsrichtlinien** Aufgabenkategorie. Sie sehen, dass EValle der Zugriff gewährt wurde. jedoch entsprechend der staging-Richtlinie des Benutzers wird der Zugriff verweigert wurde.  
  
## <a name="next-steps"></a>Nächste Schritte  
Wenn Sie ein Verwaltungssystem zentralen Server z.B. System Center Operations Manager verfügen, können Sie auch die ereignisüberwachung für Ereignisse konfigurieren. Dadurch können Administratoren die Auswirkungen der zentralen Zugriffsrichtlinien zu überwachen, bevor Sie erzwungen werden.  
  

