---
ms.assetid: 96b9f4e6-f01c-4517-8299-017d187d447e
title: Erstellen einer Regel zum Senden eines Authentifizierungsmethodenanspruchs
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4065a61e042f52298da656899289e718e010f932
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819091"
---
# <a name="create-a-rule-to-send-an-authentication-method-claim"></a>Erstellen einer Regel zum Senden eines Authentifizierungsmethodenanspruchs

>Gilt für: Windows Server 2016, Windows Server 2012 R2

Verwenden Sie entweder die **Send Group Membership als Ansprüche** Regelvorlage oder **Transformieren eines eingehenden Anspruchs** Regelvorlage zum Senden eines authentifizierungsanspruchs-Methode. Die abhängige Partei kann mithilfe ein authentifizierungsanspruchs-Methode bestimmen den Mechanismus für die Benutzeranmeldung, die der Benutzer verwendet wird, zu authentifizieren und Abrufen von Ansprüchen aus Active Directory Federation Services \(AD FS\). Sie können auch die Authentifizierungsmechanismuszusicherung-Funktion von Active Directory Federation Services \(AD FS\) in Windows Server 2012 R2 als Eingabe zum Generieren der Methode authentifizierungsansprüchen für Situationen, in dem die vertrauende Seite Sie möchte die Zugriffsebene zu ermitteln, die auf einer Smartcard-Anmeldungen basiert. Entwickler kann beispielsweise verschiedene Zugriffsebenen Verbundbenutzer, die von der Anwendung der vertrauenden Seite zuweisen. Die Ebenen des Zugriffs hängen davon ab, ob der Benutzer mit ihren Benutzer und Kennwort-Anmeldeinformationen, und ihre Smartcards nicht anmelden.  
  
Verwenden Sie je nach den Anforderungen Ihrer Organisation eine der folgenden Verfahren aus:  
  
-   Erstellen Sie mit dieser Regel mithilfe der **Send Group Membership als Ansprüche** Regelvorlage \- können Sie diese Regelvorlage verwenden, wenn Sie möchten, dass die Gruppe, die Sie in dieser Vorlage angeben, letztlich bestimmen, welche Authentifizierungsmethode Anspruch ausstellen.  
  
-   Erstellen Sie mit dieser Regel mithilfe der **Transformieren eines eingehenden Anspruchs** Regelvorlage \- können Sie diese Regelvorlage verwenden, wenn Sie möchten, um die vorhandene Authentifizierungsmethode in eine neue Authentifizierungsmethode zu ändern, die mit einem Produkt funktioniert nicht erkannt, die standard-Methode Ansprüche für AD FS-Authentifizierung.  
  


## <a name="to-create-by-using-the-send-group-membership-as-claims-rule-template-on-a-relying-party-trust-in-windows-server-2016"></a>So erstellen Sie mit das Versenden der Gruppenmitgliedschaft als Ansprüche Regelvorlage auf a Relying Party Trust in Windows Server 2016 

1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  Rechts\-klicken Sie auf der ausgewählten Vertrauensstellung, und klicken Sie dann auf **Anspruchsausstellungsrichtlinie bearbeiten**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  In der **Anspruchsausstellungsrichtlinie bearbeiten** Dialogfeld **Ausstellungstransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **Senden der Gruppenmitgliedschaft als Anspruch** aus der Liste aus, und klicken Sie dann auf **Weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)      

6.  Auf der **Regel konfigurieren** geben anspruchsregelname.  
  
7.  Klicken Sie auf **Durchsuchen**, wählen Sie die Gruppe, deren Mitglieder erhalten diese Methode authentifizierungsanspruch soll, und klicken Sie dann auf **OK**.  
  
8.  In **Typ des ausgehenden Anspruchs**Option **Authentifizierungsmethode** in der Liste.  
  
9. In **ausgehender Anspruchswert**, geben Sie eine der standardmäßigen uniform Resource Identifier \(URI\) Werte in der folgenden Tabelle, abhängig von der bevorzugten Authentifizierungsmethode aus, klicken Sie auf **abgeschlossen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  
  
|Tatsächliche Authentifizierungsmethode|Entsprechender URI|  
|--------------------------------|---------------------|  
|Authentifizierung mit Benutzername und Kennwort|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows-Authentifizierung|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|Transport Layer Security \(TLS\) gegenseitige Authentifizierung, die x. 509-Zertifikate verwendet.|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|X. 509\--basierte Authentifizierung, die keine TLS verwendet|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![Regel erstellen](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth2.PNG)
  
## <a name="to-create-by-using-the-send-group-membership-as-claims-rule-template-on-a-claims-provider-trust-in-windows-server-2016"></a>So erstellen Sie mit das Versenden der Gruppenmitgliedschaft als Ansprüche-Vorlage für eine Anspruchsanbieter-Vertrauensstellung in Windows Server 2016 
  
