---
title: subst
description: Erfahren Sie, wie Sie einen Pfad mit einem Laufwerk Buchstaben verknüpfen.
ms.topic: article
ms.assetid: 3e69234c-2312-4343-868b-afc1017c622a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 385359a49ee1cc4df95a17bef6c2aed4704a2dcd
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87881952"
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
|[\<Drive2>:]\<Path>|Gibt das physische Laufwerk und den Pfad an, die einem virtuellen Laufwerk zugewiesen werden sollen.|
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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)