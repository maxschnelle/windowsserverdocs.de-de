---
title: Leistungsoptimierung für HTTP 1.1/2
description: Empfehlungen zur Leistungsoptimierung für HTTP 1.1/2
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: ivanpash; gmonte
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: a0a4464d7a13911ec9cc7d104b6fe9292a64586e
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471245"
---
# <a name="performance-tuning-http-112"></a>Leistungsoptimierung HTTP 1.1/2

HTTP/2 soll die Leistung auf Clientseite verbessern (z. b. Seitenladezeit in einem Browser). Auf dem-Server kann dies einen geringfügigen Anstieg der CPU-Kosten darstellen. Während der Server für jede Anforderung keine einzige TCP-Verbindung benötigt, wird ein Teil dieses Zustands nun in der HTTP-Ebene beibehalten. Außerdem verfügt http/2 über eine Header Komprimierung, die eine zusätzliche CPU-Auslastung darstellt.

Für einige Situationen ist ein HTTP/1.1-Fall Back erforderlich (Zurücksetzen der http/2-Verbindung und stattdessen das Einrichten einer neuen Verbindung für die Verwendung von HTTP/1.1). Insbesondere für die TLS-Aushandlung und die HTTP-Authentifizierung (außer Basic und Digest) ist ein HTTP/1.1-Fallback erforderlich. Obwohl dadurch mehr Aufwand entsteht, implizieren diese Vorgänge bereits einige Verzögerungen und sind daher nicht besonders Leistungs sensibel.

## <a name="additional-references"></a>Zusätzliche Referenzen
- [Leistungsoptimierung für Webserver](index.md)
- [IIS 10.0-Leistungsfeineinstellung](tuning-iis-10.md)