1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  Rechts\-klicken Sie auf der ausgewählten Vertrauensstellung, und klicken Sie dann auf **Edit Claim Rules**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  In der **Edit Claim Rules** Dialogfeld **Akzeptanztransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **Senden der Gruppenmitgliedschaft als Anspruch** aus der Liste aus, und klicken Sie dann auf **Weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)     

6.  Auf der **Regel konfigurieren** geben anspruchsregelname.  
  
7.  Klicken Sie auf **Durchsuchen**, wählen Sie die Gruppe, deren Mitglieder erhalten diese Methode authentifizierungsanspruch soll, und klicken Sie dann auf **OK**.  
  
8.  In **Typ des ausgehenden Anspruchs**Option **Authentifizierungsmethode** in der Liste.  
  
9. In **ausgehender Anspruchswert**, geben Sie eine der standardmäßigen uniform Resource Identifier \(URI\) Werte in der folgenden Tabelle, abhängig von der bevorzugten Authentifizierungsmethode aus, klicken Sie auf **abgeschlossen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  
  
|Tatsächliche Authentifizierungsmethode|Entsprechender URI|  
|--------------------------------|---------------------|  
|Authentifizierung mit Benutzername und Kennwort|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows-Authentifizierung|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|Transport Layer Security \(TLS\) gegenseitige Authentifizierung, die x. 509-Zertifikate verwendet.|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|X. 509\--basierte Authentifizierung, die keine TLS verwendet|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![Regel erstellen](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth2.PNG)


## <a name="to-create-this-rule-by-using-the-transform-an-incoming-claim-rule-template-on-a-relying-party-trust-in-windows-server-2016"></a>Zum Erstellen dieser Regel mithilfe der Transformation ein eingehender Anspruch auf a Relying Party Trust in Windows Server 2016-Vorlage 

1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  Rechts\-klicken Sie auf der ausgewählten Vertrauensstellung, und klicken Sie dann auf **Anspruchsausstellungsrichtlinie bearbeiten**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  In der **Anspruchsausstellungsrichtlinie bearbeiten** Dialogfeld **Ausstellungstransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **Transformieren eines eingehenden Anspruchs** aus der Liste aus, und klicken Sie dann auf **Weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)      

6.  Auf der **Regel konfigurieren** geben anspruchsregelname.  
  
7.  In **eingehender Anspruchstyp**Option **Authentifizierungsmethode** in der Liste.  
  
8.  In **Typ des ausgehenden Anspruchs**Option **Authentifizierungsmethode** in der Liste.  
  
9. Wählen Sie **ersetzen Sie einen eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert**, und führen Sie Folgendes:  
  
    1.  In **eingehender Anspruchswert**, geben Sie den folgenden URI-Werte, die auf die tatsächliche Authentifizierungsmethode URI basieren, die ursprünglich verwendet wurde, klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  
  
    2.  In **ausgehender Anspruchswert**, geben Sie einen der Standard-URI-Werte in der folgenden Tabelle, die von Ihrer neuen bevorzugten authentifizierungswahl durch Methode abhängig ist, klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK**  um die Regel zu speichern.  
  
|Tatsächliche Authentifizierungsmethode|Entsprechender URI|  
|--------------------------------|---------------------|  
|Authentifizierung mit Benutzername und Kennwort|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows-Authentifizierung|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|Gegenseitige TLS-Authentifizierung, der x. 509-Zertifikate verwendet.|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|X. 509\--basierte Authentifizierung, die keine TLS verwendet|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![Regel erstellen](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth4.PNG)
  
> [!NOTE]  
> Andere URI-Werte können zusätzlich zu den Werten in der Tabelle verwendet werden. Die URI-Werte, die Ion angezeigt werden die vorherige Tabelle reflektieren die URIs, die die vertrauende Seite in der Standardeinstellung akzeptiert.  

## <a name="to-create-this-rule-by-using-the-transform-an-incoming-claim-rule-template-on-a-claims-provider-trust-in-windows-server-2016"></a>Zum Erstellen dieser Regel mithilfe der Transformation ein eingehender Anspruch auf eine Anspruchsanbieter-Vertrauensstellung in Windows Server 2016-Vorlage 
  
1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  Rechts\-klicken Sie auf der ausgewählten Vertrauensstellung, und klicken Sie dann auf **Edit Claim Rules**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  In der **Edit Claim Rules** Dialogfeld **Akzeptanztransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **Transformieren eines eingehenden Anspruchs** aus der Liste aus, und klicken Sie dann auf **Weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)      

6.  Auf der **Regel konfigurieren** geben anspruchsregelname.  
  
7.  In **eingehender Anspruchstyp**Option **Authentifizierungsmethode** in der Liste.  
  
8.  In **Typ des ausgehenden Anspruchs**Option **Authentifizierungsmethode** in der Liste.  
  
