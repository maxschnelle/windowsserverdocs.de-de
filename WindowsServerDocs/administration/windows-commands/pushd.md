---
title: pushd
description: Referenz Artikel für den Befehl pushd, der das aktuelle Verzeichnis für die Verwendung durch den Befehl popd speichert und dann in das angegebene Verzeichnis wechselt.
ms.topic: reference
ms.assetid: 396bc545-0f41-473e-b0ac-76fbbb74d390
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 06a12b598472fa23ee0a211e7f42c33a47a3d64c
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639606"
---
# <a name="pushd"></a>pushd

Speichert das aktuelle Verzeichnis für die Verwendung durch den **popd** -Befehl und ändert sich dann in das angegebene Verzeichnis.

Jedes Mal, wenn Sie den Befehl **pushd** verwenden, wird ein einzelnes Verzeichnis für ihre Verwendung gespeichert. Sie können jedoch mehrere Verzeichnisse mehrmals mit dem Befehl **pushd** speichern. Die Verzeichnisse werden sequenziell in einem virtuellen Stapel gespeichert. Wenn Sie also den **pushd-** Befehl einmal verwenden, wird das Verzeichnis, in dem Sie den Befehl verwenden, am unteren Rand des Stapels platziert. Wenn Sie den Befehl erneut verwenden, wird das zweite Verzeichnis auf dem ersten Verzeichnis platziert. Der Vorgang wird jedes Mal wiederholt, wenn Sie den Befehl **pushd** verwenden.

Wenn Sie den **popd-** Befehl verwenden, wird das Verzeichnis am Anfang des Stapels entfernt, und das aktuelle Verzeichnis wird in dieses Verzeichnis geändert. Wenn Sie den Befehl " **popd** " erneut verwenden, wird das nächste Verzeichnis auf dem Stapel entfernt. Wenn Befehls Erweiterungen aktiviert sind, entfernt der **popd-** Befehl alle Zuordnungen von Laufwerk Buchstaben, die durch den Befehl **pushd** erstellt wurden.

## <a name="syntax"></a>Syntax

```
pushd [<path>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<path>` | Gibt das Verzeichnis an, das das aktuelle Verzeichnis bilden soll. Dieser Befehl unterstützt relative Pfade. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Wenn Befehls Erweiterungen aktiviert sind, akzeptiert der **pushd-** Befehl entweder einen Netzwerkpfad oder den Buchstaben und Pfad eines lokalen Laufwerks.

- Wenn Sie einen Netzwerkpfad angeben, weist der **pushd-** Befehl vorübergehend den höchsten nicht verwendeten Laufwerk Buchstaben zu (beginnend mit Z:) an die angegebene Netzwerkressource. Der Befehl ändert dann das aktuelle Laufwerk und Verzeichnis in das angegebene Verzeichnis auf dem neu zugewiesenen Laufwerk. Wenn Sie den Befehl " **popd** " mit aktivierter Befehls Erweiterung verwenden, entfernt der Befehl " **popd** " den von **pushd**erstellten Laufwerksbuchstaben.

### <a name="examples"></a>Beispiele

So ändern Sie das aktuelle Verzeichnis von dem Verzeichnis, in dem das Batch Programm ausgeführt wurde, und ändern Sie es anschließend erneut:

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

- [Befehl "POPD"](popd.md)
