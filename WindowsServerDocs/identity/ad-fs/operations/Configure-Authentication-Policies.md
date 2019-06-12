---
ms.assetid: 8e7015bc-c489-4ec7-8b6e-3ece90f72317
title: Konfigurieren von Authentifizierungsrichtlinien
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 2215f172128a533e0e0d4e10b72be53ad455a262
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444962"
---
# <a name="configure-authentication-policies"></a>Konfigurieren von Authentifizierungsrichtlinien

In AD FS in Windows Server 2012 R2 den Zugriff auf Steuerelement, und der Authentifizierungsmechanismus verbessert, mit mehreren Faktoren ab, die Benutzer, Gerät, Standort und die Authentifizierung Daten enthalten. Diese Verbesserungen können Sie entweder über die Benutzeroberfläche oder über Windows PowerShell, um das Risiko von Gewähren von Berechtigungen für AD FS zu verwalten\-gesicherte Anwendungen über mehrere\-berücksichtigen, Zugriffssteuerung und mehreren\--Factor Authentication, die für Benutzer von Benutzeridentität oder der Gruppenmitgliedschaft, Netzwerkadresse, Gerätedaten, die Arbeitsplatz ist basieren\-hinzugefügt, und der Zustand über, wenn der Authentifizierungs mit mehreren\--Factor Authentication \(MFA\) durchgeführt wurde.  

Weitere Informationen zu MFA und mehreren\-berücksichtigen Sie die Zugriffssteuerung in Active Directory Federation Services \(AD FS\) in Windows Server 2012 R2, finden Sie unter den folgenden Themen:  


-   [Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose zweistufige Authentifizierung bei allen Unternehmensanwendungen](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)

-   [Verwalten von Risiken mit der bedingten Zugriffssteuerung](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md)

-   [Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)

## <a name="configure-authentication-policies-via-the-ad-fs-management-snap-in"></a>Konfigurieren von Authentifizierungsrichtlinien über die AD FS-Verwaltungs-Snap\-in  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um diese Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   

In AD FS in Windows Server 2012 R2 können Sie eine Authentifizierungsrichtlinie für einen globalen Bereich angeben, die für alle Anwendungen und Dienste, die von AD FS geschützt sind. Sie können auch Authentifizierungsrichtlinien für bestimmte Anwendungen und Dienste, die abhängig von Vertrauensstellungen und werden durch AD FS gesicherten festlegen. Angeben von eine Authentifizierungsrichtlinie für eine bestimmte Anwendung pro vertrauender Seite Vertrauensstellung wird die globalen Authentifizierungsrichtlinie nicht überschrieben. Wenn die globalen oder pro vertrauender Seite Authentifizierungsrichtlinie die MFA, MFA Vertrauensstellung wird immer dann ausgelöst, wenn der Benutzer versucht, diese Vertrauensstellung der vertrauenden Seite zu authentifizieren. Die globale Authentifizierungsrichtlinie ist ein Fallback für Partei-Vertrauensstellungen der vertrauenden Seite für Anwendungen und Dienste, die keine spezielle Authentifizierungsrichtlinie konfiguriert haben. 

## <a name="to-configure-primary-authentication-globally-in-windows-server-2012-r2"></a>Konfigurieren der primären Authentifizierung Global in Windows Server 2012 R2 

1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  

2.  In AD FS ausrichten\-, klicken Sie auf **Authentifizierungsrichtlinien**.  

3.  In der **primäre Authentifizierung** auf **bearbeiten** neben **globale Einstellungen**. Sie können auch nach rechts\-klicken Sie auf **Authentifizierungsrichtlinien**, und wählen Sie **globale primäre Authentifizierung bearbeiten**, oder klicken Sie unter der **Aktionen** wählen Sie im Bereich  **Globale primäre Authentifizierung bearbeiten**.  
![Auth-Richtlinien](media/Configure-Authentication-Policies/authpolicy1.png)

