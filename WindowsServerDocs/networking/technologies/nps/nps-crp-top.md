---
title: Verarbeitung von Verbindungsanforderungen
description: Dieses Thema enthält eine Übersicht der Anforderung der Netzwerkrichtlinienserver-Verbindung Verarbeitung in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 849d661a-42c1-4f93-b669-6009d52aad39
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6756c89dadbd01998ffef6a6d785c079076f2532
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="connection-request-processing"></a>Verarbeitung von Verbindungsanforderungen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie die Verarbeitung in der Netzwerkrichtlinienserver in Windows Server 2016-verbindungsanforderung Informationen.

>[!NOTE]
>Zusätzlich zu diesem Thema ist die folgenden Verbindungsanfrage Verarbeitung Dokumentation verfügbar.
> - [Verbindungsanforderungsrichtlinien](nps-crp-crpolicies.md)
> - [Bereichsnamen](nps-crp-realm-names.md)
> - [RADIUS-Remoteservergruppen](nps-crp-rrsg.md)

Verarbeitung der Anforderung Verbindung können Sie angeben, in dem die Authentifizierung von verbindungsanforderungen ausgeführt wird, auf dem lokalen Computer oder einen RADIUS-Remoteserver, der Mitglied einer RADIUS-Remoteservergruppe -. 

Wenn Sie auf den lokalen Server ausgeführt wird (Network Policy Server, NPS) für verbindungsanforderungen Authentifizierung durchführen möchten, können Sie die Standard-Verbindungsanforderungsrichtlinie ohne zusätzliche Konfiguration. NPS basierend auf der Standardrichtlinie, authentifiziert werden, Benutzer und Computer, auf denen ein Konto in der lokalen Domäne und in vertrauenswürdigen Domänen verfügen.

Wenn auf einem Remoteserver NPS oder anderen RADIUS-Server verbindungsanforderungen weitergeleitet werden sollen, erstellen Sie eine RADIUS-Remoteservergruppe, und konfigurieren Sie eine Verbindungsanforderungsrichtlinie, die Anforderungen an die RADIUS-Remoteservergruppe weiterleitet. Bei dieser Konfiguration NPS können Authentifizierungsanfragen mit einem RADIUS-Server weiterleiten, und Benutzer mit einem Konto in nicht vertrauenswürdigen Domänen authentifiziert werden können.

Die folgende Abbildung zeigt den Pfad einer Nachricht Access-Anforderung in einem Netzwerkzugriffsserver an einen RADIUS-Proxy und klicken Sie dann an einen RADIUS-Server in einer RADIUS-Remoteservergruppe. Auf dem RADIUS-Proxy ist der Netzwerkzugriffsserver als RADIUS-Client konfiguriert. und auf jedem RADIUS-Server, der RADIUS-Proxy als RADIUS-Client konfiguriert ist.


![Verarbeitung von NPS Verbindungsanforderungen](../../media/Nps-Connection-Request-Processing/Nps-Connection-Request-Processing.jpg)


>[!NOTE]
>Die Netzwerkzugriffsserver, die Sie mit dem Netzwerkrichtlinienserver verwenden kann, Gateway-Geräte, die mit dem RADIUS-Protokoll, z. B. 802.1 X drahtlose Zugriffspunkte und authentifizierenden Switches, Server mit Remote-Zugriff, die als VPN konfiguriert sind oder DFÜ-Server, kompatibel sind oder andere RADIUS-kompatible Geräte.

Wenn Sie NPS einige Authentifizierungsanfragen lokal zu verarbeiten, während die anderen Anforderungen an einer RADIUS-Remoteservergruppe weitergeleitet werden soll, konfigurieren Sie mehr als eine Verbindungsanforderungsrichtlinie.

Finden Sie Verbindungsanforderungsrichtlinien, um eine Verbindungsanforderungsrichtlinie zu konfigurieren, die angibt, welche NPS oder RADIUS-Server-Gruppe authentifizierungsanforderungen verarbeitet.

Zum Angeben von NPS oder andere RADIUS-Server, auf welche, die Authentifizierung Anforderungen weitergeleitet werden, finden Sie unter RADIUS-Remoteservergruppen.

## <a name="nps-as-a-radius-server-connection-request-processing"></a>NPS als ein RADIUS-Server-verbindungsverarbeitung

Wenn Sie NPS als RADIUS-Server verwenden, bieten RADIUS-Nachrichten Authentifizierung, Autorisierung und Kontoführung für Netzwerkverbindungen für den Zugriff auf folgende Weise:

1. Server, z. B. DFÜ-Netzwerkzugriffsserver, VPN-Server und drahtlose Zugriffspunkte erhalten verbindungsanforderungen von auf Clients. 

