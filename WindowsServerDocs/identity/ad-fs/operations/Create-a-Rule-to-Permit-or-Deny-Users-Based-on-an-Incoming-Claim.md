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
ms.openlocfilehash: d057c943b9c14b74b44472d446625b60f5ad9d22
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70865960"
---
# <a name="create-a-rule-to-permit-or-deny-users-based-on-an-incoming-claim"></a>Erstellen einer Regel, mit der Benutzer anhand eines eingehenden Anspruchs zugelassen oder abgelehnt werden 


In Windows Server 2016 können Sie eine **Access Control Richtlinie** verwenden, um eine Regel zu erstellen, mit der Benutzer basierend auf einem eingehenden Anspruch zugelassen oder verweigert werden.  In Windows Server 2012 R2 können Sie mithilfe der Regel Vorlage " **Benutzer auf Basis eines eingehenden Anspruchs zulassen oder verweigern** " in Active Directory-Verbunddienste (AD FS) \(AD FS\)eine Autorisierungs Regel erstellen, die den Benutzer Zugriff auf das vertrauende Seite basierend auf dem Typ und Wert eines eingehenden Anspruchs. 

So können Sie z. b. eine Regel erstellen, die nur Benutzern mit einem Gruppen Anspruch mit dem Wert "Domänen Administratoren" den Zugriff auf die vertrauende Seite gestattet. Wenn Sie allen Benutzern den Zugriff auf die vertrauende Seite gestatten möchten, verwenden Sie die Regel Vorlage " **alle Access Control zulassen** " oder " **alle Benutzer zulassen** ", abhängig von Ihrer Version von Windows Server. Benutzern, denen der Zugriff auf die vertrauende Seite über den Verbunddienst erlaubt wird, kann der Dienst durch die vertrauende Seite dennoch verweigert werden.  
  
Mithilfe des folgenden Verfahrens können Sie eine Anspruchs Regel mit dem Snap\--in "AD FS-Verwaltung" erstellen.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).  

## <a name="to-create-a-rule-to-permit-users-based-on-an-incoming-claim-on-windows-server-2016"></a>So erstellen Sie eine Regel zum Zulassen von Benutzern basierend auf einem eingehenden Anspruch auf Windows Server 2016
 
1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  
  
2.  Klicken Sie in der Konsolen Struktur unter **AD FS**auf **Access Control Richtlinien**. 
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny3.PNG)

3. Klicken Sie mit der rechten Maustaste, und wählen Sie **Access Control Richtlinie hinzufügen**
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny4.PNG)

4. Geben Sie im Feld Name einen Namen für die Richtlinie ein, eine Beschreibung, und klicken Sie auf **Hinzufügen**.
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny5.PNG)

5. Aktivieren Sie im **Regel-Editor**unter "Benutzer" einen Eincheck Vorgang **mit bestimmten Ansprüchen in der Anforderung** , und klicken Sie unten auf den **unterstrichenen** Bereich.
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny6.PNG)

6. Klicken Sie auf dem Bildschirm **Ansprüche auswählen** auf das Optionsfeld **Ansprüche** , wählen Sie den **Anspruchstyp**, den **Operator**und den **Anspruchs Wert** aus, und klicken Sie dann auf **OK**.
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny7.PNG)

7.  Klicken Sie im **Regel-Editor** auf **OK**.  Klicken Sie auf dem Bildschirm **Access Control Richtlinie hinzufügen** auf **OK**.

8. Klicken Sie in der Konsolen Struktur der **AD FS Verwaltung** unter **AD FS**auf Vertrauens Stellungen der vertrauenden **Seite**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)

9.  Klicken Sie mit der rechten Maustaste auf die Vertrauensstellung der **vertrauenden Seite** , die Sie zulassen möchten, und wählen Sie **Access Control Richtlinie bearbeiten**aus.  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

10. Wählen Sie in der Zugriffs Steuerungs Richtlinie ihre Richtlinie aus, **und klicken Sie dann auf über** nehmen und **OK**.
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny8.PNG)

## <a name="to-create-a-rule-to-deny-users-based-on-an-incoming-claim-on-windows-server-2016"></a>So erstellen Sie eine Regel zum Verweigern von Benutzern auf der Grundlage eines eingehenden Anspruchs auf Windows Server 2016
 
1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  
  
2.  Klicken Sie in der Konsolen Struktur unter **AD FS**auf **Access Control Richtlinien**. 
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny3.PNG)

