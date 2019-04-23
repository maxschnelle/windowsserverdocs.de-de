---
title: popd
description: Erfahren Sie, wie Sie das Verzeichnis in das Verzeichnis, das die zuletzt gespeicherte durch pushd ändern.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8a4c52d5-9fd1-4eac-9c0c-5767b25728ed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 6da6dc9d1fc2d8965f8a081831cb1150375209a4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827461"
---
# <a name="popd"></a>popd

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ändert das aktuelle Verzeichnis in das Verzeichnis, das durch die zuletzt gespeichert wurde die **Pushd** Befehl.
Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax
```
popd
```

### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Jedes Mal, wenn Sie verwenden die **Pushd** Befehl wird ein einzelnes Verzeichnis für Ihre Verwendung gespeichert. Sie können jedoch mehrere Verzeichnisse speichern, mithilfe der **Pushd** Befehl mehrmals.
    Die Verzeichnisse werden nacheinander in einem virtuellen Stapel gespeichert werden. Bei Verwendung der **Pushd** Befehl, nachdem das Verzeichnis, in denen, die Sie den Befehl verwenden, an das Ende des Stapels platziert wird. Wenn Sie den Befehl erneut ausführen, wird das zweite Verzeichnis zusätzlich zu dem ersten platziert. Der Vorgang wird wiederholt, jedes Mal, wenn Sie verwenden die **Pushd** Befehl.
    Können Sie die **Popd** Befehl aus, um das aktuelle Verzeichnis in das Verzeichnis, das die zuletzt gespeicherten Ändern der **Pushd** Befehl. Bei Verwendung der **Popd** -Befehls das Verzeichnis des Stapels wird aus dem Stapel entfernt, und das aktuelle Verzeichnis auf das Verzeichnis geändert wird. Bei Verwendung der **Popd** erneut den Befehl Weitere Verzeichnis auf dem Stapel entfernt wird.
-   Wenn der befehlserweiterungen aktiviert sind, die **Popd** Befehl entfernt alle Laufwerkbuchstaben Assignations erstellt **Pushd**.

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

## <a name="additional-references"></a>Zusätzliche Referenzen
-   [pushd](pushd.md)
-   [Befehlszeilensyntax](command-line-syntax-key.md)

