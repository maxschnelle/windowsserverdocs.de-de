---
ms.assetid: 8c179884-f0d9-4c7a-973d-820119cf3c38
title: Erstellen einer Regel zum Zulassen aller Benutzer
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: de85af27e699242977054420178dd3c424b2ddb3
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-rule-to-permit-all-users"></a>Erstellen einer Regel zum Zulassen aller Benutzer

>Gilt für: Windows Server 2016, Windows Server2012 R2

In Windows Server2016 können Sie mithilfe einer **Zugriffssteuerungsrichtlinie** zum Erstellen einer Regel, die allen Benutzern Zugriff auf eine vertrauende Seite ermöglichen wird.  In Windows Server2012 R2 mithilfe der **alle Benutzer zulassen** Regelvorlage in Active Directory Federation Services \(AD FS\), erstellen Sie eine Autorisierungsregel, die allen Benutzern den Zugriff auf die vertrauende Seite erhalten. 

Zusätzliche Autorisierungsregeln können Sie den Zugriff weiter einschränken. Benutzer, die die vertrauende Seite vom Verbunddienst zugreifen können Dienst dennoch durch die vertrauende Seite verweigert werden.  
  
Die folgenden Verfahren können Sie um eine Anspruchsregel mit AD FS-Verwaltungs-Snap-In erstellen.  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477). 

## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2016"></a>Zum Erstellen einer Regel zum Zulassen aller Benutzer in Windows Server2016

1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten **. 
![Erstellen der Regel](media/Create-a-Rule-to-Permit-All-Users/permitall1.PNG)

3.  Mit der rechten Maustaste die **Vertrauensstellung der vertrauenden Seite**, die Sie verwenden möchten, lassen Sie den Zugriff auf und wählen Sie **Zugriffssteuerungsrichtlinie bearbeiten **.  
![Erstellen der Regel](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

4. Auf den Zugriff steuern, wählen Sie die Richtlinie **zulassen "Jeder"**, und klicken Sie dann auf **übernehmen** und **Ok **.
![Erstellen der Regel](media/Create-a-Rule-to-Permit-All-Users/permitall3.PNG)
  
## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2012-r2"></a>Zum Erstellen einer Regel zum Zulassen aller Benutzer in Windows Server2012 R2 
  
1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD FS\\Trust Relationships\\Relying Vertrauensstellungen**, klicken Sie auf eine bestimmte Vertrauensstellung in der Liste, in denen Sie diese Regel erstellen möchten.  

3.  Mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Anspruchsregeln bearbeiten **.  
![Erstellen der Regel](media/Create-a-Rule-to-Permit-All-Users/permitall4.PNG)  

4.  In der **Anspruchsregeln bearbeiten** im Dialogfeld klicken Sie auf die **Ausstellungsautorisierungsregeln** Registerkarte oder die **Delegationsautorisierungsregeln** Registerkarte \ (basierend auf dem Typ der Autorisierungsregel Sie Require\), und klicken Sie dann auf **Regel hinzufügen** zum Starten der **Autorisierung Anspruch Assistenten zum Hinzufügen **.  
![Erstellen der Regel](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)  
5.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **alle Benutzer zulassen** aus der Liste, und klicken Sie dann auf **Weiter **.  
![Erstellen der Regel](media/Create-a-Rule-to-Permit-All-Users/permitall6.PNG)    
6.  Auf der **Regel konfigurieren** auf **Fertig stellen **.  
  
7.  In der **Anspruchsregeln bearbeiten** Dialogfeld, klicken Sie auf **OK** um die Regel zu speichern.  

## <a name="additional-references"></a>Weitere Verweise 
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  
 
[Prüfliste: Erstellen von Anspruchsregeln für eine Vertrauensstellung der vertrauenden Seite](https://technet.microsoft.com/library/ee913578.aspx)  
  
[Wann sollte eine Autorisierungsanspruchsregel verwendet](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Die Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Die Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
