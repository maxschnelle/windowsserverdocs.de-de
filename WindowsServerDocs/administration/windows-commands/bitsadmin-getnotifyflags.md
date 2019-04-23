---
title: bitsadmin getnotifyflags
description: Windows-Befehle Thema **Bitsadmin Getnotifyflags** -Ruft die Notify-Flags für den angegebenen Auftrag.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 690e94805c5e61d96603e4ade102fb3a4bda409e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889281"
---
# <a name="bitsadmin-getnotifyflags"></a>bitsadmin getnotifyflags



Ruft die Benachrichtigungsflags für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetNotifyFlags <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="remarks"></a>Hinweise

Der Auftrag kann eine oder mehrere der folgenden Benachrichtigungsflags, die enthalten.

|---|---| | 0 x 001 | Generieren Sie ein Ereignis, wenn alle Dateien im Auftrag übertragen wurden. | | 0 x 002 | Generieren Sie ein Ereignis, wenn ein Fehler auftritt. | | 0 x 004 | Deaktivieren Sie Benachrichtigungen. | | 0 x 008 | Generieren Sie ein Ereignis, wenn der Auftrag geändert wird, oder übertragungsfortschritts erfolgt. |

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel ruft die Benachrichtigungsflags für den Auftrag mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin /GetNotifyFlags myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)