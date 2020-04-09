---
title: label
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bbae8bdd-97d4-4566-9118-7c95aa07645f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7ccb86e2167682e1048161f2d5f5386a8b5cf6ed
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841173"
---
# <a name="label"></a>label



Hiermit wird die Volumebezeichnung (d. h. der Name) eines Datenträgers erstellt, geändert oder gelöscht. Bei Verwendung ohne Parameter ändert der Befehl " **Bezeichnung** " die aktuelle Volumebezeichnung oder löscht die vorhandene Bezeichnung.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
label [/mp] [<Volume>] [<Label>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/mp|Gibt an, dass das Volume als Einstellungspunkt oder Volumename behandelt werden soll.|
|\<Volume >|Gibt einen Laufwerk Buchstaben (gefolgt von einem Doppelpunkt), einen Einfügepunkt oder einen Volumenamen an. Wenn ein Volumename angegeben wird, ist der **/MP** -Parameter nicht erforderlich.|
|\<Bezeichnung >|Gibt die Bezeichnung für das Volume an.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

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

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um einen Datenträger in Laufwerk a mit Umsatz Informationen für Juli zu bezeichnen:
```
label a:sales-july
```
Um die aktuelle Bezeichnung für Laufwerk C zu löschen, führen Sie die folgenden Schritte aus:
1. Geben Sie an einer Eingabeaufforderung Folgendes ein:  
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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)