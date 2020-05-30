---
title: manage-bde-Sperre
description: Referenz Thema für den Befehl "manage-bde Lock", mit dem ein durch BitLocker geschütztes Laufwerk gesperrt wird, um den Zugriff darauf zu verhindern, wenn der entsperrungs Schlüssel nicht angegeben wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b8858e61-3a7e-4d03-8c98-5c09853f35e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 340dc7eb07eaab2583e8b325042803fd8fc82184
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222875"
---
# <a name="manage-bde-lock"></a>manage-bde-Sperre

Sperrt ein durch BitLocker geschütztes Laufwerk, um den Zugriff darauf zu verhindern, es sei denn, der Entsperrschlüssel wird bereitgestellt.

## <a name="syntax"></a>Syntax

```
manage-bde -lock [<drive>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<drive>` | Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar. |
| -Computername | Gibt an, dass "manage-bde. exe verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
| `<name>` | Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers. |
| -? oder /? | Zeigt eine kurze Hilfe an der Eingabeaufforderung an. |
| -Help oder-h | Zeigt die gesamte Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Zum Sperren von Daten Laufwerk D geben Sie Folgendes ein:

```
manage-bde –lock D:
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Manage-BDE"](manage-bde.md)
