---
title: Erhöhen der durch NPS verarbeitete gleichzeitige Authentifizierungen
description: Dieses Thema enthält Anweisungen zum Konfigurieren des Netzwerkrichtlinienservers gleichzeitiger Authentifizierungen in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 2d9cdada-0625-41c8-8248-a32259b03e47
ms.author: pashort
author: shortpatti
ms.openlocfilehash: aa70c1a26e2c22d26545e1b46a6151d71a2b4095
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="increase-concurrent-authentications-processed-by-nps"></a>Erhöhen der durch NPS verarbeitete gleichzeitige Authentifizierungen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können in diesem Thema Anweisungen zum Konfigurieren des Netzwerkrichtlinienservers gleichzeitiger Authentifizierungen verwenden.

Wenn Sie Netzwerkrichtlinienserver \(NPS\) auf einem anderen Computer als einen Domänencontroller installiert und der NPS-Server eine große Anzahl von authentifizierungsanforderungen pro Sekunde empfangen wird, können Sie NPS-Leistung verbessern, indem Vergrößern der Anzahl gleichzeitiger Authentifizierungen zwischen dem NPS-Server und dem Domänencontroller zulässig.

Zu diesem Zweck müssen Sie den folgenden Registrierungsschlüssel bearbeiten: 

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Netlogon\Parameters`

Fügen Sie einen neuen Wert mit dem Namen **"MaxConcurrentApi"** und weisen Sie ihm einen Wert von 2 bis 5. 

>[!CAUTION]
>Wenn Sie einen Wert zuweisen **"MaxConcurrentApi"** zu hoch ist, kann der NPS-Server ausgelastet platzieren, auf dem Domänencontroller.

Weitere Informationen zum Verwalten von NPS finden Sie unter [Netzwerkrichtlinienserver verwalten](nps-manage-top.md).

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).