---
title: bitsadmin setnotifyflags
description: Windows-Befehle Thema **Bitsadmin Setnotifyflags** -legt das-Ereignis Benachrichtigungsflags für den angegebenen Auftrag.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d5763d95-94a6-45ca-9e03-891c20047e06
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bc817e03e0f1916ea392830d14985a7a1377d69a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868791"
---
# <a name="bitsadmin-setnotifyflags"></a>bitsadmin setnotifyflags

Legt das-Ereignis Benachrichtigungsflags für den angegebenen Auftrag.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetNotifyFlags <Job> <NotifyFlags>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|NotifyFlags|Finden Sie unter "Hinweise"|

## <a name="remarks"></a>Hinweise

Die **NotifyFlags** Parameter kann eine oder mehrere der folgenden Benachrichtigungsflags, die enthalten.

|---|---| | 1 | Generieren Sie ein Ereignis, wenn alle Dateien im Auftrag übertragen wurden. | | 2 | Generieren Sie ein Ereignis, wenn ein Fehler auftritt. | | 4 | Deaktivieren Sie Benachrichtigungen. |

## <a name="BKMK_examples"></a>Beispiele für

Im folgenden Beispiel wird die Benachrichtigungsflags für und Ereignisse für Fehler im Auftrag für den Auftrag mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin /SetNotifyFlags myDownloadJob 3
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)