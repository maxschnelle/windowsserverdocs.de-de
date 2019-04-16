---
title: RADIUS-Clients
description: Dieses Thema enthält eine Übersicht über RADIUS-Clients für Netzwerkrichtlinienserver in Windows Server2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d3a09ac9-75f8-4f57-aab4-b0fdfe110118
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a970dabcc6f3f4fc4d8ed5a0dedd01b5a7dee71a
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="radius-clients"></a>RADIUS-Clients

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Netzwerkserver \(NAS\) ist ein Gerät, das einige Zugriffsrechte auf einem größeren Netzwerk bereitstellt. Ein NAS eine RADIUS-Infrastruktur ist auch ein RADIUS-Client, Senden von Verbindungsanforderungen und Kontoführungsnachrichten an einen RADIUS-Server für die Authentifizierung, Autorisierung und Kontoführung.

>[!NOTE]
>Clientcomputer, z.B. Laptops und andere Computer mit Clientbetriebssystemen, sind keine RADIUS-Clients. RADIUS-Clients sind Netzwerkzugriffsserver – z.B. Drahtloszugriffspunkte, 802.1X-Authentifizierungsswitches, VPN-\(VPN\) Servern und DFÜ-Server -, da sie das RADIUS-Protokoll zur Kommunikation mit RADIUS-Servern, z.B. Netzwerkrichtlinienserver \(NPS\) verwenden.

Wenn Sie NPS als RADIUS-Server oder RADIUS-Proxy bereitstellen, müssen Sie RADIUS-Clients in NPS konfigurieren.

## <a name="radius-client-examples"></a>Beispiele für die RADIUS-Client

Beispiele für Netzwerkzugriffsserver sind:

- Netzwerkzugriffsserver, die RAS-Konnektivität mit einem Unternehmensnetzwerk oder dem Internet zu ermöglichen. Ein Beispiel ist ein Computer unter dem Betriebssystem Windows Server2016 und der RAS-Dienst, der entweder herkömmliche DFÜ-bereitstellt oder virtuelles privates Netzwerk (VPN) RAS-Dienste auf ein Organisationsintranet.
- Drahtlose Zugriffspunkte, die den Zugriff auf das Netzwerk einer Organisation mit WLAN-basierte sendet und empfängt Technologien bereitstellen.
- Switches den Zugriff auf das Netzwerk einer Organisation ermöglichen, mit herkömmlichen LAN-Technologien, wie z.B. Ethernet.
- RADIUS-Proxys, die Verbindungsanforderungen an RADIUS-Server weitergeleitet, die Mitglieder einer RADIUS-Remoteservergruppe sind, die auf dem RADIUS-Proxy konfiguriert ist.

## <a name="radius-access-request-messages"></a>RADIUS-Zugriffsanforderung Nachrichten

RADIUS-Clients RADIUS-Zugriffsanforderung Nachrichten erstellen und diese an einen RADIUS-Proxy oder RADIUS-Server weiterleiten, sie Nachrichten oder Weiterleiten Access-Anforderung an einen RADIUS-Server, den sie einen anderen RADIUS-Client empfangen haben, jedoch nicht selbst erstellt.

RADIUS-Clients verarbeiten keine Access-Anforderungsnachrichten durch Ausführen der Authentifizierung, Autorisierung und Kontoführung. RADIUS-Server führen Sie diese Funktionen.

NPS, können jedoch als RADIUS-Proxy und RADIUS-Server gleichzeitig konfiguriert werden, damit einige Nachrichten Access-Anforderung verarbeitet und andere Nachrichten weitergeleitet.

## <a name="nps-as-a-radius-client"></a>NPS als RADIUS-Client

NPS fungiert als RADIUS-Client, wenn Sie es als RADIUS-Proxy-Zugriffsanforderung Nachrichten an andere RADIUS-Server für die Verarbeitung weiterleiten konfigurieren. Wenn Sie NPS als RADIUS-Proxy verwenden, sind die folgenden allgemeinen Konfigurationsschritte erforderlich:

