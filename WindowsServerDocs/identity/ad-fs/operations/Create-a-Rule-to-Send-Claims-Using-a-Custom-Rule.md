---
ms.assetid: 38eb3726-e97b-484e-9926-67e8a046b0c5
title: Erstellen einer Regel zum Senden von Ansprüchen mithilfe einer benutzerdefinierten Regel
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f0eef89e651585d48ba87d14bc782efa49087669
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824831"
---
# <a name="create-a-rule-to-send-claims-using-a-custom-rule"></a>Erstellen einer Regel zum Senden von Ansprüchen mithilfe einer benutzerdefinierten Regel

>Gilt für: Windows Server 2016, Windows Server 2012 R2

Mithilfe der **Ansprüche mit benutzerdefinierter Regel senden** Vorlage in Active Directory-Verbunddienste (AD FS), Sie können benutzerdefinierte Anspruchsregeln für die Situation, in dem eine standardregelvorlage nicht die Anforderungen des erfüllt, erstellen Ihre die Organisation. Benutzerdefinierte Anspruchsregeln in der anspruchsregelsprache geschrieben sind, und klicken Sie dann in kopiert werden müssen die **benutzerdefinierte Regel** Textfeld, bevor sie in einem Regelsatz verwendet werden können. Informationen über die Syntax für eine erweiterte Regel erstellen, finden Sie unter [The Role of the Claim Rule Language](../../ad-fs/technical-reference/The-Role-of-the-Claim-Rule-Language.md).  
  
Sie können das folgende Verfahren zum Erstellen einer Anspruchsregel mithilfe der AD FS-Verwaltungs-Snap\-in.  
  
Mitgliedschaft in **Administratoren**, oder einer entsprechenden, auf dem lokalen Computer die Mindestanforderung zum Ausführen dieses Verfahrens.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).



## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>Erstellen Sie eine Regel, um die pass-through oder Filtern eines eingehenden Anspruchs auf a Relying Party Trust in Windows Server 2016 

1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  Rechts\-klicken Sie auf der ausgewählten Vertrauensstellung, und klicken Sie dann auf **Anspruchsausstellungsrichtlinie bearbeiten**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  In der **Anspruchsausstellungsrichtlinie bearbeiten** Dialogfeld **Ausstellungstransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **Ansprüche mit benutzerdefinierter Regel senden** aus der Liste aus, und klicken Sie dann auf **Weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom3.PNG)   
  
6.  Auf der **Regel konfigurieren** Seite **anspruchsregelname**, geben Sie den Anzeigenamen für diese Regel. Klicken Sie unter **benutzerdefinierte Regel**geben oder fügen Sie die Anspruchsregel-Sprachsyntax, die Sie für diese Regel verwenden möchten.  
![Regel erstellen](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom4.PNG)     

7.  Klicken Sie auf **Fertig stellen**.  
  
8.  In der **Edit Claim Rules** Dialogfeld klicken Sie auf **OK** um die Regel zu speichern.   
  
## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>Erstellen Sie eine Regel, um die pass-through oder Filtern eines eingehenden Anspruchs auf eine Anspruchsanbieter-Vertrauensstellung in Windows Server 2016 
  
1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  Rechts\-klicken Sie auf der ausgewählten Vertrauensstellung, und klicken Sie dann auf **Edit Claim Rules**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  In der **Edit Claim Rules** Dialogfeld **Akzeptanztransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **Ansprüche mit benutzerdefinierter Regel senden** aus der Liste aus, und klicken Sie dann auf **Weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom3.PNG)   
  
6.  Auf der **Regel konfigurieren** Seite **anspruchsregelname**, geben Sie den Anzeigenamen für diese Regel. Klicken Sie unter **benutzerdefinierte Regel**geben oder fügen Sie die Anspruchsregel-Sprachsyntax, die Sie für diese Regel verwenden möchten.  
![Regel erstellen](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom4.PNG)     

7.  Klicken Sie auf **Fertig stellen**.  
  
8.  In der **Edit Claim Rules** Dialogfeld klicken Sie auf **OK** um die Regel zu speichern.   

















   
  
## <a name="to-create-a-rule-to-send-claims-by-using-a-custom-claim-in-windows-server-2012-r2"></a>Erstellen Sie eine Regel, um Ansprüche zu senden, indem Sie einen benutzerdefinierten Anspruch in Windows Server 2012 R2 
  
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
  
5.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **Ansprüche mit benutzerdefinierter Regel senden** aus der Liste aus, und klicken Sie dann auf **Weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom1.PNG)   
  
6.  Auf der **Regel konfigurieren** Seite **anspruchsregelname**, geben Sie den Anzeigenamen für diese Regel. Klicken Sie unter **benutzerdefinierte Regel**geben oder fügen Sie die Anspruchsregel-Sprachsyntax, die Sie für diese Regel verwenden möchten.  
![Regel erstellen](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom2.PNG)     

7.  Klicken Sie auf **Fertig stellen**.  
  
8.  In der **Edit Claim Rules** Dialogfeld klicken Sie auf **OK** um die Regel zu speichern.  

## <a name="additional-references"></a>Weitere Verweise 
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  
 
[Prüfliste: Erstellen von Anspruchsregeln für eine Vertrauensstellung der vertrauenden Seite](https://technet.microsoft.com/library/ee913578.aspx)  

[Prüfliste: Erstellen von Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung](https://technet.microsoft.com/library/ee913564.aspx)  
  
[Wenn Use an Authorization Claim Rule](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Die Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Die Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
