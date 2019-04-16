---
title: "TLS – SSL (Schannel SSP) (Übersicht)"
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
ms.date: 10/12/2016
ms.openlocfilehash: afd0b70264dba1e720f95e40d3d201c2c5bf1c64
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="tls---ssl-schannel-ssp-overview"></a>TLS – SSL (Schannel SSP) (Übersicht)

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema für IT-Experten werden die TLS/SSL-Implementierung in Windows mithilfe des Schannel Security Service Provider (SSP) beschrieben praktische Anwendungsfälle, Änderungen an der Implementierung von Microsoft und softwareanforderungen sowie zusätzliche Ressourcen für Windows Server2012 und Windows8 eingeführt.

**Meinten Sie:**

-   [Das Schannel-Sicherheitspaket](https://msdn.microsoft.com/library/ms678421.aspx)

-   [Sicheren Kanal](https://msdn.microsoft.com/library/windows/desktop/aa380123.aspx)

-   [Transport Layer Security-Protokoll](https://msdn.microsoft.com/library/windows/desktop/aa380516.aspx)

## <a name="BKMK_OVER"></a>TLS\SSL \(Schannel\) Beschreibung
Schannel ist ein Security Support Provider-\(SSP\), der Secure Sockets Layer-\(SSL\) und Transport Layer Security \(TLS\) implementiert, Internet-Standardauthentifizierungsprotokolle.

Die Security Support Provider Interface \(SSPI\) ist eine API, die von Windows-Systemen verwendet werden, um Sicherheit\-bezogene Funktionen wie Authentifizierungen durchzuführen. Die SSPI Dienst als gemeinsame Schnittstelle für mehrere Security Support Provider-\(SSPs\), einschließlich Schannel SSP.

Die Transport Layer Security \(TLS\)-Protokollversionen 1.0, 1.1 und 1.2, \(SSL\) Secure Sockets Layer-Protokoll, Version 2.0 und 3.0, Datagram Transport Layer Security \(DTLS\) Version 1.0, und das Private Communications Transport \(PCT\) Protokoll basieren auf Kryptografie mit öffentlichem Schlüssel. Die Sicherheitskanal \(Schannel\)-authentifizierungsprotokollsammlung enthält diese Protokolle. Alle Schannel-Protokolle verwenden ein Client/Server-Modell.

## <a name="BKMK_APP"></a>In der Praxis
Ein Problem beim Verwalten eines Netzwerks ist Daten schützen, die zwischen Programmen in einem nicht vertrauenswürdigen Netzwerk gesendet wird. Sie können TLS\SSL authentifizieren, Servern und Clientcomputern, und klicken Sie dann das Protokoll verwenden, um Nachrichten zwischen den authentifizierten Parteien zu verschlüsseln.

Beispielsweise können Sie TLS\SSL für:

-   SSL\-gesicherte Transaktionen mit einer E\-E-Commerce-Website

-   Authentifizierter Clientzugriff auf eine SSL\-gesicherten Website

-   Remotezugriff

-   SQL-Zugriff

-   E\-mail

## <a name="BKMK_SOFT"></a>Anforderungen der Clientsoftware
Das Protokoll TLS\SSL ein Client\server-Modell und basiert auf Zertifikatauthentifizierung, wofür eine Public Key-Infrastruktur erforderlich ist.

## <a name="BKMK_INSTALL"></a>Server-Manager-Informationen
Es sind keine Konfigurationsschritte erforderlich, um TLS, SSL oder Schannel implementieren.