3. Klicken Sie mit der rechten Maustaste, und wählen Sie **Access Control Richtlinie hinzufügen**
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny4.PNG)

4. Geben Sie im Feld Name einen Namen für die Richtlinie ein, eine Beschreibung, und klicken Sie auf **Hinzufügen**.
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny9.PNG)

5. Stellen Sie im **Regel-Editor**sicher, dass alle Benutzer ausgewählt sind, und klicken Sie unter mit der **Ausnahme** , dass Sie einen Eincheck Vorgang **mit bestimmten Ansprüchen in der Anforderung durch** führen, und klicken Sie dann **unten auf**
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny10.PNG)

6. Klicken Sie auf dem Bildschirm **Ansprüche auswählen** auf das Optionsfeld **Ansprüche** , wählen Sie den **Anspruchstyp**, den **Operator**und den **Anspruchs Wert** aus, und klicken Sie dann auf **OK**.
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny11.PNG)

7.  Klicken Sie im **Regel-Editor** auf **OK**.  Klicken Sie auf dem Bildschirm **Access Control Richtlinie hinzufügen** auf **OK**.

8. Klicken Sie in der Konsolen Struktur der **AD FS Verwaltung** unter **AD FS**auf Vertrauens Stellungen der vertrauenden **Seite**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)

9.  Klicken Sie mit der rechten Maustaste auf die Vertrauensstellung der **vertrauenden Seite** , die Sie zulassen möchten, und wählen Sie **Access Control Richtlinie bearbeiten**aus.  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

10. Wählen Sie in der Zugriffs Steuerungs Richtlinie ihre Richtlinie aus, **und klicken Sie dann auf über** nehmen und **OK**.
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny12.PNG)

  
## <a name="to-create-a-rule-to-permit-or-deny-users-based-on-an-incoming-claim-on-windows-server-2012-r2"></a>So erstellen Sie eine Regel zum Zulassen oder Verweigern von Benutzern basierend auf einem eingehenden Anspruch auf Windows Server 2012 R2
  
1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.    
  
2.  Klicken Sie in der Konsolen Struktur **unter\\AD FS Vertrauens\\Stellungen Vertrauens Stellungen der vertrauenden Seite**auf eine bestimmte Vertrauensstellung in der Liste, in der Sie diese Regel erstellen möchten.  
  
3.  Klicken\-Sie mit der rechten Maustaste auf die ausgewählte Vertrauensstellung und dann auf **Anspruchs Regeln bearbeiten**.  
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)   

4.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** auf die Registerkarte Ausstellungs **Autorisierungs Regeln** oder auf der Register \(Karte **Delegierungs Autorisierungs Regeln** basierend auf der\)gewünschten Autorisierungs Regel, und klicken Sie dann auf **Regel hinzufügen.** um den **Assistenten zum Hinzufügen von Autorisierungs Anspruchs Regeln**zu starten.  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)

5.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die **Option Benutzer basierend auf einem eingehenden Anspruch zulassen oder verweigern** aus der Liste aus, und klicken Sie dann auf **weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny1.PNG)

6.  Geben Sie auf der Seite **Regel konfigurieren** unter **Anspruchs Regel Name** den anzeigen Amen für diese Regel ein, wählen Sie unter eingehender **Anspruchstyp** einen Anspruchstyp in der Liste aus, und geben Sie unter **eingehender Anspruchs Wert** einen Wert ein, oder klicken Sie auf Durchsuchen \(, wenn der Wert verfügbar\) ist, wählen Sie einen Wert aus, und wählen Sie dann je nach den Anforderungen Ihrer Organisation eine der folgenden Optionen aus:  
  
    -   **Benutzern mit diesem eingehenden Anspruch Zugriff gewähren**  
  
    -   **Benutzern mit diesem eingehenden Anspruch Zugriff verweigern**  
![Regel erstellen](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny2.PNG)  
7.  Klicken Sie auf **Fertig stellen**.  
  
8.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** auf **OK** , um die Regel zu speichern.  

## <a name="additional-references"></a>Weitere Verweise 
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  
 
[Prüfliste: Erstellen von Anspruchsregeln für eine Vertrauensstellung der vertrauenden Seite](https://technet.microsoft.com/library/ee913578.aspx)  
  
[Wann sollte eine Autorisierungs Anspruchs Regel verwendet werden?](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
