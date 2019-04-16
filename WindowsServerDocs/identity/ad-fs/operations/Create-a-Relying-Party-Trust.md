---
ms.assetid: 5b9fc9c1-5d12-4ad4-8ddc-3b8a6d45b217
title: Erstellen einer Vertrauensstellung der vertrauenden Seite
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 14e1cc732ed60b7f05a9a4a9aac9037c48b702f2
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-relying-party-trust"></a>Erstellen einer Vertrauensstellung der vertrauenden Seite

>Gilt für: Windows Server 2016, Windows Server2012 R2

Das folgende Dokument enthält Informationen zu eine Vertrauensstellung der vertrauenden Seite manuell erstellen und mithilfe von Verbundmetadaten.
  
## <a name="to-create-a-claims-aware-relying-party-trust-manually"></a>Erstellen einer Ansprüche kennen der vertrauenden Seite Vertrauensstellung manuell 

Um eine neue Vertrauensstellung einer vertrauenden Seite mithilfe von AD FS-Verwaltungs-Snap-In hinzufügen und die Einstellungen manuell konfigurieren, führen Sie das folgende Verfahren auf einem Verbundserver.  

Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).
  
1. Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  Klicken Sie unter **Aktionen**, klicken Sie auf **Party Vertrauensstellung der vertrauenden Seite hinzufügen**.  
![Vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust1.PNG)   

3.  Auf der **Willkommen** Seite **Claims-aware**, und klicken Sie auf **starten**.  
![Vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust2.PNG) 
  
4.  Auf der **Auswählen einer Datenquelle** auf **Daten über die vertrauende Seite manuell eingeben**, und klicken Sie dann auf **Weiter**.  
![Vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust3.PNG) 
  
5.  Auf der **Anzeigename angeben** Geben Sie einen Namen in **Anzeigenamen**unter **Notizen** Geben Sie eine Beschreibung für diese Vertrauensstellung der vertrauenden Seite, und klicken Sie dann auf **Weiter**.  
![Vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust4.PNG) 

6. Auf der **Konfigurieren eines Zertifikats** besitzen Sie ein optionales Token Verschlüsselungszertifikat, klicken Sie auf Seite **Durchsuchen** eine Datei suchen, und klicken Sie auf **Weiter**.  
![Vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust5.PNG) 

7.  Auf der **URL konfigurieren** Seite, führen Sie eine oder beide der folgenden, klicken Sie auf **Weiter**, und fahren Sie mit Schritt8:  
  
    -   Wählen Sie die **Unterstützung für die WS-verbundprotokoll aktivieren** Kontrollkästchen. Klicken Sie unter **passiven WS-Federation-Protokoll-URL von der vertrauenden Seite Party**, geben Sie die URL für diese Vertrauensstellung der vertrauenden Seite, und klicken Sie dann auf **Weiter**.  
  
    -   Wählen Sie die **Aktivieren der Unterstützung für das SAML 2.0 WebSSO-Protokoll** Kontrollkästchen. Klicken Sie unter **der vertrauenden Seite Party SAML 2.0-SSO-Dienst-URL**, geben Sie die Security Assertion Markup Language \(SAML\) Service-Endpunkt-URL für diese Vertrauensstellung der vertrauenden Seite, und klicken Sie dann auf **Weiter**.  
![Vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust6.PNG)   

8. Auf der **Konfigurieren von Bezeichnern** Seite, geben Sie einen oder mehrere Bezeichner für diese vertrauende, klicken Sie auf **hinzufügen**, fügen sie Sie der Liste, und klicken Sie dann auf **Weiter**.  
![Vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust8.PNG)
  
9.  Auf der **Zugriffssteuerungsrichtlinie wählen** wählen Sie eine Richtlinie, und klicken Sie auf **Weiter**.  Weitere Informationen zu Zugriffsrichtlinien, finden Sie unter [Zugriffssteuerungsrichtlinien in AD FS](Access-Control-Policies-in-AD-FS.md). 
![Vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust9.PNG)

10. Auf der **bereit zum Hinzufügen der Vertrauensstellung** Seite, überprüfen Sie die Einstellungen, und klicken Sie dann auf **Weiter** zum Speichern der vertrauenden Informationen vertrauen.  
   ![Vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust10.PNG) 
11. Auf der **Fertig stellen** auf **schließen**. Diese Aktion zeigt automatisch die **Anspruchsregeln bearbeiten** Dialogfeld.  
![Vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust11.PNG) 

## <a name="to-create-a-claims-aware-relying-party-trust-using-federation-metadata"></a>Zum Erstellen einer Ansprüche kennen der vertrauenden Seite Vertrauensstellung mithilfe von Verbundmetadaten

Führen Sie das folgende Verfahren auf einem Verbundserver in der Kontopartnerorganisation, zum Hinzufügen einer neuen Vertrauensstellung einer vertrauenden Seite, mit der AD FS-Verwaltungs-Snap-In Automatisches Importieren von Konfigurationsdaten zum Partner aus Verbundmetadaten, die der Partner in einem lokalen Netzwerk oder im Internet veröffentlicht.

>[!NOTE]
>Wenn sie lange gängige Praxis, Zertifikate mit nicht qualifizierten Hostnamen wie https://myserver verwendet wurde, wird diese Zertifikate haben keinen Sicherheitswert und können einem Angreifer ermöglichen, einen Verbunddienst zu imitieren, der Verbundmetadaten veröffentlicht. Aus diesem Grund sollten beim Abfragen von Verbundmetadaten Sie nur einen vollqualifizierten Domänennamen wie https://myserver.contoso.com verwenden.

Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).


1. Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  Klicken Sie unter **Aktionen**, klicken Sie auf **Party Vertrauensstellung der vertrauenden Seite hinzufügen**.  
![Vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust1.PNG)   

3.  Auf der **Willkommen** Seite **Claims-aware**, und klicken Sie auf **starten**.  
![Vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust2.PNG) 
  
4.  Auf der **Auswählen einer Datenquelle** auf **online oder in einem lokalen Netzwerk veröffentlichte Daten über die vertrauende Seite importieren*. In **Verbundmetadaten-Adresse (Hostname oder URL)**, geben Sie die Metadaten-URL oder den Hostnamen des Verbunddiensts für den Partner, und klicken Sie dann auf **Weiter**.  
![Vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust12.PNG) 

5.  Geben Sie auf der Seite Anzeigename angeben einen Namen in **Anzeigenamen**unter Anmerkungen eine Beschreibung für diese Vertrauensstellung der vertrauenden Seite, und klicken Sie dann auf **Weiter**.

6.  Wählen Sie auf der Seite auswählen von Ausstellungsautorisierungsregeln entweder **allen Benutzern Zugriff auf diese vertrauende** oder **allen Benutzern den Zugriff auf diese vertrauende Seite verweigert**, und klicken Sie dann auf **Weiter**.

7.  Klicken Sie auf der Seite bereit zum Hinzufügen der Vertrauensstellung, überprüfen Sie die Einstellungen, und klicken Sie dann auf **Weiter** zum Speichern der vertrauenden Informationen vertrauen.

8.  Klicken Sie auf der Seite zum Fertigstellen auf **schließen**. Diese Aktion zeigt automatisch das Dialogfeld "Anspruchsregeln bearbeiten". Weitere Informationen zum Hinzufügen von Anspruchsregeln für diese Vertrauensstellung der vertrauenden Seite finden Sie weiteren Referenzen.




## <a name="see-also"></a>Siehe auch  
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md) 
