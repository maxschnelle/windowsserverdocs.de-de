---
title: bitsadmin setnotifycmdline
description: Referenz Artikel für den Befehl "bitadmin setnotifycmdline", mit dem der Befehlszeilen Befehl festgelegt wird, der ausgeführt wird, wenn die Übertragung von Daten durch den Auftrag abgeschlossen ist, oder wenn ein Auftrag in einen Zustand wechselt.
ms.topic: reference
ms.assetid: 415ae6ef-8549-48b2-9693-2368a6e24075
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7f486efcbaef5f68d6f8be7cab1caba204c77c7a
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89026228"
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

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| program_name | Der Name des Befehls, der ausgeführt werden soll, wenn der Auftrag abgeschlossen ist. Sie können diesen Wert als Null festlegen, aber wenn Sie dies tun, müssen *program_parameters* auch auf NULL festgelegt werden. |
| program_parameters | Parameter, die an *program_name*übergeben werden sollen. Sie können diesen Wert auf NULL festlegen. Wenn *program_parameters* nicht auf NULL festgelegt ist, muss der erste Parameter in *program_parameters* dem *program_name*entsprechen. |

## <a name="examples"></a>Beispiele

So führen Sie Notepad.exe nach Beendigung des Auftrags mit dem Namen *mydownloadjob*aus:

```
bitsadmin /setnotifycmdline myDownloadJob c:\winnt\system32\notepad.exe NULL
```

So zeigen Sie den EULA-Text beim Abschluss des Auftrags mydownloadjob in Notepad.exe an:

```
bitsadmin /setnotifycmdline myDownloadJob c:\winnt\system32\notepad.exe notepad c:\eula.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
