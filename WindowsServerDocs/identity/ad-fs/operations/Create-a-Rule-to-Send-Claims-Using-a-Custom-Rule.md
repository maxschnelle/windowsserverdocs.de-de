---
ms.assetid: 38eb3726-e97b-484e-9926-67e8a046b0c5
title: Erstellen einer Regel zum Senden von Ansprüchen mithilfe einer benutzerdefinierten Regel
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 0dcde4d9996f25f4d339a76f38d9753bf822ef67
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961692"
---
# <a name="create-a-rule-to-send-claims-using-a-custom-rule"></a>Erstellen einer Regel zum Senden von Ansprüchen mithilfe einer benutzerdefinierten Regel


Mithilfe der Vorlage " **Ansprüche mithilfe einer benutzerdefinierten Regel senden** " in Active Directory-Verbunddienste (AD FS) (AD FS) können Sie benutzerdefinierte Anspruchs Regeln für Situationen erstellen, in denen eine Standardregel Vorlage nicht den Anforderungen Ihrer Organisation entspricht. Benutzerdefinierte Anspruchs Regeln werden in der Anspruchs Regel Sprache geschrieben und müssen dann in das Textfeld **benutzerdefinierte Regel** kopiert werden, bevor Sie in einem Regelsatz verwendet werden können. Weitere Informationen zum Erstellen der Syntax für eine erweiterte Regel finden Sie [unter der Rolle der Anspruchs Regel Sprache](../../ad-fs/technical-reference/The-Role-of-the-Claim-Rule-Language.md).  
  
Mithilfe des folgenden Verfahrens können Sie eine Anspruchs Regel erstellen, indem Sie das Snap-in für die AD FS-Verwaltung verwenden \- .  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren**oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).



## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>So erstellen Sie eine Regel zum Weiterleiten oder Filtern eines eingehenden Anspruchs für eine Vertrauensstellung der vertrauenden Seite in Windows Server 2016 

1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie **AD FS-Verwaltung** aus.  
  
2.  Klicken Sie in der Konsolen Struktur unter **AD FS**auf Vertrauens Stellungen der vertrauenden **Seite**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  \-Klicken Sie mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Richtlinie**zum
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  Klicken Sie im Dialogfeld **Richtlinie für Anspruchs Ausstellung bearbeiten** unter Ausstellungs **Transformationsregeln** auf **Regel hinzufügen** , um den Regel-Assistenten zu starten. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die Option **Ansprüche mithilfe einer benutzerdefinierten Regel senden** aus der Liste aus, und klicken Sie dann auf **weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom3.PNG)   
  
6.  Geben Sie auf der Seite **Regel konfigurieren** unter **Anspruchs Regel Name**den anzeigen Amen für diese Regel ein. Geben Sie unter **benutzerdefinierte Regel**die Syntax der Anspruchs Regel Sprache ein, die Sie für diese Regel benötigen, oder fügen Sie Sie ein.  
![Regel erstellen](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom4.PNG)     

7.  Klicken Sie auf **Fertig stellen**.  
  
8.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** auf **OK** , um die Regel zu speichern.   
  
## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>So erstellen Sie eine Regel zum Weiterleiten oder Filtern eines eingehenden Anspruchs für eine Anspruchs Anbieter-Vertrauensstellung in Windows Server 2016 
  
1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie **AD FS-Verwaltung** aus.  
  
2.  Klicken Sie in der Konsolen Struktur unter **AD FS**auf **Anspruchs Anbieter**-Vertrauens Stellungen. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  \-Klicken Sie mit der rechten Maustaste auf die ausgewählte Vertrauensstellung und dann auf **Anspruchs Regeln bearbeiten**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** unter **Akzeptanz Transformationsregeln** auf **Regel hinzufügen** , um den Regel-Assistenten zu starten.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die Option **Ansprüche mithilfe einer benutzerdefinierten Regel senden** aus der Liste aus, und klicken Sie dann auf **weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom3.PNG)   
  
6.  Geben Sie auf der Seite **Regel konfigurieren** unter **Anspruchs Regel Name**den anzeigen Amen für diese Regel ein. Geben Sie unter **benutzerdefinierte Regel**die Syntax der Anspruchs Regel Sprache ein, die Sie für diese Regel benötigen, oder fügen Sie Sie ein.  
![Regel erstellen](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom4.PNG)     

7.  Klicken Sie auf **Fertig stellen**.  
  
8.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** auf **OK** , um die Regel zu speichern.   

















   
  
## <a name="to-create-a-rule-to-send-claims-by-using-a-custom-claim-in-windows-server-2012-r2"></a>So erstellen Sie eine Regel zum Senden von Ansprüchen mithilfe eines benutzerdefinierten Anspruchs in Windows Server 2012 R2 
  
1.  Klicken Sie in Server-Manager **auf Extras, und**klicken Sie dann auf **AD FS Verwaltung**.  
  
2.  Klicken Sie in der Konsolen Struktur unter AD FS Vertrauens Stellungen entweder auf **Anspruchs Anbieter** -Vertrauens Stellungen oder Vertrauens Stellungen der ** \\ vertrauenden** **Seite**, und klicken Sie dann auf eine bestimmte Vertrauensstellung in der Liste, in der Sie diese Regel erstellen möchten.  
  
3.  \-Klicken Sie mit der rechten Maustaste auf die ausgewählte Vertrauensstellung und dann auf **Anspruchs Regeln bearbeiten**.  
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) 
  
4.  Wählen Sie im Dialogfeld **Anspruchs Regeln bearbeiten** eine der folgenden Registerkarten aus, die von der zu bearbeitenden Vertrauensstellung und dem Regelsatz abhängt, den Sie diese Regel erstellen möchten, und klicken Sie dann auf **Regel hinzufügen** , um den Regel-Assistenten zu starten, der diesem Regelsatz zugeordnet ist:  
  
    -   **Akzeptanz Transformationsregeln**  
  
    -   **Ausstellungs Transformationsregeln**  
  
    -   **Ausstellungs Autorisierungs Regeln**  
  
    -   **Delegierungs Autorisierungs Regeln**  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)
  
5.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die Option **Ansprüche mithilfe einer benutzerdefinierten Regel senden** aus der Liste aus, und klicken Sie dann auf **weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom1.PNG)   
  
6.  Geben Sie auf der Seite **Regel konfigurieren** unter **Anspruchs Regel Name**den anzeigen Amen für diese Regel ein. Geben Sie unter **benutzerdefinierte Regel**die Syntax der Anspruchs Regel Sprache ein, die Sie für diese Regel benötigen, oder fügen Sie Sie ein.  
![Regel erstellen](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom2.PNG)     

7.  Klicken Sie auf **Fertig stellen**.  
  
8.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** auf **OK** , um die Regel zu speichern.  

## <a name="additional-references"></a>Zusätzliche Verweise 
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  
 
[Prüfliste: Erstellen von Anspruchsregeln für eine Vertrauensstellung der vertrauenden Seite](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ee913578(v=ws.11))  

[Prüfliste: Erstellen von Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ee913564(v=ws.11))  
  
[Wann sollte eine Autorisierungsanspruchsregel verwendet werden](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
