---
title: bitsadmin getminretrydelay
description: Referenz Artikel für den bizadmin getminretrydelay-Befehl, der die Zeitspanne (in Sekunden) abruft, die der Dienst nach einem vorübergehenden Fehler wartet, bevor er versucht, die Datei zu übertragen.
ms.topic: reference
ms.assetid: 54f0abab-c129-40ed-a603-50f464d26011
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1f5bc6d69e7dbc46bc7e0df3a34ac97f37fda252
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89030308"
---
# <a name="bitsadmin-getminretrydelay"></a>bitsadmin getminretrydelay

Ruft die Zeitdauer in Sekunden ab, die der Dienst nach dem Auftreten eines vorübergehenden Fehlers wartet, bevor versucht wird, die Datei zu übertragen.

## <a name="syntax"></a>Syntax

```
bitsadmin /getminretrydelay <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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
