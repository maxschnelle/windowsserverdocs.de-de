---
ms.assetid: ''
title: Clientzugriff Anspruchstypen in AD FS
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1e37aded450555d293806d1ed8903a51e3df9424
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839141"
---
#<a name="client-access-policy-claim-types-in-ad-fs"></a>Clientzugriffsrichtlinie Anspruchstypen in AD FS

Um Informationen zu zusätzlichen Kontext bereitzustellen, verwenden Sie Clientzugriffsrichtlinien die folgenden Anspruchstypen, die AD FS aus Anforderungsheaderinformationen für die Verarbeitung generiert.  Weitere Informationen finden Sie unter [die Rolle des anspruchsmoduls](../technical-reference/the-role-of-the-claims-engine.md).

##<a name="x-ms-forwarded-client-ip"></a>X-MS-Forwarded-Client-IP

Anspruchstyp: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`

Dieser AD FS-Anspruch stellt eine "versucht," Feststellung der IP-Adresse des Benutzers (z. B. der Outlook-Client) und die Anforderung dar. Dieser Anspruch kann mehrere IP-Adressen, einschließlich der Adresse von jedem Proxy, der die Anforderung weitergeleitet enthalten.  Dieser Anspruch wird aufgefüllt, von einem HTTP-Header, die derzeit wird nur von Exchange Online, die den Header aufgefüllt wird, wenn die Authentifizierungsanforderung an AD FS übergeben festgelegt. Der Wert des Anspruchs kann es sich um eine der folgenden sein:


- Eine einzelne IP-Adresse – die IP-Adresse des Clients, die direkt mit Exchange Online verbunden ist

    >! [Hinweis] Die IP-Adresse eines Clients im Unternehmensnetzwerk wird als der externe IP-Adresse des Proxys für ausgehenden Datenverkehr der Organisation oder Gateways angezeigt.

- Eine oder mehrere IP-Adressen
    - Wenn Exchange Online die IP-Adresse der verbindende Client nicht ermitteln kann, wird der Wert, der basierend auf dem Wert der X-forwarded-for-Header, eine nicht standardmäßige Headerdateien, die in der HTTP-basierten aufgenommen werden kann, fordert und wird von vielen Clients, Load balancer unterstützt festgelegt und Proxys auf dem Markt.
    - Mehrere IP-Adressen, der angibt, die Client-IP-Adresse und die Adresse für jeden Proxy, der die Anforderung zu übergeben, werden durch ein Komma getrennt werden.

    >! [Hinweis] IP-Adressen, die im Zusammenhang mit Exchange Online-Infrastruktur werden nicht in der Liste vorhanden.


>! [Warnung] Exchange Online unterstützt derzeit nur IPV4-Adressen; IPV6-Adressen werden nicht unterstützt. 


## <a name="x-ms-client-application"></a>X-MS-Client-Application

Anspruchstyp: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`

Dieser AD FS-Anspruch darstellt, das von der End-Client, der verwendeten Anwendung lose entspricht verwendete Protokoll.  Dieser Anspruch wird aufgefüllt, von einem HTTP-Header, die derzeit wird nur von Exchange Online, die den Header aufgefüllt wird, wenn die Authentifizierungsanforderung an AD FS übergeben festgelegt. Abhängig von der Anwendung wird der Wert dieses Anspruchs einen der folgenden sein:



- Bei Geräten, die Exchange Active Sync verwenden, ist der Wert Microsoft.Exchange.ActiveSync. 
- Verwendung von Microsoft Outlook-Clients möglicherweise in einem der folgenden Werte:
    - Microsoft.Exchange.Autodiscover
    - Microsoft.Exchange.OfflineAddressBook
    - Microsoft.Exchange.RPC
    - Microsoft.Exchange.WebServices
    - Microsoft.Exchange.Mapi
- Weitere mögliche Werte für diesen Header umfassen Folgendes:
    - Microsoft.Exchange.Powershell
    - Microsoft.Exchange.SMTP
    - Microsoft.Exchange.PopImap
    - Microsoft.Exchange.Pop
    - Microsoft.Exchange.Imap

## <a name="x-ms-client-user-agent"></a>X-MS-Client-User-Agent

Anspruchstyp: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`

Dieser AD FS-Anspruch enthält eine Zeichenfolge, um den Gerätetyp darstellen, den vom Client verwendet wird, um den Dienst zuzugreifen. Dies kann verwendet werden, wenn Kunden den Zugriff für bestimmte Geräte (z. B. bestimmte Arten von Smartphones) zu verhindern möchten.  Dieser Anspruch wird aufgefüllt, von einem HTTP-Header, die derzeit wird nur von Exchange Online, die den Header aufgefüllt wird, wenn die Authentifizierungsanforderung an AD FS übergeben festgelegt. Beispielwerte für diesen Anspruch enthalten (jedoch nicht beschränkt auf) die folgenden Werte.
>! [Hinweis] Die im folgenden sind Beispiele für was der Wert der X-ms-Benutzer-Agent für einen Client enthalten kann, dessen X-ms-Client-Anwendung ist "Microsoft.Exchange.ActiveSync"

- Vortex/1.0
- Apple-iPad1C1/812.1
- Apple-iPhone3C1/811.2
- Apple-iPhone/704.11
- Moto-DROID2/4.5.1
- SAMSUNGSPHD700/100.202
- Android/0.3

>! [Hinweis] Es ist auch möglich, dass dieser Wert leer ist.


## <a name="x-ms-proxy"></a>X-MS-Proxy

Anspruchstyp: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`

Dieser AD FS-Anspruch gibt an, dass die Anforderung durch den Verbundserverproxy übergeben wurde.  Dieser Anspruch wird von der Verbundserverproxy, aufgefüllt, die den Header aufgefüllt wird, wenn die Authentifizierungsanforderung an die Back-End-Verbunddienst übergeben. AD FS konvertiert es dann in einen Anspruch. 

Der Wert des Anspruchs ist der DNS-Name des Verbundserverproxys, die die Anforderung zu übergeben.

## <a name="x-ms-endpoint-absolute-path-active-vs-passive"></a>X-MS-Endpunkt-Absolute-Path (aktiv bzw. passiv)

Anspruchstyp: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`

Dieser Anspruchstyp kann zur Bestimmung der Anforderungen von "aktiv" (umfassenden)-Clients im Vergleich zu "Passiv" (Web-Browser-basiert)-Clients verwendet werden. Dadurch werden externe Anfragen von browserbasierten Anwendungen wie Outlook Web Access, SharePoint Online oder Office 365-Portal zugelassen werden, während die Anforderungen von rich-Clients wie Microsoft Outlook blockiert werden.

Der Wert des Anspruchs ist der Name der AD FS-Diensts, der die Anforderung empfangen hat.
