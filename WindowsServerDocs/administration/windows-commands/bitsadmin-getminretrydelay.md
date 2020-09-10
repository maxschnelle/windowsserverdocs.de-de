---
title: bitsadmin getminretrydelay
description: Referenz Artikel für den bizadmin getminretrydelay-Befehl, der die Zeitspanne (in Sekunden) abruft, die der Dienst nach einem vorübergehenden Fehler wartet, bevor er versucht, die Datei zu übertragen.
ms.topic: reference
ms.assetid: 54f0abab-c129-40ed-a603-50f464d26011
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: be71dc355e966b4a6ac627045f1ec5ceaf68f2d3
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631945"
---
# <a name="bitsadmin-getminretrydelay"></a>bitsadmin getminretrydelay

Ruft die Zeitdauer in Sekunden ab, die der Dienst nach dem Auftreten eines vorübergehenden Fehlers wartet, bevor versucht wird, die Datei zu übertragen.

## <a name="syntax"></a>Syntax

```
bitsadmin /getminretrydelay <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie die minimale Wiederholungs Verzögerung für den Auftrag mit dem Namen *mydownloadjob*ab:

```
bitsadmin /getminretrydelay myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
