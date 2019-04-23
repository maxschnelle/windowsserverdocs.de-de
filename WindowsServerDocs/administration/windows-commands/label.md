---
title: label
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bbae8bdd-97d4-4566-9118-7c95aa07645f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6dea364b1afe385d03b0519538ff7bbd6bb9df28
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883251"
---
# <a name="label"></a>label



Erstellt, ändert oder löscht die Bezeichnung (d. h. der Name) eines Datenträgers. Wenn Sie ohne Angabe von Parametern die **Bezeichnung** Befehl ändert die aktuelle Bezeichnung oder die vorhandene Bezeichnung gelöscht.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
label [/mp] [<Volume>] [<Label>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/mp|Gibt an, dass das Volume als ein Punkt oder ein Volume Bereitstellungsname behandelt werden soll.|
|\<Volume >|Gibt einen Laufwerkbuchstaben (gefolgt von einem Doppelpunkt), Bereitstellungspunkt oder Name des Volumes. Wenn Sie ein Volumenamen angegeben wird, die **/MP** Parameter ist nicht erforderlich.|
|\<Label>|Gibt die Bezeichnung für das Volume.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Windows zeigt die Bezeichnung und Seriennummer (sofern vorhanden) als Teil der verzeichnisauflistung.
-   Eine NTFS-Volume-Bezeichnung kann bis zu 32 Zeichen lang sein, einschließlich Leerzeichen sein. NTFS-Volumebezeichnungen beibehalten werden sollen, und zeigen den Fall, der verwendet wurde, als Sie Bezeichnung erstellt wurde.
-   Wenn Sie einen Wert für nicht angeben der **Bezeichnung** -Parameter der **Bezeichnung** Befehl zeigt eine Ausgabe im folgenden Format:  
    ```
    Volume in drive C: xxxxxxxxxxx 
    Volume Serial Number is xxxx-xxxx 
    Volume label (32 characters, ENTER for none)?
    ```  
    Sie können eine neue Bezeichnung eingeben oder EINGABETASTE drücken, um die aktuelle Bezeichnung beibehalten. Wenn Sie die EINGABETASTE drücken und das Volume verfügt derzeit über eine Bezeichnung, die **Bezeichnung** Befehl werden Sie aufgefordert, mit der folgenden Meldung:  
    ```
    Delete current volume label (Y/N)?
    ```  
    Drücken Sie Y zum Löschen der Bezeichnung, oder drücken Sie N, um die Bezeichnung beibehalten.

## <a name="BKMK_examples"></a>Beispiele für

Um eine Diskette in Laufwerk A zu bezeichnen, die Verkaufsinformationen für Juli enthält, geben Sie Folgendes ein:
```
label a:sales-july
```
Um die aktuelle Bezeichnung für Laufwerk C: zu löschen, gehen Sie folgendermaßen vor:
1.  Geben Sie an einer Eingabeaufforderung Folgendes ein:  
    ```
    Label
    ```  
    Eine Ausgabe ähnlich der folgenden sollte angezeigt werden:  
    ```
    Volume in drive C: is Main Disk
    Volume Serial Number is 6789-ABCD
    Volume label (32 characters, ENTER for none)?
    ```  
2.  Drücken Sie die EINGABETASTE. Die folgende Meldung sollte angezeigt werden:  
    ```
    Delete current volume label (Y/N)?
    ```  
3.  Drücken Sie Y, um die aktuelle Bezeichnung zu löschen.

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)