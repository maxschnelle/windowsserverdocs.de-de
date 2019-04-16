---
ms.assetid: 0039fbbb-b981-4526-a550-f3456ff27635
title: Erstellen einer Regel zum Transformieren eines eingehenden Anspruchs
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3745a0ab9d313223c611e58864dd6b4d747f0624
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="create-a-rule-to-send-an-ad-fs-1x-compatible-claim"></a>Erstellen einer Regel zum Senden eines AD FS 1.x-kompatiblen Anspruchs

>Gilt für: Windows Server 2016, Windows Server2012 R2


In Situationen, in denen verwenden Sie Active Directory Federation Services \(AD FS\) ausstellen Ansprüche, die von Verbundservern unter AD FS 1.0 empfangen werden \ (Windows Server 2003 R2\) oder AD FS 1.1 \ (Windows Server2008 oder Windows Server2008 R2\), müssen Sie Folgendes tun:  
  
-   Erstellen Sie eine Regel, die ein Anspruch ID mit einem Format UPN, E-Mail oder allgemeinen Namen gesendet wird.  
  
-   Alle anderen Ansprüche, die gesendet werden, müssen eine der folgenden Anspruchstypen verfügen:  
  
    -   AD FS 1. *x* E-Mail-Adresse  
  
    -   AD FS 1. *x* UPN  
  
    -   Allgemeiner Name  
  
    -   Gruppe  
  
    -   Alle anderen Anspruchstyp, der mit https://schemas.xmlsoap.org/claims/, z.B. https://schemas.xmlsoap.org/claims/EmployeeID  
  
Je nach den Anforderungen Ihrer Organisation anhand eines der folgenden Verfahren erstellen Sie ein AD FS 1.. *x* kompatibel NameID Anspruch:  
  
-   Erstellen diese Regel zum Problem an AD FS 1.x Name-ID Anspruch mit dem **weiterleiten oder Filtern einer eingehenden Anspruchs-Vorlage**  
  
-   Erstellen diese Regel zum Problem an AD FS 1.x Name-ID Anspruch mit dem **eine Regelvorlage eingehenden Anspruch transformieren **. Sie können diese Regelvorlage in Situationen verwenden, in denen Sie den vorhandenen Anspruchstyp in einen neuen Anspruchstyp zu ändern, die mit AD FS 1. funktioniert möchten. *X* Ansprüche.  
  
> [!NOTE]  
> Für diese Regel wie erwartet funktioniert, stellen Sie sicher, dass die Vertrauensstellung der vertrauenden Seite oder der Anspruchsanbieter-Vertrauensstellung, in dem diese Regel erstellen konfiguriert wurde mithilfe der **AD FS 1.0- und 1.1-Profil **. 




## <a name="to-create-a-rule-to-issue-an-ad-fs-1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-a-relying-party-trust-in-windows-server-2016"></a>Erstellen Sie eine Regel zum Ausstellen von einem AD FS 1. *x* Name-ID Anspruch weiterleiten oder Filtern einer Regelvorlage eingehenden Anspruch auf eine der vertrauenden Seite Vertrauensstellung in Windows Server2016 

1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten **. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  Mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Anspruch Ausstellungsrichtlinie bearbeiten **.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  In der **Anspruch Ausstellungsrichtlinie bearbeiten** Dialogfeld unter **Ausstellungstransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **weiterleiten oder Filtern eines eingehenden Anspruchs** aus der Liste, und klicken Sie dann auf **Weiter **.  
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  Auf der **Regel konfigurieren** geben einen Name der Anspruchsregel.  
  
7.  In **eingehender Anspruchstyp**Option **Name-ID** in der Liste.  
  
8.  In **eingehenden namensbezeichnerformat**, wählen Sie eine der folgenden AD FS 1. *x*\-compatible Anspruch Formate aus der Liste:  
  
    -   **UPN**  
  
    -   **E\-Mail**  
  
    -   **Allgemeiner Name**  
  
9. Wählen Sie eine der folgenden Optionen, je nach den Anforderungen Ihrer Organisation:  
  
    -   **Alle Anspruchswerte weiterleiten**  
  
    -   **Nur einen bestimmten Anspruchswert weiterleiten**  
  
    -   **Nur Anspruchswerte weiterleiten Sie, die einem bestimmten E-Mail-Suffixwert entsprechen**  
  
    -   **Nur Anspruchswerte weiterleiten Sie, die mit einem bestimmten Wert starten**  
![Erstellen der Regel](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs3.PNG)   

10. Klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  

  
## <a name="to-create-a-rule-to-issue-an-ad-fs-1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-a-claims-provider-trust-in-windows-server-2016"></a>Erstellen Sie eine Regel zum Ausstellen von einem AD FS 1. *x* Name-ID Anspruch weiterleiten oder Filtern einer eingehenden Anspruchs-Vorlage auf einer Anspruchsanbieter-Vertrauensstellung in Windows Server2016 
  
