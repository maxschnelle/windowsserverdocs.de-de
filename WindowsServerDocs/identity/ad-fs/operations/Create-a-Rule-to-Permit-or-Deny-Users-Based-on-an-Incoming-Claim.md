---
ms.assetid: 3d770385-9834-4ebe-b66c-b684e0245971
title: Erstellen einer Regel zum Zulassen oder Verweigern von Benutzern auf eines eingehenden Anspruchs basieren
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: afcbb8c7a08a84eda2a794c9565061d7d61d470b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-rule-to-permit-or-deny-users-based-on-an-incoming-claim"></a>Erstellen einer Regel zum Zulassen oder Verweigern von Benutzern auf eines eingehenden Anspruchs basieren 

>Gilt für: Windows Server 2016, Windows Server2012 R2

In Windows Server2016 können Sie mithilfe einer **Zugriffssteuerungsrichtlinie** zum Erstellen einer Regel, die von zulässt, Benutzer auf Basis eines eingehenden Anspruchs verweigern.  In Windows Server2012 R2 mithilfe der **zulassen oder verweigern Benutzer auf Basis eines eingehenden Anspruchs** Regelvorlage in Active Directory Federation Services \(AD FS\), können Sie eine Autorisierungsregel, die gewähren oder Verweigern von Zugriff des Benutzers auf die vertrauende Seite basierend auf dem Typ und Wert eines eingehenden Anspruchs erstellen. 

Z.B. können dies Sie eine Regel erstellen, die nur Benutzer zulässt, die einer Anspruch mit einem Wert von Domänenadministratoren Gruppe auf die vertrauende Seite zugreifen. Wenn Sie möchten, dass alle Benutzer für den Zugriff auf die vertrauende Seite verwenden die **zulassen "Jeder"** Zugriffssteuerungsrichtlinie oder die **alle Benutzer zulassen** Regelvorlage abhängig von Ihrer Version von Windows Server. Benutzer, die die vertrauende Seite vom Verbunddienst zugreifen können Dienst dennoch durch die vertrauende Seite verweigert werden.  
  
Das folgende Verfahren können zum Erstellen einer Anspruchsregel mit AD FS-Verwaltungs-Snap-In.  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).  

## <a name="to-create-a-rule-to-permit-users-based-on-an-incoming-claim-on-windows-server-2016"></a>Zum Erstellen einer Regel zum Zulassen der Benutzer auf Basis eines eingehenden Anspruchs unter Windows Server2016
 
1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Zugriffsrichtlinien **. 
![Erstellen der Regel](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny3.PNG)

3. Mit der rechten Maustaste, und wählen Sie **Zugriffssteuerungsrichtlinie hinzufügen **.
![Erstellen der Regel](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny4.PNG)

4. Geben Sie im Namenfeld einen Namen für die Richtlinie, eine Beschreibung und auf **hinzufügen **.
![Erstellen der Regel](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny5.PNG)

5. Auf der **Regel-Editor**, unterstellt werden Benutzer, aktivieren Sie das Kontrollkästchen **mit bestimmten Ansprüche in der Anforderung**, und klicken Sie auf den unterstrichenen **bestimmten** unten.
![Erstellen der Regel](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny6.PNG)

6. Auf der **wählen Ansprüche** auf die **Ansprüche** Optionsfeld, wählen Sie die **Anspruchstyp**, die **Operator**, und die **Anspruchswert** klicken Sie dann auf **Ok **.
![Erstellen der Regel](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny7.PNG)

7.  Auf der **Regel-Editor** klicken Sie auf **Ok **.  Auf der **Zugriffssteuerungsrichtlinie hinzufügen** auf **Ok **.

8. In der **AD FS-Verwaltungs** Konsolenstruktur unter **AD FS**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten **. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)

