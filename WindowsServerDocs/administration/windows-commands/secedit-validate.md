---
title: 'secedit: Validate'
description: Referenz Artikel für * * * *-
ms.topic: reference
ms.assetid: 9fb06354-f55a-4ca4-9fbc-9a872eb9b9cf
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: be7ae316a189203aa70769d1d37291f532166735
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635530"
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

## <a name="remarks"></a>Hinweise

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