---
title: bitsadmin getstate
description: Referenz Artikel für den bizadmin GetState-Befehl, der den Zustand des angegebenen Auftrags abruft.
ms.topic: article
ms.assetid: 1252d6cf-14ca-44df-beb2-930ff011f297
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 38ad3cedbd4dc9b0cc3d5e855ea4fabd1736b6aa
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893847"
---
# <a name="bitsadmin-getstate"></a>bitsadmin getstate

Ruft den Zustand des angegebenen Auftrags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getstate <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

#### <a name="output"></a>Output

Die zurückgegebenen Ausgabewerte können wie folgt lauten:

| State | BESCHREIBUNG |
| --------------- | ----------- |
| In Warteschlange | Der Auftrag wartet darauf, ausgeführt zu werden. |
| Verbindung | Bits kontaktiert den Server. |
| Übertragung wird ausgeführt | Bits überträgt Daten. |
| Übertragen | Bits hat erfolgreich alle Dateien im Auftrag übertragen. |
| Ausgesetzt | Der Auftrag wurde angehalten. |
| Fehler | Ein nicht BEHEB barer Fehler ist aufgetreten. die Übertragung wird nicht wiederholt. |
| Transient_Error | Ein BEHEB barer Fehler ist aufgetreten. der Übertragungs Versuch wird wiederholt, wenn die minimale Wiederholungs Verzögerung abläuft. |
| Bestätigt | Der Auftrag wurde abgeschlossen. |
| Canceled | Der Auftrag wurde abgebrochen. |

## <a name="examples"></a>Beispiele

So rufen Sie den Status des Auftrags mit dem Namen *mydownloadjob*ab

```
bitsadmin /getstate myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
