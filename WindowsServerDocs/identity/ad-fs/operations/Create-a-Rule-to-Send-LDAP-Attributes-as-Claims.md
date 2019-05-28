---
ms.assetid: 66664b80-2590-46c0-bfca-82402088e42c
title: Erstellen Sie eine Regel zum Senden von LDAP-Attributen als Ansprüche
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 00ea4f9f868b9c82c2a0859be971db26394251a3
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189352"
---
# <a name="create-a-rule-to-send-ldap-attributes-as-claims"></a>Erstellen Sie eine Regel zum Senden von LDAP-Attributen als Ansprüche


Verwenden das Senden von LDAP-Attributen als Ansprüche Regelvorlage in Active Directory-Verbunddienste \(AD FS\), Sie können eine Regel, die Attribute aus einem Lightweight Directory Access Protocol auswählen erstellen \(LDAP\)-Attributspeicher wie Active Directory als Ansprüche an die vertrauende Seite gesendet. Angenommen, Sie können diese Regelvorlage um a Send LDAP Attributes zu erstellen, wie Ansprüche Regel extrahiert, die Attributwerte für authentifizierte Benutzer aus der **"DisplayName"** und **"telephoneNumber"** Active Directory Attribute, und klicken Sie dann diese Werte als zwei unterschiedliche ausgehende Ansprüche senden.  
  
Mit dieser Regel können Sie auch alle Gruppenmitgliedschaften des Benutzers senden. Wenn Sie nur einzelne Gruppenmitgliedschaften senden möchten, verwenden Sie die Regelvorlage „Gruppenmitgliedschaft als Anspruch senden“. Sie können das folgende Verfahren zum Erstellen einer Anspruchsregel mit der AD FS-Verwaltungs-Snap\-in.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).  

## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-a-relying-party-trust-in-windows-server-2016"></a>Zum Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche für a Relying Party Trust in Windows Server 2016 

1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  Rechts\-klicken Sie auf der ausgewählten Vertrauensstellung, und klicken Sie dann auf **Anspruchsausstellungsrichtlinie bearbeiten**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  In der **Anspruchsausstellungsrichtlinie bearbeiten** Dialogfeld **Ausstellungstransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **LDAP-Attributen als Ansprüche senden** aus der Liste aus, und klicken Sie dann auf **Weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap1.PNG)    

6.  Auf der **Regel konfigurieren** Seite **anspruchsregelname** Geben Sie den Anzeigenamen für diese Regel wählen die **Attribut Store**, und wählen Sie das LDAP-Attribut, und ordnen Sie es der Typ des ausgehenden Anspruchs. 
![Regel erstellen](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap2.PNG)    

7.  Klicken Sie auf die **Fertig stellen** Schaltfläche.  
  
8.  In der **Edit Claim Rules** Dialogfeld klicken Sie auf **OK** um die Regel zu speichern.
  
## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-a-claims-provider-trust-in-windows-server-2016"></a>Zum Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche für eine Anspruchsanbieter-Vertrauensstellung in Windows Server 2016 
  
1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  Rechts\-klicken Sie auf der ausgewählten Vertrauensstellung, und klicken Sie dann auf **Edit Claim Rules**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  In der **Edit Claim Rules** Dialogfeld **Akzeptanztransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **LDAP-Attributen als Ansprüche senden** aus der Liste aus, und klicken Sie dann auf **Weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap1.PNG)       

6.  Auf der **Regel konfigurieren** Seite **anspruchsregelname** Geben Sie den Anzeigenamen für diese Regel wählen die **Attribut Store**, und wählen Sie das LDAP-Attribut, und ordnen Sie es der Typ des ausgehenden Anspruchs. 
![Regel erstellen](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap2.PNG)      

7.  Klicken Sie auf die **Fertig stellen** Schaltfläche.  
  
8.  In der **Edit Claim Rules** Dialogfeld klicken Sie auf **OK** um die Regel zu speichern.  

 
  
## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-windows-server-2012-r2"></a>Zum Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche für Windows Server 2012 R2  
  
1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **FSAD für AD FS\\Vertrauensstellungen**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen** oder **Vertrauensstellungen für vertrauende Seiten**, und klicken Sie dann auf eine bestimmte Vertrauensstellung in der Liste, die zum Erstellen dieser Regel werden sollen.  
  
3.  Rechts\-klicken Sie auf der ausgewählten Vertrauensstellung, und klicken Sie dann auf **Edit Claim Rules**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)  
  
4.  In der **Edit Claim Rules** im Dialogfeld Wählen Sie eine der folgenden Registerkarten, abhängig von der Vertrauensstellung, die Sie bearbeiten und welche Regel legen Sie diese Regel in erstellen möchten, und klicken Sie dann auf **Regel hinzufügen** um die Regel zu starten. Legen Sie den Assistenten, der dieser Regel zugeordnet ist:  
  
    -   **Akzeptanztransformationsregeln**  
  
    -   **Ausstellungstransformationsregeln**  
  
    -   **Ausstellungsautorisierungsregeln**  
  
    -   **Autorisierungsregeln**  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG) 
  
5.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **LDAP-Attributen als Ansprüche senden** aus der Liste aus, und klicken Sie dann auf **Weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap3.PNG)  
  
6.  Auf der **Regel konfigurieren** Seite **anspruchsregelname** Geben Sie den Anzeigenamen für diese Regel unter **Attributspeicher** wählen **Active Directory**, und wählen Sie unter **Zuordnen von LDAP-Attributen zu ausgehenden Anspruchstypen** wählen Sie den gewünschten **LDAP-Attribut** und entsprechenden **ausgehenden Anspruchstyp** die Typen aus der Dropdownliste\-unten aufgelistet.  
  
    Sie müssen wählen Sie eine neue LDAP-Attribut und den ausgehenden Anspruch Typ-Paar in einer anderen Zeile für jedes Active Directory-Attribut, die einen Anspruch für als Teil dieser Regel ausgegeben werden sollen.  
![Regel erstellen](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap4.PNG)    
7.  Klicken Sie auf die **Fertig stellen** Schaltfläche.  
  
8.  In der **Edit Claim Rules** Dialogfeld klicken Sie auf **OK** um die Regel zu speichern.  

## <a name="additional-references"></a>Weitere Verweise 
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  
 
[Prüfliste: Erstellen von Anspruchsregeln für eine Vertrauensstellung der vertrauenden Seite](https://technet.microsoft.com/library/ee913578.aspx)  

[Prüfliste: Erstellen von Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung](https://technet.microsoft.com/library/ee913564.aspx)  
  
[Wenn Use an Authorization Claim Rule](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
