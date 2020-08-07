---
title: ftp cd
description: Referenz Artikel für den Befehl FTP CD, der das Arbeitsverzeichnis auf dem Remote Computer ändert.
ms.topic: article
ms.assetid: a574855a-31b4-45c6-bce2-581c7231c99b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f38e8ff306bfcdf200c260df6cb4160f27c316d0
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889565"
---
# <a name="ftp-cd"></a>ftp cd

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert das Arbeitsverzeichnis auf dem Remote Computer.

## <a name="syntax"></a>Syntax

```
cd <remotedirectory>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| <remotedirectory> | Gibt das Verzeichnis auf dem Remote Computer an, das Sie ändern möchten. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um das Verzeichnis auf dem Remote Computer in *docs*zu ändern:

```
cd Docs
```

Um das Verzeichnis auf dem Remote Computer in *Videos*zu ändern, geben Sie Folgendes ein:

```
cd  May Videos
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