4.  In der **globale Authentifizierungsrichtlinie bearbeiten** Fenster auf die **primären** Registerkarte können Sie die folgenden Einstellungen als Teil der globalen Authentifizierungsrichtlinie konfigurieren:  

    -   Authentifizierungsmethoden für die primäre Authentifizierung verwendet werden. Sie können die verfügbaren Authentifizierungsmethoden unter Auswählen der **Extranet** und **Intranet**.  

    -   Die Geräteauthentifizierung über den **Geräteauthentifizierung aktivieren** Kontrollkästchen. Weitere Informationen finden Sie unter [Join to Workplace from Any Device for SSO and Seamless Second Factor Authentication Across Company Applications](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md).  
![Auth-Richtlinien](media/Configure-Authentication-Policies/authpolicy2.png)  

## <a name="to-configure-primary-authentication-per-relying-party-trust"></a>So konfigurieren Sie die primäre Authentifizierung pro vertrauender Seite Vertrauensstellung  

1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  

2.  In AD FS ausrichten\-, klicken Sie auf **Authentifizierungsrichtlinien**\\**pro Relying Party Trust**, und klicken Sie dann auf die Vertrauensstellung der vertrauenden Seite für das Konfigurieren der Authentifizierung werden sollen Richtlinien.  

3.  Entweder direkt\-klicken Sie auf die Vertrauensstellung der vertrauenden Seite für die Sie zum Konfigurieren von Authentifizierungsrichtlinien, und wählen Sie dann möchten **benutzerdefinierte primäre Authentifizierung bearbeiten**, oder klicken Sie unter den **Aktionen** Bereich Wählen Sie **benutzerdefinierte primäre Authentifizierung bearbeiten**.  
![Auth-Richtlinien](media/Configure-Authentication-Policies/authpolicy5.png)   

4.  In der **Authentifizierungsrichtlinie bearbeiten, für die < der vertrauenden Seite\_Partei\_Vertrauensstellung\_Name >** Fenster unter der **primären** Registerkarte können Sie die folgende Einstellungen konfigurieren als Teil der **pro Vertrauensstellung der vertrauenden Seite** Authentifizierungsrichtlinie:  

    -   Gibt an, ob Benutzer ihre Anmeldeinformationen jedes Mal bei der Registrierung angeben müssen\-im über die **Benutzer sind erforderlich, um die Anmeldeinformationen jedes Mal bei der Registrierung angeben\-in** Kontrollkästchen.  
![Auth-Richtlinien](media/Configure-Authentication-Policies/authpolicy6.png) 

## <a name="to-configure-multi-factor-authentication-globally"></a>So konfigurieren Sie die Multi-Factor Authentication Global  

1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  

2.  In AD FS ausrichten\-, klicken Sie auf **Authentifizierungsrichtlinien**.  

3.  In der **mit mehreren\-zweistufige Authentifizierung** auf **bearbeiten** neben **globale Einstellungen**. Können Sie auch die rechten Maustaste\-klicken Sie auf **Authentifizierungsrichtlinien**, und wählen Sie **bearbeiten globaler Multi\-zweistufige Authentifizierung**, oder klicken Sie unter der **Aktionen**wählen Sie im Bereich **bearbeiten globaler mehrere\-zweistufige Authentifizierung**.  
![Auth-Richtlinien](media/Configure-Authentication-Policies/authpolicy8.png)   

4.  In der **globale Authentifizierungsrichtlinie bearbeiten** Fenster unter dem **mit mehreren\-Faktor** Registerkarte können Sie die folgenden Einstellungen konfigurieren, als Teil der globalen Multi\-Faktor Authentifizierungsrichtlinie für die:  

    -   Einstellungen und Bedingungen für MFA über die verfügbaren Optionen unter der **Benutzer\/Gruppen**, **Geräte**, und **Speicherorte** Abschnitte.  

    -   Um MFA für diese Einstellungen zu aktivieren, müssen Sie mindestens eine zusätzliche Authentifizierungsmethode auswählen. **Zertifikatauthentifizierung** ist die Standardoption zur Verfügung. Sie können auch andere benutzerdefinierte zusätzliche Authentifizierungsmethoden, z. B. Windows Azure Active Authentication konfigurieren. Weitere Informationen finden Sie unter [Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md).  

