---
ms.assetid: 5728847d-dcef-4694-9080-d63bfb1fe24b
title: Zugriffssteuerungsrichtlinien in AD FS
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0b4549192bc4dab9edf3b2a10421325144ed0cd2
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="access-control-policies-in-windows-server-2012-r2-and-windows-server-2012-ad-fs"></a>Zugriffssteuerungsrichtlinien in Windows Server 2012 R2 und Windows Server 2012 AD FS

>Gilt für: Windows Server 2012 R2 und Windows Server 2012 

Stellen Sie die Richtlinien in diesem Artikel beschriebenen verwendet zwei Arten von Ansprüchen  
  
1.  Angeblich AD FS basierend auf den Informationen erstellt, der AD FS und Web Application Proxy kann untersuchen und zu überprüfen, wie die IP-Adresse des Clients, die direkte Verbindung mit AD FS oder den drahtlosen Zugriffspunkt.  
  
2.  Ansprüche von AD FS erstellt basierend auf den Informationen, die vom Client als HTTP-Header zu AD FS weitergeleitet  
  
>**Wichtige**: die Richtlinien wie im folgenden dokumentiert blockiert Windows 10-Domänenbeitritt und melden Sie sich auf Szenarien, die Zugriff auf die folgenden zusätzlichen Endpunkte erfordern

AD FS-Endpunkte für Windows 10-Domänenbeitritt und melden Sie sich auf erforderlich
- [verbunddienstname] / Adfs/Services/Vertrauensstellung/2005/Windowstransport
- [verbunddienstname] / Adfs/Services/Trust/13/Windowstransport
- [verbunddienstname] / Adfs/Services/Vertrauensstellung/2005/Usernamemixed
- [verbunddienstname] / Adfs/Services/Trust/13/Usernamemixed 
- [verbunddienstname] / Adfs/Services/Vertrauensstellung/2005/Certificatemixed
- [verbunddienstname] / Adfs/Services/Trust/13/Certificatemixed

Aktualisieren Sie zum Beheben alle Richtlinien, die verweigert basierend auf den Endpunkt Anspruch Ausnahme für die oben genannten Endpunkte zu ermöglichen.

Z. B. die Regel unten:

`c1:[Type == "https://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "/adfs/ls/"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`  

würde aktualisiert werden:

`c1:[Type == "https://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "(/adfs/ls/)|(/adfs/services/trust/2005/windowstransport)|(/adfs/services/trust/13/windowstransport)|(/adfs/services/trust/2005/usernamemixed)|(/adfs/services/trust/13/usernamemixed)|(/adfs/services/trust/2005/certificatemixed)|(/adfs/services/trust/13/certificatemixed)"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`



> [!NOTE]
>  Ansprüche aus dieser Kategorie sollte nur zum Implementieren von Business-Richtlinien verwendet werden und nicht als Sicherheitsrichtlinien für den Zugriff auf das Netzwerk zu schützen.  Es ist möglich, dass nicht autorisierte Clients Header mit falsche Informationen als eine Möglichkeit für den Zugriff zu senden.  
  
Die Richtlinien in diesem Artikel beschriebenen sollte immer mit einer anderen Authentifizierungsmethode, z. B. Benutzernamen und Kennwörter oder Multi-Factor Authentication verwendet werden.  
  
## <a name="client-access-policies-scenarios"></a>Szenarien der Client-Richtlinien  
  
|**Szenario**|**Beschreibung**| 
| --- | --- | 
|Szenario 1: Blockiert den externen Zugriff auf Office 365|Office 365-Zugriff wird von allen Clients im internen Unternehmensnetzwerk zulässig, aber von externen Clientanforderungen werden basierend auf der IP-Adresse des externen Client abgelehnt.|  
|Szenario 2: Blockiert den externen Zugriff auf Office 365 mit Ausnahme von Exchange ActiveSync|Office 365-Zugriff ist möglich, alle Clients im internen Unternehmensnetzwerk, sowie alle externen Client-Geräte, z. B. Smartphones, die von Exchange ActiveSync verwenden. Alle anderen externen Clients, z. B. die Verwendung von Outlook, werden blockiert.|  
|Szenario 3: Blockieren Sie alle externen Zugriff auf Office 365 mit Ausnahme von browserbasierten Anwendungen|Blöcke der externe Zugriff auf Office 365, mit Ausnahme der passiven (Browser-basiert) Anwendungen wie Outlook Web Access oder SharePoint Online.|  
|Szenario 4: Blockieren Sie alle externen Zugriff auf Office 365 mit Ausnahme der angegebenen Active Directory-Gruppen|Dieses Szenario wird für das Testen und Überprüfen der Bereitstellung der Zugriffsrichtlinie verwendet. Der externe Zugriff auf Office 365 wird nur für eine oder mehrere Active Directory-Gruppe blockiert. Sie können auch auf externe Zugriff nur auf Mitglieder einer Gruppe verwendet werden.|  
  
