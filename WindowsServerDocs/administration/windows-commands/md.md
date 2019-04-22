---
title: md
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82162d00-cc34-4776-9e55-4b4836dbd6a9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1396038410ecc5db5a124a1768038c4f8c8bea8c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820841"
---
# <a name="md"></a>md



Erstellt ein Verzeichnis oder Unterverzeichnis.

> [!NOTE]
> Dieser Befehl ist identisch mit der **Mkdir** Befehl.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
md [<Drive>:]<Path>
mkdir [<Drive>:]<Path>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Laufwerk >:|Gibt das Laufwerk, auf dem Sie das neue Verzeichnis erstellen möchten.|
|\<Pfad >|Erforderlich. Gibt den Namen und Speicherort des neuen Verzeichnisses. Die maximale Länge jeder einzelnen Pfads richtet sich nach dem Dateisystem.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Befehlserweiterungen, die standardmäßig aktiviert sind, können Sie eine einzige **Md** Befehl zum Erstellen von zwischenverzeichnisse in einem angegebenen Pfad.

## <a name="BKMK_examples"></a>Beispiele für

Um ein Verzeichnis namens Directory1 im aktuellen Verzeichnis zu erstellen, geben Sie Folgendes ein:
```
md Directory1
```
Um die Verzeichnisstruktur Taxes\Property\Current im Stammverzeichnis mit befehlserweiterungen aktiviert zu erstellen, geben Sie Folgendes ein:
```
md \Taxes\Property\Current
```
Geben Sie die folgende Sequenz von Befehlen zum Erstellen der Verzeichnisstruktur Taxes\Property\Current in das Stammverzeichnis an, wie im vorherigen Beispiel, jedoch mit befehlserweiterungen deaktiviert:
```
md \Taxes
cd \Taxes 
md Property
cd Property
md Current
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)

[Cmd](cmd.md)