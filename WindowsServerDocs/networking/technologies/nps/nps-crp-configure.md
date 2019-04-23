---
title: Konfigurieren von Verbindungsanforderungsrichtlinien
description: Dieses Thema enthält Informationen zum Konfigurieren von Verbindungsanforderungsrichtlinien im Netzwerkrichtlinienserver unter Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: f62c6a67-4dda-47f8-8bdf-9b76c37953e6
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4f80f9fb8be0c44cfb5685e5b9cc489282e4961d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884511"
---
# <a name="configure-connection-request-policies"></a>Konfigurieren von Verbindungsanforderungsrichtlinien

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, erstellen und konfigurieren Verbindungsanforderungsrichtlinien, die bestimmen, ob den lokalen NPS Verbindungsanfragen verarbeitet oder leitet sie an die remote-RADIUS-Server zur Verarbeitung weiter.

Verbindungsanforderungsrichtlinien bestehen Sätze von Bedingungen, mit denen Netzwerkadministratoren die Remote Authentication Dial-in User Service (RADIUS)-Server festlegen können. Führen Sie der Authentifizierungs und Autorisierung der Verbindung anfordert, die die Server mit der Netzwerkrichtlinienserver \(NPS\) von RADIUS-Clients empfängt.

Die Standard-Verbindungsanforderungsrichtlinie NPS als RADIUS-Server verwendet und verarbeitet alle authentifizierungsanforderungen lokal.

Um einen Server mit NPS als RADIUS-Proxy und Weiterleiten von verbindungsanforderungen an andere NPS oder RADIUS-Server fungieren zu konfigurieren, müssen Sie eine remote-RADIUS-Servergruppe neben dem Hinzufügen einer neuen Verbindungsanforderungsrichtlinie, der angibt, Bedingungen und Einstellungen konfigurieren, die Weiterleitung von verbindungsanforderungen müssen übereinstimmen.

Sie können eine neue RADIUS-Remoteservergruppe erstellen, während Sie eine neue Verbindungsanforderungsrichtlinie mit dem Assistenten für neue Verbindungen erstellen.

Wenn Sie den NPS, fungiert als lokal Anforderungen von eine RADIUS-Server und die Prozess-Verbindung nicht möchten, können Sie die Standard-Verbindungsanforderungsrichtlinie löschen.

Wenn Sie möchten den NPS fungieren als beide einem RADIUS-Server verarbeitet verbindungsanforderungen lokal, und fügen eine neue Richtlinie mithilfe des folgenden Verfahrens als RADIUS-Proxy, einige verbindungsanforderungen an einer RADIUS-Remoteservergruppe weitergeleitet und dann bestätigen, dass der Standardwert Verbindungsanforderungsrichtlinie, ist die letzte Richtlinie, die verarbeitet werden, indem Sie diesen letzten in der Liste der Richtlinien.

## <a name="add-a-connection-request-policy"></a>Fügen Sie eine Verbindungsanforderungsrichtlinie hinzu.

Grundvoraussetzung für die Ausführung dieses Vorgangs ist die Mitgliedschaft in **Domänen-Admins** oder einer gleichwertigen Gruppe.

### <a name="to-add-a-new-connection-request-policy"></a>Eine neue Verbindungsanforderungsrichtlinie hinzufügen 

1. Klicken Sie im Server-Manager **Tools**, und klicken Sie dann auf **Network Policy Server** die NPS-Konsole zu öffnen. 
2. Doppelklicken Sie in der Konsolenstruktur auf **Richtlinien**.
3. Mit der rechten Maustaste **Verbindungsanforderungsrichtlinien**, und klicken Sie dann auf **neue Verbindungsanforderungsrichtlinie**.
4. Verwenden Sie Anforderung Richtlinienassistent für neue Verbindungen zum Konfigurieren der Verbindung Richtlinie anfordern, und wenn nicht zuvor konfiguriert haben, eine remote-RADIUS-Servergruppe.


Weitere Informationen zum Verwalten von NPS finden Sie unter [Verwalten des Netzwerkrichtlinienservers](nps-manage-top.md).

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).

