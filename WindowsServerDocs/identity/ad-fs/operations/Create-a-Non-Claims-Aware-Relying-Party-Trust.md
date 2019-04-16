---
ms.assetid: 7b7ae389-5032-44f7-9c0a-94398c3e4d88
title: "Erstellen einer Ansprüche nicht bewusst Vertrauensstellung der vertrauenden Seite"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f46675ff4c471af743fd8782c1e3036e7c546256
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-non-claims-aware-relying-party-trust"></a>Erstellen einer Ansprüche nicht unterstützenden Vertrauensstellungen der vertrauenden Seite Vertrauensstellung

>Gilt für: Windows Server 2016, Windows Server2012 R2

In AD FS-Verwaltungs-Snap-In, Claims\ unterstützenden Vertrauensstellungen der vertrauenden Seite Vertrauensstellungen sind Objekte, die erstellt werden, um die Vertrauensstellung zwischen Verbunddienst und eine einzelne webbasierte Anwendung, die nicht Claims\-fähig und, erfolgt über das Web Application Proxy, darzustellen.  
  
Eine Claims\ unterstützende Vertrauensstellung für vertrauende Seiten wird eine Vertrauensstellung für vertrauende Seiten von IDs, Namen und Regeln für die Authentifizierung und Autorisierung besteht aus, wenn die Vertrauensstellung der vertrauenden Seite über das Web Application Proxy zugegriffen wird. Diese webbasierten Anwendungen, die nicht auf Ansprüche angewiesen sind also diese Authentication\ der integrierten Windows-basierte Apps können Autorisierungsregeln, die Zugriff zu erzwingen, die Ansprüche basierend auf den Zugriff mit dem Unternehmensnetzwerk über das Web Application Proxy externen ist.  
  
Führen Sie das folgende Verfahren zum Hinzufügen einer neuen Claims\ unterstützende Vertrauensstellung für vertrauende Seiten, mithilfe von AD FS-Verwaltungs-Snap-In.  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
##<a name="to-create-a-non-claims-aware-relying-party-trust-manually"></a>Zum manuellen Erstellen einer Ansprüche nicht bewusst Vertrauensstellungen der vertrauenden Seite Vertrauensstellung 
1. Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  Klicken Sie unter **Aktionen**, klicken Sie auf **Party Vertrauensstellung der vertrauenden Seite hinzufügen**.  
![Vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust1.PNG)   

3.  Auf der **Willkommen** Seite **Non-Claims-aware**, und klicken Sie auf **starten**.  
![Vertrauende Seite](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon1.PNG) 
  
4.  Auf der **Anzeigename angeben** Geben Sie einen Namen in **Anzeigenamen**unter **Notizen** Geben Sie eine Beschreibung für diese Vertrauensstellung der vertrauenden Seite, und klicken Sie dann auf **Weiter**.  
![Vertrauende Seite](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon2.PNG)

5. Auf der **Konfigurieren von Bezeichnern** Seite, geben Sie einen oder mehrere Bezeichner für diese vertrauende, klicken Sie auf **hinzufügen**, fügen sie Sie der Liste, und klicken Sie dann auf **Weiter**.  
![Vertrauende Seite](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon3.PNG)

6.  Auf der **Zugriffssteuerungsrichtlinie wählen** wählen Sie eine Richtlinie, und klicken Sie auf **Weiter**.  Weitere Informationen zu Zugriffsrichtlinien, finden Sie unter [Zugriffssteuerungsrichtlinien in AD FS](Access-Control-Policies-in-AD-FS.md). 
![Vertrauende Seite](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon4.PNG)

7. Auf der **bereit zum Hinzufügen der Vertrauensstellung** Seite, überprüfen Sie die Einstellungen, und klicken Sie dann auf **Weiter** zum Speichern der vertrauenden Informationen vertrauen.  
   ![Vertrauende Seite](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon5.PNG) 

8. Auf der **Fertig stellen** auf **schließen**. Diese Aktion zeigt automatisch die **Anspruchsregeln bearbeiten** Dialogfeld.  
![Vertrauende Seite](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon6.PNG)  
  
## <a name="see-also"></a>Siehe auch  
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md) 
