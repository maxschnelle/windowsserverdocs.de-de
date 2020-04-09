---
title: bitsadmin nowrap
description: Windows-Befehls Thema für **bizadmin NoWrap**, das jede Zeile von Ausgabetext abschneidet, der über den äußersten rechten Rand des Befehls Fensters hinausgeht.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 85a47b90-783a-41e4-96f2-81f26ae8ca93
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f9f1db370d8a8917aa03a414a27623a1024df192
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850183"
---
# <a name="bitsadmin-nowrap"></a>bitsadmin nowrap

Verkürzt jede Zeile von Ausgabetext, der über den rechten Rand des Befehls Fensters hinausgeht. Standardmäßig wird die Ausgabe durch alle Switches außer dem **Monitor** Switch umschlossen. Geben Sie den Schalter " **nowrap** " vor anderen Switches an.

## <a name="syntax"></a>Syntax

```
bitsadmin /nowrap
```

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird der Status für den Auftrag mit dem Namen *mydownloadjob* abgerufen, und die Ausgabe wird nicht eingeschlossen.

```
C:\>bitsadmin /nowrap /getstate myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)