1. Netzwerkzugriffsserver, z.B. drahtlose Zugriffspunkte und VPN-Server, werden die IP-Adresse des NPS-Proxy als angegebenen RADIUS-Server oder der authentifizierende Server konfiguriert. Dies ermöglicht die Netzwerkzugriffsserver, die Access-Anforderungsnachrichten anhand der Informationen, dass sie von Access-Clients zum Weiterleiten von Nachrichten an den NPS-Proxy empfangen erstellen.

2. Der NPS-Proxy konfiguriert ist, indem Sie jeden Netzwerkzugriffsserver als RADIUS-Client hinzufügen. Dieser Konfigurationsschritt ermöglicht den NPS-Proxy zum Empfangen von Nachrichten aus den Netzwerkzugriffsservern und in der gesamten Authentifizierung mit ihnen kommunizieren. Darüber hinaus werden Verbindungsanforderungsrichtlinien auf dem NPS-Proxy konfiguriert, um anzugeben, welche Meldungen Access-Anforderung an einen oder mehrere RADIUS-Server weitergeleitet. Diese Richtlinien sind auch mit einem RADIUS-Remoteservergruppe, konfiguriert, die NPS darüber informiert werden, wo Sie von den Netzwerkzugriffsservern empfangenen Nachrichten gesendet.

3. Der NPS oder andere RADIUS-Server, die Mitglieder der RADIUS-Remoteservergruppe auf dem NPS-Proxy sind sind zum Empfangen von Nachrichten aus der NPS-Proxy konfiguriert. Dies geschieht durch Konfigurieren des NPS-Proxys als RADIUS-Client.

## <a name="radius-client-properties"></a>Eigenschaften von RADIUS-Client

Wenn Sie einen RADIUS-Client für die NPS-Konfiguration über die NPS-Konsole oder durch die Verwendung der Netsh-Befehle für Netzwerkrichtlinienserver oder Windows PowerShell-Befehle hinzufügen, konfigurieren Sie NPS zum Empfangen von RADIUS-Zugriffsanforderung Nachrichten von einem Netzwerkzugriffsserver oder RADIUS-Proxy.

Wenn Sie einen RADIUS-Client in NPS konfigurieren, können Sie die folgenden Eigenschaften festlegen:

### <a name="client-name"></a>Client-Name

 Einen Anzeigenamen für den RADIUS-Client, wodurch es leichter zu identifizieren, wenn Sie die NPS-Snap-In oder Netsh-Befehle für den NPS verwenden.

### <a name="ip-address"></a>IP-Adresse

Das Internet Protocol Version 4 \(IPv4\) oder der Domain Name System \(DNS\) Name des RADIUS-Clients.

### <a name="client-vendor"></a>Client-Anbieter

Der Hersteller des RADIUS-Clients. Andernfalls können Sie den RADIUS-Standardwert für Client-Hersteller.

### <a name="shared-secret"></a>Gemeinsamen geheimen Schlüssel

Eine Textzeichenfolge, die als Kennwort zwischen RADIUS-Clients, RADIUS-Server und RADIUS-Proxys verwendet wird. Wenn das Attribut Nachrichtenauthentifizierung verwendet wird, ist der gemeinsame geheime Schlüssel auch zum Verschlüsseln von RADIUS-Nachrichten als Schlüssel verwendet. Diese Zeichenfolge muss auf dem RADIUS-Client und dem NPS-Snap-In konfiguriert werden.

### <a name="message-authenticator-attribute"></a>Nachricht Authentifikator-Attribut

Beschrieben in RFC 2869, "RADIUS-Erweiterungen", ein Hash Message Digest 5 \(MD5\) der gesamten RADIUS-Nachricht. Wenn der Nachrichtenauthentifizierung RADIUS-Attribut vorhanden ist, wird es überprüft. Wenn die Überprüfung fehlschlägt, wird die RADIUS-Meldung verworfen. Wenn die Clienteinstellungen das Nachrichtenauthentifizierung-Attribut erfordern nicht vorhanden ist, wird die RADIUS-Meldung verworfen. Die Verwendung des Attributs Nachrichtenauthentifizierung wird empfohlen.

>[!NOTE]
>Der Nachrichtenauthentifizierung-Attribut ist erforderlich und standardmäßig aktiviert, wenn Sie die Extensible Authentication Protocol \(EAP\)-Authentifizierung verwenden. 

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).

