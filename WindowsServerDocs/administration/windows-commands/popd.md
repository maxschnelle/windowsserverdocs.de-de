---
title: popd
description: Erfahren Sie, wie Sie das Verzeichnis in das Verzeichnis ändern, das zuletzt vom Befehl pushd gespeichert wurde.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8a4c52d5-9fd1-4eac-9c0c-5767b25728ed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: a1638f8d0d62b730578cb21fac5a74e58ad06b74
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723296"
---
# <a name="popd"></a>popd

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert das aktuelle Verzeichnis in das Verzeichnis, das zuletzt durch den Befehl **pushd** gespeichert wurde.


## <a name="syntax"></a>Syntax
```
popd
```

#### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen
-   Jedes Mal, wenn Sie den Befehl **pushd** verwenden, wird ein einzelnes Verzeichnis für ihre Verwendung gespeichert. Sie können jedoch mehrere Verzeichnisse mehrmals mit dem Befehl **pushd** speichern.
    Die Verzeichnisse werden sequenziell in einem virtuellen Stapel gespeichert. Wenn Sie den Befehl **pushd** einmal verwenden, wird das Verzeichnis, in dem Sie den Befehl verwenden, am unteren Rand des Stapels platziert. Wenn Sie den Befehl erneut verwenden, wird das zweite Verzeichnis auf dem ersten Verzeichnis platziert. Der Vorgang wird jedes Mal wiederholt, wenn Sie den Befehl **pushd** verwenden.
    Mit dem Befehl **popd** können Sie das aktuelle Verzeichnis in das Verzeichnis ändern, das zuletzt vom Befehl **pushd** gespeichert wurde. Wenn Sie den **popd-** Befehl verwenden, wird das Verzeichnis am oberen Rand des Stapels aus dem Stapel entfernt, und das aktuelle Verzeichnis wird in dieses Verzeichnis geändert. Wenn Sie den Befehl " **popd** " erneut verwenden, wird das nächste Verzeichnis auf dem Stapel entfernt.
-   Wenn Befehls Erweiterungen aktiviert sind, entfernt der **popd-** Befehl alle von **pushd**erstellten Laufwerksbuchstaben-Zuweisungen.

## <a name="examples"></a><a name="BKMK_examples"></a>Beispiele
Zeigt, wie Sie den Befehl **pushd** und den Befehl **popd** in einem Batch Programm verwenden können, um das aktuelle Verzeichnis von dem Verzeichnis zu ändern, in dem das Batch Programm ausgeführt wurde, und es dann wieder zurück zu ändern:

```
@echo off
rem This batch file deletes all .txt files in a specified directory
pushd %1
del *.txt
popd
cls
echo All text files deleted in the %1 directory
```

## <a name="additional-references"></a>Zusätzliche Referenzen
-   [pushd](pushd.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

