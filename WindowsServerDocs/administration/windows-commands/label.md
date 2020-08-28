---
title: label
description: Referenz Artikel für den Befehl Bezeichnung, der die Volumebezeichnung (d. h. den Namen) eines Datenträgers erstellt, ändert oder löscht.
ms.topic: reference
ms.assetid: bbae8bdd-97d4-4566-9118-7c95aa07645f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 486461059e90d0d1e1c6fa413e6db595f82924bb
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89028198"
---
# <a name="label"></a>label

Hiermit wird die Volumebezeichnung (d. h. der Name) eines Datenträgers erstellt, geändert oder gelöscht. Bei Verwendung ohne Parameter ändert der Befehl " **Bezeichnung** " die aktuelle Volumebezeichnung oder löscht die vorhandene Bezeichnung.

## <a name="syntax"></a>Syntax

```
label [/mp] [<volume>] [<label>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| /mp | Gibt an, dass das Volume als Einstellungspunkt oder Volumename behandelt werden soll. |
| `<volume>` | Gibt einen Laufwerk Buchstaben (gefolgt von einem Doppelpunkt), einen Einfügepunkt oder einen Volumenamen an. Wenn ein Volumename angegeben wird, ist der **/MP** -Parameter nicht erforderlich. |
| `<label>` | Gibt die Bezeichnung für das Volume an. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="remarks"></a>Bemerkungen

- In Windows werden die Volumebezeichnung und die Seriennummer (sofern eine) als Teil der Verzeichnis Auflistung angezeigt.

- Eine NTFS-Volumebezeichnung kann bis zu 32 Zeichen lang sein, einschließlich Leerzeichen. NTFS-Volumebezeichnungen behalten den Fall bei, der beim Erstellen der Bezeichnung verwendet wurde, und zeigen ihn an.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um einen Datenträger in Laufwerk a mit Umsatz Informationen für Juli zu bezeichnen:

```
label a:sales-july
```

Um die aktuelle Bezeichnung für Laufwerk C anzuzeigen und zu löschen, führen Sie die folgenden Schritte aus:

1. Geben Sie an der Eingabeaufforderung Folgendes ein:

   ```
   label
   ```

   Eine Ausgabe ähnlich der folgenden sollte angezeigt werden:

   ```
   Volume in drive C: is Main Disk
   Volume Serial Number is 6789-ABCD
   Volume label (32 characters, ENTER for none)?
   ```

2. Drücken Sie die EINGABETASTE. Die folgende Eingabeaufforderung sollte angezeigt werden:

   ```
   Delete current volume label (Y/N)?
   ```

3. Drücken Sie **Y** , um die aktuelle Bezeichnung zu löschen, oder **N** , wenn Sie die vorhandene Bezeichnung beibehalten möchten.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)