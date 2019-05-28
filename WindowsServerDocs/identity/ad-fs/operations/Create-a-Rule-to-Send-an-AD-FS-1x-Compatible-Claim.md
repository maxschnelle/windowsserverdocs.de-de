---
ms.assetid: 0039fbbb-b981-4526-a550-f3456ff27635
title: Erstellen einer Regel zum Transformieren eines eingehenden Anspruchs
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c87b76224d1ac5dbe3befc837fad8879d0b9a1ef
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189396"
---
# <a name="create-a-rule-to-send-an-ad-fs-1x-compatible-claim"></a>Erstellen Sie eine Regel zum Senden eines-kompatibler Anspruchs von AD FS 1.x

In Situationen, in dem Sie Active Directory-Verbunddienste verwenden \(AD FS\) für Ansprüche, die von Verbundservern unter AD FS 1.0 empfangen werden, Problem \(Windows Server 2003 R2\) oder AD FS 1.1 \(Windows Server 2008 oder Windows Server 2008 R2\), müssen Sie Folgendes tun:  
  
-   Erstellen Sie eine Regel, die einen namens-ID-Anspruchstyp in einem Format des UPN, E-Mail oder allgemeinen Namen gesendet wird.  
  
-   Alle anderen Ansprüche, die gesendet werden müssen es sich um eine der folgenden Anspruchstypen haben:  
  
    -   AD FS 1. *x* e-Mail-Adresse  
  
    -   AD FS 1.*x* UPN  
  
    -   Allgemeiner Name  
  
    -   Gruppieren  
  
    -   Alle anderen Anspruchstyp, der mit beginnt https://schemas.xmlsoap.org/claims/, z. B. https://schemas.xmlsoap.org/claims/EmployeeID  
  
Je nach den Anforderungen Ihrer Organisation verwenden Sie eine der folgenden Verfahren erstellen Sie einen AD FS 1. aus. *x* kompatibel "NameID"-Anspruch:  
  
-   Erstellen Sie mit dieser Regel, um das Problem ein AD FS 1.x namens-ID mit der **Pass-Through oder Filtern eine Regelvorlage eingehenden Anspruchs**  
  
-   Erstellen Sie mit dieser Regel, um das Problem ein AD FS 1.x namens-ID mit der **Transformieren einer eingehenden Anspruchs Regelvorlage**. Sie können diese Regelvorlage in Situationen verwenden, in denen der Typ des vorhandenen Anspruchs in einen neuen Anspruchstyp zu ändern, die mit AD FS 1. funktionieren sollen.  *x* Ansprüche.  
  
> [!NOTE]  
> Für diese Regel wie erwartet funktioniert, stellen Sie sicher, dass die Vertrauensstellung der vertrauenden Seite oder die Anspruchsanbieter-Vertrauensstellung Sie mit dieser Regel erstellen zur Verwendung konfiguriert wurden die **AD FS 1.0 und 1.1-Profil**. 




## <a name="to-create-a-rule-to-issue-an-adfs1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-a-relying-party-trust-in-windows-server-2016"></a>Erstellen Sie eine Regel zum Ausführen von AD FS 1. *x* namens-ID Anspruch mit dem Pass-Through oder Filtern von einer Vorlage des eingehenden Anspruchs-Regel auf a Relying Party Trust in Windows Server 2016 

1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  Rechts\-klicken Sie auf der ausgewählten Vertrauensstellung, und klicken Sie dann auf **Anspruchsausstellungsrichtlinie bearbeiten**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  In der **Anspruchsausstellungsrichtlinie bearbeiten** Dialogfeld **Ausstellungstransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **Pass-Through oder Filtern eines eingehenden Anspruchs** aus der Liste aus, und klicken Sie dann auf **weiter** .  
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  Auf der **Regel konfigurieren** geben anspruchsregelname.  
  
7.  In **eingehender Anspruchstyp**Option **namens-ID** in der Liste.  
  
