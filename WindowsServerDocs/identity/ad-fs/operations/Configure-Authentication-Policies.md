---
ms.assetid: 8e7015bc-c489-4ec7-8b6e-3ece90f72317
title: Konfigurieren von Authentifizierungsrichtlinien
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 7faffb7ccbb4b0ea3c65329d18f915d7dafcd46f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="configure-authentication-policies"></a>Konfigurieren von Authentifizierungsrichtlinien

>Gilt für: Windows Server 2012 R2

In AD FS unter Windows Server 2012 R2 sowohl Steuerelement auch der Authentifizierungsmechanismus werden durch mehrere Faktoren, die Benutzer, Gerät, Standort und Authentifizierung gehören verbessert. Diese Erweiterungen zu ermöglichen Ihnen, entweder über die Benutzeroberfläche oder über Windows PowerShell, um das Risiko von Erteilen von Zugriffsberechtigungen auf AD FS\ gesicherte Anwendungen über Multithread-Factor Access Control und Multithread-Faktor-Authentifizierung, die auf Benutzer Benutzeridentität oder der Gruppenmitgliedschaft, Netzwerkadresse,, um Gerätedaten Workplace\ eingebunden basieren und Authentifizierungsstatus bei Multithread-Faktor-Authentifizierung \(MFA\) wurde ausgeführt.  
  
Weitere Informationen zur MFA und Multithread-Faktor Zugriffssteuerung in Active Directory Federation Services \(AD FS\) in Windows Server 2012 R2 finden Sie unter den folgenden Themen:  


-   [Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose zweistufige Authentifizierung bei allen Unternehmensanwendungen](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)

-   [Verwalten von Risiken mit Steuerung des bedingten Zugriffs](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md)

-   [Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)

## <a name="configure-authentication-policies-via-the-ad-fs-management-snap-in"></a>Konfigurieren von Authentifizierungsrichtlinien über AD FS-Verwaltungs-Snap-in  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer die Mindestanforderung für diese Verfahren abzuschließen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
In AD FS unter Windows Server 2012 R2 können Sie eine Authentifizierungsrichtlinie für einen globalen Bereich angeben, die gilt für alle Anwendungen und Dienste, die von AD FS geschützt sind. Sie können auch festlegen, dass Authentifizierungsrichtlinien für bestimmte Anwendungen und Dienste, die abhängig von Vertrauensstellungen und von AD FS geschützt sind. Geben Sie eine Authentifizierungsrichtlinie für eine bestimmte Anwendung pro vertrauende Seite Vertrauensstellung überschreibt nicht die globale Authentifizierungsrichtlinie. Wenn der globalen oder pro vertrauende Seite Authentifizierungsrichtlinie die MFA MFA Vertrauensstellung wird ausgelöst, wenn der Benutzer versucht, um diese Vertrauensstellung der vertrauenden Seite zu authentifizieren. Die globale Authentifizierungsrichtlinie dient als Fallback für Vertrauensstellungen für Anwendungen und Dienste, die keine spezielle Authentifizierungsrichtlinie konfiguriert haben vertrauenden Seite. 

## <a name="to-configure-primary-authentication-globally-in-windows-server-2012-r2"></a>So konfigurieren Sie primäre Authentifizierung Global in Windows Server 2012 R2 
  
1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In AD FS-Snap-in, klicken Sie auf **Authentifizierungsrichtlinien**.  
  
3.  In der **primäre Authentifizierung** auf **bearbeiten** neben **globale Einstellungen**. Sie können auch mit der rechten Maustaste auf **Authentifizierungsrichtlinien**, und wählen Sie **globale primäre Authentifizierung bearbeiten**, oder klicken Sie unter der **Aktionen** Bereich **globale primäre Authentifizierung bearbeiten**.  
![Auth-Richtlinien](media/Configure-Authentication-Policies/authpolicy1.png)
  