> [!WARNING]  
> Sie können zusätzliche Authentifizierungsmethoden nur global konfigurieren.  
![Auth-Richtlinien](media/Configure-Authentication-Policies/authpolicy9.png)  

## <a name="to-configure-multi-factor-authentication-per-relying-party-trust"></a>So konfigurieren Sie mehrere\--Factor Authentication pro vertrauender Seite Vertrauensstellung  

1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  

2.  In AD FS ausrichten\-, klicken Sie auf **Authentifizierungsrichtlinien**\\**pro Relying Party Trust**, und klicken Sie dann auf die Vertrauensstellung der vertrauenden Seite für die Konfiguration der MFA werden sollen.  

3.  Entweder direkt\-klicken Sie auf die Vertrauensstellung der vertrauenden Seite für die Sie zum Konfigurieren der mehrstufigen Authentifizierung, und wählen Sie dann möchten **mit mehreren Bearbeiten von benutzerdefinierten\-zweistufige Authentifizierung**, oder klicken Sie unter den **Aktionen** Bereich Wählen Sie **mit mehreren Bearbeiten von benutzerdefinierten\-zweistufige Authentifizierung**.  

4.  In der **Authentifizierungsrichtlinie bearbeiten, für die < der vertrauenden Seite\_Partei\_Vertrauensstellung\_Name >** Fenster unter der **mit mehreren\-Faktor** Registerkarte können Sie Konfigurieren Sie die folgenden Einstellungen als Teil der pro\-Richtlinie vertrauende Seite Trust-Authentifizierung:  

    -   Einstellungen und Bedingungen für MFA über die verfügbaren Optionen unter der **Benutzer\/Gruppen**, **Geräte**, und **Speicherorte** Abschnitte.  

## <a name="configure-authentication-policies-via-windows-powershell"></a>Konfigurieren von Authentifizierungsrichtlinien mit Windows PowerShell  
Windows PowerShell ermöglicht mehr Flexibilität bei der Verwendung von verschiedenen Faktoren ab, der Zugriffssteuerung und die Regeln der Authentifizierungsmechanismus, der in AD FS unter Windows Server 2012 R2 zum Konfigurieren von Authentifizierungsrichtlinien für die und Autorisierung zur Verfügung stehen, die erforderlich sind Implementieren von "true" für den bedingten Zugriff für Ihre AD FS \-gesicherte Ressourcen.  

Die Mindestanforderung zum Abschließen dieser Verfahren ist die Mitgliedschaft in Administratoren oder einer entsprechenden Gruppe auf dem lokalen Computer.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/"go.Microsoft.com"\/Fwlink\/? LinkId\=83477\).   

### <a name="to-configure-an-additional-authentication-method-via-windows-powershell"></a>So konfigurieren Sie eine zusätzliche Authentifizierungsmethode über Windows PowerShell  

1.  Öffnen Sie auf dem Verbundserver Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  


~~~
`Set-AdfsGlobalAuthenticationPolicy –AdditionalAuthenticationProvider CertificateAuthentication  `
~~~


> [!WARNING]  
> Mit dem Befehl `Get-AdfsGlobalAuthenticationPolicy` können Sie überprüfen, ob der oben angegebene Befehl erfolgreich ausgeführt wurde.  

### <a name="to-configure-mfa-per-relying-party-trust-that-is-based-on-a-users-group-membership-data"></a>So konfigurieren Sie MFA pro\-Vertrauensstellung der vertrauenden, die basierend auf der Gruppenmitgliedschaftsdaten eines Benutzers  

1.  Öffnen Sie auf dem Verbundserver das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus:  


~~~
`$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust`  
~~~


> [!WARNING]  
> Ersetzen Sie Sie sicher, dass *< der vertrauenden Seite\_Partei\_Vertrauensstellung >* durch den Namen der Vertrauensstellung der vertrauenden Seite.  

