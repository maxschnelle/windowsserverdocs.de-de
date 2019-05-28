---
ms.assetid: 8c179884-f0d9-4c7a-973d-820119cf3c38
title: Erstellen einer Regel zum Zulassen aller Benutzer
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: abb00e14dd0b3ce7b06efba816fbd7452e7bf0f1
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189413"
---
# <a name="create-a-rule-to-permit-all-users"></a>Erstellen einer Regel zum Zulassen aller Benutzer

In Windows Server 2016 können Sie eine **Access Control-Richtlinie** zum Erstellen einer Regel, die alle Benutzer Zugriff auf eine relying Party erhalten wird.  In Windows Server 2012 R2 mit der **alle Benutzer zulassen** Regelvorlage in Active Directory-Verbunddienste \(AD FS\), können Sie eine Autorisierungsregel, die allen Benutzern Zugriff auf die vertrauende Seite gewähren wird erstellen die Partei. 

Sie können mithilfe zusätzliche Autorisierungsregeln verwenden, um den Zugriff weiter einzuschränken. Benutzern, denen der Zugriff auf die vertrauende Seite über den Verbunddienst erlaubt wird, kann der Dienst durch die vertrauende Seite dennoch verweigert werden.  
  
Sie können die folgenden Verfahren verwenden, erstellen Sie eine Anspruchsregel mit der AD FS-Verwaltungs-Snap\-in.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477). 

## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2016"></a>Zum Erstellen einer Regel zum Zulassen von allen Benutzern in Windows Server 2016

1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten**. 
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall1.PNG)

3.  Mit der rechten Maustaste die **Vertrauensstellung der vertrauenden Seite** , die Sie verwenden möchten, lassen Sie den Zugriff auf, und wählen Sie **Access-Control-Richtlinie bearbeiten**.  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

4. Auf den Zugriff steuern Sie die Richtlinie wählen **alle zulassen** , und klicken Sie dann auf **übernehmen** und **Ok**.
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall3.PNG)
  
## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2012-r2"></a>Zum Erstellen einer Regel zum Zulassen von allen Benutzern in Windows Server 2012 R2 
  
1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **AD FS\\Vertrauensstellungen\\Vertrauensstellungen für vertrauende Seiten**, klicken Sie auf eine bestimmte Vertrauensstellung in der Liste, die zum Erstellen dieser Regel werden sollen.  

3.  Rechts\-klicken Sie auf der ausgewählten Vertrauensstellung, und klicken Sie dann auf **Edit Claim Rules**.  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall4.PNG)  

4.  In der **Edit Claim Rules** Dialogfeld klicken Sie auf der **Ausstellungsautorisierungsregeln** Registerkarte oder die **Delegationsautorisierungsregeln** Registerkarte \(basierend auf den Typ des Autorisierungsregel, die Sie benötigen\), und klicken Sie dann auf **Regel hinzufügen** zum Starten der **Autorisierung Anspruch Assistenten zum Hinzufügen von**.  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)  
5.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **alle Benutzer zulassen** aus der Liste aus, und klicken Sie dann auf **Weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall6.PNG)    
6.  Auf der **Regel konfigurieren** auf **Fertig stellen**.  
  
7.  In der **Edit Claim Rules** Dialogfeld klicken Sie auf **OK** um die Regel zu speichern.  

## <a name="additional-references"></a>Weitere Verweise 
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  
 
[Prüfliste: Erstellen von Anspruchsregeln für eine Vertrauensstellung der vertrauenden Seite](https://technet.microsoft.com/library/ee913578.aspx)  
  
[Wenn Use an Authorization Claim Rule](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
