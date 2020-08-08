---
title: 'AD FS Problembehandlung: "fddler-WS-Federation"'
description: Dieses Dokument zeigt eine ausführliche Ablauf Verfolgung eines WS-Verbund Austauschs mit AD FS
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/18/2018
ms.topic: article
ms.openlocfilehash: f30b66bd80b3c5002bdc2c66a1d89718cdb1ee39
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956207"
---
# <a name="ad-fs-troubleshooting---fiddler---ws-federation"></a>AD FS Problembehandlung: "fddler-WS-Federation"

![AD FS-und Windows Server-Verbund Diagramm](media/ad-fs-tshoot-fiddler-ws-fed/fiddler9.png)

## <a name="step-1-and-2"></a>Schritt 1 und 2

Dies ist der Anfang der Ablauf Verfolgung.  In diesem Frame wird Folgendes angezeigt:

![Start der Ablauf Verfolgung von "fddler"](media/ad-fs-tshoot-fiddler-ws-fed/fiddler1.png)

Anforderung:

- HTTP Get an unsere vertrauende Seite (http://sql1.contoso.com/SampApp)

Antwort:

- Die Antwort ist ein HTTP 302 (Redirect).  Die Transport Daten im Antwortheader zeigen an, wohin die Umleitung zu (https://sts.contoso.com/adfs/ls)
- Die Umleitungs-URL enthält WA = wsignin 1,0, das mitteilt, dass unsere RP-Anwendung eine WS-Verbund-Anmeldungs Anforderung für uns erstellt und diese an den/ADFS/ls/-Endpunkt des AD FS gesendet hat.  Dies wird als Umleitungs Bindung bezeichnet.

![Transportieren von Daten im Antwortheader](media/ad-fs-tshoot-fiddler-ws-fed/fiddler2.png)

## <a name="step-3-and-4"></a>Schritt 3 und 4

![Fortsetzungs-laufverfolgungsdatei](media/ad-fs-tshoot-fiddler-ws-fed/fiddler3.png)

Anforderung:

- HTTP Get to Your AD FS Server (STS..............

Antwort:

- Die Antwort ist eine Eingabeaufforderung für Anmelde Informationen.  Dies gibt an, dass die Formular Authentifizierung verwendet wird.
- Wenn Sie auf die WebView der Antwort klicken, wird die Eingabeaufforderung für die Anmelde Informationen angezeigt.

![Fortsetzung der Ablauf Verfolgung von "ddler"](media/ad-fs-tshoot-fiddler-ws-fed/fiddler6.png)

## <a name="step-5-and-6"></a>Schritt 5 und 6

![Registerkarte "WebView" der Eingabeaufforderung zur Eingabeaufforderung für Anmelde Informationen](media/ad-fs-tshoot-fiddler-ws-fed/fiddler4.png)

Anforderung:

- HTTP Post mit unserem Benutzernamen und Kennwort.
- Wir stellen unsere Anmelde Informationen vor.  Wenn Sie sich die Rohdaten in der Anforderung ansehen, werden die Anmelde Informationen angezeigt.

Antwort:

- Die Antwort wird gefunden, und das verschlüsselte msiauth-Cookie wird erstellt und zurückgegeben.  Hiermit wird die SAML-Assertion überprüft, die von unserem Client erzeugt wird.  Dies wird auch als "Authentifizierungs Cookie" bezeichnet und ist nur vorhanden, wenn AD FS der IDP ist.

## <a name="step-7-and-8"></a>Schritt 7 und 8

![Fortsetzung der Ablauf Verfolgung von "ddler"](media/ad-fs-tshoot-fiddler-ws-fed/fiddler5.png)

Anforderung:

- Nun, da wir authentifiziert wurden, führen wir eine weitere HTTP GET-Anforderung für den AD FS Server durch und stellen unser Authentifizierungs Token dar.

Antwort:

- Die Antwort ist ein HTTP-OK. Dies bedeutet, dass AD FS den Benutzer basierend auf den bereitgestellten Anmelde Informationen authentifiziert hat.
- Außerdem legen wir 3 Cookies auf den Client zurück.
    - Msisauthenticated enthält einen Base64-codierten Zeitstempelwert für den Zeitpunkt, zu dem der Client authentifiziert wurde.
    - Msisloopdetectioncookie wird vom AD FS Endlosschleifen Erkennungsmechanismus verwendet, um Clients zu beenden, die in einer endlos Umleitungs Schleife zum Verbund Server beendet wurden. Die Cookie-Daten sind ein Zeitstempel, der Base64-codiert ist.
    - Msissignout wird verwendet, um den IDP und alle für die SSO-Sitzung besuchten RPS nachzuverfolgen. Dieses Cookie wird verwendet, wenn eine WS-Verbund-Abmeldung aufgerufen wird. Der Inhalt dieses Cookies kann mit einem Base64-Decoder angezeigt werden.

## <a name="step-9-and-10"></a>Schritt 9 und 10

![Fortsetzung der Ablauf Verfolgung von "ddler"](media/ad-fs-tshoot-fiddler-ws-fed/fiddler7.png)

Anforderung:

- HTTP Post

Antwort:

- Die Antwort ist "found".

## <a name="step-11-and-12"></a>Schritt 11 und 12

![Abschließen der Ablauf Verfolgung von "fddler"](media/ad-fs-tshoot-fiddler-ws-fed/fiddler8.png)

Anforderung:

- HTTP-GET

Antwort:

- Die Antwort ist "OK".

## <a name="next-steps"></a>Nächste Schritte

- [Behandeln von AD FS-Problemen](ad-fs-tshoot-overview.md)