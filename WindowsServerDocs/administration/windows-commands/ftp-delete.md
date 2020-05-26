---
title: FTP löschen
description: Referenz Thema für den Befehl FTP DELETE, mit dem Dateien auf Remote Computern gelöscht werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 067c45f3-e4e8-4450-b8b6-836994f6adfe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 43ea2ef90f29970a42b0196717ce4d2d3552a32c
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83819951"
---
# <a name="ftp-delete"></a>FTP löschen

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löscht Dateien auf Remote Computern.

## <a name="syntax"></a>Syntax

```
delete <remotefile>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<remotefile>` | Gibt die Datei an, die gelöscht werden soll. |

### <a name="examples"></a>Beispiele

Um die Datei " *Test. txt* " auf dem Remote Computer zu löschen, geben Sie Folgendes ein:

```
delete test.txt
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
