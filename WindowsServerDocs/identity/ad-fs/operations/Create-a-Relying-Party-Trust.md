---
ms.assetid: 5b9fc9c1-5d12-4ad4-8ddc-3b8a6d45b217
title: Erstellen einer Vertrauensstellung der vertrauenden Seite
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: e2fba718a68f33f917e4e64863281ff151696ce6
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86965632"
---
# <a name="create-a-relying-party-trust"></a>Erstellen einer Vertrauensstellung der vertrauenden Seite


Das folgende Dokument enthält Informationen zum manuellen Erstellen einer Vertrauensstellung der vertrauenden Seite und zum Verwenden von Verbund Metadaten.
  
## <a name="to-create-a-claims-aware-relying-party-trust-manually"></a>So erstellen Sie manuell eine Ansprüche unterstützende Vertrauensstellung der vertrauenden Seite 

Zum Hinzufügen einer neuen Vertrauensstellung der vertrauenden Seite über das Snap-in "AD FS-Verwaltung" \- und manuelles Konfigurieren der Einstellungen führen Sie das folgende Verfahren auf einem Verbund Server aus.  

Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).
  
1. Klicken Sie im Server-Manager auf **Tools**, und wählen Sie **AD FS-Verwaltung** aus.  
  
2.  Klicken Sie unter **Aktionen**auf Vertrauensstellung der **vertrauenden Seite hinzufügen**.  
![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust1.PNG)   

3.  Wählen Sie auf der **Willkommen**-Seite **Ansprüche unterstützend**, und klicken Sie auf **Start**.  
![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust2.PNG) 
  
4.  Klicken Sie auf der Seite **Datenquelle auswählen** auf **Daten über die vertrauende Seite manuell eingeben **, und klicken Sie anschließend auf **Weiter**.  
![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust3.PNG) 
  
5.  Geben Sie auf der Seite **Anzeigename angeben** einen Namen in **Anzeigename** ein, geben Sie unter **Hinweise** eine Beschreibung für diese Vertrauensstellung der vertrauenden Seite ein, und klicken Sie dann auf **Weiter**.  
![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust4.PNG) 

6. Wenn Sie über ein optionales tokenverschlüsselungszertifikat verfügen, klicken Sie auf der Seite **Zertifikat konfigurieren** auf **Durchsuchen** , um eine Zertifikat Datei zu suchen, und klicken Sie dann auf **weiter**.  
![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust5.PNG) 

7.  Führen Sie auf der Seite **URL konfigurieren** eine oder beide der folgenden Aktionen aus, klicken Sie auf **weiter**, und fahren Sie dann mit Schritt 8:  
  
    -   Aktivieren Sie das Kontrollkästchen **Unterstützung für das \- passive WS-Verbund Protokoll aktivieren** . Geben Sie unter ** \- URL des passiven WS**-Verbund Protokolls die URL für diese Vertrauensstellung der vertrauenden Seite ein, und klicken Sie dann auf **weiter**.  
  
    -   Aktivieren Sie das Kontrollkästchen **Unterstützung für das SAML 2.0 WebSSO-Protokoll aktivieren**. Geben Sie unter **SAML 2,0 SSO-Dienst-URL**der vertrauenden Seite die Security Assertion Markup Language \( SAML \) -Dienst Endpunkt-URL für diese Vertrauens **Next**Stellung der vertrauenden Seite ein, und klicken Sie dann auf  
![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust6.PNG)   

8. Geben Sie auf der Seite **Konfigurieren von Bezeichnern** einen oder mehrere Bezeichner für diese vertrauende Seite an, klicken Sie auf **Hinzufügen**, um diese der Liste hinzufügen, und klicken Sie dann auf **Weiter**.  
![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust8.PNG)
  
9.  Wählen Sie auf der Seite **Zugriffssteuerungsrichtlinie auswählen** eine Richtlinie aus, und klicken Sie auf **Weiter**.  Weitere Informationen zu Access Control Richtlinien finden Sie unter [Access Control Policies in AD FS](Access-Control-Policies-in-AD-FS.md). 
![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust9.PNG)

