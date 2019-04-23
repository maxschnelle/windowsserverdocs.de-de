---
title: Übersicht über die TLS/SSL (Schannel SSP)
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b7b0432-1bef-4912-8c9a-8989d47a4da9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/16/2018
ms.openlocfilehash: a6571e5e06e07fd62ad4cf39bab322b45c90a9f9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848601"
---
# <a name="tlsssl-overview-schannel-ssp"></a>Übersicht über die TLS/SSL (Schannel SSP)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10

In diesem Thema für IT-Experten die TLS- und SSL-Implementierungen in Windows, indem Sie praktische Anwendungen, die Schannel Security Service Provider (SSP) vorgestellt, ändert sich in der Microsoft Implementierung und softwareanforderungen für plus Zusätzliche Ressourcen für Windows Server 2012 und Windows 8.

## <a name="BKMK_OVER"></a>Beschreibung
Schannel ist ein Sicherheitsdienstanbieter (Security Support Provider, SSP), der die Internet-Standardauthentifizierungsprotokolle SSL (Secure Sockets Layer) und TSL (Transport Layer Security) implementiert.

Die Security Support Provider-Schnittstelle (Security Support Provider Interface, SSPI) ist eine API, die von Windows-Systemen verwendet wird, um sicherheitsbezogene Funktionen wie Authentifizierungen durchzuführen. Die SSPI-Funktionen als eine allgemeine Schnittstelle für mehrere SSPs, einschließlich des Schannel SSP.

TLS-Versionen 1.0, 1.1 und 1.2, SSL-Versionen 2.0 und 3.0, sowie das Datagram Transport Layer Security \(DTLS\) Protocol, Version 1.0 und das Private Communications Transport \(PCT\) Protokoll basiert auf Verschlüsselung mit öffentlichem Schlüssel. Die Schannel-Authentifizierungsprotokollsammlung enthält diese Protokolle. Alle Schannel-Protokolle verwenden ein Client/Server-Modell.

## <a name="BKMK_APP"></a>Anwendungen
Ein Problem beim Verwalten eines Netzwerks ist das Sichern von Daten, die zwischen Anwendungen in einem nicht vertrauenswürdigen Netzwerk gesendet werden. Sie können TLS und SSL verwenden, Authentifizierung von Servern und Clientcomputern und dann das Protokoll zu verwenden, um Nachrichten zwischen den authentifizierten Parteien zu verschlüsseln.

Sie können TLS/SSL beispielsweise für Folgendes verwenden:

-   SSL-gesicherte Transaktionen mit einer E-Commerce-Website
-   Authentifizierten Clientzugriff auf einer SSL-gesicherten Website
-   Remotezugriff
-   SQL-Zugriff
-   E-Mail

## <a name="BKMK_SOFT"></a>Anforderungen an
TLS und SSL-Protokolle verwenden ein Client/Server-Modell und basiert auf Zertifikatauthentifizierung, wofür eine public Key-Infrastruktur erfordert.

## <a name="BKMK_INSTALL"></a>Informationen zur Server-Manager
Es sind keine Konfigurationsschritte erforderlich, TLS, SSL oder Schannel zu implementieren.

## <a name="see-also"></a>Siehe auch ##

-   [Das Schannel-Sicherheitspaket](https://docs.microsoft.com/windows/desktop/com/schannel)
-   [Sicherer Kanal](https://docs.microsoft.com/windows/desktop/SecAuthN/secure-channel)
-   [Transport Layer Security Protocol](https://docs.microsoft.com/windows/desktop/SecAuthN/transport-layer-security-protocol)
