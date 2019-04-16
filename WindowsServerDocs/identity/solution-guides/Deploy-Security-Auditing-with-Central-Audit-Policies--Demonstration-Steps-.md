---
ms.assetid: 22347a94-aeea-44b4-85fb-af2c968f432a
title: "Bereitstellen der Sicherheitsüberwachung mit zentralen Überwachungsrichtlinien (Demonstrationsschritte)"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ac2b1643ed151e94c3815abca9a57eb3706c845a
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="deploy-security-auditing-with-central-audit-policies-demonstration-steps"></a>Bereitstellen der Sicherheitsüberwachung mit zentralen Überwachungsrichtlinien (Demonstrationsschritte)

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

In diesem Szenario überwachen Sie den Zugriff auf Dateien im Ordner "Finance Documents" mithilfe der Finanzrichtlinie, die Sie in erstellt [Bereitstellen einer zentralen Zugriffsrichtlinie & 40; Schrittezur Veranschaulichung & 41;](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md). Wenn ein Benutzer, die Zugriff auf den Ordner nicht autorisiert ist, versucht, darauf zuzugreifen, wird die Aktivität in der Ereignisanzeige erfasst.   
 Zum Testen dieses Szenarios sind die folgenden Schritteerforderlich.  
  
|Aufgabe|Beschreibung|  
|--------|---------------|  
|[Konfigurieren globaler Objektzugriff](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md#BKMK_1)|In diesem Schrittkonfigurieren Sie die globale objektzugriffsrichtlinie auf dem Domänencontroller.|  
|[Update mithilfe von Gruppenrichtlinieneinstellungen](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md#BKMK_2)|Melden Sie sich mit dem Dateiserver und die Aktualisierung der Gruppenrichtlinie angewendet.|  
|[Stellen Sie sicher, dass die globale objektzugriffsrichtlinie angewendet wurde](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md#BKMK_3)|Anzeigen der relevanten Ereignisse in der Ereignisanzeige. Die Ereignisse sollten Metadaten für den Typ von Land und den Dokumenttyp umfassen.|  
  
## <a name="BKMK_1"></a>Konfigurieren von globalen objektzugriffsrichtlinie  
In diesem Schrittkonfigurieren Sie die globale objektzugriffsrichtlinie auf dem Domänencontroller.  
  
#### <a name="to-configure-a-global-object-access-policy"></a>So konfigurieren Sie eine globale objektzugriffsrichtlinie  
  
1.  Melden Sie sich am Domänencontroller DC1 als Contoso\administrator mit dem Kennwort **pass@word1**.  
  
2.  Zeigen Sie im Server-Manager auf **Tools**, und klicken Sie dann auf **Gruppenrichtlinienverwaltung **.  
  
3.  Doppelklicken Sie in der Konsolenstruktur auf **Domänen**, doppelklicken Sie auf **contoso.com**, klicken Sie auf **Contoso**, und doppelklicken Sie dann auf **Dateiserver **.  
  
4.  Mit der rechten Maustaste **flexibleAccessGPO**, und klicken Sie auf **bearbeiten **.  
  
5.  Doppelklicken Sie auf **Computerkonfiguration**, doppelklicken Sie auf **Richtlinien**, und doppelklicken Sie dann auf **Windows-Einstellungen **.  
  
6.  Doppelklicken Sie auf **Sicherheitseinstellungen**, doppelklicken Sie auf **erweiterte Überwachungsrichtlinienkonfiguration**, und doppelklicken Sie dann auf **Überwachungsrichtlinien **.  
  
7.  Doppelklicken Sie auf **Objektzugriff**, und doppelklicken Sie dann auf **Dateisystem Überwachen **.  
  
8.  Wählen Sie die **konfigurieren Sie die folgenden Ereignisse** Kontrollkästchen die **Erfolg** und **Fehler** Kontrollkästchen, und klicken Sie dann auf **OK **.  
  
9. Doppelklicken Sie im Navigationsbereich auf **globale Objektzugriffsüberwachung**, und doppelklicken Sie dann auf **Dateisystem **.  
  
10. Wählen Sie die **definieren Sie diese Richtlinieneinstellung**, und klicken Sie auf **konfigurieren **.  
  
11. In der **Advanced Security Settings for Globaldatei** auf **hinzufügen**, klicken Sie dann auf **Prinzipal auswählen**, Typ **jeder**, und klicken Sie dann auf **OK **.  
  
12. In der **Überwachungseintrag für Globaldatei**, aktivieren Sie **Vollzugriff** in die **Berechtigungen** Feld.  
  
13. In der **eine Bedingung hinzufügen:** auf **eine Bedingung hinzufügen,** und führt Sie in der Dropdownliste auswählen   
    [**Ressource**] [**Abteilung**] [**Any of**] [**Value**] [**Finanzen**].  
  
14. Klicken Sie auf **OK** dreimal zum Abschließen der Konfigurations von der globalen Objektzugriffs Richtlinieneinstellung überwachen.  
  
15. Klicken Sie im Navigationsbereich auf **Objektzugriff**, und doppelklicken Sie im Ergebnisbereich auf **Handleänderungsüberwachung **. Klicken Sie auf **folgende Überwachungsereignisse konfigurieren**, **Erfolg**, und **Fehler**, klicken Sie auf **OK**, und schließen Sie dann die flexible Zugriffsoption Gruppenrichtlinienobjekt.  
  
## <a name="BKMK_2"></a>Aktualisieren von Gruppenrichtlinieneinstellungen  
In diesem Schrittaktualisieren Sie die Gruppenrichtlinieneinstellungen, nachdem Sie die Überwachungsrichtlinie erstellt haben.  
  
#### <a name="to-update-group-policy-settings"></a>Um Gruppenrichtlinieneinstellungen zu aktualisieren.  
  
1.  Melden Sie sich am Dateiserver FILE1 als Contoso\Administrator mit dem Kennwort **pass@word1**.  
  
2.  Drücken Sie die Windows Taste + R, geben Sie dann **Cmd** um ein Eingabeaufforderungsfenster zu öffnen.  
  
    > [!NOTE]  
    > Wenn die **User Account Control** Dialogfeld angezeigt wird, stellen Sie sicher, dass die Aktion, die angezeigt wird, was Sie möchten, und klicken Sie dann auf **Ja **.  
  
3.  Typ **Gpupdate/force** und drücken Sie dann die EINGABETASTE.  
  
## <a name="BKMK_3"></a>Stellen Sie sicher, dass die globale objektzugriffsrichtlinie angewendet wurde  
Nachdem die Gruppenrichtlinieneinstellungen angewendet wurden, können Sie überprüfen, ob die Überwachungsrichtlinieneinstellungen richtig angewendet wurden.  
  
#### <a name="to-verify-that-the-global-object-access-policy-has-been-applied"></a>Um sicherzustellen, dass die globale objektzugriffsrichtlinie angewendet wurde  
  
1.  Melden Sie sich Clientcomputer CLIENT1 als "contoso\mreid". Navigieren Sie zum Ordner HYPERLINK "file:///\\\ID_AD_FILE1\\\Finance" \\\ FILE1\Finance Dokumente, und ändern Sie Word-Dokument 2.  
  
2.  Melden Sie sich am Dateiserver FILE1 als "Contoso\Administrator" an. Öffnen Sie die Ereignisanzeige, wechseln Sie zu **Windows-Protokolle**Option **Security**, und stellen Sie sicher, dass Ihre Aktivitäten zu Überwachungsereignissen geführt hat **4656** und **4663** (obwohl Sie nicht explizit Überwachungs-SACLs auf die Dateien oder Ordner, die Sie erstellt festgelegt, geändert und gelöscht).  
  
> [!IMPORTANT]  
> Ein neues Anmeldeereignis wird auf dem Computer generiert, in dem die Ressource im Auftrag des Benutzers befindet, für die effektive Zugriff überprüft wird. Beim Analysieren von Sicherheitsüberwachungsprotokollen für Anmeldung Benutzeraktivitäten zur Unterscheidung von Anmeldeereignissen, die aufgrund des effektiven Zugriffs generiert werden und solche, die aufgrund der generiert eine interaktive Netzwerkbenutzer melden Sie sich, die Informationen zur Identitätswechselebene eingeschlossen ist. Wenn das Anmeldeereignis aufgrund des effektiven Zugriffs generiert wird, werden die Identitätswechselebene Identität. Ein Netzwerk interaktive Anmeldung generiert normalerweise ein Anmeldeereignis mit der Identitätswechselebene = Identitätswechsel oder Delegierung.  
  
## <a name="BKMK_Links"></a>Siehe auch  
  
-   [Szenario: Der Dateizugriffsüberwachung](Scenario--File-Access-Auditing.md)  
  
-   [Planen der Datei Dateizugriffsüberwachung](Plan-for-File-Access-Auditing.md)  
  
-   [Dynamische Zugriffssteuerung: Szenarioübersicht](Dynamic-Access-Control--Scenario-Overview.md)  
  