4.  In der **globale Authentifizierungsrichtlinie bearbeiten** Fenster auf die **primären** Registerkarte können Sie die folgenden Einstellungen als Teil der globalen Authentifizierungsrichtlinie konfigurieren:  
  
    -   Authentifizierungsmethoden für die primäre Authentifizierung verwendet werden. Sie können die verfügbaren Authentifizierungsmethoden unter Auswählen der **Extranet** und **Intranet**.  
  
    -   Geräteauthentifizierung über die **Geräteauthentifizierung aktivieren** Kontrollkästchen. Weitere Informationen finden Sie unter [Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose zweistufige Authentifizierung über Unternehmensanwendungen](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md).  
![Auth-Richtlinien](media/Configure-Authentication-Policies/authpolicy2.png)  

## <a name="to-configure-primary-authentication-per-relying-party-trust"></a>So konfigurieren Sie primäre Authentifizierung pro vertrauende Seite Vertrauensstellung  
  
1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In AD FS-Snap-in, klicken Sie auf **Authentifizierungsrichtlinien**\\**pro Vertrauensstellungen der vertrauenden Seite Vertrauensstellung**, und klicken Sie dann auf die Vertrauensstellung einer vertrauenden Seite für die Sie Authentifizierungsrichtlinien konfigurieren möchten.  
  
3.  Entweder mit der rechten Maustaste auf der vertrauenden Seite Vertrauensstellung für die Sie konfigurieren möchten Authentifizierungsrichtlinien, und wählen Sie dann **benutzerdefinierte primäre Authentifizierung bearbeiten**, oder klicken Sie unter der **Aktionen** Bereich **benutzerdefinierte primäre Authentifizierung bearbeiten**.  
![Auth-Richtlinien](media/Configure-Authentication-Policies/authpolicy5.png)   

4.  In der **Authentifizierungsrichtlinie für < Relying\_party\_trust\_name > Bearbeiten** Fenster unter der **primären** Registerkarte können Sie die folgende Einstellung konfigurieren, als Teil der **pro Vertrauensstellung der vertrauenden Seite** Authentifizierungsrichtlinie:  
  
    -   Gibt an, ob Benutzer ihre Anmeldeinformationen bei Standardparameter an jedem müssen über die **Benutzer sind erforderlich, um ihre Anmeldeinformationen bei Standardparameter an jedem** Kontrollkästchen.  
![Auth-Richtlinien](media/Configure-Authentication-Policies/authpolicy6.png) 

## <a name="to-configure-multi-factor-authentication-globally"></a>So konfigurieren Sie die mehrstufige Authentifizierung Global  
  
1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In AD FS-Snap-in, klicken Sie auf **Authentifizierungsrichtlinien**.  
  
3.  In der **Multithread-Faktor-Authentifizierung** auf **bearbeiten** neben **globale Einstellungen**. Außerdem können Sie mit der rechten Maustaste auf **Authentifizierungsrichtlinien**, und wählen Sie **globale bearbeiten Multithread-Faktor-Authentifizierung**, oder unter der **Aktionen** , wählen Sie im Bereich **globale bearbeiten Multithread-Faktor-Authentifizierung**.  
![Auth-Richtlinien](media/Configure-Authentication-Policies/authpolicy8.png)   

4.  In der **globale Authentifizierungsrichtlinie bearbeiten** Fenster unter der **Multithread-Faktor** Registerkarte als Teil der globalen Multithread-Factor Authentication-Richtlinie können Sie die folgenden Einstellungen konfigurieren:  
  
    -   Einstellungen oder Bedingungen für die MFA über die verfügbaren Optionen unter der **Ordner %%amp;quot;Benutzer\/Gruppen**, **Geräte**, und **Speicherorte** Abschnitte.  
  
    -   Um die MFA für jede dieser Einstellungen zu aktivieren, müssen Sie mindestens eine zusätzliche Authentifizierungsmethode auswählen. **Authentifizierung Zertifikat** ist die Standardoption verfügbar. Sie können auch andere benutzerdefinierte zusätzliche Authentifizierungsmethoden, z. B. Windows Azure Active-Authentifizierung konfigurieren. Weitere Informationen finden Sie unter [Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md).  
  
> [!WARNING]  
> Sie können nur global Weitere Authentifizierungsmethoden konfigurieren.  
![Auth-Richtlinien](media/Configure-Authentication-Policies/authpolicy9.png)  

