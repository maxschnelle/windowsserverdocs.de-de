---
title: Verarbeitung von Verbindungsanforderungen
description: Dieses Thema enthält einen Überblick über die Netzwerkrichtlinienserver-verbindungsanforderung, die Verarbeitung in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 849d661a-42c1-4f93-b669-6009d52aad39
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6ab08dced15cfadd5a0fc773efc2ddaa2da24c08
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829111"
---
# <a name="connection-request-processing"></a>Verarbeitung von Verbindungsanforderungen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, Informationen zu verbindungsanforderung, die Verarbeitung in der Netzwerkrichtlinienserver unter Windows Server 2016.

>[!NOTE]
>Zusätzlich zu diesem Thema ist die folgenden verbindungsanforderung verarbeitet der Dokumentation verfügbar.
> - [Verbindungsanforderungsrichtlinien](nps-crp-crpolicies.md)
> - [Bereichsnamen](nps-crp-realm-names.md)
> - [Remote-RADIUS-Servergruppen](nps-crp-rrsg.md)

Sie können verbindungsanforderungsverarbeitung verwenden, um anzugeben, in dem die Authentifizierung der verbindungsanforderungen durchgeführt wird, auf dem lokalen Computer oder einen RADIUS-Remoteserver, der Mitglied einer remote-RADIUS-Servergruppe -. 

Wenn Sie den lokalen Server (Network Policy Server, NPS) zum Durchführen der Authentifizierung für die Weiterleitung von verbindungsanforderungen ausführen möchten, können Sie die Standard-Verbindungsanforderungsrichtlinie ohne zusätzliche Konfiguration. NPS basierend auf der Standardrichtlinie, authentifiziert werden, Benutzer und Computer, auf denen ein Konto in der lokalen Domäne und in vertrauenswürdigen Domänen.

Wenn Sie die Weiterleitung von verbindungsanforderungen an einen Remoteserver NPS oder anderen RADIUS-Server weiterleiten möchten, erstellen Sie eine remote-RADIUS-Servergruppe, und Konfigurieren einer Verbindungsanforderungsrichtlinie, die Anforderungen an diese remote-RADIUS-Server-Gruppe weiterleitet. Mit dieser Konfiguration können NPS können authentifizierungsanforderungen an RADIUS-Server weiterleiten, und Benutzer mit Konten in nicht vertrauenswürdigen Domänen authentifiziert werden können.

Die folgende Abbildung zeigt den Pfad einer Access-Request-Nachricht von einem Netzwerkserver für den Zugriff auf einen RADIUS-Proxy und dann an einen RADIUS-Server in einer remote-RADIUS-Servergruppe an. Klicken Sie auf den RADIUS-Proxy wird Network Access Server als RADIUS-Client konfiguriert; und der RADIUS-Proxy wird auf jedem RADIUS-Server als RADIUS-Client konfiguriert.


![Verarbeitung der NPS-Verbindungsanforderung](../../media/Nps-Connection-Request-Processing/Nps-Connection-Request-Processing.jpg)


>[!NOTE]
>Die Netzwerkzugriffsserver, die Verwendung mit NPS möglich Gatewaygeräte, die mit dem RADIUS-Protokoll, z. B. 802.1X-authentifizierten drahtlosen Zugriffspunkten und authentifizierenden Switches, Ausführen des Remotezugriffs, die wie VPN konfiguriert sind oder DFÜ-Server, kompatibel sind oder anderen RADIUS-kompatiblen Geräten.

Wenn Sie NPS, um einige authentifizierungsanforderungen beim Weiterleiten von anderen Anforderungen an einer remote-RADIUS-Servergruppe lokal zu verarbeiten möchten, konfigurieren Sie mehr als eine Verbindungsanforderungsrichtlinie.

Um eine Verbindungsanforderungsrichtlinie zu konfigurieren, die angibt, welche NPS oder RADIUS-Server-Gruppe authentifizierungsanforderungen verarbeitet, finden Sie unter "Verbindungsanforderungsrichtlinien".

Um anzugeben, NPS- oder andere RADIUS-Server, an die Authentifizierung Anforderungen weitergeleitet werden, finden Sie unter "RADIUS-Remoteservergruppen".

## <a name="nps-as-a-radius-server-connection-request-processing"></a>NPS als verbindungsanforderungsverarbeitung ein RADIUS-server

Wenn Sie NPS als RADIUS-Server verwenden, geben Sie RADIUS-Nachrichten-Authentifizierung, Autorisierung und Kontoführung für Verbindungen mit Netzwerken den Zugriff auf folgende Weise:

1. Zugriffsserver, z. B. DFÜ-Netzwerk-Zugriffsserver, VPN-Server und Drahtloszugriffspunkte, empfangen verbindungsanforderungen von Zugriffsclients. 

