---
title: secedit validate
description: Referenz Artikel zum Validate-Befehl "Secedit", mit dem die in einer Sicherheits Vorlage gespeicherten Sicherheitseinstellungen überprüft werden.
ms.topic: reference
ms.assetid: 9fb06354-f55a-4ca4-9fbc-9a872eb9b9cf
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 057573cf5bc28a47f5140fb58e23ee1ed4bbc4c1
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388101"
---
# <a name="secedit-validate"></a>secedit/Validate

Überprüft die Sicherheitseinstellungen, die in einer Sicherheits Vorlage (INF-Datei) gespeichert sind. Das Überprüfen von Sicherheits Vorlagen kann Ihnen helfen, zu bestimmen, ob eine beschädigte oder nicht ordnungsgemäß festgelegt ist. Beschädigte oder falsch festgelegte Sicherheits Vorlagen werden nicht angewendet.

## <a name="syntax"></a>Syntax

```
secedit /validate <configuration file name>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<configuration file name>` | Erforderlich. Gibt den Pfad und den Dateinamen für die Sicherheits Vorlage an, die überprüft wird. Die Protokolldateien werden mit diesem Befehl nicht aktualisiert. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um zu überprüfen, ob die Datei "Rollback. inf", " *secrbkconfiguration. inf*", nach dem Rollback weiterhin gültig ist:

```
secedit /validate secRBKcontoso.inf
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [secedit/analyze](secedit-analyze.md)

- [secedit/configure](secedit-configure.md)

- [secedit/Export](secedit-export.md)

- [secedit/generaterollback](secedit-generaterollback.md)

- [secedit/Import](secedit-import.md)