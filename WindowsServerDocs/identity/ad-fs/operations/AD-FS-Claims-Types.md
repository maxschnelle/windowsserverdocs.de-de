---
ms.assetid: ''
title: Client Zugriffs-Anspruchs Typen in AD FS
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a689e68ae60268880fd28158820c1803ab35bc33
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358622"
---
# <a name="client-access-policy-claim-types-in-ad-fs"></a>Anspruchs Typen für Client Zugriffsrichtlinien in AD FS

Um zusätzliche Anforderungs Kontextinformationen bereitzustellen, verwenden Client Zugriffsrichtlinien die folgenden Anspruchs Typen, die AD FS aus den Anforderungs Header Informationen für die Verarbeitung generiert.  Weitere Informationen finden Sie [unter The Role of the Claims Engine](../technical-reference/the-role-of-the-claims-engine.md).

## <a name="x-ms-forwarded-client-ip"></a>X-MS-weitergeleitete Client-IP

Anspruchstyp:`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`

Dieser AD FS Anspruch stellt einen "besten Versuch" dar, die IP-Adresse des Benutzers (z. b. den Outlook-Client) zu ermitteln, der die Anforderung sendet. Dieser Anspruch kann mehrere IP-Adressen enthalten, einschließlich der Adresse jedes Proxys, von dem die Anforderung weitergeleitet wurde.  Dieser Anspruch wird mit einem HTTP-Header aufgefüllt, der derzeit nur von Exchange Online festgelegt wird, der den-Header auffüllt, wenn die Authentifizierungsanforderung an AD FS übergeben wird. Der Wert des Anspruchs kann eines der folgenden sein:


- Eine einzelne IP-Adresse: die IP-Adresse des Clients, der direkt mit Exchange Online verbunden ist

    >! Nebenbei Die IP-Adresse eines Clients im Unternehmensnetzwerk wird als IP-Adresse der externen Schnittstelle des ausgehenden Proxys oder Gateways der Organisation angezeigt.

- Mindestens eine IP-Adresse
  - Wenn Exchange Online die IP-Adresse des Clients, der die Verbindung herstellt, nicht ermitteln kann, wird der Wert auf Grundlage des Werts des x-weitergeleiteten-für-Headers festgelegt, ein nicht standardmäßiger Header, der in http-basierten Anforderungen eingeschlossen werden kann und von vielen Clients, Lasten Ausgleichs Modulen und unterstützt wird. Proxys auf dem Markt.
  - Mehrere IP-Adressen, die angeben, dass die Client-IP-Adresse und die Adresse der einzelnen Proxys, die die Anforderung bestehen, durch Kommas getrennt werden

    >! Nebenbei IP-Adressen im Zusammenhang mit der Exchange Online-Infrastruktur sind nicht in der Liste vorhanden.


>! Davor Exchange Online unterstützt zurzeit nur IPv4-Adressen. IPv6-Adressen werden nicht unterstützt. 


## <a name="x-ms-client-application"></a>X-MS-Client-Anwendung

Anspruchstyp:`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`

Dieser AD FS Anspruch stellt das vom Endclient verwendete Protokoll dar, das der verwendeten Anwendung lose entspricht.  Dieser Anspruch wird mit einem HTTP-Header aufgefüllt, der derzeit nur von Exchange Online festgelegt wird, der den-Header auffüllt, wenn die Authentifizierungsanforderung an AD FS übergeben wird. Abhängig von der Anwendung ist der Wert dieses Anspruchs einer der folgenden:



- Bei Geräten, die Exchange Active Sync verwenden, lautet der Wert Microsoft. Exchange. ActiveSync. 
- Die Verwendung des Microsoft Outlook-Clients kann zu einem der folgenden Werte führen:
    - Microsoft. Exchange. autodiscover
    - Microsoft. Exchange. OfflineAddressBook
    - Microsoft. Exchange. RPC
    - Microsoft. Exchange. Webservices
    - Microsoft. Exchange. MAPI
- Zu den anderen möglichen Werten für diesen Header zählen die folgenden:
    - Microsoft. Exchange. PowerShell
    - Microsoft. Exchange. SMTP
    - Microsoft. Exchange. PopImap
    - Microsoft. Exchange. Pop
    - Microsoft. Exchange. IMAP

## <a name="x-ms-client-user-agent"></a>X-MS-Client-User-Agent

Anspruchstyp:`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`

Dieser AD FS Anspruch stellt eine Zeichenfolge bereit, die den Gerätetyp darstellt, der vom Client für den Zugriff auf den Dienst verwendet wird. Dies kann verwendet werden, wenn Kunden den Zugriff für bestimmte Geräte (z. b. bestimmte Arten von Smartphones) verhindern möchten.  Dieser Anspruch wird mit einem HTTP-Header aufgefüllt, der derzeit nur von Exchange Online festgelegt wird, der den-Header auffüllt, wenn die Authentifizierungsanforderung an AD FS übergeben wird. Beispiel Werte für diesen Anspruch sind die unten aufgeführten Werte (aber nicht beschränkt auf).
>! Nebenbei Im folgenden finden Sie Beispiele für den Wert des x-MS-User-Agent-Werts für einen Client, dessen x-MS-Client-Anwendung "Microsoft. Exchange. ActiveSync" ist.

- Vortex/1.0
- Apple-iPad1C1/812.1
- Apple-iPhone3C1/811.2
- Apple-iPhone/704.11
- Moto-DROID2/4.5.1
- SAMSUNGSPHD700/100.202
- Android/0.3

>! Nebenbei Es ist auch möglich, dass dieser Wert leer ist.


## <a name="x-ms-proxy"></a>X-MS-Proxy

Anspruchstyp:`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`

Dieser AD FS Anspruch gibt an, dass die Anforderung den Verbund Server Proxy übermittelt hat.  Dieser Anspruch wird durch den Verbund Server Proxy aufgefüllt, der den-Header auffüllt, wenn die Authentifizierungsanforderung an das Back-End-Verbunddienst übergeben wird. AD FS dann in einen Anspruch konvertiert. 

Der Wert des Anspruchs ist der DNS-Name des Verbund Server Proxys, der die Anforderung übermittelt hat.

## <a name="x-ms-endpoint-absolute-path-active-vs-passive"></a>X-MS-Endpoint-absolute-path (aktiv/passiv)

Anspruchstyp:`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`

Dieser Anspruchstyp kann zum Bestimmen von Anforderungen verwendet werden, die von "aktiven" (Rich) Clients und "passiven" (Webbrowser basierten) Clients stammen. Dadurch können externe Anforderungen von browserbasierten Anwendungen wie Outlook Webzugriff, SharePoint Online oder dem Office 365-Portal zugelassen werden, während Anforderungen, die von Rich-Clients wie Microsoft Outlook stammen, blockiert werden.

Der Wert des Anspruchs ist der Name des AD FS Dienstanbieter, der die Anforderung empfangen hat.
