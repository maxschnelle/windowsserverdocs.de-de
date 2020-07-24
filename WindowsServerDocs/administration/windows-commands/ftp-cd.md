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
ms.openlocfilehash: 0676021eb923ef3f1c9225de624bb58e47a70c3c
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86957982"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
