---
ms.assetid: 5b9fc9c1-5d12-4ad4-8ddc-3b8a6d45b217
title: Erstellen einer Vertrauensstellung der vertrauenden Seite
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a0d32edd7ebc23fa724439710c6511642d9c49a3
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79323052"
---
# <a name="create-a-relying-party-trust"></a>Erstellen einer Vertrauensstellung der vertrauenden Seite


Das folgende Dokument enthält Informationen zum manuellen Erstellen einer Vertrauensstellung der vertrauenden Seite und zum Verwenden von Verbund Metadaten.
  
## <a name="to-create-a-claims-aware-relying-party-trust-manually"></a>So erstellen Sie manuell eine Ansprüche unterstützende Vertrauensstellung der vertrauenden Seite 

Zum Hinzufügen einer neuen Vertrauensstellung der vertrauenden Seite mithilfe des Snap\-"AD FS-Verwaltung" in und manuelles Konfigurieren der Einstellungen führen Sie das folgende Verfahren auf einem Verbund Server aus.  

Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).
  
1. Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  
  
2.  Klicken Sie unter **Aktionen**auf Vertrauensstellung der **vertrauenden Seite hinzufügen**.  
![der vertrauenden Seite](media/Create-a-Relying-Party-Trust/addtrust1.PNG)   

3.  Wählen Sie auf der Seite **Willkommen** die Option **Ansprüche beachten** aus, und klicken Sie auf **starten**.  
![der vertrauenden Seite](media/Create-a-Relying-Party-Trust/addtrust2.PNG) 
  
4.  Klicken Sie auf der Seite **Datenquelle auswählen** auf **Daten über die vertrauende Seite manuell eingeben** , und klicken Sie anschließend auf **Weiter**.  
![der vertrauenden Seite](media/Create-a-Relying-Party-Trust/addtrust3.PNG) 
  
5.  Geben Sie auf der Seite **Anzeige Name angeben** einen Namen in das Feld **Anzeige Name**ein, geben Sie unter **Hinweise** eine Beschreibung für diese Vertrauensstellung der vertrauenden Seite ein, und klicken Sie dann auf **weiter**.  
![der vertrauenden Seite](media/Create-a-Relying-Party-Trust/addtrust4.PNG) 

6. Wenn Sie über ein optionales tokenverschlüsselungszertifikat verfügen, klicken Sie auf der Seite **Zertifikat konfigurieren** auf **Durchsuchen** , um eine Zertifikat Datei zu suchen, und klicken Sie dann auf **weiter**.  
![der vertrauenden Seite](media/Create-a-Relying-Party-Trust/addtrust5.PNG) 

7.  Führen Sie auf der Seite **URL konfigurieren** eine oder beide der folgenden Aktionen aus, klicken Sie auf **weiter**, und fahren Sie dann mit Schritt 8:  
  
    -   Aktivieren Sie das Kontrollkästchen **Unterstützung für das passive WS\-Federation-Protokoll aktivieren** . Geben Sie unter vertrauende **Seite WS\-passive Verbund Protokoll-URL**die URL für diese Vertrauensstellung der vertrauenden Seite ein, und klicken Sie dann auf **weiter**.  
  
    -   Aktivieren Sie das Kontrollkästchen **Unterstützung für das SAML 2.0 WebSSO-Protokoll aktivieren**. Geben Sie unter **SAML 2,0 SSO-Dienst-URL**der vertrauenden Seite die Security Assertion Markup Language \(SAML-\) Dienst Endpunkt-URL für diese Vertrauensstellung der vertrauenden Seite ein, und klicken Sie auf **weiter**  
![der vertrauenden Seite](media/Create-a-Relying-Party-Trust/addtrust6.PNG)   

8. Geben Sie auf der Seite **Konfigurieren von Bezeichnern** einen oder mehrere Bezeichner für diese vertrauende Seite an, klicken Sie auf **Hinzufügen**, um diese der Liste hinzufügen, und klicken Sie dann auf **Weiter**.  
![der vertrauenden Seite](media/Create-a-Relying-Party-Trust/addtrust8.PNG)
  
9.  Wählen Sie unter **Access Control Richtlinie auswählen** eine Richtlinie aus, und klicken Sie auf **weiter**.  Weitere Informationen zu Access Control Richtlinien finden Sie unter [Access Control Policies in AD FS](Access-Control-Policies-in-AD-FS.md). 
![der vertrauenden Seite](media/Create-a-Relying-Party-Trust/addtrust9.PNG)

