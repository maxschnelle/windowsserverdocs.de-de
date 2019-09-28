---
title: 'AD FS Problembehandlung: Schleifen Erkennung'
description: In diesem Dokument wird beschrieben, wie Sie die Schleifen Erkennung beheben.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 2f8842dc53756cc4f65b6d6794a8c4952e111c00
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385345"
---
# <a name="ad-fs-troubleshooting---loop-detection"></a>AD FS Problembehandlung: Schleifen Erkennung 
 
Schleifen in AD FS treten auf, wenn eine vertrauende Seite ein gültiges Sicherheits Token fortlaufend ablehnt und zurück an AD FS umgeleitet wird.

## <a name="loop-detection-cookie"></a>Schleifen Erkennungs Cookie
Um dies zu verhindern, hat AD FS das als Schleifen Erkennungs Cookie bezeichnete Cookie implementiert. Standardmäßig wird von AD FS ein Cookie in die passiven Webclients mit dem Namen **msisloopdetectioncookie**geschrieben. Dieses Cookie enthält einen Zeitstempel-Wert und eine Anzahl von Token, die ausgegeben werden.  Dadurch können AD FS nachverfolgen, wie oft und wie oft ein Client die Verbunddienst innerhalb einer bestimmten Zeitspanne besucht hat.

Wenn ein passiver Client die Verbunddienst für ein Token innerhalb von 20 Sekunden fünf Mal besucht, löst AD FS den folgenden Fehler aus:

**MSIS7042: Dieselbe Client Browsersitzung hat "{0}" Anforderungen in den letzten "{1}" Sekunden gestellt. Weitere Informationen erhalten Sie vom Administrator.**

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



