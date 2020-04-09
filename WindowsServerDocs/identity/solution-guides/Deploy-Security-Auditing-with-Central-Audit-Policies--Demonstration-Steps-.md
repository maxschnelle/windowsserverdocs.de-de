---
ms.assetid: 22347a94-aeea-44b4-85fb-af2c968f432a
title: Bereitstellen der Sicherheitsüberwachung mit zentralen Überwachungsrichtlinien (Demonstrationsschritte)
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 9ad3f069eaea6917d29f56a00c6ecde035ecb01d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861193"
---
# <a name="deploy-security-auditing-with-central-audit-policies-demonstration-steps"></a>Bereitstellen der Sicherheitsüberwachung mit zentralen Überwachungsrichtlinien (Demonstrationsschritte)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Szenario überwachen Sie den Zugriff auf Dateien im Ordner "Finance Documents" mithilfe der Finance-Richtlinie, die Sie unter Bereitstellen [einer &#40;zentralen Zugriffs&#41;Richtlinie](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md)erstellt haben. Wenn ein Benutzer, der nicht auf den Ordner zugreifen darf, dennoch versucht, darauf zuzugreifen, wird die Aktivität in der Ereignisanzeige aufgezeichnet.   
 Zum Testen dieses Szenarios sind die folgenden Schritte erforderlich.  
  
