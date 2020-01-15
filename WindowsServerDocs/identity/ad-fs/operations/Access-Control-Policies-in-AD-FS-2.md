---
ms.assetid: ''
title: Client Access Control Richtlinien in Active Directory-Verbunddienste (AD FS) 2,0
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 4f5d2cfa8383bcf3c0813b272f8c4828473b8df9
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/14/2020
ms.locfileid: "75948608"
---
# <a name="client-access-control-policies-in-ad-fs-20"></a>Client Access Control Richtlinien in AD FS 2,0
Mit den Client Zugriffsrichtlinien in Active Directory-Verbunddienste (AD FS) 2,0 können Sie Benutzern den Zugriff auf Ressourcen einschränken oder gewähren.  In diesem Dokument wird beschrieben, wie Sie Client Zugriffsrichtlinien in AD FS 2,0 aktivieren und die gängigsten Szenarien konfigurieren.

## <a name="enabling-client-access-policy-in-ad-fs-20"></a>Aktivieren der Client Zugriffs Richtlinie in AD FS 2,0

Führen Sie die folgenden Schritte aus, um die Client Zugriffs Richtlinie zu aktivieren.

### <a name="step-1-install-the-update-rollup-2-for-ad-fs-20-package-on-your-ad-fs-servers"></a>Schritt 1: Installieren des Updaterollup 2 für AD FS 2,0-Paket auf Ihren AD FS Servern

