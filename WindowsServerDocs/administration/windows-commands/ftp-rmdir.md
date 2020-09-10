---
title: ftp rmdir
description: Referenz Artikel für den FTP-Befehl rmdir, mit dem ein Stammverzeichnis gelöscht wird.
ms.topic: reference
ms.assetid: cf4778a4-9534-49c7-a061-850dc3504a67
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 53ba40b22b7bf83794ed2bc05d00fc02f79598c1
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89621600"
---
# <a name="ftp-rmdir"></a>ftp rmdir

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löscht ein Remoteverzeichnis.

## <a name="syntax"></a>Syntax

```
rmdir <directory>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<directory>` | Gibt den Namen des zu löschenden Remote Verzeichnisses an. |

### <a name="examples"></a>Beispiele

Um das *Bild* Remote Verzeichnis zu löschen, geben Sie Folgendes ein:

```
rmdir pictures
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
