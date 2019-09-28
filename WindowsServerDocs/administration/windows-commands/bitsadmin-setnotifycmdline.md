---
title: bitsadmin setnotifycmdline
description: Thema für Windows-Befehle für * * * *-bizadmin setnotifycmdlinesets der Befehlszeilen Befehl, der ausgeführt wird, wenn der Auftrag das Übertragen von Daten abgeschlossen hat oder wenn ein Auftrag in einen Zustand wechselt.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 415ae6ef-8549-48b2-9693-2368a6e24075
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7a307fe552e7d8ec5852de953a3a439cb02246ec
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380476"
---
# <a name="bitsadmin-setnotifycmdline"></a>bitsadmin setnotifycmdline

Legt den Befehlszeilen Befehl fest, der ausgeführt wird, wenn die Übertragung von Daten durch den Auftrag abgeschlossen ist oder wenn ein Auftrag in einen Zustand wechselt.

**Bits 1,2 und früher**: Nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetNotifyCmdLine <Job> <ProgramName> [ProgramParameters]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Program Name|Der Name des Befehls, der ausgeführt werden soll, wenn der Auftrag abgeschlossen ist.|
|Programm Parameter|Parameter, die Sie an *Programmname*übergeben möchten.|

## <a name="remarks"></a>Hinweise

Sie können NULL für *Programmname* und *Program Parameters*angeben. Wenn *Program Name* NULL ist, müssen die *Programm Parameter* NULL sein.

> [!IMPORTANT]
> Wenn " *Program Parameters* " nicht NULL ist, muss der erste Parameter in " *Program Parameters* " dem *Programmnamen*entsprechen.

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird der Befehlszeilen Befehl festgelegt, der vom Dienst zum Ausführen von Editor verwendet wird, wenn der Auftrag mit dem Namen *mydownloadjob* abgeschlossen ist.
```
C:\>bitsadmin /SetNotifyCmdLine myDownloadJob c:\winnt\system32\notepad.exe NULL
```
```
C:\>bitsadmin /SetNotifyCmdLine myDownloadJob c:\winnt\system32\notepad.exe "notepad c:\eula.txt"
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)