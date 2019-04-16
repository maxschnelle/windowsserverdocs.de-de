---
ms.assetid: ef83960f-d2cf-441f-b2b6-d97822ec7149
title: Erstellen einer Regel zum Transformieren eines eingehenden Anspruchs
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e982b7608f7602268657ceae74f641bbaaaec939
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-rule-to-transform-an-incoming-claim"></a>Erstellen einer Regel zum Transformieren eines eingehenden Anspruchs

>Gilt für: Windows Server 2016, Windows Server2012 R2

Mithilfe der **Transformieren eines eingehenden Anspruchs** Regelvorlage in Active Directory Federation Services \(AD FS\), einen eingehenden Anspruch auswählen, ändern Sie den Anspruchstyp und Ändern der Anspruchswert. Beispielsweise können Sie diese Regelvorlage zum Erstellen einer Regel, die einen Rollenanspruch mit den gleichen Anspruchswert eines eingehenden Anspruchs der Gruppe gesendet. Sie können auch diese Regel senden Gruppenanspruch mit dem Anspruchswert Käufer ein eingehenden Anspruchs der Gruppe mit dem Wert "Administratoren" ist, oder Sie können nur Benutzerprinzipalname \(UPN\) Ansprüche von diesem Zweck mit @fabrikam.  
  
Das folgende Verfahren können zum Erstellen einer Anspruchsregel mit AD FS-Verwaltungs-Snap-In.  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer die Mindestanforderung zum Ausführen dieses Verfahrens.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477). 

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

6.  Auf der **Regel konfigurieren** Seite unter **Name der Anspruchsregel**, geben Sie den Namen für diese Regel. In **eingehender Anspruchstyp**, wählen Sie ein Anspruch Geben Sie die Liste. In **ausgehenden Anspruchstyp**, wählen Sie einen Anspruchstyp aus der Liste, und wählen Sie dann eine der folgenden Optionen, die von den Anforderungen Ihrer Organisation abhängig ist:  
  
    -   **Alle Anspruchswerte weiterleiten**  
  
    -   **Ersetzen Sie einen eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert**  
  
    -   **Ersetzen Sie eingehende E\ E-Mail-Suffixansprüche durch ein neues E\ E-Mail-Suffix**  
![Erstellen der Regel](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform4.PNG)   

7.  Klicken Sie auf die **Fertig stellen** Schaltfläche.  
  
8.  In der **Anspruchsregeln bearbeiten** Dialogfeld, klicken Sie auf **OK** um die Regel zu speichern.
  
