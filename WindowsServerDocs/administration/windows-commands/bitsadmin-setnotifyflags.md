---
title: bitsadmin setnotifyflags
description: 'Windows-Befehls Thema für **bitadmin setnotifyflags** : legt die ereignisbenachrichtigungsflags für den angegebenen Auftrag fest.'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: d9cfabf05610cbbe8fa65fd16b0d33e161dcef9b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380451"
---
# <a name="bitsadmin-setnotifyflags"></a>bitsadmin setnotifyflags

Legt die ereignisbenachrichtigungsflags für den angegebenen Auftrag fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetNotifyFlags <Job> <NotifyFlags>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Notifyflags|Siehe Hinweise|

## <a name="remarks"></a>Hinweise

Der **notifyflags** -Parameter kann eine oder mehrere der folgenden Benachrichtigungs Flags enthalten.

|-----|-----| | 1 | Generiert ein Ereignis, wenn alle Dateien im Auftrag übertragen wurden. | 2 | Generiert ein Ereignis, wenn ein Fehler auftritt. | | 4 | Benachrichtigungen deaktivieren. |

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel werden die Benachrichtigungs Flags für übertragene Aufträge und Fehler Ereignis Aufträge für einen Auftrag mit dem Namen *mydownloadjob*festgelegt.
```
C:\>bitsadmin /SetNotifyFlags myDownloadJob 3
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)