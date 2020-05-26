---
title: FTP-CD
description: Referenz Thema für den FTP-CD-Befehl, mit dem das Arbeitsverzeichnis auf dem Remote Computer geändert wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a574855a-31b4-45c6-bce2-581c7231c99b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dbeff9c2fca654120347f0f616325b700f5c9be3
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820000"
---
# <a name="ftp-cd"></a>FTP-CD

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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
