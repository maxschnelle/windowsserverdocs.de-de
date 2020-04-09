---
title: pushd
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 396bc545-0f41-473e-b0ac-76fbbb74d390
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e7866a54e83bd57c8689512a1b75b151f74cb93c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837093"
---
# <a name="pushd"></a>pushd



Speichert das aktuelle Verzeichnis für die Verwendung durch den **popd** -Befehl und ändert sich dann in das angegebene Verzeichnis.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
pushd [<Path>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Pfad >|Gibt das Verzeichnis an, das das aktuelle Verzeichnis bilden soll. Dieser Befehl unterstützt relative Pfade.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Jedes Mal, wenn Sie den Befehl **pushd** verwenden, wird ein einzelnes Verzeichnis für ihre Verwendung gespeichert. Sie können jedoch mehrere Verzeichnisse mehrmals mit dem Befehl **pushd** speichern.

    Die Verzeichnisse werden sequenziell in einem virtuellen Stapel gespeichert. Wenn Sie den Befehl **pushd** einmal verwenden, wird das Verzeichnis, in dem Sie den Befehl verwenden, am unteren Rand des Stapels platziert. Wenn Sie den Befehl erneut verwenden, wird das zweite Verzeichnis auf dem ersten Verzeichnis platziert. Der Vorgang wird jedes Mal wiederholt, wenn Sie den Befehl **pushd** verwenden.

    Mit dem Befehl **popd** können Sie das aktuelle Verzeichnis in das Verzeichnis ändern, das zuletzt vom Befehl **pushd** gespeichert wurde. Wenn Sie den **popd-** Befehl verwenden, wird das Verzeichnis am oberen Rand des Stapels aus dem Stapel entfernt, und das aktuelle Verzeichnis wird in dieses Verzeichnis geändert. Wenn Sie den Befehl " **popd** " erneut verwenden, wird das nächste Verzeichnis auf dem Stapel entfernt.
-   Wenn Befehls Erweiterungen aktiviert sind, akzeptiert der **pushd-** Befehl entweder einen Netzwerkpfad oder den Buchstaben und Pfad eines lokalen Laufwerks.
-   Wenn Sie einen Netzwerkpfad angeben, weist der **pushd-** Befehl vorübergehend den höchsten nicht verwendeten Laufwerk Buchstaben zu (beginnend mit Z:) an die angegebene Netzwerkressource. Der Befehl ändert dann das aktuelle Laufwerk und Verzeichnis in das angegebene Verzeichnis auf dem neu zugewiesenen Laufwerk. Wenn Sie den Befehl " **popd** " mit aktivierter Befehls Erweiterung verwenden, entfernt der Befehl " **popd** " den von **pushd**erstellten Laufwerksbuchstaben.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird gezeigt, wie Sie den Befehl **pushd** und den Befehl **popd** in einem Batch Programm verwenden können, um das aktuelle Verzeichnis von dem Verzeichnis zu ändern, in dem das Batch Programm ausgeführt wurde, und es dann wieder zurück zu ändern:
```
@echo off
rem This batch file deletes all .txt files in a specified directory
pushd %1
del *.txt
popd
cls
echo All text files deleted in the %1 directory
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Popd](popd.md)