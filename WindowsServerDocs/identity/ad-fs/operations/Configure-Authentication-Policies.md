---
ms.assetid: 8e7015bc-c489-4ec7-8b6e-3ece90f72317
title: Konfigurieren von Authentifizierungsrichtlinien
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: ef38b0280a5753b0995e85d0809de6b632fa3afc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358119"
---
# <a name="configure-authentication-policies"></a>Konfigurieren von Authentifizierungsrichtlinien

In AD FS werden in Windows Server 2012 R2 sowohl die Zugriffs Steuerung als auch der Authentifizierungsmechanismus durch mehrere Faktoren erweitert, die Benutzer-, Geräte-, Standort-und Authentifizierungsdaten umfassen. Diese Verbesserungen ermöglichen es Ihnen, entweder über die Benutzeroberfläche oder über Windows PowerShell zu verwalten, das Risiko zu gewähren,\-dass AD FS gesicherten Anwendungen\-über die Multi-Factor Access Control und Multi\-Faktor Authentifizierung, die auf Benutzeridentität oder Gruppenmitgliedschaft, Netzwerkadresse, Gerätedaten, die mit dem\-Arbeitsplatz verbunden sind, und dem Authentifizierungs\-Status bei \(Multi-Factor Authentication-MFAbasiert\) wurde ausgeführt.  

Weitere Informationen zu MFA und zur mehr\-stufigen Zugriffs Steuerung in Active Directory-Verbunddienste (AD FS) \(AD FS\) in Windows Server 2012 R2 finden Sie in den folgenden Themen:  


-   [Arbeitsplatzbeitritt von einem beliebigen Gerät für SSO und die nahtlose zweistufige Authentifizierung bei allen Unternehmensanwendungen](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)

-   [Verwalten von Risiken mit der bedingten Zugriffssteuerung](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md)

-   [Verwalten von Risiken mit zusätzlicher mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)

## <a name="configure-authentication-policies-via-the-ad-fs-management-snap-in"></a>Konfigurieren von Authentifizierungs Richtlinien über das Snap\--in "AD FS-Verwaltung"  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um diese Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   

In AD FS können Sie in Windows Server 2012 R2 eine Authentifizierungs Richtlinie in einem globalen Bereich angeben, die für alle von AD FS gesicherten Anwendungen und Dienste gilt. Sie können auch Authentifizierungs Richtlinien für bestimmte Anwendungen und Dienste festlegen, die auf Vertrauens Stellungen von Vertrauens Stellungen basieren und durch AD FS gesichert werden. Wenn eine Authentifizierungs Richtlinie für eine bestimmte Anwendung pro Vertrauensstellung der vertrauenden Seite angegeben wird, wird die globale Authentifizierungs Richtlinie nicht überschrieben. Wenn die Authentifizierungs Richtlinie für globale oder pro Vertrauensstellung der vertrauenden Seite MFA erfordert, wird MFA ausgelöst, wenn der Benutzer versucht, sich bei dieser Vertrauensstellung der vertrauenden Seite zu authentifizieren. Die globale Authentifizierungs Richtlinie ist ein Fall Back für die Vertrauens Stellungen der vertrauenden Seite für Anwendungen und Dienste, die nicht über eine bestimmte konfigurierte Authentifizierungs Richtlinie verfügen. 

## <a name="to-configure-primary-authentication-globally-in-windows-server-2012-r2"></a>So konfigurieren Sie die primäre Authentifizierung Global in Windows Server 2012 R2 

1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  

2.  Klicken Sie in\-AD FS Snap in auf **Authentifizierungs Richtlinien**.  

3.  Klicken Sie im Abschnitt **primäre Authentifizierung** neben **globale Einstellungen**auf **Bearbeiten** . Sie können auch mit\-der rechten Maustaste auf **Authentifizierungs Richtlinien**klicken und **globale primäre Authentifizierung bearbeiten**auswählen, oder wählen Sie im Bereich **Aktionen** die Option **globale primäre Authentifizierung bearbeiten**aus.  
![Authentifizierungs Richtlinien](media/Configure-Authentication-Policies/authpolicy1.png)

