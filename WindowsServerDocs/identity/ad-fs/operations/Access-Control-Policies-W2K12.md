---
ms.assetid: 5728847d-dcef-4694-9080-d63bfb1fe24b
title: Access Control Richtlinien in AD FS in Windows Server 2012 R2
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/05/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 649b5d8b05b4512a7c42419af043db9afe4a1fde
ms.sourcegitcommit: de8fea497201d8f3d995e733dfec1d13a16cb8fa
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87863837"
---
# <a name="access-control-policies-in-windows-server-2012-r2-and-windows-server-2012-ad-fs"></a>Access Control Richtlinien in Windows Server 2012 R2 und Windows Server 2012 AD FS


Die in diesem Artikel beschriebenen Richtlinien nutzen zwei Arten von Ansprüchen.

1.  Anspruchs AD FS die basierend auf Informationen erstellt werden, die der AD FS und der webanwendungsproxy überprüfen und überprüfen können, z. b. die IP-Adresse des Clients, der direkt mit AD FS oder WAP

2.  Anspruchs AD FS erstellt basierend auf Informationen, die vom Client als HTTP-Header an AD FS weitergeleitet werden.

>**Wichtig**: die unten aufgeführten Richtlinien blockieren Windows 10-Domänen Beitritt und-Anmelde Szenarien, die Zugriff auf die folgenden zusätzlichen Endpunkte erfordern.

AD FS Endpunkte, die für das beitreten und Anmelden von Windows 10-Domänen erforderlich sind
- [Verbund Dienst Name]/ADFS/Services/Trust/2005/windowstransport
- [Verbund Dienst Name]/ADFS/Services/Trust/13/windowstransport
- [Verbund Dienst Name]/ADFS/Services/Trust/2005/usernamemixed
- [Verbund Dienst Name]/ADFS/Services/Trust/13/usernamemixed
- [Verbund Dienst Name]/ADFS/Services/Trust/2005/certificatemixed
- [Verbund Dienst Name]/ADFS/Services/Trust/13/certificatemixed

>**Wichtig**:/ADFS/Services/Trust/2005/windowstransport-und/ADFS/Services/Trust/13/windowstransport-Endpunkte sollten nur für den Intranetzugriff aktiviert werden, da Sie als Intranetorientierte Endpunkte verwendet werden sollen, die eine WIA-Bindung auf HTTPS verwenden. Wenn Sie Sie für das Extranet verfügbar machen, können Anforderungen an diese Endpunkte für die Umgehung von Sperrungs Schutz-Anforderungen Diese Endpunkte müssen auf dem Proxy deaktiviert werden (d. h. vom Extranet deaktiviert), um die AD-Konto Sperre zu schützen.

Aktualisieren Sie zum Beheben von Richtlinien, die auf Grundlage des Endpunkt Anspruchs ablehnen, um eine Ausnahme für die oben genannten Endpunkte zuzulassen.

Beispielsweise die folgende Regel:

`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "/adfs/ls/"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`

wird aktualisiert in:

`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "(/adfs/ls/)|(/adfs/services/trust/2005/windowstransport)|(/adfs/services/trust/13/windowstransport)|(/adfs/services/trust/2005/usernamemixed)|(/adfs/services/trust/13/usernamemixed)|(/adfs/services/trust/2005/certificatemixed)|(/adfs/services/trust/13/certificatemixed)"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`



> [!NOTE]
>  Ansprüche aus dieser Kategorie sollten nur verwendet werden, um Geschäftsrichtlinien und nicht als Sicherheitsrichtlinien zu implementieren, um den Zugriff auf Ihr Netzwerk zu schützen.  Es ist möglich, dass nicht autorisierte Clients Header mit falschen Informationen senden, um Zugriff zu erhalten.

Die in diesem Artikel beschriebenen Richtlinien sollten immer mit einer anderen Authentifizierungsmethode verwendet werden, wie z. b. Benutzername und Kennwort oder Multi-Factor Authentication.

## <a name="client-access-policies-scenarios"></a>Szenarios für Client Zugriffsrichtlinien

|**Szenario**|**Beschreibung**|
| --- | --- |
|Szenario 1: Blockieren des gesamten externen Zugriffs auf Office 365|Der Zugriff auf Office 365 ist für alle Clients im internen Unternehmensnetzwerk zulässig, Anforderungen externer Clients werden jedoch basierend auf der IP-Adresse des externen Clients verweigert.|
|Szenario 2: Blockieren des gesamten externen Zugriffs auf Office 365 mit Ausnahme von Exchange ActiveSync|Der Zugriff auf Office 365 ist von allen Clients im internen Unternehmensnetzwerk sowie von externen Client Geräten (z. b. Smartphones) zulässig, die Exchange ActiveSync nutzen. Alle anderen externen Clients, z. b. solche, die Outlook verwenden, werden blockiert.|
|Szenario 3: Blockieren des gesamten externen Zugriffs auf Office 365 außer auf browserbasierten Anwendungen|Blockiert den externen Zugriff auf Office 365, mit Ausnahme von passiven (browserbasierten) Anwendungen wie Outlook Webzugriff oder SharePoint Online.|
|Szenario 4: Blockieren des gesamten externen Zugriffs auf Office 365 mit Ausnahme der vorgesehenen Active Directory Gruppen|Dieses Szenario wird zum Testen und Überprüfen der Bereitstellung der Client Zugriffs Richtlinie verwendet. Der externe Zugriff auf Office 365 wird nur für Mitglieder einer oder mehrerer Active Directory Gruppe blockiert. Sie kann auch verwendet werden, um nur den Mitgliedern einer Gruppe externen Zugriff zu gewähren.|

