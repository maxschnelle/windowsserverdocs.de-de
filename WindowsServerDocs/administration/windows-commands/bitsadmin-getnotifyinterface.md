---
title: bitsadmin getnotifyinterface
description: Windows-Befehle Thema **Bitsadmin Getnotifyinterface** -bestimmt, ob ein anderes Programm eine COM-Rückrufschnittstelle, für den angegebenen Auftrag registriert wurde.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 40bf9dd8-b167-406a-80a6-a5a6f1b8cf7f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8316721a20cc477f9e8e15fc57b5d1c861da3ff4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868041"
---
# <a name="bitsadmin-getnotifyinterface"></a>bitsadmin getnotifyinterface

Bestimmt, ob ein anderes Programm eine COM-Rückrufschnittstelle (die Notify-Schnittstelle) für den angegebenen Auftrag registriert hat.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetNotifyInterface <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="remarks"></a>Hinweise

Zeigt registriert oder.

> [!NOTE]
> Es ist nicht möglich, um die Anwendung zu ermitteln, die die Rückrufschnittstelle registrierte.

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel ruft die Notify-Schnittstelle für den Auftrag mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin /GetNotifyInterface myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)