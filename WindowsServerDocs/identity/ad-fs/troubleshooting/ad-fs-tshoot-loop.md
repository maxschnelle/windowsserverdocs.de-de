---
title: AD FS-Problembehandlung – Erkennung einer Schleife
description: In diesem Dokument wird beschrieben, wie Schleife Erkennung behandeln
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: cc8eeb11e44da3b8f26b1ab94143c189bca9ed38
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830911"
---
# <a name="ad-fs-troubleshooting---loop-detection"></a>AD FS-Problembehandlung – Erkennung einer Schleife 
 
Schleifen in AD FS ausgegeben, wenn eine vertrauende Seite kontinuierlich lehnt einen gültigen Sicherheitstoken an AD FS umgeleitet.

## <a name="loop-detection-cookie"></a>Schleife Erkennung cookie
Um dies zu verhindern, hat AD FS implementiert, die Schleife Erkennung Cookie bezeichnet wird. Standardmäßig schreibt die AD FS ein Cookie für passive Webclients mit dem Namen **MSISLoopDetectionCookie**. Dieses Cookie enthält einen Timestamp-Wert und eine Anzahl von Token ausgegebenen Wert.  Dadurch wird die AD FS, zu verfolgen, wie oft und wie oft ein Client den Verbunddienst in einer bestimmten Zeitspanne besucht hat.

Wenn eine passive Client besucht löst den Verbunddienst für ein Token fünf (5) Mal innerhalb von 20 Sekunden, AD FS den folgenden Fehler:

**MSIS7042: Wurde von der gleichen Clientbrowsersitzung "{0}: Anforderungen in den letzten"{1}"Sekunden. Weitere Informationen erhalten Sie von Ihrem Administrator.**

Eingabe in Endlosschleifen wird oft durch ein fehlerhaftes Verhalten aufweist, die Sie der vertrauenden Seite, die nicht erfolgreich das von AD FS ausgestellten Token verwendet verursacht, und der Anwendung gesendeten passiven Client wieder zu AD FS wiederholt für ein neues Token.  AD FS ist, wird dem passive Client ein neues Token jedes Mal, solange sie nicht 5 Anforderungen innerhalb von 20 Sekunden überschritten werden. 

## <a name="adjusting-the-loop-detection-cookie"></a>Anpassen der Schleife Erkennung von Cookies
Sie können PowerShell verwenden, um die Anzahl der Token ausgestellt werden, Wert und den Timespan-Wert zu ändern.

```powershell
Set-AdfsProperties -LoopDetectionMaximumTokensIssuedInterval 5  -LoopDetectionTimeIntervalInSeconds 20
```
Der Mindestwert für **LoopDetectionMaximumTokensIssuedInterval** ist 1.

Der Mindestwert für **LoopDetectionTimeIntervalInSeconds** ist 5.

Sie können auch die Erkennung der Schleife deaktivieren, wenn Sie Leistungstests durchführen.

```powershell
Set-AdfsProperties -EnableLoopDetection $false
```

>[!IMPORTANT]
>Es ist jedoch davon abgeraten, um Erkennung von Schleife dauerhaft zu deaktivieren, wie dies dadurch verhindert, dass Benutzer in die Endlosschleife Zustände eingeben.


## <a name="next-steps"></a>Nächste Schritte

- [AD FS-Problembehandlung](ad-fs-tshoot-overview.md)