## <a name="enabling-client-access-policy"></a>Aktivieren der Client Zugriffs Richtlinie
 Um die Client Zugriffs Richtlinie in AD FS in Windows Server 2012 R2 zu aktivieren, müssen Sie die Vertrauensstellung der vertrauenden Seite Microsoft Office 365 Identity Platform aktualisieren. Wählen Sie eines der unten aufgeführten Beispielszenarien aus, um die Anspruchs Regeln für die **Microsoft Office 365-Identitäts Plattform** -Vertrauensstellung der vertrauenden Seite zu konfigurieren, die den Anforderungen Ihrer Organisation am besten entspricht.

###  <a name="scenario-1-block-all-external-access-to-office-365"></a><a name="scenario1"></a>Szenario 1: Blockieren des gesamten externen Zugriffs auf Office 365
 Dieses Client Zugriffsrichtlinien-Szenario ermöglicht den Zugriff von allen internen Clients und blockiert alle externen Clients basierend auf der IP-Adresse des externen Clients. Mithilfe der folgenden Verfahren können Sie die richtigen Ausstellungs Autorisierungs Regeln zur Office 365-Vertrauensstellung der vertrauenden Seite für Ihr ausgewähltes Szenario hinzufügen.

##### <a name="to-create-rules-to-block-all-external-access-to-office-365"></a>So erstellen Sie Regeln, die den gesamten externen Zugriff auf Office 365 blockieren

1.  Klicken Sie in **Server-Manager**auf **Extras, und klicken Sie dann**auf **AD FS Verwaltung**.

2.  Klicken Sie in der Konsolen Struktur unter **AD fs\trust-Beziehungen**auf Vertrauens Stellungen der vertrauenden **Seite**, klicken Sie mit der rechten Maustaste auf die **Microsoft Office 365 Identität der Identitäts Plattform** , und klicken Sie dann auf **Anspruchs Regeln bearbeiten**.

3.  Wählen Sie im Dialogfeld **Anspruchs Regeln bearbeiten** die Registerkarte Ausstellungs **Autorisierungs Regeln** aus, und klicken Sie dann auf **Regel hinzufügen** , um den Anspruchs Regel-Assistenten zu starten.

4.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die Option **Ansprüche mithilfe einer benutzerdefinierten Regel senden**aus, und klicken Sie dann auf **weiter**.

5.  Geben Sie auf der Seite **Regel konfigurieren** unter **Anspruchs Regel Name**den anzeigen Amen für diese Regel ein, z. b. Wenn ein IP-Anspruch außerhalb des gewünschten Bereichs vorhanden ist. Geben Sie unter **benutzerdefinierte Regel**die folgende Syntax der Anspruchs Regel Sprache ein, oder fügen Sie Sie ein (ersetzen Sie den obigen Wert für "x-ms-weitergeleitete Client-IP" durch einen gültigen IP-Ausdruck):`c1:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");` </br>
6.  Klicken Sie auf **Fertig stellen**. Vergewissern Sie sich, dass die neue Regel in der Liste Ausstellungs Autorisierungs Regeln angezeigt wird, bevor Sie die Standardregel **für den Zugriff auf alle Benutzer zulassen** (die Ablehnungs Regel hat Vorrang, auch wenn Sie zuvor in der Liste angezeigt wird).  Wenn Sie nicht über die Standardregel für das Zulassen von Zugriffsberechtigungen verfügen, können Sie am Ende der Liste mit der Anspruchs Regel Sprache wie folgt eine hinzufügen:  </br>

    `c:[] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true"); `

7.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** auf **OK**, um die neuen Regeln zu speichern. Die resultierende Liste sollte wie folgt aussehen.

     ![Ausstellungsautorisierungsregeln](media/Access-Control-Policies-W2K12/clientaccess1.png "ADFS_Client_Access_1")

