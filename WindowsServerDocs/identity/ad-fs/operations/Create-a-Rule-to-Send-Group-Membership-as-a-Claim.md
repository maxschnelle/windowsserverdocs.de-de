---
ms.assetid: 475e34f9-9399-43f4-a840-9dd77258e11a
title: Erstellen einer Regel zum Senden der Gruppenmitgliedschaft als Anspruch
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d4fb03de9de2dcca36b18ce089db11ed599de820
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-rule-to-send-group-membership-as-a-claim"></a>Erstellen einer Regel zum Senden der Gruppenmitgliedschaft als Anspruch

>Gilt für: Windows Server 2016, Windows Server2012 R2

Das Versenden der Gruppenmitgliedschaft als eine anspruchsregelvorlage in Active Directory Federation Services \(AD FS\) verwenden, können Sie eine Regel erstellen, die sie zum Auswählen einer Active Directory-Sicherheitsgruppe als Anspruch senden erlauben. Von dieser Regel, die auf der Grundlage der Gruppe, die Sie auswählen, wird nur ein einzelner Anspruch ausgegeben werden. Beispielsweise können Sie diese Regelvorlage zum Erstellen einer Regel, die einen Gruppenanspruch mit dem Wert der Administrator senden, wenn der Benutzer ein Mitglied der Sicherheitsgruppe "Domänen-Admins" ist. Diese Regel sollte nur für Benutzer in der lokalen Active Directory-Domäne verwendet werden.  
  
Das folgende Verfahren können zum Erstellen einer Anspruchsregel mit AD FS-Verwaltungs-Snap-In.  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   

## <a name="to-create-a-rule-to-send-group-membership-as-a-claim-on-a-relying-party-trust-in-windows-server-2016"></a>Zum Erstellen einer Regel zum Senden der Gruppenmitgliedschaft als Anspruch auf eine der vertrauenden Seite Vertrauensstellung in Windows Server2016 

1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten **. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  Mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Anspruch Ausstellungsrichtlinie bearbeiten **.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  In der **Anspruch Ausstellungsrichtlinie bearbeiten** Dialogfeld unter **Ausstellungstransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **Senden der Gruppenmitgliedschaft als Anspruch** aus der Liste, und klicken Sie dann auf **Weiter**.  
![Erstellen der Regel](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)      

6.   Auf der **Regel konfigurieren** Seite **Name der Anspruchsregel** Geben Sie den Namen für diese Regel **Gruppe des Benutzers** klicken Sie auf **Durchsuchen** und wählen Sie eine Gruppe, unter **ausgehenden Anspruchstyp** wählen Sie den gewünschten Anspruchstyp, und klicken Sie dann unter **ausgehenden Anspruchs Typ** Geben Sie einen Wert.
![Erstellen der Regel](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group4.PNG)   

7.  Klicken Sie auf die **Fertig stellen** Schaltfläche.  
  
8.  In der **Anspruchsregeln bearbeiten** Dialogfeld, klicken Sie auf **OK** um die Regel zu speichern.
  
## <a name="to-create-a-rule-to-to-send-group-membership-as-a-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>Zum Erstellen einer Regel zum Senden der Gruppenmitgliedschaft als Anspruch auf eine Anspruchsanbieter-Vertrauensstellung in Windows Server2016 
  
1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen **. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  Mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Anspruchsregeln bearbeiten **.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  In der **Anspruchsregeln bearbeiten** Dialogfeld unter **Akzeptanztransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **Senden der Gruppenmitgliedschaft als Anspruch** aus der Liste, und klicken Sie dann auf **Weiter**.  
![Erstellen der Regel](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)     

6.   Auf der **Regel konfigurieren** Seite **Name der Anspruchsregel** Geben Sie den Namen für diese Regel **Gruppe des Benutzers** klicken Sie auf **Durchsuchen** und wählen Sie eine Gruppe, unter **ausgehenden Anspruchstyp** wählen Sie den gewünschten Anspruchstyp, und klicken Sie dann unter **ausgehenden Anspruchs Typ** Geben Sie einen Wert. 
![Erstellen der Regel](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group4.PNG)      

7.  Klicken Sie auf die **Fertig stellen** Schaltfläche.  
  
8.  In der **Anspruchsregeln bearbeiten** Dialogfeld, klicken Sie auf **OK** um die Regel zu speichern.  




  
## <a name="to-create-a-rule-to-send-group-membership-as-a-claim-in-windows-server-2012-r2"></a>Zum Erstellen einer Regel zum Senden der Gruppenmitgliedschaft als Anspruch in Windows Server2012 R2 
  
1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD FS\\Trust Beziehungen**, klicken Sie entweder **Anspruchsanbieter-Vertrauensstellungen** oder **Vertrauensstellungen für vertrauende Seiten**, und klicken Sie dann auf eine bestimmte Vertrauensstellung in der Liste, in denen Sie diese Regel erstellen möchten.  
  
3.  Mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Anspruchsregeln bearbeiten **.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)  
  
4.  In der **Anspruchsregeln bearbeiten** klicken Sie im Dialogfeld Wählen Sie eine der folgenden Registerkarten, abhängig von der Vertrauensstellung, die Sie bearbeiten und welche Regel legen Sie diese Regel in erstellen möchten, und klicken Sie dann auf **Regel hinzufügen** des Assistenten zu starten, die diesen Regelsatz zugeordnet ist:  
  
    -   **Akzeptanztransformationsregeln**  
  
    -   **Ausstellungstransformationsregeln**  
  
    -   **Ausstellungsautorisierungsregeln**  
  
    -   **Autorisierungsregeln**  
![Erstellen der Regel](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)
    
5.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **Senden der Gruppenmitgliedschaft als Anspruch** aus der Liste, und klicken Sie dann auf **Weiter**.  
![Erstellen der Regel](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group1.PNG)

6.  Auf der **Regel konfigurieren** Seite **Name der Anspruchsregel** Geben Sie den Namen für diese Regel **Gruppe des Benutzers** klicken Sie auf **Durchsuchen** und wählen Sie eine Gruppe, unter **ausgehenden Anspruchstyp** wählen Sie den gewünschten Anspruchstyp, und klicken Sie dann unter **ausgehenden Anspruchs Typ** Geben Sie einen Wert.  
![Erstellen der Regel](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group2.PNG)  

7.  Klicken Sie auf **Fertig stellen**.  
  
8.  In der **Anspruchsregeln bearbeiten** Dialogfeld, klicken Sie auf **OK** um die Regel zu speichern.  



## <a name="additional-references"></a>Weitere Verweise 
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  
 
[Prüfliste: Erstellen von Anspruchsregeln für eine Vertrauensstellung der vertrauenden Seite](https://technet.microsoft.com/library/ee913578.aspx)  

[Prüfliste: Erstellen von Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung](https://technet.microsoft.com/library/ee913564.aspx)  
  
[Wann sollte eine Autorisierungsanspruchsregel verwendet](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Die Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Die Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
