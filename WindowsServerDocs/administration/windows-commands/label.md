---
title: label
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bbae8bdd-97d4-4566-9118-7c95aa07645f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 63603eda8d23b6f7b89b8d1ba858575a60e3c65c
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724516"
---
# <a name="label"></a>label



Hiermit wird die Volumebezeichnung (d. h. der Name) eines Datenträgers erstellt, geändert oder gelöscht. Bei Verwendung ohne Parameter ändert der Befehl " **Bezeichnung** " die aktuelle Volumebezeichnung oder löscht die vorhandene Bezeichnung.



## <a name="syntax"></a>Syntax

```
label [/mp] [<Volume>] [<Label>]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|/mp|Gibt an, dass das Volume als Einstellungspunkt oder Volumename behandelt werden soll.|
|\<Volume>|Gibt einen Laufwerk Buchstaben (gefolgt von einem Doppelpunkt), einen Einfügepunkt oder einen Volumenamen an. Wenn ein Volumename angegeben wird, ist der **/MP** -Parameter nicht erforderlich.|
|\<Bezeichnung>|Gibt die Bezeichnung für das Volume an.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

- In Windows werden die Volumebezeichnung und die Seriennummer (sofern eine) als Teil der Verzeichnis Auflistung angezeigt.
- Eine NTFS-Volumebezeichnung kann bis zu 32 Zeichen lang sein, einschließlich Leerzeichen. NTFS-Volumebezeichnungen behalten den Fall bei, der beim Erstellen der Bezeichnung verwendet wurde, und zeigen ihn an.
- Wenn Sie keinen Wert für den **Label** -Parameter angeben, zeigt der **Label** -Befehl die Ausgabe im folgenden Format an:  
  ```
  Volume in drive C: xxxxxxxxxxx 
  Volume Serial Number is xxxx-xxxx 
  Volume label (32 characters, ENTER for none)?
  ```  
  Sie können eine neue Volumebezeichnung eingeben oder die EINGABETASTE drücken, um die aktuelle Bezeichnung beizubehalten. Wenn Sie die EINGABETASTE drücken und das Volume derzeit über eine Bezeichnung verfügt, werden Sie mit dem Befehl **Bezeichnung** zur Eingabe der folgenden Meldung aufgefordert:  
  ```
  Delete current volume label (Y/N)?
  ```  
  Drücken Sie Y, um die Bezeichnung zu löschen, oder drücken Sie N, um die Bezeichnung beizubehalten.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um einen Datenträger in Laufwerk a mit Umsatz Informationen für Juli zu bezeichnen:
```
label a:sales-july
```
Um die aktuelle Bezeichnung für Laufwerk C zu löschen, führen Sie die folgenden Schritte aus:
1. Geben Sie an der Eingabeaufforderung Folgendes ein:  
   ```
   Label
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
3. Drücken Sie Y, um die aktuelle Bezeichnung zu löschen.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)