|Aufgabe|Beschreibung|  
|--------|---------------|  
|[Konfigurieren des globalen Objekt Zugriffs](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md#BKMK_1)|In diesem Schritt konfigurieren Sie die globale Objektzugriffsrichtlinie auf dem Domänencontroller.|  
|[Aktualisieren von Gruppenrichtlinie Einstellungen](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md#BKMK_2)|Melden Sie sich am Dateiserver an, und wenden Sie die Gruppenrichtlinienaktualisierung an.|  
|[Überprüfen Sie, ob die globale Objekt Zugriffs Richtlinie angewendet wurde.](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md#BKMK_3)|Zeigen Sie die relevanten Ereignisse in der Ereignisanzeige an. Die Ereignisse sollten Metadaten für das Land und den Dokumenttyp umfassen.|  
  
## <a name="configure-global-object-access-policy"></a><a name="BKMK_1"></a>Globale Objekt Zugriffs Richtlinie konfigurieren  
In diesem Schritt konfigurieren Sie die globale Objektzugriffsrichtlinie auf dem Domänencontroller.  
  
#### <a name="to-configure-a-global-object-access-policy"></a>So konfigurieren Sie eine globale Objektzugriffsrichtlinie  
  
1. Melden Sie sich beim Domänen Controller DC1 als condeso\administrator mit dem Kennwort <strong>pass@word1</strong>an.  
  
2. Zeigen Sie in Server-Manager auf **Extras**, und klicken Sie dann auf **Gruppenrichtlinienverwaltung**.  
  
3. Doppelklicken Sie in der Konsolenstruktur auf **Domänen**, doppelklicken Sie auf **contoso.com**, klicken Sie auf **Contoso**, und doppelklicken Sie dann auf **Dateiserver**.  
  
4. Klicken Sie mit der rechten Maustaste auf **FlexibleAccessGPO**, und klicken Sie dann auf **Bearbeiten**.  
  
5. Doppelklicken Sie auf **Computerkonfiguration**, doppelklicken Sie auf **Richtlinien**, und doppelklicken Sie dann auf **Windows-Einstellungen**.  
  
6. Doppelklicken Sie auf **Sicherheitseinstellungen**, doppelklicken Sie auf **Erweiterte Überwachungsrichtlinienkonfiguration**, und doppelklicken Sie dann auf **Überwachungsrichtlinien**.  
  
7. Doppelklicken Sie auf **Objektzugriff**, und doppelklicken Sie dann auf **Dateisystem überwachen**.  
  
8. Aktivieren Sie das Kontrollkästchen **Folgende Überwachungsereignisse konfigurieren**, aktivieren Sie die Kontrollkästchen **Erfolgreich** und **Fehler**, und klicken Sie dann auf **OK**.  
  
9. Doppelklicken Sie im Navigationsbereich auf **Globale Objektzugriffsüberwachung**, und doppelklicken Sie dann auf **Dateisystem**.  
  
10. Aktivieren Sie das Kontrollkästchen **Diese Richtlinieneinstellung definieren**, und klicken Sie auf **Konfigurieren**.  
  
11. Klicken Sie im Feld **Erweiterte Sicherheitseinstellungen für SACL der Globaldatei** auf **Hinzufügen**, klicken Sie auf **Prinzipal auswählen**, geben Sie **Jeder** ein, und klicken Sie dann auf **OK**.  
  
12. Wählen Sie im Feld **Überwachungseintrag für SACL der Globaldatei** die Option **Vollzugriff** im Feld **Berechtigungen** aus.  
  
13. Klicken Sie im Abschnitt **Bedingung hinzufügen** auf **Bedingung hinzufügen** , und wählen Sie in den Dropdown Listen die Option   
    [**Ressource**] [**Abteilung**] [**Any von**] [**Wert**] [**Finanzen**].  
  
14. Klicken Sie dreimal auf **OK**, um die Konfiguration der Richtlinieneinstellung für die globale Objektzugriffsüberwachung abzuschließen.  
  
15. Klicken Sie im Navigationsbereich auf **Objektzugriff**, und doppelklicken Sie im Ergebnisbereich auf **Handleänderung überwachen**. Klicken Sie auf **Folgende Überwachungsereignisse konfigurieren**, **Erfolgreich** und **Fehler**, klicken Sie auf **OK**, und schließen Sie dann das GPO für den flexiblen Zugriff.  
  
## <a name="update-group-policy-settings"></a><a name="BKMK_2"></a>Aktualisieren von Gruppenrichtlinie Einstellungen  
In diesem Schritt aktualisieren Sie die Gruppenrichtlinieneinstellungen, nachdem Sie die Überwachungsrichtlinie erstellt haben.  
  
#### <a name="to-update-group-policy-settings"></a>So aktualisieren Sie die Gruppenrichtlinieneinstellungen  
  
1. Melden Sie sich am Dateiserver file1 als condeso\administrator mit dem Kennwort an <strong>pass@word1</strong>.  
  
2. Drücken Sie die Windows-Taste+R, und geben Sie **cmd** ein, um ein Befehlseingabefenster zu öffnen.  
  
   > [!NOTE]  
   > Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass die angezeigte Aktion ausgeführt werden soll, und klicken Sie anschließend auf **Ja**.  
  
3. Geben Sie **gpupdate /force** ein, und drücken Sie dann die EINGABETASTE.  
  
## <a name="verify-that-the-global-object-access-policy-has-been-applied"></a><a name="BKMK_3"></a>Überprüfen Sie, ob die globale Objekt Zugriffs Richtlinie angewendet wurde.  
Nachdem die Gruppenrichtlinieneinstellungen angewendet wurden, können Sie überprüfen, ob die Überwachungsrichtlinieneinstellungen richtig angewendet wurden.  
  
#### <a name="to-verify-that-the-global-object-access-policy-has-been-applied"></a>So stellen Sie sicher, dass die globale Objektzugriffsrichtlinie angewendet wurde  
  
1.  Melden Sie sich am Clientcomputer CLIENT1 als %%amp;quot;Contoso\MReid%%amp;quot; an. Navigieren Sie zum Ordner Hyperlink "file:///\\\\\\\ ID_AD_FILE1\\\Finance" \\\ FILE1\Finance Dokumente, und ändern Sie Word Document 2.  
  
2.  Melden Sie sich am Dateiserver FILE1 als %%amp;quot;contoso\administrator%%amp;quot; an. Öffnen Sie die Ereignisanzeige, wechseln Sie zu **Windows-Protokolle**, wählen Sie **Sicherheit** aus, und vergewissern Sie sich, dass Ihre Aktivitäten zu den Überwachungsereignissen **4656** und **4663** geführt haben (obwohl sie keine expliziten Überwachungs-SACLs für die erstellten, geänderten und gelöschten Dateien oder Ordner festgelegt haben).  
  
> [!IMPORTANT]  
> Ein neues Anmeldeereignis wird auf dem Computer generiert, auf dem sich die Ressource befindet. Dies geschieht im Namen des Benutzers, für den der effektive Zugriff überprüft wird. Um beim Analysieren von Sicherheitsüberwachungsprotokollen für Benutzeranmeldeaktivitäten zwischen Anmeldeereignissen, die aufgrund des effektiven Zugriffs generiert wurden, und solchen, die aufgrund einer interaktiven Netzwerkbenutzeranmeldung generiert wurden, zu unterscheiden, werden die Informationen zur Identitätswechselebene eingeschlossen. Wenn das Anmeldeereignis aufgrund des effektiven Zugriffs generiert wird, ist die Identitätswechselebene %%amp;quot;Identität%%amp;quot;. Eine interaktive Netzwerkbenutzeranmeldung generiert normalerweise ein Anmeldeereignis mit der Identitätswechselebene %%amp;quot;Identitätswechsel%%amp;quot; oder %%amp;quot;Delegierung%%amp;quot;.  
  
## <a name="see-also"></a><a name="BKMK_Links"></a>Siehe auch  
  
-   [Szenario: Datei Zugriffs Überwachung](Scenario--File-Access-Auditing.md)  
  
-   [Planen der Dateizugriffsüberwachung](Plan-for-File-Access-Auditing.md)  
  
-   [Dynamisches Access Control: Szenarioübersicht](Dynamic-Access-Control--Scenario-Overview.md)  
  

