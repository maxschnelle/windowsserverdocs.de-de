---
title: bitsadmin getminretrydelay
description: Referenz Artikel für den bizadmin getminretrydelay-Befehl, der die Zeitspanne (in Sekunden) abruft, die der Dienst nach einem vorübergehenden Fehler wartet, bevor er versucht, die Datei zu übertragen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 54f0abab-c129-40ed-a603-50f464d26011
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 066eb9a2c967d9d5e92aa8dbad2001a65a682796
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927015"
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
