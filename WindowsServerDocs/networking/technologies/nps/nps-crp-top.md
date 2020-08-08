---
title: Verarbeitung von Verbindungsanforderungen
description: Dieses Thema enthält eine Übersicht über die Verarbeitung von Verbindungsanforderungen für Netzwerk Richtlinien Server in Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 849d661a-42c1-4f93-b669-6009d52aad39
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 9b50fe9a3adce7967a555237446e77e4d4080221
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955597"
---
# <a name="connection-request-processing"></a>Verarbeitung von Verbindungsanforderungen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erfahren Sie mehr über die Verarbeitung von Verbindungsanforderungen auf dem Netzwerk Richtlinien Server unter Windows Server 2016.

>[!NOTE]
>Zusätzlich zu diesem Thema ist die folgende Dokumentation zur Verarbeitung von Verbindungsanforderungen verfügbar.
> - [Verbindungs Anforderungs Richtlinien](nps-crp-crpolicies.md)
> - [Bereichs Namen](nps-crp-realm-names.md)
> - [Remote-RADIUS-Server Gruppen](nps-crp-rrsg.md)

Sie können die Verarbeitung von Verbindungsanforderungen verwenden, um anzugeben, wo die Authentifizierung von Verbindungsanforderungen erfolgt: auf dem lokalen Computer oder auf einem Remote-RADIUS-Server, der Mitglied einer RADIUS-Remote Server Gruppe ist.

Wenn der lokale Server, auf dem der Netzwerk Richtlinien Server (Network Policy Server, NPS) ausgeführt wird, eine Authentifizierung für Verbindungsanforderungen ausführen soll, können Sie die Standard-Verbindungs Anforderungs Richtlinie ohne zusätzliche Konfiguration verwenden. Basierend auf der Standard Richtlinie authentifiziert NPS Benutzer und Computer, die über ein Konto in der lokalen Domäne und vertrauenswürdigen Domänen verfügen.

Wenn Sie Verbindungsanforderungen an einen NPS-Remote Server oder einen anderen RADIUS-Server weiterleiten möchten, erstellen Sie eine Remote-RADIUS-Server Gruppe, und konfigurieren Sie dann eine Verbindungs Anforderungs Richtlinie, die Anforderungen an diese RADIUS-Remote Server Gruppe weiterleitet. Mit dieser Konfiguration können NPS Authentifizierungsanforderungen an beliebige RADIUS-Server weiterleiten, und Benutzer mit Konten in nicht vertrauenswürdigen Domänen können authentifiziert werden.

Die folgende Abbildung zeigt den Pfad einer Access-Request-Nachricht von einem Netzwerk Zugriffs Server zu einem RADIUS-Proxy und dann auf einen RADIUS-Server in einer RADIUS-Remote Server Gruppe. Auf dem RADIUS-Proxy ist der Netzwerk Zugriffs Server als RADIUS-Client konfiguriert. und auf jedem RADIUS-Server ist der RADIUS-Proxy als RADIUS-Client konfiguriert.


![NPS-Verbindungs Anforderungs Verarbeitung](../../media/Nps-Connection-Request-Processing/Nps-Connection-Request-Processing.jpg)


>[!NOTE]
>Bei den Netzwerk Zugriffs Servern, die Sie mit NPS verwenden, kann es sich um Gatewaygeräte handeln, die mit dem RADIUS-Protokoll kompatibel sind, z. b. drahtlose 802.1 x-Zugriffspunkte und authentifizier Ende Switches, Server mit Remote Zugriff, die als VPN-oder DFÜ-Server oder andere mit RADIUS kompatible Geräte konfiguriert sind

Wenn Sie möchten, dass NPS einige Authentifizierungsanforderungen lokal verarbeitet, während andere Anforderungen an eine Remote-RADIUS-Server Gruppe weitergeleitet werden, müssen Sie mehr als eine Verbindungs Anforderungs Richtlinie konfigurieren.

Informationen zum Konfigurieren einer Verbindungs Anforderungs Richtlinie, die angibt, welche NPS-oder RADIUS-Server Gruppe Authentifizierungsanforderungen verarbeitet, finden Sie unter Verbindungs Anforderungs Richtlinien.

Informationen zum Angeben von NPS oder anderen RADIUS-Servern, an die Authentifizierungsanforderungen weitergeleitet werden, finden Sie unter Remote-RADIUS-Server Gruppen

## <a name="nps-as-a-radius-server-connection-request-processing"></a>NPS als RADIUS-Server-Verbindungs Anforderungs Verarbeitung

Wenn Sie NPS als RADIUS-Server verwenden, bieten RADIUS-Nachrichten Authentifizierung, Autorisierung und Kontoführung für Netzwerk Zugriffs Verbindungen auf folgende Weise:

1. Zugriffs Server, z. b. DFÜ-Netzwerk Zugriffs Server, VPN-Server und drahtlos Zugriffspunkte, empfangen Verbindungsanforderungen von Zugriffs Clients.

