---
title: AD FS - Fiddler - WS-Verbund-Problembehandlung
description: In diesem Dokument wird eine ausführliche Ablaufverfolgung von einem Exchange WS-Verbund mit AD FS
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/18/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: be1c9f466ec13272d10f0fb9ca31cf326a1ec29a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59846901"
---
# <a name="ad-fs-troubleshooting---fiddler---ws-federation"></a>AD FS - Fiddler - WS-Verbund-Problembehandlung
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler9.png)

## <a name="step-1-and-2"></a>Schritt 1 und 2
Dies ist der Anfang unsere Ablaufverfolgung.  In diesem Frame wird Folgendes angezeigt: ![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler1.png)

Anforderung:

- HTTP GET auf unsere relying Party (http://sql1.contoso.com/SampApp)

Antwort:

- Die Antwort ist eine HTTP 302 (Umleitung).  Die Übertragung von Daten in der Antwortheader zeigt, wo, eine Umleitung an)https://sts.contoso.com/adfs/ls)
- Die umleitungs-URL enthält wa = Wsignin 1.0, die mitteilt, dass unsere Anwendung der vertrauenden Seite ein WS-Verbund-anmeldungsanforderung für uns erstellt und diese an die AD FS /adfs/ls/Endpunkt gesendet werden.  Dies wird bezeichnet als Umleitungs-Bindung.
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler2.png)

## <a name="step-3-and-4"></a>Schritt 3 und 4

![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler3.png)

Anforderung:

- HTTP GET, um unsere server(sts.contoso.com) AD FS

Antwort:

- Die Antwort ist eine Eingabeaufforderung für Anmeldeinformationen.  Dies bedeutet, dass wir Forms Authnetication verwenden
- Durch Klicken auf die Webansicht der Antwort sehen Sie die Anmeldeinformationen aufgefordert.
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler6.png)

## <a name="step-5-and-6"></a>Schritt 5 und 6

![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler4.png)

Anforderung:

- HTTP-POST mit dem Benutzernamen und Kennwort.  
- Wir stellen unsere Anmeldeinformationen.  Die unformatierten Daten in der Anforderung anhand sehen die Anmeldeinformationen

Antwort:

- Die Antwort ist, gefunden und die MSIAuth verschlüsseltes Cookie erstellt und zurückgegeben wird.  Hiermit wird die erzeugten unserer Clients-SAML-Assertion zu überprüfen.  Dies ist auch bekannt als "Authentifizierungscookie" und werden nur vorhanden, wenn AD FS den Idp ist.


## <a name="step-7-and-8"></a>Schritt 7 und 8
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler5.png)

Anforderung:

- Nun, dass wir authentifiziert haben wir eine andere HTTP GET auf dem AD FS-Server und Präsentieren von Authentifizierungstoken

Antwort:

- Die Antwort ist ein HTTP-OK-Dies bedeutet, dass AD FS den Benutzer basierend auf der bereitgestellten Anmeldeinformationen authentifiziert hat
- Außerdem legen wir 3 Cookies an den client
    - MSISAuthenticated enthält einen base64-codierte Timestamp-Wert für, wenn der Client authentifiziert wurde.
    - MSISLoopDetectionCookie wird von der AD FS Endlosschleife-Erkennungsmechanismus für Stop-Clients verwendet, die sich in eine unendliche Weiterleitungsschleife Verbundserver beendet haben. Die Cookiedaten werden einen Zeitstempel, der base64-codiert ist.
    - MSISSignout wird zum Nachverfolgen der IdP verwendet, und alle RPs besucht, für die SSO-Sitzung. Dieses Cookie wird verwendet, wenn eine WS-Verbund-abmeldeanforderungen aufgerufen wird. Sie sehen, dass der Inhalt dieses Cookies, die einen base64-Decoder verwenden.
    
## <a name="step-9-and-10"></a>Schritt 9 und 10
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler7.png) Anforderung:

- HTTP-POST

Antwort:

- Die Antwort ist ein gefunden

## <a name="step-11-and-12"></a>Schritt 11 und 12
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler8.png) Anforderung:

- HTTP-GET

Antwort:

- Die Antwort ist in Ordnung

## <a name="next-steps"></a>Nächste Schritte

- [AD FS-Problembehandlung](ad-fs-tshoot-overview.md)