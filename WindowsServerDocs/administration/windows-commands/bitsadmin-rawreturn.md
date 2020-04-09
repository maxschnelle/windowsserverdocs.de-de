---
title: bitsadmin rawreturn
description: Windows-Befehls Thema für **bisiadmin rawreturn**, das für die Verarbeitung geeignete Daten zurückgibt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bbe97130-26f6-4cdd-84f1-baf530ce38b7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e8cd84b6082b1fda8061ee7b324dd66991d3b206
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849883"
---
# <a name="bitsadmin-rawreturn"></a>bitsadmin rawreturn

Gibt Daten zurück, die für die-Verarbeitung geeignet sind. In der Regel verwenden Sie diesen Befehl zusammen mit den Switches **/Create** und **/Get***, um nur den Wert zu erhalten. Dieser Switch muss vor anderen Schaltern angegeben werden.

## <a name="syntax"></a>Syntax

```
bitsadmin /rawreturn
```

## <a name="remarks"></a>Hinweise

- Entfernt Zeilen mit Zeilen und Formatierungen aus der Ausgabe.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel werden die Rohdaten für den Status des Auftrags mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\>bitsadmin /rawreturn /getstate myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)