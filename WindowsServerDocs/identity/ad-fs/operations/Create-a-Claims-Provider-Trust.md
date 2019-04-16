---
ms.assetid: a4f7842c-cfca-4d78-916e-023d12a9cdf0
title: Erstellen einer Anspruchsanbieter-Vertrauensstellung
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b4dc20713fdd137b019a072037e35e9219e02fa9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-claims-provider-trust"></a>Erstellen einer Anspruchsanbieter-Vertrauensstellung

>Gilt für: Windows Server 2016, Windows Server2012 R2

Um eine neue Anspruchsanbieter-Vertrauensstellung mithilfe von AD FS-Verwaltungs-Snap-In hinzufügen und die Einstellungen manuell konfigurieren, führen Sie das folgende Verfahren auf einen ressourcenpartnerverbundserver in der Ressourcenpartnerorganisation.  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer die Mindestanforderung zum Ausführen dieses Verfahrens.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
## <a name="to-create-a-claims-provider-trust-manually"></a>So erstellen Sie manuell eine Anspruchsanbieter-Vertrauensstellung  
  
1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  Klicken Sie unter **Aktionen**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellung hinzufügen**.  
![Anspruchsanbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim1.PNG)   
  
3.  Auf der **Willkommen** auf **starten**. 
![Anspruchsanbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim2.PNG)    
  
4.  Auf der **Auswählen einer Datenquelle** auf **EINGABETASTE Anspruchsdaten Anbieter Vertrauensstellung manuell**, und klicken Sie dann auf **Weiter**.  
![Anspruchsanbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim3.PNG)     

5.  Auf der **Anzeigename angeben** geben einen **Anzeigenamen**unter **Notizen**, geben Sie eine Beschreibung für diese Anbieter Vertrauensstellung, und klicken Sie dann auf **Weiter**.  
![Anspruchsanbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim4.PNG)     

6.  Auf der **URL konfigurieren** geben die **URL des passiven WS-Verbund:** ggf., und klicken Sie auf **Weiter**.
![Anspruchsanbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim5.PNG)     

8. Auf der **Bezeichner konfigurieren** Seite unter **Anspruchsanbieter-Vertrauensstellung ID**, geben Sie den entsprechenden Bezeichner ein, und klicken Sie dann auf **Weiter**.  
![Anspruchsanbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim6.PNG)    

9. Auf der **Konfigurieren von Zertifikaten** auf **hinzufügen** eine Datei suchen und die Liste der Zertifikate hinzufügen, und klicken Sie auf **Weiter**.  
![Anspruchsanbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim7.PNG)    

10. Auf der **bereit zum Hinzufügen der Vertrauensstellung** auf **Weiter** Ihrer Ansprüche Anbieter Vertrauensstellungsinformationen speichern.  
![Anspruchsanbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim8.PNG)    

11. Auf der **Fertig stellen** auf **schließen**. Diese Aktion zeigt automatisch die **Anspruchsregeln bearbeiten** Dialogfeld. Weitere Informationen zum Hinzufügen von Anspruchsregeln für diese Anspruchsanbieter-Vertrauensstellung finden Sie unter den folgenden zusätzlichen Referenzen.  
![Anspruchsanbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim9.PNG)

## <a name="to-create-a-claims-provider-trust-using-federation-metadata"></a>Erstellen eine Anspruchsanbieter-Vertrauensstellung mithilfe von Verbundmetadaten
Führen Sie zum Hinzufügen einer neuen Anspruchsanbieter-Vertrauensstellung, über das AD FS-Verwaltungs-Snap-In, automatisches Importieren von Konfigurationsdaten zum Partner aus Verbundmetadaten, die der Partner in einem lokalen Netzwerk oder dem Internet veröffentlicht hat das folgende Verfahren auf einem Verbundserver in der Ressourcenpartnerorganisation.

>[!NOTE]
>Wenn sie lange gängige Praxis, Zertifikate mit nicht qualifizierten Hostnamen wie https://myserver verwendet wurde, wird diese Zertifikate haben keinen Sicherheitswert und können einem Angreifer ermöglichen, einen Verbunddienst zu imitieren, der Verbundmetadaten veröffentlicht. Aus diesem Grund sollten beim Abfragen von Verbundmetadaten Sie nur einen vollqualifizierten Domänennamen wie https://myserver.contoso.com verwenden.

1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  Klicken Sie unter **Aktionen**, klicken Sie auf **Party Vertrauensstellung der vertrauenden Seite hinzufügen**.  
![Anspruchsanbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim1.PNG)   
  
3.  Auf der **Willkommen** auf **starten**. 
![Anspruchsanbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim2.PNG)    
  
4.  Auf der **Auswählen einer Datenquelle** auf **online oder in einem lokalen Netzwerk veröffentlichte Daten über den Anspruchsanbieter importieren**. Geben Sie im Verbund-Adresse (Hostname oder URL) der **Verbundmetadaten-URL** oder den Hostnamen für den Partner, und klicken Sie dann auf **Weiter**.
![Anspruchsanbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim10.PNG)    

5.  Typ der Seite Anzeigename angeben einen **Anzeigenamen**, geben Sie unter Anmerkungen eine Beschreibung für diese Anbieter Vertrauensstellung, und klicken Sie dann auf **Weiter**.

6.  Klicken Sie auf der Seite bereit zum Hinzufügen der Vertrauensstellung auf **Weiter** Ihrer Ansprüche Anbieter Vertrauensstellungsinformationen speichern.

7.  Klicken Sie auf der Seite zum Fertigstellen auf **schließen**. Dies wird automatisch das Dialogfeld "Anspruchsregeln bearbeiten" angezeigt. Weitere Informationen zum Hinzufügen von Anspruchsregeln für diese Anspruchsanbieter-Vertrauensstellung, finden Sie im AbschnittWeitere Referenzen.



    
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Konfigurieren der Ressourcenpartnerorganisation](../../ad-fs/deployment/Checklist--Configuring-the-Resource-Partner-Organization.md)  
  
[Prüfliste: Erstellen von Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung](../../ad-fs/deployment/Checklist--Creating-Claim-Rules-for-a-Claims-Provider-Trust.md)  
  
## <a name="see-also"></a>Siehe auch  
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md) 
  
