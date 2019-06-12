---
ms.assetid: 5728847d-dcef-4694-9080-d63bfb1fe24b
title: Zugriffssteuerungsrichtlinien in AD FS
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/05/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: cc3de72aa993546151b103d6eeacd160f81a4270
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444385"
---
# <a name="access-control-policies-in-windows-server-2012-r2-and-windows-server-2012-ad-fs"></a>Richtlinien für die Zugriffssteuerung in Windows Server 2012 R2 und WindowsServer 2012 AD FS


Stellen Sie die Richtlinien, die in diesem Artikel beschriebenen verwendet zwei Arten von Ansprüchen  

1.  Behauptet, dass AD FS auf Basis der Informationen erstellt, der AD FS und Web Application Proxy können Sie überprüfen und zu überprüfen, wie z. B. die IP-Adresse des Clients, die direkte Verbindung mit AD FS oder den drahtlosen Zugriffspunkt.  

2.  AD FS-Ansprüche erstellt auf Basis der Informationen, die vom Client als HTTP-Header mit AD FS weitergeleitet  

>**Wichtig**: Die Richtlinien, wie im folgenden dokumentiert blockiert Windows 10-Domänenbeitritt und melden Sie sich bei Szenarien, die Zugriff auf die folgenden zusätzlichen Endpunkte erfordern.

Erforderlich für Windows 10-Domäne beitreten, und melden Sie AD FS-Endpunkte
- [federation service name]/adfs/services/trust/2005/windowstransport
- [federation service name]/adfs/services/trust/13/windowstransport
- [federation service name]/adfs/services/trust/2005/usernamemixed
- [federation service name]/adfs/services/trust/13/usernamemixed 
- [federation service name]/adfs/services/trust/2005/certificatemixed
- [federation service name]/adfs/services/trust/13/certificatemixed

Um beheben, aktualisieren Sie alle Richtlinien, die verweigern basierend auf der Behauptung Endpunkt, um die Ausnahme für die oben genannten Endpunkte zu ermöglichen.

Beispielsweise der folgenden Regel:

`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "/adfs/ls/"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`  

würde aktualisiert werden:

`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "(/adfs/ls/)|(/adfs/services/trust/2005/windowstransport)|(/adfs/services/trust/13/windowstransport)|(/adfs/services/trust/2005/usernamemixed)|(/adfs/services/trust/13/usernamemixed)|(/adfs/services/trust/2005/certificatemixed)|(/adfs/services/trust/13/certificatemixed)"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`



> [!NOTE]
>  Ansprüche aus dieser Kategorie sollte nur verwendet werden, um Business-Richtlinien zu implementieren und nicht als von Sicherheitsrichtlinien für den Zugriff auf Ihr Netzwerk zu schützen.  Es ist möglich, dass nicht autorisierte Clients zum Senden von Headern mit falscher Informationen als eine Möglichkeit für den Zugriff.  

In diesem Artikel beschriebenen Richtlinien sollten immer mit einer anderen Authentifizierungsmethode verwendet werden, z. B. Benutzername und Kennwort oder Multi-Factor Authentication verwendet werden.  

## <a name="client-access-policies-scenarios"></a>Client-Zugriffsszenarien für Richtlinien  

|**Szenario**|**Beschreibung**| 
| --- | --- | 
|Szenario 1: Blockieren des gesamten externen Zugriff auf Office 365|Office 365-Zugriff von allen Clients im internen Unternehmensnetzwerk zulässig ist, aber basierend auf der IP-Adresse des externen Clients die Anforderungen von externen Clients abgelehnt.|  
|Szenario 2: Blockieren des gesamten externen Zugriff auf Office 365 mit Ausnahme von Exchange ActiveSync|Office 365-Zugriff ist zulässig, von allen Clients im internen Unternehmensnetzwerk sowie alle externen Clientgeräte, z. B. Smartphones, die von Exchange ActiveSync verwenden. Alle anderen externen Clients, z. B. mithilfe von Outlook, werden blockiert.|  
|Szenario 3: Blockieren des gesamten externen Zugriff auf Office 365 außer durch browserbasierte Anwendungen|Blöcke externen Zugriff auf Office 365, mit Ausnahme der passive (browserbasiert)-Anwendungen wie Outlook Web Access oder SharePoint Online.|  
|Szenario 4: Blockieren des gesamten externen Zugriff auf Office 365 mit Ausnahme der angegebenen Active Directory-Gruppen|Dieses Szenario wird für das Testen und Überprüfen der Bereitstellung von Access-Richtlinie verwendet. Externen Zugriff auf Office 365 wird nur für Mitglieder der Gruppe für eine oder mehrere Active Directory blockiert. Sie können auch verwendet werden, um externen Zugriff nur für Mitglieder einer Gruppe bereitstellen.|  

