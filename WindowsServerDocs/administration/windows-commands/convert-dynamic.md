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
ms.openlocfilehash: 3474da8c1f4a3e58d9e77c36abe4390ec2f5b731
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928975"
---
# <a name="convert-dynamic"></a>convert dynamic

Konvertiert einen Basis Datenträger in einen dynamischen Datenträger. Ein Basis Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Verwenden Sie den Befehl Datenträger [auswählen](select-disk.md) , um einen Basis Datenträger auszuwählen und den Fokus darauf zu verschieben.

> [!NOTE]
> Anweisungen zur Verwendung dieses Befehls finden Sie unter [Ändern eines dynamischen Datenträgers zurück auf einen Basis](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc755238(v=ws.11))Datenträger.

## <a name="syntax"></a>Syntax

```
convert dynamic [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

#### <a name="remarks"></a>Hinweise

- Alle vorhandenen Partitionen auf dem Basis Datenträger werden zu einfachen Volumes.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um einen einfachen Datenträger in einen dynamischen Datenträger zu konvertieren:

```
convert dynamic
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Convert-Befehl](convert.md)
