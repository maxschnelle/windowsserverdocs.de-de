---
title: 'secedit: Validate'
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9fb06354-f55a-4ca4-9fbc-9a872eb9b9cf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b93ad6ceadb08f6df8390edc3fc454d951519aad
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83821097"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Secedit:generaterollback](secedit-generaterollback.md)
-   [Secedit](secedit.md)
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)