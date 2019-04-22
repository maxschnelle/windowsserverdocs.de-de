---
title: Erhöhen der durch NPS verarbeiteten gleichzeitigen Authentifizierungen
description: Dieses Thema enthält Anweisungen zum Konfigurieren des Netzwerkrichtlinienservers gleichzeitiger Authentifizierungen in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 2d9cdada-0625-41c8-8248-a32259b03e47
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fd930e34a4adf6c55812385b691df3e3575a4280
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818261"
---
# <a name="increase-concurrent-authentications-processed-by-nps"></a>Erhöhen der durch NPS verarbeiteten gleichzeitigen Authentifizierungen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema Anweisungen zum Konfigurieren des Netzwerkrichtlinienservers gleichzeitiger Authentifizierungen verwenden.

Bei der Installation des Netzwerkrichtlinienservers \(NPS\) auf einem anderen Computer als eine Domäne einer Controller und dem NPS ist eine große Anzahl von authentifizierungsanforderungen pro Sekunde empfangen, können Sie NPS-Leistung durch Erhöhen der Anzahl der verbessern gleichzeitiger Authentifizierungen, die zwischen den NPS- und dem Domänencontroller zulässig.

Zu diesem Zweck müssen Sie den folgenden Registrierungsschlüssel bearbeiten: 

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Netlogon\Parameters`

Fügen Sie einen neuen Wert, der mit dem Namen **"MaxConcurrentApi"** und weisen Sie es einen Wert zwischen 2 und 5. 

>[!CAUTION]
>Wenn Sie einen Wert zuzuweisen **"MaxConcurrentApi"** ist zu hoch, den NPS möglicherweise einen übermäßigen Last auf Ihrem Domänencontroller platzieren.

Weitere Informationen zum Verwalten von NPS finden Sie unter [Verwalten des Netzwerkrichtlinienservers](nps-manage-top.md).

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).