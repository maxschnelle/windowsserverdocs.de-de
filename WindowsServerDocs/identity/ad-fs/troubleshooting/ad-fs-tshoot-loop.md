---
title: 'AD FS Problembehandlung: Schleifen Erkennung'
description: In diesem Dokument wird beschrieben, wie Sie die Schleifen Erkennung beheben.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2017
ms.topic: article
ms.openlocfilehash: e3d654f44ba75d9b647c0c1d9db7345c7ea75435
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953090"
---
# <a name="ad-fs-troubleshooting---loop-detection"></a>AD FS Problembehandlung: Schleifen Erkennung

Schleifen in AD FS treten auf, wenn eine vertrauende Seite ein gültiges Sicherheits Token fortlaufend ablehnt und zurück an AD FS umgeleitet wird.

## <a name="loop-detection-cookie"></a>Schleifen Erkennungs Cookie
Um dies zu verhindern, hat AD FS das als Schleifen Erkennungs Cookie bezeichnete Cookie implementiert. Standardmäßig wird von AD FS ein Cookie in die passiven Webclients mit dem Namen **msisloopdetectioncookie**geschrieben. Dieses Cookie enthält einen Zeitstempel-Wert und eine Anzahl von Token, die ausgegeben werden.  Dadurch können AD FS nachverfolgen, wie oft und wie oft ein Client die Verbunddienst innerhalb einer bestimmten Zeitspanne besucht hat.

Wenn ein passiver Client die Verbunddienst für ein Token innerhalb von 20 Sekunden fünf Mal besucht, löst AD FS den folgenden Fehler aus:

**MSIS7042: die Client Browsersitzung hat " {0} " Anforderungen in den letzten {1} Sekunden angegeben. Weitere Informationen erhalten Sie von Ihrem Administrator.**

Das Eintreten in unendliche Schleifen wird häufig durch eine nicht verhaltende Anwendung der vertrauenden Seite verursacht, die das von AD FS ausgegebene Token nicht erfolgreich nutzt, und die Anwendung sendet den passiven Client wiederholt an AD FS, wiederholt für ein neues Token.  AD FS gibt den passiven Client jedes Mal ein neues Token aus, solange nicht fünf Anforderungen innerhalb von 20 Sekunden überschritten werden.

## <a name="adjusting-the-loop-detection-cookie"></a>Anpassen des Cookies für die Schleifen Erkennung
Sie können PowerShell verwenden, um die Anzahl der ausgegebenen Token und den TimeSpan-Wert zu ändern.

```powershell
Set-AdfsProperties -LoopDetectionMaximumTokensIssuedInterval 5  -LoopDetectionTimeIntervalInSeconds 20
```
Der minimale Wert für **loopdetectionmaximumtekensissuedinterval** ist 1.

Der minimale Wert für **loopdetectiontimeintervalinseconds** ist 5.

Sie können die Schleifen Erkennung auch deaktivieren, wenn Sie Leistungstests durchgeführt haben.

```powershell
Set-AdfsProperties -EnableLoopDetection $false
```

>[!IMPORTANT]
>Es wird nicht empfohlen, die Schleifen Erkennung dauerhaft zu deaktivieren, da dadurch verhindert wird, dass Benutzer in Endlosschleifen Zustände eintreten.


## <a name="next-steps"></a>Nächste Schritte

- [Behandeln von AD FS-Problemen](ad-fs-tshoot-overview.md)



