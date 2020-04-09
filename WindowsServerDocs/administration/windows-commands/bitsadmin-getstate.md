---
title: bitsadmin getstate
description: Windows-Befehls Thema für **bizadmin GetState**, das den Zustand des angegebenen Auftrags abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1252d6cf-14ca-44df-beb2-930ff011f297
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 43cd8c8e614cce65f55b16fc5395b1d37de0cf95
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850463"
---
# <a name="bitsadmin-getstate"></a>bitsadmin getstate

Ruft den Zustand des angegebenen Auftrags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getstate <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="output"></a>Ausgabe

Die Ausgabewerte umfassen Folgendes:

| Phase | Beschreibung |
| --------------- | ----------- |
| In Warteschlange | Der Auftrag wartet darauf, ausgeführt zu werden. |
| Verbindung wird aufgebaut | Bits kontaktiert den Server. |
| Tra | Bits überträgt Daten. |
| Übertragen | Bits hat erfolgreich alle Dateien im Auftrag übertragen. |
| Suspended | Der Auftrag wurde angehalten. |
| Error | Ein nicht BEHEB barer Fehler ist aufgetreten. die Übertragung wird nicht wiederholt. |
| Transient_Error | Ein BEHEB barer Fehler ist aufgetreten. der Übertragungs Versuch wird wiederholt, wenn die minimale Wiederholungs Verzögerung abläuft. |
| Gewürdigt | Der Auftrag wurde abgeschlossen. |
| Canceled | Der Auftrag wurde abgebrochen. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird der Status für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\>bitsadmin /getstate myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
