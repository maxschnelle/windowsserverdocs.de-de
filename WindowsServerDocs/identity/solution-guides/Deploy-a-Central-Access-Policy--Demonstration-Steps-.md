---
ms.assetid: 8738c03d-6ae8-49a7-8b0c-bef7eab81057
title: Bereitstellen einer zentralen Zugriffsrichtlinie (Demonstrationsschritte)
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 16973b32407985ffc3f66bf5ac579384a756b5d0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817141"
---
# <a name="deploy-a-central-access-policy-demonstration-steps"></a>Bereitstellen einer zentralen Zugriffsrichtlinie (Demonstrationsschritte)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Szenario werden die Finanzabteilungs-Sicherheitsvorgänge zusammen mit der zentralen Informationssicherheit verwendet, um die Notwendigkeit für eine zentrale Zugriffsrichtlinie anzugeben, sodass sie auf Dateiservern archivierte Finanzinformationen schützen kann. Die archivierten Finanzinformationen jedes Lands kann durch alle Finanzmitarbeiter aus demselben Land mit Lesezugriff aufgerufen werden. Eine zentrale Finanzadministratorgruppe kann auf die Finanzinformationen aus allen Ländern zugreifen.  
  
Das Bereitstellen einer zentralen Zugriffsrichtlinie beinhaltet die folgenden Phasen:  
  