8.  In **eingehenden namensbezeichnerformat**, wählen Sie eine der folgenden AD FS 1. *X*\-kompatiblen Anspruch Formate aus der Liste:  
  
    -   **UPN**  
  
    -   **E\--e-Mails**  
  
    -   **Allgemeiner Name**  
  
9. Wählen Sie eine der folgenden Optionen, je nach den Anforderungen Ihrer Organisation:  
  
    -   **Alle Anspruchswerte weiterleiten**  
  
    -   **Pass-through-nur einen bestimmten Anspruchswert**  
  
    -   **Pass-through-nur Anspruchswerte, die einem bestimmten e-Mail-Suffixwert entsprechen**  
  
    -   **Pass-through-nur Anspruchswerte durchalufen, die mit einem bestimmten Wert beginnen.**  
![Regel erstellen](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs3.PNG)   

10. Klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  

  
## <a name="to-create-a-rule-to-issue-an-adfs1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-a-claims-provider-trust-in-windows-server-2016"></a>Erstellen Sie eine Regel zum Ausführen von AD FS 1. *x* namens-ID-Anspruch mit dem Pass-Through oder Filtern eine Vorlage des eingehenden Anspruchs-Regel für eine Anspruchsanbieter-Vertrauensstellung in Windows Server 2016 
  
1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  Rechts\-klicken Sie auf der ausgewählten Vertrauensstellung, und klicken Sie dann auf **Edit Claim Rules**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  In der **Edit Claim Rules** Dialogfeld **Akzeptanztransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **Pass-Through oder Filtern eines eingehenden Anspruchs** aus der Liste aus, und klicken Sie dann auf **weiter** .  
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  Auf der **Regel konfigurieren** geben anspruchsregelname.  
  
7.  In **eingehender Anspruchstyp**Option **namens-ID** in der Liste.  
  
8.  In **eingehenden namensbezeichnerformat**, wählen Sie eine der folgenden AD FS 1. *X*\-kompatiblen Anspruch Formate aus der Liste:  
  
    -   **UPN**  
  
    -   **E\--e-Mails**  
  
    -   **Allgemeiner Name**  
  
9. Wählen Sie eine der folgenden Optionen, je nach den Anforderungen Ihrer Organisation:  
  
    -   **Alle Anspruchswerte weiterleiten**  
  
    -   **Pass-through-nur einen bestimmten Anspruchswert**  
  
    -   **Pass-through-nur Anspruchswerte, die einem bestimmten e-Mail-Suffixwert entsprechen**  
  
    -   **Pass-through-nur Anspruchswerte durchalufen, die mit einem bestimmten Wert beginnen.**  
![Regel erstellen](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs3.PNG)   

10. Klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  

  

## <a name="to-create-a-rule-to-transform-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>Zum Erstellen einer Regel zum Transformieren eines eingehenden Anspruchs auf a Relying Party Trust in Windows Server 2016 

1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  Rechts\-klicken Sie auf der ausgewählten Vertrauensstellung, und klicken Sie dann auf **Anspruchsausstellungsrichtlinie bearbeiten**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  In der **Anspruchsausstellungsrichtlinie bearbeiten** Dialogfeld **Ausstellungstransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **Transformieren eines eingehenden Anspruchs** aus der Liste aus, und klicken Sie dann auf **Weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)      

6.  Auf der **Regel konfigurieren** geben anspruchsregelname.  
  
7.  In **eingehender Anspruchstyp**, wählen Sie den Typ des eingehenden Anspruchs, der in der Liste transformiert werden sollen.  
  
8.  In **Typ des ausgehenden Anspruchs**Option **namens-ID** in der Liste.  
  
9. In **ausgehende namensbezeichnerformat**, wählen Sie eine der folgenden AD FS 1. *X*\-kompatiblen Anspruch Formate aus der Liste:  
  
    -   **UPN**  
  
    -   **E\--e-Mails**  
  
    -   **Allgemeiner Name**  
  