4.  Im Fenster **Globale Authentifizierungs Richtlinie bearbeiten** auf der Registerkarte **primär** können Sie die folgenden Einstellungen als Teil der globalen Authentifizierungs Richtlinie konfigurieren:  

    -   Authentifizierungsmethoden, die für die primäre Authentifizierung verwendet werden sollen. Sie können unter dem **Extranet** und **Intranet**verfügbare Authentifizierungsmethoden auswählen.  

    -   Geräte Authentifizierung über das Kontrollkästchen **Geräte Authentifizierung aktivieren** . Weitere Informationen finden Sie unter [Arbeitsplatzbeitritt von einem beliebigen Gerät für SSO und die nahtlose zweistufige Authentifizierung bei allen Unternehmensanwendungen](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md).  
![Authentifizierungs Richtlinien](media/Configure-Authentication-Policies/authpolicy2.png)  

## <a name="to-configure-primary-authentication-per-relying-party-trust"></a>So konfigurieren Sie die primäre Authentifizierung pro Vertrauender Seite  

1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  

2.  Klicken Sie in\-AD FS Snap-in auf **Authentifizierungs Richtlinien**\\**pro Vertrauensstellung der vertrauenden Seite**, und klicken Sie dann auf die Vertrauensstellung der vertrauenden Seite, für die Sie Authentifizierungs Richtlinien konfigurieren möchten.  

3.  Klicken Sie\-entweder mit der rechten Maustaste auf die Vertrauensstellung der vertrauenden Seite, für die Sie Authentifizierungs Richtlinien konfigurieren möchten, und wählen Sie dann **benutzerdefinierte primäre Authentifizierung bearbeiten**aus, oder wählen Sie im Bereich **Aktionen** die Option **benutzerdefinierte primäre Authentifizierung**.  
![Authentifizierungs Richtlinien](media/Configure-Authentication-Policies/authpolicy5.png)   

4.  Im Fenster " **Authentifizierungs Richtlinie für <\_Vertrauensstellung der vertrauenden\_\_Seite bearbeiten" >** auf der Registerkarte " **primär** " können Sie die folgende Einstellung als Teil der pro Vertrauensstellung der **vertrauenden Seite** konfigurieren. Authentifizierungs Richtlinie:  

    -   Ob Benutzer jedes Mal, wenn Sie sich über die Benutzer anmelden\-müssen, Ihre Anmelde Informationen angeben müssen **, müssen bei\-jedem Anmeldevorgang Ihre Anmelde Informationen** eingeben.  
![Authentifizierungs Richtlinien](media/Configure-Authentication-Policies/authpolicy6.png) 

## <a name="to-configure-multi-factor-authentication-globally"></a>So konfigurieren Sie die Multi-Factor Authentication Global  

1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  

2.  Klicken Sie in\-AD FS Snap in auf **Authentifizierungs Richtlinien**.  

3.  Klicken Sie im Abschnitt **\-Multi-Factor Authentication** neben **globale Einstellungen**auf **Bearbeiten** . Sie können auch mit\-der rechten Maustaste auf **Authentifizierungs Richtlinien**klicken und **globale\-mehrstufige Authentifizierung bearbeiten**auswählen. Sie können auch im Bereich **Aktionen** die Option **globale Multi\--Factor Authentication bearbeiten auswählen.** .  
![Authentifizierungs Richtlinien](media/Configure-Authentication-Policies/authpolicy8.png)   

4.  Im Fenster **Globale Authentifizierungs Richtlinie bearbeiten** können Sie die folgenden Einstellungen auf der Registerkarte **\-Multi-Factor** Authentication als Teil der globalen Multi\--Factor Authentication-Richtlinie konfigurieren:  

    -   Einstellungen oder Bedingungen für MFA über verfügbare Optionen in den Abschnitten **Benutzer\/Gruppen**, **Geräte**und **Standorte** .  

    -   Wenn Sie MFA für eine dieser Einstellungen aktivieren möchten, müssen Sie mindestens eine zusätzliche Authentifizierungsmethode auswählen. Die Standardoption **Zertifikat Authentifizierung** ist die Standardoption. Sie können auch andere benutzerdefinierte zusätzliche Authentifizierungsmethoden konfigurieren, z. b. Windows Azure Active Authentication. Weitere Informationen finden [Sie im Handbuch Exemplarische Vorgehensweise: Verwalten von Risiken mit zusätzlichen Multi-Factor Authentication für sensible](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)Anwendungen.  