## <a name="enabling-client-access-policy"></a>Aktivieren des Client-Richtlinie  
 Um die Client-Richtlinien in AD FS unter Windows Server 2012 R2 zu aktivieren, müssen Sie die Microsoft Office 365-Identitätsplattform Vertrauensstellung einer vertrauenden Seite aktualisieren. Wählen Sie eine der den Beispielszenarien aus, um den Anspruchsregeln konfigurieren, auf die **Microsoft Office 365-Identitätsplattform** Vertrauensstellung für vertrauende Seiten, am besten den Erfordernissen Ihrer Organisation entspricht.  
  
###  <a name="scenario1"></a>Szenario 1: Blockiert den externen Zugriff auf Office 365  
 Dabei Policy Client Zugriff ermöglicht den Zugriff auf alle internen Clients und blockiert alle externen Clients basierend auf der IP-Adresse des externen Clients. Die folgenden Verfahren können Sie die richtigen Ausstellung Autorisierungsregeln mit dem Office 365 für Ihr Szenario ausgewählte Vertrauensstellung einer vertrauenden Seite hinzufügen.  
  
##### <a name="to-create-rules-to-block-all-external-access-to-office-365"></a>Zum Erstellen von Regeln zum Blockieren von externen Zugriff auf Office 365  
  
1.  Von **Server-Manager**, klicken Sie auf **Tools**, klicken Sie dann auf **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD Fs\vertrauensstellungen**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten**, mit der rechten Maustaste die **Microsoft Office 365-Identitätsplattform** vertrauen, und klicken Sie dann auf **Anspruchsregeln bearbeiten**.  
  
3.  In der **Anspruchsregeln bearbeiten** wählen Sie im Dialogfeld die **Ausstellungsautorisierungsregeln** Registerkarte, und klicken Sie dann auf **Regel hinzufügen** , den Anspruch Regel-Assistenten zu starten.  
  
4.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **Senden von Ansprüchen mit benutzerdefinierter Regel**, und klicken Sie dann auf **Weiter**.  
  
5.  Auf der **Regel konfigurieren** Seite unter **Name der Anspruchsregel**, geben Sie der Anzeigenamen für diese Regel ein, z. B. "liegt außerhalb des gewünschten Bereichs an sowie alle Ansprüche in IP-deny". Klicken Sie unter **benutzerdefinierte Regel**, geben oder fügen Sie die folgende Syntax anspruchsregelsprache (ersetzen Sie den Wert für "X-ms-weitergeleitet-Client-IP-" in eine gültige IP-Ausdruck oben):  
`c1:[Type == " https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");` </br>
6.  Klicken Sie auf **Fertig stellen**. Stellen Sie sicher, dass die neue Regel in der Liste von Ausstellungsautorisierungsregeln vor auf den Standardwert angezeigt wird **ermöglichen den Zugriff auf alle Benutzer** Regel (die Deny-Regel Vorrang, obwohl sie weiter oben in der Liste angezeigt wird).  Wenn Sie nicht die standardmäßige Zugriffsregel zulassen verfügen, können Sie eine am Ende der Liste mithilfe der anspruchsregelsprache wie folgt hinzufügen:  </br>
    
    `c:[] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true"); ` 

7.  Speichern Sie die neuen Regeln in der **Anspruchsregeln bearbeiten** Dialogfeld, klicken Sie auf **OK**. Die resultierende Liste sieht wie folgt aus.  
  
     ![Ausstellungsautorisierungsregeln](media/Access-Control-Policies-W2K12/clientaccess1.png "ADFS_Client_Access_1")  
  
###  <a name="scenario2"></a>Szenario 2: Blockiert den externen Zugriff auf Office 365 mit Ausnahme von Exchange ActiveSync  
 Im folgende Beispiel ermöglicht den Zugriff auf alle Office 365-Anwendungen wie Exchange Online von internen Clients wie Outlook. Es blockiert den Zugriff von Clients, die sich außerhalb des Unternehmensnetzwerks befinden wie die IP-Adresse von Clients, mit Ausnahme von Exchange ActiveSync-Clients, z. B. Smartphones angegeben.  
  
##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-exchange-activesync"></a>Zum Erstellen von Regeln zum Blockieren von externen Zugriff auf Office 365 mit Ausnahme von Exchange ActiveSync  
  