## <a name="to-configure-multi-factor-authentication-per-relying-party-trust"></a>So konfigurieren Sie Multithread-Faktor-Authentifizierung pro vertrauende Seite Vertrauensstellung  
  
1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**.  
  
2.  In AD FS-Snap-in, klicken Sie auf **Authentifizierungsrichtlinien**\\**pro Vertrauensstellungen der vertrauenden Seite Vertrauensstellung**, und klicken Sie dann auf die Vertrauensstellung einer vertrauenden Seite für die Konfiguration der MFA werden soll.  
  
3.  Entweder mit der rechten Maustaste auf der vertrauenden Seite Vertrauensstellung für die sollen Konfigurieren der mehrstufigen Authentifizierung, und wählen Sie dann **Bearbeiten benutzerdefinierter Multithread-Factor Authentication**, oder klicken Sie unter der **Aktionen** Bereich **Bearbeiten benutzerdefinierter Multithread-Factor Authentication**.  
  
4.  In der **Authentifizierungsrichtlinie für < Relying\_party\_trust\_name > Bearbeiten** Fenster unter der **Multithread-Faktor** Registerkarte können Sie die folgenden Einstellungen konfigurieren, als Teil der Per\ vertrauende vertrauen Authentifizierungsrichtlinie:  
  
    -   Einstellungen oder Bedingungen für die MFA über die verfügbaren Optionen unter der **Ordner %%amp;quot;Benutzer\/Gruppen**, **Geräte**, und **Speicherorte** Abschnitte.  

## <a name="configure-authentication-policies-via-windows-powershell"></a>Konfigurieren von Authentifizierungsrichtlinien über Windows PowerShell  
Windows PowerShell ermöglicht eine größere Flexibilität bei der Verwendung von verschiedenen Faktoren ab, der Steuerung des Zugriffs und der Authentifizierungsmethode, die in AD FS unter Windows Server 2012 R2 zum Konfigurieren von Authentifizierungsrichtlinien und Autorisierung verfügbar sind Regeln, die zum Implementieren von "true" bedingten Zugriff für Ihre AD FS \-secured Ressourcen erforderlich sind.  
  
Mitglied der Gruppe Administratoren oder einer entsprechenden Gruppe auf dem lokalen Computer ist die Mindestanforderung für diese Verfahren abzuschließen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \ (http:///\/ go.microsoft.com\/Fwlink\ /? LinkId\ = 83477\).   
  
### <a name="to-configure-an-additional-authentication-method-via-windows-powershell"></a>So konfigurieren Sie eine zusätzliche Authentifizierungsmethode über Windows PowerShell  
  
1.  Auf dem Verbundserver das Windows PowerShell-Befehlsfenster geöffnet, und führen Sie den folgenden Befehl aus.  
  

    `Set-AdfsGlobalAuthenticationPolicy –AdditionalAuthenticationProvider CertificateAuthentication  `

  
> [!WARNING]  
> Um sicherzustellen, dass dieser Befehl erfolgreich ausgeführt wurde, können Sie Ausführen der `Get-AdfsGlobalAuthenticationPolicy` Befehl.  
  
### <a name="to-configure-mfa-per-relying-party-trust-that-is-based-on-a-users-group-membership-data"></a>So konfigurieren Sie die MFA Per\ der vertrauenden Seite Vertrauensstellung, die basierend auf der Gruppenmitgliedschaftsdaten des Benutzers  
  
1.  Auf dem Verbundserver das Windows PowerShell-Befehlsfenster geöffnet, und führen Sie den folgenden Befehl aus:  
  

    `$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust`  
  
  
> [!WARNING]  
> Sicher, dass Sie ersetzen *< Relying\_party\_trust >* mit dem Namen des Ihre Vertrauensstellung der vertrauenden Seite.  
  
2.  Führen Sie in der gleichen Windows PowerShell-Befehlsfenster den folgenden Befehl ein.  
  
 
    $MfaClaimRule = "c: [Typ == '" https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid'", Wert = ~ '" ^(?i) < Group_SID >$ ' "] = > Problem (Typ =" "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'", Wert ' "https://schemas.microsoft.com/claims/multipleauthn'"); " 
    
    Set-AdfsRelyingPartyTrust – TargetRelyingParty $rp – AdditionalAuthenticationRules $MfaClaimRule
  
  
