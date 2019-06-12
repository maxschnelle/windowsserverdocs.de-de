---
ms.assetid: ''
title: Client Access Control-Richtlinien in Active Directory-Verbunddienste 2.0
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 036d6d0543687e7f82caf3dfd2c3bb0b4a981181
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445049"
---
# <a name="client-access-control-policies-in-ad-fs-20"></a>Client-Zugriffssteuerungsrichtlinien in AD FS 2.0
Eine Client-Zugriffsrichtlinien in Active Directory-Verbunddienste 2.0 können Sie einschränken oder gewähren Benutzerzugriff auf Ressourcen.  Dieses Dokument beschreibt, wie Sie Clientzugriffsrichtlinien in AD FS 2.0 zu aktivieren und konfigurieren Sie die häufigsten Szenarien.

## <a name="enabling-client-access-policy-in-ad-fs-20"></a>Aktivieren die Clientzugriffsrichtlinie in AD FS 2.0

Um Clientzugriffsrichtlinie zu aktivieren, führen Sie die folgenden Schritte aus.

### <a name="step-1-install-the-update-rollup-2-for-ad-fs-20-package-on-your-ad-fs-servers"></a>Schritt 1: Installieren Sie das Updaterollup 2 für AD FS 2.0-Paket auf Ihrem AD FS-Server