###  <a name="scenario-2-block-all-external-access-to-office-365-except-exchange-activesync"></a><a name="scenario2"></a>Szenario 2: Blockieren des gesamten externen Zugriffs auf Office 365 mit Ausnahme von Exchange ActiveSync
 Im folgenden Beispiel wird der Zugriff auf alle Office 365-Anwendungen einschließlich Exchange Online von internen Clients einschließlich Outlook ermöglicht. Der Zugriff von Clients, die sich außerhalb des Unternehmensnetzwerks befinden, wird durch die Client-IP-Adresse, mit Ausnahme von Exchange ActiveSync-Clients wie Smartphones, blockiert.

##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-exchange-activesync"></a>So erstellen Sie Regeln, um den gesamten externen Zugriff auf Office 365 mit Ausnahme von Exchange ActiveSync zu blockieren

1.  Klicken Sie in **Server-Manager**auf **Extras, und klicken Sie dann**auf **AD FS Verwaltung**.

2.  Klicken Sie in der Konsolen Struktur unter **AD fs\trust-Beziehungen**auf Vertrauens Stellungen der vertrauenden **Seite**, klicken Sie mit der rechten Maustaste auf die **Microsoft Office 365 Identität der Identitäts Plattform** , und klicken Sie dann auf **Anspruchs Regeln bearbeiten**.

3.  Wählen Sie im Dialogfeld **Anspruchs Regeln bearbeiten** die Registerkarte Ausstellungs **Autorisierungs Regeln** aus, und klicken Sie dann auf **Regel hinzufügen** , um den Anspruchs Regel-Assistenten zu starten.

4.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die Option **Ansprüche mithilfe einer benutzerdefinierten Regel senden**aus, und klicken Sie dann auf **weiter**.

5.  Geben Sie auf der Seite **Regel konfigurieren** unter **Anspruchs Regel Name**den anzeigen Amen für diese Regel ein, z. b. Wenn ein IP-Anspruch außerhalb des gewünschten Bereichs vorhanden ist, geben Sie den ipoutsiderange-Anspruch aus. Geben Sie unter **benutzerdefinierte Regel**die folgende Syntax der Anspruchs Regel Sprache ein, oder fügen Sie Sie ein (ersetzen Sie den obigen Wert für "x-ms-weitergeleitete Client-IP" durch einen gültigen IP-Ausdruck):

    `c1:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`

6.  Klicken Sie auf **Fertig stellen**. Vergewissern Sie sich, dass die neue Regel in der Liste Ausstellungs **Autorisierungs Regeln** angezeigt wird.

7.  Klicken Sie anschließend im Dialogfeld **Anspruchs Regeln bearbeiten** auf der Registerkarte Ausstellungs **Autorisierungs Regeln** auf **Regel hinzufügen** , um den Anspruchs Regel-Assistenten erneut zu starten.

8.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die Option **Ansprüche mithilfe einer benutzerdefinierten Regel senden**aus, und klicken Sie dann auf **weiter**.

9. Geben Sie auf der Seite **Regel konfigurieren** unter **Anspruchs Regel Name**den anzeigen Amen für diese Regel ein, z. b. wenn es eine IP-Adresse außerhalb des gewünschten Bereichs gibt und ein nicht-EAS-x-MS-Client-Application-Anspruch vorhanden ist. Geben oder fügen Sie unter **benutzerdefinierte Regel**die folgende Syntax der Anspruchs Regel Sprache ein:

    ```
    c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value != "Microsoft.Exchange.ActiveSync"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");
    ```

10. Klicken Sie auf **Fertig stellen**. Vergewissern Sie sich, dass die neue Regel in der Liste Ausstellungs **Autorisierungs Regeln** angezeigt wird.

11. Klicken Sie anschließend im Dialogfeld **Anspruchs Regeln bearbeiten** auf der Registerkarte Ausstellungs **Autorisierungs Regeln** auf **Regel hinzufügen** , um den Anspruchs Regel-Assistenten erneut zu starten.

12. Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage** die Option **Ansprüche mithilfe einer benutzerdefinierten Regel senden**aus, und klicken Sie dann auf **weiter**.

13. Geben Sie auf der Seite **Regel konfigurieren** unter **Anspruchs Regel Name**den anzeigen Amen für diese Regel ein, z. b. "überprüfen, ob Anwendungs Anspruch vorhanden ist". Geben oder fügen Sie unter **benutzerdefinierte Regel**die folgende Syntax der Anspruchs Regel Sprache ein:

    ```
    NOT EXISTS([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application"]) => add(Type = "http://custom/xmsapplication", Value = "fail");
    ```

14. Klicken Sie auf **Fertig stellen**. Vergewissern Sie sich, dass die neue Regel in der Liste Ausstellungs **Autorisierungs Regeln** angezeigt wird.

15. Klicken Sie anschließend im Dialogfeld **Anspruchs Regeln bearbeiten** auf der Registerkarte Ausstellungs **Autorisierungs Regeln** auf **Regel hinzufügen** , um den Anspruchs Regel-Assistenten erneut zu starten.

16. Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage** die Option **Ansprüche mithilfe einer benutzerdefinierten Regel senden**aus, und klicken Sie dann auf **weiter**.