9. Wählen Sie **ersetzen Sie einen eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert**, und führen Sie Folgendes:  
  
    1.  In **eingehender Anspruchswert**, geben Sie den folgenden URI-Werte, die auf die tatsächliche Authentifizierungsmethode URI basieren, die ursprünglich verwendet wurde, klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  
  
    2.  In **ausgehender Anspruchswert**, geben Sie einen der Standard-URI-Werte in der folgenden Tabelle, die von Ihrer neuen bevorzugten authentifizierungswahl durch Methode abhängig ist, klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK**  um die Regel zu speichern.  
  
|Tatsächliche Authentifizierungsmethode|Entsprechender URI|  
|--------------------------------|---------------------|  
|Authentifizierung mit Benutzername und Kennwort|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows-Authentifizierung|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|Gegenseitige TLS-Authentifizierung, der x. 509-Zertifikate verwendet.|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|X. 509\--basierte Authentifizierung, die keine TLS verwendet|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![Regel erstellen](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth4.PNG)























## <a name="to-create-this-rule-by-using-the-send-group-membership-as-claims-rule-template-in-windows-server-2012-r2"></a>So erstellen Sie mit dieser Regel verwenden das Versenden der Gruppenmitgliedschaft als Ansprüche Regelvorlage in Windows Server 2012 R2  
  
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
  
6.  Auf der **Regel konfigurieren** geben anspruchsregelname.  
  
7.  Klicken Sie auf **Durchsuchen**, wählen Sie die Gruppe, deren Mitglieder erhalten diese Methode authentifizierungsanspruch soll, und klicken Sie dann auf **OK**.  
  
8.  In **Typ des ausgehenden Anspruchs**Option **Authentifizierungsmethode** in der Liste.  
  
9. In **ausgehender Anspruchswert**, geben Sie eine der standardmäßigen uniform Resource Identifier \(URI\) Werte in der folgenden Tabelle, abhängig von der bevorzugten Authentifizierungsmethode aus, klicken Sie auf **abgeschlossen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  
  
|Tatsächliche Authentifizierungsmethode|Entsprechender URI|  
|--------------------------------|---------------------|  
|Authentifizierung mit Benutzername und Kennwort|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows-Authentifizierung|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|Transport Layer Security \(TLS\) gegenseitige Authentifizierung, die x. 509-Zertifikate verwendet.|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|X. 509\--basierte Authentifizierung, die keine TLS verwendet|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![Regel erstellen](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth1.PNG)
 
> [!NOTE]  
> Andere URI-Werte können zusätzlich zu den Werten in der Tabelle verwendet werden. Die URI-Werte, die in der vorherigen Tabelle aufgeführten wider, die URIs, die die vertrauende Seite in der Standardeinstellung akzeptiert wird.  
  
## <a name="to-create-this-rule-by-using-the-transform-an-incoming-claim-rule-template-in-windows-server-2012-r2"></a>Zum Erstellen dieser Regel mithilfe der Transformation einer eingehenden anspruchsregelvorlage in Windows Server 2012 R2  
   
  
  
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
  
6.  Auf der **Regel konfigurieren** geben anspruchsregelname.  
  
7.  In **eingehender Anspruchstyp**Option **Authentifizierungsmethode** in der Liste.  
  
8.  In **Typ des ausgehenden Anspruchs**Option **Authentifizierungsmethode** in der Liste.  
  
9. Wählen Sie **ersetzen Sie einen eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert**, und führen Sie Folgendes:  
  
    1.  In **eingehender Anspruchswert**, geben Sie den folgenden URI-Werte, die auf die tatsächliche Authentifizierungsmethode URI basieren, die ursprünglich verwendet wurde, klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK** um die Regel zu speichern.  
  
    2.  In **ausgehender Anspruchswert**, geben Sie einen der Standard-URI-Werte in der folgenden Tabelle, die von Ihrer neuen bevorzugten authentifizierungswahl durch Methode abhängig ist, klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK**  um die Regel zu speichern.  
  
|Tatsächliche Authentifizierungsmethode|Entsprechender URI|  
|--------------------------------|---------------------|  
|Authentifizierung mit Benutzername und Kennwort|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows-Authentifizierung|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|Gegenseitige TLS-Authentifizierung, der x. 509-Zertifikate verwendet.|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|X. 509\--basierte Authentifizierung, die keine TLS verwendet|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![Regel erstellen](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth3.PNG)
  
> [!NOTE]  
> Andere URI-Werte können zusätzlich zu den Werten in der Tabelle verwendet werden. Die URI-Werte, die Ion angezeigt werden die vorherige Tabelle reflektieren die URIs, die die vertrauende Seite in der Standardeinstellung akzeptiert.  

## <a name="additional-references"></a>Weitere Verweise 
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  
 
[Prüfliste: Erstellen von Anspruchsregeln für eine Vertrauensstellung der vertrauenden Seite](https://technet.microsoft.com/library/ee913578.aspx)  

[Prüfliste: Erstellen von Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung](https://technet.microsoft.com/library/ee913564.aspx)  
  
[Wenn Use an Authorization Claim Rule](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Die Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Die Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
