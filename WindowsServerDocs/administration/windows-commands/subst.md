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
ms.openlocfilehash: 62ba0de33e69998e7d3e343b1e53c1de7e630e10
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721612"
---
# <a name="subst"></a>subst



Ordnet einen Pfad einem Laufwerk Buchstaben zu. Bei Verwendung ohne Parameter zeigt **subst** die Namen der virtuellen Laufwerke an.



## <a name="syntax"></a>Syntax

```
subst [<Drive1>: [<Drive2>:]<Path>] 
subst <Drive1>: /d
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<Drive1>:|Gibt das virtuelle Laufwerk an, dem Sie einen Pfad zuweisen möchten.|
|[\<Drive2>:] \<Pfad>|Gibt das physische Laufwerk und den Pfad an, die einem virtuellen Laufwerk zugewiesen werden sollen.|
|/d|Löscht ein ersetzes (virtuelles) Laufwerk.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)