17. Geben Sie auf der Seite **Regel konfigurieren** unter **Anspruchs Regel Name**den anzeigen Amen für diese Regel ein, z. b. "Benutzer mit ipoutsiderange true und Anwendungsfehler ablehnen". Geben oder fügen Sie unter **benutzerdefinierte Regel**die folgende Syntax der Anspruchs Regel Sprache ein:

    ```
    c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://custom/xmsapplication", Value == "fail"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");
    ```

18.  Klicken Sie auf **Fertig stellen**. Vergewissern Sie sich, dass die neue Regel direkt unterhalb der vorherigen Regel und vor der Standardregel "Zugriff auf alle Benutzer zulassen" in der Liste "Ausstellungs Autorisierungs Regeln" angezeigt wird (die Ablehnungs Regel hat Vorrang, auch wenn Sie zuvor in der Liste angezeigt wird).<p>Wenn Sie nicht über die Standardregel für das Zulassen von Zugriffsberechtigungen verfügen, können Sie am Ende der Liste mit der Anspruchs Regel Sprache wie folgt eine hinzufügen:

        ```
        c:[] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");
        ```

1.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** auf OK, um die neuen Regeln zu speichern. Die resultierende Liste sollte wie folgt aussehen.

    ![Ausstellungsautorisierungsregeln](media/Access-Control-Policies-W2K12/clientaccess2.png )

###  <a name="scenario-3-block-all-external-access-to-office-365-except-browser-based-applications"></a><a name="scenario3"></a>Szenario 3: Blockieren des gesamten externen Zugriffs auf Office 365 außer auf browserbasierten Anwendungen

##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-browser-based-applications"></a>So erstellen Sie Regeln, um den gesamten externen Zugriff auf Office 365 außer browserbasierten Anwendungen zu blockieren

1.  Klicken Sie in **Server-Manager**auf **Extras, und klicken Sie dann**auf **AD FS Verwaltung**.

2.  Klicken Sie in der Konsolen Struktur unter **AD fs\trust-Beziehungen**auf Vertrauens Stellungen der vertrauenden **Seite**, klicken Sie mit der rechten Maustaste auf die **Microsoft Office 365 Identität der Identitäts Plattform** , und klicken Sie dann auf **Anspruchs Regeln bearbeiten**.

3.  Wählen Sie im Dialogfeld **Anspruchs Regeln bearbeiten** die Registerkarte Ausstellungs **Autorisierungs Regeln** aus, und klicken Sie dann auf **Regel hinzufügen** , um den Anspruchs Regel-Assistenten zu starten.

4.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die Option **Ansprüche mithilfe einer benutzerdefinierten Regel senden**aus, und klicken Sie dann auf **weiter**.

5.  Geben Sie auf der Seite **Regel konfigurieren** unter **Anspruchs Regel Name**den anzeigen Amen für diese Regel ein, z. b. Wenn ein IP-Anspruch außerhalb des gewünschten Bereichs vorhanden ist, geben Sie den ipoutsiderange-Anspruch aus. Geben Sie unter **benutzerdefinierte Regel**die folgende Syntax der Anspruchs Regel Sprache ein, oder fügen Sie Sie ein (ersetzen Sie den obigen Wert für "x-ms-weitergeleitete Client-IP" durch einen gültigen IP-Ausdruck):

   ```
   c1:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");
   ```

1.  Klicken Sie auf **Fertig stellen**. Vergewissern Sie sich, dass die neue Regel in der Liste Ausstellungs **Autorisierungs Regeln** angezeigt wird.

2.  Klicken Sie anschließend im Dialogfeld **Anspruchs Regeln bearbeiten** auf der Registerkarte Ausstellungs **Autorisierungs Regeln** auf **Regel hinzufügen** , um den Anspruchs Regel-Assistenten erneut zu starten.

3.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage** die Option **Ansprüche mithilfe einer benutzerdefinierten Regel senden**aus, und klicken Sie dann auf **weiter**.

4. Geben Sie auf der Seite **Regel konfigurieren** unter **Anspruchs Regel Name**den anzeigen Amen für diese Regel ein, z. b. ", wenn eine IP-Adresse außerhalb des gewünschten Bereichs und der Endpunkt nicht/adfs/ls ist, Deny". Geben oder fügen Sie unter **benutzerdefinierte Regel**die folgende Syntax der Anspruchs Regel Sprache ein:

    ```
    c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "/adfs/ls/"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`
    ```

10. Klicken Sie auf **Fertig stellen**. Vergewissern Sie sich, dass die neue Regel in der Liste Ausstellungs Autorisierungs Regeln angezeigt wird, bevor Sie die Standardregel **für den Zugriff auf alle Benutzer zulassen** (die Ablehnungs Regel hat Vorrang, auch wenn Sie zuvor in der Liste angezeigt wird).  </br></br> Wenn Sie nicht über die Standardregel für das Zulassen von Zugriffsberechtigungen verfügen, können Sie am Ende der Liste mit der Anspruchs Regel Sprache wie folgt eine hinzufügen:

   `c:[] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");`

11. Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** auf **OK**, um die neuen Regeln zu speichern. Die resultierende Liste sollte wie folgt aussehen.

    ![Ausstellung](media/Access-Control-Policies-W2K12/clientaccess3.png)

###  <a name="scenario-4-block-all-external-access-to-office-365-except-for-designated-active-directory-groups"></a><a name="scenario4"></a>Szenario 4: Blockieren des gesamten externen Zugriffs auf Office 365 mit Ausnahme der vorgesehenen Active Directory Gruppen
 Im folgenden Beispiel wird der Zugriff von internen Clients basierend auf der IP-Adresse ermöglicht. Der Zugriff von Clients außerhalb des Unternehmensnetzwerks, die über eine externe Client-IP-Adresse verfügen, wird blockiert, mit Ausnahme der Einzelpersonen in einer angegebenen Active Directory Gruppe. führen Sie die folgenden Schritte aus, um die richtigen Ausstellungs Autorisierungs Regeln mithilfe des Anspruchs Regel-Assistenten der **Microsoft Office 365 Identity Platform** -Vertrauensstellung der vertrauenden Seite hinzuzufügen:

##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-for-designated-active-directory-groups"></a>So erstellen Sie Regeln, die den gesamten externen Zugriff auf Office 365 blockieren, mit Ausnahme der vorgesehenen Active Directory Gruppen

1.  Klicken Sie in **Server-Manager**auf **Extras, und klicken Sie dann**auf **AD FS Verwaltung**.

2.  Klicken Sie in der Konsolen Struktur unter **AD fs\trust-Beziehungen**auf Vertrauens Stellungen der vertrauenden **Seite**, klicken Sie mit der rechten Maustaste auf die **Microsoft Office 365 Identität der Identitäts Plattform** , und klicken Sie dann auf **Anspruchs Regeln bearbeiten**.

3.  Wählen Sie im Dialogfeld **Anspruchs Regeln bearbeiten** die Registerkarte Ausstellungs **Autorisierungs Regeln** aus, und klicken Sie dann auf **Regel hinzufügen** , um den Anspruchs Regel-Assistenten zu starten.

4.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die Option **Ansprüche mithilfe einer benutzerdefinierten Regel senden**aus, und klicken Sie dann auf **weiter**.

5.  Geben Sie auf der Seite **Regel konfigurieren** unter **Anspruchs Regel Name**den anzeigen Amen für diese Regel ein, z. b. "Wenn ein IP-Anspruch außerhalb des gewünschten Bereichs vorhanden ist, geben Sie den ipoutsiderange-Anspruch aus." Geben Sie unter **benutzerdefinierte Regel**die folgende Syntax der Anspruchs Regel Sprache ein, oder fügen Sie Sie ein (ersetzen Sie den obigen Wert für "x-ms-weitergeleitete Client-IP" durch einen gültigen IP-Ausdruck):

    ```
    `c1:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] && c2:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`
    ```

6. Klicken Sie auf **Fertig stellen**. Vergewissern Sie sich, dass die neue Regel in der Liste Ausstellungs **Autorisierungs Regeln** angezeigt wird.

7. Klicken Sie anschließend im Dialogfeld **Anspruchs Regeln bearbeiten** auf der Registerkarte Ausstellungs **Autorisierungs Regeln** auf **Regel hinzufügen** , um den Anspruchs Regel-Assistenten erneut zu starten.

8. Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage** die Option **Ansprüche mithilfe einer benutzerdefinierten Regel senden**aus, und klicken Sie dann auf **weiter**.

9. Geben Sie auf der Seite **Regel konfigurieren** unter **Anspruchs Regel Name**den anzeigen Amen für diese Regel ein, z. b. "Gruppen-SID überprüfen". Geben Sie unter **benutzerdefinierte Regel**die folgende Syntax der Anspruchs Regel Sprache ein, oder fügen Sie Sie ein (ersetzen Sie "groupsid" durch die tatsächliche SID der Ad-Gruppe, die Sie verwenden):

    ```
    NOT EXISTS([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-32-100"]) => add(Type = "http://custom/groupsid", Value = "fail");
    ```

10. Klicken Sie auf **Fertig stellen**. Vergewissern Sie sich, dass die neue Regel in der Liste Ausstellungs **Autorisierungs Regeln** angezeigt wird.

11. Klicken Sie anschließend im Dialogfeld **Anspruchs Regeln bearbeiten** auf der Registerkarte Ausstellungs **Autorisierungs Regeln** auf **Regel hinzufügen** , um den Anspruchs Regel-Assistenten erneut zu starten.

12. Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage** die Option **Ansprüche mithilfe einer benutzerdefinierten Regel senden**aus, und klicken Sie dann auf **weiter**.