2. Der Zugriffs Server, der für die Verwendung von RADIUS als Authentifizierungs-, Autorisierungs-und Kontoführungs Protokoll konfiguriert ist, erstellt eine Access-Request-Nachricht und sendet Sie an den NPS.

3. Der NPS wertet die Access-Request-Nachricht aus.

4. Bei Bedarf sendet der NPS eine Access-Challenge-Nachricht an den Zugriffs Server. Der Zugriffs Server verarbeitet die Anforderung und sendet eine aktualisierte Zugriffs Anforderung an den NPS.

5. Die Benutzer Anmelde Informationen werden geprüft, und die Einwähleigenschaften des Benutzerkontos werden mithilfe einer sicheren Verbindung mit einem Domänen Controller abgerufen.

6. Der Verbindungsversuch wird sowohl mit den Einwähleigenschaften des Benutzerkontos als auch mit den Netzwerk Richtlinien autorisiert.

7. Wenn der Verbindungsversuch sowohl authentifiziert als auch autorisiert ist, sendet der NPS eine Access-Accept-Nachricht an den Zugriffs Server. Wenn der Verbindungsversuch entweder nicht authentifiziert oder nicht autorisiert ist, sendet der NPS eine Zugriffs Ablehnungs Nachricht an den Zugriffs Server.

8. Der Zugriffs Server schließt den Verbindungsprozess mit dem Zugriffs Client ab und sendet eine Buchhaltungs Anforderungs Nachricht an den NPS, bei dem die Nachricht protokolliert wird.

9. Der NPS sendet eine Buchhaltungs Antwort an den Zugriffs Server.

>[!NOTE]
>Der Zugriffs Server sendet außerdem Buchhaltungs Anforderungs Nachrichten während des Zeitraums, in dem die Verbindung hergestellt wird, wenn die Zugriffs Client Verbindung geschlossen wird und wenn der Zugriffs Server gestartet und beendet wird.

## <a name="nps-as-a-radius-proxy-connection-request-processing"></a>NPS als RADIUS-Proxy Verbindungs Anforderungs Verarbeitung

Wenn NPS als RADIUS-Proxy zwischen einem RADIUS-Client und einem RADIUS-Server verwendet wird, werden die RADIUS-Nachrichten für Netzwerk Zugriffs Verbindungsversuche folgendermaßen weitergeleitet:

1. Zugriffs Server, z. b. DFÜ-Netzwerk Zugriffs Server, VPN-Server (virtuelles privates Netzwerk) und drahtlos Zugriffspunkte, empfangen Verbindungsanforderungen von Zugriffs Clients.

2. Der Zugriffs Server, der für die Verwendung von RADIUS als Authentifizierungs-, Autorisierungs-und Kontoführungs Protokoll konfiguriert ist, erstellt eine Access-Request-Nachricht und sendet Sie an den NPS, der als NPS-RADIUS-Proxy verwendet wird.

3. Der NPS-RADIUS-Proxy empfängt die Access-Request-Nachricht und bestimmt basierend auf den lokal konfigurierten Verbindungs Anforderungs Richtlinien, wohin die Access-Request-Nachricht weiterzuleiten ist.

4. Der NPS-RADIUS-Proxy leitet die Access-Request-Nachricht an den entsprechenden RADIUS-Server weiter.

5. Der RADIUS-Server wertet die Access-Request-Nachricht aus.

6. Wenn dies erforderlich ist, sendet der RADIUS-Server eine Access-Challenge-Nachricht an den NPS-RADIUS-Proxy, wo er an den Zugriffs Server weitergeleitet wird. Der Zugriffs Server verarbeitet die Abfrage mit dem Zugriffs Client und sendet eine aktualisierte Zugriffs Anforderung an den NPS-RADIUS-Proxy, wo er an den RADIUS-Server weitergeleitet wird.

7. Der RADIUS-Server authentifiziert und autorisiert den Verbindungsversuch.

8. Wenn der Verbindungsversuch sowohl authentifiziert als auch autorisiert ist, sendet der RADIUS-Server eine Access-Accept-Nachricht an den NPS-RADIUS-Proxy, der an den Zugriffs Server weitergeleitet wird. Wenn der Verbindungsversuch entweder nicht authentifiziert oder nicht autorisiert ist, sendet der RADIUS-Server eine Zugriffs Ablehnungs Nachricht an den NPS-RADIUS-Proxy, wo er an den Zugriffs Server weitergeleitet wird.

9. Der Zugriffs Server schließt den Verbindungsprozess mit dem Zugriffs Client ab und sendet eine Buchhaltungs Anforderungs Nachricht an den NPS-RADIUS-Proxy. Der NPS-RADIUS-Proxy protokolliert die Buchhaltungsdaten und leitet die Nachricht an den RADIUS-Server weiter.

10. Der RADIUS-Server sendet eine Buchhaltungs Antwort an den NPS-RADIUS-Proxy, wo er an den Zugriffs Server weitergeleitet wird.

Weitere Informationen zu NPS finden Sie unter [Netzwerk Richtlinien Server (Network Policy Server, NPS)](nps-top.md).
