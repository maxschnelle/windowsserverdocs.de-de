---
title: subst
description: Erfahren Sie, wie Sie einen Pfad mit einem Laufwerk Buchstaben verknüpfen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3e69234c-2312-4343-868b-afc1017c622a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 43cbc57aba29ea0b9150dccdfc566a93017a09a5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833643"
---
# <a name="subst"></a>subst



Ordnet einen Pfad einem Laufwerk Buchstaben zu. Bei Verwendung ohne Parameter zeigt **subst** die Namen der virtuellen Laufwerke an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
subst [<Drive1>: [<Drive2>:]<Path>] 
subst <Drive1>: /d
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Drive1 >:|Gibt das virtuelle Laufwerk an, dem Sie einen Pfad zuweisen möchten.|
|[\<drive2 >:]\<Pfad >|Gibt das physische Laufwerk und den Pfad an, die einem virtuellen Laufwerk zugewiesen werden sollen.|
|/d|Löscht ein ersetzes (virtuelles) Laufwerk.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Die folgenden Befehle funktionieren nicht und dürfen nicht auf Laufwerken verwendet werden, die im **subst** -Befehl angegeben sind:

    **chkdsk**

    **diskcomp**

    **diskcopy**

    **format**

    **label**

    **recover**
-   Der *Drive1* -Parameter muss innerhalb des Bereichs liegen, der durch den **LastDrive** -Befehl angegeben wird. Andernfalls zeigt **subst** die folgende Fehlermeldung an:

    `Invalid parameter - drive1:`

## <a name="examples"></a><a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um ein virtuelles Laufwerk Z für den Pfad b:\user\tool\forms zu erstellen:
```
subst z: b:\user\betty\forms 
```
Anstatt den vollständigen Pfad einzugeben, können Sie dieses Verzeichnis erreichen, indem Sie den Buchstaben des virtuellen Laufwerks gefolgt von einem Doppelpunkt wie folgt eingeben:
```
z: 
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)