---
title: bitsadmin setnotifycmdline
description: Referenz Thema für den bitadmin setnotifycmdline-Befehl, mit dem der Befehlszeilen Befehl festgelegt wird, der ausgeführt wird, wenn der Auftrag das Übertragen von Daten abgeschlossen hat, oder wenn ein Auftrag in einen Zustand wechselt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 415ae6ef-8549-48b2-9693-2368a6e24075
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b21d7151a5b646a4fe07d073220614f5e3c99539
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720131"
---
# <a name="bitsadmin-setnotifycmdline"></a>bitsadmin setnotifycmdline

Legt den Befehlszeilen Befehl fest, der ausgeführt wird, nachdem der Auftrag das Übertragen von Daten abgeschlossen hat oder nachdem ein Auftrag in einen angegebenen Zustand gelangt ist.

> [!NOTE]
> Dieser Befehl wird von Bits 1,2 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /setnotifycmdline <job> <program_name> [program_parameters]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| program_name | Der Name des Befehls, der ausgeführt werden soll, wenn der Auftrag abgeschlossen ist. Sie können diesen Wert als Null festlegen, aber wenn Sie dies tun, müssen *program_parameters* auch auf NULL festgelegt werden. |
| program_parameters | Parameter, die an *program_name*übergeben werden sollen. Sie können diesen Wert auf NULL festlegen. Wenn *program_parameters* nicht auf NULL festgelegt ist, muss der erste Parameter in *program_parameters* dem *program_name*entsprechen. |

## <a name="examples"></a>Beispiele

So führen Sie "Notepad. exe" nach Beendigung des Auftrags mit dem Namen " *mydownloadjob*" aus:

```
bitsadmin /setnotifycmdline myDownloadJob c:\winnt\system32\notepad.exe NULL
```

So zeigen Sie den EULA-Text in Notepad. exe an, wenn der Auftrag mit dem Namen mydownloadjob abgeschlossen ist:

```
bitsadmin /setnotifycmdline myDownloadJob c:\winnt\system32\notepad.exe notepad c:\eula.txt
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
