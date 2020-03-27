---
title: Erhöhen der durch NPS verarbeiteten gleichzeitigen Authentifizierungen
description: Dieses Thema enthält Anweisungen zum Konfigurieren der gleichzeitigen Authentifizierungen von Netzwerk Richtlinien Servern in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 2d9cdada-0625-41c8-8248-a32259b03e47
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 5397a1de41717dfc65ee0b0582c1289c6a53b33a
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316294"
---
# <a name="increase-concurrent-authentications-processed-by-nps"></a>Erhöhen der durch NPS verarbeiteten gleichzeitigen Authentifizierungen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema finden Sie Anweisungen zum Konfigurieren der gleichzeitigen Authentifizierungen von Netzwerk Richtlinien Servern.

Wenn Sie den Netzwerk Richtlinien Server \(NPS-\) auf einem anderen Computer als einem Domänen Controller installiert haben und der NPS eine große Anzahl von Authentifizierungsanforderungen pro Sekunde empfängt, können Sie die NPS-Leistung verbessern, indem Sie die Anzahl der gleichzeitigen Authentifizierungen erhöhen, die zwischen dem NPS und dem Domänen Controller zulässig sind.

Zu diesem Zweck müssen Sie den folgenden Registrierungsschlüssel bearbeiten: 

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Netlogon\Parameters`

Fügen Sie einen neuen Wert mit dem Namen " **MaxConcurrentApi** " hinzu, und weisen Sie ihm einen Wert zwischen 2 und 5 zu. 

>[!CAUTION]
>Wenn Sie **MaxConcurrentApi einen zu hohen Wert für MaxConcurrentApi** zuweisen, kann Ihr Domänen Controller durch die NPS übermäßig stark ausgelastet werden.

Weitere Informationen zum Verwalten von NPS finden Sie unter [Verwalten des Netzwerk Richtlinien Servers](nps-manage-top.md).

Weitere Informationen zu NPS finden Sie unter [Netzwerk Richtlinien Server (Network Policy Server, NPS)](nps-top.md).