## <a name="enabling-client-access-policy"></a>Aktivieren die Clientzugriffsrichtlinie  
 Um Clientzugriffsrichtlinie in AD FS unter Windows Server 2012 R2 zu aktivieren, müssen Sie die Microsoft Office 365 Identity Platform, die Vertrauensstellung einer vertrauenden Seite aktualisieren. Wählen Sie eine der in den Beispielszenarien unten, um die Anspruchsregeln konfigurieren, auf die **Microsoft Office 365 Identity Platform** Vertrauensstellung der vertrauenden, dass die Anforderungen Ihrer Organisation am besten erfüllt.  

###  <a name="scenario1"></a> Szenario 1: Blockieren des gesamten externen Zugriff auf Office 365  
 Diese Szenarios Client für den Zugriff ermöglicht Zugriff auf alle internen Clients und blockiert alle externen Clients, die basierend auf der IP-Adresse des externen Clients. Sie können die folgenden Verfahren verwenden, die richtigen Regeln für Ausstellungsautorisierung Office 365 für Ihr ausgewähltes Szenario Vertrauensstellung einer vertrauenden Seite hinzu.  

##### <a name="to-create-rules-to-block-all-external-access-to-office-365"></a>Zum Erstellen von Regeln zum Blockieren des gesamten externen Zugriff auf Office 365  

1.  Von **Server-Manager**, klicken Sie auf **Tools**, klicken Sie dann auf **AD FS-Verwaltung**.  

2.  In der Konsolenstruktur unter **AD Fs\vertrauensstellungen**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten**, mit der rechten Maustaste die **Microsoft Office 365 Identity Platform** vertrauen, und klicken Sie dann auf **Anspruchsregeln bearbeiten**.  

3.  In der **Edit Claim Rules** wählen Sie im Dialogfeld die **Ausstellungsautorisierungsregeln** Registerkarte, und klicken Sie dann auf **Regel hinzufügen** um den Assistenten zum Starten.  

4.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **Ansprüche mit benutzerdefinierter Regel senden**, und klicken Sie dann auf **Weiter**.  

5.  Auf der **Regel konfigurieren** Seite **anspruchsregelname**, Typ, der der Anzeigenamen für diese Regel ein, z. B. "Es ist IP-Anspruch außerhalb des gewünschten Bereichs, verweigern". Klicken Sie unter **benutzerdefinierte Regel**geben oder fügen Sie die folgende Anspruchsregel-Sprachsyntax (ersetzen Sie den Wert oben für "X-ms-forwarded-Client-Ip" mit einem gültigen IP-Ausdruck):  
`c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");` </br>
6.  Klicken Sie auf **Fertig stellen**. Stellen Sie sicher, dass die neue Regel wird, in der Liste von Ausstellungsautorisierungsregeln vor auf den Standardwert angezeigt **ermöglichen den Zugriff auf alle Benutzer** Regel (Deny-Regel Vorrang, obwohl er weiter oben in der Liste angezeigt wird).  Wenn Sie nicht die Standardeinstellung Zugriffsregel zulassen verfügen, können Sie eine am Ende der Liste mithilfe der anspruchsregelsprache wie folgt hinzufügen:  </br>

    `c:[] => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true"); ` 

7.  Speichern Sie die neuen Regeln, in der **Edit Claim Rules** Dialogfeld klicken Sie auf **OK**. Die resultierende Liste sollte wie folgt aussehen.  

     ![Ausstellungsautorisierungsregeln](media/Access-Control-Policies-W2K12/clientaccess1.png "ADFS_Client_Access_1")  

###  <a name="scenario2"></a> Szenario 2: Blockieren des gesamten externen Zugriff auf Office 365 mit Ausnahme von Exchange ActiveSync  
 Im folgende Beispiel ermöglicht den Zugriff auf alle Office 365-Anwendungen, einschließlich von internen Clients, einschließlich Outlook Exchange Online. Blockiert den Zugriff von Clients, die sich außerhalb des Unternehmensnetzwerks befinden, wie durch die Client IP-Adresse, mit Ausnahme von Exchange ActiveSync-Clients wie z. B. Smartphones.  

##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-exchange-activesync"></a>Zum Erstellen von Regeln zum Blockieren des gesamten externen Zugriff auf Office 365 mit Ausnahme von Exchange ActiveSync  

