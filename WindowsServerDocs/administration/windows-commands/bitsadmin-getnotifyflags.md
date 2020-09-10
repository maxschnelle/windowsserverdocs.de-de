---
title: bitsadmin getnotifyflags
description: Referenz Artikel für den bizadmin getnotifyflags-Befehl, der die Benachrichtigungs-Flags für den angegebenen Auftrag abruft.
ms.topic: reference
ms.assetid: d4657e6c-8959-4db7-a4af-e73d3f80ecf8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b7cdc2d65316bfcc856bb0fe55a9379d4fc6ba6b
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631903"
---
# <a name="bitsadmin-getnotifyflags"></a>bitsadmin getnotifyflags

Ruft die benachrichtigungflags für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getnotifyflags <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="remarks"></a>Hinweise

Der Auftrag kann eine oder mehrere der folgenden Benachrichtigungs Flags enthalten:

| Flag | Beschreibung |
| ----- | ----- |
| 0x001 | Generiert ein Ereignis, wenn alle Dateien im Auftrag übertragen wurden. |
| 0x002 | Generiert ein Ereignis, wenn ein Fehler auftritt. |
| 0x004 | Deaktivieren Sie Benachrichtigungen. |
| 0x008 | Generieren Sie ein Ereignis, wenn der Auftrag geändert oder der Übertragungs Fortschritt durchgeführt wird. |

## <a name="examples"></a>Beispiele

So rufen Sie die Benachrichtigungs-Flags für den Auftrag mit dem Namen *mydownloadjob*ab:

```
bitsadmin /getnotifyflags myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