> [!WARNING]  
> Sie können nur zusätzliche Authentifizierungsmethoden Global konfigurieren.  
![Authentifizierungs Richtlinien](media/Configure-Authentication-Policies/authpolicy9.png)  

## <a name="to-configure-multi-factor-authentication-per-relying-party-trust"></a>So konfigurieren Sie\-die mehrstufige Authentifizierung pro Vertrauensstellung der vertrauenden Seite  

1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  

2.  Klicken Sie in\-AD FS Snap-in auf **Authentifizierungs Richtlinien**\\**pro Vertrauensstellung der vertrauenden Seite**, und klicken Sie dann auf die Vertrauensstellung der vertrauenden Seite, für die Sie MFA konfigurieren möchten.  

3.  Klicken Sie\-entweder mit der rechten Maustaste auf die Vertrauensstellung der vertrauenden Seite, für die Sie MFA konfigurieren möchten, und wählen Sie dann **benutzerdefinierte mehrstufige\-Authentifizierung bearbeiten**aus, oder wählen Sie im Bereich **Aktionen** die Option **benutzerdefiniertes\- Faktor Authentifizierung**.  

4.  Im Fenster " **Authentifizierungs Richtlinie für <\_Vertrauensstellung der vertrauenden\_\_Seite bearbeiten" >** auf der Registerkarte "Multi **\--Factor** " können Sie die folgenden Einstellungen als Teil der pro\-Authentifizierungs Richtlinie für Vertrauens Stellungen der vertrauenden Seite:  

    -   Einstellungen oder Bedingungen für MFA über verfügbare Optionen in den Abschnitten **Benutzer\/Gruppen**, **Geräte**und **Standorte** .  

## <a name="configure-authentication-policies-via-windows-powershell"></a>Konfigurieren von Authentifizierungs Richtlinien über Windows PowerShell  
Windows PowerShell ermöglicht mehr Flexibilität bei der Verwendung verschiedener Zugriffs Steuerungs Faktoren und des in AD FS in Windows Server 2012 R2 verfügbaren Authentifizierungsmechanismus zum Konfigurieren von Authentifizierungs Richtlinien und Autorisierungs Regeln, die für erforderlich sind. Implementieren Sie einen echten bedingten Zugriff für \-Ihre AD FS gesicherten Ressourcen.  

Sie müssen mindestens Mitglied der Gruppe "Administratoren" oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um diese Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.Microsoft.com\/\/swlink? LinkId\=83477\).   

### <a name="to-configure-an-additional-authentication-method-via-windows-powershell"></a>So konfigurieren Sie eine zusätzliche Authentifizierungsmethode über Windows PowerShell  

1.  Öffnen Sie auf dem Verbund Server das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  


~~~
`Set-AdfsGlobalAuthenticationPolicy –AdditionalAuthenticationProvider CertificateAuthentication  `
~~~


> [!WARNING]  
> Mit dem Befehl `Get-AdfsGlobalAuthenticationPolicy` können Sie überprüfen, ob der oben angegebene Befehl erfolgreich ausgeführt wurde.  

### <a name="to-configure-mfa-per-relying-party-trust-that-is-based-on-a-users-group-membership-data"></a>So konfigurieren Sie die MFA pro\-Vertrauensstellung der vertrauenden Seite, die auf den Gruppen Mitgliedschafts Daten eines Benutzers basiert  

1.  Öffnen Sie auf dem Verbundserver das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus:  


~~~
`$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust`  
~~~


> [!WARNING]  
> Ersetzen Sie *<\_> Vertrauensstellung\_der vertrauenden Seite* durch den Namen Ihrer Vertrauensstellung der vertrauenden Seite.  