1.  Von **Server-Manager**, klicken Sie auf **Tools**, klicken Sie dann auf **AD FS-Verwaltung**.  

2.  In der Konsolenstruktur unter **AD Fs\vertrauensstellungen**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten**, mit der rechten Maustaste die **Microsoft Office 365 Identity Platform** vertrauen, und klicken Sie dann auf **Anspruchsregeln bearbeiten**.  

3.  In der **Edit Claim Rules** wählen Sie im Dialogfeld die **Ausstellungsautorisierungsregeln** Registerkarte, und klicken Sie dann auf **Regel hinzufügen** um den Assistenten zum Starten.  

4.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **Ansprüche mit benutzerdefinierter Regel senden**, und klicken Sie dann auf **Weiter**.  

5.  Auf der **Regel konfigurieren** Seite **anspruchsregelname**, geben Sie den Anzeigenamen für diese Regel aus, für das Beispiel "Es ist IP-Anspruch außerhalb des gewünschten Bereichs, stellen Ipoutsiderange Anspruch". Klicken Sie unter **benutzerdefinierte Regel**geben oder fügen Sie die folgende Anspruchsregel-Sprachsyntax (ersetzen Sie den Wert oben für "X-ms-forwarded-Client-Ip" mit einem gültigen IP-Ausdruck):  

    `c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`  

6.  Klicken Sie auf **Fertig stellen**. Stellen Sie sicher, dass die neue Regel wird, in angezeigt der **Ausstellungsautorisierungsregeln** Liste.  

7.  Dann in der **Edit Claim Rules** Dialogfelds die **Ausstellungsautorisierungsregeln** auf **Regel hinzufügen** , den Assistenten zum erneut zu starten.  

8.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **Ansprüche mit benutzerdefinierter Regel senden**, und klicken Sie dann auf **Weiter**.  

9. Auf der **Regel konfigurieren** Seite **anspruchsregelname**, Typ, der der Anzeigenamen für diese Regel ein, z. B. "Wenn eine IP-Adresse außerhalb des gewünschten Bereichs und es wird ein Anspruch nicht von EAS X-ms-Client-Anwendung verweigern ". Klicken Sie unter **benutzerdefinierte Regel**geben oder fügen Sie die folgende Anspruchsregel-Sprachsyntax:  


~~~
`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value != "Microsoft.Exchange.ActiveSync"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`  
~~~

10. Klicken Sie auf **Fertig stellen**. Stellen Sie sicher, dass die neue Regel wird, in angezeigt der **Ausstellungsautorisierungsregeln** Liste.  

11. Dann in der **Edit Claim Rules** Dialogfelds die **Ausstellungsautorisierungsregeln** auf **Regel hinzufügen** , den Assistenten zum erneut zu starten.  

12. Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage,** wählen **Ansprüche mit benutzerdefinierter Regel senden**, und klicken Sie dann auf **Weiter**.  

13. Auf der **Regel konfigurieren** Seite **anspruchsregelname**, geben Sie den Anzeigenamen für diese Regel ein, z. B. "Überprüfen Sie, ob anwendungsanspruch vorhanden ist". Klicken Sie unter **benutzerdefinierte Regel**geben oder fügen Sie die folgende Anspruchsregel-Sprachsyntax:  

   ```  
   NOT EXISTS([Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application"]) => add(Type = "http://custom/xmsapplication", Value = "fail");  
   ```  

14. Klicken Sie auf **Fertig stellen**. Stellen Sie sicher, dass die neue Regel wird, in angezeigt der **Ausstellungsautorisierungsregeln** Liste.  

15. Dann in der **Edit Claim Rules** Dialogfelds die **Ausstellungsautorisierungsregeln** auf **Regel hinzufügen** , den Assistenten zum erneut zu starten.  

16. Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage,** wählen **Ansprüche mit benutzerdefinierter Regel senden**, und klicken Sie dann auf **Weiter**.  

17. Auf der **Regel konfigurieren** Seite **anspruchsregelname**, geben Sie den Anzeigenamen für diese Regel ein, z. B. "Verweigern Benutzer mit Ipoutsiderange" true "und nicht". Klicken Sie unter **benutzerdefinierte Regel**geben oder fügen Sie die folgende Anspruchsregel-Sprachsyntax:  