10. Überprüfen Sie auf der Seite **Bereit zum Hinzufügen der Vertrauensstellung** die Einstellungen, und klicken Sie dann auf **Weiter**, um die Informationen zur Vertrauensstellung der vertrauenden Seite zu speichern.  
   ![der vertrauenden Seite](media/Create-a-Relying-Party-Trust/addtrust10.PNG) 
11. Klicken Sie auf der Seite **Fertig stellen** auf **Schließen**. Dadurch wird automatisch das Dialogfeld **Anspruchsregeln bearbeiten** angezeigt.  
![der vertrauenden Seite](media/Create-a-Relying-Party-Trust/addtrust11.PNG) 

## <a name="to-create-a-claims-aware-relying-party-trust-using-federation-metadata"></a>So erstellen Sie eine Ansprüche unterstützende Vertrauensstellung der vertrauenden Seite mit Verbund Metadaten

Zum Hinzufügen einer neuen Vertrauensstellung der vertrauenden Seite verwenden Sie das Snap-in "AD FS-Verwaltung", indem Sie Konfigurationsdaten über den Partner automatisch aus Verbund Metadaten importieren, die der Partner in einem lokalen Netzwerk oder im Internet veröffentlicht hat. führen Sie dazu das folgende Verfahren auf einem Verbund Server in der Konto Partnerorganisation.

>[!NOTE]
>Obwohl es seit langem üblich ist, Zertifikate mit nicht qualifizierten Hostnamen wie z. b. https://myserverzu verwenden, haben diese Zertifikate keinen Sicherheitswert und können einem Angreifer ermöglichen, die Identität eines Verbunddienst anzunehmen, der Verbund Metadaten veröffentlicht. Daher sollten Sie beim Abfragen von Verbund Metadaten nur einen voll qualifizierten Domänen Namen verwenden, z. b. https://myserver.contoso.com.

Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).


1. Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  
  
2. Klicken Sie unter **Aktionen**auf Vertrauensstellung der **vertrauenden Seite hinzufügen**.  
   ![der vertrauenden Seite](media/Create-a-Relying-Party-Trust/addtrust1.PNG)   

3. Wählen Sie auf der Seite **Willkommen** die Option **Ansprüche beachten** aus, und klicken Sie auf **starten**.  
   ![der vertrauenden Seite](media/Create-a-Relying-Party-Trust/addtrust2.PNG) 
  
4. Klicken Sie auf der Seite **Datenquelle auswählen** auf Daten zur vertrauenden Seite <strong>importieren, die Online oder in einem lokalen Netzwerk veröffentlicht ist *. Geben Sie in * * Verbund Metadaten-Adresse (Hostname oder URL)</strong>die Verbund Metadaten-URL oder den Hostnamen für den Partner ein, und klicken Sie dann auf **weiter**.  
   ![der vertrauenden Seite](media/Create-a-Relying-Party-Trust/addtrust12.PNG) 

5. Geben Sie auf der Seite Anzeige Name angeben einen Namen unter **Anzeige Name**ein, geben Sie unter Hinweise eine Beschreibung für diese Vertrauensstellung der vertrauenden Seite ein, und klicken Sie dann auf **weiter**.

6. Wählen Sie auf der Seite Ausstellungs Autorisierungs Regeln auswählen entweder **allen Benutzern den Zugriff auf diese** vertrauende Seite gestatten aus, oder **verweigern Sie allen Benutzern den Zugriff auf diese**vertrauende Seite, und klicken Sie dann auf **weiter**.

7. Überprüfen Sie auf der Seite bereit zum Hinzufügen der Vertrauensstellung die Einstellungen, und klicken Sie dann auf **weiter** , um die Informationen zur Vertrauensstellung der vertrauenden Seite

8. Klicken Sie auf der Seite Fertigstellen auf **Schließen**. Dadurch wird automatisch das Dialogfeld Anspruchsregeln bearbeiten angezeigt. Weitere Informationen zum Hinzufügen von Anspruchsregeln für diese Vertrauensstellung für die vertrauende Seite finden Sie unter „Weitere Referenzen“.




## <a name="see-also"></a>Weitere Informationen  
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md) 
