---
title: fsutil hardlink
description: Referenz Artikel für den Befehl "ssutil hardlink", mit dem eine feste Verknüpfung zwischen einer vorhandenen Datei und einer neuen Datei erstellt wird.
manager: dmoss
ms.author: toklima
author: toklima
ms.assetid: 835fc6f1-cc84-4189-b29a-dde90792469e
ms.topic: reference
ms.date: 10/16/2017
ms.openlocfilehash: 9d3782736686106b892f3b35e74573e4e162ae80
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89037358"
---
# <a name="fsutil-hardlink"></a>fsutil hardlink

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

Erstellt eine feste Verknüpfung zwischen einer vorhandenen Datei und einer neuen Datei. Ein fester Link ist ein Verzeichniseintrag für eine Datei. Jede Datei kann als mindestens eine feste Verknüpfung angesehen werden.

Auf NTFS-Volumes kann jede Datei über mehrere feste Links verfügen, sodass eine einzelne Datei in vielen Verzeichnissen (oder sogar im gleichen Verzeichnis mit unterschiedlichen Namen) angezeigt werden kann. Da alle Links auf dieselbe Datei verweisen, können Programme alle Links öffnen und die Datei ändern. Eine Datei wird nur dann aus dem Dateisystem gelöscht, nachdem alle Verknüpfungen damit gelöscht wurden. Nachdem Sie einen festen Link erstellt haben, kann er von Programmen wie jeder andere Dateiname verwendet werden.

## <a name="syntax"></a>Syntax

```
fsutil hardlink create <newfilename> <existingfilename>
fsutil hardlink list <filename>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| create | Legt eine NTFS-feste Verknüpfung zwischen einer vorhandenen Datei und einer neuen Datei fest. (Ein virtueller NTFS-Link ähnelt einem festen POSIX-Link.) |
| \<newfilename> | Gibt die Datei an, mit der Sie einen festen Link erstellen möchten. |
| \<existingfilename> | Gibt die Datei an, aus der ein fester Link erstellt werden soll. |
| list | Listet die festen Links zu *Dateiname*auf. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [fsutil](fsutil.md)
