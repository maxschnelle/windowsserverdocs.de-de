---
ms.assetid: 96b9f4e6-f01c-4517-8299-017d187d447e
title: Erstellen einer Regel zum Senden eines Authentifizierungsmethodenanspruchs
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4065a61e042f52298da656899289e718e010f932
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-rule-to-send-an-authentication-method-claim"></a>Erstellen einer Regel zum Senden eines Authentifizierungsmethodenanspruchs

>Gilt für: Windows Server 2016, Windows Server2012 R2

Verwenden Sie entweder die **Senden der Gruppenmitgliedschaft als Ansprüche** Regelvorlage oder die **Transformieren eines eingehenden Anspruchs** Regelvorlage zum Senden eines authentifizierungsmethodenanspruchs. Ein authentifizierungsmethodenanspruchs können die vertrauende Seite um den Mechanismus für die Anmeldung zu bestimmen, den der Benutzer verwendet wird, zu authentifizieren und Ansprüche vom Active Directory Federation Services \(AD FS\) erhalten. Sie können auch das Feature zur Authentifizierungsmechanismussicherung von Active Directory Federation Services \(AD FS\) in Windows Server2012 R2 als Eingabe Authentifizierung Methode Ansprüche für Situationen zu generieren, in dem die vertrauende Seite möchte, dass die Zugriffsebene bestimmt, der basierend auf der Smartcard-Anmeldung, verwenden. Beispielsweise kann Entwickler verschiedene Zugriffsebenen Verbundbenutzer der relying Party Anwendung zuweisen. Die Zugriffsebenen sind davon abhängig, ob der Benutzer mit ihren Namen und das Kennwort Benutzeranmeldeinformationen, im Gegensatz zu Smartcards anmelden.  
  
Abhängig von den Anforderungen Ihrer Organisation verwenden Sie eines der folgenden Verfahren:  
  
-   Erstellen Sie mit dieser Regel mithilfe der **Senden der Gruppenmitgliedschaft als Ansprüche** Regelvorlage \-Sie können diese Regelvorlage verwenden, wenn die Gruppe an, die Sie angeben, die in dieser Vorlage zu bestimmen, welche Authentifizierungsmethode letztendlich Anspruch ausgestellt werden sollen.  
  
-   Erstellen Sie mit dieser Regel mithilfe der **Transformieren eines eingehenden Anspruchs** Regelvorlage \-Sie können diese Regelvorlage verwenden, um die vorhandene Authentifizierungsmethode in eine neue Authentifizierungsmethode zu ändern, das mit einem Produkt kompatibel ist, die Standard-Methode Ansprüche für AD FS-Authentifizierung nicht erkennt.  
  


## <a name="to-create-by-using-the-send-group-membership-as-claims-rule-template-on-a-relying-party-trust-in-windows-server-2016"></a>Erstellen Sie mithilfe der Gruppenmitgliedschaft senden als Ansprüche Regelvorlage auf eine der vertrauenden Seite Vertrauensstellung in Windows Server2016 

1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten **. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  Mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Anspruch Ausstellungsrichtlinie bearbeiten **.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  In der **Anspruch Ausstellungsrichtlinie bearbeiten** Dialogfeld unter **Ausstellungstransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **Senden der Gruppenmitgliedschaft als Anspruch** aus der Liste, und klicken Sie dann auf **Weiter**.  
![Erstellen der Regel](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)      

6.  Auf der **Regel konfigurieren** geben einen Name der Anspruchsregel.  
  
7.  Klicken Sie auf **Durchsuchen**, wählen Sie die Gruppe, deren Mitglieder dieser authentifizierungsmethodenanspruchs empfangen soll, und klicken Sie dann auf **OK**.  
  
8.  In **ausgehenden Anspruchstyp**Option **Authentifizierungsmethode** in der Liste.  
  
9. In **ausgehenden Anspruchswert**, geben Sie einen uniform Resource Identifier \(URI\) Standardwerte in der folgenden Tabelle, je nach Ihrer bevorzugten Authentifizierungsmethode, klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  
  
|Aktuelle Authentifizierungsmethode|Entsprechende URI|  
|--------------------------------|---------------------|  
|Benutzernamen- und Kennwort|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows-Authentifizierung|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|Transport Layer Security \(TLS\) gegenseitige Authentifizierung, der x. 509-Zertifikate verwendet.|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|X.509\-basierte Authentifizierung, die TLS nicht verwendet|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![Erstellen der Regel](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth2.PNG)
  
## <a name="to-create-by-using-the-send-group-membership-as-claims-rule-template-on-a-claims-provider-trust-in-windows-server-2016"></a>Erstellen Sie mithilfe der Gruppenmitgliedschaft senden als Ansprüche-Vorlage auf einer Anspruchsanbieter-Vertrauensstellung in Windows Server2016 
  