2. Der Zugriffsserver, der so konfiguriert, dass für die Verwendung von RADIUS als die Authentifizierung, Autorisierung und Kontoführungsprotokoll, erstellt eine Access-Request-Nachricht und sendet sie an den NPS. 

3. Der NPS wertet die Access-Request-Nachricht. 

4. Falls erforderlich, sendet der NPS eine Access-Challenge-Nachricht an den Zugriffsserver. Der Zugriffsserver verarbeitet die Abfrage und sendet eine aktualisierte Access-Request an den NPS. 

5. Die Anmeldeinformationen des Benutzers werden überprüft, und die Einwähleigenschaften des Benutzerkontos werden abgerufen, indem Sie über eine sichere Verbindung zu einem Domänencontroller. 

6. Der Verbindungsversuch wird mit der Einwähleigenschaften des Benutzerkontos und Netzwerkrichtlinien autorisiert. 

7. Wenn der Verbindungsversuch authentifiziert und autorisiert ist, sendet der NPS eine Access-Accept-Nachricht an den Zugriffsserver. Wenn der Verbindungsversuch entweder nicht authentifiziert oder nicht autorisiert, sendet der NPS eine Access-Reject-Nachricht an den Zugriffsserver. 

8. Der Zugriffsserver den Verbindungsprozess mit dem Zugriffsclient abgeschlossen und sendet eine Accounting-Request-Nachricht an den NPS, in dem die Meldung protokolliert wird. 

9. Der NPS sendet eine Accounting-Response an den Zugriffsserver. 

>[!NOTE]
>Der Access-Server sendet Accounting-Request-Nachrichten auch während des Zeitraums, in dem die Verbindung hergestellt wird, wenn die Access-Client-Verbindung geschlossen wird und wenn die Access-Server gestartet oder beendet wird.

## <a name="nps-as-a-radius-proxy-connection-request-processing"></a>NPS als ein RADIUS-Proxy-verbindungsanforderungsverarbeitung

Wenn NPS als RADIUS-Proxy zwischen RADIUS-Client und RADIUS-Server verwendet wird, auf RADIUS-Nachrichten für das Netzwerk Verbindung, die Versuche, wie folgt weitergeleitet werden zugreifen:

1. Zugriffsserver, z. B. DFÜ-Netzwerk-Zugriffsserver, virtuelles privates Netzwerk (VPN)-Server und Drahtloszugriffspunkte, empfangen verbindungsanforderungen von Zugriffsclients.

2. Der Zugriffsserver, der so konfiguriert, dass RADIUS als die Authentifizierung, Autorisierung und Kontoführungsprotokoll verwenden, erstellt eine Access-Request-Nachricht und sendet sie an den NPS, der als der NPS RADIUS-Proxy verwendet wird.

3. Der NPS RADIUS-Proxy die Access-Request-Nachricht empfängt und, basierend auf den lokal konfigurierten Verbindungsanforderungsrichtlinien, bestimmt, wo Sie die Access-Request-Nachricht weitergeleitet werden.

4. Der NPS RADIUS-Proxy leitet die Access-Request-Nachricht an den geeigneten RADIUS-Server weiter.

5. Der RADIUS-Server wertet die Access-Request-Nachricht.

6. Falls erforderlich, sendet der RADIUS-Server eine Access-Challenge-Nachricht an den NPS RADIUS-Proxy, in dem sie den Zugriff auf den Server weitergeleitet wird. Der Zugriffsserver die Herausforderung bei der Zugriffsclient verarbeitet und sendet eine aktualisierte Access-Request an den NPS RADIUS-Proxy, in dem sie an den RADIUS-Server weitergeleitet.

7. Der RADIUS-Server authentifiziert und autorisiert den Verbindungsversuch.

8. Wenn der Verbindungsversuch authentifiziert und autorisiert ist, sendet der RADIUS-Server eine Access-Accept-Nachricht an den NPS RADIUS-Proxy, in dem sie den Zugriff auf den Server weitergeleitet wird. Wenn der Verbindungsversuch entweder nicht authentifiziert oder nicht autorisiert, sendet der RADIUS-Server eine Access-Reject-Nachricht an den NPS RADIUS-Proxy, in dem sie den Zugriff auf den Server weitergeleitet wird.

9. Der Zugriffsserver den Verbindungsprozess mit dem Zugriffsclient abgeschlossen und sendet eine Accounting-Request-Nachricht an den NPS RADIUS-Proxy. Der NPS RADIUS-Proxy protokolliert die Buchhaltungsdaten und leitet die Nachricht an den RADIUS-Server weiter.

10. Der RADIUS-Server sendet eine Accounting-Response an den NPS RADIUS-Proxy, in dem sie den Zugriff auf den Server weitergeleitet werden.

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).
