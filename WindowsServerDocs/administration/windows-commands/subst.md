---
title: subst
description: Erfahren Sie, wie Sie einen Pfad mit einem Laufwerkbuchstaben zuweisen.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3e69234c-2312-4343-868b-afc1017c622a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 858195de89ca8661cf47c25b6cf9b519cc4efbf8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858071"
---
# <a name="subst"></a>subst



Ordnet einen Pfad einen Laufwerkbuchstaben zu. Wenn Sie ohne Angabe von Parametern **Subst** zeigt die Namen der virtuellen Laufwerke in Kraft.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
subst [<Drive1>: [<Drive2>:]<Path>] 
subst <Drive1>: /d
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Laufwerk1 >:|Gibt das virtuelle Laufwerk an, das Sie dem angegebenen Pfad zuweisen möchten.|
|[\<Laufwerk2 >:]\<Pfad >|Gibt den physischen Laufwerk und Pfad, der Sie ein virtuelles Laufwerk zuweisen möchten.|
|/d|Löscht ein ersetzte (virtuelles) Laufwerk.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Die folgenden Befehle funktionieren nicht, und sollte nicht verwendet werden, auf Laufwerken, die im angegebenen die **Subst** Befehl:

    **chkdsk**

    **diskcomp**

    **diskcopy**

    **format**

    **label**

    **recover**
-   Die *Laufwerk1* Parameter muss innerhalb des Bereichs, der angegeben wird die **Lastdrive** Befehl. Wenn dies nicht der Fall ist, **Subst** wird die folgende Fehlermeldung angezeigt:

    `Invalid parameter - drive1:`

## <a name="BKMK_examples"></a>Beispiele für

Um ein virtuelles Laufwerk Z für den Pfad B:\User\Betty\Forms zu erstellen, geben Sie Folgendes ein:
```
subst z: b:\user\betty\forms 
```
Anstatt den vollständigen Pfad zu verwenden, können Sie dieses Verzeichnis erreichen, geben Sie die Buchstaben des virtuellen Laufwerks, gefolgt von einem Doppelpunkt wie folgt:
```
z: 
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)