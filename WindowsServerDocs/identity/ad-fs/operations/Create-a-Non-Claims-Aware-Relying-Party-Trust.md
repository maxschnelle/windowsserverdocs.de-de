---
ms.assetid: 7b7ae389-5032-44f7-9c0a-94398c3e4d88
title: Erstellen einer Ansprüche nicht unterstützenden Vertrauensstellung der vertrauenden Seite
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f46675ff4c471af743fd8782c1e3036e7c546256
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839341"
---
# <a name="create-a-non-claims-aware-relying-party-trust"></a>Erstellen einer Vertrauensstellung nicht Ansprüche unterstützende der vertrauenden Seite

>Gilt für: Windows Server 2016, Windows Server 2012 R2

Im AD FS-Verwaltungs-Snap-\-in nicht\-Ansprüche\-bewusst sind Objekte, die erstellt werden, um die Vertrauensstellung zwischen Verbunddienst und eine einzelne Web darstellen oder Vertrauensstellungen der vertrauenden\--basierten Anwendung, das nicht ist Ansprüche\-kennen, die über den Webanwendungsproxy erfolgt.  
  
Ein nicht\-Ansprüche\-Vertrauensstellung der vertrauenden Seite ist eine Vertrauensstellung der vertrauenden die IDs, Namen und Regeln für die Authentifizierung und Autorisierung besteht, bei der Vertrauensstellung der vertrauenden Seite über den Webanwendungsproxy zugegriffen wird. Diese Web-\--basierte Anwendungen, die Ansprüche, das heißt, diese integrierten Windows-Authentifizierung nicht abhängen\-basierenden Anwendungen möglich Autorisierungsregeln, die Zugriff zu erzwingen, die auf Ansprüchen basiert, wenn der Zugriff ist externe mit dem Unternehmensnetzwerk über den Webanwendungsproxy.  
  
Zum Hinzufügen einer neuen nicht\-Ansprüche\-bewusst Vertrauensstellung der vertrauenden, mit der AD FS-Verwaltungs-Snap\-, führen Sie das folgende Verfahren.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
##<a name="to-create-a-non-claims-aware-relying-party-trust-manually"></a>Eine Ansprüche nicht beachten der vertrauenden Seite Vertrauensstellung manuell erstellen. 
1. Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  Klicken Sie unter **Aktionen**, klicken Sie auf **Partei Vertrauensstellung der vertrauenden Seite hinzufügen**.  
![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust1.PNG)   

3.  Auf der **Willkommen** Seite **nicht als eine Ansprüche unterstützende** , und klicken Sie auf **starten**.  
![vertrauende Seite](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon1.PNG) 
  
4.  Auf der **Anzeigename angeben** geben einen Namen im **Anzeigenamen**unter **Anmerkungen zu dieser** Geben Sie eine Beschreibung für diese Vertrauensstellung der vertrauenden Seite, und klicken Sie dann auf **weiter** .  
![vertrauende Seite](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon2.PNG)

5. Geben Sie auf der Seite **Konfigurieren von Bezeichnern** einen oder mehrere Bezeichner für diese vertrauende Seite an, klicken Sie auf **Hinzufügen**, um diese der Liste hinzufügen, und klicken Sie dann auf **Weiter**.  
![vertrauende Seite](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon3.PNG)

6.  Auf der **Zugriffssteuerungsrichtlinien wählen** wählen Sie eine Richtlinie, und klicken Sie auf **Weiter**.  Weitere Informationen zu Access Control-Richtlinien, finden Sie unter [Zugriffssteuerungsrichtlinien in AD FS](Access-Control-Policies-in-AD-FS.md). 
![vertrauende Seite](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon4.PNG)

7. Überprüfen Sie auf der Seite **Bereit zum Hinzufügen der Vertrauensstellung** die Einstellungen, und klicken Sie dann auf **Weiter**, um die Informationen zur Vertrauensstellung der vertrauenden Seite zu speichern.  
   ![vertrauende Seite](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon5.PNG) 

8. Klicken Sie auf der Seite **Fertig stellen** auf **Schließen**. Dadurch wird automatisch das Dialogfeld **Anspruchsregeln bearbeiten** angezeigt.  
![vertrauende Seite](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon6.PNG)  
  
## <a name="see-also"></a>Siehe auch  
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md) 
