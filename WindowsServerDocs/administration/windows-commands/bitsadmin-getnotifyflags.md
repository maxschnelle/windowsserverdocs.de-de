---
title: bitsadmin getnotifyflags
description: Windows-Befehls Thema für **bitadmin getnotifyflags** -Ruft die Benachrichtigungs Flags für den angegebenen Auftrag ab.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d4657e6c-8959-4db7-a4af-e73d3f80ecf8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 56ee3a30050b6cc934b35bab24e9508911ea250e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381477"
---
# <a name="bitsadmin-getnotifyflags"></a>bitsadmin getnotifyflags



Ruft die Benachrichtigungs Flags für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetNotifyFlags <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="remarks"></a>Hinweise

Der Auftrag kann eine oder mehrere der folgenden Benachrichtigungs Flags enthalten.

|-----|-----| | 0x001 | Generiert ein Ereignis, wenn alle Dateien im Auftrag übertragen wurden. | 0x002 | Generiert ein Ereignis, wenn ein Fehler auftritt. | | 0x004 | Benachrichtigungen deaktivieren. | | 0x008 | Generiert ein Ereignis, wenn der Auftrag geändert oder der Übertragungs Fortschritt durchgeführt wird. |

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel werden die Benachrichtigungs Flags für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.
```
C:\>bitsadmin /GetNotifyFlags myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)