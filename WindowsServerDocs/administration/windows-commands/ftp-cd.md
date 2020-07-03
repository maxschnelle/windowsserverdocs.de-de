---
title: ftp cd
description: Referenz Artikel für den Befehl FTP CD, der das Arbeitsverzeichnis auf dem Remote Computer ändert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a574855a-31b4-45c6-bce2-581c7231c99b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0442e2ad6070b84e84632bc6d8646b979d7f948b
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933289"
---
# <a name="ftp-cd"></a>ftp cd

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert das Arbeitsverzeichnis auf dem Remote Computer.

## <a name="syntax"></a>Syntax

```
cd <remotedirectory>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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

- [Zusätzlicher FTP-Leitfaden](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