13. Geben Sie auf der Seite **Regel konfigurieren** unter **Anspruchs Regel Name**den anzeigen Amen für diese Regel ein, z. b. "Benutzer mit ipoutsiderange true und groupsid Fail ablehnen". Geben oder fügen Sie unter **benutzerdefinierte Regel**die folgende Syntax der Anspruchs Regel Sprache ein:

   ```
   c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://custom/groupsid", Value == "fail"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");
   ```

14. Klicken Sie auf **Fertig stellen**. Vergewissern Sie sich, dass die neue Regel direkt unterhalb der vorherigen Regel und vor der Standardregel "Zugriff auf alle Benutzer zulassen" in der Liste "Ausstellungs Autorisierungs Regeln" angezeigt wird (die Ablehnungs Regel hat Vorrang, auch wenn Sie zuvor in der Liste angezeigt wird).  </br></br>Wenn Sie nicht über die Standardregel für das Zulassen von Zugriffsberechtigungen verfügen, können Sie am Ende der Liste mit der Anspruchs Regel Sprache wie folgt eine hinzufügen:

   ```
   c:[] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");
   ```

15. Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** auf OK, um die neuen Regeln zu speichern. Die resultierende Liste sollte wie folgt aussehen.

     ![Ausstellung](media/Access-Control-Policies-W2K12/clientaccess4.png)

##  <a name="building-the-ip-address-range-expression"></a><a name="buildingip"></a>Der Ausdruck für den IP-Adressbereich wird aufgebaut
 Der "x-ms-weitergeleitete Client-IP"-Anspruch wird mit einem HTTP-Header aufgefüllt, der zurzeit nur von Exchange Online festgelegt ist. dieser Wert füllt den Header auf, wenn die Authentifizierungsanforderung an AD FS übergeben wird. Der Wert des Anspruchs kann eines der folgenden sein:

> [!NOTE]
> Exchange Online unterstützt derzeit nur IPv4-und nicht IPv6-Adressen.

- Eine einzelne IP-Adresse: die IP-Adresse des Clients, der direkt mit Exchange Online verbunden ist

> [!NOTE]
> - Die IP-Adresse eines Clients im Unternehmensnetzwerk wird als IP-Adresse der externen Schnittstelle des ausgehenden Proxys oder Gateways der Organisation angezeigt.
> - Clients, die über ein VPN oder Microsoft DirectAccess (da) mit dem Unternehmensnetzwerk verbunden sind, werden je nach Konfiguration von VPN oder da möglicherweise als interne Unternehmens Clients oder als externe Clients angezeigt.

- Mindestens eine IP-Adresse: Wenn Exchange Online die IP-Adresse des Clients, der die Verbindung herstellt, nicht ermitteln kann, wird der Wert auf Grundlage des Werts des x-weitergeleiteten für-Headers festgelegt, ein nicht standardmäßiger Header, der in http-basierten Anforderungen eingeschlossen werden kann und von vielen Clients, Lasten Ausgleichs Modulen und Proxys auf dem Markt unterstützt wird.

> [!NOTE]
> 1. Mehrere IP-Adressen, die die Client-IP-Adresse und die Adresse der einzelnen Proxys angeben, die die Anforderung übermittelt haben, werden durch Kommas getrennt.
> 2. IP-Adressen im Zusammenhang mit der Exchange Online-Infrastruktur werden nicht in der Liste angezeigt.

### <a name="regular-expressions"></a>Reguläre Ausdrücke
 Wenn Sie einen Bereich von IP-Adressen zuordnen müssen, ist es erforderlich, einen regulären Ausdruck zu erstellen, um den Vergleich durchzuführen. In der nächsten Reihe von Schritten werden Beispiele für das Erstellen eines solchen Ausdrucks für die folgenden Adressbereiche bereitgestellt (Beachten Sie, dass Sie diese Beispiele entsprechend Ihrem öffentlichen IP-Adressbereich ändern müssen):

- 192.168.1.1 – 192.168.1.25