9.  Mit der rechten Maustaste die **Vertrauensstellung der vertrauenden Seite**, die Sie verwenden möchten, lassen Sie den Zugriff auf und wählen Sie **Zugriffssteuerungsrichtlinie bearbeiten **.  
![Erstellen der Regel](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

10. Klicken Sie auf der Zugriffssteuerungsrichtlinie wählen Sie die Richtlinie, und klicken Sie dann auf **übernehmen** und **Ok **.
![Erstellen der Regel](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny8.PNG)

## <a name="to-create-a-rule-to-deny-users-based-on-an-incoming-claim-on-windows-server-2016"></a>Erstellen Sie eine Regel zum Verweigern Benutzer auf Basis eines eingehenden Anspruchs unter Windows Server2016
 
1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Zugriffsrichtlinien **. 
![Erstellen der Regel](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny3.PNG)

3. Mit der rechten Maustaste, und wählen Sie **Zugriffssteuerungsrichtlinie hinzufügen **.
![Erstellen der Regel](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny4.PNG)

4. Geben Sie im Namenfeld einen Namen für die Richtlinie, eine Beschreibung und auf **hinzufügen **.
![Erstellen der Regel](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny9.PNG)

5. Auf der **Regel-Editor**, stellen Sie sicher, dass jeder ausgewählt ist und wählen Sie unter **außer** aktivieren Sie das Kontrollkästchen **mit bestimmten Ansprüche in der Anforderung**, und klicken Sie auf den unterstrichenen **bestimmte** unten.
![Erstellen der Regel](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny10.PNG)

6. Auf der **wählen Ansprüche** auf die **Ansprüche** Optionsfeld, wählen Sie die **Anspruchstyp**, die **Operator**, und die **Anspruchswert** klicken Sie dann auf **Ok **.
![Erstellen der Regel](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny11.PNG)

7.  Auf der **Regel-Editor** klicken Sie auf **Ok **.  Auf der **Zugriffssteuerungsrichtlinie hinzufügen** auf **Ok **.

8. In der **AD FS-Verwaltungs** Konsolenstruktur unter **AD FS**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten **. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)

9.  Mit der rechten Maustaste die **Vertrauensstellung der vertrauenden Seite**, die Sie verwenden möchten, lassen Sie den Zugriff auf und wählen Sie **Zugriffssteuerungsrichtlinie bearbeiten **.  
![Erstellen der Regel](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

10. Klicken Sie auf der Zugriffssteuerungsrichtlinie wählen Sie die Richtlinie, und klicken Sie dann auf **übernehmen** und **Ok **.
![Erstellen der Regel](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny12.PNG)

  
## <a name="to-create-a-rule-to-permit-or-deny-users-based-on-an-incoming-claim-on-windows-server-2012-r2"></a>Erstellen eine Regel zum Zulassen oder Verweigern von Benutzern anhand eines eingehenden Anspruchs auf Windows Server2012 R2
  
1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.    
  
2.  In der Konsolenstruktur unter **AD FS\\Trust Relationships\\Relying Vertrauensstellungen**, klicken Sie auf eine bestimmte Vertrauensstellung in der Liste, in denen Sie diese Regel erstellen möchten.  
  
3.  Mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Anspruchsregeln bearbeiten **.  
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)   

4.  In der **Anspruchsregeln bearbeiten** im Dialogfeld klicken Sie auf die **Ausstellungsautorisierungsregeln** Registerkarte oder die **Delegationsautorisierungsregeln** Registerkarte \ (basierend auf dem Typ der Autorisierungsregel Sie Require\), und klicken Sie dann auf **Regel hinzufügen** zum Starten der **Autorisierung Anspruch Assistenten zum Hinzufügen **.  
![Erstellen der Regel](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)

5.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **zulassen oder verweigern Benutzer auf Basis eines eingehenden Anspruchs** aus der Liste, und klicken Sie dann auf **Weiter **.  
![Erstellen der Regel](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny1.PNG)

6.  Auf der **Regel konfigurieren** Seite **Name der Anspruchsregel** Geben Sie den Namen für diese Regel **eingehender Anspruchstyp** wählen Sie einen Anspruchstyp aus der Liste unter **eingehender Anspruchswert** Geben Sie einen Wert ein, oder klicken Sie auf Durchsuchen \ (sofern Available\) und wählen Sie einen Wert ein, und wählen Sie dann eine der folgenden Optionen, je nach den Anforderungen Ihrer Organisation:  
  
    -   **Benutzer mit diesem eingehenden Anspruch Zugriff gewähren**  
  
    -   **Benutzern mit diesem eingehenden Anspruch Zugriff verweigern**  
![Erstellen der Regel](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny2.PNG)  
7.  Klicken Sie auf **Fertig stellen**.  
  
8.  In der **Anspruchsregeln bearbeiten** Dialogfeld, klicken Sie auf **OK** um die Regel zu speichern.  

## <a name="additional-references"></a>Weitere Verweise 
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  
 
[Prüfliste: Erstellen von Anspruchsregeln für eine Vertrauensstellung der vertrauenden Seite](https://technet.microsoft.com/library/ee913578.aspx)  
  
[Wann sollte eine Autorisierungsanspruchsregel verwendet](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Die Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Die Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
