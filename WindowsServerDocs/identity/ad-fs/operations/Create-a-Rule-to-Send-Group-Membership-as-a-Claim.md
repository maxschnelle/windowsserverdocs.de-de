---
ms.assetid: 475e34f9-9399-43f4-a840-9dd77258e11a
title: Erstellen einer Regel zum Senden der Gruppenmitgliedschaft als Anspruch
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 96ab653393fbc5f0a4306db53f84c2d9ba6c7f5f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847451"
---
# <a name="create-a-rule-to-send-group-membership-as-a-claim"></a>Erstellen einer Regel zum Senden der Gruppenmitgliedschaft als Anspruch

>Gilt für: Windows Server 2016, Windows Server 2012 R2

Verwenden das Versenden der Gruppenmitgliedschaft als eine anspruchsregelvorlage in Active Directory-Verbunddienste \(AD FS\), Sie können eine Regel, die Sie auswählen, eine Active Directory-Sicherheitsgruppe als Anspruch senden erleichtern wird erstellen. Von dieser Regel, die auf Grundlage der Gruppe, die Sie auswählen, wird nur ein einzelner Anspruch ausgegeben werden. Beispielsweise können Sie diese Regelvorlage zum Erstellen einer Regel, die einen Gruppenanspruch mit dem Wert des Admin Center senden, wenn der Benutzer ein Mitglied der Sicherheitsgruppe "Domänen-Admins" ist. Diese Regel sollte nur für Benutzer in der lokalen Active Directory-Domäne verwendet werden.  
  
Sie können das folgende Verfahren zum Erstellen einer Anspruchsregel mit der AD FS-Verwaltungs-Snap\-in.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   

## <a name="to-create-a-rule-to-send-group-membership-as-a-claim-on-a-relying-party-trust-in-windows-server-2016"></a>Zum Erstellen einer Regel zum Senden der Gruppenmitgliedschaft als Anspruch auf a Relying Party Trust in Windows Server 2016 

1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  Rechts\-klicken Sie auf der ausgewählten Vertrauensstellung, und klicken Sie dann auf **Anspruchsausstellungsrichtlinie bearbeiten**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  In der **Anspruchsausstellungsrichtlinie bearbeiten** Dialogfeld **Ausstellungstransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **Senden der Gruppenmitgliedschaft als Anspruch** aus der Liste aus, und klicken Sie dann auf **Weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)      

6.   Auf der **Regel konfigurieren** Seite **anspruchsregelname** Geben Sie den Anzeigenamen für diese Regel in **Gruppe des Benutzers** klicken Sie auf **Durchsuchen** , und wählen Sie eine unter Gruppe **Typ des ausgehenden Anspruchs** wählen Sie den gewünschten Anspruchstyp "", und klicken Sie dann unter **ausgehenden Anspruchstyp** Geben Sie einen Wert.
![Regel erstellen](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group4.PNG)   

7.  Klicken Sie auf die **Fertig stellen** Schaltfläche.  
  
8.  In der **Edit Claim Rules** Dialogfeld klicken Sie auf **OK** um die Regel zu speichern.
  
## <a name="to-create-a-rule-to-send-group-membership-as-a-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>Zum Erstellen einer Regel zum Senden der Gruppenmitgliedschaft als Anspruch auf eine Anspruchsanbieter-Vertrauensstellung in Windows Server 2016 
  
1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  Rechts\-klicken Sie auf der ausgewählten Vertrauensstellung, und klicken Sie dann auf **Edit Claim Rules**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  In der **Edit Claim Rules** Dialogfeld **Akzeptanztransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **Senden der Gruppenmitgliedschaft als Anspruch** aus der Liste aus, und klicken Sie dann auf **Weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)     

6.   Auf der **Regel konfigurieren** Seite **anspruchsregelname** Geben Sie den Anzeigenamen für diese Regel in **Gruppe des Benutzers** klicken Sie auf **Durchsuchen** , und wählen Sie eine unter Gruppe **Typ des ausgehenden Anspruchs** wählen Sie den gewünschten Anspruchstyp "", und klicken Sie dann unter **ausgehenden Anspruchstyp** Geben Sie einen Wert. 
![Regel erstellen](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group4.PNG)      

7.  Klicken Sie auf die **Fertig stellen** Schaltfläche.  
  
8.  In der **Edit Claim Rules** Dialogfeld klicken Sie auf **OK** um die Regel zu speichern.  




  
## <a name="to-create-a-rule-to-send-group-membership-as-a-claim-in-windows-server-2012-r2"></a>Zum Erstellen einer Regel zum Senden der Gruppenmitgliedschaft als Anspruch in Windows Server 2012 R2 
  
1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **AD FS\\Vertrauensstellungen**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen** oder **Vertrauensstellungen für vertrauende Seiten**, und klicken Sie dann auf einen bestimmten Vertrauen Sie in der Liste, die zum Erstellen dieser Regel werden sollen.  
  
3.  Rechts\-klicken Sie auf der ausgewählten Vertrauensstellung, und klicken Sie dann auf **Edit Claim Rules**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)  
  
4.  In der **Edit Claim Rules** im Dialogfeld Wählen Sie eine der folgenden Registerkarten, abhängig von der Vertrauensstellung, die Sie bearbeiten und welche Regel legen Sie diese Regel in erstellen möchten, und klicken Sie dann auf **Regel hinzufügen** um die Regel zu starten. Legen Sie den Assistenten, der dieser Regel zugeordnet ist:  
  
    -   **Akzeptanztransformationsregeln**  
  
    -   **Ausstellungstransformationsregeln**  
  
    -   **Ausstellungsautorisierungsregeln**  
  
    -   **Autorisierungsregeln**  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)
    
5.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **Senden der Gruppenmitgliedschaft als Anspruch** aus der Liste aus, und klicken Sie dann auf **Weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group1.PNG)

6.  Auf der **Regel konfigurieren** Seite **anspruchsregelname** Geben Sie den Anzeigenamen für diese Regel in **Gruppe des Benutzers** klicken Sie auf **Durchsuchen** , und wählen Sie eine unter Gruppe **Typ des ausgehenden Anspruchs** wählen Sie den gewünschten Anspruchstyp "", und klicken Sie dann unter **ausgehenden Anspruchstyp** Geben Sie einen Wert.  
![Regel erstellen](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group2.PNG)  

7.  Klicken Sie auf **Fertig stellen**.  
  
8.  In der **Edit Claim Rules** Dialogfeld klicken Sie auf **OK** um die Regel zu speichern.  



## <a name="additional-references"></a>Weitere Verweise 
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  
 
[Prüfliste: Erstellen von Anspruchsregeln für eine Vertrauensstellung der vertrauenden Seite](https://technet.microsoft.com/library/ee913578.aspx)  

[Prüfliste: Erstellen von Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung](https://technet.microsoft.com/library/ee913564.aspx)  
  
[Wenn Use an Authorization Claim Rule](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Die Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Die Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