1.  Von **Server-Manager**, klicken Sie auf **Tools**, klicken Sie dann auf **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD Fs\vertrauensstellungen**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten**, mit der rechten Maustaste die **Microsoft Office 365-Identitätsplattform** vertrauen, und klicken Sie dann auf **Anspruchsregeln bearbeiten**.  
  
3.  In der **Anspruchsregeln bearbeiten** wählen Sie im Dialogfeld die **Ausstellungsautorisierungsregeln** Registerkarte, und klicken Sie dann auf **Regel hinzufügen** , den Anspruch Regel-Assistenten zu starten.  
  
4.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **Senden von Ansprüchen mit benutzerdefinierter Regel**, und klicken Sie dann auf **Weiter**.  
  
5.  Auf der **Regel konfigurieren** Seite unter **Name der Anspruchsregel**, geben Sie den Namen für diese Regel für Beispiel "liegt außerhalb des gewünschten Bereichs an sowie alle Ansprüche in IP-stellen Ipoutsiderange Anspruch". Klicken Sie unter **benutzerdefinierte Regel**, geben oder fügen Sie die folgende Syntax anspruchsregelsprache (ersetzen Sie den Wert für "X-ms-weitergeleitet-Client-IP-" in eine gültige IP-Ausdruck oben):  
    
    `c1:[Type == " https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`  

6.  Klicken Sie auf **Fertig stellen**. Stellen Sie sicher, dass in die neue Regel wird der **Ausstellungsautorisierungsregeln** Liste.  
  
7.  Weiter, in der **Anspruchsregeln bearbeiten** Dialogfeld auf die **Ausstellungsautorisierungsregeln** auf **Regel hinzufügen** um den Anspruch Regel-Assistenten erneut zu starten.  
  
8.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **Senden von Ansprüchen mit benutzerdefinierter Regel**, und klicken Sie dann auf **Weiter**.  
  
9. Auf der **Regel konfigurieren** Seite unter **Name der Anspruchsregel**, geben Sie der Anzeigenamen für diese Regel ein, z. B. "Wenn eine IP-Adresse sich außerhalb des gewünschten Bereichs und es wird ein Anspruch nicht EAS X-ms-Clientanwendung verweigern". Klicken Sie unter **benutzerdefinierte Regel**, geben oder fügen Sie die folgende Syntax anspruchsregelsprache:  
  

    `c1:[Type == "https://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value != "Microsoft.Exchange.ActiveSync"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`  
  
10. Klicken Sie auf **Fertig stellen**. Stellen Sie sicher, dass in die neue Regel wird der **Ausstellungsautorisierungsregeln** Liste.  
  
11. Weiter, in der **Anspruchsregeln bearbeiten** Dialogfeld auf die **Ausstellungsautorisierungsregeln** auf **Regel hinzufügen** um den Anspruch Regel-Assistenten erneut zu starten.  
  
12. Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage,** wählen **Senden von Ansprüchen mit benutzerdefinierter Regel**, und klicken Sie dann auf **Weiter**.  
  
13. Auf der **Regel konfigurieren** Seite unter **Name der Anspruchsregel**, geben Sie den Namen für diese Regel, z. B. "überprüfen, ob Anwendung Anspruchs vorhanden ist". Klicken Sie unter **benutzerdefinierte Regel**, geben oder fügen Sie die folgende Syntax anspruchsregelsprache:  
  
    ```  
    NOT EXISTS([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application"]) => add(Type = "http://custom/xmsapplication", Value = "fail");  
    ```  
  
14. Klicken Sie auf **Fertig stellen**. Stellen Sie sicher, dass in die neue Regel wird der **Ausstellungsautorisierungsregeln** Liste.  
  
15. Weiter, in der **Anspruchsregeln bearbeiten** Dialogfeld auf die **Ausstellungsautorisierungsregeln** auf **Regel hinzufügen** um den Anspruch Regel-Assistenten erneut zu starten.  
  
16. Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage,** wählen **Senden von Ansprüchen mit benutzerdefinierter Regel**, und klicken Sie dann auf **Weiter**.  
  
17. Auf der **Regel konfigurieren** Seite unter **Name der Anspruchsregel**, geben Sie den Anzeigenamen für diese Regel ein, z. B. "deny Benutzer Ipoutsiderange" true "und einer Anwendung nicht". Klicken Sie unter **benutzerdefinierte Regel**, geben oder fügen Sie die folgende Syntax anspruchsregelsprache:  
  
