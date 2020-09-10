---
title: ftp cd
description: Referenz Artikel für den Befehl FTP CD, der das Arbeitsverzeichnis auf dem Remote Computer ändert.
ms.topic: reference
ms.assetid: a574855a-31b4-45c6-bce2-581c7231c99b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f315fea0d7fea0f894921d5e2b0a8d1b5cea39e6
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89638527"
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
