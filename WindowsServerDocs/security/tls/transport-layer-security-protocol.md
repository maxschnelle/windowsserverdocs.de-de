---
title: Transport Layer Security-Protokoll
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: de510bb0-a9f6-4bbe-8f8a-8dd7473bbae8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 94c81a79e5f3fd8fc22eafde3de8bd3d0bdd73f0
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# Transport Layer Security-Protokoll

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema für IT-Experten wird beschrieben, wie das Transport Layer Security (TLS)-Protokoll funktioniert und enthält Links zu den IETF-RFCs für TLS 1.0, TLS 1.1 und TLS 1.2.

Die Protokolle TLS (und SSL) befinden sich zwischen der Anwendungsschicht-Protokoll und die TCP/IP-Ebene, in dem sie sicherer und Anwendungsdaten auf der Transportebene senden können. Da die Protokolle zwischen der Anwendungsschicht und der Transportschicht arbeiten, kann mehrere Protokolle auf Anwendungsebene von TLS und SSL unterstützen.

TLS und SSL wird davon ausgegangen, dass ein verbindungsorientierte Transport, in der Regel TCP, verwendet wird. Das Protokoll ermöglicht Client- und Serveranwendungen die folgenden Sicherheitsrisiken erkennen:

-   Manipulation von Nachrichten

-   Nachricht abfangen

-   Nachrichtenfälschung

Die Protokolle TLS und SSL können in zwei Ebenen unterteilt werden. Die erste Ebene besteht aus des Anwendungsprotokolls und die drei Handshake: Handshake-Protokoll, die Spezifikation ändern Cipher-Protokoll und die Warnung Protokoll. Die zweite Ebene ist das datensatzprotokoll. Die folgende Abbildungzeigt die verschiedenen Ebenen und ihre Elemente.

**TLS und SSL-Protokoll-Ebenen**


Der Schannel-SSP implementiert die Protokolle TLS und SSL unverändert. Das SSL-Protokoll ist eine proprietäre, aber der Internet Engineering Task Force erzeugt die öffentlichen TLS-Spezifikationen. Informationen über die TLS / SSL-Version wird in Windows-Versionen unterstützt, finden Sie unter [Protokolle TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/en-us/library/windows/desktop/mt808159(v=vs.85).aspx). Die folgende Tabelle enthält die Spezifikationen für jede TLS-Version. Jede Spezifikation enthält folgende Informationen:

-   Die TLS-Datensatzprotokoll

-   Die TLS-Handshake-Protokolle: \-Änderung Cipher Spezifikation Protokoll \-Protokoll-Warnung

-   Kryptografische Berechnungen

-   Obligatorische-Verschlüsselungssammlungen

-   Application Data Protocol

[RFC 5246 - die Transport Layer Security (TLS) Protokoll, Version 1.2](http://tools.ietf.org/html/rfc5246)

[RFC 4346 - die Transport Layer Security (TLS)-Protokoll Version 1.1](http://tools.ietf.org/html/rfc4346)

[RFC 2246 – die TLS-Protokollversion 1.0](http://tools.ietf.org/html/rfc2246)

## <a name="BKMK_SessionResumption"></a>TLS-sitzungswiederaufnahme
In Windows Server2012 R2 eingeführt wurde, implementiert der Schannel SSP den serverseitigen Teil des TLS-sitzungswiederaufnahme. Die Implementierung der clientseitigen RFC 5077 wurde in Windows8 hinzugefügt.

Geräte, die TLS häufig mit Server verbinden, müssen eine Verbindung herzustellen. TLS-sitzungswiederaufnahme reduziert die Kosten für die TLS-Verbindungen herstellen, da die Wiederaufnahme einen abgekürzten TLS-Handshake beinhaltet. Dies erleichtert die weitere Wiederaufnahme Versuche in eigener Regie eine Gruppe von TLS-Servern des jeweils anderen TLS-Sitzung fortsetzen. Diese Änderung bietet die folgenden für TLS-Clients, die RFC 5077, einschließlich Windows Phone und Windows RT-Geräten unterstützt:

-   Reduzierter Ressourcenbedarf auf dem Server

-   Reduzierte Bandbreite und damit die Effizienz von Clientverbindungen verbessert

-   Geringere Dauer der TLS-Handshakes durch Wiederaufnahme der Verbindung

Informationen zur statusfreien TLS-sitzungswiederaufnahme finden Sie im IETF-Dokument [RFC 5077.](http://www.ietf.org/rfc/rfc5077)

## <a name="BKMK_AppProtocolNego"></a>Anwendungsprotokollverhandlung
 Windows Server2012 R2 und Windows8.1-Unterstützung, die clientseitige TLS-Anwendungsprotokolls ermöglicht. Anwendungen können Protokolle als Teil der Standard-HTTP-2.0-Entwicklung nutzen, und Benutzer Onlinedienste wie Google und Twitter mithilfe von Apps, die das SPDY-Protokoll ausgeführt zugreifen können.

Informationen zur Funktionsweise der anwendungsprotokollverhandlung finden Sie unter [Transport Layer Security (TLS) Application Layer Protocol Negotiation Extension](http://tools.ietf.org/search/draft-ietf-tls-applayerprotoneg-05).

## <a name="BKMK_SNI"></a>TLS-Unterstützung für Server Name Indication Erweiterungen
Das Feature (Server Name Indication, SNI) erweitert die SSL- und TLS-Protokolle, um die richtige Identifizierung des Servers zulassen, wenn zahlreiche virtuelle Abbilder auf einem einzelnen Server ausgeführt werden. Bei virtuellen hostszenarios werden mehrere Domänen (jede über ein eigenes Zertifikat verfügt) auf einem Server gehostet. In diesem Fall hat der Server keine Möglichkeit, im Voraus wissen, welches Zertifikat er an den Client gesendet. Dank SNI kann des Clients die Zieldomäne weiter oben im Protokoll informieren, und der Server das richtige Zertifikat auswählen kann.

Die folgende zusätzliche Funktionalität:

-   Ermöglicht es Ihnen, mehrere SSL-Websites auf einem einzelnen Internetprotokoll und Portkombination hosten

-   Verringert die Speicherauslastung, wenn mehrere SSL-Websites auf einem einzelnen Webserver gehostet werden

-   Können mehrere Benutzer gleichzeitig eine Verbindung zu SSL-Websites herstellen