`c1:[Type == "https://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://custom/xmsapplication", Value == "fail"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`</br>  
18. Klicken Sie auf **Fertig stellen**. Stellen Sie sicher, dass die neue Regel direkt unterhalb der vorherigen Regel angezeigt, und vor dem Regel auf den Standardwert ermöglichen den Zugriff auf alle Benutzer in der Ausstellungsautorisierungsregeln Liste (die Deny-Regel hat Vorrang, obwohl sie weiter oben in der Liste angezeigt wird).  </br>Wenn Sie nicht die standardmäßige Zugriffsregel zulassen verfügen, können Sie eine am Ende der Liste mithilfe der anspruchsregelsprache wie folgt hinzufügen:</br></br>      `c:[] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");`</br></br>
19. Speichern Sie die neuen Regeln in der **Anspruchsregeln bearbeiten** Dialogfeld auf OK. Die resultierende Liste sieht wie folgt aus.  
  
     ![Ausstellungsautorisierungsregeln](media/Access-Control-Policies-W2K12/clientaccess2.png )  
  
###  <a name="scenario3"></a>Szenario 3: Blockieren Sie alle externen Zugriff auf Office 365 mit Ausnahme von browserbasierten Anwendungen  
  
##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-browser-based-applications"></a>Zum Erstellen von Regeln zum Blockieren von externen Zugriff auf Office 365 mit Ausnahme der Browser-basierte Anwendungen  
  
1.  Von **Server-Manager**, klicken Sie auf **Tools**, klicken Sie dann auf **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD Fs\vertrauensstellungen**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten**, mit der rechten Maustaste die **Microsoft Office 365-Identitätsplattform** vertrauen, und klicken Sie dann auf **Anspruchsregeln bearbeiten**.  
  
3.  In der **Anspruchsregeln bearbeiten** wählen Sie im Dialogfeld die **Ausstellungsautorisierungsregeln** Registerkarte, und klicken Sie dann auf **Regel hinzufügen** , den Anspruch Regel-Assistenten zu starten.  
  
4.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **Senden von Ansprüchen mit benutzerdefinierter Regel**, und klicken Sie dann auf **Weiter**.  
  
5.  Auf der **Regel konfigurieren** Seite unter **Name der Anspruchsregel**, geben Sie den Namen für diese Regel für Beispiel "liegt außerhalb des gewünschten Bereichs an sowie alle Ansprüche in IP-stellen Ipoutsiderange Anspruch". Klicken Sie unter **benutzerdefinierte Regel**, geben oder fügen Sie die folgende Syntax anspruchsregelsprache (ersetzen Sie den Wert für "X-ms-weitergeleitet-Client-IP-" in eine gültige IP-Ausdruck oben):  </br>
`c1:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`   
6.  Klicken Sie auf **Fertig stellen**. Stellen Sie sicher, dass in die neue Regel wird der **Ausstellungsautorisierungsregeln** Liste.  
  
7.  Weiter, in der **Anspruchsregeln bearbeiten** Dialogfeld auf die **Ausstellungsautorisierungsregeln** auf **Regel hinzufügen** um den Anspruch Regel-Assistenten erneut zu starten.  
  
8.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage,** wählen **Senden von Ansprüchen mit benutzerdefinierter Regel**, und klicken Sie dann auf **Weiter**.  
  
9. Auf der **Regel konfigurieren** Seite unter **Name der Anspruchsregel**, geben Sie der Anzeigenamen für diese Regel ein, z. B. ", wenn eine IP-Adresse sich außerhalb des gewünschten Bereichs ist und der Endpunkt ist nicht/Adfs/ls, verweigern". Klicken Sie unter **benutzerdefinierte Regel**, geben oder fügen Sie die folgende Syntax anspruchsregelsprache:  
  
 
    `c1:[Type == "https://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "/adfs/ls/"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`  
  
10. Klicken Sie auf **Fertig stellen**. Stellen Sie sicher, dass die neue Regel in der Liste von Ausstellungsautorisierungsregeln vor auf den Standardwert angezeigt wird **ermöglichen den Zugriff auf alle Benutzer** Regel (die Deny-Regel Vorrang, obwohl sie weiter oben in der Liste angezeigt wird).  </br></br> Wenn Sie nicht die standardmäßige Zugriffsregel zulassen verfügen, können Sie eine am Ende der Liste mithilfe der anspruchsregelsprache wie folgt hinzufügen:  
  
    `c:[] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");`
  
11. Speichern Sie die neuen Regeln in der **Anspruchsregeln bearbeiten** Dialogfeld, klicken Sie auf **OK**. Die resultierende Liste sieht wie folgt aus.  
  
     ![Ausstellung](media/Access-Control-Policies-W2K12/clientaccess3.png)  
  
