---
ms.assetid: 6127963f-71b2-4d8f-8b53-7c525bf06521
title: Erstellen einer Regel zum Weiterleiten oder Filtern eines eingehenden Anspruchs
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 50f50cd4e096b107a2b58ac05328ff8ed413f2dc
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-rule-to-pass-through-or-filter-an-incoming-claim"></a>Erstellen einer Regel zum Weiterleiten oder Filtern eines eingehenden Anspruchs

>Gilt für: Windows Server 2016, Windows Server2012 R2

Die weiterleiten oder Filtern einer eingehenden Anspruchs-Vorlage in Active Directory Federation Services \(AD FS\) verwenden, können Sie alle eingehenden Ansprüche mit einem ausgewählten Anspruchstyp passieren. Sie können auch die Werte der eingehenden Ansprüche mit einem ausgewählten Anspruchstyp filtern. Beispielsweise können Sie diese Regelvorlage zum Erstellen einer Regel, die alle eingehenden Gruppenansprüche gesendet wird. Sie können auch diese Regel nur für Benutzer Dienstprinzipalnamen \(UPN\) Ansprüche gesendet werden, die mit @fabrikam.  
  
Das folgende Verfahren können zum Erstellen einer Anspruchsregel mit AD FS-Verwaltungs-Snap-In.  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   

## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>Erstellen eine Regel zum Weiterleiten oder Filtern eines eingehenden Anspruchs auf eine der vertrauenden Seite Vertrauensstellung in Windows Server2016 

1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten **. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  Mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Anspruch Ausstellungsrichtlinie bearbeiten **.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  In der **Anspruch Ausstellungsrichtlinie bearbeiten** Dialogfeld unter **Ausstellungstransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **weiterleiten oder Filtern eines eingehenden Anspruchs** aus der Liste, und klicken Sie dann auf **Weiter **.  
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  Auf der **Regel konfigurieren** Seite **Name der Anspruchsregel** Geben Sie den Namen für diese Regel **eingehender Anspruchstyp** wählen Sie einen Anspruchstyp aus der Liste, und wählen Sie dann eine der folgenden Optionen, je nach den Anforderungen Ihrer Organisation:  
  
    -   **Alle Anspruchswerte weiterleiten**  
  
    -   **Nur einen bestimmten Anspruchswert weiterleiten**  
  
    -   **Nur Anspruchswerte weiterleiten Sie, die einem bestimmten E-Mail-Suffixwert entsprechen**  
  
    -   **Nur Anspruchswerte weiterleiten Sie, die mit einem bestimmten Wert starten**  
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule5.PNG)    

7.  Klicken Sie auf die **Fertig stellen** Schaltfläche.  
  
8.  In der **Anspruchsregeln bearbeiten** Dialogfeld, klicken Sie auf **OK** um die Regel zu speichern.
  
## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>Erstellen eine Regel zum Weiterleiten oder Filtern eines eingehenden Anspruchs auf eine Anspruchsanbieter-Vertrauensstellung in Windows Server2016 
  
1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen **. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  Mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Anspruchsregeln bearbeiten **.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  In der **Anspruchsregeln bearbeiten** Dialogfeld unter **Akzeptanztransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **weiterleiten oder Filtern eines eingehenden Anspruchs** aus der Liste, und klicken Sie dann auf **Weiter **.  
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  Auf der **Regel konfigurieren** Seite **Name der Anspruchsregel** Geben Sie den Namen für diese Regel **eingehender Anspruchstyp** wählen Sie einen Anspruchstyp aus der Liste, und wählen Sie dann eine der folgenden Optionen, je nach den Anforderungen Ihrer Organisation:  
  
    -   **Alle Anspruchswerte weiterleiten**  
  
    -   **Nur einen bestimmten Anspruchswert weiterleiten**  
  
    -   **Nur Anspruchswerte weiterleiten Sie, die einem bestimmten E-Mail-Suffixwert entsprechen**  
  
    -   **Nur Anspruchswerte weiterleiten Sie, die mit einem bestimmten Wert starten**  
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule5.PNG)    

7.  Klicken Sie auf die **Fertig stellen** Schaltfläche.  
  
8.  In der **Anspruchsregeln bearbeiten** Dialogfeld, klicken Sie auf **OK** um die Regel zu speichern.  

## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-in-windows-server-2012-r2"></a>Erstellen eine Regel zum Weiterleiten oder Filtern eines eingehenden Anspruchs in Windows Server2012 R2

1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD FSAD FS\\Trust Beziehungen**, klicken Sie entweder **Anspruchsanbieter-Vertrauensstellungen** oder **Vertrauensstellungen für vertrauende Seiten**, und klicken Sie dann auf eine bestimmte Vertrauensstellung in der Liste, in denen Sie diese Regel erstellen möchten.  
  
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

6.  Auf der **Regel konfigurieren** Seite **Name der Anspruchsregel** Geben Sie den Namen für diese Regel **eingehender Anspruchstyp** wählen Sie einen Anspruchstyp aus der Liste, und wählen Sie dann eine der folgenden Optionen, je nach den Anforderungen Ihrer Organisation:  
  
    -   **Alle Anspruchswerte weiterleiten**  
  
    -   **Nur einen bestimmten Anspruchswert weiterleiten**  
  
    -   **Nur Anspruchswerte weiterleiten Sie, die einem bestimmten E-Mail-Suffixwert entsprechen**  
  
    -   **Nur Anspruchswerte weiterleiten Sie, die mit einem bestimmten Wert starten**  
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule8.PNG)    

7.  Klicken Sie auf die **Fertig stellen** Schaltfläche.  
  
8.  In der **Anspruchsregeln bearbeiten** Dialogfeld, klicken Sie auf **OK** um die Regel zu speichern.  



  
## <a name="additional-references"></a>Weitere Verweise  
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  
  
[Verwendung von Pass-Through or Filter Claim Rule](../../ad-fs/technical-reference/When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md)  
  
[Die Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Die Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
  