Laden Sie das Paket [Updaterollup 2 für Active Directory-Verbunddienste (AD FS) (AD FS) 2,0](https://support.microsoft.com/help/2681584/description-of-update-rollup-2-for-active-directory-federation-services-ad-fs-2.0) herunter, und installieren Sie es auf allen Verbund Servern und Verbund Server Proxys.

### <a name="step-2-add-five-claim-rules-to-the-active-directory-claims-provider-trust"></a>Schritt 2: Hinzufügen von fünf Anspruchs Regeln zur Active Directory Anspruchs Anbieter-Vertrauensstellung

Nachdem Updaterollup 2 auf allen AD FS Servern und Proxys installiert wurde, gehen Sie folgendermaßen vor, um einen Satz von Anspruchs Regeln hinzuzufügen, die die neuen Anspruchs Typen für die Richtlinien-Engine verfügbar machen.

Zu diesem Zweck fügen Sie mit dem folgenden Verfahren fünf Akzeptanz Transformationsregeln für jeden der neuen Anforderungs Kontext-Anspruchs Typen hinzu.

Erstellen Sie auf der Active Directory Anspruchs Anbieter-Vertrauensstellung eine neue Akzeptanz Transformations Regel, um jeden der neuen Anforderungs Kontext-Anspruchs Typen zu durchlaufen.

#### <a name="to-add-a-claim-rule-to-the-active-directory-claims-provider-trust-for-each-of-the-five-context-claim-types"></a>Fügen Sie der Active Directory Anspruchs Anbieter-Vertrauensstellung für jeden der fünf Kontext Anspruchs Typen eine Anspruchs Regel hinzu:


1. Klicken Sie auf Start, zeigen Sie auf Programme, zeigen Sie auf Verwaltung, und klicken Sie dann auf AD FS 2,0-Verwaltung.
2. Klicken Sie in der Konsolen Struktur unter AD FS 2.0 \ Vertrauens Stellungen auf Anspruchs Anbieter-Vertrauens Stellungen, klicken Sie mit der rechten Maustaste auf Active Directory, und klicken Sie dann auf Anspruchs Regeln bearbeiten.
3. Wählen Sie im Dialogfeld Anspruchs Regeln bearbeiten die Registerkarte Akzeptanz Transformationsregeln aus, und klicken Sie dann auf Regel hinzufügen, um den Regel-Assistenten zu starten.
4. Wählen Sie auf der Seite Regel Vorlage auswählen unter Anspruchs Regel Vorlage die Option Pass-Through oder einen eingehenden Anspruch Filtern aus der Liste aus, und klicken Sie dann auf Weiter.
5. Geben Sie auf der Seite Regel konfigurieren unter Anspruchs Regel Name den anzeigen Amen für diese Regel ein. Geben Sie unter Typ des eingehenden Anspruchs die folgende Anspruchstyp-URL ein, und wählen Sie dann alle Anspruchs Werte durchlaufen aus.</br>
        `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`</br>
6. Um die Regel zu überprüfen, wählen Sie Sie in der Liste aus, klicken Sie auf Regel bearbeiten und dann auf Regel Sprache anzeigen. Die Anspruchs Regel Sprache sollte wie folgt aussehen: `c:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip"] => issue(claim = c);`
7. Klicken Sie auf Fertigstellen.
8. Klicken Sie im Dialogfeld Anspruchs Regeln bearbeiten auf OK, um die Regeln zu speichern.
9. Wiederholen Sie die Schritte 2 bis 6, um eine zusätzliche Anspruchs Regel für jeden der verbleibenden vier Anspruchs Typen zu erstellen, bis alle fünf Regeln erstellt wurden.

    `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`


~~~
`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`

`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`

`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`
~~~

### <a name="step-3-update-the-microsoft-office-365-identity-platform-relying-party-trust"></a>Schritt 3: Aktualisieren der Microsoft Office 365 Identity Platform-Vertrauensstellung der vertrauenden Seite

Wählen Sie eines der unten aufgeführten Beispielszenarien aus, um die Anspruchs Regeln für die Microsoft Office 365-Identitäts Plattform-Vertrauensstellung der vertrauenden Seite zu konfigurieren, die den Anforderungen Ihrer Organisation am besten entspricht.

## <a name="client-access-policy-scenarios-for-ad-fs-20"></a>Szenarien für die Client Zugriffs Richtlinie für AD FS 2,0
In den folgenden Abschnitten werden die Szenarien beschrieben, die für AD FS 2,0

### <a name="scenario-1-block-all-external-access-to-office-365"></a>Szenario 1: Blockieren des gesamten externen Zugriffs auf Office 365

Dieses Client Zugriffsrichtlinien-Szenario ermöglicht den Zugriff von allen internen Clients und blockiert alle externen Clients basierend auf der IP-Adresse des externen Clients. Der Regelsatz basiert auf der standardmäßigen Ausstellungs Autorisierungs Regel, die den Zugriff auf alle Benutzer zulässt. Mithilfe des folgenden Verfahrens können Sie eine Ausstellungs Autorisierungs Regel zur Office 365-Vertrauensstellung der vertrauenden Seite hinzufügen.

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365"></a>So erstellen Sie eine Regel zum Blockieren des gesamten externen Zugriffs auf Office 365



1. Klicken Sie auf Start, zeigen Sie auf Programme, zeigen Sie auf Verwaltung, und klicken Sie dann auf AD FS 2,0-Verwaltung.
2. Klicken Sie in der Konsolen Struktur unter AD FS 2.0 \ Vertrauens Stellungen auf Vertrauens Stellungen der vertrauenden Seite, klicken Sie mit der rechten Maustaste auf die Microsoft Office 365 Identity Platform-Vertrauensstellung, und klicken Sie dann auf Anspruchs Regeln bearbeiten. 
3. Wählen Sie im Dialogfeld Anspruchs Regeln bearbeiten die Registerkarte Ausstellungs Autorisierungs Regeln aus, und klicken Sie dann auf Regel hinzufügen, um den Anspruchs Regel-Assistenten zu starten.
4. Wählen Sie auf der Seite Regel Vorlage auswählen unter Anspruchs Regel Vorlage die Option Ansprüche mithilfe einer benutzerdefinierten Regel senden aus, und klicken Sie dann auf Weiter.
5. Geben Sie auf der Seite Regel konfigurieren unter Anspruchs Regel Name den anzeigen Amen für diese Regel ein. Geben Sie unter benutzerdefinierte Regel die folgende Syntax der Anspruchs Regel Sprache ein, oder fügen Sie Sie ein: `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");` 
6. Klicken Sie auf Fertigstellen. Vergewissern Sie sich, dass die neue Regel direkt unterhalb der Regel Zugriff auf alle Benutzer zulassen in der Liste Ausstellungs Autorisierungs Regeln angezeigt wird.
7. Um die Regel zu speichern, klicken Sie im Dialogfeld Anspruchs Regeln bearbeiten auf OK.

>[!NOTE]
>Sie müssen den obigen Wert für "öffentliche IP-Adresse-Regex" durch einen gültigen IP-Ausdruck ersetzen. Weitere Informationen finden Sie unter Building the IP Address Range Expression.


### <a name="scenario-2-block-all-external-access-to-office-365-except-exchange-activesync"></a>Szenario 2: Blockieren des gesamten externen Zugriffs auf Office 365 mit Ausnahme von Exchange ActiveSync

Im folgenden Beispiel wird der Zugriff auf alle Office 365-Anwendungen einschließlich Exchange Online von internen Clients einschließlich Outlook ermöglicht. Der Zugriff von Clients, die sich außerhalb des Unternehmensnetzwerks befinden, wird durch die Client-IP-Adresse, mit Ausnahme von Exchange ActiveSync-Clients wie Smartphones, blockiert. Der Regelsatz basiert auf der standardmäßigen Ausstellungs Autorisierungs Regel mit dem Titel zulassen des Zugriffs für alle Benutzer. Führen Sie die folgenden Schritte aus, um mithilfe des Anspruchs Regel-Assistenten eine Ausstellungs Autorisierungs Regel zur Office 365-Vertrauensstellung der vertrauenden Seite hinzuzufügen:

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365"></a>So erstellen Sie eine Regel zum Blockieren des gesamten externen Zugriffs auf Office 365



1. Klicken Sie auf Start, zeigen Sie auf Programme, zeigen Sie auf Verwaltung, und klicken Sie dann auf AD FS 2,0-Verwaltung.
2. Klicken Sie in der Konsolen Struktur unter AD FS 2.0 \ Vertrauens Stellungen auf Vertrauens Stellungen der vertrauenden Seite, klicken Sie mit der rechten Maustaste auf die Microsoft Office 365 Identity Platform-Vertrauensstellung, und klicken Sie dann auf Anspruchs Regeln bearbeiten. 
3. Wählen Sie im Dialogfeld Anspruchs Regeln bearbeiten die Registerkarte Ausstellungs Autorisierungs Regeln aus, und klicken Sie dann auf Regel hinzufügen, um den Anspruchs Regel-Assistenten zu starten.
4. Wählen Sie auf der Seite Regel Vorlage auswählen unter Anspruchs Regel Vorlage die Option Ansprüche mithilfe einer benutzerdefinierten Regel senden aus, und klicken Sie dann auf Weiter.
5. Geben Sie auf der Seite Regel konfigurieren unter Anspruchs Regel Name den anzeigen Amen für diese Regel ein. Geben Sie unter benutzerdefinierte Regel die folgende Syntax der Anspruchs Regel Sprache ein, oder fügen Sie Sie ein: `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application",
    Value=="Microsoft.Exchange.Autodiscover"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application",
    Value=="Microsoft.Exchange.ActiveSync"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. Klicken Sie auf Fertigstellen. Vergewissern Sie sich, dass die neue Regel direkt unterhalb der Regel Zugriff auf alle Benutzer zulassen in der Liste Ausstellungs Autorisierungs Regeln angezeigt wird.
7. Um die Regel zu speichern, klicken Sie im Dialogfeld Anspruchs Regeln bearbeiten auf OK.

>[!NOTE]
>Sie müssen den obigen Wert für "öffentliche IP-Adresse-Regex" durch einen gültigen IP-Ausdruck ersetzen. Weitere Informationen finden Sie unter Building the IP Address Range Expression.

### <a name="scenario-3-block-all-external-access-to-office-365-except-browser-based-applications"></a>Szenario 3: Blockieren des gesamten externen Zugriffs auf Office 365 außer auf browserbasierten Anwendungen

Der Regelsatz basiert auf der standardmäßigen Ausstellungs Autorisierungs Regel mit dem Titel zulassen des Zugriffs für alle Benutzer. Gehen Sie folgendermaßen vor, um der Microsoft Office 365 Identity Platform-Vertrauensstellung der vertrauenden Seite mithilfe des Anspruchs Regel-Assistenten eine Ausstellungs Autorisierungs Regel hinzuzufügen:

>[!NOTE]
>Dieses Szenario wird bei einem Proxy eines Drittanbieters aufgrund von Einschränkungen bei Client Zugriffsrichtlinien-Headern mit passiven (webbasierten) Anforderungen nicht unterstützt.

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365-except-browser-based-applications"></a>So erstellen Sie eine Regel, die den gesamten externen Zugriff auf Office 365 außer browserbasierten Anwendungen blockiert



1. Klicken Sie auf Start, zeigen Sie auf Programme, zeigen Sie auf Verwaltung, und klicken Sie dann auf AD FS 2,0-Verwaltung.
2. Klicken Sie in der Konsolen Struktur unter AD FS 2.0 \ Vertrauens Stellungen auf Vertrauens Stellungen der vertrauenden Seite, klicken Sie mit der rechten Maustaste auf die Microsoft Office 365 Identity Platform-Vertrauensstellung, und klicken Sie dann auf Anspruchs Regeln bearbeiten. 
3. Wählen Sie im Dialogfeld Anspruchs Regeln bearbeiten die Registerkarte Ausstellungs Autorisierungs Regeln aus, und klicken Sie dann auf Regel hinzufügen, um den Anspruchs Regel-Assistenten zu starten.
4. Wählen Sie auf der Seite Regel Vorlage auswählen unter Anspruchs Regel Vorlage die Option Ansprüche mithilfe einer benutzerdefinierten Regel senden aus, und klicken Sie dann auf Weiter.
5. Geben Sie auf der Seite Regel konfigurieren unter Anspruchs Regel Name den anzeigen Amen für diese Regel ein. Geben Sie unter benutzerdefinierte Regel die folgende Syntax der Anspruchs Regel Sprache ein, oder fügen Sie Sie ein: `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value == "/adfs/ls/"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. Klicken Sie auf Fertigstellen. Vergewissern Sie sich, dass die neue Regel direkt unterhalb der Regel Zugriff auf alle Benutzer zulassen in der Liste Ausstellungs Autorisierungs Regeln angezeigt wird.
7. Um die Regel zu speichern, klicken Sie im Dialogfeld Anspruchs Regeln bearbeiten auf OK.

### <a name="scenario-4-block-all-external-access-to-office-365-for-designated-active-directory-groups"></a>Szenario 4: Blockieren des gesamten externen Zugriffs auf Office 365 für bestimmte Active Directory Gruppen

Im folgenden Beispiel wird der Zugriff von internen Clients basierend auf der IP-Adresse ermöglicht. Der Zugriff von Clients außerhalb des Unternehmensnetzwerks, die über eine externe Client-IP-Adresse verfügen, wird blockiert, mit Ausnahme der Einzelpersonen in einer angegebenen Active Directory Gruppe. der Regelsatz basiert auf der standardmäßigen Ausstellungs Autorisierungs Regel mit dem Titel zulassen des Zugriffs auf Alle Benutzer. Gehen Sie folgendermaßen vor, um der Microsoft Office 365 Identity Platform-Vertrauensstellung der vertrauenden Seite mithilfe des Anspruchs Regel-Assistenten eine Ausstellungs Autorisierungs Regel hinzuzufügen:

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365-for-designated-active-directory-groups"></a>So erstellen Sie eine Regel, um den gesamten externen Zugriff auf Office 365 für bestimmte Active Directory Gruppen zu blockieren



1. Klicken Sie auf Start, zeigen Sie auf Programme, zeigen Sie auf Verwaltung, und klicken Sie dann auf AD FS 2,0-Verwaltung.
2. Klicken Sie in der Konsolen Struktur unter AD FS 2.0 \ Vertrauens Stellungen auf Vertrauens Stellungen der vertrauenden Seite, klicken Sie mit der rechten Maustaste auf die Microsoft Office 365 Identity Platform-Vertrauensstellung, und klicken Sie dann auf Anspruchs Regeln bearbeiten. 
3. Wählen Sie im Dialogfeld Anspruchs Regeln bearbeiten die Registerkarte Ausstellungs Autorisierungs Regeln aus, und klicken Sie dann auf Regel hinzufügen, um den Anspruchs Regel-Assistenten zu starten.
4. Wählen Sie auf der Seite Regel Vorlage auswählen unter Anspruchs Regel Vorlage die Option Ansprüche mithilfe einer benutzerdefinierten Regel senden aus, und klicken Sie dann auf Weiter.
5. Geben Sie auf der Seite Regel konfigurieren unter Anspruchs Regel Name den anzeigen Amen für diese Regel ein. Geben Sie unter benutzerdefinierte Regel die folgende Syntax der Anspruchs Regel Sprache ein, oder fügen Sie Sie ein: `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    exists([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "Group SID value of allowed AD group"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. Klicken Sie auf Fertigstellen. Vergewissern Sie sich, dass die neue Regel direkt unterhalb der Regel Zugriff auf alle Benutzer zulassen in der Liste Ausstellungs Autorisierungs Regeln angezeigt wird.
7. Um die Regel zu speichern, klicken Sie im Dialogfeld Anspruchs Regeln bearbeiten auf OK.


### <a name="descriptions-of-the-claim-rule-language-syntax-used-in-the-above-scenarios"></a>Beschreibungen der in den obigen Szenarien verwendeten Syntax der Anspruchs Regel Sprache

|                                                                                                   Beschreibung                                                                                                   |                                                                     Syntax der Anspruchs Regel Sprache                                                                     |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              Standard AD FS Regel, um den Zugriff auf alle Benutzer zuzulassen. Diese Regel sollte bereits in der Liste der Autorisierungs Regeln für die Vertrauensstellung der vertrauenden Seite der Microsoft Office 365-Identitäts Plattform vorhanden sein              |                                  = > Problem (Type = "<https://schemas.microsoft.com/authorization/claims/permit>", Value = "true");                                   |
|                               Das Hinzufügen dieser Klausel zu einer neuen, benutzerdefinierten Regel gibt an, dass die Anforderung vom Verbund Server Proxy stammt (d. h., Sie verfügt über den Header x-ms-Proxy).                                |                                                                                                                                                                    |
|                                                                                 Es wird empfohlen, dass alle Regeln dies einschließen.                                                                                  |                                    vorhanden ([Type = = "<https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy>"])                                    |
|                                                         Wird verwendet, um festzulegen, dass die Anforderung von einem Client mit einer IP-Adresse im definierten zulässigen Bereich erfolgt.                                                         | Nicht vorhanden ([Type = = "<https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip>", Value = ~ "vom Kunden bereitgestellte öffentliche IP-Adresse-Regex"]) |
|                                    Diese Klausel wird verwendet, um anzugeben, dass die Anforderung verweigert werden soll, wenn die Anwendung, auf die zugegriffen wird, nicht Microsoft. Exchange. ActiveSync ist.                                     |       Nicht vorhanden ([Type = = "<https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application>", Value = = "Microsoft. Exchange. ActiveSync"])        |
|                                                      Mit dieser Regel können Sie feststellen, ob der-Befehl über einen Webbrowser erfolgte und nicht verweigert wird.                                                      |              Nicht vorhanden ([Type = = "<https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path>", Value = = "/ADFS/ls/"])               |
| Diese Regel gibt an, dass nur die Benutzer in einer bestimmten Active Directory Gruppe (basierend auf dem SID-Wert) verweigert werden sollen. Wenn Sie diese Anweisung nicht hinzufügen, bedeutet dies, dass eine Gruppe von Benutzern unabhängig vom Standort zugelassen wird. |             vorhanden ([Type = = "<https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid>", Value = ~ "{Group sid value of allowed Ad Group}"])              |
|                                                                Dies ist eine erforderliche Klausel, um eine DENY-Anweisung auszugeben, wenn alle vorangehenden Bedingungen erfüllt sind.                                                                 |                                   = > Problem (Type = "<https://schemas.microsoft.com/authorization/claims/deny>", Value = "true");                                    |

### <a name="building-the-ip-address-range-expression"></a>Der Ausdruck für den IP-Adressbereich wird aufgebaut

Der "x-ms-weitergeleitete Client-IP"-Anspruch wird mit einem HTTP-Header aufgefüllt, der zurzeit nur von Exchange Online festgelegt ist. dieser Wert füllt den Header auf, wenn die Authentifizierungsanforderung an AD FS übergeben wird. Der Wert des Anspruchs kann eines der folgenden sein:

>[!Note] 
>Exchange Online unterstützt derzeit nur IPv4-und nicht IPv6-Adressen.

Eine einzelne IP-Adresse: die IP-Adresse des Clients, der direkt mit Exchange Online verbunden ist

>[!Note] 
>Die IP-Adresse eines Clients im Unternehmensnetzwerk wird als IP-Adresse der externen Schnittstelle des ausgehenden Proxys oder Gateways der Organisation angezeigt.

Clients, die über ein VPN oder Microsoft DirectAccess (da) mit dem Unternehmensnetzwerk verbunden sind, werden je nach Konfiguration von VPN oder da möglicherweise als interne Unternehmens Clients oder als externe Clients angezeigt.

Mindestens eine IP-Adresse: Wenn Exchange Online die IP-Adresse des Clients, der die Verbindung herstellt, nicht ermitteln kann, wird der Wert basierend auf dem Wert des x-weitergeleiteten für-Headers festgelegt, einem nicht standardmäßigen Header, der in http-basierten Anforderungen eingeschlossen werden kann und von vielen unterstützt wird. Clients, Lasten Ausgleichs Module und Proxys auf dem Markt.

>[!Note]
>Mehrere IP-Adressen, die die Client-IP-Adresse und die Adresse der einzelnen Proxys angeben, die die Anforderung übermittelt haben, werden durch Kommas getrennt.

IP-Adressen im Zusammenhang mit der Exchange Online-Infrastruktur werden nicht in der Liste angezeigt.


#### <a name="regular-expressions"></a>Reguläre Ausdrücke

Wenn Sie einen Bereich von IP-Adressen zuordnen müssen, ist es erforderlich, einen regulären Ausdruck zu erstellen, um den Vergleich durchzuführen. In der nächsten Reihe von Schritten werden Beispiele für das Erstellen eines solchen Ausdrucks für die folgenden Adressbereiche bereitgestellt (Beachten Sie, dass Sie diese Beispiele entsprechend Ihrem öffentlichen IP-Adressbereich ändern müssen):


- 192.168.1.1 – 192.168.1.25
- 10.0.0.1 – 10.0.0.14

Zuerst lautet das grundlegende Muster, das einer einzelnen IP-Adresse entspricht, wie folgt: \b # # #\.###\.###\.# # # \b

Durch die Erweiterung können wir zwei unterschiedliche IP-Adressen wie folgt mit einem or-Ausdruck vergleichen: \b # # #\.###\.###\.# # # \b | \b # # #\.###\.###\.# # # \b

Ein Beispiel für die Anpassung von nur zwei Adressen (z. b. 192.168.1.1 oder 10.0.0.1) lautet: \b192\.168\.1\.1 \ b | \b10\.0\.0\.1 \ b

Auf diese Weise können Sie eine beliebige Anzahl von Adressen eingeben. Wenn ein Adressbereich zulässig sein muss, z. b. 192.168.1.1 – 192.168.1.25, muss der Abgleich Zeichen nach Zeichen durchgeführt werden: \b192\.168\.1\.([1-9] | 1 [0-9] | 2 [0-5]) \b

>[!Note] 
>Die IP-Adresse wird als Zeichenfolge und nicht als Zahl behandelt.


Die Regel wird wie folgt aufgeschlüsselt: \b192\.168\.1\.

Dies entspricht einem beliebigen Wert, der mit 192.168.1 beginnt.

Folgendes entspricht den Bereichen, die für den Teil der Adresse nach dem letzten Dezimaltrennzeichen erforderlich sind:


- ([1-9] entspricht Adressen, die auf 1-9 enden
- | 1 [0-9] entspricht Adressen, die in 10-19 enden
- | 2 [0-5]) entspricht Adressen, die auf 20-25 enden

>[!Note]
>Die Klammern müssen ordnungsgemäß positioniert werden, damit Sie nicht mit anderen Teilen von IP-Adressen übereinstimmen.

Wenn der 192-Block übereinstimmt, können wir einen ähnlichen Ausdruck für den 10-Block schreiben: \b10\.0\.0\.([1-9] | 1 [0-4]) \b

Und der folgende Ausdruck sollte mit allen Adressen für "192.168.1.1 ~ 25" und "10.0.0.1 ~ 14": \b192\.168\.1\.([1-9] | 1 [0-9] | 2 [0-5]) \b | \b10\.0\.0\.([1-9] | 1 [0-4]) \b verglichen werden.

#### <a name="testing-the-expression"></a>Testen des Ausdrucks

Regex-Ausdrücke können recht kompliziert werden, daher wird dringend empfohlen, ein Regex-Überprüfungs Tool zu verwenden. Wenn Sie eine Internetsuche nach "Online-Regex Expression Builder" durchführen, finden Sie mehrere gute Online Dienstprogramme, mit denen Sie Ihre Ausdrücke anhand von Beispiel Daten ausprobieren können.

Beim Testen des Ausdrucks ist es wichtig, dass Sie wissen, was zu erwarten ist. Das Exchange Online-System sendet möglicherweise viele IP-Adressen, die durch Kommas getrennt sind. Der oben angegebene Ausdruck funktioniert für dieses. Dies ist jedoch wichtig, wenn Sie die Regex-Ausdrücke testen. Beispielsweise kann eine der folgenden Beispiel Eingaben verwendet werden, um die obigen Beispiele zu überprüfen: 

192.168.1.1, 192.168.1.2, 192.169.1.1. 192.168.12.1, 192.168.1.10, 192.168.1.25, 192.168.1.26, 192.168.1.30, 1192.168.1.20 

10.0.0.1, 10.0.0.5, 10.0.0.10, 10.0.1.0, 10.0.1.1, 110.0.0.1, 10.0.0.14, 10.0.0.15, 10.0.0.10, 10, 0.0.1 











## <a name="validating-the-deployment"></a>Überprüfen der Bereitstellung

### <a name="security-audit-logs"></a>Sicherheits Überwachungs Protokolle

Aktivieren Sie die Überwachungs Protokollierung auf dem AD FS Server, um zu überprüfen, ob die neuen Anforderungs Kontext Ansprüche gesendet werden und für die AD FS Anspruchs Verarbeitungs Pipeline verfügbar sind. Senden Sie dann einige Authentifizierungsanforderungen, und überprüfen Sie die Anspruchs Werte in den standardmäßigen Sicherheits Überwachungs Protokoll-Einträgen. 

Um die Protokollierung von Überwachungs Ereignissen im Sicherheitsprotokoll auf einem AD FS Server zu aktivieren, führen Sie die Schritte unter Konfigurieren der Überwachung für AD FS 2,0 aus.

### <a name="event-logging"></a>Ereignisprotokollierung

Standardmäßig werden fehlgeschlagene Anforderungen im Anwendungs Ereignisprotokoll unter Anwendungs-und Dienst Protokolle \ AD FS 2,0 \ admin protokolliert. Weitere Informationen zur Ereignisprotokollierung für AD FS finden [Sie unter Einrichten der AD FS 2,0-Ereignisprotokollierung](https://technet.microsoft.com/library/adfs2-troubleshooting-configuring-computers.aspx).

### <a name="configuring-verbose-ad-fs-tracing-logs"></a>Konfigurieren von ausführlichen AD FS Ablauf Verfolgungs Protokollen

AD FS Ablauf Verfolgungs Ereignisse werden im Debugprotokoll AD FS 2,0 protokolliert. Informationen zum Aktivieren der Ablauf Verfolgung finden Sie unter [configure Debug Tracing for AD FS 2,0](https://technet.microsoft.com/library/adfs2-troubleshooting-configuring-computers.aspx).

Nachdem Sie die Ablauf Verfolgung aktiviert haben, verwenden Sie die folgende Befehlszeilen Syntax, um den ausführlichen Protokolliergrad zu aktivieren: wevtutil. exe SL "AD FS 2,0 Tracing/Debug"/l: 5  

## <a name="related"></a>Verwandte Themen
Weitere Informationen zu den neuen Anspruchs Typen finden Sie unter [AD FS Anspruchs Typen](AD-FS-Claims-Types.md).

