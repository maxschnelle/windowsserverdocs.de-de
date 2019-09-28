---
title: TLS-Protokoll (Transport Layer Security)
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: aca2db3ae5bf424dd0f855d24c1ef771039c8b14
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403373"
---
# <a name="transport-layer-security-protocol"></a>TLS-Protokoll (Transport Layer Security)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows 10

In diesem Thema für IT-Experten wird beschrieben, wie das Transport Layer Security (TLS)-Protokoll funktioniert und Links zu den IETF-RFCs für TLS 1,0, TLS 1,1 und TLS 1,2 bereitstellt.

Die TLS-(und SSL-) Protokolle befinden sich zwischen der Anwendungsprotokoll Ebene und der TCP/IP-Schicht, wo Sie Anwendungsdaten sichern und an die Transportschicht senden können. Da die Protokolle zwischen der Anwendungsschicht und der Transportschicht funktionieren, können TLS und SSL mehrere Protokolle auf Anwendungsebene unterstützen.

TLS und SSL nehmen an, dass ein Verbindungs orientierter Transport (in der Regel TCP) verwendet wird. Das Protokoll ermöglicht Client-und Server Anwendungen, die folgenden Sicherheitsrisiken zu erkennen:

-   Manipulation von Nachrichten

-   Abfangen der Nachricht

-   Nachrichten Fälschung

Die TLS-und SSL-Protokolle können in zwei Ebenen unterteilt werden. Die erste Ebene besteht aus dem Anwendungsprotokoll und den drei Hand Shake-Protokollen: dem Handshake-Protokoll, dem Änderungs Verschlüsselungsprotokoll und dem Warnungs Protokoll. Die zweite Ebene ist das Daten Satz Protokoll. In der folgenden Abbildung werden die verschiedenen Ebenen und ihre Elemente veranschaulicht.

**TLS-und SSL-Protokoll Ebenen**


Der Schannel-SSP implementiert die TLS-und SSL-Protokolle ohne Änderungen. Das SSL-Protokoll ist proprietär, aber die Internet Engineering Task Force erstellt die öffentlichen TLS-Spezifikationen. Informationen dazu, welche TLS-oder SSL-Version in Windows-Versionen unterstützt wird, finden Sie unter [Protokolle in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159(v=vs.85).aspx). In der folgenden Tabelle sind die Spezifikationen für jede TLS-Version aufgeführt. Jede Spezifikation enthält Informationen zu folgenden Informationen:

-   Das TLS-Daten Satz Protokoll

-   Die TLS-Handshaking-Protokolle: \--Protokoll für Protokoll \--Warnung

-   Kryptografische Berechnungen

-   Obligatorische Verschlüsselungs Sammlungen

-   Anwendungsdaten Protokoll

[RFC 5246-die Transport Layer Security (TLS)-Protokoll Version 1,2](http://tools.ietf.org/html/rfc5246)

[RFC 4346-die Transport Layer Security (TLS)-Protokoll Version 1,1](http://tools.ietf.org/html/rfc4346)

[RFC 2246-TLS-Protokoll, Version 1,0](http://tools.ietf.org/html/rfc2246)

## <a name="BKMK_SessionResumption"></a>TLS-Sitzungs Wiederaufnahme
Der Schannel SSP wurde in Windows Server 2012 R2 eingeführt und implementierte den Server seitigen Teil der Wiederaufnahme der TLS-Sitzung. Die Client seitige Implementierung von RFC 5077 wurde in Windows 8 hinzugefügt.

Geräte, die TLS-Verbindungen mit Servern herstellen, müssen die Verbindung häufig wiederherstellen. Durch die Wiederaufnahme der TLS-Sitzung werden die Kosten für das Einrichten von TLS-Verbindungen reduziert, da die Wiederaufnahme einen Dadurch wird eine größere Anzahl von Wiederholungs versuchen ermöglicht, da eine Gruppe von TLS-Servern die TLS-Sitzungen der anderen Gruppe wieder aufnehmen kann. Diese Änderung bietet die folgenden Einsparungen für jeden TLS-Client, der RFC 5077 unterstützt, einschließlich Windows Phone und Windows RT-Geräten:

-   Reduzierter Ressourcenbedarf auf dem Server

-   Reduzierte Bandbreite und damit verbesserte Effizienz von Clientverbindungen

-   Reduzierte Zeit für den TLS-Handshake aufgrund von Fort Läufen der Verbindung

Informationen zur Zustands losen Wiederaufnahme der TLS-Sitzung finden Sie im IETF-Dokument [RFC 5077.](http://www.ietf.org/rfc/rfc5077)

## <a name="BKMK_AppProtocolNego"></a>Anwendungsprotokoll Aushandlung
 In Windows Server 2012 R2 und Windows 8.1 wurde Unterstützung eingeführt, die die Client seitige TLS-Anwendungsprotokoll Aushandlung ermöglicht. Anwendungen können Protokolle als Teil der http 2,0-Standardentwicklung nutzen, und Benutzer können auf Onlinedienste z. b. Google und Twitter zugreifen, indem Sie Apps verwenden, die das SPDY-Protokoll ausführen.

Weitere Informationen zur Funktionsweise der Anwendungsprotokoll Aushandlung finden Sie unter [Transport Layer Security (TLS) Application Layer Protocol](http://tools.ietf.org/search/draft-ietf-tls-applayerprotoneg-05)Aushandlungs Erweiterung.

## <a name="BKMK_SNI"></a>TLS-Unterstützung für Servernamensanzeige-Erweiterungen
Das SNI-Feature stellt eine Erweiterung der Protokolle SSL und TLS dar und ermöglicht die richtige Identifizierung des Servers, wenn zahlreiche virtuelle Abbilder auf einem einzelnen Server ausgeführt werden. In einem virtuellen Hostingszenario werden mehrere Domänen (die jeweils über ein eigenes potenziell unterschiedliches Zertifikat verfügen) auf einem Server gehostet. In diesem Fall kann der Server nicht im Voraus wissen, welches Zertifikat an den Client gesendet werden soll. SNI ermöglicht es dem Client, die Zieldomäne weiter oben im Protokoll zu informieren. Dies ermöglicht es dem Server, das richtige Zertifikat ordnungsgemäß auszuwählen.

Die folgende zusätzliche Funktionalität:

-   Ermöglicht das Hosten mehrerer SSL-Websites in einer einzelnen Internet Protokoll-und Port Kombination.

-   Der Speicherbedarf wird reduziert, wenn mehrere SSL-Websites auf einem einzelnen Webserver gehostet werden.

-   Ermöglicht mehr Benutzern das gleichzeitige Herstellen von Verbindungen mit SSL-Websites



