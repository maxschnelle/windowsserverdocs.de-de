---
title: bitsadmin setnotifyflags
description: Windows-Befehls Thema für bitadmin setnotifyflags, mit dem die ereignisbenachrichtigungsflags für den angegebenen Auftrag festgelegt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d5763d95-94a6-45ca-9e03-891c20047e06
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fd3001fa4ae7f51cab92556f4f2f498511cca5ae
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849283"
---
# <a name="bitsadmin-setnotifyflags"></a>bitsadmin setnotifyflags

Legt die ereignisbenachrichtigungsflags für den angegebenen Auftrag fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetNotifyFlags <Job> <NotifyFlags>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Notifyflags|Siehe Hinweise|

## <a name="remarks"></a>Hinweise

Der **notifyflags** -Parameter kann eine oder mehrere der folgenden Benachrichtigungs Flags enthalten.

|-----|-----| | 1 | Generiert ein Ereignis, wenn alle Dateien im Auftrag übertragen wurden. | 2 | Generiert ein Ereignis, wenn ein Fehler auftritt. | | 4 | Benachrichtigungen deaktivieren. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel werden die Benachrichtigungs Flags für übertragene Aufträge und Fehler Ereignis Aufträge für einen Auftrag mit dem Namen *mydownloadjob*festgelegt.
```
C:\>bitsadmin /SetNotifyFlags myDownloadJob 3
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)