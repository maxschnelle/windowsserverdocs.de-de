---
title: Konfigurieren von Verbindungsanforderungsrichtlinien
description: Dieses Thema enthält Informationen zum Konfigurieren von Verbindungsanforderungsrichtlinien im Netzwerkrichtlinienserver in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: f62c6a67-4dda-47f8-8bdf-9b76c37953e6
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9677e147bdaea4de71a054cd6c52d81126e005d1
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="configure-connection-request-policies"></a>Konfigurieren von Verbindungsanforderungsrichtlinien

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können in diesem Thema erstellen und Konfigurieren von Verbindungsanforderungsrichtlinien, die bestimmen, ob der lokalen NPS-Server verbindungsanforderungen verarbeitet oder an den RADIUS-Remoteserver für die Verarbeitung weiterleitet.

Verbindungsanforderungsrichtlinien sind Bedingungen und Einstellungen, mit denen Netzwerkadministratoren festlegen, welche Server Remote Authentication Dial-in User Service (RADIUS) führen Sie die Authentifizierung und Autorisierung von verbindungsanforderungen zu verarbeiten, die der Server mit der Netzwerkrichtlinienserver \(NPS\) von RADIUS-Clients empfängt.

Die standardmäßige Verbindungsanforderungsrichtlinie verwendet NPS als RADIUS-Server und alle lokal-authentifizierungsanforderungen verarbeitet.

Um einen Server mit NPS als RADIUS-Proxy und Vorwärts verbindungsanforderungen an andere NPS oder RADIUS-Server fungieren zu konfigurieren, müssen Sie konfigurieren, eine RADIUS-Remoteservergruppe zusätzlich zum Hinzufügen einer neuen Verbindungsanforderungsrichtlinie, die angibt, Bedingungen und Einstellungen, die die verbindungsanforderungen übereinstimmen müssen.

Sie können eine neue RADIUS-Remoteservergruppe erstellen, während der Erstellung einer neuen Verbindungsanforderungsrichtlinie mit dem Assistenten für neue Verbindungen.

Wenn Sie den NPS-Server fungiert als RADIUS-Server und Prozess Verbindung lokal anfordert, nicht möchten, können Sie die Standard-Verbindungsanforderungsrichtlinie löschen.

Wenn der NPS-Server als einen RADIUS-Server fungieren soll, Verarbeitung von verbindungsanforderungen lokal und als RADIUS-Proxy, einige verbindungsanforderungen an einer RADIUS-Remoteservergruppe weitergeleitet werden, fügen Sie eine neue Richtlinie mithilfe des folgenden Verfahrens und stellen Sie sicher, dass der standardmäßige Verbindungsanforderungsrichtlinie die letzte Richtlinie verarbeitet, indem sie zuletzt in der Liste der Richtlinien platzieren ist.

## <a name="add-a-connection-request-policy"></a>Fügen Sie eine Verbindungsanforderungsrichtlinie hinzu

Mitgliedschaft in **Domänen-Admins**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.

### <a name="to-add-a-new-connection-request-policy"></a>So fügen Sie eine neue Verbindungsanforderungsrichtlinie hinzu 

1. Klicken Sie im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver** die NPS-Konsole zu öffnen. 
2. Doppelklicken Sie in der Konsolenstruktur auf **Richtlinien**.
3. Mit der rechten Maustaste **Verbindungsanforderungsrichtlinien**, und klicken Sie dann auf **neue Verbindungsanforderungsrichtlinie**.
4. Verwenden Sie die neue Assistenten so konfigurieren Sie die Verbindung eine Richtlinie anfordern, und falls nicht vorher konfiguriert, eine RADIUS-Remoteservergruppe.


Weitere Informationen zum Verwalten von NPS finden Sie unter [Netzwerkrichtlinienserver verwalten](nps-manage-top.md).

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).

