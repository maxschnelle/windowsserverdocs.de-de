---
title: TLS-Protokoll (Transport Layer Security)
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: de510bb0-a9f6-4bbe-8f8a-8dd7473bbae8
author: justinha
ms.author: justinha
manager: brianlic-msft
ms.date: 05/16/2018
ms.openlocfilehash: 77e3ee9d89bff7ab6e95ea47ffa141e6e1004ba4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853021"
---
# <a name="transport-layer-security-protocol"></a>TLS-Protokoll (Transport Layer Security)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10

In diesem Thema für IT-Experten wird beschrieben, wie das Protokoll Transport Layer Security (TLS) funktioniert, und enthält Links zu den IETF-RFCs für TLS 1.0, TLS 1.1 und TLS 1.2.

Die Protokolle TLS (und SSL) befinden sich zwischen der Anwendungsschicht-Protokoll und die TCP/IP-Ebene, in dem sie schützen und Anwendungsdaten an die Transportschicht gesendet. Da zwischen der Anwendungsebene und der Transportschicht die Protokolle arbeiten, können mehrere Protokolle auf Anwendungsebene von TLS und SSL unterstützen.

TLS und SSL wird davon ausgegangen, dass es sich bei ein verbindungsorientierten Transport, in der Regel TCP-Protokoll verwendet wird. Das Protokoll ermöglicht Client- und serveranwendungen, um den folgenden Sicherheitsrisiken zu erkennen:

-   Eine Manipulation der Nachricht

-   Der Nachrichtenabfangfunktion

-   Nachrichtenfälschung

Die Protokolle TLS und SSL können in zwei Ebenen unterteilt werden. Die erste Ebene besteht aus dem Anwendungsprotokoll und drei Protokolle, die Handshake: die Handshake-Protokoll, das Änderung Cipher Spec-Protokoll und das alert-Protokoll. Die zweite Ebene ist das datensatzprotokoll. Die folgende Abbildung veranschaulicht die verschiedenen Ebenen und die zugehörigen Elemente.

**TLS und SSL-Protokollebenen**


Der Schannel-SSP implementiert die Protokolle TLS und SSL, ohne Änderungen. Das SSL-Protokoll ist eine proprietäre, aber der Internet Engineering Task Force, erzeugt die öffentlichen TLS-Spezifikationen. Informationen dazu, welcher TLS oder SSL-Version wird in Windows-Versionen unterstützt, finden Sie unter [Protokolle in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/en-us/library/windows/desktop/mt808159(v=vs.85).aspx). Die folgende Tabelle enthält die Spezifikationen für jeden TLS-Version. Jeder Spezifikation enthält folgende Informationen:

-   Die TLS-Datensatzprotokoll

-   Die TLS-Handshake-Protokolle: \- Ändern von Cipher Spec Protokoll \- Warnung Protokoll

-   Kryptografische Berechnungen

-   Obligatorische Verschlüsselungssammlungen

-   Daten-Anwendungsprotokoll

[RFC 5246 - die Transport Layer Security (TLS)-Protokollversion 1.2](http://tools.ietf.org/html/rfc5246)

[RFC 4346 - die Transport Layer Security (TLS) Protokoll, Version 1.1](http://tools.ietf.org/html/rfc4346)

[RFC 2246 – die TLS-Protokollversion 1.0](http://tools.ietf.org/html/rfc2246)

## <a name="BKMK_SessionResumption"></a>TLS-sitzungswiederaufnahme
In Windows Server 2012 R2 eingeführt wurde, implementiert der Schannel SSP den serverseitigen Teil der TLS-sitzungswiederaufnahme. Die Implementierung der clientseitigen RFC 5077 wurde in Windows 8 hinzugefügt.

Geräte, die TLS-Verbindungen mit Servern herstellen, müssen die Verbindung häufig wiederherstellen. TLS-sitzungswiederaufnahme reduziert die Kosten für die TLS-Verbindungen herstellen, da der Wiederaufnahme einen abgekürzten TLS-Handshake umfasst. Dies ermöglicht größere Anzahl indem eine Gruppe von TLS-Servern zum Fortsetzen der gegenseitigen TLS-Sitzungen. Diese Änderung bietet die folgenden einsparungen für jeden TLS-Client, der RFC 5077, einschließlich Windows Phone und Windows RT-Geräte unterstützt:

-   Reduzierter Ressourcenbedarf auf dem Server

-   Reduzierte Bandbreite und damit verbesserte Effizienz von Clientverbindungen

-   Geringere Dauer der TLS-Handshakes durch Wiederaufnahme der Verbindung

Informationen zur statusfreien TLS-sitzungswiederaufnahme finden Sie im IETF-Dokument [RFC 5077.](http://www.ietf.org/rfc/rfc5077)

## <a name="BKMK_AppProtocolNego"></a>Anwendungsprotokollverhandlung
 Windows Server 2012 R2 und Windows 8.1-Unterstützung, die die clientseitige TLS-anwendungsprotokollverhandlung ermöglicht. Anwendungen können Protokolle nutzen, als Teil der standard-HTTP-2.0-Entwicklung, und Benutzer können Onlinedienste wie Google und Twitter mithilfe von apps, die das SPDY-Protokoll zugreifen.

Weitere Informationen zur Funktionsweise der anwendungsprotokollverhandlung finden Sie unter [Transport Layer Security (TLS) Application Layer Protocol Negotiation Extension](http://tools.ietf.org/search/draft-ietf-tls-applayerprotoneg-05).

## <a name="BKMK_SNI"></a>TLS-Unterstützung für Server Name Indication-Erweiterungen
Das SNI-Feature stellt eine Erweiterung der Protokolle SSL und TLS dar und ermöglicht die richtige Identifizierung des Servers, wenn zahlreiche virtuelle Abbilder auf einem einzelnen Server ausgeführt werden. In einem virtuellen hostszenarios werden mehrere Domänen (jedes mit eigenen Zertifikat) auf einem Server gehostet. In diesem Fall kann der Server nicht im Voraus wissen, welches Zertifikat er an den Client gesendet. Dank SNI kann des Clients die Zieldomäne weiter oben in das Protokoll zu informieren, und der Server das richtige Zertifikat auswählen kann.

Die folgende zusätzliche Funktionalität:

-   Ermöglicht es Ihnen, mehrere SSL-Websites auf einem einzelnen Internet-Protokoll und Port-Kombination zu hosten.

-   Der Speicherbedarf wird reduziert, wenn mehrere SSL-Websites auf einem einzelnen Webserver gehostet werden.

-   Können mehrere Benutzer gleichzeitig mit SSL-Websites zu verbinden



