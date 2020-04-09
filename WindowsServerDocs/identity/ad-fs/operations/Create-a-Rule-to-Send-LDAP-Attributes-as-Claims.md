---
ms.assetid: 66664b80-2590-46c0-bfca-82402088e42c
title: Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 6280ee1fb761b154cadb948d18c7b67cb6b8e784
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816653"
---
# <a name="create-a-rule-to-send-ldap-attributes-as-claims"></a>Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche


Mithilfe der Regel Vorlage "LDAP-Attribute als Ansprüche senden" in Active Directory-Verbunddienste (AD FS) \(AD FS\)können Sie eine Regel erstellen, mit der Attribute aus einem Lightweight Directory Access Protocol \(LDAP\)-Attribut Speicher (z. b. Active Directory) ausgewählt werden, die als Ansprüche an die vertrauende Seite gesendet werden. Beispielsweise können Sie diese Regel Vorlage verwenden, um eine Regel zum Senden von LDAP-Attributen als Ansprüche zu erstellen, die Attributwerte für authentifizierte Benutzer aus den Active Directory Attribute **Display Name** und **telefonienumber** extrahiert und diese Werte dann als zwei unterschiedliche ausgehende Ansprüche sendet.  
  
Mit dieser Regel können Sie auch alle Gruppenmitgliedschaften des Benutzers senden. Wenn Sie nur einzelne Gruppenmitgliedschaften senden möchten, verwenden Sie die Regelvorlage „Gruppenmitgliedschaft als Anspruch senden“. Mithilfe des folgenden Verfahrens können Sie eine Anspruchs Regel mit dem AD FS-Verwaltungs-Snap\-in erstellen.  
  
Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).  

## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-a-relying-party-trust-in-windows-server-2016"></a>So erstellen Sie eine Regel zum Senden von LDAP-Attributen als Ansprüche für eine Vertrauensstellung der vertrauenden Seite in Windows Server 2016 

1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  
  
2.  Klicken Sie in der Konsolen Struktur unter **AD FS**auf Vertrauens Stellungen der vertrauenden **Seite**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  Klicken Sie mit der rechten\-auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Anspruchs Ausstellungs Richtlinie bearbeiten**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  Klicken Sie im Dialogfeld **Richtlinie für Anspruchs Ausstellung bearbeiten** unter Ausstellungs **Transformationsregeln** auf **Regel hinzufügen** , um den Regel-Assistenten zu starten. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die Option **LDAP-Attribute als Ansprüche senden** aus der Liste aus, und klicken Sie dann auf **weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap1.PNG)    

6.  Geben Sie auf der Seite **Regel konfigurieren** unter **Anspruchs Regel Name** den anzeigen Amen für diese Regel ein, wählen Sie den **Attribut Speicher**aus, und wählen Sie dann das LDAP-Attribut aus, und ordnen Sie es dem ausgehenden Anspruchstyp zu. 
![Regel erstellen](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap2.PNG)    

7.  Klicken Sie auf **Fertig** stellen.  
  
8.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** auf **OK** , um die Regel zu speichern.
  
## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-a-claims-provider-trust-in-windows-server-2016"></a>So erstellen Sie eine Regel zum Senden von LDAP-Attributen als Ansprüche für eine Anspruchs Anbieter-Vertrauensstellung in Windows Server 2016 
  
1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  
  
2.  Klicken Sie in der Konsolen Struktur unter **AD FS**auf **Anspruchs Anbieter**-Vertrauens Stellungen. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  Klicken Sie mit der rechten\-auf die ausgewählte Vertrauensstellung und dann auf **Anspruchs Regeln bearbeiten**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** unter **Akzeptanz Transformationsregeln** auf **Regel hinzufügen** , um den Regel-Assistenten zu starten.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die Option **LDAP-Attribute als Ansprüche senden** aus der Liste aus, und klicken Sie dann auf **weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap1.PNG)       

6.  Geben Sie auf der Seite **Regel konfigurieren** unter **Anspruchs Regel Name** den anzeigen Amen für diese Regel ein, wählen Sie den **Attribut Speicher**aus, und wählen Sie dann das LDAP-Attribut aus, und ordnen Sie es dem ausgehenden Anspruchstyp zu. 
![Regel erstellen](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap2.PNG)      

7.  Klicken Sie auf **Fertig** stellen.  
  
8.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** auf **OK** , um die Regel zu speichern.  

 
  
## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-windows-server-2012-r2"></a>So erstellen Sie eine Regel zum Senden von LDAP-Attributen als Ansprüche für Windows Server 2012 R2  
  
1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  
  
2.  Klicken Sie in der Konsolen Struktur unter **AD FSAD FS\\Vertrauens**Stellungen auf **Anspruchs Anbieter** -Vertrauens Stellungen oder Vertrauens Stellungen der vertrauenden **Seite**, und klicken Sie dann auf eine bestimmte Vertrauensstellung in der Liste, in der Sie diese Regel erstellen möchten.  
  
3.  Klicken Sie mit der rechten\-auf die ausgewählte Vertrauensstellung und dann auf **Anspruchs Regeln bearbeiten**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)  
  
4.  Wählen Sie im Dialogfeld **Anspruchs Regeln bearbeiten** je nach der zu bearbeitenden Vertrauensstellung und dem Regelsatz, in dem Sie diese Regel erstellen möchten, eine der folgenden Registerkarten aus, und klicken Sie dann auf **Regel hinzufügen** , um den Regel-Assistenten zu starten, der diesem Regelsatz zugeordnet ist:  
  
    -   **Akzeptanz Transformationsregeln**  
  
    -   **Ausstellungs Transformationsregeln**  
  
    -   **Ausstellungs Autorisierungs Regeln**  
  
    -   **Delegierungs Autorisierungs Regeln**  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG) 
  
5.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die Option **LDAP-Attribute als Ansprüche senden** aus der Liste aus, und klicken Sie dann auf **weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap3.PNG)  
  
6.  Geben Sie auf der Seite **Regel konfigurieren** unter **Anspruchs Regel Name** den anzeigen Amen für diese Regel ein, wählen Sie unter **Attribut Speicher** die Option **Active Directory**aus, und wählen Sie unter **Zuordnung von LDAP-Attributen zu ausgehenden Anspruchs Typen** das gewünschte **LDAP-Attribut** und die entsprechenden Typen von **ausgehenden anspruchtypen** aus den\-Dropdown Listen aus.  
  
    Sie müssen für jedes Active Directory Attribut, für das Sie einen Anspruch als Teil dieser Regel ausgeben möchten, ein neues LDAP-Attribut und ein paar für einen ausgehenden Anspruchstyp in einer anderen Zeile auswählen.  
![Regel erstellen](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap4.PNG)    
7.  Klicken Sie auf **Fertig** stellen.  
  
8.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** auf **OK** , um die Regel zu speichern.  

## <a name="additional-references"></a>Weitere Verweise 
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  
 
[Prüfliste: Erstellen von Anspruchs Regeln für eine Vertrauensstellung der vertrauenden](https://technet.microsoft.com/library/ee913578.aspx)  

[Prüfliste: Erstellen von Anspruchs Regeln für eine Anspruchs Anbieter-Vertrauensstellung](https://technet.microsoft.com/library/ee913564.aspx)  
  
[Wann sollte eine Autorisierungs Anspruchs Regel verwendet werden?](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
