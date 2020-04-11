---
title: bitsadmin setnotifycmdline
description: Windows-Befehls Thema für **bitadmin setnotifycmdline**, das den Befehlszeilen Befehl festlegt, der ausgeführt wird, wenn der Auftrag das Übertragen von Daten abgeschlossen hat, oder wenn ein Auftrag in einen Zustand wechselt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 415ae6ef-8549-48b2-9693-2368a6e24075
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b268b68cbd355a7fe7f993d678a98f6fcb99f0ab
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122899"
---
# <a name="bitsadmin-setnotifycmdline"></a>bitsadmin setnotifycmdline

Legt den Befehlszeilen Befehl fest, der ausgeführt wird, wenn die Übertragung von Daten durch den Auftrag abgeschlossen ist oder wenn ein Auftrag in einen angegebenen Zustand eintritt.

> [!NOTE]
> Dieser Befehl wird von Bits 1,2 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /setnotifycmdline <job> <program_name> [program_parameters]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| program_name | Der Name des Befehls, der ausgeführt werden soll, wenn der Auftrag abgeschlossen ist. Sie können diesen Wert als Null festlegen, aber wenn Sie dies tun, müssen *program_parameters* auch auf NULL festgelegt werden. |
| program_parameters | Parameter, die an *program_name*übergeben werden sollen. Sie können diesen Wert auf NULL festlegen. Wenn *program_parameters* nicht auf NULL festgelegt ist, muss der erste Parameter in *program_parameters* dem *program_name*entsprechen. |

## <a name="examples"></a>Beispiele

Im folgenden Beispiel wird der Befehlszeilen Befehl festgelegt, der vom-Dienst verwendet wird, um Notepad. exe auszuführen, nachdem der Auftrag mit dem Namen *mydownloadjob* abgeschlossen wurde.

```
C:\>bitsadmin /setnotifycmdline myDownloadJob c:\winnt\system32\notepad.exe NULL
```

```
C:\>bitsadmin /setnotifycmdline myDownloadJob c:\winnt\system32\notepad.exe notepad c:\eula.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)