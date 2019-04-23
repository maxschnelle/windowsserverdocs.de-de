---
title: pushd
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 396bc545-0f41-473e-b0ac-76fbbb74d390
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 548f39921c1f6aa3837e6443e396922396eb84f7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887461"
---
# <a name="pushd"></a>pushd



Speichert das aktuelle Verzeichnis für die Verwendung durch die **Popd** -Befehl, und klicken Sie dann Änderungen an das angegebene Verzeichnis.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
pushd [<Path>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Pfad >|Gibt das Verzeichnis aus, um das aktuelle Verzeichnis zu machen. Dieser Befehl unterstützt relative Pfade.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Jedes Mal, wenn Sie verwenden die **Pushd** Befehl wird ein einzelnes Verzeichnis für Ihre Verwendung gespeichert. Sie können jedoch mehrere Verzeichnisse speichern, mithilfe der **Pushd** Befehl mehrmals.

    Die Verzeichnisse werden nacheinander in einem virtuellen Stapel gespeichert werden. Bei Verwendung der **Pushd** Befehl, nachdem das Verzeichnis, in denen, die Sie den Befehl verwenden, an das Ende des Stapels platziert wird. Wenn Sie den Befehl erneut ausführen, wird das zweite Verzeichnis zusätzlich zu dem ersten platziert. Der Vorgang wird wiederholt, jedes Mal, wenn Sie verwenden die **Pushd** Befehl.

    Können Sie die **Popd** Befehl aus, um das aktuelle Verzeichnis in das Verzeichnis, das die zuletzt gespeicherten Ändern der **Pushd** Befehl. Bei Verwendung der **Popd** -Befehls das Verzeichnis des Stapels wird aus dem Stapel entfernt, und das aktuelle Verzeichnis auf das Verzeichnis geändert wird. Bei Verwendung der **Popd** erneut den Befehl Weitere Verzeichnis auf dem Stapel entfernt wird.
-   Wenn der befehlserweiterungen aktiviert sind, die **Pushd** Befehl akzeptiert ein Netzwerkpfad oder einen lokalen Laufwerkbuchstaben und Pfad.
-   Wenn Sie einen Netzwerkpfad, Angeben der **Pushd** Befehl vorübergehend weist den höchsten nicht verwendeten Laufwerkbuchstaben (beginnend mit Z:) mit der angegebenen Netzwerkressource. Der Befehl ändert das aktuelle Laufwerk und Verzeichnis anschließend in das angegebene Verzeichnis auf dem neu zugewiesenen Laufwerk an. Bei Verwendung der **Popd** Befehl befehlserweiterungen aktiviert, die **Popd** Befehl entfernt die Laufwerkbuchstaben Assignation erstellt **Pushd**.

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel zeigt Informationen zur Verwendung der **Pushd** Befehl und die **Popd** in einer Batchdatei so ändern Sie das aktuelle Verzeichnis als dem in dem das Batch-Programm ausgeführt wurde, und ändern sie wieder den Befehl:
```
@echo off
rem This batch file deletes all .txt files in a specified directory
pushd %1
del *.txt
popd
cls
echo All text files deleted in the %1 directory
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)

[Popd](popd.md)