1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen **. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  Mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Anspruchsregeln bearbeiten **.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  In der **Anspruchsregeln bearbeiten** Dialogfeld unter **Akzeptanztransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **Senden der Gruppenmitgliedschaft als Anspruch** aus der Liste, und klicken Sie dann auf **Weiter**.  
![Erstellen der Regel](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)     

6.  Auf der **Regel konfigurieren** geben einen Name der Anspruchsregel.  
  
7.  Klicken Sie auf **Durchsuchen**, wählen Sie die Gruppe, deren Mitglieder dieser authentifizierungsmethodenanspruchs empfangen soll, und klicken Sie dann auf **OK**.  
  
8.  In **ausgehenden Anspruchstyp**Option **Authentifizierungsmethode** in der Liste.  
  
9. In **ausgehenden Anspruchswert**, geben Sie einen uniform Resource Identifier \(URI\) Standardwerte in der folgenden Tabelle, je nach Ihrer bevorzugten Authentifizierungsmethode, klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  
  
|Aktuelle Authentifizierungsmethode|Entsprechende URI|  
|--------------------------------|---------------------|  
|Benutzernamen- und Kennwort|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows-Authentifizierung|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|Transport Layer Security \(TLS\) gegenseitige Authentifizierung, der x. 509-Zertifikate verwendet.|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|X.509\-basierte Authentifizierung, die TLS nicht verwendet|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![Erstellen der Regel](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth2.PNG)


## <a name="to-create-this-rule-by-using-the-transform-an-incoming-claim-rule-template-on-a-relying-party-trust-in-windows-server-2016"></a>Um diese Regel erstellen, mit der Transformation ein eingehender Anspruch auf eine der vertrauenden Seite Vertrauensstellung in Windows Server2016-Vorlage 

1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten **. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  Mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Anspruch Ausstellungsrichtlinie bearbeiten **.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  In der **Anspruch Ausstellungsrichtlinie bearbeiten** Dialogfeld unter **Ausstellungstransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **Transformieren eines eingehenden Anspruchs** aus der Liste, und klicken Sie dann auf **Weiter **.  
![Erstellen der Regel](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)      

6.  Auf der **Regel konfigurieren** geben einen Name der Anspruchsregel.  
  
7.  In **eingehender Anspruchstyp**Option **Authentifizierungsmethode** in der Liste.  
  
8.  In **ausgehenden Anspruchstyp**Option **Authentifizierungsmethode** in der Liste.  
  
9. Wählen Sie **ersetzen Sie einen eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert**, und führen Sie die folgenden:  
  
    1.  In **eingehender Anspruchswert**, geben Sie den folgenden URI-Werte, die auf die aktuelle Authentifizierungsmethode URI basieren, die ursprünglich verwendet wurde, klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  
  
    2.  In **ausgehenden Anspruchswert**, geben Sie einen URI Standardwerte in der folgenden Tabelle, in der Programmiersprache Methode bevorzugte Authentifizierung abhängt, klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  
  
|Aktuelle Authentifizierungsmethode|Entsprechende URI|  
|--------------------------------|---------------------|  
|Benutzernamen- und Kennwort|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows-Authentifizierung|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|TLS gegenseitige Authentifizierung, der x. 509-Zertifikate verwendet.|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|X.509\-basierte Authentifizierung, die TLS nicht verwendet|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![Erstellen der Regel](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth4.PNG)
  
> [!NOTE]  
> Zusätzlich zu den Werten in der Tabelle können andere URI-Werte verwendet werden. Die URI-Werte, die von einer einfinger angezeigt werden in der vorherige Tabelle entsprechen die URIs, die die vertrauende Seite standardmäßig akzeptiert.  

## <a name="to-create-this-rule-by-using-the-transform-an-incoming-claim-rule-template-on-a-claims-provider-trust-in-windows-server-2016"></a>Um diese Regel erstellen, mit der Transformation ein eingehender Anspruch auf eine Anspruchsanbieter-Vertrauensstellung in Windows Server2016-Vorlage 
  
