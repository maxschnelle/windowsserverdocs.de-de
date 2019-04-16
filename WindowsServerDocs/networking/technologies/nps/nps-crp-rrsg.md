---
title: RADIUS-Remoteservergruppen
description: Dieses Thema enthält eine Übersicht über Network Policy Server RADIUS-Remoteservergruppen in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d81678a7-be21-48f2-9b3f-5a75d6aef013
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1f27b5e501f110a038264cd54d75c8b8f9566a64
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="remote-radius-server-groups"></a>RADIUS-Remoteservergruppen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Wenn Sie den Netzwerkrichtlinienserver (Network Policy Server, NPS) als Proxy Remote Authentication Dial-in User Service (RADIUS) konfigurieren, verwenden Sie NPS verbindungsanforderungen an RADIUS-Server weitergeleitet, die die verbindungsanforderungen verarbeiten, da sie Authentifizierung und Autorisierung in der Domäne ausführen können, wo sich die Benutzer- oder Computerkonto befindet. Wenn Sie verbindungsanforderungen an einen oder mehrere RADIUS-Server in nicht vertrauenswürdigen Domänen weiterleiten möchten, können Sie z. B. NPS als RADIUS-Proxy, der Anfragen an den RADIUS-Servern in der nicht vertrauenswürdigen Domäne weiterzuleiten konfigurieren.

>[!NOTE]
>RADIUS-Remoteservergruppen sind nicht im Zusammenhang mit und getrennt von Windows-Gruppen.

Wenn Sie um NPS als RADIUS-Proxy zu konfigurieren, müssen Sie eine Verbindungsanforderungsrichtlinie erstellen, die alle für den NPS, welche Nachrichten weiterleiten zu bewerten und wo die Nachrichten erforderlichen Informationen enthält.

Wenn Sie eine RADIUS-Remoteservergruppe in NPS konfigurieren und eine Verbindungsanforderungsrichtlinie mit der Gruppe, werden Sie den Speicherort festlegen, in denen NPS verbindungsanforderungen weitergeleitet wird.

## <a name="configuring-radius-servers-for-a-group"></a>Konfigurieren von RADIUS-Servern für eine Gruppe

Eine RADIUS-Remoteservergruppe ist eine benannte Gruppe, die eine oder mehrere RADIUS-Server enthält. Wenn Sie mehr als einen Server konfigurieren, können Sie angeben, für den Netzwerklastenausgleich-Einstellungen entweder die Reihenfolge bestimmen, in der die Server durch den Proxy verwendet werden, oder zum Verteilen von des Nachrichtenfluss RADIUS auf alle Server in der Gruppe auf einem oder mehreren Servern mit zu vielen Verbindungsanfragen Überlastung zu vermeiden.

Jeder Server in der Gruppe hat die folgenden Einstellungen.

- **Namen oder die Adresse**. Jedes Mitglied der Gruppe muss innerhalb der Gruppe einen eindeutigen Namen haben. Der Name kann sein, eine IP-Adresse oder einen Namen, der in der IP-Adresse aufgelöst werden kann.

- **Authentifizierung und-Kontoführung**. Sie können authentifizierungsanforderungen, kontoführungsanforderungen oder beides für die einzelnen remote Gruppenmitglieder für die RADIUS-Server weiterleiten.

- **Lastenausgleich**. Eine Einstellung der Priorität wird verwendet, um anzugeben, die Mitglied der Gruppe der primäre Server ist (die Priorität wird auf 1 festgelegt). Für Mitglieder der Gruppe, die die gleiche Priorität haben, wird eine Gewichtung-Einstellung verwendet, um Häufigkeit berechnen RADIUS-Nachrichten werden für jeden Server gesendet. Zusätzliche Einstellungen können in dem der NPS-Server erkannt wird, wenn ein Gruppenmitglied zunächst nicht verfügbar ist, und sobald es verfügbar ist, nachdem er festgestellt wurde, nicht verfügbar ist, können Sie konfigurieren.

Nachdem Sie einen RADIUS-Remoteservergruppe konfiguriert haben, können Sie die Gruppe in der Authentifizierung und kontoführungseinstellungen eine Verbindungsanforderungsrichtlinie angeben. Aus diesem Grund können Sie eine RADIUS-Remoteservergruppe zuerst konfigurieren. Als Nächstes können Sie die Verbindungsanforderungsrichtlinie die Verwendung der neu konfigurierte RADIUS-Remoteservergruppe konfigurieren. Alternativ können Sie den Assistenten für neue Verbindungen zu eine neue RADIUS-Remoteservergruppe erstellen, während Sie die Verbindungsanforderungsrichtlinie erstellen.

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).