`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://custom/xmsapplication", Value == "fail"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`</br>  
18. Klicken Sie auf **Fertig stellen**. Stellen Sie sicher, dass die neue Regel unmittelbar unterhalb der vorherigen Regel angezeigt wird, und vor dem Zugriff auf alle Benutzer standardmäßig-Regel in der Regeln für Ausstellungsautorisierung-Liste (die Deny-Regel hat Vorrang, obwohl er weiter oben in der Liste angezeigt wird).  </br>Wenn Sie nicht die Standardeinstellung Zugriffsregel zulassen verfügen, können Sie eine am Ende der Liste mithilfe der anspruchsregelsprache wie folgt hinzufügen:</br></br>      `c:[] => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");`</br></br>
19. Speichern Sie die neuen Regeln, in der **Edit Claim Rules** Dialogfeld auf OK. Die resultierende Liste sollte wie folgt aussehen.  

    ![Ausstellungsautorisierungsregeln](media/Access-Control-Policies-W2K12/clientaccess2.png )  

###  <a name="scenario3"></a> Szenario 3: Blockieren des gesamten externen Zugriff auf Office 365 außer durch browserbasierte Anwendungen  

##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-browser-based-applications"></a>Zum Erstellen von Regeln zum Blockieren des gesamten externen Zugriff auf Office 365 außer durch browserbasierte Anwendungen  

1.  Von **Server-Manager**, klicken Sie auf **Tools**, klicken Sie dann auf **AD FS-Verwaltung**.  

2.  In der Konsolenstruktur unter **AD Fs\vertrauensstellungen**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten**, mit der rechten Maustaste die **Microsoft Office 365 Identity Platform** vertrauen, und klicken Sie dann auf **Anspruchsregeln bearbeiten**.  

3.  In der **Edit Claim Rules** wählen Sie im Dialogfeld die **Ausstellungsautorisierungsregeln** Registerkarte, und klicken Sie dann auf **Regel hinzufügen** um den Assistenten zum Starten.  

4.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **Ansprüche mit benutzerdefinierter Regel senden**, und klicken Sie dann auf **Weiter**.  

5.  Auf der **Regel konfigurieren** Seite **anspruchsregelname**, geben Sie den Anzeigenamen für diese Regel aus, für das Beispiel "Es ist IP-Anspruch außerhalb des gewünschten Bereichs, stellen Ipoutsiderange Anspruch". Klicken Sie unter **benutzerdefinierte Regel**geben oder fügen Sie die folgende Anspruchsregel-Sprachsyntax (ersetzen Sie den Wert oben für "X-ms-forwarded-Client-Ip" mit einem gültigen IP-Ausdruck):  </br>
`c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`   
6.  Klicken Sie auf **Fertig stellen**. Stellen Sie sicher, dass die neue Regel wird, in angezeigt der **Ausstellungsautorisierungsregeln** Liste.  

7.  Dann in der **Edit Claim Rules** Dialogfelds die **Ausstellungsautorisierungsregeln** auf **Regel hinzufügen** , den Assistenten zum erneut zu starten.  

8.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage,** wählen **Ansprüche mit benutzerdefinierter Regel senden**, und klicken Sie dann auf **Weiter**.  

9. Auf der **Regel konfigurieren** Seite **anspruchsregelname**, Typ, der der Anzeigenamen für diese Regel ein, z. B. "Wenn es eine IP-Adresse außerhalb des gewünschten Bereichs und der Endpunkt ist nicht/Adfs/ls, verweigern". Klicken Sie unter **benutzerdefinierte Regel**geben oder fügen Sie die folgende Anspruchsregel-Sprachsyntax:  


~~~
`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "/adfs/ls/"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`  
~~~

10. Klicken Sie auf **Fertig stellen**. Stellen Sie sicher, dass die neue Regel wird, in der Liste von Ausstellungsautorisierungsregeln vor auf den Standardwert angezeigt **ermöglichen den Zugriff auf alle Benutzer** Regel (Deny-Regel Vorrang, obwohl er weiter oben in der Liste angezeigt wird).  </br></br> Wenn Sie nicht die Standardeinstellung Zugriffsregel zulassen verfügen, können Sie eine am Ende der Liste mithilfe der anspruchsregelsprache wie folgt hinzufügen:  

   `c:[] => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");`

11. Speichern Sie die neuen Regeln, in der **Edit Claim Rules** Dialogfeld klicken Sie auf **OK**. Die resultierende Liste sollte wie folgt aussehen.  

    ![Ausstellung](media/Access-Control-Policies-W2K12/clientaccess3.png)  

