---
title: bitsadmin setnotifycmdline
description: Windows-Befehls Thema für bitadmin setnotifycmdline, mit dem der Befehlszeilen Befehl festgelegt wird, der ausgeführt wird, wenn der Auftrag das Übertragen von Daten abgeschlossen hat oder wenn ein Auftrag in einen Zustand wechselt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 415ae6ef-8549-48b2-9693-2368a6e24075
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 761a7003e44e8dc15cb2dd2f1ce5a1a23be53286
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849333"
---
# <a name="bitsadmin-setnotifycmdline"></a>bitsadmin setnotifycmdline

Legt den Befehlszeilen Befehl fest, der ausgeführt wird, wenn die Übertragung von Daten durch den Auftrag abgeschlossen ist oder wenn ein Auftrag in einen Zustand wechselt.

**Bits 1,2 und früher**: nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetNotifyCmdLine <Job> <ProgramName> [ProgramParameters]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Program Name|Der Name des Befehls, der ausgeführt werden soll, wenn der Auftrag abgeschlossen ist.|
|Programm Parameter|Parameter, die Sie an *Programmname*übergeben möchten.|

## <a name="remarks"></a>Hinweise

Sie können NULL für *Programmname* und *Program Parameters*angeben. Wenn *Program Name* NULL ist, müssen die *Programm Parameter* NULL sein.

> [!IMPORTANT]
> Wenn " *Program Parameters* " nicht NULL ist, muss der erste Parameter in " *Program Parameters* " dem *Programmnamen*entsprechen.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird der Befehlszeilen Befehl festgelegt, der vom Dienst zum Ausführen von Editor verwendet wird, wenn der Auftrag mit dem Namen *mydownloadjob* abgeschlossen ist.
```
C:\>bitsadmin /SetNotifyCmdLine myDownloadJob c:\winnt\system32\notepad.exe NULL
```
```
C:\>bitsadmin /SetNotifyCmdLine myDownloadJob c:\winnt\system32\notepad.exe notepad c:\eula.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)