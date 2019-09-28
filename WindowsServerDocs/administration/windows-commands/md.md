---
title: md
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 965a5c506535a2c52d6cc7b3557c6104182c12a5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373689"
---
# <a name="md"></a>md



Erstellt ein Verzeichnis oder ein Unterverzeichnis.

> [!NOTE]
> Dieser Befehl ist mit dem Befehl " **mkdir** " identisch.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
md [<Drive>:]<Path>
mkdir [<Drive>:]<Path>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|> \<drive:|Gibt das Laufwerk an, auf dem das neue Verzeichnis erstellt werden soll.|
|\<path >|Erforderlich. Gibt den Namen und den Speicherort des neuen Verzeichnisses an. Die maximale Länge eines einzelnen Pfads wird vom Dateisystem festgelegt.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Befehls Erweiterungen, die standardmäßig aktiviert sind, ermöglichen die Verwendung eines einzelnen **MD** -Befehls, um zwischen Verzeichnisse in einem angegebenen Pfad zu erstellen.

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um ein Verzeichnis mit dem Namen directory1 innerhalb des aktuellen Verzeichnisses zu erstellen:
```
md Directory1
```
Geben Sie Folgendes ein, um die Verzeichnisstruktur taxes\property\current innerhalb des Stamm Verzeichnisses mit aktivierter Befehls Erweiterung zu erstellen:
```
md \Taxes\Property\Current
```
Um die Verzeichnisstruktur taxes\property\current innerhalb des Stamm Verzeichnisses wie im vorherigen Beispiel zu erstellen, aber mit deaktivierten Befehls Erweiterungen, geben Sie die folgende Befehlssequenz ein:
```
md \Taxes
cd \Taxes 
md Property
cd Property
md Current
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Cmd](cmd.md)