---
ms.assetid: ef83960f-d2cf-441f-b2b6-d97822ec7149
title: Erstellen einer Regel zum Transformieren eines eingehenden Anspruchs
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6bd107aca6c6f33cdf5f88e5b48a52fdea8d2086
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189341"
---
# <a name="create-a-rule-to-transform-an-incoming-claim"></a>Erstellen einer Regel zum Transformieren eines eingehenden Anspruchs


Mithilfe der **Transformieren eines eingehenden Anspruchs** Regelvorlage in Active Directory-Verbunddienste \(AD FS\), können Sie einen eingehenden Anspruch auswählen, ändern Sie den Anspruchstyp und Ändern der Anspruchswert. Beispielsweise können Sie diese Regelvorlage zum Erstellen einer Regel, die einen Rollenanspruch mit dem gleichen Anspruchswert eines eingehenden Anspruchs für die Gruppe gesendet. Sie können auch mit dieser Regel verwenden, senden Sie die einen Gruppenanspruch mit einem Anspruchswert, der Käufer beim eingehenden Gruppenanspruch mit einem Wert von Administratoren vorhanden ist oder Sie können nur Benutzerprinzipalname senden \(UPN\) Ansprüche, die mit @fabrikam.  
  
Sie können das folgende Verfahren zum Erstellen einer Anspruchsregel mit der AD FS-Verwaltungs-Snap\-in.  
  
Mitgliedschaft in **Administratoren**, oder einer entsprechenden, auf dem lokalen Computer die Mindestanforderung zum Ausführen dieses Verfahrens.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477). 

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

6.  Auf der **Regel konfigurieren** Seite **anspruchsregelname**, geben Sie den Anzeigenamen für diese Regel. In **eingehender Anspruchstyp**, wählen Sie einen Anspruchstyp aus der Liste. In **Typ des ausgehenden Anspruchs**, wählen Sie einen Anspruchstyp aus der Liste, und wählen Sie dann eine der folgenden Optionen, die von den Anforderungen Ihrer Organisation abhängig ist:  
  
    -   **Alle Anspruchswerte weiterleiten**  
  
    -   **Ersetzen Sie einen eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert**  
  
    -   **Ersetzen Sie eingehende e\-e-Mail-suffixansprüche mit einer neuen e\-e-Mail-Suffix**  
![Regel erstellen](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform4.PNG)   

7.  Klicken Sie auf die **Fertig stellen** Schaltfläche.  
  
8.  In der **Edit Claim Rules** Dialogfeld klicken Sie auf **OK** um die Regel zu speichern.
  