###  <a name="scenario4"></a>Szenario 4: Blockieren Sie alle externen Zugriff auf Office 365 mit Ausnahme der angegebenen Active Directory-Gruppen  
 Im folgenden Beispiel wird der Zugriff von internen Clients basierend auf IP-Adresse. Es blockiert den Zugriff von Clients, die sich außerhalb des Unternehmensnetzwerks befinden, auf denen eine externer Client-IP-Adresse verfügen, mit Ausnahme von Personen in einem angegebenen Active Directory-Group.Use die folgenden Schritte aus, um die richtigen Ausstellung von Autorisierungsregeln zum Hinzufügen der **Microsoft Office 365-Identitätsplattform** Vertrauensstellung einer vertrauenden Seite mit dem Assistenten für Anspruch:  
  
##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-for-designated-active-directory-groups"></a>Zum Erstellen von Regeln zum Blockieren von externen Zugriff auf Office 365, mit Ausnahme von festgelegten Active Directory-Gruppen  
  
1.  Von **Server-Manager**, klicken Sie auf **Tools**, klicken Sie dann auf **AD FS-Verwaltungs**.  
  
2.  In der Konsolenstruktur unter **AD Fs\vertrauensstellungen**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten**, mit der rechten Maustaste die **Microsoft Office 365-Identitätsplattform** vertrauen, und klicken Sie dann auf **Anspruchsregeln bearbeiten**.  
  
3.  In der **Anspruchsregeln bearbeiten** wählen Sie im Dialogfeld die **Ausstellungsautorisierungsregeln** Registerkarte, und klicken Sie dann auf **Regel hinzufügen** , den Anspruch Regel-Assistenten zu starten.  
  
4.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage**Option **Senden von Ansprüchen mit benutzerdefinierter Regel**, und klicken Sie dann auf **Weiter**.  
  
5.  Auf der **Regel konfigurieren** Seite unter **Name der Anspruchsregel**, geben Sie den Namen für diese Regel für Beispiel "liegt außerhalb des gewünschten Bereichs an sowie alle Ansprüche in IP-stellen Ipoutsiderange Anspruch." Klicken Sie unter **benutzerdefinierte Regel**, geben oder fügen Sie die folgende Syntax anspruchsregelsprache (ersetzen Sie den Wert für "X-ms-weitergeleitet-Client-IP-" in eine gültige IP-Ausdruck oben):  
  
      
    `c1:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] && c2:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`  

6.  Klicken Sie auf **Fertig stellen**. Stellen Sie sicher, dass in die neue Regel wird der **Ausstellungsautorisierungsregeln** Liste.  
  
7.  Weiter, in der **Anspruchsregeln bearbeiten** Dialogfeld auf die **Ausstellungsautorisierungsregeln** auf **Regel hinzufügen** um den Anspruch Regel-Assistenten erneut zu starten.  
  
8.  Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage,** wählen **Senden von Ansprüchen mit benutzerdefinierter Regel**, und klicken Sie dann auf **Weiter**.  
  
9. Auf der **Regel konfigurieren** Seite unter **Name der Anspruchsregel**, geben Sie den Anzeigenamen für diese Regel ein, z. B. "Überprüfen Gruppen-SID". Klicken Sie unter **benutzerdefinierte Regel**, geben oder fügen Sie die folgende Syntax anspruchsregelsprache (ersetzen Sie "Gruppen-SID" durch den SID der AD-Gruppe, die Sie verwenden):  
   
    `NOT EXISTS([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-32-100"]) => add(Type = "http://custom/groupsid", Value = "fail");`  

10. Klicken Sie auf **Fertig stellen**. Stellen Sie sicher, dass in die neue Regel wird der **Ausstellungsautorisierungsregeln** Liste.  
  
11. Weiter, in der **Anspruchsregeln bearbeiten** Dialogfeld auf die **Ausstellungsautorisierungsregeln** auf **Regel hinzufügen** um den Anspruch Regel-Assistenten erneut zu starten.  
  
12. Auf der **Regelvorlage auswählen** Seite unter **anspruchsregelvorlage,** wählen **Senden von Ansprüchen mit benutzerdefinierter Regel**, und klicken Sie dann auf **Weiter**.  
  
13. Auf der **Regel konfigurieren** Seite unter **Name der Anspruchsregel**, geben Sie den Anzeigenamen für diese Regel ein, z. B. "deny fehl, Benutzer mit Ipoutsiderange" true "und die Gruppen-SID". Klicken Sie unter **benutzerdefinierte Regel**, geben oder fügen Sie die folgende Syntax anspruchsregelsprache:  
   
    `c1:[Type == "https://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://custom/groupsid", Value == "fail"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`  

14. Klicken Sie auf **Fertig stellen**. Stellen Sie sicher, dass die neue Regel direkt unterhalb der vorherigen Regel angezeigt, und vor dem Regel auf den Standardwert ermöglichen den Zugriff auf alle Benutzer in der Ausstellungsautorisierungsregeln Liste (die Deny-Regel hat Vorrang, obwohl sie weiter oben in der Liste angezeigt wird).  </br></br>Wenn Sie nicht die standardmäßige Zugriffsregel zulassen verfügen, können Sie eine am Ende der Liste mithilfe der anspruchsregelsprache wie folgt hinzufügen:  
   
    `c:[] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");`  