10. Wählen Sie eine der folgenden Optionen, je nach den Anforderungen Ihrer Organisation:  
  
    -   **Alle Anspruchswerte weiterleiten**  
  
    -   **Ersetzen Sie einen eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert**  
  
    -   **Ersetzen Sie eingehende e\-e-Mail-suffixansprüche mit einer neuen e\-e-Mail-Suffix**  
![Regel erstellen](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs4.PNG)    

11. Klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  

  


## <a name="to-create-a-rule-to-transform-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>Zum Erstellen einer Regel zum Transformieren eines eingehenden Anspruchs auf eine Anspruchsanbieter-Vertrauensstellung in Windows Server 2016 
  
1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  Rechts\-klicken Sie auf der ausgewählten Vertrauensstellung, und klicken Sie dann auf **Edit Claim Rules**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  In der **Edit Claim Rules** Dialogfeld **Akzeptanztransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **Transformieren eines eingehenden Anspruchs** aus der Liste aus, und klicken Sie dann auf **Weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)      

6.  Auf der **Regel konfigurieren** geben anspruchsregelname.  
  
7.  In **eingehender Anspruchstyp**, wählen Sie den Typ des eingehenden Anspruchs, der in der Liste transformiert werden sollen.  
  
8.  In **Typ des ausgehenden Anspruchs**Option **namens-ID** in der Liste.  
  
9. In **ausgehende namensbezeichnerformat**, wählen Sie eine der folgenden AD FS 1. *X*\-kompatiblen Anspruch Formate aus der Liste:  
  
    -   **UPN**  
  
    -   **E\--e-Mails**  
  
    -   **Allgemeiner Name**  
  
10. Wählen Sie eine der folgenden Optionen, je nach den Anforderungen Ihrer Organisation:  
  
    -   **Alle Anspruchswerte weiterleiten**  
  
    -   **Ersetzen Sie einen eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert**  
  
    -   **Ersetzen Sie eingehende e\-e-Mail-suffixansprüche mit einer neuen e\-e-Mail-Suffix**  
![Regel erstellen](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs4.PNG)    

11. Klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  













  
## <a name="to-create-a-rule-to-issue-an-adfs1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-windows-server-2012-r2"></a>Erstellen Sie eine Regel zum Ausführen von AD FS 1. *x* namens-ID Anspruch mit dem Pass-Through oder Filtern von einer Vorlage des eingehenden Anspruchs-Regel auf Windows Server 2012 R2
  
1.  Klicken Sie im Server-Manager **Tools**, und klicken Sie dann auf **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **AD FS\\Vertrauensstellungen**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen** oder **Vertrauensstellungen für vertrauende Seiten**, und klicken Sie dann auf einen bestimmten Vertrauen Sie in der Liste, die zum Erstellen dieser Regel werden sollen.  
  
3.  Rechts\-klicken Sie auf der ausgewählten Vertrauensstellung, und klicken Sie dann auf **Edit Claim Rules**.  
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) 
  
4.  In der **Edit Claim Rules** im Dialogfeld Wählen Sie eine der folgenden Registerkarten, abhängig von der Vertrauensstellung, die Sie bearbeiten und welche Regel legen Sie, diese Regel in erstellen möchten, und klicken Sie dann auf **Regel hinzufügen** zum Starten des Regel-Assistenten Das ist mit diesem Regelsatz verknüpft:  
  
    -   **Akzeptanztransformationsregeln**  
  
    -   **Ausstellungstransformationsregeln**  
  
    -   **Ausstellungsautorisierungsregeln**  
  
    -   **Autorisierungsregeln**  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **Pass-Through oder Filtern eines eingehenden Anspruchs** aus der Liste aus, und klicken Sie dann auf **weiter** .  
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule7.PNG)  
  
6.  Auf der **Regel konfigurieren** geben anspruchsregelname.  
  
7.  In **eingehender Anspruchstyp**Option **namens-ID** in der Liste.  
  