1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen **. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  Mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Anspruchsregeln bearbeiten **.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  In der **Anspruchsregeln bearbeiten** Dialogfeld unter **Akzeptanztransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **weiterleiten oder Filtern eines eingehenden Anspruchs** aus der Liste, und klicken Sie dann auf **Weiter **.  
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  Auf der **Regel konfigurieren** geben einen Name der Anspruchsregel.  
  
7.  In **eingehender Anspruchstyp**Option **Name-ID** in der Liste.  
  
8.  In **eingehenden namensbezeichnerformat**, wählen Sie eine der folgenden AD FS 1. *x*\-compatible Anspruch Formate aus der Liste:  
  
    -   **UPN**  
  
    -   **E\-Mail**  
  
    -   **Allgemeiner Name**  
  
9. Wählen Sie eine der folgenden Optionen, je nach den Anforderungen Ihrer Organisation:  
  
    -   **Alle Anspruchswerte weiterleiten**  
  
    -   **Nur einen bestimmten Anspruchswert weiterleiten**  
  
    -   **Nur Anspruchswerte weiterleiten Sie, die einem bestimmten E-Mail-Suffixwert entsprechen**  
  
    -   **Nur Anspruchswerte weiterleiten Sie, die mit einem bestimmten Wert starten**  
![Erstellen der Regel](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs3.PNG)   

10. Klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  

  

## <a name="to-create-a-rule-to-transform-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>Zum Erstellen einer Regel zum Transformieren eines eingehenden Anspruchs auf eine der vertrauenden Seite Vertrauensstellung in Windows Server2016 

1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten **. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  Mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Anspruch Ausstellungsrichtlinie bearbeiten **.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  In der **Anspruch Ausstellungsrichtlinie bearbeiten** Dialogfeld unter **Ausstellungstransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **Transformieren eines eingehenden Anspruchs** aus der Liste, und klicken Sie dann auf **Weiter **.  
![Erstellen der Regel](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)      

6.  Auf der **Regel konfigurieren** geben einen Name der Anspruchsregel.  
  
7.  In **eingehender Anspruchstyp**, wählen Sie den Typ des eingehenden Anspruchs, die Sie in der Liste umwandeln möchten.  
  
8.  In **ausgehenden Anspruchstyp**Option **Name-ID** in der Liste.  
  
9. In **ausgehende namensbezeichnerformat**, wählen Sie eine der folgenden AD FS 1. *x*\-compatible Anspruch Formate aus der Liste:  
  
    -   **UPN**  
  
    -   **E\-Mail**  
  
    -   **Allgemeiner Name**  
  
10. Wählen Sie eine der folgenden Optionen, je nach den Anforderungen Ihrer Organisation:  
  
    -   **Alle Anspruchswerte weiterleiten**  
  
    -   **Ersetzen Sie einen eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert**  
  
    -   **Ersetzen Sie eingehende E\ E-Mail-Suffixansprüche durch ein neues E\ E-Mail-Suffix**  
![Erstellen der Regel](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs4.PNG)    

11. Klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  

  


## <a name="to-create-a-rule-to-transform-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>Zum Erstellen einer Regel zum Transformieren eines eingehenden Anspruchs auf eine Anspruchsanbieter-Vertrauensstellung in Windows Server2016 
  
1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen **. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  Mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Anspruchsregeln bearbeiten **.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  In der **Anspruchsregeln bearbeiten** Dialogfeld unter **Akzeptanztransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **Transformieren eines eingehenden Anspruchs** aus der Liste, und klicken Sie dann auf **Weiter **.  
![Erstellen der Regel](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)      

6.  Auf der **Regel konfigurieren** geben einen Name der Anspruchsregel.  
  
7.  In **eingehender Anspruchstyp**, wählen Sie den Typ des eingehenden Anspruchs, die Sie in der Liste umwandeln möchten.  
  
8.  In **ausgehenden Anspruchstyp**Option **Name-ID** in der Liste.  
  
9. In **ausgehende namensbezeichnerformat**, wählen Sie eine der folgenden AD FS 1. *x*\-compatible Anspruch Formate aus der Liste:  
  
    -   **UPN**  
  
    -   **E\-Mail**  
  
    -   **Allgemeiner Name**  
  
10. Wählen Sie eine der folgenden Optionen, je nach den Anforderungen Ihrer Organisation:  
  
    -   **Alle Anspruchswerte weiterleiten**  
  
    -   **Ersetzen Sie einen eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert**  
  
    -   **Ersetzen Sie eingehende E\ E-Mail-Suffixansprüche durch ein neues E\ E-Mail-Suffix**  
![Erstellen der Regel](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs4.PNG)    

11. Klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  













  
## <a name="to-create-a-rule-to-issue-an-ad-fs-1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-windows-server-2012-r2"></a>Erstellen Sie eine Regel zum Ausstellen von einem AD FS 1. *x* Name-ID Anspruch weiterleiten oder Filtern einer eingehenden Anspruchs Regelvorlage unter Windows Server2012 R2
  
1.  Klicken Sie im Server-Manager auf **Tools**, und klicken Sie dann auf **AD FS-Verwaltungs **.  
  
2.  In der Konsolenstruktur unter **AD FS\\Trust Beziehungen**, klicken Sie entweder **Anspruchsanbieter-Vertrauensstellungen** oder **Vertrauensstellungen für vertrauende Seiten**, und klicken Sie dann auf eine bestimmte Vertrauensstellung in der Liste, in denen Sie diese Regel erstellen möchten.  
  
3.  Mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Anspruchsregeln bearbeiten **.  
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) 
  
4.  In der **Anspruchsregeln bearbeiten** klicken Sie im Dialogfeld Wählen Sie eine der folgenden Registerkarten, abhängig von der Vertrauensstellung, die Sie bearbeiten und welche Regel legen Sie, diese Regel in erstellen möchten, und klicken Sie dann auf **Regel hinzufügen** des Assistenten zu starten, die diesen Regelsatz zugeordnet ist:  
  
    -   **Akzeptanztransformationsregeln**  
  
    -   **Ausstellungstransformationsregeln**  
  
    -   **Ausstellungsautorisierungsregeln**  
  
    -   **Autorisierungsregeln**  
![Erstellen der Regel](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **weiterleiten oder Filtern eines eingehenden Anspruchs** aus der Liste, und klicken Sie dann auf **Weiter **.  
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule7.PNG)  
  
6.  Auf der **Regel konfigurieren** geben einen Name der Anspruchsregel.  
  
7.  In **eingehender Anspruchstyp**Option **Name-ID** in der Liste.  
  
8.  In **eingehenden namensbezeichnerformat**, wählen Sie eine der folgenden AD FS 1. *x*\-compatible Anspruch Formate aus der Liste:  
  
    -   **UPN**  
  
    -   **E\-Mail**  
  
    -   **Allgemeiner Name**  
  
9. Wählen Sie eine der folgenden Optionen, je nach den Anforderungen Ihrer Organisation:  
  
    -   **Alle Anspruchswerte weiterleiten**  
  
    -   **Nur einen bestimmten Anspruchswert weiterleiten**  
  
    -   **Nur Anspruchswerte weiterleiten Sie, die einem bestimmten E-Mail-Suffixwert entsprechen**  
  
    -   **Nur Anspruchswerte weiterleiten Sie, die mit einem bestimmten Wert starten**  
![Erstellen der Regel](media/\Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs1.PNG)   

10. Klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  

  
## <a name="to-create-a-rule-to-issue-an-ad-fs-1x-name-id-claim-using-the-transform-an-incoming-claim-rule-template-in-windows-server-2012-r2"></a>Erstellen Sie eine Regel zum Ausstellen von einem AD FS 1. *x* Anspruch über der Transformation einer eingehenden Anspruchs-Vorlage in Windows Server2012 R2  
  
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
  
5.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **Transformieren eines eingehenden Anspruchs** aus der Liste, und klicken Sie dann auf **Weiter **.  
![Erstellen der Regel](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform1.PNG)   
  
6.  Auf der **Regel konfigurieren** geben einen Name der Anspruchsregel.  
  
7.  In **eingehender Anspruchstyp**, wählen Sie den Typ des eingehenden Anspruchs, die Sie in der Liste umwandeln möchten.  
  
8.  In **ausgehenden Anspruchstyp**Option **Name-ID** in der Liste.  
  
9. In **ausgehende namensbezeichnerformat**, wählen Sie eine der folgenden AD FS 1. *x*\-compatible Anspruch Formate aus der Liste:  
  
    -   **UPN**  
  
    -   **E\-Mail**  
  
    -   **Allgemeiner Name**  
  
10. Wählen Sie eine der folgenden Optionen, je nach den Anforderungen Ihrer Organisation:  
  
    -   **Alle Anspruchswerte weiterleiten**  
  
    -   **Ersetzen Sie einen eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert**  
  
    -   **Ersetzen Sie eingehende E\ E-Mail-Suffixansprüche durch ein neues E\ E-Mail-Suffix**  
![Erstellen der Regel](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs2.PNG)    

11. Klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  

## <a name="additional-references"></a>Weitere Verweise 
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  
 
[Prüfliste: Erstellen von Anspruchsregeln für eine Vertrauensstellung der vertrauenden Seite](https://technet.microsoft.com/library/ee913578.aspx)  

[Prüfliste: Erstellen von Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung](https://technet.microsoft.com/library/ee913564.aspx)  
  
[Wann sollte eine Autorisierungsanspruchsregel verwendet](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Die Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Die Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