> [!NOTE]  
> Nehmen Sie mit dem Wert der Sicherheits-ID ersetzen Sie < Group\_SID > \(SID\) der \(AD\) Active Directory-Gruppe.  
  
### <a name="to-configure-mfa-globally-based-on-users-group-membership-data"></a>Konfiguration der MFA Global basierend auf Gruppenmitgliedschaftsdaten des Benutzers  
  
1.  Auf dem Verbundserver das Windows PowerShell-Befehlsfenster geöffnet, und führen Sie den folgenden Befehl aus.  
  

    $MfaClaimRule = "c: [Typ == '" https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid'", Wert == '" Group_SID'"]  
     = > Problem (Type = "" https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'", Wert =" "https://schemas.microsoft.com/claims/multipleauthn'"); "  
      
    Set-AdfsAdditionalAuthenticationRule $MfaClaimRule  

  
> [!NOTE]  
> Sicher, dass Sie ersetzen *< Group\_SID >* mit dem Wert der SID der AD-Gruppe.  
  
### <a name="to-configure-mfa-globally-based-on-users-location"></a>Konfiguration der MFA Global basierend auf Position des Benutzers  
  
1.  Auf dem Verbundserver das Windows PowerShell-Befehlsfenster geöffnet, und führen Sie den folgenden Befehl aus.  
  
 
    $MfaClaimRule = "c: [Typ == '" https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork'", Wert == '" True_or_false'"]  
     = > Problem (Type = "" https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'", Wert =" "https://schemas.microsoft.com/claims/multipleauthn'"); "  
  
    Set-AdfsAdditionalAuthenticationRule $MfaClaimRule  
  

  
> [!NOTE]  
> Sicher, dass Sie ersetzen *< True\_or\_false >* entweder mit `true` oder `false`. Der Wert hängt von der bestimmten Bedingung, die basiert auf, ob die zugriffsanforderung über das extranet oder das Intranet erfolgt.  
  
### <a name="to-configure-mfa-globally-based-on-users-device-data"></a>Konfiguration der MFA Global basierend auf Benutzerdaten Gerät  
  
1.  Auf dem Verbundserver das Windows PowerShell-Befehlsfenster geöffnet, und führen Sie den folgenden Befehl aus.  
  

    $MfaClaimRule = "c: [Typ == '" https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser'", Wert '" True_or_false"' ==]  
     = > Problem (Type = "" https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'", Wert =" "https://schemas.microsoft.com/claims/multipleauthn'"); "  
  
    Set-AdfsAdditionalAuthenticationRule $MfaClaimRule  

  
> [!NOTE]  
> Sicher, dass Sie ersetzen *< True\_or\_false >* entweder mit `true` oder `false`. Der Wert hängt von der bestimmten Bedingung, die basiert ist, ob das Gerät Workplace\ angehören oder nicht.  
  
### <a name="to-configure-mfa-globally-if-the-access-request-comes-from-the-extranet-and-from-a-non-workplace-joined-device"></a>MFA global zu konfigurieren, wenn die zugriffsanforderung über das extranet und von einem Gerät Workplace\ eingebundene erfolgt.  
  
1.  Auf dem Verbundserver das Windows PowerShell-Befehlsfenster geöffnet, und führen Sie den folgenden Befehl aus.  
  
 
    `Set-AdfsAdditionalAuthenticationRule "c:[Type == '"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser'", Value == '"true_or_false'"] && c2:[Type == '"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork'", Value == '" true_or_false '"] => issue(Type = '"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'", Value ='"https://schemas.microsoft.com/claims/multipleauthn'");" ` 
 
  
> [!NOTE]  
> Sicherstellen, dass beide ersetzen *< True\_or\_false >* entweder mit `true` oder `false`, abhängig von Ihrer spezifischen regelbedingungen. Die regelbedingungen sind abhängig davon, ob das Gerät Workplace\ eingebunden ist und ob der Zugriff erfolgt über das extranet erfolgt oder Intranet.  
  
### <a name="to-configure-mfa-globally-if-access-comes-from-an-extranet-user-that-belongs-to-a-certain-group"></a>Konfiguration der MFA Global Zugriff über ein extranet Benutzer stammt, der einer bestimmten Gruppe gehört  
  
1.  Auf dem Verbundserver das Windows PowerShell-Befehlsfenster geöffnet, und führen Sie den folgenden Befehl aus.  
  

    Set-AdfsAdditionalAuthenticationRule "c: [Typ == `"https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid`", Wert == `"group_SID`"] & & c2: [Typ == `"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`", Wert == `"true_or_false`"] = > Problem (Type = `"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod`", Wert = "" https://schemas.microsoft.com/claims/
      
> [!NOTE]  
> Sicher, dass Sie ersetzen *< Group\_SID >* mit dem Wert, der die Gruppen-SID und *< True\_or\_false >* entweder mit `true` oder `false`, hängt von der bestimmten Bedingung, die basiert auf, ob der Zugriff erfolgt über das extranet erfolgt oder Intranet.  
  
### <a name="to-grant-access-to-an-application-based-on-user-data-via-windows-powershell"></a>So gewähren Sie den Zugriff auf eine Anwendung basierend auf Benutzerdaten über Windows PowerShell  
  
1.  Auf dem Verbundserver das Windows PowerShell-Befehlsfenster geöffnet, und führen Sie den folgenden Befehl aus.  
  
    ```  
    $rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust  
  
    ```  
  
> [!NOTE]  
> Sicher, dass Sie ersetzen *< Relying\_party\_trust >* mit dem Wert der Vertrauensstellung der vertrauenden Seite.  
  
2.  Führen Sie in der gleichen Windows PowerShell-Befehlsfenster den folgenden Befehl ein.  
  
    ```  
  
      $GroupAuthzRule = "@RuleTemplate = `“Authorization`” @RuleName = `"Foo`" c:[Type == `"https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid`", Value =~ `"^(?i)<group_SID>$`"] =>issue(Type = `"https://schemas.microsoft.com/authorization/claims/deny`", Value = `"DenyUsersWithClaim`");"  
    Set-AdfsRelyingPartyTrust –TargetRelyingParty $rp –IssuanceAuthorizationRules $GroupAuthzRule  
    ```  
  
> [!NOTE]  
> > Sicher, dass Sie ersetzen *< Group\_SID >* mit dem Wert der SID der AD-Gruppe.  
  
### <a name="to-grant-access-to-an-application-that-is-secured-by-ad-fs-only-if-this-users-identity-was-validated-with-mfa"></a>Um den Zugriff auf eine Anwendung zu gewähren, die von AD FS nur, wenn die Identität des Benutzers geschützt ist wurde mit der MFA bestätigt  
  
1.  Auf dem Verbundserver das Windows PowerShell-Befehlsfenster geöffnet, und führen Sie den folgenden Befehl aus.  
  

    `$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust ` 
 
  
> [!NOTE]  
> Sicher, dass Sie ersetzen *< Relying\_party\_trust >* mit dem Wert der Vertrauensstellung der vertrauenden Seite.  
  
2.  Führen Sie in der gleichen Windows PowerShell-Befehlsfenster den folgenden Befehl ein.  
  
    ```  
    $GroupAuthzRule = "@RuleTemplate = `"Authorization`"  
    @RuleName = `"PermitAccessWithMFA`"  
    c:[Type == `"https://schemas.microsoft.com/claims/authnmethodsreferences`", Value =~ `"^(?i)https://schemas\.microsoft\.com/claims/multipleauthn$`"] => issue(Type = `"https://schemas.microsoft.com/authorization/claims/permit`", Value = ‘“PermitUsersWithClaim’");"  
  
    ```  
  
### <a name="to-grant-access-to-an-application-that-is-secured-by-ad-fs-only-if-the-access-request-comes-from-a-workplace-joined-device-that-is-registered-to-the-user"></a>Gewähren Sie den Zugriff auf eine Anwendung, die von AD FS nur gesichert ist, wenn die zugriffsanforderung von einem Workplace\ eingebundenen Gerät, die registriert ist erfolgt, für den Benutzer  
  
1.  Auf dem Verbundserver das Windows PowerShell-Befehlsfenster geöffnet, und führen Sie den folgenden Befehl aus.  
  
    ```  
    $rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust  
  
    ```  
  
> [!NOTE]  
> Sicher, dass Sie ersetzen *< Relying\_party\_trust >* mit dem Wert der Vertrauensstellung der vertrauenden Seite.  
  
2.  Führen Sie in der gleichen Windows PowerShell-Befehlsfenster den folgenden Befehl ein.  
  

    $GroupAuthzRule = "@RuleTemplate = `"Authorization`"  
    @RuleName = `"PermitAccessFromRegisteredWorkplaceJoinedDevice`"  
    "c:" [Typ == `"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser`", Wert = ~ `"^(?i)true$`"] = > Problem (Type = `"https://schemas.microsoft.com/authorization/claims/permit`", Wert = `"PermitUsersWithClaim`");  
  

  
### <a name="to-grant-access-to-an-application-that-is-secured-by-ad-fs-only-if-the-access-request-comes-from-a-workplace-joined-device-that-is-registered-to-a-user-whose-identity-has-been-validated-with-mfa"></a>Gewähren Sie den Zugriff auf eine Anwendung, die von AD FS nur gesichert ist, wenn die zugriffsanforderung von einem Workplace\ eingebundenen Gerät, die registriert ist für einen Benutzer stammt, dessen Identität mit der MFA bestätigt wurde  
  
1.  Auf dem Verbundserver das Windows PowerShell-Befehlsfenster geöffnet, und führen Sie den folgenden Befehl aus.  
  
 
    `$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust ` 
 
  
> [!NOTE]  
> Sicher, dass Sie ersetzen *< Relying\_party\_trust >* mit dem Wert der Vertrauensstellung der vertrauenden Seite.  
  
2.  Führen Sie in der gleichen Windows PowerShell-Befehlsfenster den folgenden Befehl ein.  
  
    ```  
    $GroupAuthzRule = ‘@RuleTemplate = “Authorization”  
    @RuleName = “RequireMFAOnRegisteredWorkplaceJoinedDevice”  
    c1:[Type == `"https://schemas.microsoft.com/claims/authnmethodsreferences`", Value =~ `"^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$`"] &&  
    c2:[Type == `"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser`", Value =~ `"^(?i)true$”] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit`", Value = `"PermitUsersWithClaim`");"  
  
    ```  
  
### <a name="to-grant-extranet-access-to-an-application-secured-by-ad-fs-only-if-the-access-request-comes-from-a-user-whose-identity-has-been-validated-with-mfa"></a>So gewähren Sie extranet-Zugriff auf eine Anwendung, die von AD FS geschützt werden, nur dann, wenn die zugriffsanforderung von einem Benutzer stammt, dessen Identität mit der MFA bestätigt wurde  
  
1.  Auf dem Verbundserver das Windows PowerShell-Befehlsfenster geöffnet, und führen Sie den folgenden Befehl aus.  
  
 
    `$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust`  

  
> [!NOTE]  
> Sicher, dass Sie ersetzen *< Relying\_party\_trust >* mit dem Wert der Vertrauensstellung der vertrauenden Seite.  
  
2.  Führen Sie in der gleichen Windows PowerShell-Befehlsfenster den folgenden Befehl ein.  
  

    $GroupAuthzRule = "@RuleTemplate = `"Authorization`"  
    @RuleName = `"RequireMFAForExtranetAccess`"  
    C1: [Typ == `"https://schemas.microsoft.com/claims/authnmethodsreferences`", Wert = ~ `"^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$`"] & &  
    C2: [Typ == `"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`", Wert = ~ `"^(?i)false$`"] = > Problem (Type = `"https://schemas.microsoft.com/authorization/claims/permit`", Wert = `"PermitUsersWithClaim`"); "  

## <a name="additional-references"></a>Weitere Verweise  

[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md)