8.  In **eingehenden namensbezeichnerformat**, wählen Sie eine der folgenden AD FS 1. *X*\-kompatiblen Anspruch Formate aus der Liste:  
  
    -   **UPN**  
  
    -   **E\--e-Mails**  
  
    -   **Allgemeiner Name**  
  
9. Wählen Sie eine der folgenden Optionen, je nach den Anforderungen Ihrer Organisation:  
  
    -   **Alle Anspruchswerte weiterleiten**  
  
    -   **Pass-through-nur einen bestimmten Anspruchswert**  
  
    -   **Pass-through-nur Anspruchswerte, die einem bestimmten e-Mail-Suffixwert entsprechen**  
  
    -   **Pass-through-nur Anspruchswerte durchalufen, die mit einem bestimmten Wert beginnen.**  
![Regel erstellen](media/\Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs1.PNG)   

10. Klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  

  
## <a name="to-create-a-rule-to-issue-an-adfs1x-name-id-claim-using-the-transform-an-incoming-claim-rule-template-in-windows-server-2012-r2"></a>Erstellen Sie eine Regel zum Ausführen von AD FS 1. *x* namens-ID-Anspruch, die mit der Transformation einer eingehenden Anspruchs Regelvorlage in Windows Server 2012 R2  
  
1.  Klicken Sie im Server-Manager **Tools**, und klicken Sie dann auf **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **AD FS\\Vertrauensstellungen**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen** oder **Vertrauensstellungen für vertrauende Seiten**, und klicken Sie dann auf einen bestimmten Vertrauen Sie in der Liste, die zum Erstellen dieser Regel werden sollen.  
  
3.  Rechts\-klicken Sie auf der ausgewählten Vertrauensstellung, und klicken Sie dann auf **Edit Claim Rules**.  
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) 
  
4.  In der **Edit Claim Rules** (Dialogfeld), wählen Sie eine der folgenden Registerkarten, die für die Vertrauensstellung abhängt, die Sie bearbeiten und in der Regel legen Sie möchten, erstellen diese Regel, und klicken Sie dann auf **Regel hinzufügen** um die Regel zu starten. Legen Sie den Assistenten, der dieser Regel zugeordnet ist:  
  
    -   **Akzeptanztransformationsregeln**  
  
    -   **Ausstellungstransformationsregeln**  
  
    -   **Ausstellungsautorisierungsregeln**  
  
    -   **Autorisierungsregeln**  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)
  
5.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **Transformieren eines eingehenden Anspruchs** aus der Liste aus, und klicken Sie dann auf **Weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform1.PNG)   
  
6.  Auf der **Regel konfigurieren** geben anspruchsregelname.  
  
7.  In **eingehender Anspruchstyp**, wählen Sie den Typ des eingehenden Anspruchs, der in der Liste transformiert werden sollen.  
  
8.  In **Typ des ausgehenden Anspruchs**Option **namens-ID** in der Liste.  
  
9. In **ausgehende namensbezeichnerformat**, wählen Sie eine der folgenden AD FS 1. *X*\-kompatiblen Anspruch Formate aus der Liste:  
  
    -   **UPN**  
  
    -   **E\--e-Mails**  
  
    -   **Allgemeiner Name**  
  
10. Wählen Sie eine der folgenden Optionen, je nach den Anforderungen Ihrer Organisation:  
  
    -   **Alle Anspruchswerte weiterleiten**  
  
    -   **Ersetzen Sie einen eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert**  
  
    -   **Ersetzen Sie eingehende e\-e-Mail-suffixansprüche mit einer neuen e\-e-Mail-Suffix**  
![Regel erstellen](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs2.PNG)    

11. Klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  

## <a name="additional-references"></a>Weitere Verweise 
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  
 
[Prüfliste: Erstellen von Anspruchsregeln für eine Vertrauensstellung der vertrauenden Seite](https://technet.microsoft.com/library/ee913578.aspx)  

[Prüfliste: Erstellen von Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung](https://technet.microsoft.com/library/ee913564.aspx)  
  
[Wenn Use an Authorization Claim Rule](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