2. Führen Sie in der gleichen Windows PowerShell-Befehlsfenster den folgenden Befehl ein.  


~~~
$MfaClaimRule = “c:[Type == ‘“https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid’”, Value =~ ‘“^(?i) <group_SID>$’”] => issue(Type = ‘“https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod’”, Value ‘“https://schemas.microsoft.com/claims/multipleauthn’”);” 

Set-AdfsRelyingPartyTrust –TargetRelyingParty $rp –AdditionalAuthenticationRules $MfaClaimRule
~~~


> [!NOTE]  
> Achten Sie darauf, ersetzen Sie < Gruppe\_SID > mit dem Wert der Sicherheits-ID \(SID\) Ihrer Active Directory \(AD\) Gruppe.  

### <a name="to-configure-mfa-globally-based-on-users-group-membership-data"></a>So konfigurieren Sie MFA auf Grundlage Global Gruppenmitgliedschaftsdaten des Benutzers  

1.  Öffnen Sie auf dem Verbundserver Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  


~~~
$MfaClaimRule = “c:[Type == ‘" https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid’", Value == ‘"group_SID’"]  
 => issue(Type = ‘"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod’", Value = ‘"https://schemas.microsoft.com/claims/multipleauthn’");”  

Set-AdfsAdditionalAuthenticationRule $MfaClaimRule  
~~~


> [!NOTE]  
> Ersetzen Sie Sie sicher, dass *< Gruppe\_SID >* mit dem Wert der SID der AD-Gruppe.  

### <a name="to-configure-mfa-globally-based-on-users-location"></a>So konfigurieren Sie MFA auf Global auf Grundlage des Benutzerstandorts  

1.  Öffnen Sie auf dem Verbundserver Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  


~~~
$MfaClaimRule = “c:[Type == ‘" https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork’", Value == ‘"true_or_false’"]  
 => issue(Type = ‘"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod’", Value = ‘"https://schemas.microsoft.com/claims/multipleauthn’");”  

Set-AdfsAdditionalAuthenticationRule $MfaClaimRule  
~~~



> [!NOTE]  
> Ersetzen Sie Sie sicher, dass *< true\_oder\_"false" >* mit `true` oder `false`. Der Wert hängt von der bestimmten regelbedingung, die abhängig ist, gibt an, ob die zugriffsanforderung über das extranet oder das Intranet erfolgt.  

### <a name="to-configure-mfa-globally-based-on-users-device-data"></a>Konfiguration der MFA Global basierend auf Daten der Benutzer und Gerät  

1.  Öffnen Sie auf dem Verbundserver Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  


~~~
$MfaClaimRule = "c:[Type == ‘" https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser’", Value == ‘"true_or_false"']  
 => issue(Type = ‘"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod’", Value = ‘"https://schemas.microsoft.com/claims/multipleauthn’");"  

Set-AdfsAdditionalAuthenticationRule $MfaClaimRule  
~~~


> [!NOTE]  
> Ersetzen Sie Sie sicher, dass *< true\_oder\_"false" >* mit `true` oder `false`. Der Wert hängt von der bestimmten regelbedingung, die abhängig ist, gibt an, ob das Gerät dem Arbeitsplatz ist\-verknüpft oder nicht.  

### <a name="to-configure-mfa-globally-if-the-access-request-comes-from-the-extranet-and-from-a-non-workplace-joined-device"></a>MFA Global konfigurieren, wenn die zugriffsanforderung über das extranet und über eine nicht erfolgt\-Workplace\-verbundenen Gerät  

1.  Öffnen Sie auf dem Verbundserver Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  


~~~
`Set-AdfsAdditionalAuthenticationRule "c:[Type == '"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser'", Value == '"true_or_false'"] && c2:[Type == '"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork'", Value == '" true_or_false '"] => issue(Type = '"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'", Value ='"https://schemas.microsoft.com/claims/multipleauthn'");" ` 
~~~


> [!NOTE]  
> Achten Sie darauf, ersetzen Sie beide Instanzen von *< true\_oder\_"false" >* mit `true` oder `false`, abhängig vom Ihrem spezifischen regelbedingungen. Die-regelbedingungen beruhen auf gibt an, ob das Gerät dem Arbeitsplatz ist\-angehören oder nicht und gibt an, ob die zugriffsanforderung erfolgt über das extranet oder Intranet.  

### <a name="to-configure-mfa-globally-if-access-comes-from-an-extranet-user-that-belongs-to-a-certain-group"></a>MFA Global konfigurieren, wenn der Zugriff von einer extranet Benutzer stammen, die einer bestimmten Gruppe gehört  

1.  Öffnen Sie auf dem Verbundserver Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  


~~~
Set-AdfsAdditionalAuthenticationRule "c:[Type == `"https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid`", Value == `"group_SID`"] && c2:[Type == `"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`", Value== `"true_or_false`"] => issue(Type = `"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod`", Value =`"https://schemas.microsoft.com/claims/
~~~

> [!NOTE]  
> Ersetzen Sie Sie sicher, dass *< Gruppe\_SID >* mit dem Wert, der die Gruppen-SID und *< true\_oder\_"false" >* mit `true` oder `false`, welche hängt von der bestimmten regelbedingung, die abhängig ist, gibt an, ob die zugriffsanforderung über das extranet erfolgt oder Intranet.  

### <a name="to-grant-access-to-an-application-based-on-user-data-via-windows-powershell"></a>Gewähren von Zugriff auf eine Anwendung, die basierend auf Benutzerdaten über Windows PowerShell  

1.  Öffnen Sie auf dem Verbundserver Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  

    ```  
    $rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust  

    ```  

> [!NOTE]  
> Ersetzen Sie Sie sicher, dass *< der vertrauenden Seite\_Partei\_Vertrauensstellung >* mit dem Wert der Vertrauensstellung der vertrauenden Seite.  

2. Führen Sie in der gleichen Windows PowerShell-Befehlsfenster den folgenden Befehl ein.  

   ```  

     $GroupAuthzRule = "@RuleTemplate = `“Authorization`” @RuleName = `"Foo`" c:[Type == `"https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid`", Value =~ `"^(?i)<group_SID>$`"] =>issue(Type = `"https://schemas.microsoft.com/authorization/claims/deny`", Value = `"DenyUsersWithClaim`");"  
   Set-AdfsRelyingPartyTrust –TargetRelyingParty $rp –IssuanceAuthorizationRules $GroupAuthzRule  
   ```  

> [!NOTE]  
> > Ersetzen Sie Sie sicher, dass *< Gruppe\_SID >* mit dem Wert der SID der AD-Gruppe.  

### <a name="to-grant-access-to-an-application-that-is-secured-by-ad-fs-only-if-this-users-identity-was-validated-with-mfa"></a>Um Zugriff auf eine Anwendung zu gewähren, die durch AD FS nur, wenn die Identität des Benutzers gesichert wird wurde mit der MFA bestätigt  

1.  Öffnen Sie auf dem Verbundserver Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  


~~~
`$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust ` 
~~~


> [!NOTE]  
> Ersetzen Sie Sie sicher, dass *< der vertrauenden Seite\_Partei\_Vertrauensstellung >* mit dem Wert der Vertrauensstellung der vertrauenden Seite.  

2. Führen Sie in der gleichen Windows PowerShell-Befehlsfenster den folgenden Befehl ein.  

   ```  
   $GroupAuthzRule = "@RuleTemplate = `"Authorization`"  
   @RuleName = `"PermitAccessWithMFA`"  
   c:[Type == `"https://schemas.microsoft.com/claims/authnmethodsreferences`", Value =~ `"^(?i)https://schemas\.microsoft\.com/claims/multipleauthn$`"] => issue(Type = `"https://schemas.microsoft.com/authorization/claims/permit`", Value = ‘“PermitUsersWithClaim’");"  

   ```  

### <a name="to-grant-access-to-an-application-that-is-secured-by-ad-fs-only-if-the-access-request-comes-from-a-workplace-joined-device-that-is-registered-to-the-user"></a>Gewähren von Zugriff auf eine Anwendung, die durch AD FS nur, wenn den Zugriff gesichert ist Anforderung eingeht, aus einem Arbeitsbereich\-eingebundenes Gerät, das für den Benutzer registriert ist  

1.  Öffnen Sie auf dem Verbundserver Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  

    ```  
    $rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust  

    ```  

> [!NOTE]  
> Ersetzen Sie Sie sicher, dass *< der vertrauenden Seite\_Partei\_Vertrauensstellung >* mit dem Wert der Vertrauensstellung der vertrauenden Seite.  

2. Führen Sie in der gleichen Windows PowerShell-Befehlsfenster den folgenden Befehl ein.  


~~~
$GroupAuthzRule = "@RuleTemplate = `"Authorization`"  
@RuleName = `"PermitAccessFromRegisteredWorkplaceJoinedDevice`"  
c:[Type == `"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser`", Value =~ `"^(?i)true$`"] => issue(Type = `"https://schemas.microsoft.com/authorization/claims/permit`", Value = `"PermitUsersWithClaim`");  
~~~



### <a name="to-grant-access-to-an-application-that-is-secured-by-ad-fs-only-if-the-access-request-comes-from-a-workplace-joined-device-that-is-registered-to-a-user-whose-identity-has-been-validated-with-mfa"></a>Gewähren von Zugriff auf eine Anwendung, die durch AD FS nur, wenn den Zugriff gesichert ist Anforderung eingeht, aus einem Arbeitsbereich\-Gerät mit domänenzugehörigkeit, die für einen Benutzer registriert ist, dessen Identität mit der MFA bestätigt wurde,  

1.  Öffnen Sie auf dem Verbundserver Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  


~~~
`$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust ` 
~~~


> [!NOTE]  
> Ersetzen Sie Sie sicher, dass *< der vertrauenden Seite\_Partei\_Vertrauensstellung >* mit dem Wert der Vertrauensstellung der vertrauenden Seite.  

2. Führen Sie in der gleichen Windows PowerShell-Befehlsfenster den folgenden Befehl ein.  

   ```  
   $GroupAuthzRule = ‘@RuleTemplate = “Authorization”  
   @RuleName = “RequireMFAOnRegisteredWorkplaceJoinedDevice”  
   c1:[Type == `"https://schemas.microsoft.com/claims/authnmethodsreferences`", Value =~ `"^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$`"] &&  
   c2:[Type == `"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser`", Value =~ `"^(?i)true$”] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit`", Value = `"PermitUsersWithClaim`");"  

   ```  

### <a name="to-grant-extranet-access-to-an-application-secured-by-ad-fs-only-if-the-access-request-comes-from-a-user-whose-identity-has-been-validated-with-mfa"></a>Extranet-Zugriff auf eine Anwendung, die durch AD FS gesicherten, nur dann, wenn die zugriffsanforderung von einem Benutzer stammt, dessen Identität mit der MFA bestätigt wurde, wurde, zu gewähren  

1.  Öffnen Sie auf dem Verbundserver Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  


~~~
`$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust`  
~~~


> [!NOTE]  
> Ersetzen Sie Sie sicher, dass *< der vertrauenden Seite\_Partei\_Vertrauensstellung >* mit dem Wert der Vertrauensstellung der vertrauenden Seite.  

2. Führen Sie in der gleichen Windows PowerShell-Befehlsfenster den folgenden Befehl ein.  


~~~
$GroupAuthzRule = "@RuleTemplate = `"Authorization`"  
@RuleName = `"RequireMFAForExtranetAccess`"  
c1:[Type == `"https://schemas.microsoft.com/claims/authnmethodsreferences`", Value =~ `"^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$`"] &&  
c2:[Type == `"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`", Value =~ `"^(?i)false$`"] => issue(Type = `"https://schemas.microsoft.com/authorization/claims/permit`", Value = `"PermitUsersWithClaim`");"  
~~~

## <a name="additional-references"></a>Weitere Verweise  

[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md)