###  <a name="scenario4"></a> Szenario 4: Blockieren des gesamten externen Zugriff auf Office 365 mit Ausnahme der angegebenen Active Directory-Gruppen  
 Im folgenden Beispiel wird der Zugriff von internen Clients basierend auf IP-Adresse. Blockiert den Zugriff von Clients, die sich außerhalb des Unternehmensnetzwerks befinden, die eine externen Client-IP-Adresse verfügen, mit Ausnahme der Personen in einer angegebenen Active Directory-Group.Use die folgenden Schritte aus, um die richtige Ausstellungsautorisierung hinzuzufügen, die Sie die Regeln **Microsoft Office 365 Identity Platform** -Vertrauensstellung der vertrauenden mit dem Assistenten zum:  

##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-for-designated-active-directory-groups"></a>Zum Erstellen von Regeln zum Blockieren des gesamten externen Zugriff auf Office 365, mit Ausnahme von angegebenen Active Directory-Gruppen  

1.  Von **Server-Manager**, klicken Sie auf **Tools**, klicken Sie dann auf **AD FS-Verwaltung**.  

2.  In der Konsolenstruktur unter **AD Fs\vertrauensstellungen**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten**, mit der rechten Maustaste die **Microsoft Office 365 Identity Platform** vertrauen, und klicken Sie dann auf **Anspruchsregeln bearbeiten**.  

3.  In der **Edit Claim Rules** wählen Sie im Dialogfeld die **Ausstellungsautorisierungsregeln** Registerkarte, und klicken Sie dann auf **Regel hinzufügen** um den Assistenten zum Starten.  

4.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **Ansprüche mit benutzerdefinierter Regel senden**, und klicken Sie dann auf **Weiter**.  

5.  Auf der **Regel konfigurieren** Seite **anspruchsregelname**, geben Sie den Anzeigenamen für diese Regel aus, für das Beispiel "Es ist IP-Anspruch außerhalb des gewünschten Bereichs, stellen Ipoutsiderange Anspruch." Klicken Sie unter **benutzerdefinierte Regel**geben oder fügen Sie die folgende Anspruchsregel-Sprachsyntax (ersetzen Sie den Wert oben für "X-ms-forwarded-Client-Ip" mit einem gültigen IP-Ausdruck):  


~~~
`c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] && c2:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`  
~~~

6. Klicken Sie auf **Fertig stellen**. Stellen Sie sicher, dass die neue Regel wird, in angezeigt der **Ausstellungsautorisierungsregeln** Liste.  

7. Dann in der **Edit Claim Rules** Dialogfelds die **Ausstellungsautorisierungsregeln** auf **Regel hinzufügen** , den Assistenten zum erneut zu starten.  

8. Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage,** wählen **Ansprüche mit benutzerdefinierter Regel senden**, und klicken Sie dann auf **Weiter**.  

9. Auf der **Regel konfigurieren** Seite **anspruchsregelname**, geben Sie den Anzeigenamen für diese Regel ein, z. B. "Überprüfen Gruppen-SID". Klicken Sie unter **benutzerdefinierte Regel**geben oder fügen Sie die folgende Anspruchsregel-Sprachsyntax (ersetzen Sie "Gruppen-SID" mit der tatsächlichen SID der AD-Gruppe, die Sie verwenden):  

    `NOT EXISTS([Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-32-100"]) => add(Type = "http://custom/groupsid", Value = "fail");`  

10. Klicken Sie auf **Fertig stellen**. Stellen Sie sicher, dass die neue Regel wird, in angezeigt der **Ausstellungsautorisierungsregeln** Liste.  

11. Dann in der **Edit Claim Rules** Dialogfelds die **Ausstellungsautorisierungsregeln** auf **Regel hinzufügen** , den Assistenten zum erneut zu starten.  

12. Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage,** wählen **Ansprüche mit benutzerdefinierter Regel senden**, und klicken Sie dann auf **Weiter**.  

13. Auf der **Regel konfigurieren** Seite **anspruchsregelname**, geben Sie den Anzeigenamen für diese Regel ein, z. B. "Verweigern Benutzer mit Ipoutsiderange" true "und die Gruppen-SID nicht". Klicken Sie unter **benutzerdefinierte Regel**geben oder fügen Sie die folgende Anspruchsregel-Sprachsyntax:  

   `c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://custom/groupsid", Value == "fail"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`  

14. Klicken Sie auf **Fertig stellen**. Stellen Sie sicher, dass die neue Regel unmittelbar unterhalb der vorherigen Regel angezeigt wird, und vor dem Zugriff auf alle Benutzer standardmäßig-Regel in der Regeln für Ausstellungsautorisierung-Liste (die Deny-Regel hat Vorrang, obwohl er weiter oben in der Liste angezeigt wird).  </br></br>Wenn Sie nicht die Standardeinstellung Zugriffsregel zulassen verfügen, können Sie eine am Ende der Liste mithilfe der anspruchsregelsprache wie folgt hinzufügen:  

   `c:[] => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");`  