> [!NOTE]  
> Wenn Sie das Dynamic Access Control-Szenario einrichten, die AD FS verwendet\-Ansprüche ausgestellt, zuerst eine transformationsregel erstellen, auf die Anspruchsanbieter-Vertrauensstellung und in **eingehender Anspruchstyp**, geben Sie den Namen für den eingehenden Anspruch aus, oder, wenn Sie eine anspruchsbeschreibung wurde zuvor erstellt haben, wählen sie aus der Liste. In zweiter **Typ des ausgehenden Anspruchs**, wählen Sie die Anspruchs-URL, die Sie möchten, und erstellen Sie eine transformationsregel klicken Sie dann auf die Vertrauensstellung der vertrauenden Seite Ausstellen der Gerät-Anspruchs.  
>   
> Weitere Informationen zu Dynamic Access Control-Szenarien finden Sie unter [Dynamic Access Control Content Roadmap](../../solution-guides/dynamic-access-control--scenario-overview.md) oder [Using AD DS-Ansprüchen mit AD FS](https://technet.microsoft.com/library/hh831504.aspx). 

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

6.  Auf der **Regel konfigurieren** Seite **anspruchsregelname**, geben Sie den Anzeigenamen für diese Regel. In **eingehender Anspruchstyp**, wählen Sie einen Anspruchstyp aus der Liste. In **Typ des ausgehenden Anspruchs**, wählen Sie einen Anspruchstyp aus der Liste, und wählen Sie dann eine der folgenden Optionen, die von den Anforderungen Ihrer Organisation abhängig ist:  
  
    -   **Alle Anspruchswerte weiterleiten**  
  
    -   **Ersetzen Sie einen eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert**  
  
    -   **Ersetzen Sie eingehende e\-e-Mail-suffixansprüche mit einer neuen e\-e-Mail-Suffix**  
![Regel erstellen](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform4.PNG)       

7.  Klicken Sie auf die **Fertig stellen** Schaltfläche.  
  
8.  In der **Edit Claim Rules** Dialogfeld klicken Sie auf **OK** um die Regel zu speichern.  

> [!NOTE]  
> Wenn Sie das Dynamic Access Control-Szenario einrichten, die AD FS verwendet\-Ansprüche ausgestellt, zuerst eine transformationsregel erstellen, auf die Anspruchsanbieter-Vertrauensstellung und in **eingehender Anspruchstyp**, geben Sie den Namen für den eingehenden Anspruch aus, oder, wenn Sie eine anspruchsbeschreibung wurde zuvor erstellt haben, wählen sie aus der Liste. In zweiter **Typ des ausgehenden Anspruchs**, wählen Sie die Anspruchs-URL, die Sie möchten, und erstellen Sie eine transformationsregel klicken Sie dann auf die Vertrauensstellung der vertrauenden Seite Ausstellen der Gerät-Anspruchs.  
>   
> Weitere Informationen zu Dynamic Access Control-Szenarien finden Sie unter [Dynamic Access Control Content Roadmap](../../solution-guides/dynamic-access-control--scenario-overview.md) oder [Using AD DS-Ansprüchen mit AD FS](https://technet.microsoft.com/library/hh831504.aspx).   
  
## <a name="to-create-a-rule-to-transform-an-incoming-claim-in-windows-server-2012-r2"></a>Zum Erstellen einer Regel zum Transformieren eines eingehenden Anspruchs in Windows Server 2012 R2 
  
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

6.  Auf der **Regel konfigurieren** Seite **anspruchsregelname**, geben Sie den Anzeigenamen für diese Regel. In **eingehender Anspruchstyp**, wählen Sie einen Anspruchstyp aus der Liste. In **Typ des ausgehenden Anspruchs**, wählen Sie einen Anspruchstyp aus der Liste, und wählen Sie dann eine der folgenden Optionen, die von den Anforderungen Ihrer Organisation abhängig ist:  
  
    -   **Alle Anspruchswerte weiterleiten**  
  
    -   **Ersetzen Sie einen eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert**  
  
    -   **Ersetzen Sie eingehende e\-e-Mail-suffixansprüche mit einer neuen e\-e-Mail-Suffix**  
![Regel erstellen](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform2.PNG)  

> [!NOTE]  
> Wenn Sie das Dynamic Access Control-Szenario einrichten, die AD FS verwendet\-Ansprüche ausgestellt, zuerst eine transformationsregel erstellen, auf die Anspruchsanbieter-Vertrauensstellung und in **eingehender Anspruchstyp**, geben Sie den Namen für den eingehenden Anspruch aus, oder, wenn Sie eine anspruchsbeschreibung wurde zuvor erstellt haben, wählen sie aus der Liste. In zweiter **Typ des ausgehenden Anspruchs**, wählen Sie die Anspruchs-URL, die Sie möchten, und erstellen Sie eine transformationsregel klicken Sie dann auf die Vertrauensstellung der vertrauenden Seite Ausstellen der Gerät-Anspruchs.  
>   
> Weitere Informationen zu Dynamic Access Control-Szenarien finden Sie unter [Dynamic Access Control Content Roadmap](../../solution-guides/dynamic-access-control--scenario-overview.md) oder [Using AD DS-Ansprüchen mit AD FS](https://technet.microsoft.com/library/hh831504.aspx).  
  
7.  Klicken Sie auf **Fertig stellen**.  
  
8.  In der **Edit Claim Rules** Dialogfeld klicken Sie auf **OK** um die Regel zu speichern.  

## <a name="additional-references"></a>Weitere Verweise 
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  
 
[Prüfliste: Erstellen von Anspruchsregeln für eine Vertrauensstellung der vertrauenden Seite](https://technet.microsoft.com/library/ee913578.aspx)  

[Prüfliste: Erstellen von Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung](https://technet.microsoft.com/library/ee913564.aspx)  
  
[Wenn Use an Authorization Claim Rule](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
