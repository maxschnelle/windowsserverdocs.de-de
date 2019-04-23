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
ms.openlocfilehash: 9912927a7b75e4c9f04aa3d24eb7ed46c73a7dd2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855261"
---
# <a name="remote-radius-server-groups"></a>RADIUS-Remoteservergruppen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Wenn Sie als Remote Authentication Dial-in User Service (RADIUS)-Proxy (Network Policy Server, NPS) konfigurieren, verwenden Sie NPS verbindungsanforderungen an den RADIUS-Server weitergeleitet, die sind, kann die Weiterleitung von verbindungsanforderungen verarbeiten, da sie ausführen können Authentifizierung und Autorisierung in der Domäne, in denen der Benutzer- oder Computerkonto befindet. Wenn Sie die Weiterleitung von verbindungsanforderungen an einen oder mehrere RADIUS-Server in nicht vertrauenswürdigen Domänen weiterleiten möchten, können Sie z. B. NPS als RADIUS-Proxy zum Weiterleiten von Anforderungen an die remote-RADIUS-Server in nicht vertrauenswürdigen Domäne konfigurieren.

>[!NOTE]
>RADIUS-Remoteservergruppen sind unabhängig von und getrennt von der Windows-Gruppen.

Um NPS als RADIUS-Proxy konfigurieren zu können, müssen Sie eine Verbindungsanforderungsrichtlinie erstellen, die alle Informationen erforderlich sind, für NPS zum Auswerten der Nachrichten weiterleiten sowie zum Senden von Nachrichten enthält.

Wenn Sie eine remote-RADIUS-Servergruppe in NPS konfigurieren, und Sie eine Verbindungsanforderungsrichtlinie, mit der Gruppe konfigurieren, werden Sie den Speicherort festlegen, in denen NPS verbindungsanforderungen weitergeleitet werden.

## <a name="configuring-radius-servers-for-a-group"></a>Konfigurieren von RADIUS-Servern für eine Gruppe

Eine remote-RADIUS-Servergruppe ist eine benannte Gruppe, die einen oder mehrere RADIUS-Server enthält. Wenn Sie mehr als einem Server konfigurieren, können Sie angeben lastenausgleichseinstellungen entweder die Reihenfolge zu bestimmen, in der die Server über den Proxy verwendet werden, oder um den Fluss der RADIUS-Nachrichten auf allen Servern in der Gruppe, um zu verhindern, dass das Überladen von einem oder mehreren Servern zu verteilen. mit zu vielen verbindungsanforderungen.

Jeder Server in der Gruppe weist die folgenden Einstellungen an.

- **Namen oder die Adresse**. Jedes Mitglied muss innerhalb der Gruppe einen eindeutigen Namen haben. Der Name kann sein, eine IP-Adresse oder ein Name, der in die IP-Adresse aufgelöst werden kann.

- **Authentifizierung und-Kontoführung**. Sie können authentifizierungsanforderungen, kontoführungsanforderungen oder für jedes Mitglied der remote-RADIUS-Server weiterleiten.

- **Lastenausgleich**. Eine prioritätseinstellung wird verwendet, um anzugeben, welches Mitglied der Gruppe der primäre Server ist (die Priorität wird auf 1 festgelegt). Für Gruppenmitglieder, die dieselbe Priorität haben, eine Gewichtung wird verwendet, wie oft berechnen RADIUS-Nachrichten zu den einzelnen Servern gesendet werden. Sie können zusätzliche Einstellungen verwenden, in dem der NPS erkennt, wenn ein Gruppenmitglied zunächst nicht verfügbar ist, und sobald es verfügbar ist, nachdem er festgestellt wurde, nicht verfügbar ist, können Sie konfigurieren.

Nachdem Sie eine Remote-RADIUS-Servergruppe konfiguriert haben, können Sie die Gruppe in die Authentifizierungs- und kontoführungseinstellungen für eine Verbindungsanforderungsrichtlinie angeben. Aus diesem Grund können Sie eine RADIUS-Remoteservergruppe zuerst konfigurieren. Als Nächstes können Sie die Verbindungsanforderungsrichtlinie, die neu konfigurierte RADIUS-Remoteservergruppe Verwendung konfigurieren. Alternativ können Sie den Assistenten für neue Verbindungen um zu eine neue RADIUS-Remoteservergruppe zu erstellen, während Sie die Verbindungsanforderungsrichtlinie erstellen.

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).