15. Speichern Sie die neuen Regeln, in der **Edit Claim Rules** Dialogfeld auf OK. Die resultierende Liste sollte wie folgt aussehen.  

     ![Ausstellung](media/Access-Control-Policies-W2K12/clientaccess4.png)  

##  <a name="buildingip"></a> Erstellen die IP-Adresse-Range-Ausdruck  
 Der X-ms-forwarded-Client-Ip-Anspruch wird von einem HTTP-Header aufgefüllt, die derzeit nur von Exchange Online, die den Header aufgefüllt wird festgelegt ist, wenn die Authentifizierungsanforderung an AD FS übergeben. Der Wert des Anspruchs kann es sich um eine der folgenden sein:  

> [!NOTE]
>  Exchange Online unterstützt derzeit nur für IPV4- und nicht auf IPV6-Adressen.  

-   Eine einzelne IP-Adresse: Die IP-Adresse des Clients, die direkt mit Exchange Online verbunden ist  

> [!NOTE]
> - Die IP-Adresse eines Clients im Unternehmensnetzwerk wird als der externe IP-Adresse des Proxys für ausgehenden Datenverkehr der Organisation oder Gateways angezeigt.  
>   -   Clients, die mit dem Unternehmensnetzwerk, indem Sie ein VPN oder von Microsoft DirectAccess (DA verbunden sind) möglicherweise als internen Unternehmenskunden oder als externe Clients, die je nach Konfiguration des VPN-Verbindung oder da auszulagern.  

-   Eine oder mehrere IP-Adressen: Wenn Sie Exchange Online die IP-Adresse der verbindende Client nicht ermitteln kann, wird es legen Sie den Wert basierend auf den Wert der X-forwarded-for-Header, eine nicht standardmäßige Headerdateien, die in der HTTP-basierten Anforderungen enthalten sein kann und wird von vielen Clients, Load balancer unterstützt, und -Proxys auf dem Markt.  

> [!NOTE]
> 1. Mehrere IP-Adressen, der angibt, die Client-IP-Adresse und die Adresse für jeden Proxy, der die Anforderung zu übergeben, werden durch ein Komma getrennt werden.  
>    2. IP-Adressen, die im Zusammenhang mit Exchange Online-Infrastruktur werden nicht in der Liste.  

### <a name="regular-expressions"></a>Reguläre Ausdrücke  
 Wenn Sie einen Bereich von IP-Adressen übereinstimmen müssen, ist es notwendig, einen regulären Ausdruck zum Ausführen des Vergleichs zu erstellen. In den nächsten Schritten bieten wir Beispiele dafür, wie ein solcher Ausdruck entsprechend die folgenden Adressbereiche (Beachten Sie, dass Sie werden so ändern Sie diesen Beispielen entsprechend Ihrer öffentlichen IP-Adressbereich) erstellen:  

- 192.168.1.1 – 192.168.1.25  

- 10.0.0.1 – 10.0.0.14  

  Erstens ist das grundlegende Muster, die eine einzelne IP-Adresse übereinstimmen, wird wie folgt: \b###\\. ###\\. ###\\. ### \b  

  Erweitern diese aus, wir können entsprechen zwei verschiedene IP-Adressen mit einem OR-Ausdruck wie folgt: \b###\\. ###\\. ###\\. ### \b&#124;\b###\\. ###\\. ###\\. ### \b  

  Natürlich wäre ein Beispiel, das nur zwei Adressen (z.B. 192.168.1.1 oder 10.0.0.1) übereinstimmen: \b192\\.168\\.1\\. 1\b&#124;\b10\\.0\\.0\\. 1\b  

  Dadurch können Sie das Verfahren, mit dem Sie eine beliebige Anzahl von Adressen eingeben können. Wo müssen ein Bereich von Adresse, das z. B. 192.168.1.1 – 192.168.1.25, zugelassen, werden den entsprechenden vorgenommen werden Zeichen durch Zeichen: \b192\\.168\\.1\\. () [1-9] &#124;1 [0-9]&#124;2 [0-5]) \b  

  Bitte beachten Sie Folgendes:  

- Die IP-Adresse wird als Zeichenfolge und kein Zahl behandelt.  

- Die Regel wird wie folgt unterteilt: \b192\\.168\\.1\\.  

- Dies entspricht jeder Wert beginnt mit 192.168.1 aufweisen.  