- 10.0.0.1 – 10.0.0.14

  Zuerst lautet das grundlegende Muster, das einer einzelnen IP-Adresse entspricht, wie folgt: \b # # # \\ . # # # \\ . # # # \\ . # # # \b

  Dadurch können wir zwei unterschiedliche IP-Adressen wie folgt mit einem or-Ausdruck vergleichen: \b # # # \\ . # # # \\ . # # # \\ . # # # \b&#124; \b # # # \\ . # # # \\ . # # # \\ . # # # \b

  Ein Beispiel für die Anpassung von nur zwei Adressen (z. b. 192.168.1.1 oder 10.0.0.1) lautet: \b192 \\ . 168 1. \\ \\ 1&#124; \b10 \\ 0 \\ . 0 \\ . 1 \ b

  Auf diese Weise können Sie eine beliebige Anzahl von Adressen eingeben. Wenn ein Adressbereich zulässig sein muss, z. b. 192.168.1.1 – 192.168.1.25, muss die Übereinstimmung Zeichen nach Zeichen durchgeführt werden: \b192 \\ . 168 \\ . 1 \\ . ( [1-9] &#124;1 [0-9] &#124;2 [0-5]) \b

  Beachten Sie Folgendes:

- Die IP-Adresse wird als Zeichenfolge und nicht als Zahl behandelt.

- Die Regel wird wie folgt aufgegliedert: \b192 \\ . 168 \\ . 1 \\ .

- Dies entspricht einem beliebigen Wert, der mit 192.168.1 beginnt.

- Folgendes entspricht den Bereichen, die für den Teil der Adresse nach dem letzten Dezimaltrennzeichen erforderlich sind:

  - ([1-9] entspricht Adressen, die auf 1-9 enden

  - &#124;1 [0-9] entspricht Adressen, die auf 10-19 enden

  - &#124;2 [0-5]) entspricht Adressen, die auf 20-25 enden

- Beachten Sie, dass die Klammern ordnungsgemäß positioniert werden müssen, damit Sie nicht mit anderen Teilen von IP-Adressen übereinstimmen.

- Wenn der 192-Block übereinstimmt, können wir einen ähnlichen Ausdruck für den 10-Block schreiben: \b10 \\ 0 \\ . 0 \\ . ( [1-9] &#124;1 [0-4]) \b

- Der folgende Ausdruck muss alle Adressen für "192.168.1.1 ~ 25" und "10.0.0.1 ~ 14": \b192 \\ . 168 \\ . 1 entsprechen \\ . [1-9] &#124;1 [0-9] &#124;2 [0-5]) \b&#124; \b10 \\ 0 \\ . 0 \\ . ( [1-9] &#124;1 [0-4]) \b

### <a name="testing-the-expression"></a>Testen des Ausdrucks
 Regex-Ausdrücke können recht kompliziert werden, daher wird dringend empfohlen, ein Regex-Überprüfungs Tool zu verwenden. Wenn Sie eine Internetsuche nach "Online-Regex Expression Builder" durchführen, finden Sie mehrere gute Online Dienstprogramme, mit denen Sie Ihre Ausdrücke anhand von Beispiel Daten ausprobieren können.

 Beim Testen des Ausdrucks ist es wichtig, dass Sie wissen, was zu erwarten ist. Das Exchange Online-System sendet möglicherweise viele IP-Adressen, die durch Kommas getrennt sind. Der oben angegebene Ausdruck funktioniert für dieses. Dies ist jedoch wichtig, wenn Sie die Regex-Ausdrücke testen. Beispielsweise kann eine der folgenden Beispiel Eingaben verwendet werden, um die obigen Beispiele zu überprüfen:

 192.168.1.1, 192.168.1.2, 192.169.1.1. 192.168.12.1, 192.168.1.10, 192.168.1.25, 192.168.1.26, 192.168.1.30, 1192.168.1.20

 10.0.0.1, 10.0.0.5, 10.0.0.10, 10.0.1.0, 10.0.1.1, 110.0.0.1, 10.0.0.14, 10.0.0.15, 10.0.0.10, 10, 0.0.1

## <a name="claim-types"></a>Anspruchstypen
 AD FS in Windows Server 2012 R2 bietet Anforderungs Kontextinformationen mithilfe der folgenden Anspruchs Typen:

### <a name="x-ms-forwarded-client-ip"></a>X-MS-weitergeleitete Client-IP
 Anspruchstyp:`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`

 Dieser AD FS Anspruch stellt einen "besten Versuch" dar, die IP-Adresse des Benutzers (z. b. den Outlook-Client) zu ermitteln, der die Anforderung sendet. Dieser Anspruch kann mehrere IP-Adressen enthalten, einschließlich der Adresse jedes Proxys, von dem die Anforderung weitergeleitet wurde.  Dieser Anspruch wird mit einem http-Wert aufgefüllt. Der Wert des Anspruchs kann eines der folgenden sein:

- Eine einzelne IP-Adresse: die IP-Adresse des Clients, der direkt mit Exchange Online verbunden ist

> [!NOTE]
> Die IP-Adresse eines Clients im Unternehmensnetzwerk wird als IP-Adresse der externen Schnittstelle des ausgehenden Proxys oder Gateways der Organisation angezeigt.

- Mindestens eine IP-Adresse

  - Wenn Exchange Online die IP-Adresse des Clients, der die Verbindung herstellt, nicht ermitteln kann, wird der Wert auf Grundlage des Werts des x-weitergeleiteten-für-Headers festgelegt, ein nicht standardmäßiger Header, der in http-basierten Anforderungen eingeschlossen werden kann und von vielen Clients, Lasten Ausgleichs Modulen und Proxys auf dem Markt unterstützt wird.

  - Mehrere IP-Adressen, die angeben, dass die Client-IP-Adresse und die Adresse der einzelnen Proxys, die die Anforderung bestehen, durch Kommas getrennt werden

> [!NOTE]
> IP-Adressen im Zusammenhang mit der Exchange Online-Infrastruktur sind nicht in der Liste vorhanden.

> [!WARNING]
> Exchange Online unterstützt zurzeit nur IPv4-Adressen. IPv6-Adressen werden nicht unterstützt.

### <a name="x-ms-client-application"></a>X-MS-Client-Anwendung
 Anspruchstyp:`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`

 Dieser AD FS Anspruch stellt das vom Endclient verwendete Protokoll dar, das der verwendeten Anwendung lose entspricht.  Dieser Anspruch wird mit einem HTTP-Header aufgefüllt, der derzeit nur von Exchange Online festgelegt wird, der den-Header auffüllt, wenn die Authentifizierungsanforderung an AD FS übergeben wird. Abhängig von der Anwendung ist der Wert dieses Anspruchs einer der folgenden:

- Bei Geräten, die Exchange Active Sync verwenden, lautet der Wert Microsoft. Exchange. ActiveSync.

- Die Verwendung des Microsoft Outlook-Clients kann zu einem der folgenden Werte führen:

    - Microsoft. Exchange. autodiscover

    - Microsoft. Exchange. OfflineAddressBook

    - Microsoft. Exchange. rpcmicrosoft. Exchange. Webservices

    - Microsoft. Exchange. rpcmicrosoft. Exchange. Webservices

- Zu den anderen möglichen Werten für diesen Header zählen die folgenden:

    - Microsoft. Exchange. PowerShell

    - Microsoft. Exchange. SMTP

    - Microsoft. Exchange. Pop

    - Microsoft. Exchange. IMAP

### <a name="x-ms-client-user-agent"></a>X-MS-Client-User-Agent
 Anspruchstyp:`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`

 Dieser AD FS Anspruch stellt eine Zeichenfolge bereit, die den Gerätetyp darstellt, der vom Client für den Zugriff auf den Dienst verwendet wird. Dies kann verwendet werden, wenn Kunden den Zugriff für bestimmte Geräte (z. b. bestimmte Arten von Smartphones) verhindern möchten.  Beispiel Werte für diesen Anspruch sind die unten aufgeführten Werte (aber nicht beschränkt auf).

 Im folgenden finden Sie Beispiele für den Wert des x-MS-User-Agent-Werts für einen Client, dessen x-MS-Client-Anwendung "Microsoft. Exchange. ActiveSync" ist.

- Vortex/1.0

- Apple-iPad1C1/812.1

- Apple-iPhone3C1/811.2

- Apple-iPhone/704.11

- Moto-DROID2/4.5.1

- SAMSUNGSPHD700/100.202

- Android/0.3

  Es ist auch möglich, dass dieser Wert leer ist.

### <a name="x-ms-proxy"></a>X-MS-Proxy
 Anspruchstyp:`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`

 Dieser AD FS Anspruch gibt an, dass die Anforderung den webanwendungsproxy übermittelt hat.  Dieser Anspruch wird durch den webanwendungsproxy aufgefüllt, der den-Header auffüllt, wenn die Authentifizierungsanforderung an das Back-End-Verbunddienst übergeben wird. AD FS dann in einen Anspruch konvertiert.

 Der Wert des Anspruchs ist der DNS-Name des webanwendungsproxys, der die Anforderung übermittelt hat.

### <a name="insidecorporatenetwork"></a>Insizercorporatenetwork
 Anspruchstyp:`https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`

 Ähnlich wie bei dem obigen Anspruchstyp "x-ms-Proxy" gibt dieser Anspruchstyp an, ob die Anforderung den webanwendungsproxy übermittelt hat. Anders als bei x-ms-Proxy ist insidecorporatenetwork ein boolescher Wert mit true, der eine Anforderung direkt an den Verbund Dienst innerhalb des Unternehmensnetzwerks anzeigt.

### <a name="x-ms-endpoint-absolute-path-active-vs-passive"></a>X-MS-Endpoint-absolute-path (aktiv/passiv)
 Anspruchstyp:`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`

 Dieser Anspruchstyp kann zum Bestimmen von Anforderungen verwendet werden, die von "aktiven" (Rich) Clients und "passiven" (Webbrowser basierten) Clients stammen. Dadurch können externe Anforderungen von browserbasierten Anwendungen wie Outlook Webzugriff, SharePoint Online oder dem Office 365-Portal zugelassen werden, während Anforderungen, die von Rich-Clients wie Microsoft Outlook stammen, blockiert werden.

 Der Wert des Anspruchs ist der Name des AD FS Dienstanbieter, der die Anforderung empfangen hat.

## <a name="see-also"></a>Weitere Informationen
 [AD FS-Vorgänge](../ad-fs-operations.md)
