---
ms.assetid: 3d770385-9834-4ebe-b66c-b684e0245971
title: Erstellen einer Regel, mit der Benutzer anhand eines eingehenden Anspruchs zugelassen oder abgelehnt werden
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 72fe425b040f83a217a144976265c7754830c91b
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189503"
---
# <a name="create-a-rule-to-permit-or-deny-users-based-on-an-incoming-claim"></a>Erstellen einer Regel, mit der Benutzer anhand eines eingehenden Anspruchs zugelassen oder abgelehnt werden 


In Windows Server 2016 können Sie eine **Access Control-Richtlinie** zum Erstellen einer Regel, die zulassen oder verweigern Benutzer auf Grundlage eines eingehenden Anspruchs.  In Windows Server 2012 R2 mit der **zulassen oder verweigern Sie, dass sich Benutzer anhand eines eingehenden Anspruchs** Regelvorlage in Active Directory-Verbunddienste \(AD FS\), können Sie eine Autorisierungsregel, die gewähren erstellen oder Verweigern Sie den Benutzerzugriff auf die vertrauende Seite basierend auf dem Typ und Wert eines eingehenden Anspruchs. 

Angenommen, können dies Sie zum Erstellen einer Regel, die nur Benutzer, die einen Gruppenanspruch mit dem Wert der Domänen-Admins zulässt, auf die vertrauende Seite haben. Wenn Sie alle Benutzer auf die vertrauende Seite zugreifen kann, verwenden Sie zulassen möchten die **zulassen jeder** Access Control-Richtlinie oder die **alle Benutzer zulassen** Regelvorlage abhängig von Ihrer Version von Windows Server. Benutzern, denen der Zugriff auf die vertrauende Seite über den Verbunddienst erlaubt wird, kann der Dienst durch die vertrauende Seite dennoch verweigert werden.  
  
Sie können das folgende Verfahren zum Erstellen einer Anspruchsregel mit der AD FS-Verwaltungs-Snap\-in.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).  

## <a name="to-create-a-rule-to-permit-users-based-on-an-incoming-claim-on-windows-server-2016"></a>Zum Erstellen einer Regel zum Zulassen der Benutzer auf Grundlage eines eingehenden Anspruchs unter Windows Server 2016
 
1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Zugriffssteuerungsrichtlinien**. 
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny3.PNG)

3. Mit der rechten Maustaste, und wählen Sie **Access-Control-Richtlinie hinzufügen**.
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny4.PNG)

4. Geben Sie im Namenfeld einen Namen für die Richtlinie, eine Beschreibung und klicken Sie auf **hinzufügen**.
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny5.PNG)

5. Auf der **Regeleditor**, unterstellt werden Benutzer, aktivieren Sie das Kontrollkästchen **mit bestimmten Ansprüchen in der Anforderung** , und klicken Sie auf das unterstrichene **bestimmte** am unteren Rand.
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny6.PNG)

6. Auf der **Ansprüche wählen** Bildschirm, klicken Sie auf der **Ansprüche** Optionsfeld, wählen Sie die **Anspruchstyp**, wird die **Operator**, und die  **Anspruchswert** klicken Sie dann auf **Ok**.
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny7.PNG)

7.  Auf der **Regeleditor** klicken Sie auf **Ok**.  Auf der **Access-Control-Richtlinie hinzufügen** auf **Ok**.

8. In der **AD FS-Verwaltung** in der Konsolenstruktur unter **AD FS**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)

9.  Mit der rechten Maustaste die **Vertrauensstellung der vertrauenden Seite** , die Sie verwenden möchten, lassen Sie den Zugriff auf, und wählen Sie **Access-Control-Richtlinie bearbeiten**.  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

10. Klicken Sie auf die Access-Control-Richtlinie wählen Sie Ihre Richtlinie, und klicken Sie dann auf **übernehmen** und **Ok**.
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny8.PNG)

## <a name="to-create-a-rule-to-deny-users-based-on-an-incoming-claim-on-windows-server-2016"></a>Zum Erstellen einer Regel zum Ablehnen der Benutzer auf Grundlage eines eingehenden Anspruchs unter Windows Server 2016
 
1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Zugriffssteuerungsrichtlinien**. 
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny3.PNG)

