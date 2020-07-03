---
title: convert basic
description: Referenz Artikel zum Convert Basic-Befehl, der einen leeren dynamischen Datenträger in einen Basis Datenträger konvertiert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 61329896-3b56-4959-8d58-45cbe18ba860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a61c3d9fd8d708a41347f0bcf46aa627e960153c
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928980"
---
# <a name="convert-basic"></a>convert basic

Konvertiert einen leeren dynamischen Datenträger in einen Basis Datenträger. Ein dynamischer Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl Datenträger [auswählen](select-disk.md) einen dynamischen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.

> [!IMPORTANT]
> Der Datenträger muss leer sein, um ihn in einen Basis Datenträger zu konvertieren. Sichern Sie Ihre Daten, und löschen Sie dann alle Partitionen oder Volumes, bevor Sie den Datenträger umstellen.

> [!NOTE]
> Anweisungen zur Verwendung dieses Befehls finden Sie unter [Ändern eines dynamischen Datenträgers zurück auf einen Basis](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc755238(v=ws.11))Datenträger.

## <a name="syntax"></a>Syntax

```
convert basic [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den ausgewählten dynamischen Datenträger in Basic zu konvertieren:

```
convert basic
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Convert-Befehl](convert.md)