- Der folgenden entspricht die Bereiche, die für den Teil der Adresse nach dem letzten Punkt erforderlich:  

  -   ([1-9] Übereinstimmungen Adressen mit 1 bis 9  

  -   &#124;1 [0-9] entspricht der Adressen mit den 10-19  

  -   &#124;2[0-5]) Übereinstimmungen Adressen mit den 20-25  

- Beachten Sie, dass die Klammern korrekt positioniert werden müssen, damit Sie starten nicht übereinstimmende andere Bereiche von IP-Adressen.  

- Mit dem 192 Block abgeglichen, Schreiben wir einen ähnlichen Ausdruck für den 10-Block: \b10\\.0\\.0\\. () [1-9] &#124;1 [0-4]) \b  

- Und platzieren sie zusammen, sollte der folgende Ausdruck alle Adressen für "192.168.1.1~25" und "10.0.0.1~14" übereinstimmen: \b192\\.168\\.1\\. () [1-9] &#124;1 [0-9]&#124;2 [0-5]) \b&#124;\b10\\.0\\.0\\. () [1-9] &#124;1 [0-4]) \b  

### <a name="testing-the-expression"></a>Testen den Ausdruck  
 Regex-Ausdrücke können recht schwierig werden, deshalb wird ausdrücklich empfohlen, mithilfe eines Tools der Regex-Überprüfung. Wenn Sie eine Internetsuche nach "online Regex-Ausdrucks-Generator" tun, finden Sie mehrere gute online-Hilfsprogramme, die Sie Ihren Ausdrücken anhand von Beispieldaten ausprobieren können.  

 Wenn Sie den Ausdruck zu testen, ist es wichtig, dass Sie verstehen, was Sie erwarten können, müssen übereinstimmen. Das Exchange online-System senden möglicherweise viele IP-Adressen, getrennt durch Kommas. Die oben aufgeführten Ausdrücke funktionieren für diese. Allerdings ist es wichtig, zu kümmern beim Testen Ihrer Regex-Ausdrücke. Beispielsweise kann eine im folgende Beispiel mit der Eingabe, um zu überprüfen, ob die Beispiele oben verwenden:  

 192.168.1.1, 192.168.1.2, 192.169.1.1. 192.168.12.1, 192.168.1.10, 192.168.1.25, 192.168.1.26, 192.168.1.30, 1192.168.1.20  

 10.0.0.1, 10.0.0.5, 10.0.0.10, 10.0.1.0, 10.0.1.1, 110.0.0.1, 10.0.0.14, 10.0.0.15, 10.0.0.10, 10,0.0.1  

## <a name="claim-types"></a>Anspruchstypen  
 AD FS unter Windows Server 2012 R2 bietet anforderungskontextinformationen verwenden die folgenden Anspruchstypen:  

### <a name="x-ms-forwarded-client-ip"></a>X-MS-Forwarded-Client-IP  
 Anspruchstyp: `http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`  

 Dieser AD FS-Anspruch stellt eine "versucht," Feststellung der IP-Adresse des Benutzers (z. B. der Outlook-Client) und die Anforderung dar. Dieser Anspruch kann mehrere IP-Adressen, einschließlich der Adresse von jedem Proxy, der die Anforderung weitergeleitet enthalten.  Dieser Anspruch wird von einem HTTP aufgefüllt. Der Wert des Anspruchs kann es sich um eine der folgenden sein:  

-   Eine einzelne IP-Adresse – die IP-Adresse des Clients, die direkt mit Exchange Online verbunden ist  

> [!NOTE]
>  Die IP-Adresse eines Clients im Unternehmensnetzwerk wird als der externe IP-Adresse des Proxys für ausgehenden Datenverkehr der Organisation oder Gateways angezeigt.  

-   Eine oder mehrere IP-Adressen  

    -   Wenn Exchange Online die IP-Adresse der verbindende Client nicht ermitteln kann, wird der Wert, der basierend auf dem Wert der X-forwarded-for-Header, eine nicht standardmäßige Headerdateien, die in der HTTP-basierten aufgenommen werden kann, fordert und wird von vielen Clients, Load balancer unterstützt festgelegt und Proxys auf dem Markt.  

    -   Mehrere IP-Adressen, der angibt, die Client-IP-Adresse und die Adresse für jeden Proxy, der die Anforderung zu übergeben, werden durch ein Komma getrennt werden.  

> [!NOTE]
>  IP-Adressen, die im Zusammenhang mit Exchange Online-Infrastruktur werden nicht in der Liste vorhanden.  

> [!WARNING]
>  Exchange Online unterstützt derzeit nur IPV4-Adressen; IPV6-Adressen werden nicht unterstützt.  

### <a name="x-ms-client-application"></a>X-MS-Client-Application  
 Anspruchstyp: `http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`  

 Dieser AD FS-Anspruch darstellt, das von der End-Client, der verwendeten Anwendung lose entspricht verwendete Protokoll.  Dieser Anspruch wird aufgefüllt, von einem HTTP-Header, die derzeit wird nur von Exchange Online, die den Header aufgefüllt wird, wenn die Authentifizierungsanforderung an AD FS übergeben festgelegt. Abhängig von der Anwendung wird der Wert dieses Anspruchs einen der folgenden sein:  

-   Bei Geräten, die Exchange Active Sync verwenden, ist der Wert Microsoft.Exchange.ActiveSync.  

-   Verwendung von Microsoft Outlook-Clients möglicherweise in einem der folgenden Werte:  

    -   Microsoft.Exchange.Autodiscover  

    -   Microsoft.Exchange.OfflineAddressBook  

    -   Microsoft.Exchange.RPCMicrosoft.Exchange.WebServices  

    -   Microsoft.Exchange.RPCMicrosoft.Exchange.WebServices  

-   Weitere mögliche Werte für diesen Header umfassen Folgendes:  

    -   Microsoft.Exchange.Powershell  

    -   Microsoft.Exchange.SMTP  

    -   Microsoft.Exchange.Pop  

    -   Microsoft.Exchange.Imap  

### <a name="x-ms-client-user-agent"></a>X-MS-Client-User-Agent  
 Anspruchstyp: `http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`  

 Dieser AD FS-Anspruch enthält eine Zeichenfolge, um den Gerätetyp darstellen, den vom Client verwendet wird, um den Dienst zuzugreifen. Dies kann verwendet werden, wenn Kunden den Zugriff für bestimmte Geräte (z. B. bestimmte Arten von Smartphones) zu verhindern möchten.  Beispielwerte für diesen Anspruch enthalten (jedoch nicht beschränkt auf) die folgenden Werte.  

 Die im folgenden sind Beispiele für was der Wert der X-ms-Benutzer-Agent für einen Client enthalten kann, dessen X-ms-Client-Anwendung ist "Microsoft.Exchange.ActiveSync"  

- Vortex/1.0  

- Apple-iPad1C1/812.1  

- Apple-iPhone3C1/811.2  

- Apple-iPhone/704.11  

- Moto-DROID2/4.5.1  

- SAMSUNGSPHD700/100.202  

- Android/0.3  

  Es ist auch möglich, dass dieser Wert leer ist.  

### <a name="x-ms-proxy"></a>X-MS-Proxy  
 Anspruchstyp: `http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`  

 Dieser AD FS-Anspruch gibt an, dass die Anforderung über die Web Application Proxy übergeben wurde.  Dieser Anspruch wird von der Web Application Proxy, aufgefüllt, die den Header aufgefüllt wird, wenn die Authentifizierungsanforderung an die Back-End-Verbunddienst übergeben. AD FS konvertiert es dann in einen Anspruch.  

 Der Wert des Anspruchs ist der DNS-Name von der Web Application Proxy, der die Anforderung zu übergeben.  

### <a name="insidecorporatenetwork"></a>InsideCorporateNetwork  
 Anspruchstyp: `http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`  

 Ähnlich wie die oben genannten X-ms-Proxy-Anspruchstyp, dieser Anspruchstyp angibt, ob die Anforderung über den webanwendungsproxy übergeben hat. Im Gegensatz zu X-ms-Proxy ist Insidecorporatenetwork ein boolescher Wert mit "true", der angibt, einer Anforderung direkt an den Verbunddienst von innerhalb des Unternehmensnetzwerks.  

### <a name="x-ms-endpoint-absolute-path-active-vs-passive"></a>X-MS-Endpunkt-Absolute-Path (aktiv bzw. passiv)  
 Anspruchstyp: `http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`  

 Dieser Anspruchstyp kann zur Bestimmung der Anforderungen von "aktiv" (umfassenden)-Clients im Vergleich zu "Passiv" (Web-Browser-basiert)-Clients verwendet werden. Dadurch werden externe Anfragen von browserbasierten Anwendungen wie Outlook Web Access, SharePoint Online oder Office 365-Portal zugelassen werden, während die Anforderungen von rich-Clients wie Microsoft Outlook blockiert werden.  

 Der Wert des Anspruchs ist der Name der AD FS-Diensts, der die Anforderung empfangen hat.  

## <a name="see-also"></a>Siehe auch  
 [AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md)
