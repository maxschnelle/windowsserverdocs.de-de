---
title: popd
description: Referenz Artikel für den PnPUtil-Befehl, der das aktuelle Verzeichnis in das Verzeichnis ändert, das zuletzt durch den Befehl pushd gespeichert wurde.
ms.topic: reference
ms.assetid: 8a4c52d5-9fd1-4eac-9c0c-5767b25728ed
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 07/11/2018
ms.openlocfilehash: 4884e294f878a55125a035d7113ce857e1964634
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89633655"
---
# <a name="popd"></a>popd

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der Befehl " **popd** " ändert das aktuelle Verzeichnis in das Verzeichnis, das zuletzt durch den Befehl " **pushd** " gespeichert wurde.

Jedes Mal, wenn Sie den Befehl **pushd** verwenden, wird ein einzelnes Verzeichnis für ihre Verwendung gespeichert. Sie können jedoch mehrere Verzeichnisse mehrmals mit dem Befehl **pushd** speichern. Die Verzeichnisse werden sequenziell in einem virtuellen Stapel gespeichert. Wenn Sie also den **pushd-** Befehl einmal verwenden, wird das Verzeichnis, in dem Sie den Befehl verwenden, am unteren Rand des Stapels platziert. Wenn Sie den Befehl erneut verwenden, wird das zweite Verzeichnis auf dem ersten Verzeichnis platziert. Der Vorgang wird jedes Mal wiederholt, wenn Sie den Befehl **pushd** verwenden.

Wenn Sie den **popd-** Befehl verwenden, wird das Verzeichnis am Anfang des Stapels entfernt, und das aktuelle Verzeichnis wird in dieses Verzeichnis geändert. Wenn Sie den Befehl " **popd** " erneut verwenden, wird das nächste Verzeichnis auf dem Stapel entfernt. Wenn Befehls Erweiterungen aktiviert sind, entfernt der **popd-** Befehl alle Zuordnungen von Laufwerk Buchstaben, die durch den Befehl **pushd** erstellt wurden.

## <a name="syntax"></a>Syntax

```
popd
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Wenn Sie das aktuelle Verzeichnis von dem Verzeichnis, in dem das Batch Programm ausgeführt wurde, ändern und es anschließend wieder ändern möchten, geben Sie Folgendes ein:

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

- [pushd](pushd.md)
