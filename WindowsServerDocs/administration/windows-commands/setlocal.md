---
title: setlocal
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e4e4b6d3-3f1a-4851-a782-25ee2470e16e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 70e58e3c3a7c3de594c620f7530816b57727d4c3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868861"
---
# <a name="setlocal"></a>setlocal



Startet die Lokalisierung von Umgebungsvariablen in einer Batchdatei. Lokalisierung wird fortgesetzt, bis ein entsprechender **Endlocal** Befehl gefunden, oder das Ende der Batch-Datei erreicht ist.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
setlocal [enableextensions | disableextensions] [enabledelayedexpansion | disabledelayedexpansion]
```

## <a name="arguments"></a>Argumente

|Argument|Beschreibung|
|--------|-----------|
|enableextensions|Ermöglicht die befehlserweiterungen, bis der passende **Endlocal** Befehl festgestellt wird, unabhängig von der Einstellung aus, bevor Sie die **Setlocal** -Befehl ausgeführt wurde.|
|disableextensions|Die befehlserweiterungen deaktiviert, bis der passende **Endlocal** Befehl festgestellt wird, unabhängig von der Einstellung aus, bevor Sie die **Setlocal** -Befehl ausgeführt wurde.|
|enabledelayedexpansion|Ermöglicht die verzögerte umgebungsvariablenerweiterung bis der passende **Endlocal** Befehl festgestellt wird, unabhängig von der Einstellung vor dem **Setlocal** -Befehl ausgeführt wurde.|
|DISABLEDELAYEDEXPANSION|Deaktiviert die verzögerte umgebungsvariablenerweiterung bis der passende **Endlocal** Befehl festgestellt wird, unabhängig von der Einstellung vor dem **Setlocal** -Befehl ausgeführt wurde.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Mithilfe von **Setlocal**

    Bei Verwendung von **Setlocal** außerhalb einer Skript oder Batch-Datei, die sie hat keine Auswirkungen.
-   Ändern von Umgebungsvariablen

    Verwendung **Setlocal** Umgebungsvariablen zu ändern, wenn Sie eine Batchdatei ausführen. Umgebungsänderungen nach dem Ausführen **Setlocal** befinden sich lokal auf die Batch-Datei. Das Cmd.exe-Programm vorherige Einstellungen wiederhergestellt, wenn es trifft eine **Endlocal** Befehl oder das Ende der Batchdatei erreicht.
-   Schachtelung-Befehle

    Sie haben mehr als eine **Setlocal** oder **Endlocal** Befehl in einem Batchprogramm (d. h. geschachtelte Befehle).
-   Befehlserweiterungen in Batchdateien testen

    Die **Setlocal** Befehl wird die ERRORLEVEL-Variable. Wenn Sie erfolgreich {**Enableextensions** | **Disableextensions**} oder {**Enabledelayedexpansion**  |   **DISABLEDELAYEDEXPANSION**}, die ERRORLEVEL-Variable nastaven NA hodnotu **0** (null). Andernfalls wird es zum festgelegt **1**. Sie können diese Informationen in Batchskripts verwenden, um festzustellen, ob die Erweiterungen verfügbar sind, wie im folgenden Beispiel gezeigt:  
    ```
    setlocal enableextensions
    verify other 2>nul
    if errorlevel 1 echo Unable to enable extensions
    ```  
    Da **Cmd** die ERRORLEVEL-Variable wird nicht festgelegt werden, wenn befehlserweiterungen deaktiviert sind, die **überprüfen** Befehl initialisiert die ERRORLEVEL-Variable einen Wert ungleich NULL aus, bei der Verwendung mit einem ungültigen Argument. Auch bei Verwendung der **Setlocal** Befehl mit Argumenten {**Enableextensions** | **Disableextensions**} oder {**Enabledelayedexpansion**   |  **Disabledelayedexpansion**} und darin wird die ERRORLEVEL-Variable nicht festgelegt, um **1**, befehlserweiterungen sind nicht verfügbar.

## <a name="BKMK_examples"></a>Beispiele für

Sie können Umgebungsvariablen in einer Batchdatei lokalisieren, wie im folgenden Beispielskript gezeigt:
```
rem *******Begin Comment**************
rem This program starts the superapp batch program on the network,
rem directs the output to a file, and displays the file
rem in Notepad.
rem *******End Comment**************
@echo off
setlocal
path=g:\programs\superapp;%path%
call superapp>c:\superapp.out
endlocal
start notepad c:\superapp.out
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)