---
title: label
description: Referenz Thema für den Befehl "Bezeichnung", mit dem die Volumebezeichnung (d. h. der Name) eines Datenträgers erstellt, geändert oder gelöscht wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bbae8bdd-97d4-4566-9118-7c95aa07645f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f2d09328f79215c497bcb0ea4549b1f6ac227994
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817260"
---
# <a name="label"></a>label

Hiermit wird die Volumebezeichnung (d. h. der Name) eines Datenträgers erstellt, geändert oder gelöscht. Bei Verwendung ohne Parameter ändert der Befehl " **Bezeichnung** " die aktuelle Volumebezeichnung oder löscht die vorhandene Bezeichnung.

## <a name="syntax"></a>Syntax

```
label [/mp] [<volume>] [<label>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| /mp | Gibt an, dass das Volume als Einstellungspunkt oder Volumename behandelt werden soll. |
| `<volume>` | Gibt einen Laufwerk Buchstaben (gefolgt von einem Doppelpunkt), einen Einfügepunkt oder einen Volumenamen an. Wenn ein Volumename angegeben wird, ist der **/MP** -Parameter nicht erforderlich. |
| `<label>` | Gibt die Bezeichnung für das Volume an. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="remarks"></a>Hinweise

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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)