2. Führen Sie im selben Windows PowerShell-Befehlsfenster den folgenden Befehl aus.  


~~~
$MfaClaimRule = “c:[Type == ‘“https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid'”, Value =~ ‘“^(?i) <group_SID>$'”] => issue(Type = ‘“https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'”, Value ‘“https://schemas.microsoft.com/claims/multipleauthn'”);” 

Set-AdfsRelyingPartyTrust –TargetRelyingParty $rp –AdditionalAuthenticationRules $MfaClaimRule
~~~


> [!NOTE]  
> Stellen Sie sicher, dass\_Sie < Gruppen-sid-> durch den \(Wert\) der sicherheitsbezeichnersid der Active Directory \(AD\) -Gruppe ersetzen.  

### <a name="to-configure-mfa-globally-based-on-users-group-membership-data"></a>So konfigurieren Sie die MFA Global basierend auf den Gruppen Mitgliedschafts Daten der Benutzer  

1.  Öffnen Sie auf dem Verbund Server das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  


~~~
$MfaClaimRule = “c:[Type == ‘" https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid'", Value == ‘"group_SID'"]  
 => issue(Type = ‘"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'", Value = ‘"https://schemas.microsoft.com/claims/multipleauthn'");”  

Set-AdfsAdditionalAuthenticationRule $MfaClaimRule  
~~~


> [!NOTE]  
> Stellen Sie sicher, dass *< Gruppen\_-sid->* durch den Wert der SID der Ad-Gruppe ersetzt wird.  

### <a name="to-configure-mfa-globally-based-on-users-location"></a>So konfigurieren Sie die MFA Global basierend auf dem Speicherort des Benutzers  

1.  Öffnen Sie auf dem Verbund Server das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  


~~~
$MfaClaimRule = “c:[Type == ‘" https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork'", Value == ‘"true_or_false'"]  
 => issue(Type = ‘"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'", Value = ‘"https://schemas.microsoft.com/claims/multipleauthn'");”  

Set-AdfsAdditionalAuthenticationRule $MfaClaimRule  
~~~



> [!NOTE]  
> Stellen Sie sicher, dass Sie *< true\_-\_oder false->* entweder `true` durch oder `false`ersetzen. Der Wert hängt von ihrer speziellen Regel Bedingung ab, die darauf basiert, ob die Zugriffs Anforderung aus dem Extranet oder dem Intranet stammt.  

### <a name="to-configure-mfa-globally-based-on-users-device-data"></a>So konfigurieren Sie die MFA Global basierend auf den Gerätedaten des Benutzers  

1.  Öffnen Sie auf dem Verbund Server das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  


~~~
$MfaClaimRule = "c:[Type == ‘" https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser'", Value == ‘"true_or_false"']  
 => issue(Type = ‘"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'", Value = ‘"https://schemas.microsoft.com/claims/multipleauthn'");"  

Set-AdfsAdditionalAuthenticationRule $MfaClaimRule  
~~~


> [!NOTE]  
> Stellen Sie sicher, dass Sie *< true\_-\_oder false->* entweder `true` durch oder `false`ersetzen. Der Wert hängt von ihrer speziellen Regel Bedingung ab, die darauf basiert, ob das Gerät\-dem Arbeitsplatz beigetreten ist oder nicht.  

### <a name="to-configure-mfa-globally-if-the-access-request-comes-from-the-extranet-and-from-a-non-workplace-joined-device"></a>So konfigurieren Sie die MFA Global, wenn die Zugriffs Anforderung aus dem Extranet und einem\-nicht\-mit dem Arbeitsplatz verbundenen Gerät stammt  

1.  Öffnen Sie auf dem Verbund Server das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  


~~~
`Set-AdfsAdditionalAuthenticationRule "c:[Type == '"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser'", Value == '"true_or_false'"] && c2:[Type == '"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork'", Value == '" true_or_false '"] => issue(Type = '"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'", Value ='"https://schemas.microsoft.com/claims/multipleauthn'");" ` 
~~~