15. Speichern Sie die neuen Regeln in der **Anspruchsregeln bearbeiten** Dialogfeld auf OK. Die resultierende Liste sieht wie folgt aus.  
  
     ![Ausstellung](media/Access-Control-Policies-W2K12/clientaccess4.png)  
  
##  <a name="buildingip"></a>Erstellen von IP-Adresse Range-Ausdrucks  
 Der X-ms-weitergeleitet-Client-Ip-Anspruch wird über einen HTTP-Header aufgefüllt, die derzeit nur von Exchange Online, das den Header ausfüllt festgelegt ist, wenn die Authentifizierungsanforderung an AD FS übergeben. Der Wert des Anspruchs kann eines der folgenden sein:  
  
> [!NOTE]
>  Exchange Online unterstützt derzeit nur für IPv4- und nicht IPV6-Adressen.  
  
-   Eine einzelne IP-Adresse: die IP-Adresse des Clients, die direkt mit Exchange Online verbunden ist  
  
> [!NOTE]
>  -   Die IP-Adresse eines Clients im Unternehmensnetzwerk wird als die externe IP-Adresse Ihres Unternehmens ausgehende Proxy oder Gateway angezeigt.  
> -   Clients, die mit dem Unternehmensnetzwerk, über ein VPN oder durch Microsoft DirectAccess (DA verbunden sind) können als interne Firmenkunden oder externe Clients, die je nach Konfiguration des VPN- oder stützt angezeigt.  
  
-   Eine oder mehrere IP-Adressen: Wenn Exchange Online kann nicht die IP-Adresse des verbundenen Clients ermittelt, wird der Wert basierend auf den Wert der X-weitergeleitet-für-Header einen nicht standardmäßigen Header, der im HTTP-basierte Anforderungen enthalten sein kann und wird von vielen Clients, Lastenausgleichsmodule und Proxys auf dem Markt unterstützt festgelegt.  
  
> [!NOTE]
>  1.  Mehrere IP-Adressen, der angibt, die Client-IP-Adresse und die Adresse für jeden Proxy, der die Anforderung übergeben werden durch ein Komma getrennt werden.  
> 2.  IP-Adressen, die im Zusammenhang mit Exchange Online-Infrastruktur werden nicht in der Liste.  
  
### <a name="regular-expressions"></a>Reguläre Ausdrücke  
 Wenn Sie einen Bereich von IP-Adressen entsprechen müssen, ist es erforderlich, erstellen Sie einen regulären Ausdruck ein, um den Vergleich durchführt. In den nächsten Schritten bieten wir Beispiele für die Vorgehensweise beim Erstellen solcher Ausdrucks entsprechend der folgenden Adressbereiche (Beachten Sie, die Sie ändern diesen Beispielen entsprechend Ihrer öffentlichen IP-Adressbereich):  
  
-   192.168.1.1 – 192.168.1.25  
  
