---
title: RADIUS-Clients
description: Dieses Thema enthält einen Überblick über RADIUS-Clients für Netzwerkrichtlinienserver unter Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d3a09ac9-75f8-4f57-aab4-b0fdfe110118
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fdca45237d971c1b2e08443112b63d3ce77e4a2d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874311"
---
# <a name="radius-clients"></a>RADIUS-Clients

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Network Access Server \(NAS\) ist ein Gerät, das Zugriff auf ein größeres Netzwerk bereitstellt. Eine RADIUS-Infrastruktur NAS ist auch ein RADIUS-Client, senden verbindungsanforderungen und Kontoführungsnachrichten an einen RADIUS-Server für die Authentifizierung, Autorisierung und ressourcenerfassung.

>[!NOTE]
>Clientcomputer, z. B. Laptops und andere Computer mit Clientbetriebssystemen, sind keine RADIUS-Clients. RADIUS-Clients sind Netzwerkzugriffsserver – z. B. Drahtloszugriffspunkte, 802.1X-Authentifizierungsswitches, virtuelles privates Netzwerk \(VPN\) -Server und DFÜ-Server – da sie das RADIUS-Protokoll verwenden, für die Kommunikation mit RADIUS Server wie Network Policy Server \(NPS\) Server.

Um NPS als RADIUS-Server oder einen RADIUS-Proxy bereitzustellen, müssen Sie die RADIUS-Clients in NPS konfigurieren.

## <a name="radius-client-examples"></a>Beispiele für die RADIUS-client

Beispiele für Netzwerkzugriffsserver sind:

- Network Access Server, die RAS-Verbindungen mit einem Unternehmensnetzwerk oder dem Internet bereitstellen. Ein Beispiel ist ein Computer unter dem Betriebssystem Windows Server 2016 der RAS-Dienst, der bietet entweder herkömmliche Einwählverbindung, oder virtuelles privates Netzwerk (VPN) von RAS-Dienste auf ein Organisationsintranet.
- Drahtlose Zugriffspunkte, die den Zugriff auf das Netzwerk einer Organisation, die über drahtlose übertragungs- und empfangstechnologien Technologien zu bieten.
- Switches, die den Zugriff auf das Netzwerk einer Organisation, mit der LAN-Technologien, z. B. Ethernet bereitstellen.
- RADIUS-Proxys, die Weiterleitung von verbindungsanforderungen an den RADIUS-Server weiterleiten, die einen remote-RADIUS-Servergruppe angehören, die auf dem RADIUS-Proxy konfiguriert ist.

## <a name="radius-access-request-messages"></a>RADIUS-Access-Request-Nachrichten

RADIUS-Clients entweder RADIUS-Access-Request-Nachrichten erstellen und an einen RADIUS-Proxy oder RADIUS-Server weitergeleitet werden, oder sie weiterleiten Access-Request-Nachrichten an einen RADIUS-Server, den sie von einem anderen RADIUS-Client erhalten haben, aber noch nicht selbst erstellt.

RADIUS-Clients verarbeiten durch Ausführen von Authentifizierung, Autorisierung und Kontoführung nicht Access-Request-Nachrichten. Nur die RADIUS-Servern führen Sie diese Funktionen.

NPS, kann jedoch als RADIUS-Proxy und einem RADIUS-Server gleichzeitig konfiguriert werden, damit sie eine Access-Request-Nachrichten verarbeitet und anderen Meldungen weiterleitet.

## <a name="nps-as-a-radius-client"></a>NPS als RADIUS-client

NPS fungiert als RADIUS-Client, wenn Sie es als RADIUS-Proxy zum Weiterleiten von Access-Request-Nachrichten an andere RADIUS-Server für die Verarbeitung konfigurieren. Wenn Sie NPS als RADIUS-Proxy verwenden, sind die folgenden allgemeinen Konfigurationsschritte erforderlich:

1. Netzwerkzugriffsserver, z. B. drahtlose Zugriffspunkte und VPN-Server, werden mit der IP-Adresse des NPS-Proxys als die angegebenen RADIUS-Server oder der authentifizierenden Server konfiguriert. Dadurch wird die Netzwerkzugriffsserver, die Access-Request-Nachrichten basierend auf Informationen, dass der Erhalt von Access-Clients zum Weiterleiten von Nachrichten an den NPS-Proxy erstellen.