10. Überprüfen Sie auf der Seite **Bereit zum Hinzufügen der Vertrauensstellung** die Einstellungen, und klicken Sie dann auf **Weiter**, um die Informationen zur Vertrauensstellung der vertrauenden Seite zu speichern.  
   ![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust10.PNG) 
11. Klicken Sie auf der Seite **Fertig stellen** auf **Schließen**. Dadurch wird automatisch das Dialogfeld **Anspruchsregeln bearbeiten** angezeigt.  
![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust11.PNG) 

## <a name="to-create-a-claims-aware-relying-party-trust-using-federation-metadata"></a>So erstellen Sie eine Ansprüche unterstützende Vertrauensstellung der vertrauenden Seite mit Verbund Metadaten

Zum Hinzufügen einer neuen Vertrauensstellung der vertrauenden Seite verwenden Sie das AD FS-Verwaltungs-Snap-in, indem Sie Konfigurationsdaten zum Partner aus Verbund Metadaten, die der Partner in einem lokalen Netzwerk oder im Internet veröffentlicht hat, automatisch importieren. führen Sie dazu das folgende Verfahren auf einem Verbund Server in der Konto Partnerorganisation aus.

>[!NOTE]
>Obwohl es seit langem üblich ist, Zertifikate mit nicht qualifizierten Hostnamen wie zu verwenden https://myserver , haben diese Zertifikate keinen Sicherheitswert und können einem Angreifer ermöglichen, die Identität eines Verbunddienst anzunehmen, der Verbund Metadaten veröffentlicht. Daher sollten Sie beim Abfragen von Verbund Metadaten nur einen voll qualifizierten Domänen Namen wie verwenden https://myserver.contoso.com .

Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).


1. Klicken Sie im Server-Manager auf **Tools**, und wählen Sie **AD FS-Verwaltung** aus.  
  
2. Klicken Sie unter **Aktionen**auf Vertrauensstellung der **vertrauenden Seite hinzufügen**.  
   ![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust1.PNG)   

3. Wählen Sie auf der **Willkommen**-Seite **Ansprüche unterstützend**, und klicken Sie auf **Start**.  
   ![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust2.PNG) 
  
4. Klicken Sie auf der Seite **Datenquelle auswählen** auf Daten zur vertrauenden Seite <strong>importieren, die Online oder in einem lokalen Netzwerk veröffentlicht ist *. Geben Sie in * * Verbund Metadaten-Adresse (Hostname oder URL)</strong>die Verbund Metadaten-URL oder den Hostnamen für den Partner ein, und klicken Sie dann auf **weiter**.  
   ![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust12.PNG) 

5. Geben Sie auf der Seite Anzeige Name angeben einen Namen unter **Anzeige Name**ein, geben Sie unter Hinweise eine Beschreibung für diese Vertrauensstellung der vertrauenden Seite ein, und klicken Sie dann auf **weiter**.

6. Wählen Sie auf der Seite Auswählen von Ausstellungsautorisierungsregeln entweder **Allen Benutzern Zugriff auf diese vertrauende Seite gewähren** oder **Allen Benutzern Zugriff auf diese vertrauende Seite verweigern**, und klicken Sie dann auf **Weiter**.

7. Überprüfen Sie die Einstellungen auf der Seite Bereit zum Hinzufügen der Vertrauensstellung, und klicken Sie dann auf **Weiter**, um die Daten Ihrer Vertrauensstellung der vertrauenden Seite zu speichern.

8. Klicken Sie auf der Seite Fertig stellen auf **Schließen**. Dadurch wird automatisch das Dialogfeld Anspruchsregeln bearbeiten angezeigt. Weitere Informationen zum Hinzufügen von Anspruchsregeln für diese Vertrauensstellung für die vertrauende Seite finden Sie unter „Weitere Referenzen“.




## <a name="see-also"></a>Weitere Informationen  
[AD FS-Vorgänge](../ad-fs-operations.md) 