-   10.0.0.1 – 10.0.0.14  
  
 Zuerst wird das grundlegende Muster, die eine einzelne IP-Adresse entsprechen, werden wie folgt: \b###\\.###\\.###\\.###\b  
  
 Erweitern diese, wir können entsprechen zwei verschiedene IP-Adressen mit einem Ausdruck oder wie folgt: \b###\\.###\\.###\\.###\b & #124;\b###\\.###\\.###\\.###\b  
  
 Daher wäre ein Beispiel mit nur zwei Adressen (z. B. 192.168.1.1 oder 10.0.0.1) übereinstimmen: \b192\\.168\\.1\\.1\b & #124;\b10\\.0\\.0\\.1\b  
  
 Dadurch können Sie das Verfahren, mit dem Sie eine beliebige Anzahl von Adressen eingeben können. Wo müssen eine Reihe von Adresse z. B. 192.168.1.1 – 192.168.1.25, zulässig, werden den entsprechenden vorgenommen werden Zeichen von Zeichen: \b192\\.168\\.1\\. ([1 bis 9] & #124; 1 [0-9] & #124; 2 [0 bis 5]) \b  
  
 Bitte beachten Sie Folgendes:  
  
-   Die IP-Adresse wird als Zeichenfolge und keine Zahl behandelt.  
  
-   Die Regel wird wie folgt aufgeteilt: \b192\\.168\\.1\\.  
  
-   Jeder Wert, beginnend mit 192.168.1 entspricht.  
  
-   Die folgenden entspricht die Bereiche, die für den Teil der Adresse nach dem letzten Punkt erforderlich:  
  
    -   ([1 bis 9] Übereinstimmungen Adressen mit 1 bis 9  
  
    -   & #124; 1 [0-9] entspricht Adressen mit 10-19  
  
    -   & #124;2[0-5]) Übereinstimmungen Adressen mit 20-25  
  
-   Beachten Sie, dass die Klammern richtig positioniert werden müssen, und für die keine andere Teile der IP-Adressen entsprechen.  
  
-   Mit dem 192 Block zugeordnet wird, können wir einen ähnlichen Ausdruck für die 10 Block schreiben: \b10\\.0\\.0\\. ([1 bis 9] & #124; 1 [0-4]) \b  
  
-   Und zusammenfügen, sollte der folgende Ausdruck alle Adressen für "192.168.1.1~25" und "10.0.0.1~14" entsprechen: \b192\\.168\\.1\\. ([1 bis 9] & #124; 1 [0-9] & #124; 2 [0 bis 5]) \b & #124;\b10\\.0\\.0\\. ([1 bis 9] & #124; 1 [0-4]) \b  
  
### <a name="testing-the-expression"></a>Testen den Ausdruck  
 Regex-Ausdrücke können sehr einfach, werden daher empfehlen wir dringend mithilfe eines Tools der Regex-Überprüfung. Wenn Sie eine Internetsuche nach "online Regex-Ausdrucks-Generator" tun, finden Sie einige gute online-Dienstprogramme, die Sie zum Testen Ihrer Ausdrücke mit Beispieldaten zulassen.  
  
 Wenn Sie den Ausdruck zu testen, ist es wichtig, dass Sie verstehen, was Sie erwarten können, müssen übereinstimmen. Exchange online viele IP-Adressen durch Kommas getrennt gesendet. Die oben angegebenen Ausdrücke funktioniert dies. Allerdings ist es wichtig, nachfolgend beim Testen Ihrer Regex-Ausdrücke. Beispielsweise kann eine im folgende Beispiel als Eingabe für den obigen Beispielen überprüfen verwenden:  
  
 192.168.1.1, 192.168.1.2, 192.169.1.1. 192.168.12.1, 192.168.1.10, 192.168.1.25, 192.168.1.26, 192.168.1.30, 1192.168.1.20  
  
 10.0.0.1, 10.0.0.5, 10.0.0.10, 10.0.1.0, 10.0.1.1, 110.0.0.1, 10.0.0.14, 10.0.0.15, 10.0.0.10, 10,0.0.1  
  
## <a name="claim-types"></a>Anspruchstypen  
 AD FS unter Windows Server 2012 R2 bietet Anforderung Kontextinformationen mithilfe der folgenden Anspruchstypen:  
  
### <a name="x-ms-forwarded-client-ip"></a>X-MS-weitergeleitet-Client-IP  
 Typ des Anspruchs: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`  
  
 Diesen Anspruch von AD FS stellt einen "beste Versuch" ermitteln die IP-Adresse des Benutzers (z.B. Outlook-Client), der die Anforderung dar. Diesem Anspruch kann mehrere IP-Adressen, einschließlich der Adresse des jeden Proxy, der die Anforderung weitergeleitet enthalten.  Diesen Anspruch wird von einer HTTP aufgefüllt. Der Wert des Anspruchs kann eine der folgenden sein:  
  
-   Eine einzelne IP-Adresse - IP-Adresse des Clients, die direkt mit Exchange Online verbunden ist  
  
> [!NOTE]
>  Die IP-Adresse eines Clients im Unternehmensnetzwerk wird als die externe IP-Adresse Ihres Unternehmens ausgehende Proxy oder Gateway angezeigt.  
  
-   Eine oder mehrere IP-Adressen  
  
    -   Wenn Sie Exchange Online die IP-Adresse des verbundenen Clients nicht ermitteln kann, wird es legen Sie den Wert basierend auf den Wert der X-weitergeleitet-für-Header ein nicht standardmäßiger Header, der HTTP-basierten enthalten sein kann anfordert und von vielen Clients, Lastenausgleichsmodule und Proxys auf dem Markt unterstützt wird.  
  
    -   Mehrere IP-Adressen, der angibt, die Client-IP-Adresse und die Adresse für jeden Proxy, der die Anforderung übergeben werden durch ein Komma getrennt werden.  
  
> [!NOTE]
>  IP-Adressen, die im Zusammenhang mit Exchange Online-Infrastruktur werden nicht in der Liste vorhanden sein.  
  
> [!WARNING]
>  Exchange Online unterstützt derzeit nur-IPv4-Adressen. IPV6-Adressen wird nicht unterstützt.  
  
### <a name="x-ms-client-application"></a>X-MS-Client-Anwendung  
 Typ des Anspruchs: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`  
  
 Diesen Anspruch von AD FS stellt das Protokoll verwendet wird dem Endbenutzer, die lose entspricht der Anwendung verwendet wird.  Diesen Anspruch über einen HTTP-Header, die aktuell aufgefüllt wird nur festlegen, indem Sie Exchange Online, mit dem die Kopfzeile gefüllt, wenn Sie die Authentifizierungsanforderung an AD FS übergeben. Abhängig von der Anwendung wird der Wert dieses Anspruchs eines der folgenden sein:  
  
-   Im Fall von Geräten, die Exchange ActiveSync verwenden, ist der Wert Microsoft.Exchange.ActiveSync.  
  
-   Verwendung von Microsoft Outlook-Client möglicherweise in einem der folgenden Werte:  
  
    -   Microsoft.Exchange.Autodiscover  
  
    -   Microsoft.Exchange.OfflineAddressBook  
  
    -   Microsoft.Exchange.RPCMicrosoft.Exchange.WebServices  
  
    -   Microsoft.Exchange.RPCMicrosoft.Exchange.WebServices  
  
-   Andere mögliche Werte für diesen Header sind folgende:  
  
    -   Microsoft.Exchange.PowerShell  
  
    -   Microsoft.Exchange.SMTP  
  
    -   Microsoft.Exchange.Pop  
  
    -   Microsoft.Exchange.Imap  
  
### <a name="x-ms-client-user-agent"></a>X-MS-Client-Benutzer-Agent  
 Typ des Anspruchs: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`  
  
 Diesen Anspruch von AD FS bietet eine Zeichenfolge, um den Gerätetyp darstellen, den der Client verwendet, um den Dienst zuzugreifen. Dies kann verwendet werden, wenn Kunden, um den Zugriff für bestimmte Geräte (z.B. bestimmte Arten von Smartphones) zu verhindern möchten.  Beispielwerte für diesen Anspruch enthalten (jedoch nicht beschränkt auf) die folgenden Werte.  
  
 Die im folgenden sind Beispiele für was der X-ms-Benutzer-Agent-Wert für einen Client enthalten kann, deren X-ms-Client-Anwendung ist "Microsoft.Exchange.ActiveSync"  
  
-   Vortex/1.0  
  
-   Apple-iPad1C1/812.1  
  
-   Apple-iPhone3C1/811.2  
  
-   Apple-iPhone/704.11  
  
-   Moto-DROID2/4.5.1  
  
-   SAMSUNGSPHD700/100.202  
  
-   Android/0.3  
  
 Es ist auch möglich, dass dieser Wert leer ist.  
  
### <a name="x-ms-proxy"></a>X-MS-Proxy  
 Typ des Anspruchs: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`  
  
 Diesen Anspruch von AD FS weist darauf hin, dass die Anforderung durch den Web Application Proxy bestanden hat.  Diesen Anspruch wird durch die Web Application Proxy aufgefüllt, das die Kopfzeile ausfüllt, wenn die Authentifizierungsanforderung an den Back-End-Verbunddienst übergeben. AD FS konvertiert es dann in einen Anspruch.  
  
 Der Wert des Anspruchs ist der DNS-Name des Web Application Proxy, der die Anforderung übergeben.  
  
### <a name="insidecorporatenetwork"></a>InsideCorporateNetwork  
 Typ des Anspruchs: `https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`  
  
 Ähnlich wie die oben genannten X-ms-Proxy Anspruchstyp, dieser Anspruchstyp gibt an, ob die Anforderung über den webanwendungsproxy übergeben wurde. Im Gegensatz zu X-ms-Proxy ist Insidecorporatenetwork ein boolescher Wert mit "true" angezeigt, die eine Anforderung direkt an den Verbunddienst von innerhalb des Unternehmensnetzwerks.  
  
### <a name="x-ms-endpoint-absolute-path-active-vs-passive"></a>X-MS-Endpunkt-Absolute-Pfad (aktiv oder passiv)  
 Typ des Anspruchs: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`  
  
 Dieser Typ des Anspruchs kann zur Bestimmung von Anfragen von "aktiv" (rich)-Clients im Vergleich zu "passiven" (Web-Browser-basiert)-Clients verwendet werden. Dadurch können externe Anforderungen von browserbasierten Anwendungen wie Outlook Web Access, SharePoint Online oder Office365-Portal zugelassen werden, während die Anfragen von rich-Clients wie Microsoft Outlook blockiert werden.  
  
 Der Wert des Anspruchs ist der Name des AD FS-Diensts, die die Anforderung empfangen.  
  
## <a name="see-also"></a>Siehe auch  
 [AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md)
