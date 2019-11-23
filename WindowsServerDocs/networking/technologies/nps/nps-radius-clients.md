---
title: RADIUS-Clients
description: Dieses Thema bietet einen Überblick über RADIUS-Clients für den Netzwerk Richtlinien Server unter Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: d3a09ac9-75f8-4f57-aab4-b0fdfe110118
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1dfc1bb71d2800a8a9587e54147950dfd7fb371f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71395996"
---
# <a name="radius-clients"></a>RADIUS-Clients

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Ein Netzwerk Zugriffs Server \(NAS\) ist ein Gerät, das ein gewisses Maß an Zugriff auf ein größeres Netzwerk bietet. Ein NAS, das eine RADIUS-Infrastruktur verwendet, ist auch ein RADIUS-Client, der Verbindungsanforderungen und Buchhaltungs Nachrichten an einen RADIUS-Server zur Authentifizierung, Autorisierung und Kontoführung sendet.

>[!NOTE]
>Client Computer, z. b. Laptop Computer und andere Computer, auf denen Client Betriebssysteme ausgeführt werden, sind keine RADIUS-Clients. RADIUS-Clients sind Netzwerk Zugriffs Server, z. b. drahtlos Zugriffspunkte, 802.1 x-authentifizier Ende Switches, virtuelles privates Netzwerk \(VPN\) Servern und DFÜ-Server, da Sie das RADIUS-Protokoll für die Kommunikation mit RADIUS-Servern wie Netzwerk Richtlinien Server \(NPS-\) Servern verwenden.

Zum Bereitstellen von NPS als RADIUS-Server oder RADIUS-Proxy müssen Sie RADIUS-Clients in NPS konfigurieren.

## <a name="radius-client-examples"></a>Beispiele für RADIUS-Clients

Beispiele für Netzwerk Zugriffs Server:

- Netzwerk Zugriffs Server, die Remote Zugriffs Verbindungen mit einem Organisations Netzwerk oder dem Internet bereitstellen. Ein Beispiel hierfür ist ein Computer, auf dem das Betriebssystem Windows Server 2016 ausgeführt wird, und der RAS-Dienst, der entweder herkömmliche DFÜ-oder VPN-Remote Zugriffs Dienste (Virtual Private Network) für das Intranet einer Organisation bereitstellt.
- Drahtlose Zugriffspunkte, die physischen Zugriff auf ein Organisations Netzwerk mithilfe von drahtlos basierten Übertragungs-und Empfangs Technologien ermöglichen.
- Switches, die physischen Zugriff auf das Netzwerk einer Organisation ermöglichen, indem herkömmliche LAN-Technologien wie z. b. Ethernet verwendet werden.
- RADIUS-Proxys, die Verbindungsanforderungen an RADIUS-Server weiterleiten, die Mitglieder einer RADIUS-Remote Server Gruppe sind, die auf dem RADIUS-Proxy konfiguriert ist.

## <a name="radius-access-request-messages"></a>RADIUS-Zugriff-Anforderungs Nachrichten

RADIUS-Clients erstellen entweder RADIUS-Access-Request-Nachrichten und leiten Sie an einen RADIUS-Proxy oder einen RADIUS-Server weiter, oder Sie leiten Zugriffs Anforderungs Nachrichten an einen RADIUS-Server weiter, der von einem anderen RADIUS-Client empfangen wurde, jedoch nicht selbst erstellt wurde.

RADIUS-Clients verarbeiten keine Zugriffs Anforderungs Nachrichten, indem Sie Authentifizierung, Autorisierung und Kontoführung durchführen. Diese Funktionen werden nur von RADIUS-Servern durchgeführt.

NPS kann jedoch sowohl als RADIUS-Proxy als auch als RADIUS-Server gleichzeitig konfiguriert werden, sodass einige Zugriffs Anforderungs Nachrichten verarbeitet und andere Nachrichten weitergeleitet werden.

## <a name="nps-as-a-radius-client"></a>NPS als RADIUS-Client

NPS fungiert als RADIUS-Client, wenn Sie ihn als RADIUS-Proxy konfigurieren, um Access-Request-Nachrichten für die Verarbeitung an andere RADIUS-Server weiterzuleiten. Wenn Sie NPS als RADIUS-Proxy verwenden, sind die folgenden allgemeinen Konfigurationsschritte erforderlich:

1. Netzwerk Zugriffs Server, z. b. drahtlos Zugriffspunkte und VPN-Server, werden mit der IP-Adresse des NPS-Proxys als festgelegte RADIUS-Server oder authentifizierenden Server konfiguriert. Dadurch können Netzwerk Zugriffs Server, die Zugriffs Anforderungs Nachrichten basierend auf Informationen erstellen, die Sie von Zugriffs Clients erhalten, Nachrichten an den NPS-Proxy weiterleiten.

2. Der NPS-Proxy wird konfiguriert, indem jeder Netzwerk Zugriffs Server als RADIUS-Client hinzugefügt wird. Dieser Konfigurationsschritt ermöglicht es dem NPS-Proxy, Nachrichten von den Netzwerk Zugriffs Servern zu empfangen und während der Authentifizierung mit Ihnen zu kommunizieren. Außerdem werden Verbindungs Anforderungs Richtlinien auf dem NPS-Proxy konfiguriert, um anzugeben, welche zugriffsanforderungs-Nachrichten an einen oder mehrere RADIUS-Server weiterzuleiten sind. Diese Richtlinien werden auch mit einer RADIUS-Remote Server Gruppe konfiguriert, die NPS mitteilt, wohin die Nachrichten gesendet werden sollen, die Sie von den Netzwerk Zugriffs Servern empfängt.

3. Die NPS-oder anderen RADIUS-Server, die Mitglieder der RADIUS-Remote Server Gruppe auf dem NPS-Proxy sind, werden so konfiguriert, dass Sie Nachrichten vom NPS-Proxy empfangen. Dies wird erreicht, indem der NPS-Proxy als RADIUS-Client konfiguriert wird.

## <a name="radius-client-properties"></a>RADIUS-Client Eigenschaften

Wenn Sie der NPS-Konfiguration über die NPS-Konsole einen RADIUS-Client hinzufügen oder indem Sie die Netsh-Befehle für NPS-oder Windows PowerShell-Befehle verwenden, konfigurieren Sie NPS für den Empfang von RADIUS-Access-Request-Nachrichten von einem Netzwerk Zugriffs Server oder einem RADIUS-Proxy.

Wenn Sie einen RADIUS-Client in NPS konfigurieren, können Sie die folgenden Eigenschaften festlegen:

### <a name="client-name"></a>Client Name

 Ein Anzeige Name für den RADIUS-Client, mit dem Sie leichter erkennen können, wenn Sie das NPS-Snap-in oder Netsh-Befehle für NPS verwenden.

### <a name="ip-address"></a>IP-Adresse

Internet Protokollversion 4 \(IPv4-\) Adresse oder der Domain Name System \(DNS-\) Name des RADIUS-Clients.

### <a name="client-vendor"></a>Client-Vendor

Der Anbieter des RADIUS-Clients. Andernfalls können Sie den RADIUS-Standardwert für Client-Vendor verwenden.

### <a name="shared-secret"></a>Gemeinsamer geheimer Schlüssel

Eine Text Zeichenfolge, die als Kennwort zwischen RADIUS-Clients, RADIUS-Servern und RADIUS-Proxys verwendet wird. Wenn das Message Authenticator-Attribut verwendet wird, wird der gemeinsame geheime Schlüssel auch als Schlüssel zum Verschlüsseln von RADIUS-Nachrichten verwendet. Diese Zeichenfolge muss auf dem RADIUS-Client und im NPS-Snap-in konfiguriert werden.

### <a name="message-authenticator-attribute"></a>Message Authenticator-Attribut

Beschrieben in RFC 2869, "RADIUS Extensions", a Message Digest 5 \(MD5\) Hash der gesamten RADIUS-Nachricht. Wenn das RADIUS Message Authenticator-Attribut vorhanden ist, wird es überprüft. Wenn die Überprüfung fehlschlägt, wird die RADIUS-Nachricht verworfen. Wenn die Client Einstellungen das Message Authenticator-Attribut erfordern und es nicht vorhanden ist, wird die RADIUS-Nachricht verworfen. Es wird empfohlen, das Message Authenticator-Attribut zu verwenden.

>[!NOTE]
>Das Message Authenticator-Attribut ist erforderlich und wird standardmäßig aktiviert, wenn Sie das Extensible Authentication-Protokoll \(EAP-\) Authentifizierung verwenden. 

Weitere Informationen zu NPS finden Sie unter [Netzwerk Richtlinien Server (Network Policy Server, NPS)](nps-top.md).