1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen **. 
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  Mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Anspruchsregeln bearbeiten **.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  In der **Anspruchsregeln bearbeiten** Dialogfeld unter **Akzeptanztransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten.
![Erstellen der Regel](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **Transformieren eines eingehenden Anspruchs** aus der Liste, und klicken Sie dann auf **Weiter **.  
![Erstellen der Regel](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)      

6.  Auf der **Regel konfigurieren** geben einen Name der Anspruchsregel.  
  
7.  In **eingehender Anspruchstyp**Option **Authentifizierungsmethode** in der Liste.  
  
8.  In **ausgehenden Anspruchstyp**Option **Authentifizierungsmethode** in der Liste.  
  
9. Wählen Sie **ersetzen Sie einen eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert**, und führen Sie die folgenden:  
  
    1.  In **eingehender Anspruchswert**, geben Sie den folgenden URI-Werte, die auf die aktuelle Authentifizierungsmethode URI basieren, die ursprünglich verwendet wurde, klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  
  
    2.  In **ausgehenden Anspruchswert**, geben Sie einen URI Standardwerte in der folgenden Tabelle, in der Programmiersprache Methode bevorzugte Authentifizierung abhängt, klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  
  
|Aktuelle Authentifizierungsmethode|Entsprechende URI|  
|--------------------------------|---------------------|  
|Benutzernamen- und Kennwort|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows-Authentifizierung|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|TLS gegenseitige Authentifizierung, der x. 509-Zertifikate verwendet.|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|X.509\-basierte Authentifizierung, die TLS nicht verwendet|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![Erstellen der Regel](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth4.PNG)























## <a name="to-create-this-rule-by-using-the-send-group-membership-as-claims-rule-template-in-windows-server-2012-r2"></a>Zum Erstellen dieser Regel mithilfe der Gruppenmitgliedschaft senden als Ansprüche Regelvorlage in Windows Server2012 R2  
  
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
  
6.  Auf der **Regel konfigurieren** geben einen Name der Anspruchsregel.  
  
7.  Klicken Sie auf **Durchsuchen**, wählen Sie die Gruppe, deren Mitglieder dieser authentifizierungsmethodenanspruchs empfangen soll, und klicken Sie dann auf **OK**.  
  
8.  In **ausgehenden Anspruchstyp**Option **Authentifizierungsmethode** in der Liste.  
  
9. In **ausgehenden Anspruchswert**, geben Sie einen uniform Resource Identifier \(URI\) Standardwerte in der folgenden Tabelle, je nach Ihrer bevorzugten Authentifizierungsmethode, klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  
  
|Aktuelle Authentifizierungsmethode|Entsprechende URI|  
|--------------------------------|---------------------|  
|Benutzernamen- und Kennwort|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows-Authentifizierung|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|Transport Layer Security \(TLS\) gegenseitige Authentifizierung, der x. 509-Zertifikate verwendet.|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|X.509\-basierte Authentifizierung, die TLS nicht verwendet|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![Erstellen der Regel](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth1.PNG)
 
> [!NOTE]  
> Zusätzlich zu den Werten in der Tabelle können andere URI-Werte verwendet werden. Die URI-Werte, die in der obigen Tabelle aufgeführt sind entsprechend die URIs, die die vertrauende Seite standardmäßig akzeptiert.  
  
## <a name="to-create-this-rule-by-using-the-transform-an-incoming-claim-rule-template-in-windows-server-2012-r2"></a>Zum Erstellen dieser Regel mithilfe der Transformation einer eingehenden Anspruchs-Vorlage in Windows Server2012 R2  
   
  
  
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
  
6.  Auf der **Regel konfigurieren** geben einen Name der Anspruchsregel.  
  
7.  In **eingehender Anspruchstyp**Option **Authentifizierungsmethode** in der Liste.  
  
8.  In **ausgehenden Anspruchstyp**Option **Authentifizierungsmethode** in der Liste.  
  
9. Wählen Sie **ersetzen Sie einen eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert**, und führen Sie die folgenden:  
  
    1.  In **eingehender Anspruchswert**, geben Sie den folgenden URI-Werte, die auf die aktuelle Authentifizierungsmethode URI basieren, die ursprünglich verwendet wurde, klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  
  
    2.  In **ausgehenden Anspruchswert**, geben Sie einen URI Standardwerte in der folgenden Tabelle, in der Programmiersprache Methode bevorzugte Authentifizierung abhängt, klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  
  
|Aktuelle Authentifizierungsmethode|Entsprechende URI|  
|--------------------------------|---------------------|  
|Benutzernamen- und Kennwort|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows-Authentifizierung|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|TLS gegenseitige Authentifizierung, der x. 509-Zertifikate verwendet.|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|X.509\-basierte Authentifizierung, die TLS nicht verwendet|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![Erstellen der Regel](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth3.PNG)
  
> [!NOTE]  
> Zusätzlich zu den Werten in der Tabelle können andere URI-Werte verwendet werden. Die URI-Werte, die von einer einfinger angezeigt werden in der vorherige Tabelle entsprechen die URIs, die die vertrauende Seite standardmäßig akzeptiert.  

## <a name="additional-references"></a>Weitere Verweise 
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  
 
[Prüfliste: Erstellen von Anspruchsregeln für eine Vertrauensstellung der vertrauenden Seite](https://technet.microsoft.com/library/ee913578.aspx)  

[Prüfliste: Erstellen von Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung](https://technet.microsoft.com/library/ee913564.aspx)  
  
[Wann sollte eine Autorisierungsanspruchsregel verwendet](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Die Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Die Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
