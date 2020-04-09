---
title: Leistungsoptimierung für HTTP 1.1/2
description: Empfehlungen zur Leistungsoptimierung für HTTP 1.1/2
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: ivanpash; gmonte
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 5e62f7428f015193896aba5c7d9c146bd11e7225
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851683"
---
# <a name="performance-tuning-http-112"></a>Leistungsoptimierung HTTP 1.1/2

HTTP/2 soll die Leistung auf Clientseite verbessern (z. b. Seitenladezeit in einem Browser). Auf dem-Server kann dies einen geringfügigen Anstieg der CPU-Kosten darstellen. Während der Server für jede Anforderung keine einzige TCP-Verbindung benötigt, wird ein Teil dieses Zustands nun in der HTTP-Ebene beibehalten. Außerdem verfügt http/2 über eine Header Komprimierung, die eine zusätzliche CPU-Auslastung darstellt.

Für einige Situationen ist ein HTTP/1.1-Fall Back erforderlich (Zurücksetzen der http/2-Verbindung und stattdessen das Einrichten einer neuen Verbindung für die Verwendung von HTTP/1.1). Insbesondere für die TLS-Aushandlung und die HTTP-Authentifizierung (außer Basic und Digest) ist ein HTTP/1.1-Fallback erforderlich. Obwohl dadurch mehr Aufwand entsteht, implizieren diese Vorgänge bereits einige Verzögerungen und sind daher nicht besonders Leistungs sensibel.

## <a name="see-also"></a>Siehe auch
- [Leistungsoptimierung für Webserver](index.md) 
- [IIS 10.0-Leistungsfeineinstellung](tuning-iis-10.md)