---
title: bitsadmin getstate
description: Referenz Artikel für den bizadmin GetState-Befehl, der den Zustand des angegebenen Auftrags abruft.
ms.topic: reference
ms.assetid: 1252d6cf-14ca-44df-beb2-930ff011f297
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2faf05bd245f0b59eb9f10d0d46d96e8e1d3e11c
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631658"
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
