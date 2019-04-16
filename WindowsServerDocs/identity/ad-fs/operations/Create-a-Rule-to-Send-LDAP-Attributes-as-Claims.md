---
ms.assetid: 66664b80-2590-46c0-bfca-82402088e42c
title: "Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e9762e4bc50a1c2b862999af5269a0da376ec9a1
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-rule-to-send-ldap-attributes-as-claims"></a>Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche

>Gilt für: Windows Server 2016, Windows Server2012 R2

Das Senden von LDAP-Attributen als Ansprüche Regelvorlage in Active Directory Federation Services \(AD FS\) verwenden, können Sie eine Regel erstellen, die Attribute aus einem Attributspeicher Lightweight Directory Access Protocol \(LDAP\) wie z.B. Active Directory, senden als Ansprüche an die vertrauende Seite ausgewählt wird. Angenommen, Sie können diese Regelvorlage a Send LDAP Attributes erstellt wie Ansprüche Regel extrahiert, die Attributwerte für authentifizierte Benutzer aus der **DisplayName** und **TelephoneNumber** Active Directory-Attribute, und klicken Sie dann diese Werte als zwei unterschiedliche ausgehende Ansprüche senden.  
  
Mit dieser Regel können auch Gruppenmitgliedschaften des Benutzers senden. Wenn Sie nur einzelne Gruppenmitgliedschaften senden möchten, verwenden Sie das Versenden der Gruppenmitgliedschaft als eine anspruchsregelvorlage. Das folgende Verfahren können zum Erstellen einer Anspruchsregel mit AD FS-Verwaltungs-Snap-In.  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).  

## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-a-relying-party-trust-in-windows-server-2016"></a>Zum Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche für eine der vertrauenden Seite Vertrauensstellung in Windows Server2016 

1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten **. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  Mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Anspruch Ausstellungsrichtlinie bearbeiten **.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  In der **Anspruch Ausstellungsrichtlinie bearbeiten** Dialogfeld unter **Ausstellungstransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **Senden von LDAP-Attributen als Ansprüche** aus der Liste, und klicken Sie dann auf **Weiter **.  
![Erstellen der Regel](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap1.PNG)    

6.  Auf der **Regel konfigurieren** Seite **Name der Anspruchsregel** Geben Sie den Namen für diese Regel ein, wählen die **Attributspeicher**, und wählen Sie dann das LDAP-Attribut und dem ausgehenden Anspruchstyp zuordnen. 
![Erstellen der Regel](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap2.PNG)    

7.  Klicken Sie auf die **Fertig stellen** Schaltfläche.  
  
8.  In der **Anspruchsregeln bearbeiten** Dialogfeld, klicken Sie auf **OK** um die Regel zu speichern.
  
## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-a-claims-provider-trust-in-windows-server-2016"></a>Zum Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche für eine Anspruchsanbieter-Vertrauensstellung in Windows Server2016 
  
1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen **. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  Mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Anspruchsregeln bearbeiten **.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  In der **Anspruchsregeln bearbeiten** Dialogfeld unter **Akzeptanztransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **Senden von LDAP-Attributen als Ansprüche** aus der Liste, und klicken Sie dann auf **Weiter **.  
![Erstellen der Regel](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap1.PNG)       

6.  Auf der **Regel konfigurieren** Seite **Name der Anspruchsregel** Geben Sie den Namen für diese Regel ein, wählen die **Attributspeicher**, und wählen Sie dann das LDAP-Attribut und dem ausgehenden Anspruchstyp zuordnen. 
![Erstellen der Regel](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap2.PNG)      

7.  Klicken Sie auf die **Fertig stellen** Schaltfläche.  
  
8.  In der **Anspruchsregeln bearbeiten** Dialogfeld, klicken Sie auf **OK** um die Regel zu speichern.  

 
  
## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-windows-server-2012-r2"></a>Zum Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche für Windows Server2012 R2  
  
1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD FSAD FS\\Trust Beziehungen**, klicken Sie entweder **Anspruchsanbieter-Vertrauensstellungen** oder **Vertrauensstellungen für vertrauende Seiten**, und klicken Sie dann auf eine bestimmte Vertrauensstellung in der Liste, in denen Sie diese Regel erstellen möchten.  
  
3.  Mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Anspruchsregeln bearbeiten **.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)  
  
4.  In der **Anspruchsregeln bearbeiten** klicken Sie im Dialogfeld Wählen Sie eine der folgenden Registerkarten, abhängig von der Vertrauensstellung, die Sie bearbeiten und welche Regel legen Sie diese Regel in erstellen möchten, und klicken Sie dann auf **Regel hinzufügen** des Assistenten zu starten, die diesen Regelsatz zugeordnet ist:  
  
    -   **Akzeptanztransformationsregeln**  
  
    -   **Ausstellungstransformationsregeln**  
  
    -   **Ausstellungsautorisierungsregeln**  
  
    -   **Autorisierungsregeln**  
![Erstellen der Regel](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG) 
  
5.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **Senden von LDAP-Attributen als Ansprüche** aus der Liste, und klicken Sie dann auf **Weiter **.  
![Erstellen der Regel](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap3.PNG)  
  
6.  Auf der **Regel konfigurieren** Seite **Name der Anspruchsregel** Geben Sie den Anzeigenamen für diese Regel unter **Attributspeicher** wählen **Active Directory**, und wählen Sie unter **Zuordnen von LDAP-Attributen zu ausgehenden Anspruchstypen** wählen Sie den gewünschten **LDAP-Attribut** und die entsprechenden **ausgehenden Anspruchs Typ** Typen aus der Drop\ aufgeführt.  
  
    Sie haben, wählen Sie eine neue LDAP-Attribut und die ausgehenden Anspruchs Typ-Paar in einer anderen Zeile für jedes Active Directory-Attribut, das Ausstellen eines Anspruchs für im Rahmen dieser Regel werden sollen.  
![Erstellen der Regel](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap4.PNG)    
7.  Klicken Sie auf die **Fertig stellen** Schaltfläche.  
  
8.  In der **Anspruchsregeln bearbeiten** Dialogfeld, klicken Sie auf **OK** um die Regel zu speichern.  

## <a name="additional-references"></a>Weitere Verweise 
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  
 
[Prüfliste: Erstellen von Anspruchsregeln für eine Vertrauensstellung der vertrauenden Seite](https://technet.microsoft.com/library/ee913578.aspx)  

[Prüfliste: Erstellen von Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung](https://technet.microsoft.com/library/ee913564.aspx)  
  
[Wann sollte eine Autorisierungsanspruchsregel verwendet](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Die Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Die Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
