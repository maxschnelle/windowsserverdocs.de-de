---
title: Leistungsoptimierung für HTTP 1.1/2
description: Für HTTP 1.1/2-Empfehlungen zur leistungsoptimierung
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: IvanPash; GMonte
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: bf85efa88e377966135c23a548119f19c39cceba
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866371"
---
# <a name="performance-tuning-http-112"></a>Leistungsoptimierung für HTTP 1.1/2

HTTP/2 dient zum Verbessern der Leistung auf dem Client (z. B. Seitenladezeit in einem Browser). Auf dem Server kann er einen leichten Anstieg in der CPU-Kosten darstellen. Während der Server nicht mehr eine einzelne TCP-Verbindung für jede Anforderung erfordert, werden einige dieses Zustands jetzt in der HTTP-Ebene gespeichert werden. Darüber hinaus hat HTTP/2-Header-Komprimierung, die zusätzliche CPU-Auslastung darstellt.

Einige Situationen erfordern eine HTTP/1.1-fallback (HTTP/2-Verbindung zurücksetzen und stattdessen Herstellen einer neuen Verbindung, um die Verwendung von HTTP/1.1). Insbesondere benötigt Neuverhandlung von TLS und HTTP-Authentifizierung (mit Ausnahme von Basis- und Digestauthentifizierung) über HTTP/1.1-fallback. Obwohl dies overhead erzeugt wird, werden diese Vorgänge bereits impliziert eine Verzögerung und sind daher nicht besonders leistungsabhängigen.

## <a name="see-also"></a>Siehe auch
- [Web-Server zur leistungsoptimierung](index.md) 
- [IIS 10.0 zur leistungsoptimierung](tuning-iis-10.md)