> [!NOTE]  
> Wenn Sie das Szenario für die dynamische Zugriffssteuerung, die AD-FS\ ausgestellten Ansprüche verwendet einrichten, Erstellen einer transformationsregel zunächst auf die Anspruchsanbieter-Vertrauensstellung, und klicken Sie im **eingehender Anspruchstyp**, geben Sie den Namen für den eingehenden Anspruch oder, wenn eine anspruchsbeschreibung erstellt wurde, wählen sie in der Liste. Zweitens **ausgehenden Anspruchstyp**, wählen Sie den Anspruch-URL, die Sie möchten, und erstellen Sie dann auf die Vertrauensstellung der vertrauenden Seite den Geräteanspruch ausstellen eine transformationsregel.  
>   
> Weitere Informationen zu dynamischen Zugriffssteuerung Szenarien finden Sie unter [Dynamic Access-Steuerelement Inhaltsroadmap](../../solution-guides/dynamic-access-control--scenario-overview.md) oder [Using AD DS-Ansprüchen mit AD FS ](https://technet.microsoft.com/library/hh831504.aspx). 

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

6.  Auf der **Regel konfigurieren** Seite unter **Name der Anspruchsregel**, geben Sie den Namen für diese Regel. In **eingehender Anspruchstyp**, wählen Sie ein Anspruch Geben Sie die Liste. In **ausgehenden Anspruchstyp**, wählen Sie einen Anspruchstyp aus der Liste, und wählen Sie dann eine der folgenden Optionen, die von den Anforderungen Ihrer Organisation abhängig ist:  
  
    -   **Alle Anspruchswerte weiterleiten**  
  
    -   **Ersetzen Sie einen eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert**  
  
    -   **Ersetzen Sie eingehende E\ E-Mail-Suffixansprüche durch ein neues E\ E-Mail-Suffix**  
![Erstellen der Regel](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform4.PNG)       

7.  Klicken Sie auf die **Fertig stellen** Schaltfläche.  
  
8.  In der **Anspruchsregeln bearbeiten** Dialogfeld, klicken Sie auf **OK** um die Regel zu speichern.  

> [!NOTE]  
> Wenn Sie das Szenario für die dynamische Zugriffssteuerung, die AD-FS\ ausgestellten Ansprüche verwendet einrichten, Erstellen einer transformationsregel zunächst auf die Anspruchsanbieter-Vertrauensstellung, und klicken Sie im **eingehender Anspruchstyp**, geben Sie den Namen für den eingehenden Anspruch oder, wenn eine anspruchsbeschreibung erstellt wurde, wählen sie in der Liste. Zweitens **ausgehenden Anspruchstyp**, wählen Sie den Anspruch-URL, die Sie möchten, und erstellen Sie dann auf die Vertrauensstellung der vertrauenden Seite den Geräteanspruch ausstellen eine transformationsregel.  
>   
> Weitere Informationen zu dynamischen Zugriffssteuerung Szenarien finden Sie unter [Dynamic Access-Steuerelement Inhaltsroadmap](../../solution-guides/dynamic-access-control--scenario-overview.md) oder [Using AD DS-Ansprüchen mit AD FS ](https://technet.microsoft.com/library/hh831504.aspx).   
  
## <a name="to-create-a-rule-to-transform-an-incoming-claim-in-windows-server-2012-r2"></a>Zum Erstellen einer Regel zum Transformieren eines eingehenden Anspruchs in Windows Server2012 R2 
  
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

6.  Auf der **Regel konfigurieren** Seite unter **Name der Anspruchsregel**, geben Sie den Namen für diese Regel. In **eingehender Anspruchstyp**, wählen Sie ein Anspruch Geben Sie die Liste. In **ausgehenden Anspruchstyp**, wählen Sie einen Anspruchstyp aus der Liste, und wählen Sie dann eine der folgenden Optionen, die von den Anforderungen Ihrer Organisation abhängig ist:  
  
    -   **Alle Anspruchswerte weiterleiten**  
  
    -   **Ersetzen Sie einen eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert**  
  
    -   **Ersetzen Sie eingehende E\ E-Mail-Suffixansprüche durch ein neues E\ E-Mail-Suffix**  
![Erstellen der Regel](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform2.PNG)  

> [!NOTE]  
> Wenn Sie das Szenario für die dynamische Zugriffssteuerung, die AD-FS\ ausgestellten Ansprüche verwendet einrichten, Erstellen einer transformationsregel zunächst auf die Anspruchsanbieter-Vertrauensstellung, und klicken Sie im **eingehender Anspruchstyp**, geben Sie den Namen für den eingehenden Anspruch oder, wenn eine anspruchsbeschreibung erstellt wurde, wählen sie in der Liste. Zweitens **ausgehenden Anspruchstyp**, wählen Sie den Anspruch-URL, die Sie möchten, und erstellen Sie dann auf die Vertrauensstellung der vertrauenden Seite den Geräteanspruch ausstellen eine transformationsregel.  
>   
> Weitere Informationen zu dynamischen Zugriffssteuerung Szenarien finden Sie unter [Dynamic Access-Steuerelement Inhaltsroadmap](../../solution-guides/dynamic-access-control--scenario-overview.md) oder [Using AD DS-Ansprüchen mit AD FS ](https://technet.microsoft.com/library/hh831504.aspx).  
  
7.  Klicken Sie auf **Fertig stellen**.  
  
8.  In der **Anspruchsregeln bearbeiten** Dialogfeld, klicken Sie auf **OK** um die Regel zu speichern.  

## <a name="additional-references"></a>Weitere Verweise 
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  
 
[Prüfliste: Erstellen von Anspruchsregeln für eine Vertrauensstellung der vertrauenden Seite](https://technet.microsoft.com/library/ee913578.aspx)  

[Prüfliste: Erstellen von Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung](https://technet.microsoft.com/library/ee913564.aspx)  
  
[Wann sollte eine Autorisierungsanspruchsregel verwendet](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Die Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Die Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
