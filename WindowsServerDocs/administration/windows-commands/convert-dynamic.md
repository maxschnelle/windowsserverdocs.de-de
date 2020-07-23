---
title: convert dynamic
description: Referenz Artikel zum Convert Dynamic-Befehl, mit dem ein Basis Datenträger in einen dynamischen Datenträger konvertiert wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7b8fa4b1-850f-4e48-b05f-871c883ea33c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8c57986bf46dc7d22eeecfb6d7ad085f5e3f7e8c
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86958542"
---
# <a name="convert-dynamic"></a>convert dynamic

Konvertiert einen Basis Datenträger in einen dynamischen Datenträger. Ein Basis Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Verwenden Sie den Befehl Datenträger [auswählen](select-disk.md) , um einen Basis Datenträger auszuwählen und den Fokus darauf zu verschieben.

> [!NOTE]
> Anweisungen zur Verwendung dieses Befehls finden Sie unter [Ändern eines dynamischen Datenträgers zurück auf einen Basis](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc755238(v=ws.11))Datenträger.

## <a name="syntax"></a>Syntax

```
convert dynamic [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

#### <a name="remarks"></a>Bemerkungen

- Alle vorhandenen Partitionen auf dem Basis Datenträger werden zu einfachen Volumes.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um einen einfachen Datenträger in einen dynamischen Datenträger zu konvertieren:

```
convert dynamic
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Convert-Befehl](convert.md)
