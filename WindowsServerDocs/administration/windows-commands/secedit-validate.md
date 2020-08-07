---
title: 'secedit: Validate'
description: Referenz Artikel für * * * *-
ms.topic: article
ms.assetid: 9fb06354-f55a-4ca4-9fbc-9a872eb9b9cf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 30bb02f0d7947aa77f7ac41d5f7b179ca8fd236b
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87882937"
---
# <a name="seceditvalidate"></a>secedit: Validate



Überprüft die Sicherheitseinstellungen, die in einer Sicherheits Vorlage (INF-Datei) gespeichert sind.

## <a name="syntax"></a>Syntax

```
Secedit /validate <configuration file name>

```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|Konfigurationsdateiname|Erforderlich.</br>Gibt den Pfad und den Dateinamen für die Sicherheits Vorlage an, die überprüft wird.|

## <a name="remarks"></a>Bemerkungen

Das Überprüfen von Sicherheits Vorlagen kann Ihnen helfen, wenn eine beschädigte oder nicht ordnungsgemäß festgelegt ist.

Eine ungültige Sicherheits Vorlage wird nicht angewendet.

Die Protokolldatei wird nicht aktualisiert.

In Windows Server 2008 wurde durch `Secedit /refreshpolicy` ersetzt `gpupdate` . Weitere Informationen zum Aktualisieren von Sicherheitseinstellungen finden Sie unter [gpupdate](gpupdate.md).

## <a name="examples"></a>Beispiele

Nachdem ein Rollback für eine Sicherheits Vorlage ausgeführt wurde, sollten Sie überprüfen, ob die Rollback-INF-Datei "secrbkconfiguration. inf" gültig ist.
```
Secedit /validate secRBKcontoso.inf
```

## <a name="additional-references"></a>Weitere Verweise

-   [Secedit:generaterollback](secedit-generaterollback.md)
-   [Secedit](secedit.md)
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)