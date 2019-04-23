---
title: bitsadmin setnotifycmdline
description: Windows-Befehle Thema ***-Bitsadmin SetnotifycmdlineSets die Befehlszeile, die ausgeführt werden, wenn der Auftrag abgeschlossen ist, Übertragen von Daten oder ein Auftrag in einen Zustand wechselt.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: f1cea4e99cbaaf3881c6f436bdb932090ad6b006
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859071"
---
# <a name="bitsadmin-setnotifycmdline"></a>bitsadmin setnotifycmdline

Legt fest, die Befehlszeile, die ausgeführt werden, wenn der Auftrag abgeschlossen ist, Übertragen von Daten oder ein Auftrag in einen Zustand wechselt.

**BITS-Version 1.2 und früher**: Nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetNotifyCmdLine <Job> <ProgramName> [ProgramParameters]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|ProgramName|Der Name des Befehls, der ausgeführt werden, wenn der Auftrag abgeschlossen ist.|
|ProgramParameters|Parameter, die Sie übergeben möchten *ProgramName*.|

## <a name="remarks"></a>Hinweise

Sie können angeben, dass NULL für *ProgramName* und *ProgramParameters*. Wenn *ProgramName* NULL ist, *ProgramParameters* muss NULL sein.

> [!IMPORTANT]
> Wenn *ProgramParameters* ist nicht NULL, und klicken Sie dann auf den ersten Parameter im *ProgramParameters* übereinstimmen *ProgramName*.

## <a name="BKMK_examples"></a>Beispiele für

Im folgenden Beispiel wird die Befehlszeile zum Ausführen des Editors, wenn der Auftrag mit dem Namen vom Dienst verwendete *MyDownloadJob* abgeschlossen ist.
```
C:\>bitsadmin /SetNotifyCmdLine myDownloadJob c:\winnt\system32\notepad.exe NULL
```
```
C:\>bitsadmin /SetNotifyCmdLine myDownloadJob c:\winnt\system32\notepad.exe "notepad c:\eula.txt"
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)