---
ms.assetid: 
title: Steuerung des Zugriffs Clientrichtlinien in Active Directory-Verbunddienste 2.0
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 00b9cd17c7a5c206e06bea12fd90762adb336715
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="client-access-control-policies-in-ad-fs-20"></a>Steuerung des Zugriffs Clientrichtlinien in AD FS 2.0
Ein Client-Richtlinien in Active Directory-Verbunddienste 2.0 können Sie einschränken oder gewähren des Zugriffs auf Ressourcen.  Dieses Dokument beschreibt die Vorgehensweise beim Aktivieren des Client-Richtlinien in AD FS 2.0 und die häufigsten Szenarien konfigurieren.

## <a name="enabling-client-access-policy-in-ad-fs-20"></a>Aktivieren des Client-Richtlinien in AD FS 2.0

Führen Sie die folgenden Schritte aus, um Client-Richtlinie zu aktivieren.

### <a name="step-1-install-the-update-rollup-2-for-ad-fs-20-package-on-your-ad-fs-servers"></a>Schritt 1: Installieren Sie das Updaterollup 2 für AD FS 2.0 Paket auf die AD FS-Server

Herunterladen der [Updaterollup 2 für Active Directory-Verbunddienste (AD FS) 2.0](https://support.microsoft.com/en-us/help/2681584/description-of-update-rollup-2-for-active-directory-federation-services-ad-fs-2.0) Verpacken und auf alle Verbundserver und Verbundserverproxys installieren.

### <a name="step-2-add-five-claim-rules-to-the-active-directory-claims-provider-trust"></a>Schritt 2: Hinzufügen der Active Directory-Anspruchsanbieter-Vertrauensstellung fünf Anspruchsregeln

Nach Updaterollup 2 für alle AD FS-Server und Proxys installiert wurde, verwenden Sie das folgende Verfahren zum Hinzufügen einer Gruppe von Anspruchsregeln, die die neue Anspruchstypen für das Richtlinienmodul verfügbar macht.

Zu diesem Zweck werden Sie fünf akzeptanztransformationsregeln für jede neue Anforderung Kontext Anspruch Typen mithilfe des folgenden Verfahrens hinzufügen.

Erstellen Sie auf der Active Directory-Anspruchsanbieter-Vertrauensstellung eine neue Regel der Annahme Transformation durch jede neue Anforderung Kontext Anspruch Typen übergeben.

#### <a name="to-add-a-claim-rule-to-the-active-directory-claims-provider-trust-for-each-of-the-five-context-claim-types"></a>Zum Hinzufügen einer Anspruchsregel in Active Directory-Anspruchsanbieter-Vertrauensstellung für jede der fünf Kontext Anspruchstypen:


1. Klicken Sie auf Start, zeigen Sie auf Programme, zeigen Sie auf Verwaltung, und klicken Sie dann auf AD FS 2.0-Verwaltung.
2. Klicken Sie in der Konsolenstruktur unter AD 2 FS. 0\vertrauensstellungen klicken Sie auf die Anspruchsanbieter-Vertrauensstellungen rechten Maustaste auf Active Directory, und klicken Sie dann auf Anspruchsregeln bearbeiten.
3. Wählen Sie die Registerkarte "Akzeptanztransformationsregeln", und klicken Sie dann auf Regel hinzufügen, um den Assistenten zu starten, klicken Sie im Dialogfeld "Anspruchsregeln bearbeiten".
4. Wählen Sie auf der Seite Regelvorlage auswählen unter anspruchsregelvorlage weiterleiten oder Filtern eines eingehenden Anspruchs aus der Liste, und klicken Sie dann auf Weiter.
5. Geben Sie auf der Seite Regel konfigurieren unter Name der Anspruchsregel den Anzeigenamen für diese Regel. Eingehende Anspruchstyp, geben Sie die folgende URL des Anspruchs-Typ, und wählen Sie dann alle Anspruchswerte weiterleiten Pass.</br>
        `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`</br>
6. Um die Regel zu überprüfen, wählen sie in der Liste und klicken Sie dann auf Regel bearbeiten, und klicken Sie dann Regelsprache anzeigen. Die anspruchsregelsprache sollte wie folgt aussehen: `c:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip"] => issue(claim = c);`
7. Klicken Sie auf "Fertig stellen".
8. Klicken Sie auf OK, um die Regeln zu speichern, klicken Sie im Dialogfeld "Anspruchsregeln bearbeiten".
9. Wiederholen Sie die Schritte 2 bis 6, und erstellen Sie eine zusätzliche Anspruchsregel für jede der verbleibenden vier Anspruchstypen unten, bis alle fünf Regeln erstellt wurden.

    `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`


    `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`

    `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`

    `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`

### <a name="step-3-update-the-microsoft-office-365-identity-platform-relying-party-trust"></a>Schritt 3: Aktualisieren der Microsoft Office 365-Identitätsplattform Vertrauensstellung einer vertrauenden Seite

Wählen Sie ein Szenario aus, um den Anspruchsregeln auf der Microsoft Office 365 Identitätsplattform, die die Bedürfnisse Ihrer Organisation am besten entspricht Vertrauensstellung einer vertrauenden Seite konfigurieren.

## <a name="client-access-policy-scenarios-for-ad-fs-20"></a>Client-Richtlinie Szenarien für AD FS 2.0
In den folgenden Abschnitten werden die Szenarien beschreiben, die für AD FS 2.0 vorhanden sind.

### <a name="scenario-1-block-all-external-access-to-office-365"></a>Szenario 1: Blockiert den externen Zugriff auf Office 365

Dabei Policy Client Zugriff ermöglicht den Zugriff auf alle internen Clients und blockiert alle externen Clients basierend auf der IP-Adresse des externen Clients. Der Regelsatz baut auf die Ausstellung standardmäßige Autorisierungsregel allen Benutzern Zugriff gewähren. Das folgende Verfahren können Office 365-Vertrauensstellung einer vertrauenden Seite eine Ausstellung Autorisierungsregel hinzu.

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365"></a>Erstellen Sie eine Regel zum Blockieren von externen Zugriff auf Office 365



1. Klicken Sie auf Start, zeigen Sie auf Programme, zeigen Sie auf Verwaltung, und klicken Sie dann auf AD FS 2.0-Verwaltung.
2. Klicken Sie in der Konsolenstruktur unter AD 2 FS. 0\vertrauensstellungen auf die Vertrauensstellungen der vertrauenden Seite, mit der rechten Maustaste in der Microsoft Office 365-Identitätsplattform Vertrauensstellung, und klicken Sie dann auf Anspruchsregeln bearbeiten. 
3. Wählen Sie die Registerkarte "Ausstellungsautorisierungsregeln", und klicken Sie dann auf Regel hinzufügen, um den Anspruch Regel-Assistenten zu starten, klicken Sie im Dialogfeld "Anspruchsregeln bearbeiten".
4. Klicken Sie auf der Seite Regelvorlage auswählen unter anspruchsregelvorlage senden Ansprüchen mit benutzerdefinierter Regel wählen Sie aus, und klicken Sie dann auf Weiter.
5. Geben Sie auf der Seite Regel konfigurieren unter Name der Anspruchsregel den Anzeigenamen für diese Regel. Geben Sie unter benutzerdefinierte Regel einen Wert ein, oder fügen Sie die folgende Syntax anspruchsregelsprache: `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");` 
6. Klicken Sie auf "Fertig stellen". Stellen Sie sicher, dass die neue Regel wird direkt unter den Zugriff erlauben, auf alle Benutzer in der Liste von Ausstellungsautorisierungsregeln angezeigt.
7. Klicken Sie auf "OK", um die Regel im Dialogfeld "Anspruchsregeln bearbeiten" zu speichern.

>[!NOTE]
>Sie ist den Wert für "öffentliche IP-Adresse Regex" oben in eine gültige IP-Ausdruck zu ersetzen. finden Sie unter der IP-Adressbereich Ausdruck für Weitere Informationen zu erstellen.


### <a name="scenario-2-block-all-external-access-to-office-365-except-exchange-activesync"></a>Szenario 2: Blockiert den externen Zugriff auf Office 365 mit Ausnahme von Exchange ActiveSync

Im folgende Beispiel ermöglicht den Zugriff auf alle Office 365-Anwendungen wie Exchange Online von internen Clients wie Outlook. Es blockiert den Zugriff von Clients, die sich außerhalb des Unternehmensnetzwerks befinden wie die IP-Adresse von Clients, mit Ausnahme von Exchange ActiveSync-Clients, z. B. Smartphones angegeben. Der Regelsatz baut auf Standard Ausstellung Autorisierungsregel, die mit dem Titel allen Benutzern Zugriff gewähren. Verwenden Sie die folgenden Schritte aus, um eine Ausstellung Autorisierungsregel mit dem Office 365 mit dem Assistenten für Anspruch Vertrauensstellung einer vertrauenden Seite hinzufügen:

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365"></a>Erstellen Sie eine Regel zum Blockieren von externen Zugriff auf Office 365



1. Klicken Sie auf Start, zeigen Sie auf Programme, zeigen Sie auf Verwaltung, und klicken Sie dann auf AD FS 2.0-Verwaltung.
2. Klicken Sie in der Konsolenstruktur unter AD 2 FS. 0\vertrauensstellungen auf die Vertrauensstellungen der vertrauenden Seite, mit der rechten Maustaste in der Microsoft Office 365-Identitätsplattform Vertrauensstellung, und klicken Sie dann auf Anspruchsregeln bearbeiten. 
3. Wählen Sie die Registerkarte "Ausstellungsautorisierungsregeln", und klicken Sie dann auf Regel hinzufügen, um den Anspruch Regel-Assistenten zu starten, klicken Sie im Dialogfeld "Anspruchsregeln bearbeiten".
4. Klicken Sie auf der Seite Regelvorlage auswählen unter anspruchsregelvorlage senden Ansprüchen mit benutzerdefinierter Regel wählen Sie aus, und klicken Sie dann auf Weiter.
5. Geben Sie auf der Seite Regel konfigurieren unter Name der Anspruchsregel den Anzeigenamen für diese Regel. Geben Sie unter benutzerdefinierte Regel einen Wert ein, oder fügen Sie die folgende Syntax anspruchsregelsprache: `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application",
    Value=="Microsoft.Exchange.Autodiscover"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application",
    Value=="Microsoft.Exchange.ActiveSync"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. Klicken Sie auf "Fertig stellen". Stellen Sie sicher, dass die neue Regel wird direkt unter den Zugriff erlauben, auf alle Benutzer in der Liste von Ausstellungsautorisierungsregeln angezeigt.
7. Klicken Sie auf "OK", um die Regel im Dialogfeld "Anspruchsregeln bearbeiten" zu speichern.

>[!NOTE]
>Sie ist den Wert für "öffentliche IP-Adresse Regex" oben in eine gültige IP-Ausdruck zu ersetzen. finden Sie unter der IP-Adressbereich Ausdruck für Weitere Informationen zu erstellen.

### <a name="scenario-3-block-all-external-access-to-office-365-except-browser-based-applications"></a>Szenario 3: Blockieren Sie alle externen Zugriff auf Office 365 mit Ausnahme von browserbasierten Anwendungen

Der Regelsatz baut auf Standard Ausstellung Autorisierungsregel, die mit dem Titel allen Benutzern Zugriff gewähren. Verwenden Sie die folgenden Schritte aus, die Microsoft Office 365 Identity-Plattform, mit dem Assistenten für Anspruch Vertrauensstellung einer vertrauenden Seite eine Ausstellung Autorisierungsregel hinzu:

>[!NOTE]
>Dieses Szenario wird nicht mit einem Drittanbieter-Proxy aufgrund von Einschränkungen auf Client Access Richtlinie Header mit Anforderungen für den passiven (Web-based) unterstützt.

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365-except-browser-based-applications"></a>Erstellen Sie eine Regel zum Blockieren von externen Zugriff auf Office 365 mit Ausnahme der Browser-basierte Anwendungen



1. Klicken Sie auf Start, zeigen Sie auf Programme, zeigen Sie auf Verwaltung, und klicken Sie dann auf AD FS 2.0-Verwaltung.
2. Klicken Sie in der Konsolenstruktur unter AD 2 FS. 0\vertrauensstellungen auf die Vertrauensstellungen der vertrauenden Seite, mit der rechten Maustaste in der Microsoft Office 365-Identitätsplattform Vertrauensstellung, und klicken Sie dann auf Anspruchsregeln bearbeiten. 
3. Wählen Sie die Registerkarte "Ausstellungsautorisierungsregeln", und klicken Sie dann auf Regel hinzufügen, um den Anspruch Regel-Assistenten zu starten, klicken Sie im Dialogfeld "Anspruchsregeln bearbeiten".
4. Klicken Sie auf der Seite Regelvorlage auswählen unter anspruchsregelvorlage senden Ansprüchen mit benutzerdefinierter Regel wählen Sie aus, und klicken Sie dann auf Weiter.
5. Geben Sie auf der Seite Regel konfigurieren unter Name der Anspruchsregel den Anzeigenamen für diese Regel. Geben Sie unter benutzerdefinierte Regel einen Wert ein, oder fügen Sie die folgende Syntax anspruchsregelsprache: `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value == "/adfs/ls/"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. Klicken Sie auf "Fertig stellen". Stellen Sie sicher, dass die neue Regel wird direkt unter den Zugriff erlauben, auf alle Benutzer in der Liste von Ausstellungsautorisierungsregeln angezeigt.
7. Klicken Sie auf "OK", um die Regel im Dialogfeld "Anspruchsregeln bearbeiten" zu speichern.

### <a name="scenario-4-block-all-external-access-to-office-365-for-designated-active-directory-groups"></a>Szenario 4: Blockieren Sie alle externen Zugriff auf Office 365 für die angegebenen Active Directory-Gruppen

Im folgenden Beispiel wird der Zugriff von internen Clients basierend auf IP-Adresse. Es blockiert den Zugriff von Clients, die sich außerhalb des Unternehmensnetzwerks befinden, auf denen eine externer Client-IP-Adresse verfügen, mit Ausnahme von Personen, die in einer angegebenen Active Directory-Group.The Regel Satz baut auf dem standardmäßigen Ausstellung Autorisierungsregel, die mit dem Titel allen Benutzern Zugriff gewähren. Verwenden Sie die folgenden Schritte aus, die Microsoft Office 365 Identity-Plattform, mit dem Assistenten für Anspruch Vertrauensstellung einer vertrauenden Seite eine Ausstellung Autorisierungsregel hinzu:

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365-for-designated-active-directory-groups"></a>Erstellen Sie eine Regel zum Blockieren von externen Zugriff auf Office 365 für die angegebenen Active Directory-Gruppen



1. Klicken Sie auf Start, zeigen Sie auf Programme, zeigen Sie auf Verwaltung, und klicken Sie dann auf AD FS 2.0-Verwaltung.
2. Klicken Sie in der Konsolenstruktur unter AD 2 FS. 0\vertrauensstellungen auf die Vertrauensstellungen der vertrauenden Seite, mit der rechten Maustaste in der Microsoft Office 365-Identitätsplattform Vertrauensstellung, und klicken Sie dann auf Anspruchsregeln bearbeiten. 
3. Wählen Sie die Registerkarte "Ausstellungsautorisierungsregeln", und klicken Sie dann auf Regel hinzufügen, um den Anspruch Regel-Assistenten zu starten, klicken Sie im Dialogfeld "Anspruchsregeln bearbeiten".
4. Klicken Sie auf der Seite Regelvorlage auswählen unter anspruchsregelvorlage senden Ansprüchen mit benutzerdefinierter Regel wählen Sie aus, und klicken Sie dann auf Weiter.
5. Geben Sie auf der Seite Regel konfigurieren unter Name der Anspruchsregel den Anzeigenamen für diese Regel. Geben Sie unter benutzerdefinierte Regel einen Wert ein, oder fügen Sie die folgende Syntax anspruchsregelsprache: `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    exists([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "Group SID value of allowed AD group"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. Klicken Sie auf "Fertig stellen". Stellen Sie sicher, dass die neue Regel wird direkt unter den Zugriff erlauben, auf alle Benutzer in der Liste von Ausstellungsautorisierungsregeln angezeigt.
7. Klicken Sie auf "OK", um die Regel im Dialogfeld "Anspruchsregeln bearbeiten" zu speichern.


### <a name="descriptions-of-the-claim-rule-language-syntax-used-in-the-above-scenarios"></a>Eine Beschreibung der Syntax anspruchsregelsprache in den oben genannten Szenarien verwendet

|Beschreibung|Die Syntax Anspruchs|
|-----|-----| 
|AD FS Standardregel, die allen Benutzern Zugriff gewähren. Diese Regel sollte bereits in der Microsoft Office 365-Identitätsplattform Ausstellungsautorisierungsregeln Liste Vertrauensstellung einer vertrauenden Seite vorhanden sein.|= > Problem (Type = "https://schemas.microsoft.com/authorization/claims/permit", Wert = "true");| 
|Dieser Klausel hinzufügen, um eine neue, benutzerdefinierte Regel gibt an, dass die Anforderung von der Verbundserverproxy stammt (d. h., sie hat den X-ms-Proxy-Header)
Es wird empfohlen, dass alle Regeln dazu gehören.|Vorhanden ist ([Typ == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"])| 
|Zum Einrichten, dass die Anforderung von einem Client mit eine IP-Adresse im definierten zulässigen wird verwendet.|NICHT vorhanden ist ([Typ == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-Client-ip", Wert = ~ "Kunden bereitgestellten öffentlichen IP-Adresse Regex"])| 
|Diese Klausel wird verwendet, um anzugeben, dass wenn die Anwendung zugegriffen wird, nicht Microsoft.Exchange.ActiveSync ist die Anforderung abgelehnt werden soll.|NICHT vorhanden ist ([Typ "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-Client-application" ==, Value=="Microsoft.Exchange.ActiveSync"])| 
|Mit dieser Regel können Sie bestimmen, ob der Aufruf über einen Webbrowser wurde, und nicht verweigert werden wird.|NICHT vorhanden ist ([Typ == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path," Wert == "/ Adfs/ls /"])| 
|Diese Regel gibt an, dass nur Benutzer in einer bestimmten Active Directory-Gruppe (basierend auf den Wert der SID) abgelehnt werden soll. Hinzufügen von nicht zu dieser Erklärung bedeutet, dass eine Gruppe von Benutzern zugelassen werden soll, unabhängig vom Speicherort.|Vorhanden ist ([Typ == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Wert = ~ "{Gruppe SID-Wert, der zulässige AD-Gruppe}"])| 
|Dies ist eine erforderliche Klausel Deny ausgegeben, wenn alle vorangegangenen Bedingungen erfüllt sind.|= > Problem (Type = "https://schemas.microsoft.com/authorization/claims/deny", Wert = "true");|

### <a name="building-the-ip-address-range-expression"></a>Erstellen von IP-Adresse Range-Ausdrucks

Der X-ms-weitergeleitet-Client-Ip-Anspruch wird über einen HTTP-Header aufgefüllt, die derzeit nur von Exchange Online, das den Header ausfüllt festgelegt ist, wenn die Authentifizierungsanforderung an AD FS übergeben. Der Wert des Anspruchs kann eines der folgenden sein:

>[!Note] 
>Exchange Online unterstützt derzeit nur für IPv4- und nicht IPV6-Adressen.

Eine einzelne IP-Adresse: die IP-Adresse des Clients, die direkt mit Exchange Online verbunden ist

>[!Note] 
>Die IP-Adresse eines Clients im Unternehmensnetzwerk wird als die externe IP-Adresse Ihres Unternehmens ausgehende Proxy oder Gateway angezeigt.

Clients, die mit dem Unternehmensnetzwerk, über ein VPN oder durch Microsoft DirectAccess (DA verbunden sind) können als interne Firmenkunden oder externe Clients, die je nach Konfiguration des VPN- oder stützt angezeigt.

Eine oder mehrere IP-Adressen: Wenn Exchange Online kann nicht die IP-Adresse des verbundenen Clients ermittelt, wird der Wert basierend auf den Wert der X-weitergeleitet-für-Header einen nicht standardmäßigen Header, der im HTTP-basierte Anforderungen enthalten sein kann und wird von vielen Clients, Lastenausgleichsmodule und Proxys auf dem Markt unterstützt festgelegt.

>[!Note]
>Mehrere IP-Adressen, der angibt, die Client-IP-Adresse und die Adresse für jeden Proxy, der die Anforderung übergeben werden durch ein Komma getrennt werden.

IP-Adressen, die im Zusammenhang mit Exchange Online-Infrastruktur werden nicht in der Liste angezeigt.


#### <a name="regular-expressions"></a>Reguläre Ausdrücke

Wenn Sie einen Bereich von IP-Adressen entsprechen müssen, ist es erforderlich, erstellen Sie einen regulären Ausdruck ein, um den Vergleich durchführt. In den nächsten Schritten bieten wir Beispiele für die Vorgehensweise beim Erstellen solcher Ausdrucks entsprechend der folgenden Adressbereiche (Beachten Sie, die Sie ändern diesen Beispielen entsprechend Ihrer öffentlichen IP-Adressbereich):


- 192.168.1.1 – 192.168.1.25
- 10.0.0.1 – 10.0.0.14

Zuerst wird das grundlegende Muster, die eine einzelne IP-Adresse entsprechen, werden wie folgt: \b###\.###\.###\.###\b

Erweitern diese, wir können entsprechen zwei verschiedene IP-Adressen mit einem Ausdruck oder wie folgt: \b###\.###\.###\.###\b|\b###\.###\.###\.###\b

Daher wäre ein Beispiel mit nur zwei Adressen (z. B. 192.168.1.1 oder 10.0.0.1) übereinstimmen: \b192\.168\.1\.1\b|\b10\.0\.0\.1\b

Dadurch können Sie das Verfahren, mit dem Sie eine beliebige Anzahl von Adressen eingeben können. Bei ein Bereich der Adresse zugelassen, z. B. 192.168.1.1 – 192.168.1.25 müssen, die entsprechende vorgenommen werden Zeichen von Zeichen: \b192\.168\.1\. ([1 bis 9] | [0-9]-1 | 2 [0 bis 5]) \b

>[!Note] 
>Die IP-Adresse wird als Zeichenfolge und keine Zahl behandelt.


Die Regel wird wie folgt aufgeteilt: \b192\.168\.1\.

Jeder Wert, beginnend mit 192.168.1 entspricht.

Die folgenden entspricht die Bereiche, die für den Teil der Adresse nach dem letzten Punkt erforderlich:


- ([1 bis 9] Übereinstimmungen Adressen mit 1 bis 9
- | 1 [0-9] entspricht Adressen mit 10-19
- |2[0-5]) Übereinstimmungen Adressen mit 20-25

>[!Note]
>Die Klammern müssen richtig positioniert werden, sodass Sie nicht mit anderen Teilen der IP-Adressen.

Mit dem 192 Block zugeordnet wird, können wir einen ähnlichen Ausdruck für die 10 Block schreiben: \b10\.0\.0\. ([1 bis 9] | [0-4]-1) \b

Und zusammenfügen, sollte der folgende Ausdruck alle Adressen für "192.168.1.1~25" und "10.0.0.1~14" entsprechen: \b192\.168\.1\. ([1-9]|1[0-9]|2[0-5])\b|\b10\.0\.0\. ([1 bis 9] | [0-4]-1) \b

#### <a name="testing-the-expression"></a>Testen den Ausdruck

Regex-Ausdrücke können sehr einfach, werden daher empfehlen wir dringend mithilfe eines Tools der Regex-Überprüfung. Wenn Sie eine Internetsuche nach "online Regex-Ausdrucks-Generator" tun, finden Sie einige gute online-Dienstprogramme, die Sie zum Testen Ihrer Ausdrücke mit Beispieldaten zulassen.

Wenn Sie den Ausdruck zu testen, ist es wichtig, dass Sie verstehen, was Sie erwarten können, müssen übereinstimmen. Exchange online viele IP-Adressen durch Kommas getrennt gesendet. Die oben angegebenen Ausdrücke funktioniert dies. Allerdings ist es wichtig, nachfolgend beim Testen Ihrer Regex-Ausdrücke. Beispielsweise kann eine im folgende Beispiel als Eingabe für den obigen Beispielen überprüfen verwenden: 

192.168.1.1, 192.168.1.2, 192.169.1.1. 192.168.12.1, 192.168.1.10, 192.168.1.25, 192.168.1.26, 192.168.1.30, 1192.168.1.20 

10.0.0.1, 10.0.0.5, 10.0.0.10, 10.0.1.0, 10.0.1.1, 110.0.0.1, 10.0.0.14, 10.0.0.15, 10.0.0.10, 10,0.0.1 











## <a name="validating-the-deployment"></a>Überprüfen der Bereitstellung

### <a name="security-audit-logs"></a>Sicherheitsüberwachungsprotokollen

Um sicherzustellen, dass der neue Anforderungskontext Ansprüche gesendet werden und stehen für die AD FS-Verarbeitungspipeline Ansprüche, aktivieren Sie Überwachung, die Protokollierung auf dem AD FS-Server. Dann werden senden Sie einige Authentifizierungsanfragen und überprüfen Sie die Anspruchswerte in die Standardsicherheit Überwachungsprotokolleinträge. 

Zum Aktivieren der Protokollierung von Überwachungsprotokollen, Ereignisse, um die Sicherheit auf einem AD FS-Server anmelden, führen Sie die Schritte unter konfigurieren die Überwachung für AD FS 2.0 aus.

### <a name="event-logging"></a>Ereignisprotokollierung

Standardmäßig Anforderungsfehler angemeldet sind, in das Anwendungsereignisprotokoll finden Sie unter Anwendungs- und Dienstprotokolle \ AD FS 2.0 \ Admin.For finden Sie weitere Informationen über die ereignisprotokollierung für AD FS unter [richten Sie AD FS 2.0-ereignisprotokollierung](https://technet.microsoft.com/library/adfs2-troubleshooting-configuring-computers.aspx).

### <a name="configuring-verbose-ad-fs-tracing-logs"></a>Konfigurieren der ausführlichen AD FS Ablaufverfolgungsprotokollen protokolliert

AD FS-Ablaufverfolgungsereignisse werden in das AD FS 2.0-Debugprotokoll protokolliert. Um Sie zu aktivieren, finden Sie unter [Konfigurieren der Debugablaufverfolgung für AD FS 2.0](https://technet.microsoft.com/en-us/library/adfs2-troubleshooting-configuring-computers.aspx).

Nachdem Sie die Protokollierung aktiviert haben, verwenden Sie die folgende Befehlszeilensyntax zum Aktivieren der ausführlichen Protokollierungsstufe: wevtutil.exe sl "AD FS 2.0-Ablaufverfolgung/Debug" /l: 5  

## <a name="related"></a>Im Zusammenhang mit
Weitere Informationen zu den neuen Anspruchstypen finden Sie unter [AD FS-Anspruchsanbieter-Typen](AD-FS-Claims-Types.md).
 
