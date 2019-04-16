---
ms.assetid: 38eb3726-e97b-484e-9926-67e8a046b0c5
title: "Erstellen einer Regel zum Senden von Ansprüchen mit benutzerdefinierter Regel"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f0eef89e651585d48ba87d14bc782efa49087669
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-rule-to-send-claims-using-a-custom-rule"></a>Erstellen einer Regel zum Senden von Ansprüchen mit benutzerdefinierter Regel

>Gilt für: Windows Server 2016, Windows Server2012 R2

Mithilfe der **Senden von Ansprüchen mit benutzerdefinierter Regel** Vorlage in Active Directory-Verbunddienste (AD FS), können Sie benutzerdefinierte Anspruchsregeln für Situationen, in denen eine standardregelvorlage nicht die Anforderungen Ihrer Organisation erfüllt, erstellen. Benutzerdefinierte Anspruchsregeln in der anspruchsregelsprache geschrieben sind, und klicken Sie dann in kopiert werden müssen die **benutzerdefinierte Regel** Textfeld, bevor sie in einem Regelsatz verwendet werden können. Informationen zum Erstellen der Syntax für eine erweiterte Regel finden Sie unter [The Role of the Claim Rule Language](../../ad-fs/technical-reference/The-Role-of-the-Claim-Rule-Language.md).  
  
Das folgende Verfahren können Sie eine Anspruchsregel erstellen Sie mithilfe von AD FS-Verwaltungs-Snap-In.  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer die Mindestanforderung zum Ausführen dieses Verfahrens.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).



## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>Erstellen eine Regel zum Weiterleiten oder Filtern eines eingehenden Anspruchs auf eine der vertrauenden Seite Vertrauensstellung in Windows Server2016 

1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten **. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  Mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Anspruch Ausstellungsrichtlinie bearbeiten **.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  In der **Anspruch Ausstellungsrichtlinie bearbeiten** Dialogfeld unter **Ausstellungstransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **Senden von Ansprüchen mit benutzerdefinierter Regel** aus der Liste, und klicken Sie dann auf **Weiter**.  
![Erstellen der Regel](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom3.PNG)   
  
6.  Auf der **Regel konfigurieren** Seite unter **Name der Anspruchsregel**, geben Sie den Namen für diese Regel. Klicken Sie unter **benutzerdefinierte Regel**, geben oder fügen Sie die Syntax anspruchsregelsprache, die Sie für diese Regel verwenden möchten.  
![Erstellen der Regel](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom4.PNG)     

7.  Klicken Sie auf **Fertig stellen**.  
  
8.  In der **Anspruchsregeln bearbeiten** Dialogfeld, klicken Sie auf **OK** um die Regel zu speichern.   
  
## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>Erstellen eine Regel zum Weiterleiten oder Filtern eines eingehenden Anspruchs auf eine Anspruchsanbieter-Vertrauensstellung in Windows Server2016 
  
1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen **. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  Mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Anspruchsregeln bearbeiten **.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  In der **Anspruchsregeln bearbeiten** Dialogfeld unter **Akzeptanztransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **Senden von Ansprüchen mit benutzerdefinierter Regel** aus der Liste, und klicken Sie dann auf **Weiter**.  
![Erstellen der Regel](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom3.PNG)   
  
6.  Auf der **Regel konfigurieren** Seite unter **Name der Anspruchsregel**, geben Sie den Namen für diese Regel. Klicken Sie unter **benutzerdefinierte Regel**, geben oder fügen Sie die Syntax anspruchsregelsprache, die Sie für diese Regel verwenden möchten.  
![Erstellen der Regel](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom4.PNG)     

7.  Klicken Sie auf **Fertig stellen**.  
  
8.  In der **Anspruchsregeln bearbeiten** Dialogfeld, klicken Sie auf **OK** um die Regel zu speichern.   

















   
  
## <a name="to-create-a-rule-to-send-claims-by-using-a-custom-claim-in-windows-server-2012-r2"></a>Zum Erstellen einer Regel zum Senden von Ansprüchen mit einem benutzerdefinierten Anspruch in Windows Server2012 R2 
  
1.  Klicken Sie im Server-Manager auf **Tools**, und klicken Sie dann auf **AD FS-Verwaltungs **.  
  
2.  In der Konsolenstruktur unter **AD FS\\Trust Beziehungen**, klicken Sie entweder **Anspruchsanbieter-Vertrauensstellungen** oder **Vertrauensstellungen für vertrauende Seiten**, und klicken Sie dann auf eine bestimmte Vertrauensstellung in der Liste, in denen Sie diese Regel erstellen möchten.  
  
3.  Mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Anspruchsregeln bearbeiten **.  
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) 
  
4.  In der **Anspruchsregeln bearbeiten** Dialogfeld, wählen Sie eine der folgenden Registerkarten, die in der Vertrauensstellung abhängig ist, dass Sie bearbeiten und in der Regel legen Sie möchten erstellen diese Regel, und klicken Sie dann auf **Regel hinzufügen** des Assistenten zu starten, die diesen Regelsatz zugeordnet ist:  
  
    -   **Akzeptanztransformationsregeln**  
  
    -   **Ausstellungstransformationsregeln**  
  
    -   **Ausstellungsautorisierungsregeln**  
  
    -   **Autorisierungsregeln**  
![Erstellen der Regel](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)
  
5.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **Senden von Ansprüchen mit benutzerdefinierter Regel** aus der Liste, und klicken Sie dann auf **Weiter**.  
![Erstellen der Regel](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom1.PNG)   
  
6.  Auf der **Regel konfigurieren** Seite unter **Name der Anspruchsregel**, geben Sie den Namen für diese Regel. Klicken Sie unter **benutzerdefinierte Regel**, geben oder fügen Sie die Syntax anspruchsregelsprache, die Sie für diese Regel verwenden möchten.  
![Erstellen der Regel](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom2.PNG)     

7.  Klicken Sie auf **Fertig stellen**.  
  
8.  In der **Anspruchsregeln bearbeiten** Dialogfeld, klicken Sie auf **OK** um die Regel zu speichern.  

## <a name="additional-references"></a>Weitere Verweise 
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  
 
[Prüfliste: Erstellen von Anspruchsregeln für eine Vertrauensstellung der vertrauenden Seite](https://technet.microsoft.com/library/ee913578.aspx)  

[Prüfliste: Erstellen von Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung](https://technet.microsoft.com/library/ee913564.aspx)  
  
[Wann sollte eine Autorisierungsanspruchsregel verwendet](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Die Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Die Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
