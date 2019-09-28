---
ms.assetid: 7b7ae389-5032-44f7-9c0a-94398c3e4d88
title: Erstellen einer Ansprüche nicht unterstützenden Vertrauensstellung der vertrauenden Seite
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b0ea877170a07db6abe9ac82e72d1722600ec933
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358113"
---
# <a name="create-a-non-claims-aware-relying-party-trust"></a>Erstellen einer Ansprüche nicht unterstützenden Vertrauensstellung der vertrauenden Seite


Im AD FS Management-Snap @ no__t-0in sind nicht @ no__t-1claims @ no__t-2aware-Vertrauens Stellungen der vertrauenden Seite Objekte, die erstellt werden, um die Vertrauensstellung zwischen dem Verbund Dienst und einer einzelnen Web @ no__t-3based-Anwendung darzustellen, die keine Ansprüche @ no__t-4aware hat und die der Zugriff erfolgt über den webanwendungsproxy.  
  
Eine Non @ no__t-0claims @ no__t-1aware-Vertrauensstellung der vertrauenden Seite ist eine Vertrauensstellung der vertrauenden Seite, die aus bezeichnerwerten, Namen und Regeln für die Authentifizierung und Autorisierung besteht, wenn auf die Vertrauensstellung der vertrauenden Seite über den Webanwendung Diese auf Web @ no__t basierenden Anwendungen, die sich nicht auf Ansprüche stützen, d. h. diese integrierten Windows-Authentifizierung @ no__t-1based-Anwendungen, können Autorisierungs Regeln aufweisen, die den Zugriff erzwingen, der auf Ansprüchen basiert, wenn der Zugriff außerhalb des Unternehmensnetzwerk über den webanwendungsproxy.  
  
Führen Sie das folgende Verfahren aus, um eine neue nicht-@ no__t-0claims @ no__t-1aware-Vertrauensstellung AD FS der vertrauenden Seite hinzuzufügen.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
## <a name="to-create-a-non-claims-aware-relying-party-trust-manually"></a>So erstellen Sie eine nicht Ansprüche unterstützende Vertrauensstellung der vertrauenden Seite manuell 
1. Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  
  
2.  Klicken Sie unter **Aktionen**auf Vertrauensstellung der **vertrauenden Seite hinzufügen**.  
![vertrauende Seite @ no__t-1   

3.  Wählen Sie auf der Seite **Willkommen** die Option **nicht Anspruchs** fähig aus, und klicken Sie auf **starten**.  
![vertrauende Seite @ no__t-1 
  
4.  Geben Sie auf der Seite **Anzeige Name angeben** einen Namen in das Feld **Anzeige Name**ein, geben Sie unter **Hinweise** eine Beschreibung für diese Vertrauensstellung der vertrauenden Seite ein, und klicken Sie dann auf **weiter**.  
![vertrauende Seite @ no__t-1

5. Geben Sie auf der Seite **Konfigurieren von Bezeichnern** einen oder mehrere Bezeichner für diese vertrauende Seite an, klicken Sie auf **Hinzufügen**, um diese der Liste hinzufügen, und klicken Sie dann auf **Weiter**.  
![vertrauende Seite @ no__t-1

6.  Wählen Sie unter **Access Control Richtlinie auswählen** eine Richtlinie aus, und klicken Sie auf **weiter**.  Weitere Informationen zu Access Control Richtlinien finden Sie unter [Access Control Policies in AD FS](Access-Control-Policies-in-AD-FS.md). 
![vertrauende Seite @ no__t-1

7. Überprüfen Sie auf der Seite **Bereit zum Hinzufügen der Vertrauensstellung** die Einstellungen, und klicken Sie dann auf **Weiter**, um die Informationen zur Vertrauensstellung der vertrauenden Seite zu speichern.  
   ![vertrauende Seite @ no__t-1 

8. Klicken Sie auf der Seite **Fertig stellen** auf **Schließen**. Dadurch wird automatisch das Dialogfeld **Anspruchsregeln bearbeiten** angezeigt.  
![vertrauende Seite @ no__t-1  
  
## <a name="see-also"></a>Siehe auch  
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md) 