2. Die Access-Server so konfiguriert, dass für die Verwendung von RADIUS als die Authentifizierung, Autorisierung und Kontoführung-Protokoll wird eine Nachricht Access-Anforderung erstellt und an den NPS-Server gesendet. 

3. Der NPS-Server wertet die Access-Anforderungsnachricht. 

4. Falls erforderlich, sendet der NPS-Server eine Access-Challenge-Nachricht an einem Server. Die Access-Server verarbeitet die Abfrage und sendet eine aktualisierte Access-Anforderung an den NPS-Server. 

5. Die Anmeldeinformationen des Benutzers werden überprüft, und die DFÜ-Eigenschaften des Benutzerkontos werden mit einer sicheren Verbindung mit einem Domänencontroller abgerufen. 

6. Der Verbindungsversuch wird mit beiden die DFÜ-Eigenschaften des Benutzerkontos und Netzwerkrichtlinien autorisiert. 

7. Der Verbindungsversuch authentifiziert und autorisiert ist, sendet der NPS-Server eine Access-Accept-Nachricht an den Server zugreifen. Wenn der Verbindungsversuch nicht authentifiziert oder nicht autorisiert wurde, sendet der NPS-Server eine Access-Reject-Nachricht auf einem Server. 

8. Die Access-Server schließt den Verbindungsvorgang mit dem Zugriffsclient und sendet eine Accounting-Request-Nachricht an den NPS-Server, auf dem die Meldung protokolliert wird. 

9. Der NPS-Server sendet eine Kontoführung-Antwort an den Server zugreifen. 

>[!NOTE]
>Der RAS-Server sendet Kontoführungsanforderung Nachrichten auch die Zeit, an dem die Verbindung hergestellt wird, wenn der Clientverbindung geschlossen wird, und bei ein Server gestartet oder beendet wird.

## <a name="nps-as-a-radius-proxy-connection-request-processing"></a>NPS als ein RADIUS-Proxy verbindungsverarbeitung

Wenn Sie NPS als RADIUS-Proxy zwischen RADIUS-Client und einem RADIUS-Server verwendet wird, zugreifen RADIUS-Nachrichten für Netzwerk Verbindung, die Versuche auf folgende Weise weitergeleitet werden:

1. Server, z. B. DFÜ-Netzwerkzugriffsserver, virtuelles privates Netzwerk (VPN)-Server und drahtlose Zugriffspunkte erhalten verbindungsanforderungen von auf Clients.

2. Die Access-Server so konfiguriert, dass für die Verwendung von RADIUS als die Authentifizierung, Autorisierung und Kontoführung-Protokoll wird eine Nachricht Access-Anforderung erstellt und sendet sie an den NPS-Server, der als der NPS RADIUS-Proxy verwendet wird.

3. Der NPS RADIUS-Proxy empfängt die Zugriffsanforderung Meldung und, basierend auf der lokal konfigurierten Verbindungsanforderungsrichtlinien, legt fest, wo die Zugriffsanforderung Nachricht weiterzuleiten.

4. Der NPS RADIUS-Proxy leitet die Zugriffsanforderung Nachricht an den entsprechenden RADIUS-Server weiter.

5. Der RADIUS-Server wertet die Access-Anforderungsnachricht.

6. Falls erforderlich, sendet der RADIUS-Server eine Access-Challenge-Nachricht an den NPS RADIUS-Proxy, in dem sie die Access-Server weitergeleitet. Die Access-Server verarbeitet die Abfrage mit dem Zugriffsclient und sendet eine aktualisierte Access-Anforderung an den NPS RADIUS-Proxy, wo sie mit dem RADIUS-Server weitergeleitet.

7. Der RADIUS-Server authentifiziert und autorisiert den Verbindungsversuch.

8. Der Verbindungsversuch authentifiziert und autorisiert ist, sendet der RADIUS-Server eine Access-Accept-Nachricht an den NPS RADIUS-Proxy, wo sie die Access-Server weitergeleitet. Wenn der Verbindungsversuch nicht authentifiziert oder nicht autorisiert wurde, sendet der RADIUS-Server eine Access-Reject-Nachricht an den NPS RADIUS-Proxy, in dem sie die Access-Server weitergeleitet.

9. Die Access-Server schließt den Verbindungsvorgang mit dem Zugriffsclient und sendet eine Nachricht Kontoführung-Anforderung an den NPS-RADIUS-Proxy. Der NPS RADIUS-Proxy protokolliert die Kontoführungsdaten und leitet die Nachricht an den RADIUS-Server weiter.

10. Der RADIUS-Server sendet eine Accounting-Antwort an den NPS RADIUS-Proxy, wo sie die Access-Server weitergeleitet.

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).
