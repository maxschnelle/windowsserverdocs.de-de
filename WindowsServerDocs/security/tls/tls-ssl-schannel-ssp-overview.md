---
title: Übersicht über TLS/SSL (Schannel SSP)
description: Windows Server-Sicherheit
ms.topic: article
ms.assetid: 1b7b0432-1bef-4912-8c9a-8989d47a4da9
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 05/16/2018
ms.openlocfilehash: 21ad7977039eda311dd6f093fc53c09c08cf0317
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89637840"
---
# <a name="tlsssl-overview-schannel-ssp"></a>Übersicht über TLS/SSL (Schannel SSP)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows 10

In diesem Thema für IT-Experten werden die TLS-und SSL-Implementierungen in Windows mithilfe des SChannel Security Service Provider (SSP) vorgestellt, indem praktische Anwendungen, Änderungen in der Implementierung von Microsoft und Softwareanforderungen sowie zusätzliche Ressourcen für Windows Server 2012 und Windows 8 beschrieben werden.

## <a name="description"></a><a name="BKMK_OVER"></a>BESCHREIBUNG
Schannel ist ein Sicherheitsdienstanbieter (Security Support Provider, SSP), der die Internet-Standardauthentifizierungsprotokolle SSL (Secure Sockets Layer) und TSL (Transport Layer Security) implementiert.

Die Security Support Provider-Schnittstelle (Security Support Provider Interface, SSPI) ist eine API, die von Windows-Systemen verwendet wird, um sicherheitsbezogene Funktionen wie Authentifizierungen durchzuführen. Die SSPI fungiert als gemeinsame Schnittstelle für mehrere SSPs, einschließlich des Schannel SSP.

Die TLS-Versionen 1,0, 1,1 und 1,2, die SSL-Versionen 2,0 und 3,0 sowie das Datagramm Transport Layer Security \( DTLS- \) Protokollversion 1,0 und das PCT-Protokoll des privaten Kommunikations Transports \( \) basieren auf der Kryptografie mit öffentlichem Schlüssel. Die Schannel-Authentifizierungsprotokollsammlung enthält diese Protokolle. Alle Schannel-Protokolle verwenden ein Client/Server-Modell.

## <a name="applications"></a><a name="BKMK_APP"></a>Anwendungen
Ein Problem bei der Netzwerkverwaltung ist der Schutz von Daten, die zwischen Anwendungen über ein nicht vertrauenswürdiges Netzwerk gesendet werden. Sie können TLS und SSL zum Authentifizieren von Servern und Client Computern verwenden und dann das Protokoll verwenden, um Nachrichten zwischen den authentifizierten Parteien zu verschlüsseln.

Sie können TLS/SSL beispielsweise für Folgendes verwenden:

-   SSL-gesicherte Transaktionen mit einer E-Commerce-Website
-   Authentifizierten Clientzugriff auf einer SSL-gesicherten Website
-   Remotezugriff
-   SQL-Zugriff
-   E-Mail

## <a name="requirements"></a><a name="BKMK_SOFT"></a>Requirements (Anforderungen)
TLS-und SSL-Protokolle verwenden ein Client/Server-Modell und basieren auf der Zertifikat Authentifizierung, die eine Public Key-Infrastruktur erfordert.

## <a name="server-manager-information"></a><a name="BKMK_INSTALL"></a>Informationen zum Server-Manager
Zum Implementieren von TLS, SSL oder SChannel sind keine Konfigurationsschritte erforderlich.

## <a name="additional-references"></a>Weitere Verweise ##

-   [Das Schannel-Sicherheitspaket](/windows/desktop/com/schannel)
-   [Secure Channel](/windows/desktop/SecAuthN/secure-channel)
-   [Transport Layer Security-Protokoll](/windows/desktop/SecAuthN/transport-layer-security-protocol)