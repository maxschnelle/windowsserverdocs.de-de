---
ms.assetid: 
title: Clientzugriff Anspruchstypen in AD FS
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1e37aded450555d293806d1ed8903a51e3df9424
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
#<a name="client-access-policy-claim-types-in-ad-fs"></a>Client-Richtlinie Anspruchstypen in AD FS

Um zusätzliche Anforderung Kontextinformationen bereitzustellen, verwenden Sie Client-Richtlinien die folgenden Anspruchstypen, die von AD FS Anforderung Header-Informationen für die Verarbeitung generiert.  Weitere Informationen finden Sie unter [die Rolle des anspruchsmoduls](../technical-reference/the-role-of-the-claims-engine.md).

##<a name="x-ms-forwarded-client-ip"></a>X-MS-weitergeleitet-Client-IP

Typ des Anspruchs: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`

Diesen Anspruch von AD FS stellt einen "beste Versuch" ermitteln die IP-Adresse des Benutzers (z.B. Outlook-Client), der die Anforderung dar. Diesem Anspruch kann mehrere IP-Adressen, einschließlich der Adresse des jeden Proxy, der die Anforderung weitergeleitet enthalten.  Diesen Anspruch über einen HTTP-Header, die aktuell aufgefüllt wird nur festlegen, indem Sie Exchange Online, mit dem die Kopfzeile gefüllt, wenn Sie die Authentifizierungsanforderung an AD FS übergeben. Der Wert des Anspruchs kann eine der folgenden sein:


- Eine einzelne IP-Adresse - IP-Adresse des Clients, die direkt mit Exchange Online verbunden ist

    >! [Hinweis] Die IP-Adresse eines Clients im Unternehmensnetzwerk wird als die externe IP-Adresse Ihres Unternehmens ausgehende Proxy oder Gateway angezeigt.

- Eine oder mehrere IP-Adressen
    - Wenn Sie Exchange Online die IP-Adresse des verbundenen Clients nicht ermitteln kann, wird es legen Sie den Wert basierend auf den Wert der X-weitergeleitet-für-Header ein nicht standardmäßiger Header, der HTTP-basierten enthalten sein kann anfordert und von vielen Clients, Lastenausgleichsmodule und Proxys auf dem Markt unterstützt wird.
    - Mehrere IP-Adressen, der angibt, die Client-IP-Adresse und die Adresse für jeden Proxy, der die Anforderung übergeben werden durch ein Komma getrennt werden.

    >! [Hinweis] IP-Adressen, die im Zusammenhang mit Exchange Online-Infrastruktur werden nicht in der Liste vorhanden sein.


>! [Warnung] Exchange Online unterstützt derzeit nur-IPv4-Adressen. IPV6-Adressen wird nicht unterstützt. 


## <a name="x-ms-client-application"></a>X-MS-Client-Anwendung

Typ des Anspruchs: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`

Diesen Anspruch von AD FS stellt das Protokoll verwendet wird dem Endbenutzer, die lose entspricht der Anwendung verwendet wird.  Diesen Anspruch über einen HTTP-Header, die aktuell aufgefüllt wird nur festlegen, indem Sie Exchange Online, mit dem die Kopfzeile gefüllt, wenn Sie die Authentifizierungsanforderung an AD FS übergeben. Abhängig von der Anwendung wird der Wert dieses Anspruchs eines der folgenden sein:



- Im Fall von Geräten, die Exchange ActiveSync verwenden, ist der Wert Microsoft.Exchange.ActiveSync. 
- Verwendung von Microsoft Outlook-Client möglicherweise in einem der folgenden Werte:
    - Microsoft.Exchange.Autodiscover
    - Microsoft.Exchange.OfflineAddressBook
    - Microsoft.Exchange.RPC
    - Microsoft.Exchange.WebServices
    - Microsoft.Exchange.Mapi
- Andere mögliche Werte für diesen Header sind folgende:
    - Microsoft.Exchange.PowerShell
    - Microsoft.Exchange.SMTP
    - Microsoft.Exchange.PopImap
    - Microsoft.Exchange.Pop
    - Microsoft.Exchange.Imap

## <a name="x-ms-client-user-agent"></a>X-MS-Client-Benutzer-Agent

Typ des Anspruchs: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`

Diesen Anspruch von AD FS bietet eine Zeichenfolge, um den Gerätetyp darstellen, den der Client verwendet, um den Dienst zuzugreifen. Dies kann verwendet werden, wenn Kunden, um den Zugriff für bestimmte Geräte (z.B. bestimmte Arten von Smartphones) zu verhindern möchten.  Diesen Anspruch über einen HTTP-Header, die aktuell aufgefüllt wird nur festlegen, indem Sie Exchange Online, mit dem die Kopfzeile gefüllt, wenn Sie die Authentifizierungsanforderung an AD FS übergeben. Beispielwerte für diesen Anspruch enthalten (jedoch nicht beschränkt auf) die folgenden Werte.
>! [Hinweis] Die im folgenden sind Beispiele für was der X-ms-Benutzer-Agent-Wert für einen Client enthalten kann, deren X-ms-Client-Anwendung ist "Microsoft.Exchange.ActiveSync"

- Vortex/1.0
- Apple-iPad1C1/812.1
- Apple-iPhone3C1/811.2
- Apple-iPhone/704.11
- Moto-DROID2/4.5.1
- SAMSUNGSPHD700/100.202
- Android/0.3

>! [Hinweis] Es ist auch möglich, dass dieser Wert leer ist.


## <a name="x-ms-proxy"></a>X-MS-Proxy

Typ des Anspruchs: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`

Diesen Anspruch von AD FS weist darauf hin, dass die Anforderung durch den Verbundserverproxy bestanden hat.  Diesen Anspruch wird durch den Verbundserverproxy aufgefüllt, das die Kopfzeile ausfüllt, wenn die Authentifizierungsanforderung an den Back-End-Verbunddienst übergeben. AD FS konvertiert es dann in einen Anspruch. 

Der Wert des Anspruchs ist der DNS-Name des Verbundserverproxys, die die Anforderung übergeben.

## <a name="x-ms-endpoint-absolute-path-active-vs-passive"></a>X-MS-Endpunkt-Absolute-Pfad (aktiv oder passiv)

Typ des Anspruchs: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`

Dieser Typ des Anspruchs kann zur Bestimmung von Anfragen von "aktiv" (rich)-Clients im Vergleich zu "passiven" (Web-Browser-basiert)-Clients verwendet werden. Dadurch können externe Anforderungen von browserbasierten Anwendungen wie Outlook Web Access, SharePoint Online oder Office365-Portal zugelassen werden, während die Anfragen von rich-Clients wie Microsoft Outlook blockiert werden.

Der Wert des Anspruchs ist der Name des AD FS-Diensts, die die Anforderung empfangen.
