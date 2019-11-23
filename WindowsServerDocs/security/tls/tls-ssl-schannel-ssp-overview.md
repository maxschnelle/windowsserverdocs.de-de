---
title: Übersicht über TLS/SSL (Schannel SSP)
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 51e3886339b7864951b322d210e1a05bef4dc1e1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403363"
---
# <a name="tlsssl-overview-schannel-ssp"></a>Übersicht über TLS/SSL (Schannel SSP)

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows 10

In diesem Thema für IT-Experten werden die TLS-und SSL-Implementierungen in Windows mithilfe des SChannel Security Service Provider (SSP) vorgestellt, indem praktische Anwendungen, Änderungen in der Implementierung von Microsoft und Softwareanforderungen beschrieben werden. zusätzliche Ressourcen für Windows Server 2012 und Windows 8.

## <a name="BKMK_OVER"></a>Beschreibung
Schannel ist ein Sicherheitsdienstanbieter (Security Support Provider, SSP), der die Internet-Standardauthentifizierungsprotokolle SSL (Secure Sockets Layer) und TSL (Transport Layer Security) implementiert.

Die Security Support Provider-Schnittstelle (Security Support Provider Interface, SSPI) ist eine API, die von Windows-Systemen verwendet wird, um sicherheitsbezogene Funktionen wie Authentifizierungen durchzuführen. Die SSPI fungiert als gemeinsame Schnittstelle für mehrere SSPs, einschließlich des Schannel SSP.

Die TLS-Versionen 1,0, 1,1 und 1,2, die SSL-Versionen 2,0 und 3,0 sowie das Datagramm Transport Layer Security \(DTLS\) Protokollversion 1,0 und der Transport \(PCT\) des privaten Kommunikations Transports basieren auf der Kryptografie mit öffentlichem Schlüssel. Die Schannel-Authentifizierungsprotokollsammlung enthält diese Protokolle. Alle Schannel-Protokolle verwenden ein Client/Server-Modell.

## <a name="BKMK_APP"></a>Bereich
Ein Problem beim Verwalten eines Netzwerks ist das Sichern von Daten, die zwischen Anwendungen in einem nicht vertrauenswürdigen Netzwerk gesendet werden. Sie können TLS und SSL zum Authentifizieren von Servern und Client Computern verwenden und dann das Protokoll verwenden, um Nachrichten zwischen den authentifizierten Parteien zu verschlüsseln.

Sie können TLS/SSL beispielsweise für Folgendes verwenden:

-   SSL-gesicherte Transaktionen mit einer E-Commerce-Website
-   Authentifizierten Clientzugriff auf einer SSL-gesicherten Website
-   Remotezugriff
-   SQL-Zugriff
-   E-Mail

## <a name="BKMK_SOFT"></a>Bedingungen
TLS-und SSL-Protokolle verwenden ein Client/Server-Modell und basieren auf der Zertifikat Authentifizierung, die eine Public Key-Infrastruktur erfordert.

## <a name="BKMK_INSTALL"></a>Server-Manager Informationen
Zum Implementieren von TLS, SSL oder SChannel sind keine Konfigurationsschritte erforderlich.

## <a name="see-also"></a>Weitere Informationen ##

-   [Das SChannel-Sicherheitspaket](https://docs.microsoft.com/windows/desktop/com/schannel)
-   [Sicherer Kanal](https://docs.microsoft.com/windows/desktop/SecAuthN/secure-channel)
-   [Transport Layer Security-Protokoll](https://docs.microsoft.com/windows/desktop/SecAuthN/transport-layer-security-protocol)