> [!NOTE]  
> Stellen Sie sicher, dass beide Instanzen von *<\_"true\_" oder "false" >* entweder `true` durch oder `false`ersetzt werden. Dies hängt von den jeweiligen Regel Bedingungen ab. Die Regel Bedingungen basieren darauf, ob das Gerät dem Arbeits\-Platz beigetreten ist oder nicht, und ob die Zugriffs Anforderung aus dem Extranet oder Intranet stammt.  

### <a name="to-configure-mfa-globally-if-access-comes-from-an-extranet-user-that-belongs-to-a-certain-group"></a>So konfigurieren Sie die MFA Global, wenn der Zugriff von einem Extranet-Benutzer stammt, der zu einer bestimmten Gruppe gehört  

1.  Öffnen Sie auf dem Verbund Server das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  


~~~
Set-AdfsAdditionalAuthenticationRule "c:[Type == `"https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid`", Value == `"group_SID`"] && c2:[Type == `"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`", Value== `"true_or_false`"] => issue(Type = `"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod`", Value =`"https://schemas.microsoft.com/claims/
~~~

> [!NOTE]  
> Stellen Sie sicher, dass *<\_Gruppen-sid->* durch den Wert der Gruppen-SID und *< true\_oder\_false >* entweder `true` durch oder `false`ersetzt wird. Dies hängt von der jeweiligen Regel Bedingung ab, die basiert darauf, ob die Zugriffs Anforderung aus dem Extranet oder Intranet stammt.  

### <a name="to-grant-access-to-an-application-based-on-user-data-via-windows-powershell"></a>So gewähren Sie Zugriff auf eine Anwendung auf der Grundlage von Benutzerdaten über Windows PowerShell  

1.  Öffnen Sie auf dem Verbund Server das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  

    ```  
    $rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust  

    ```  

> [!NOTE]  
> Stellen Sie sicher, dass Sie *<\_Vertrauensstellung der >\_vertrauenden Seite* durch den Wert ihrer Vertrauensstellung der vertrauenden Seite ersetzen  

2. Führen Sie im selben Windows PowerShell-Befehlsfenster den folgenden Befehl aus.  

   ```  

     $GroupAuthzRule = "@RuleTemplate = `“Authorization`” @RuleName = `"Foo`" c:[Type == `"https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid`", Value =~ `"^(?i)<group_SID>$`"] =>issue(Type = `"https://schemas.microsoft.com/authorization/claims/deny`", Value = `"DenyUsersWithClaim`");"  
   Set-AdfsRelyingPartyTrust –TargetRelyingParty $rp –IssuanceAuthorizationRules $GroupAuthzRule  
   ```  

> [!NOTE]  
> > Stellen Sie sicher, dass *< Gruppen\_-sid->* durch den Wert der SID der Ad-Gruppe ersetzt wird.  

### <a name="to-grant-access-to-an-application-that-is-secured-by-ad-fs-only-if-this-users-identity-was-validated-with-mfa"></a>So gewähren Sie Zugriff auf eine Anwendung, die durch AD FS geschützt ist, wenn die Identität dieses Benutzers mit MFA überprüft wurde  

1.  Öffnen Sie auf dem Verbund Server das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  


~~~
`$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust ` 
~~~


> [!NOTE]  
> Stellen Sie sicher, dass Sie *<\_Vertrauensstellung der >\_vertrauenden Seite* durch den Wert ihrer Vertrauensstellung der vertrauenden Seite ersetzen  

2. Führen Sie im selben Windows PowerShell-Befehlsfenster den folgenden Befehl aus.  

   ```  
   $GroupAuthzRule = "@RuleTemplate = `"Authorization`"  
   @RuleName = `"PermitAccessWithMFA`"  
   c:[Type == `"https://schemas.microsoft.com/claims/authnmethodsreferences`", Value =~ `"^(?i)https://schemas\.microsoft\.com/claims/multipleauthn$`"] => issue(Type = `"https://schemas.microsoft.com/authorization/claims/permit`", Value = ‘“PermitUsersWithClaim'");"  

   ```  

### <a name="to-grant-access-to-an-application-that-is-secured-by-ad-fs-only-if-the-access-request-comes-from-a-workplace-joined-device-that-is-registered-to-the-user"></a>Um Zugriff auf eine Anwendung zu gewähren, die durch AD FS geschützt ist, wenn die Zugriffs Anforderung von einem\-mit dem Arbeitsplatz verbundenen Gerät stammt, das für den Benutzer registriert ist.  

1.  Öffnen Sie auf dem Verbund Server das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  

    ```  
    $rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust  

    ```  

> [!NOTE]  
> Stellen Sie sicher, dass Sie *<\_Vertrauensstellung der >\_vertrauenden Seite* durch den Wert ihrer Vertrauensstellung der vertrauenden Seite ersetzen  

2. Führen Sie im selben Windows PowerShell-Befehlsfenster den folgenden Befehl aus.  


~~~
$GroupAuthzRule = "@RuleTemplate = `"Authorization`"  
@RuleName = `"PermitAccessFromRegisteredWorkplaceJoinedDevice`"  
c:[Type == `"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser`", Value =~ `"^(?i)true$`"] => issue(Type = `"https://schemas.microsoft.com/authorization/claims/permit`", Value = `"PermitUsersWithClaim`");  
~~~



### <a name="to-grant-access-to-an-application-that-is-secured-by-ad-fs-only-if-the-access-request-comes-from-a-workplace-joined-device-that-is-registered-to-a-user-whose-identity-has-been-validated-with-mfa"></a>Um Zugriff auf eine Anwendung zu gewähren, die durch AD FS geschützt ist, wenn die Zugriffs Anforderung von einem\-mit dem Arbeitsplatz verbundenen Gerät stammt, das für einen Benutzer registriert ist, dessen Identität mit der MFA bestätigt wurde.  

1.  Öffnen Sie auf dem Verbund Server das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  


~~~
`$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust ` 
~~~


> [!NOTE]  
> Stellen Sie sicher, dass Sie *<\_Vertrauensstellung der >\_vertrauenden Seite* durch den Wert ihrer Vertrauensstellung der vertrauenden Seite ersetzen  

2. Führen Sie im selben Windows PowerShell-Befehlsfenster den folgenden Befehl aus.  

   ```  
   $GroupAuthzRule = ‘@RuleTemplate = “Authorization”  
   @RuleName = “RequireMFAOnRegisteredWorkplaceJoinedDevice”  
   c1:[Type == `"https://schemas.microsoft.com/claims/authnmethodsreferences`", Value =~ `"^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$`"] &&  
   c2:[Type == `"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser`", Value =~ `"^(?i)true$”] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit`", Value = `"PermitUsersWithClaim`");"  

   ```  

### <a name="to-grant-extranet-access-to-an-application-secured-by-ad-fs-only-if-the-access-request-comes-from-a-user-whose-identity-has-been-validated-with-mfa"></a>Zum Gewähren von Extranetzugriff auf eine durch AD FS gesicherte Anwendung nur dann, wenn die Zugriffs Anforderung von einem Benutzer stammt, dessen Identität mit der MFA bestätigt wurde.  

1.  Öffnen Sie auf dem Verbund Server das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  


~~~
`$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust`  
~~~


> [!NOTE]  
> Stellen Sie sicher, dass Sie *<\_Vertrauensstellung der >\_vertrauenden Seite* durch den Wert ihrer Vertrauensstellung der vertrauenden Seite ersetzen  

2. Führen Sie im selben Windows PowerShell-Befehlsfenster den folgenden Befehl aus.  


~~~
$GroupAuthzRule = "@RuleTemplate = `"Authorization`"  
@RuleName = `"RequireMFAForExtranetAccess`"  
c1:[Type == `"https://schemas.microsoft.com/claims/authnmethodsreferences`", Value =~ `"^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$`"] &&  
c2:[Type == `"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`", Value =~ `"^(?i)false$`"] => issue(Type = `"https://schemas.microsoft.com/authorization/claims/permit`", Value = `"PermitUsersWithClaim`");"  
~~~

## <a name="additional-references"></a>Weitere Verweise  

[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md)
