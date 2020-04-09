---
title: bitsadmin gettype
description: Windows-Befehls Thema für **bizadmin GetType**, das den Auftragstyp des angegebenen Auftrags abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bec16f04-3e95-4587-889e-3de6ad03c9c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 66a1fc5b0478e1eec26557dc9a7f76d50abcb8b6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850443"
---
# <a name="bitsadmin-gettype"></a>bitsadmin gettype

Ruft den Auftragstyp des angegebenen Auftrags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /gettype <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="output"></a>Ausgabe

Die Ausgabewerte umfassen Folgendes:

| Typ | Beschreibung |
| --------------- | ----------- |
| Herunterladen | Der Auftrag ist ein Download. |
| Hochladen | Der Auftrag ist ein Upload. |
| Upload-Antwort | Der Auftrag ist ein Upload-Antwort-Vorgang. |
| Unbekannt | Der Auftrag weist einen unbekannten Typ auf. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Das folgende Beispiel ruft den Auftragstyp für den Auftrag mit dem Namen *mydownloadjob*ab.

```
C:\>bitsadmin /gettype myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)