|Phase|Beschreibung  
|---------|---------------  
|[Planen: Bestimmen der richtliniennotwendigkeit und der erforderlichen Konfiguration für die Bereitstellung](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md#BKMK_1.2)|Bestimmen der Richtliniennotwendigkeit und der für die Bereitstellung erforderlichen Konfiguration. 
|[Implementieren: Konfigurieren der Komponenten und Richtlinie](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md#BKMK_1.3)|Konfigurieren der Komponenten und Richtlinie.  
|[Bereitstellen der zentralen Zugriffsrichtlinie](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md#BKMK_1.4)|Stellen Sie die Richtlinie bereit.  
|[Verwalten: Ändern und Staging der Richtlinie](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md#BKMK_1.5)|Richtlinienänderungen und Staging. 
  
## <a name="BKMK_1.1"></a>Einrichten einer testumgebung  
Bevor Sie beginnen, müssen Sie ein Labor zum Testen dieses Szenarios einrichten. Die Schritte zum Einrichten der testumgebung werden ausführlich im [Anhang B: Einrichten der Testumgebung](Appendix-B--Setting-Up-the-Test-Environment.md).  
  
## <a name="BKMK_1.2"></a>Plan: Bestimmen der Richtliniennotwendigkeit und der für die Bereitstellung erforderlichen Konfiguration  
In diesem Abschnitt werden eine Reihe allgemeiner Schritte erläutert, die Sie in der Planungsphase Ihrer Bereitstellung unterstützen.  
  
||Schritt|Beispiel|  
|-|--------|-----------|  
|1.1|Unternehmen bestimmt, dass eine zentrale Zugriffsrichtlinie erforderlich ist|Damit auf Dateiservern gespeicherte Finanzinformationen zu schützen, werden die Finanzabteilungs-Sicherheitsvorgänge mit der zentralen Informationssicherheit verwendet, um die Notwendigkeit für eine zentrale Zugriffsrichtlinie zu bestimmen.|  
|1.2|Ausdrücken der Zugriffsrichtlinie|Finanzdokumente sollten nur von Mitgliedern der Finanzabteilung gelesen werden. Mitglieder der Finanzabteilung sollten nur auf Dokumente in ihrem eigenen Land zugreifen. Nur Finanzadministratoren sollten über Schreibzugriff verfügen. Für Mitglieder der Gruppe "FinanceException" wird eine Ausnahme zugelassen. Diese Gruppe verfügt über Lesezugriff.|  
|1.3|Ausdrücken der Zugriffsrichtlinie in Windows Server 2012-Konstrukten|Ziel:<br /><br />-"Resource.Department" enthält "Finance"<br /><br />Zugriffsregeln:<br /><br />-Gelesen User.Country=Resource.Country und User.department zulassen = "Resource.Department"<br />– Ermöglichen Sie vollständige Kontrolle User.MemberOf(FinanceAdmin)<br /><br />Ausnahme:<br /><br />Allow read memberOf(FinanceException)|  
|1.4|Bestimmen der für die Richtlinie erforderlichen Dateieigenschaften|Dateien kennzeichnen mit:<br /><br />-Abteilung<br />/ Land|  
|1.5|Bestimmen der für die Richtlinie erforderlichen Anspruchstypen und -gruppen|Anspruchstypen:<br /><br />/ Land<br />-Abteilung<br /><br />Benutzergruppen:<br /><br />-FinanceAdmin<br />-"Financeexception"|  
|1.6|Bestimmen der Server, auf denen diese Richtlinie angewendet werden soll|Wenden Sie die Richtlinie auf alle Finanzdateiserver an.|  
  
## <a name="BKMK_1.3"></a>Implementieren: Konfigurieren der Komponenten und Richtlinie  
In diesem Abschnitt ist ein Beispiel vorhanden, in dem eine zentrale Zugriffsrichtlinie für Finanzdokumente bereitgestellt wird.  
  
|Nein|Schritt|Beispiel|  
|------|--------|-----------|  
|2.1|Erstellen von Anspruchstypen|Erstellen Sie die folgenden Anspruchstypen:<br /><br />-Abteilung<br />/ Land|  
|2.2|Erstellen von Ressourceneigenschaften|Erstellen und aktivieren Sie die folgenden Ressourceneigenschaften:<br /><br />-Abteilung<br />/ Land|  
|2.3|Konfigurieren einer zentralen Zugriffsregel|Erstellen Sie eine Regel für Finanzdokumente, die die im vorherigen Abschnitt bestimmte Richtlinie enthält.|  
|2.4|Konfigurieren einer zentralen Zugriffsrichtlinie|Erstellen Sie eine zentrale Zugriffsrichtlinie mit dem Namen „Finance Policy“, und fügen Sie dieser zentralen Zugriffsrichtlinie die Regel „Finance Documents“ hinzu.|  
|2.5|Vorgeben einer zentralen Zugriffsrichtlinie für die Dateiserver|Veröffentlichen der zentrale Zugriffsrichtlinie „Finance Policy“ auf den Dateiservern.|  
|2.6|Ermöglichen der KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos Armoring.|Ermöglichen der KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos Armoring für „contoso.com“.|  
  
Im folgenden Verfahren erstellen Sie zwei Anspruchstypen: „Country“ und „Department“.  
  
#### <a name="to-create-claim-types"></a>So erstellen Sie Anspruchstypen:  
  
1.  Öffnen Sie auf Server "DC1" im Hyper-V-Manager, und melden als "Contoso\Administrator" mit dem Kennwort **pass@word1**.  
  
2.  Öffnen Sie das Active Directory-Verwaltungscenter.  
  
3.  Klicken Sie auf das Strukturansichtssymbol****, erweitern Sie **Dynamische Zugriffssteuerung**, und wählen Sie dann **Anspruchstypen** aus.  
  
    Klicken Sie mit der rechten Maustaste auf **Anspruchstypen**, klicken Sie auf **Neu** und dann auf **Anspruchstyp**.  
  
    > [!TIP]  
    > Sie können ein Fenster vom Typ **Anspruchstyp erstellen** auch im Bereich **Aufgaben** öffnen. Klicken Sie im Bereich **Aufgaben** auf **Neu**, und klicken Sie dann auf **Anspruchstyp**.  
  
4.  Führen Sie in der Liste **Quellattribut** einen Bildlauf durch die Liste der Attribute durch, und klicken Sie auf **department**. Dadurch sollte das Feld **Anzeigename** mit **department** aufgefüllt werden. Klicken Sie auf **OK**.  
  
5.  Klicken Sie im Bereich **Aufgaben** auf **Neu**, und klicken Sie dann auf **Anspruchstyp**.  
  
6.  Führen Sie in der Liste **Quellattribut** einen Bildlauf durch die Liste der Attribute durch, und klicken Sie dann auf das Attribut **c** (Ländername). Geben Sie in das Feld **Anzeigename****country** ein.  
  
7.  Wählen Sie im Abschnitt **Vorgeschlagene Werte** die Option **Folgende Werte werden vorgeschlagen** aus, und klicken Sie dann auf **Hinzufügen**.  
  
8.  Geben Sie in die Felder **Wert** und **Anzeigename****US** ein, und klicken Sie dann auf **OK**.  
  
9. Wiederholen Sie den obigen Schritt. Geben Sie im Dialogfeld **Vorgeschlagenen Wert hinzufügen****JP** in die Felder **Wert** und **Anzeigename** ein, und klicken Sie dann auf **OK**.  
  
![Lösungshandbücher](media/Deploy-a-Central-Access-Policy--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
 
    New-ADClaimType country -SourceAttribute c -SuggestedValues:@((New-Object Microsoft.ActiveDirectory.Management.ADSuggestedValueEntry("US","US","")), (New-Object Microsoft.ActiveDirectory.Management.ADSuggestedValueEntry("JP","JP","")))  
    New-ADClaimType department -SourceAttribute department  
      
 
  
> [!TIP]  
> Sie können die Windows PowerShell-Verlaufsanzeige im Active Directory-Verwaltungscenter verwenden, um Windows PowerShell-Cmdlets nach jeder Prozedur zu durchsuchen, die Sie im Active Directory-Verwaltungscenter ausführen. Weitere Informationen finden Sie unter [Windows PowerShell History Viewer](https://technet.microsoft.com/library/hh831702)  
  
Im nächsten Schritt werden Ressourceneigenschaften erstellt. Im folgenden Verfahren erstellen Sie eine Ressourceneigenschaft, die der Liste mit den globalen Ressourceneigenschaften auf dem Domänencontroller automatisch hinzugefügt wird, sodass sie für den Dateiserver verfügbar ist.  
  
#### <a name="to-create-and-enable-pre-created-resource-properties"></a>So erstellen und aktivieren Sie vorab erstellte Ressourceneigenschaften  
  
1.  Klicken Sie im linken Bereich des Active Directory-Verwaltungscenters auf **Strukturansicht**. Erweitern Sie **Dynamische Zugriffssteuerung**, und wählen Sie dann **Ressourceneigenschaften** aus.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Ressourceneigenschaften**, klicken Sie auf **Neu** und dann auf **Referenzressourceneigenschaft**.  
  
    > [!TIP]  
    > Sie können auch eine Ressourceneigenschaft aus dem Bereich **Aufgaben** auswählen. Klicken Sie auf **Neu** und dann auf **Referenzressourceneigenschaft**.  
  
3.  Klicken Sie in **Wählen Sie den Anspruchstyp aus, dessen vorgeschlagene Werte verwendet werden sollen** auf **country**.  
  
4.  Geben Sie **country** in das Feld **Anzeigename** ein, und klicken Sie dann auf **OK**.  
  
5.  Doppelklicken Sie auf die Liste **Ressourceneigenschaften**, führen Sie einen Bildlauf zur Ressourceneigenschaft **Department** durch. Klicken Sie mit der rechten Maustaste, und klicken Sie dann auf **Aktivieren**. Dadurch wird die integrierte Ressourceneigenschaft **Department** aktiviert.  
  
6.  In der Liste **Ressourceneigenschaften** im Navigationsbereich des Active Directory-Verwaltungscenters stehen Ihnen nun zwei aktivierte Ressourceneigenschaften zur Verfügung:  
  
    -   Land  
  
    -   Department  
  
![Lösungshandbücher](media/Deploy-a-Central-Access-Policy--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
New-ADResourceProperty Country -IsSecured $true -ResourcePropertyValueType MS-DS-MultivaluedChoice -SharesValuesWith country  
Set-ADResourceProperty Department_MS -Enabled $true  
Add-ADResourcePropertyListMember "Global Resource Property List" -Members Country  
Add-ADResourcePropertyListMember "Global Resource Property List" -Members Department_MS  
  
```  
  
Im nächsten Schritt erstellen Sie die zentralen Zugriffsregeln, in denen definiert wird, wer auf Ressourcen zugreifen kann. In diesem Szenario lauten die Geschäftsregeln wie folgt:  
  
-   Finanzdokumente können nur von Mitgliedern der Finanzabteilung gelesen werden.  
  
-   Mitglieder der Finanzabteilung können nur auf Dokumente in ihrem eigenen Land zugreifen.  
  
-   Nur Finanzadministratoren können über Schreibzugriff verfügen.  
  
-   Wir ermöglichen eine Ausnahme für die Mitglieder der Gruppe „FinanceException“. Diese Gruppe verfügt über Lesezugriff.  
  
-   Sowohl der Administrator als auch der Dokumentbesitzer haben weiterhin Vollzugriff.  
  
Oder zum Ausdrücken der Regeln mit Windows Server 2012-Konstrukten:  
  
Ziel: „Resource.Department“ enthält „Finance“  
  
Zugriffsregeln:  
  
-   Allow Read User.Country=Resource.Country AND User.department = Resource.Department  
  
-   Allow Full control User.MemberOf(FinanceAdmin)  
  
-   Allow Read User.MemberOf(FinanceException)  
  
#### <a name="to-create-a-central-access-rule"></a>So erstellen Sie eine zentrale Zugriffsregel  
  
1.  Klicken Sie im linken Bereich des Active Directory-Verwaltungscenters auf **Strukturansicht**, wählen Sie **Dynamische Zugriffssteuerung** aus, und klicken Sie dann auf **Zentrale Zugriffsregeln**.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Zentrale Zugriffsregeln**, klicken Sie auf **Neu** und dann auf **Zentrale Zugriffsregel**.  
  
3.  Geben Sie **Finance Documents Rule** in das Feld **Name** ein.  
  
4.  Klicken Sie im Abschnitt **Zielressourcen** auf **Bearbeiten**, und klicken Sie im Dialogfeld **Zentrale Zugriffsregel** auf **Bedingung hinzufügen**. Fügen Sie die folgende Bedingung hinzu:   
    [**Resource**] [**Department**] [**Equals**] [**Value**] [**Finance**], und klicken Sie dann auf **OK**.  
  
5.  Wählen Sie im Abschnitt **Berechtigungen** die Option **Folgende Berechtigungen als aktuelle Berechtigungen verwenden** aus, klicken Sie auf **Bearbeiten**, und klicken Sie im Dialogfeld **Erweiterte Sicherheitseinstellungen für Berechtigungen** auf **Hinzufügen**.  
  
    > [!NOTE]  
    > Mit der Option **Folgende Berechtigungen als vorgesehene Berechtigungen verwenden** können Sie die Richtlinie in Staging erstellen. Weitere Informationen darüber, wie Sie dies umsetzen können, finden Sie im Abschnitt „Warten: Ändern und Staging der Richtlinie“ in diesem Thema.  
  
6.  Klicken Sie im Dialogfeld **Berechtigungseintrag für Berechtigungen**, klicken Sie auf **Prinzipal auswählen**, geben Sie **Authentifizierte Benutzer** ein, und klicken Sie dann auf **OK**.  
  
7.  Klicken Sie im Dialogfeld **Berechtigungseintrag** auf **Bedingung hinzufügen**, und fügen Sie die folgenden Bedingungen hinzu:   
    [**Benutzer**] [**Land**] [**eines**] [**Ressource**] [**Land**]   
     Klicken Sie auf **Bedingung hinzufügen**.   
     [**And**]   
    Klicken Sie auf [**Benutzer**] [**Abteilung**] [**eines**] [**Ressource**] [**Abteilung**]. Legen Sie die **Berechtigungen** auf **Lesen** fest.  
  
8.  Klicken Sie auf **OK** und dann auf **Hinzufügen**. Klicken Sie auf **Prinzipal auswählen**, geben Sie **FinanceAdmin** ein, und klicken Sie dann auf **OK**.  
  
9. Wählen Sie die Berechtigungen **Ändern, Lesen und Ausführen, Lesen, Schreiben** aus, und klicken Sie dann auf **OK**.  
  
10. Klicken Sie auf **Hinzufügen**, klicken Sie auf **Prinzipal auswählen**, geben Sie **FinanceException** ein, und klicken Sie dann auf **OK**. Wählen Sie aus, dass die Berechtigungen **Lesen** und **Lesen und Ausführen** lauten sollen.  
  
11. Klicken Sie dreimal auf **OK** zum Abschließen des Vorgangs, und kehren Sie zum Active Directory-Verwaltungscenter zurück.  
  
    ![Lösungshandbücher](media/Deploy-a-Central-Access-Policy--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
    Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
 
    $countryClaimType = Get-ADClaimType country  
    $departmentClaimType = Get-ADClaimType department  
    $countryResourceProperty = Get-ADResourceProperty Country  
    $departmentResourceProperty = Get-ADResourceProperty Abteilung  
    $currentAcl = "O:SYG:SYD:AR(A;; FA;; O W) (A; FA;; BA); (A; 0 x1200a9;; S-1-5-21-1787166779-1215870801-2157059049-1113) (A; 0 x1301bf;; S-1-5-21-1787166779-1215870801-2157059049-1112) (A; FA;; SY) (XA; 0 x1200a9;; AU ;((@USER. " + $countryClaimType.Name + " Any_of @RESOURCE." + $countryResourceProperty.Name + ") && (@USER." + $departmentClaimType.Name + " Any_of @RESOURCE." + $departmentResourceProperty.Name + ")))"  
    $resourceCondition = "(@RESOURCE." + $departmentResourceProperty.Name + "enthält {`"Finance`"}) "  
    New-ADCentralAccessRule "Finance Documents Rule" -CurrentAcl $currentAcl -ResourceCondition $resourceCondition  

  
> [!IMPORTANT]  
> Im obigen Cmdlet-Beispiel werden die Sicherheits-IDs für die Gruppe „FinanceAdmin“ und Benutzer zur Erstellungszeit bestimmt, und sie unterscheiden sich in Ihrem Beispiel. Beispielsweise muss der angegebene Sicherheits-ID-Wert (S-1-5-21-1787166779-1215870801-2157059049-1113) für „FinanceAdmins“ durch die tatsächliche Sicherheits-ID für die Gruppe „FinanceAdmin“ ersetzt werden, die Sie zum Erstellen in Ihrer Bereitstellung bräuchten. Sie können Windows PowerShell verwenden, zum Suchen des SID-Wertes, der diese Gruppe, diesen Wert einer Variablen zuweisen und verwenden Sie dann die Variable hier. Weitere Informationen finden Sie unter [Windows PowerShell-Tipp: Arbeiten mit SIDs](https://go.microsoft.com/fwlink/?LinkId=253545).  
  
Sie sollten nun über eine zentrale Zugriffsregel verfügen, die Personen erlaubt, auf Dokumente aus demselben Land und derselben Abteilung zuzugreifen. Die Regel ermöglicht der Gruppe „FinanceAdmin“ die Bearbeitung der Dokumente, und sie ermöglicht der Gruppe „FinanceException“, die Dokumente zu lesen. Diese Regel zielt nur auf Dokumente ab, die als „Finance“ klassifiziert wurden.  
  
#### <a name="to-add-a-central-access-rule-to-a-central-access-policy"></a>So fügen Sie eine zentrale Zugriffsregel zu einer zentralen Zugriffsrichtlinie hinzu  
  
1.  Klicken Sie im linken Bereich des Active Directory-Verwaltungscenters auf **Dynamische Zugriffssteuerung**, und klicken Sie dann auf **Zentrale Zugriffsrichtlinien**.  
  
2.  Klicken Sie im Bereich **Aufgaben** auf **Neu**, und klicken Sie dann auf **Zentrale Zugriffsrichtlinie**.  
  
3.  Geben Sie unter **Zentrale Zugriffsrichtlinie erstellen****Finance Policy** in das Feld **Name** ein.  
  
4.  Klicken Sie in **Zentrale Zugriffsregeln des Mitglieds** auf **Hinzufügen**.  
  
5.  Doppelklicken Sie auf **Finance Documents Rule**, um sie zur Liste **Folgende zentrale Zugriffsregeln hinzufügen** hinzuzufügen, und klicken Sie dann auf **OK**.  
  
6.  Klicken Sie auf **OK**, um den Vorgang abzuschließen. Sie sollten nun über eine zentrale Zugriffsrichtlinie namens „Finance Policy“ verfügen.  
  
    ![Lösungshandbücher](media/Deploy-a-Central-Access-Policy--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
    Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
    ```  
    New-ADCentralAccessPolicy "Finance Policy" Add-ADCentralAccessPolicyMember   
    -Identity "Finance Policy"   
    -Member "Finance Documents Rule"  
  
    ```  
  
#### <a name="to-apply-the-central-access-policy-across-file-servers-by-using-group-policy"></a>So wenden Sie die zentrale Zugriffsrichtlinie dateiserverübergreifend mithilfe der Gruppenrichtlinie an  
  
1.  Geben Sie **Gruppenrichtlinienverwaltung** im Feld **Suchen** auf dem Startbildschirm an****. Doppelklicken Sie auf **Gruppenrichtlinienverwaltung**.  
  
    > [!TIP]  
    > Wenn die Einstellung **Verwaltungstools anzeigen** deaktiviert ist, werden der Ordner **Verwaltung** und sein Inhalt nicht in den Ergebnissen für **Einstellungen** angezeigt.  
  
    > [!TIP]  
    > In Ihrer Produktionsumgebung sollten Sie eine Dateiserver-Organisationseinheit erstellen und dieser Organisationseinheit alle Ihre Dateiserver hinzufügen, auf die Sie diese Richtlinie anwenden möchten. Sie können eine Gruppenrichtlinie erstellen und dieser Richtlinie diese Organisationseinheit hinzufügen.  
  
2.  In diesem Schritt bearbeiten Sie das im Abschnitt für das [Erstellen des Domänencontrollers](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_Build) in der Testumgebung erstellte Gruppenrichtlinienobjekt, um die von Ihnen erstellte zentrale Zugriffsrichtlinie einzubeziehen. Navigieren Sie im Gruppenrichtlinienverwaltungs-Editor zur Organisationseinheit in der Domäne (in diesem Beispiel „contoso.com“), und wählen Sie sie aus: **Gruppenrichtlinienverwaltung**, **Gesamtstruktur: contoso.com**, **Domänen**, **contoso.com**, **Contoso**, **FileServerOU**.  
  
3.  Klicken Sie mit der rechten Maustaste auf **FlexibleAccessGPO**, und klicken Sie dann auf **Bearbeiten**.  
  
4.  Wechseln Sie im Gruppenrichtlinienverwaltungs-Editor zu **Computerkonfiguration**, erweitern Sie **Richtlinien**, erweitern Sie **Windows-Einstellungen**, und klicken Sie auf **Sicherheitseinstellungen**.  
  
5.  Erweitern Sie **Dateisystem**, klicken Sie mit der rechten Maustaste auf **Zentrale Zugriffsrichtlinie**, und klicken Sie dann auf **Zentrale Zugriffsrichtlinien verwalten**.  
  
6.  Fügen Sie **Finance Policy**  im Dialogfeld **Konfiguration der zentralen Zugriffsrichtlinien** hinzu, und klicken Sie dann auf **OK**.  
  
7.  Führen Sie einen Bildlauf zu **Erweiterte Überwachungsrichtlinienkonfiguration** durch, und erweitern Sie den Knoten.  
  
8.  Erweitern Sie **Überwachungsrichtlinien**, und wählen Sie **Objektzugriff** aus.  
  
9. Doppelklicken Sie auf **Staging zentraler Zugriffsrichtlinien überwachen**. Aktivieren Sie alle drei Kontrollkästchen, und klicken Sie dann auf **OK**. Dadurch kann das System Überwachungsereignisse empfangen, die mit zentralen Zugriffs-Staging-Richtlinien in Zusammenhang stehen.  
  
10. Doppelklicken Sie auf **Dateisystemeigenschaften überwachen**. Aktivieren Sie alle drei Kontrollkästchen, und klicken Sie dann auf **OK**.  
  
11. Schließen Sie den Gruppenrichtlinienverwaltungs-Editor. Sie haben nun der Gruppenrichtlinie die zentrale Zugriffsrichtlinie hinzugefügt.  
  
Für einen Domänencontroller der Ansprüche oder gerätautorisierungsdaten bereitstellen müssen die Domänencontroller so konfiguriert werden, dass die dynamische Zugriffssteuerung unterstützen.  
  
#### <a name="to-enable-support-for-claims-and-compound-authentication-for-contosocom"></a>So aktivieren Sie die Unterstützung für Ansprüche und die Verbundauthentifizierung für „contoso.com“  
  
1.  Öffnen Sie die Gruppenrichtlinien-Verwaltungskonsole, klicken Sie auf **contoso.com** und auf **Domänencontroller**.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Standard-Domänencontrollerrichtlinie**, und klicken Sie dann auf **Bearbeiten**.  
  
3.  Doppelklicken Sie im Fenster „Gruppenrichtlinienverwaltungs-Editor“ auf **Computerkonfiguration**, doppelklicken Sie auf **Richtlinien**, doppelklicken Sie auf **Administrative Vorlagen**, doppelklicken Sie auf **System**, und doppelklicken Sie dann auf **KDC**.  
  
4.  Doppelklicken Sie auf **KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos Armoring**. Klicken Sie im Dialogfeld **KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos Armoring** auf **Aktiviert**, und wählen Sie **Unterstützt** aus der Dropdownliste **Optionen** aus. (Sie müssen diese Einstellung aktivieren, um Benutzeransprüche in zentralen Zugriffsrichtlinien verwenden zu können.)  
  
5.  Schließen Sie **Gruppenrichtlinienverwaltung**.  
  
6.  Öffnen Sie eine Eingabeaufforderung, und geben Sie `gpupdate /force` ein.  
  
## <a name="BKMK_1.4"></a>Bereitstellen der zentralen Zugriffsrichtlinie  
  
||Schritt|Beispiel|  
|-|--------|-----------|  
|3.1|Weisen Sie die zentrale Zugriffsrichtlinie zu den entsprechenden freigegebenen Ordnern auf dem Dateiserver zu.|Weisen Sie die zentrale Zugriffsrichtlinie zu dem entsprechenden freigegebenem Ordner auf dem Dateiserver zu.|  
|3.2|Stellen Sie sicher, dass der Zugriff ordnungsgemäß konfiguriert wurde.|Überprüfen Sie den Zugriff für Benutzer aus anderen Ländern und Abteilungen.|  
  
In diesem Schritt weisen Sie die zentrale Zugriffsrichtlinie zu einem Dateiserver zu. Sie melden sich auf einem Dateiserver an, der die von Ihnen in den vorherigen Schritten erstellte zentrale Zugriffsrichtlinie empfängt, und Sie weisen einem freigegebenen Ordner die Richtlinie zu.  
  
#### <a name="to-assign-a-central-access-policy-to-a-file-server"></a>So weisen Sie einem Dateiserver eine zentrale Zugriffsrichtlinie zu  
  
1.  Stellen Sie im Hyper-V-Manager eine Verbindung mit dem Server „FILE1“ her. Melden Sie sich bei dem Server mithilfe von "Contoso\Administrator" mit dem Kennwort: **pass@word1**.  
  
2.  Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, und geben Sie Folgendes ein: **gpupdate /force**. Dadurch wird sichergestellt, dass Ihre Gruppenrichtlinienänderungen auf Ihrem Server wirksam werden.  
  
3.  Sie müssen auch die globalen Ressourceneigenschaften in Active Directory aktualisieren. Öffnen Sie ein Windows PowerShell-Fenster mit erhöhten Rechten, und geben Sie `Update-FSRMClassificationpropertyDefinition` ein. Drücken Sie die EINGABETASTE, und schließend Sie anschließend die Windows PowerShell.  
  
    > [!TIP]  
    > Sie können die globalen Ressourceneigenschaften auch aktualisieren, indem Sie sich am Dateiserver anmelden. So aktualisieren Sie die globalen Ressourceneigenschaften vom Dateiserver  
    >   
    > 1.  Melden Sie sich die Dateiserver FILE1 als %% amp;quot;Contoso\Administrator%%amp;quot; mit dem Kennwort **pass@word1**.  
    > 2.  Öffnen Sie den Ressourcen-Manager für Dateiserver. Klicken Sie zum Öffnen des Ressourcen-Managers für Dateiserver auf **Start**, geben Sie **Ressourcen-Manager für Dateiserver**ein, und klicken Sie dann auf **Ressourcen-Manager für Dateiserver**.  
    > 3.  Klicken Sie im Ressourcen-Manager für Dateiserver auf **Dateiklassifizierungsverwaltung**, klicken Sie mit der rechten Maustaste auf **Klassifizierungseigenschaften**, und klicken Sie dann auf **Aktualisieren**.  
  
4.  Öffnen Sie den Windows-Explorer, und klicken Sie im linken Bereich auf das Laufwerk „D“. Klicken Sie mit der rechten Maustaste auf den Ordner **Finance Documents**, und klicken Sie auf **Eigenschaften**.  
  
5.  Klicken Sie auf die Registerkarte **Klassifizierung**, klicken Sie auf **Country**, und wählen Sie dann **US** im Feld **Wert** aus.  
  
6.  Klicken Sie auf **Department**, wählen Sie dann **Finance** im Feld **Wert** aus, und klicken Sie auf **Übernehmen**.  
  
    > [!NOTE]  
    > Beachten Sie, dass die zentrale Zugriffsrichtlinie konfiguriert wurde, um auf Dateien für die Finanzabteilung abzuzielen. In den vorherigen Schritten wurden alle Dokumente im Ordner mit den Attributen „Country“ und „Department“ markiert.  
  
7.  Klicken Sie auf die Registerkarte **Sicherheit** und dann auf **Erweitert**. Klicken Sie auf die Registerkarte **Zentrale Richtlinie**.  
  
8.  Klicken Sie auf **Ändern**, wählen Sie **Finance Policy** aus dem Dropdownmenü aus, und klicken Sie dann auf **Übernehmen**. **Finance Documents Rule** wird in der Richtlinie aufgelistet angezeigt. Erweitern Sie das Element, um alle von Ihnen beim Erstellen der Regel in Active Directory festgelegten Berechtigungen anzuzeigen.  
  
9. Klicken Sie auf **OK**, um zum Windows-Explorer zurückzukehren.  
  
Im nächsten Schritt stellen Sie sicher, dass der Zugriff richtig konfiguriert wurde.  Für Benutzerkonten muss das richtige „Department“-Attribut festgelegt sein (legen Sie dieses mithilfe des Active Directory-Verwaltungscenters fest). Die einfachste Möglichkeit, die effektiven Ergebnisse der neuen Richtlinie anzuzeigen, besteht darin, die Registerkarte **Effektiver Zugriff** im Windows-Explorer zu verwenden. Auf der Registerkarte **Effektiver Zugriff** werden die Zugriffsrechte für ein angegebenes Benutzerkonto angezeigt.  
  
#### <a name="to-examine-the-access-for-various-users"></a>So überprüfen Sie den Zugriff für verschiedene Benutzer  
  
1.  Stellen Sie im Hyper-V-Manager eine Verbindung mit dem Server „FILE1“ her. Melden Sie sich am Server unter Verwendung von „contoso\administrator“ an. Navigieren Sie im Windows-Explorer zu Laufwerk „D:\“. Klicken Sie mit der rechten Maustaste auf den Ordner **Finance Documents**, und klicken Sie dann auf **Eigenschaften**.  
  
2.  Klicken Sie auf der Registerkarte **Sicherheit** auf **Erweitert**, und klicken Sie dann auf die Registerkarte **Effektiver Zugriff**.  
  
3.  Klicken Sie zum Überprüfen der Berechtigungen für einen Benutzer auf **wählen Sie einen Benutzer**, geben Sie den Namen des Benutzers ein, und klicken Sie dann auf **effektiven Zugriff anzeigen** um die effektiven Zugriffsrechte anzuzeigen. Zum Beispiel:  
  
    -   Myriam Delesalle (MDelesalle) ist Mitglied der Finanzabteilung und sollte die Zugriffsberechtigung „Lesen“ für den Ordner haben.  
  
    -   Miles Reid (MReid) ist ein Mitglied der Gruppe „FinanceAdmin“ und sollte die Zugriffsberechtigung „Ändern“ für den Ordner haben.  
  
    -   Esther Valle (EValle) ist kein Mitglied in der Finanzabteilung, sie ist jedoch ein Mitglied der Gruppe „FinanceException“ und sollte die Zugriffsberechtigung „Lesen“ haben.  
  
    -   Maira Wenzel (MWenzel) ist kein Mitglied der Finanzabteilung und weder ein Mitglied der Gruppe „FinanceAdmin“ noch der Gruppe „FinanceException“. Sie sollte keinerlei Zugriffsrechte für den Ordner haben.  
  
    Beachten Sie die letzte Spalte namens **Zugriff eingeschränkt durch** im Fenster für den effektiven Zugriff. Diese Spalte verrät Ihnen mit, welche Gates Berechtigungen der Person begegnen können. In diesem Fall ermöglichen die Berechtigungen „Share“ und „NTFS“ allen Benutzern den vollständigen Zugriff. Die zentrale Zugriffsrichtlinie schränkt jedoch den Zugriff anhand der von Ihnen zuvor konfigurierten Regeln ein.  
  
## <a name="BKMK_1.5"></a>Maintain: Ändern und Staging der Richtlinie  
  
||||  
|-|-|-|  
|Number|Schritt|Beispiel|  
|4.1|Konfigurieren von Geräteansprüchen für Clients|Festlegen der Gruppenrichtlinieneinstellung zum Aktivieren von Geräteansprüchen|  
|4.2|Aktivieren Sie einen Anspruch für Geräte.|Aktivieren Sie den Landanspruchstyp für Geräte.|  
|4.3|Fügen Sie der vorhandenen zentralen Zugriffsrichtlinie eine Staging-Richtlinie hinzu, die Sie ändern möchten.|Ändern Sie die „Finance Documents Rule“ zum Hinzufügen einer Staging-Richtlinie.|  
|4.4|Zeigen Sie die Ergebnisse der Staging-Richtlinie an.|Suchen Sie nach Velles Berechtigungen.|  
  
#### <a name="to-set-up-group-policy-setting-to-enable-claims-for-devices"></a>So richten Sie die Gruppenrichtlinieneinstellung zum Aktivieren von Ansprüchen für Geräte ein  
  
1.  Melden Sie sich bei „DC1“ an, öffnen Sie die Gruppenrichtlinienverwaltung, klicken Sie auf **contoso.com**, klicken Sie auf  **Standarddomänenrichtlinie**, klicken Sie mit der rechten Maustaste auf **Bearbeiten**, und wählen Sie die Option aus.  
  
2.  Navigieren Sie im Gruppenrichtlinienverwaltungs-Editor-Fenster zu **Computerkonfiguration**, **Richtlinien**, **Administrative Vorlagen**, **System**, **Kerberos**.  
  
3.  Wählen Sie die Option für die Kerberos-Clientunterstützung für Ansprüche, Verbundauthentifizierung und Kerberos Armoring****, und klicken Sie auf **Aktivieren**.  
  
#### <a name="to-enable-a-claim-for-devices"></a>So aktivieren Sie einen Anspruch für Geräte  
  
1.  Öffnen Sie auf Server "DC1" im Hyper-V-Manager, und melden als "Contoso\Administrator" mit dem Kennwort **pass@word1**.  
  
2.  Öffnen Sie im Menü **Extras** das Active Directory-Verwaltungscenter.  
  
3.  Klicken Sie auf **Strukturansicht**, erweitern Sie **Dynamische Zugriffssteuerung**, doppelklicken Sie auf **Anspruchstypen**, und doppelklicken Sie auf den Anspruch **country**.  
  
4.  Aktivieren Sie das Kontrollkästchen **Computer** unter **Ansprüche von diesem Typ können für die folgenden Klassen ausgegeben werden**. Klicken Sie auf **OK**.   
    Die Kontrollkästchen **Benutzer** und **Computer** sollten nun aktiviert sein. Der Anspruch „country“ kann nun mit Geräten zusätzlich zu Benutzern verwendet werden.  
  
Im nächsten Schritt wird eine Staging-Richtlinienregel erstellt. Staging-Richtlinien können zum Überwachen von Auswirkungen eines neuen Richtlinieneintrags verwendet werden, bevor Sie ihn aktivieren. Im folgenden Schritt erstellen Sie einen Staging-Richtlinieneintrag und überwachen die Auswirkung auf Ihren freigegebenen Ordner.  
  
#### <a name="to-create-a-staging-policy-rule-and-add-it-to-the-central-access-policy"></a>So erstellen Sie eine Staging-Richtlinienregel und fügen sie zur zentralen Zugriffsrichtlinie hinzu  
  
1.  Öffnen Sie auf Server "DC1" im Hyper-V-Manager, und melden als "Contoso\Administrator" mit dem Kennwort **pass@word1**.  
  
2.  Öffnen Sie das Active Directory-Verwaltungscenter.  
  
3.  Klicken Sie auf **Strukturansicht**, erweitern Sie **Dynamische Zugriffssteuerung**, und wählen Sie **Zentrale Zugriffsregeln** aus.  
  
4.  Klicken Sie mit der rechten Maustaste auf **Finance Documents Rule**, und klicken Sie dann auf **Eigenschaften**.  
  
5.  Aktivieren Sie das Kontrollkästchen **Konfiguration des Berechtigungsstaging aktivieren** im Abschnitt **Vorgesehene Berechtigungen**, klicken Sie auf **Bearbeiten** und dann auf **Hinzufügen**. Klicken Sie im Fenster **Berechtigungseintrag für vorgesehene Berechtigungen** auf die Verknüpfung **Prinzipal auswählen**, geben Sie **Authentifizierte Benutzer** ein, und klicken Sie dann auf **OK**.  
  
6.  Klicken Sie auf die Verknüpfung **Bedingung hinzufügen**, und fügen Sie die folgende Bedingung hinzu:   
     [**User**] [**country**] [**Any of**] [**Resource**] [**Country**].  
  
7.  Klicken Sie erneut auf **Bedingung hinzufügen**, und fügen Sie die folgende Bedingung hinzu:  
    [**And**]   
     [**Device**] [**country**] [**Any of**] [**Resource**] [**Country**]  
  
8.  Klicken Sie erneut auf **Bedingung hinzufügen**, und fügen Sie die folgende Bedingung hinzu.  
    [And]   
     [**Benutzer**] [**Gruppe**] [**Mitglied einer**] [**Wert**]\(**"financeexception"**)  
  
9. Klicken Sie zum Festlegen der Gruppe „FinanceException“ auf **Add items**, und geben Sie **FinanceException** in das Fenster **Benutzer, Computer, Dienstkonto oder Gruppe auswählen** ein.  
  
10. Klicken Sie auf **Berechtigungen**, wählen Sie **Vollzugriff** aus, und klicken Sie auf **OK**.  
  
11. Wählen Sie **FinanceException** im Fenster für die erweiterten Sicherheitseinstellungen für vorgesehene Berechtigungen aus, und klicken Sie auf **Entfernen**.  
  
12. Klicken Sie zweimal auf **OK**, um den Vorgang abzuschließen.  
  
![Lösungshandbücher](media/Deploy-a-Central-Access-Policy--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
Set-ADCentralAccessRule  
-Identity: "CN=FinanceDocumentsRule,CN=CentralAccessRules,CN=ClaimsConfiguration,CN=Configuration,DC=Contoso.com"  
-ProposedAcl: "O:SYG:SYD:AR(A;;FA;;;BA)(A;;FA;;;SY)(A;;0x1301bf;;;S-1-21=1426421603-1057776020-1604)"  
-Server: "WIN-2R92NN8VKFP.Contoso.com"  
  
```  
  
> [!NOTE]  
> Im obigen Cmdlet-Beispiel spiegelt der Wert „Server“ den Server in der Testlaborumgebung wider. Sie können die Windows PowerShell-Verlaufsanzeige verwenden, um Windows PowerShell-Cmdlets nach jeder Prozedur zu durchsuchen, die Sie im Active Directory-Verwaltungscenter ausführen. Weitere Informationen finden Sie unter [Windows PowerShell History Viewer](https://technet.microsoft.com/library/hh831702)  
  
In diesem Satz vorgesehener Berechtigungen verfügen Mitglieder der Gruppe „FinanceException“ über den vollständigen Zugriff auf Dateien ihres eigenen Lands, wenn sie über ein Gerät aus demselben Land wie das Dokument auf die Dateien zugreifen. Überwachungseinträge stehen im Dateiserver-Sicherheitsprotokoll zur Verfügung, wenn jemand aus der Finanzabteilung versucht, auf die Dateien zuzugreifen. Die Sicherheitseinstellungen werden jedoch nicht erzwungen, bis die Richtlinie vom Staging höher gestuft wird.  
  
Im nächsten Verfahren stellen Sie die Ergebnisse der Staging-Richtlinie sicher. Sie greifen mit einem Benutzernamen, der über Berechtigungen auf Grundlage der aktuellen Regel verfügt, auf den freigegebenen Ordner zu. Esther Valle (EValle) ist ein Mitglied von „FinanceException“, und zurzeit verfügt sie über Lesezugriff. Gemäß unserer Staging-Richtlinie sollte EValle keinerlei Rechte besitzen.  
  
#### <a name="to-verify-the-results-of-the-staging-policy"></a>So überprüfen Sie die Ergebnisse der Staging-Richtlinie  
  
1.  Herstellen einer Verbindung mit dem Dateiserver FILE1 im Hyper-V-Manager, und melden für als "Contoso\Administrator" mit dem Kennwort **pass@word1**.  
  
2.  Öffnen Sie ein Eingabeaufforderungsfenster, und geben Sie **gpupdate /force** ein. Dadurch wird sichergestellt, dass Ihre Gruppenrichtlinienänderungen auf Ihrem Server wirksam werden.  
  
3.  Stellen Sie im Hyper-V-Manager eine Verbindung mit dem Server „CLIENT1“ her. Melden Sie den derzeit angemeldeten Benutzer ab. Starten Sie den virtuellen Computer „CLIENT1“ neu. Klicken Sie dann melden Sie sich bei dem Computer mit Contoso\EValle pass@word1.  
  
4.  Doppelklicken Sie auf die desktopverknüpfung zu \\\FILE1\Finance Dokumente. EValle sollte weiterhin auf die Dateien zugreifen können. Wechseln Sie zurück zu „FILE1“.  
  
5.  Öffnen Sie die Ereignisanzeige über die Verknüpfung auf dem Desktop****. Erweitern Sie **Windows-Protokolle**, und wählen Sie dann **Sicherheit** aus. Öffnen Sie die Einträge mit **Event ID 4818**unter der **Staging zentraler Zugriffsrichtlinien** Aufgabenkategorie. Sie werden sehen, dass EValle der Zugriff gewährt wurde. Entsprechend der Staging-Richtlinie würde dem Benutzer jedoch der Zugriff verweigert werden.  
  
## <a name="next-steps"></a>Nächste Schritte  
Wenn Sie über ein zentrales Serververwaltungssystem wie System Center Operations Manager verfügen, können Sie auch die Ereignisüberwachung konfigurieren. Dadurch können Administratoren die Auswirkungen der zentralen Zugriffsrichtlinien überwachen, bevor sie sie erzwingen.  
  

