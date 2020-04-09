---
ms.assetid: 7b7ae389-5032-44f7-9c0a-94398c3e4d88
title: Erstellen einer Ansprüche nicht unterstützenden Vertrauensstellung der vertrauenden Seite
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: c6886145e910b76edbe99549266d651cdd7c3edf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816923"
---
# <a name="create-a-non-claims-aware-relying-party-trust"></a>Erstellen einer Ansprüche nicht unterstützenden Vertrauensstellung der vertrauenden Seite


Im\-Snap-in "AD FS-Verwaltung" in werden nicht\-Ansprüche\-die Vertrauens Stellungen der vertrauenden Seite sind Objekte, die erstellt werden, um die Vertrauensstellung zwischen dem Verbund Dienst und einer einzelnen Web\-basierten Anwendung darzustellen, die nicht von Ansprüchen\-fähig ist und auf die über den webanwendungsproxy zugegriffen wird  
  
Ein nicht\-Ansprüche\-die Vertrauensstellung der vertrauenden Seite ist eine Vertrauensstellung der vertrauenden Seite, die aus bezeichnerwerten, Namen und Regeln zur Authentifizierung und Autorisierung besteht, wenn auf die Vertrauensstellung der vertrauenden Seite über den webanwendungsproxy Diese auf Web\-basierenden Anwendungen, die sich nicht auf Ansprüche stützen, d. h. diese integrierten Windows-Authentifizierungs\-basierten Anwendungen, können Autorisierungs Regeln aufweisen, die den Zugriff erzwingen, der auf Ansprüchen basiert, wenn der Zugriff auf das Unternehmensnetzwerk über den webanwendungsproxy erfolgt.  
  
Führen Sie das folgende Verfahren aus, um eine neue, nicht\-Ansprüche\-\-AD FS die Vertrauensstellung der vertrauenden Seite in der Vertrauensstellung der vertrauenden Seite hinzuzufügen.  
  
Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
## <a name="to-create-a-non-claims-aware-relying-party-trust-manually"></a>So erstellen Sie eine nicht Ansprüche unterstützende Vertrauensstellung der vertrauenden Seite manuell 
1. Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  
  
2.  Klicken Sie unter **Aktionen**auf Vertrauensstellung der **vertrauenden Seite hinzufügen**.  
![der vertrauenden Seite](media/Create-a-Relying-Party-Trust/addtrust1.PNG)   

3.  Wählen Sie auf der Seite **Willkommen** die Option **nicht Anspruchs** fähig aus, und klicken Sie auf **starten**.  
![der vertrauenden Seite](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon1.PNG) 
  
4.  Geben Sie auf der Seite **Anzeige Name angeben** einen Namen in das Feld **Anzeige Name**ein, geben Sie unter **Hinweise** eine Beschreibung für diese Vertrauensstellung der vertrauenden Seite ein, und klicken Sie dann auf **weiter**.  
![der vertrauenden Seite](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon2.PNG)

5. Geben Sie auf der Seite **Konfigurieren von Bezeichnern** einen oder mehrere Bezeichner für diese vertrauende Seite an, klicken Sie auf **Hinzufügen**, um diese der Liste hinzufügen, und klicken Sie dann auf **Weiter**.  
![der vertrauenden Seite](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon3.PNG)

6.  Wählen Sie unter **Access Control Richtlinie auswählen** eine Richtlinie aus, und klicken Sie auf **weiter**.  Weitere Informationen zu Access Control Richtlinien finden Sie unter [Access Control Policies in AD FS](Access-Control-Policies-in-AD-FS.md). 
![der vertrauenden Seite](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon4.PNG)

7. Überprüfen Sie auf der Seite **Bereit zum Hinzufügen der Vertrauensstellung** die Einstellungen, und klicken Sie dann auf **Weiter**, um die Informationen zur Vertrauensstellung der vertrauenden Seite zu speichern.  
   ![der vertrauenden Seite](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon5.PNG) 

8. Klicken Sie auf der Seite **Fertig stellen** auf **Schließen**. Dadurch wird automatisch das Dialogfeld **Anspruchsregeln bearbeiten** angezeigt.  
![der vertrauenden Seite](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon6.PNG)  
  
## <a name="see-also"></a>Weitere Informationen  
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md) 