Herunterladen der [Updaterollup 2 für Active Directory-Verbunddienste (AD FS) 2.0](https://support.microsoft.com/en-us/help/2681584/description-of-update-rollup-2-for-active-directory-federation-services-ad-fs-2.0) Packen und installieren Sie es für alle Verbundserver und Verbundserverproxys bestimmen.

### <a name="step-2-add-five-claim-rules-to-the-active-directory-claims-provider-trust"></a>Schritt 2: Fügen Sie, dass fünf Anspruchsregeln der Active Directory-Anspruchsanbieter-Vertrauensstellung hinzu.

Nach Updaterollup 2 für alle Proxys und AD FS-Server installiert wurde, verwenden Sie wie folgt vor, um einen Satz von Anspruchsregeln hinzufügen, der die neue Anspruchstypen aufdecken der Richtlinien-Engine zur Verfügung stellt.

Zu diesem Zweck werden Sie fünf akzeptanztransformationsregeln für jede neue Anforderung Kontext Anspruchstypen mithilfe des folgenden Verfahrens hinzugefügt.

Erstellen Sie auf die Active Directory Anspruchsanbieter-Vertrauensstellung eine neue Regel der Zustimmung zur Transformation zu durchlaufen, jede neue Anforderung Kontext Anspruchstypen.

#### <a name="to-add-a-claim-rule-to-the-active-directory-claims-provider-trust-for-each-of-the-five-context-claim-types"></a>Zum Hinzufügen der Anspruchsregel in Active Directory-Anspruchsanbieter-Vertrauensstellung für jede der fünf Kontext Anspruchstypen:


1. Klicken Sie auf Start, zeigen Sie auf Programme, zeigen Sie auf Verwaltung und klicken Sie dann auf AD FS 2.0-Verwaltung.
2. Klicken Sie in der Konsolenstruktur unter AD 2 FS. 0\vertrauensstellungen auf die Anspruchsanbieter-Vertrauensstellungen, mit der rechten Maustaste in Active Directory, und klicken Sie dann auf Anspruchsregeln bearbeiten.
3. Klicken Sie im Dialogfeld "Anspruchsregeln bearbeiten" Wählen Sie der Registerkarte "Akzeptanztransformationsregeln aus", und klicken Sie dann auf Regel hinzufügen, um die Regel-Assistenten zu starten.
4. Wählen Sie auf der Seite Regelvorlage auswählen unter anspruchsregelvorlage Pass-Through oder Filtern eines eingehenden Anspruchs in der Liste, und klicken Sie dann auf Weiter.
5. Geben Sie auf der Seite Regel konfigurieren unter Name der Anspruchsregel den Anzeigenamen für diese Regel; in eingehenden Anspruchstyp, geben Sie den folgenden Anspruch-Typ-URL, und wählen Sie dann alle Anspruchswerte übergeben.</br>
        `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`</br>
6. Um die Regel zu überprüfen, wählen sie in der Liste, und klicken Sie auf die Regel bearbeiten, und klicken Sie dann Regelsprache anzeigen. Die anspruchsregelsprache sollte wie folgt aussehen: `c:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip"] => issue(claim = c);`
7. Klicken Sie auf "Fertig stellen".
8. Klicken Sie auf OK, um die Regeln zu speichern, klicken Sie im Dialogfeld "Anspruchsregeln bearbeiten".
9. Wiederholen Sie Schritte 2 bis 6, um das Erstellen einer zusätzlichen Anspruchsregel für jede der verbleibenden vier Anspruchstypen unten, bis alle fünf Regeln erstellt wurden.

    `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`


~~~
`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`

`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`

`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`
~~~

### <a name="step-3-update-the-microsoft-office-365-identity-platform-relying-party-trust"></a>Schritt 3: Aktualisieren Sie die Microsoft Office 365 Identity Platform, die Vertrauensstellung einer vertrauenden Seite

Wählen Sie eine der in den Beispielszenarien unten, um die Anspruchsregeln für die Microsoft Office 365 Identity Platform, die die Anforderungen Ihrer Organisation am besten Vertrauensstellung einer vertrauenden Seite konfigurieren.

## <a name="client-access-policy-scenarios-for-ad-fs-20"></a>Client Access-Richtlinie-Szenarien für AD FS 2.0
In den folgenden Abschnitten werden die Szenarien beschreiben, die für AD FS 2.0 vorhanden sind.

### <a name="scenario-1-block-all-external-access-to-office-365"></a>Szenario 1: Blockieren des gesamten externen Zugriff auf Office 365

Diese Szenarios Client für den Zugriff ermöglicht Zugriff auf alle internen Clients und blockiert alle externen Clients, die basierend auf der IP-Adresse des externen Clients. Der Regelsatz erstellt für die Ausstellungsautorisierung Standardregel allen Benutzern Zugriff zulassen. Sie können das folgende Verfahren verwenden, eine Ausstellungsautorisierung-Regel für die Office 365-Vertrauensstellung einer vertrauenden Seite hinzufügen.

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365"></a>Zum Erstellen einer Regel zum Blockieren des gesamten externen Zugriff auf Office 365



1. Klicken Sie auf Start, zeigen Sie auf Programme, zeigen Sie auf Verwaltung und klicken Sie dann auf AD FS 2.0-Verwaltung.
2. Klicken Sie in der Konsolenstruktur unter AD 2 FS. 0\vertrauensstellungen auf die Vertrauensstellungen für vertrauende Seiten, mit der rechten Maustaste in der Microsoft Office 365 Identity Platform-Vertrauensstellung, und klicken Sie dann auf Anspruchsregeln bearbeiten. 
3. Klicken Sie im Dialogfeld "Anspruchsregeln bearbeiten" Wählen Sie der Registerkarte "Ausstellungsautorisierungsregeln aus", und klicken Sie dann auf Regel hinzufügen, um den Anspruch-Regel-Assistenten zu starten.
4. Klicken Sie auf der Seite Regelvorlage auswählen unter anspruchsregelvorlage wählen Sie senden Ansprüche per benutzerdefinierter Regel, und klicken Sie dann auf Weiter.
5. Geben Sie auf der Seite Regel konfigurieren unter Name der Anspruchsregel den Anzeigenamen für diese Regel aus. Geben Sie unter benutzerdefinierte Regel einen Wert ein, oder fügen Sie die folgende Anspruchsregel-Sprachsyntax: `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");` 
6. Klicken Sie auf "Fertig stellen". Stellen Sie sicher, dass die neue Regel unmittelbar unterhalb der Zugriff auf alle Benutzer der Regel in der Liste der Regeln für Ausstellungsautorisierung angezeigt wird.
7. Um die Regel ein, in das Dialogfeld "Anspruchsregeln bearbeiten" zu speichern, klicken Sie auf "OK".

>[!NOTE]
>Sie müssen den Wert oben für "öffentliche IP-Adresse Regex" mit einem gültigen IP-Ausdruck zu ersetzen; finden Sie unter der IP-Adressbereich Ausdruck Weitere Informationen zu erstellen.


### <a name="scenario-2-block-all-external-access-to-office-365-except-exchange-activesync"></a>Szenario 2: Blockieren des gesamten externen Zugriff auf Office 365 mit Ausnahme von Exchange ActiveSync

Im folgende Beispiel ermöglicht den Zugriff auf alle Office 365-Anwendungen, einschließlich von internen Clients, einschließlich Outlook Exchange Online. Blockiert den Zugriff von Clients, die sich außerhalb des Unternehmensnetzwerks befinden, wie durch die Client IP-Adresse, mit Ausnahme von Exchange ActiveSync-Clients wie z. B. Smartphones. Der Regelsatz erstellt für die Ausstellungsautorisierung-Standardregel, die mit dem Titel ermöglichen allen Benutzern Zugriff gewähren. Verwenden Sie die folgenden Schritte aus, um eine Regel für die Ausstellungsautorisierung Office 365 mit dem Assistenten zum Vertrauensstellung einer vertrauenden Seite hinzufügen:

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365"></a>Zum Erstellen einer Regel zum Blockieren des gesamten externen Zugriff auf Office 365



1. Klicken Sie auf Start, zeigen Sie auf Programme, zeigen Sie auf Verwaltung und klicken Sie dann auf AD FS 2.0-Verwaltung.
2. Klicken Sie in der Konsolenstruktur unter AD 2 FS. 0\vertrauensstellungen auf die Vertrauensstellungen für vertrauende Seiten, mit der rechten Maustaste in der Microsoft Office 365 Identity Platform-Vertrauensstellung, und klicken Sie dann auf Anspruchsregeln bearbeiten. 
3. Klicken Sie im Dialogfeld "Anspruchsregeln bearbeiten" Wählen Sie der Registerkarte "Ausstellungsautorisierungsregeln aus", und klicken Sie dann auf Regel hinzufügen, um den Anspruch-Regel-Assistenten zu starten.
4. Klicken Sie auf der Seite Regelvorlage auswählen unter anspruchsregelvorlage wählen Sie senden Ansprüche per benutzerdefinierter Regel, und klicken Sie dann auf Weiter.
5. Geben Sie auf der Seite Regel konfigurieren unter Name der Anspruchsregel den Anzeigenamen für diese Regel aus. Geben Sie unter benutzerdefinierte Regel einen Wert ein, oder fügen Sie die folgende Anspruchsregel-Sprachsyntax: `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application",
    Value=="Microsoft.Exchange.Autodiscover"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application",
    Value=="Microsoft.Exchange.ActiveSync"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. Klicken Sie auf "Fertig stellen". Stellen Sie sicher, dass die neue Regel unmittelbar unterhalb der Zugriff auf alle Benutzer der Regel in der Liste der Regeln für Ausstellungsautorisierung angezeigt wird.
7. Um die Regel ein, in das Dialogfeld "Anspruchsregeln bearbeiten" zu speichern, klicken Sie auf "OK".

>[!NOTE]
>Sie müssen den Wert oben für "öffentliche IP-Adresse Regex" mit einem gültigen IP-Ausdruck zu ersetzen; finden Sie unter der IP-Adressbereich Ausdruck Weitere Informationen zu erstellen.

### <a name="scenario-3-block-all-external-access-to-office-365-except-browser-based-applications"></a>Szenario 3: Blockieren des gesamten externen Zugriff auf Office 365 außer durch browserbasierte Anwendungen

Der Regelsatz erstellt für die Ausstellungsautorisierung-Standardregel, die mit dem Titel ermöglichen allen Benutzern Zugriff gewähren. Verwenden Sie die folgenden Schritte aus, um eine Regel für die Ausstellungsautorisierung auf der Microsoft Office 365 Identity Platform, die mit dem Assistenten zum Vertrauensstellung einer vertrauenden Seite hinzufügen:

>[!NOTE]
>Dieses Szenario wird durch einen Drittanbieter-Proxy nicht aufgrund der Client Access-Richtlinie-Header mit Anforderungen für den passiven (webbasiert) unterstützt.

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365-except-browser-based-applications"></a>Zum Erstellen einer Regel zum Blockieren des gesamten externen Zugriff auf Office 365 außer durch browserbasierte Anwendungen



1. Klicken Sie auf Start, zeigen Sie auf Programme, zeigen Sie auf Verwaltung und klicken Sie dann auf AD FS 2.0-Verwaltung.
2. Klicken Sie in der Konsolenstruktur unter AD 2 FS. 0\vertrauensstellungen auf die Vertrauensstellungen für vertrauende Seiten, mit der rechten Maustaste in der Microsoft Office 365 Identity Platform-Vertrauensstellung, und klicken Sie dann auf Anspruchsregeln bearbeiten. 
3. Klicken Sie im Dialogfeld "Anspruchsregeln bearbeiten" Wählen Sie der Registerkarte "Ausstellungsautorisierungsregeln aus", und klicken Sie dann auf Regel hinzufügen, um den Anspruch-Regel-Assistenten zu starten.
4. Klicken Sie auf der Seite Regelvorlage auswählen unter anspruchsregelvorlage wählen Sie senden Ansprüche per benutzerdefinierter Regel, und klicken Sie dann auf Weiter.
5. Geben Sie auf der Seite Regel konfigurieren unter Name der Anspruchsregel den Anzeigenamen für diese Regel aus. Geben Sie unter benutzerdefinierte Regel einen Wert ein, oder fügen Sie die folgende Anspruchsregel-Sprachsyntax: `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value == "/adfs/ls/"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. Klicken Sie auf "Fertig stellen". Stellen Sie sicher, dass die neue Regel unmittelbar unterhalb der Zugriff auf alle Benutzer der Regel in der Liste der Regeln für Ausstellungsautorisierung angezeigt wird.
7. Um die Regel ein, in das Dialogfeld "Anspruchsregeln bearbeiten" zu speichern, klicken Sie auf "OK".

### <a name="scenario-4-block-all-external-access-to-office-365-for-designated-active-directory-groups"></a>Szenario 4: Blockieren des gesamten externen Zugriff auf Office 365 für die angegebenen Active Directory-Gruppen

Im folgenden Beispiel wird der Zugriff von internen Clients basierend auf IP-Adresse. Blockiert den Zugriff von Clients, die sich außerhalb des Unternehmensnetzwerks befinden, die eine externen Client-IP-Adresse verfügen, mit Ausnahme der Personen in einer angegebenen Regel für die Active Directory-domänennamenspräfix basiert die Gruppe die Ausstellungsautorisierung-Standardregel, die mit dem Titel Zugriff gewähren Alle Benutzer. Verwenden Sie die folgenden Schritte aus, um eine Regel für die Ausstellungsautorisierung auf der Microsoft Office 365 Identity Platform, die mit dem Assistenten zum Vertrauensstellung einer vertrauenden Seite hinzufügen:

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365-for-designated-active-directory-groups"></a>Zum Erstellen einer Regel zum Blockieren des gesamten externen Zugriff auf Office 365 für die angegebenen Active Directory-Gruppen



1. Klicken Sie auf Start, zeigen Sie auf Programme, zeigen Sie auf Verwaltung und klicken Sie dann auf AD FS 2.0-Verwaltung.
2. Klicken Sie in der Konsolenstruktur unter AD 2 FS. 0\vertrauensstellungen auf die Vertrauensstellungen für vertrauende Seiten, mit der rechten Maustaste in der Microsoft Office 365 Identity Platform-Vertrauensstellung, und klicken Sie dann auf Anspruchsregeln bearbeiten. 
3. Klicken Sie im Dialogfeld "Anspruchsregeln bearbeiten" Wählen Sie der Registerkarte "Ausstellungsautorisierungsregeln aus", und klicken Sie dann auf Regel hinzufügen, um den Anspruch-Regel-Assistenten zu starten.
4. Klicken Sie auf der Seite Regelvorlage auswählen unter anspruchsregelvorlage wählen Sie senden Ansprüche per benutzerdefinierter Regel, und klicken Sie dann auf Weiter.
5. Geben Sie auf der Seite Regel konfigurieren unter Name der Anspruchsregel den Anzeigenamen für diese Regel aus. Geben Sie unter benutzerdefinierte Regel einen Wert ein, oder fügen Sie die folgende Anspruchsregel-Sprachsyntax: `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    exists([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "Group SID value of allowed AD group"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. Klicken Sie auf "Fertig stellen". Stellen Sie sicher, dass die neue Regel unmittelbar unterhalb der Zugriff auf alle Benutzer der Regel in der Liste der Regeln für Ausstellungsautorisierung angezeigt wird.
7. Um die Regel ein, in das Dialogfeld "Anspruchsregeln bearbeiten" zu speichern, klicken Sie auf "OK".


### <a name="descriptions-of-the-claim-rule-language-syntax-used-in-the-above-scenarios"></a>Beschreibungen der Anspruchsregel-Sprachsyntax, die in den oben genannten Szenarien verwendet

|                                                                                                   Beschreibung                                                                                                   |                                                                     Anspruch der syntax                                                                     |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              Standardmäßige AD FS-Regel zum Zulassen des Zugriffs auf alle Benutzer. Diese Regel sollte bereits in der Microsoft Office 365 Identity Platform, die Liste der Regeln für Ausstellungsautorisierung Vertrauensstellung einer vertrauenden Seite vorhanden sein.              |                                  => issue(Type = "<https://schemas.microsoft.com/authorization/claims/permit>", Value = "true");                                   |
|                               Diese Klausel hinzufügen, um eine neue, benutzerdefinierte Regel gibt an, dass die Anforderung aus dem Verbundserverproxy herauskommt (d. h. sie hat den Header X-ms-Proxy)                                |                                                                                                                                                                    |
|                                                                                 Es wird empfohlen, dass alle Regeln, die diese enthalten.                                                                                  |                                    exists([Type == "<https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy>"])                                    |
|                                                         Verwendet, um die ermittelt, ob die Anforderung von einem Client mit einer IP-Adresse im akzeptierten Bereich definiert ist.                                                         | NOT exists([Type == "<https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip>", Value=~"customer-provided public ip address regex"]) |
|                                    Diese Klausel wird verwendet, um anzugeben, dass wenn die Anwendung auf die zugegriffen wird, nicht Microsoft.Exchange.ActiveSync ist die Anforderung abgelehnt werden soll.                                     |       NOT exists([Type == "<https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application>", Value=="Microsoft.Exchange.ActiveSync"])        |
|                                                      Mit dieser Regel können Sie bestimmen, ob der Aufruf über einen Webbrowser wurde, und nicht verweigert werden.                                                      |              NOT exists([Type == "<https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path>", Value == "/adfs/ls/"])               |
| Diese Regel gibt an, dass die einzigen Benutzer in einer bestimmten Active Directory-Gruppe (auf der Grundlage der SID-Wert) verweigert werden soll. Diese Anweisung nicht hinzugefügt, bedeutet, dass es sich bei eine Gruppe von Benutzern, unabhängig von Ihrem Standort möglich ist. |             vorhanden ist ([Type == "<https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid>", Wert = ~ "{Gruppe SID-Wert, der zulässigen Gruppe" AD "}"])              |
|                                                                Dies ist eine erforderliche Klausel Deny ausgeben, wenn alle oben genannten Bedingungen erfüllt sind.                                                                 |                                   => issue(Type = "<https://schemas.microsoft.com/authorization/claims/deny>", Value = "true");                                    |

### <a name="building-the-ip-address-range-expression"></a>Erstellen die IP-Adresse-Range-Ausdruck

Der X-ms-forwarded-Client-Ip-Anspruch wird von einem HTTP-Header aufgefüllt, die derzeit nur von Exchange Online, die den Header aufgefüllt wird festgelegt ist, wenn die Authentifizierungsanforderung an AD FS übergeben. Der Wert des Anspruchs kann es sich um eine der folgenden sein:

>[!Note] 
>Exchange Online unterstützt derzeit nur für IPV4- und nicht auf IPV6-Adressen.

Eine einzelne IP-Adresse: Die IP-Adresse des Clients, die direkt mit Exchange Online verbunden ist

>[!Note] 
>Die IP-Adresse eines Clients im Unternehmensnetzwerk wird als der externe IP-Adresse des Proxys für ausgehenden Datenverkehr der Organisation oder Gateways angezeigt.

Clients, die mit dem Unternehmensnetzwerk, indem Sie ein VPN oder von Microsoft DirectAccess (DA verbunden sind) möglicherweise als internen Unternehmenskunden oder als externe Clients, die je nach Konfiguration des VPN-Verbindung oder da auszulagern.

Eine oder mehrere IP-Adressen: Wenn Sie Exchange Online die IP-Adresse der verbindende Client nicht ermitteln kann, wird es legen Sie den Wert basierend auf den Wert der X-forwarded-for-Header, eine nicht standardmäßige Headerdateien, die in der HTTP-basierten Anforderungen enthalten sein kann und wird von vielen Clients, Load balancer unterstützt, und -Proxys auf dem Markt.

>[!Note]
>Mehrere IP-Adressen, der angibt, die Client-IP-Adresse und die Adresse für jeden Proxy, der die Anforderung zu übergeben, werden durch ein Komma getrennt werden.

IP-Adressen, die im Zusammenhang mit Exchange Online-Infrastruktur werden nicht in der Liste angezeigt.


#### <a name="regular-expressions"></a>Reguläre Ausdrücke

Wenn Sie einen Bereich von IP-Adressen übereinstimmen müssen, ist es notwendig, einen regulären Ausdruck zum Ausführen des Vergleichs zu erstellen. In den nächsten Schritten bieten wir Beispiele dafür, wie ein solcher Ausdruck entsprechend die folgenden Adressbereiche (Beachten Sie, dass Sie werden so ändern Sie diesen Beispielen entsprechend Ihrer öffentlichen IP-Adressbereich) erstellen:


- 192.168.1.1 – 192.168.1.25
- 10.0.0.1 – 10.0.0.14

Erstens ist das grundlegende Muster, die eine einzelne IP-Adresse übereinstimmen, wird wie folgt: \b###\.###\.###\.### \b

Erweitern diese aus, wir können entsprechen zwei verschiedene IP-Adressen mit einem OR-Ausdruck wie folgt: \b###\.###\.###\.### \b|\b###\. ### \. ### \.### \b

Natürlich wäre ein Beispiel, das nur zwei Adressen (z.B. 192.168.1.1 oder 10.0.0.1) übereinstimmen: \b192\.168\.1\.1\b | \b10\.0\.0\.1\b

Dadurch können Sie das Verfahren, mit dem Sie eine beliebige Anzahl von Adressen eingeben können. Wo möchten Sie ein Bereich von Adresse zulässig, z. B. 192.168.1.1 – 192.168.1.25, den entsprechenden vorgenommen werden Zeichen durch Zeichen: \b192\.168\.1\.([1-9] | [0-9]-1 | 2 [0-5]) \b

>[!Note] 
>Die IP-Adresse wird als Zeichenfolge und kein Zahl behandelt.


Die Regel wird wie folgt unterteilt: \b192\.168\.1\.

Dies entspricht jeder Wert beginnt mit 192.168.1 aufweisen.

Der folgenden entspricht die Bereiche, die für den Teil der Adresse nach dem letzten Punkt erforderlich:


- ([1-9] Übereinstimmungen Adressen mit 1 bis 9
- | 1 [0-9] entspricht der Adressen mit den 10-19
- |2[0-5]) Übereinstimmungen Adressen mit den 20-25

>[!Note]
>Die Klammern müssen richtig positioniert werden, damit Sie starten nicht übereinstimmende andere Bereiche von IP-Adressen.

Mit dem 192 Block abgeglichen, Schreiben wir einen ähnlichen Ausdruck für den 10-Block: \b10\.0\.0\.([1-9] | [0-4]-1) \b

Und platzieren sie zusammen, sollte der folgende Ausdruck alle Adressen für "192.168.1.1~25" und "10.0.0.1~14" übereinstimmen: \b192\.168\.1\.([1-9] | [0-9]-1 | 2 [0-5]) \b|\b10\.0\.0\. ([1-9] | [0-4]-1) \b

#### <a name="testing-the-expression"></a>Testen den Ausdruck

Regex-Ausdrücke können recht schwierig werden, deshalb wird ausdrücklich empfohlen, mithilfe eines Tools der Regex-Überprüfung. Wenn Sie eine Internetsuche nach "online Regex-Ausdrucks-Generator" tun, finden Sie mehrere gute online-Hilfsprogramme, die Sie Ihren Ausdrücken anhand von Beispieldaten ausprobieren können.

Wenn Sie den Ausdruck zu testen, ist es wichtig, dass Sie verstehen, was Sie erwarten können, müssen übereinstimmen. Das Exchange online-System senden möglicherweise viele IP-Adressen, getrennt durch Kommas. Die oben aufgeführten Ausdrücke funktionieren für diese. Allerdings ist es wichtig, zu kümmern beim Testen Ihrer Regex-Ausdrücke. Beispielsweise kann eine im folgende Beispiel mit der Eingabe, um zu überprüfen, ob die Beispiele oben verwenden: 

192.168.1.1, 192.168.1.2, 192.169.1.1. 192.168.12.1, 192.168.1.10, 192.168.1.25, 192.168.1.26, 192.168.1.30, 1192.168.1.20 

10.0.0.1, 10.0.0.5, 10.0.0.10, 10.0.1.0, 10.0.1.1, 110.0.0.1, 10.0.0.14, 10.0.0.15, 10.0.0.10, 10,0.0.1 











## <a name="validating-the-deployment"></a>Überprüfen der Bereitstellung

### <a name="security-audit-logs"></a>Sicherheitsüberwachungsprotokollen

Um sicherzustellen, dass der neue Anforderungskontext Ansprüche gesendet werden und stehen für die AD FS--Pipeline zur anforderungsverarbeitung Anspruchsanbieter, aktivieren Sie überwachungsprotokollierung, die auf dem AD FS-Server. Senden Sie einige authentifizierungsanforderungen und die Kontrollkästchen für die Anspruchswerte werden dann in die Standardsicherheit Überwachungsprotokolleinträge. 

Um die Protokollierung, Überwachung, auf dem Ereignisse an die Sicherheit auf AD FS-Server anmelden zu aktivieren, führen Sie die Schritte unter Konfigurieren der Überwachung für AD FS 2.0 aus.

### <a name="event-logging"></a>Protokollierung von Komponentenereignissen

Fehlerhafte Anforderungen werden protokolliert standardmäßig in das Anwendungsereignisprotokoll befindet sich im Anwendungs- und Dienstprotokolle \ AD FS 2.0 \ Admin.For die Weitere Informationen zur ereignisprotokollierung für AD FS finden Sie unter [Einrichten der AD FS 2.0-ereignisprotokollierung](https://technet.microsoft.com/library/adfs2-troubleshooting-configuring-computers.aspx).

### <a name="configuring-verbose-ad-fs-tracing-logs"></a>Konfigurieren von Ablaufverfolgungsprotokollen ausführliche AD-FS

AD FS-Ablaufverfolgungsereignisse werden in das AD FS 2.0-Debugprotokoll protokolliert. Zum Aktivieren der Ablaufverfolgung finden Sie unter [Konfigurieren der Debugablaufverfolgung für AD FS 2.0](https://technet.microsoft.com/library/adfs2-troubleshooting-configuring-computers.aspx).

Nachdem Sie die Ablaufverfolgung aktiviert haben, verwenden Sie die folgende Befehlszeilensyntax zum Aktivieren der ausführlichen Protokollierungsstufe: wevtutil.exe sl "AD FS 2.0-Ablaufverfolgung/Debug" /l:5  

## <a name="related"></a>Verwandte Themen
Weitere Informationen zu den neuen Anspruchstypen finden Sie unter [Anspruchstypen für AD FS](AD-FS-Claims-Types.md).

