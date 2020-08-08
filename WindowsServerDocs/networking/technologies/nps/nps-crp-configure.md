---
title: Konfigurieren von Verbindungsanforderungsrichtlinien
description: Dieses Thema enthält Informationen zum Konfigurieren von Verbindungs Anforderungs Richtlinien auf dem Netzwerk Richtlinien Server unter Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: f62c6a67-4dda-47f8-8bdf-9b76c37953e6
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 422ef3238aac950b7d2808d8576b186aeb430767
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969417"
---
# <a name="configure-connection-request-policies"></a>Konfigurieren von Verbindungsanforderungsrichtlinien

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Sie können dieses Thema verwenden, um Verbindungs Anforderungs Richtlinien zu erstellen und zu konfigurieren, die festlegen, ob das lokale NPS Verbindungsanforderungen verarbeitet oder Sie zur Verarbeitung an den Remote-RADIUS-Server weiterleitet.

Verbindungs Anforderungs Richtlinien sind Sätze von Bedingungen und Einstellungen, mit denen Netzwerkadministratoren festlegen können, welche Remote Authentication Dial-in User Service (RADIUS)-Server die Authentifizierung und Autorisierung von Verbindungsanforderungen durchführen, die vom Server mit Netzwerk Richtlinien Server- \( NPS \) von RADIUS-Clients empfangen werden.

Die Standard-Verbindungs Anforderungs Richtlinie verwendet NPS als RADIUS-Server und verarbeitet alle Authentifizierungsanforderungen lokal.

Zum Konfigurieren eines Servers, auf dem NPS ausgeführt wird, um als RADIUS-Proxy zu fungieren und Verbindungsanforderungen an andere NPS-oder RADIUS-Server weiterzuleiten, müssen Sie zusätzlich zum Hinzufügen einer neuen Verbindungs Anforderungs Richtlinie, die Bedingungen und Einstellungen angibt, die die Verbindungsanforderungen erfüllen müssen, eine RADIUS-Remote Server Gruppe konfigurieren.

Sie können eine neue Remote-RADIUS-Server Gruppe erstellen, während Sie eine neue Verbindungs Anforderungs Richtlinie mit dem Assistenten für neue Verbindungs Anforderungs Richtlinien erstellen.

Wenn Sie nicht möchten, dass der NPS als RADIUS-Server fungiert und Verbindungsanforderungen lokal verarbeitet, können Sie die Standard-Verbindungs Anforderungs Richtlinie löschen.

Wenn der NPS als RADIUS-Server fungieren und Verbindungsanforderungen lokal und als RADIUS-Proxy verarbeiten soll, indem einige Verbindungsanforderungen an eine Remote-RADIUS-Server Gruppe weitergeleitet werden, fügen Sie mithilfe des folgenden Verfahrens eine neue Richtlinie hinzu, und überprüfen Sie dann, ob die standardmäßige Verbindungs Anforderungs Richtlinie die letzte Richtlinie ist, die zuletzt in der Liste der Richtlinien verarbeitet wurde.

## <a name="add-a-connection-request-policy"></a>Hinzufügen einer Verbindungs Anforderungs Richtlinie

Zum Durchführen dieses Verfahrens ist mindestens die Mitgliedschaft in **Domänen-Admins** oder eine entsprechende Berechtigung erforderlich.

### <a name="to-add-a-new-connection-request-policy"></a>So fügen Sie eine neue Verbindungs Anforderungs Richtlinie hinzu

1. Klicken Sie in Server-Manager auf **Extras, und**klicken Sie dann auf **Netzwerk Richtlinien Server** , um die NPS-Konsole zu öffnen.
2. Doppelklicken Sie in der Konsolen Struktur auf **Richtlinien**.
3. Klicken Sie mit der rechten Maustaste auf **Verbindungs Anforderungs Richtlinien**, und klicken Sie dann auf **neue Verbindungs Anforderungs Richtlinie**.
4. Verwenden Sie den Assistenten für neue Verbindungs Anforderungs Richtlinien, um die Verbindungs Anforderungs Richtlinie und, falls nicht bereits konfiguriert, eine Remote-RADIUS-Server Gruppe zu konfigurieren.


Weitere Informationen zum Verwalten von NPS finden Sie unter [Verwalten des Netzwerk Richtlinien Servers](nps-manage-top.md).

Weitere Informationen zu NPS finden Sie unter [Netzwerk Richtlinien Server (Network Policy Server, NPS)](nps-top.md).