2. Der NPS-Proxy wird durch Hinzufügen von jeden Netzwerkzugriffsserver als RADIUS-Client konfiguriert. Dieser Konfigurationsschritt ermöglicht den NPS-Proxy zum Empfangen von Nachrichten aus der Netzwerkzugriffsserver zuzugreifen und mit ihnen in der gesamten Authentifizierung zu kommunizieren. Darüber hinaus sind Verbindungsanforderungsrichtlinien auf dem NPS-Proxy festlegen, welche Access-Request-Nachrichten zum Weiterleiten an einen oder mehrere RADIUS-Server konfiguriert. Diese Richtlinien sind auch mit einem remote-RADIUS-Servergruppe, konfiguriert, die NPS darüber informiert, wohin die Nachrichten an, dass er von der Netzwerkzugriffsserver empfängt gesendet.

3. Der NPS oder andere RADIUS-Server, die auf dem NPS-Proxy die remote-RADIUS-Servergruppe angehören, werden zum Empfangen von Nachrichten vom NPS-Proxy konfiguriert. Dies erfolgt durch den Proxy NPS als RADIUS-Client konfigurieren.

## <a name="radius-client-properties"></a>Eigenschaften von RADIUS-client

Wenn Sie einen RADIUS-Client mit der NPS-Konfiguration über die NPS-Konsole oder das Netsh-Befehle für Netzwerkrichtlinienserver oder Windows PowerShell-Befehle hinzufügen, werden Sie NPS zum Empfangen von RADIUS-Access-Request-Nachrichten von einem Network Access Server konfigurieren oder ein RADIUS-Proxy.

Wenn Sie einen RADIUS-Client in NPS konfigurieren, können Sie die folgenden Eigenschaften festlegen:

### <a name="client-name"></a>Clientname

 Ein Anzeigename für den RADIUS-Client, dadurch wird es leichter zu identifizieren, wenn Sie die NPS-Snap-Ins oder Netsh-Befehle für den NPS zu verwenden.

### <a name="ip-address"></a>IP-Adresse

Internetprotokoll, Version 4 \(IPv4\) Adresse oder den Domain Name System \(DNS\) Name des RADIUS-Clients.

### <a name="client-vendor"></a>Client-Vendor

Der Hersteller des RADIUS-Clients. Andernfalls können Sie den RADIUS-Standardwert für Client-Anbieter.

### <a name="shared-secret"></a>Gemeinsamer geheimer Schlüssel

Eine Textzeichenfolge, die als Kennwort zwischen RADIUS-Clients, RADIUS-Server und RADIUS-Proxys verwendet wird. Wenn das Attribut für die Nachrichtenauthentifizierung verwendet wird, ist der gemeinsame geheime Schlüssel auch als Schlüssel verwendet, um RADIUS-Nachrichten zu verschlüsseln. Diese Zeichenfolge muss auf dem RADIUS-Client und der NPS-Snap-in konfiguriert werden.

### <a name="message-authenticator-attribute"></a>Authenticator-Nachrichtenattribut

Beschrieben in RFC 2869, "RADIUS-Erweiterungen", ein Message Digest 5 \(MD5\) Hash der gesamten RADIUS-Nachricht. Wenn die Nachrichtenauthentifizierung für RADIUS-Attribut vorhanden ist, wird es überprüft. Wenn sie die Überprüfung fehlschlägt, wird die RADIUS-Nachricht verworfen. Wenn die Clienteinstellungen für die Nachrichtenauthentifizierung-Attribut ist erforderlich, und es nicht vorhanden ist, wird die RADIUS-Nachricht verworfen. Verwendung des Attributs Nachrichtenauthentifizierung wird empfohlen.

>[!NOTE]
>Das Attribut für die Nachrichtenauthentifizierung ist erforderlich, und standardmäßig aktiviert, wenn Sie Extensible Authentication-Protokoll verwenden \(EAP\) Authentifizierung. 

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).