3. Mit der rechten Maustaste, und wählen Sie **Access-Control-Richtlinie hinzufügen**.
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny4.PNG)

4. Geben Sie im Namenfeld einen Namen für die Richtlinie, eine Beschreibung und klicken Sie auf **hinzufügen**.
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny9.PNG)

5. Auf der **Regeleditor**, stellen Sie sicher, dass alle Benutzer aktiviert ist und wählen Sie unter **außer** aktivieren Sie das Kontrollkästchen **mit bestimmten Ansprüchen in der Anforderung** , und klicken Sie auf das unterstrichene  **bestimmte** am unteren Rand.
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny10.PNG)

6. Auf der **Ansprüche wählen** Bildschirm, klicken Sie auf der **Ansprüche** Optionsfeld, wählen Sie die **Anspruchstyp**, wird die **Operator**, und die  **Anspruchswert** klicken Sie dann auf **Ok**.
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny11.PNG)

7.  Auf der **Regeleditor** klicken Sie auf **Ok**.  Auf der **Access-Control-Richtlinie hinzufügen** auf **Ok**.

8. In der **AD FS-Verwaltung** in der Konsolenstruktur unter **AD FS**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)

9.  Mit der rechten Maustaste die **Vertrauensstellung der vertrauenden Seite** , die Sie verwenden möchten, lassen Sie den Zugriff auf, und wählen Sie **Access-Control-Richtlinie bearbeiten**.  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

10. Klicken Sie auf die Access-Control-Richtlinie wählen Sie Ihre Richtlinie, und klicken Sie dann auf **übernehmen** und **Ok**.
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny12.PNG)

  
## <a name="to-create-a-rule-to-permit-or-deny-users-based-on-an-incoming-claim-on-windows-server-2012-r2"></a>Erstellen Sie eine Regel zum Zulassen oder verweigern Benutzer auf Grundlage eines eingehenden Anspruchs unter Windows Server 2012 R2
  
1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.    
  
2.  In der Konsolenstruktur unter **AD FS\\Vertrauensstellungen\\Vertrauensstellungen für vertrauende Seiten**, klicken Sie auf eine bestimmte Vertrauensstellung in der Liste, die zum Erstellen dieser Regel werden sollen.  
  
3.  Rechts\-klicken Sie auf der ausgewählten Vertrauensstellung, und klicken Sie dann auf **Edit Claim Rules**.  
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)   

4.  In der **Edit Claim Rules** Dialogfeld klicken Sie auf der **Ausstellungsautorisierungsregeln** Registerkarte oder die **Delegationsautorisierungsregeln** Registerkarte \(basierend auf den Typ des Autorisierungsregel, die Sie benötigen\), und klicken Sie dann auf **Regel hinzufügen** zum Starten der **Autorisierung Anspruch Assistenten zum Hinzufügen von**.  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)

5.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **zulassen oder verweigern Sie, dass sich Benutzer anhand eines eingehenden Anspruchs** aus der Liste aus, und klicken Sie dann auf  **Nächste**.  
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny1.PNG)

6.  Auf der **Regel konfigurieren** Seite **anspruchsregelname** Geben Sie den Anzeigenamen für diese Regel in **eingehender Anspruchstyp** wählen Sie einen Anspruchstyp in der Liste unter  **Wert des eingehenden Anspruchs** einen Wert eingeben, oder klicken Sie auf Durchsuchen \(ist es verfügbaren\) und wählen Sie einen Wert ein, und wählen Sie dann eine der folgenden Optionen, je nach den Anforderungen Ihrer Organisation:  
  
    -   **Benutzer mit diesem eingehenden Anspruch Zugriff gewähren**  
  
    -   **Benutzern mit diesem eingehenden Anspruch Zugriff verweigern**  
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny2.PNG)  
7.  Klicken Sie auf **Fertig stellen**.  
  
8.  In der **Edit Claim Rules** Dialogfeld klicken Sie auf **OK** um die Regel zu speichern.  

## <a name="additional-references"></a>Weitere Verweise 
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  
 
[Prüfliste: Erstellen von Anspruchsregeln für eine Vertrauensstellung der vertrauenden Seite](https://technet.microsoft.com/library/ee913578.aspx)  
  
[Wenn Use an Authorization Claim Rule](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
