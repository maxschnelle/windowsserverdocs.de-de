---
title: bitsadmin getnotifyflags
description: Referenz Artikel für den bizadmin getnotifyflags-Befehl, der die Benachrichtigungs-Flags für den angegebenen Auftrag abruft.
ms.topic: reference
ms.assetid: d4657e6c-8959-4db7-a4af-e73d3f80ecf8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3b0281629eb98a7f74defb0971b691fd656d9d97
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033438"
---
# <a name="bitsadmin-getnotifyflags"></a>bitsadmin getnotifyflags

Ruft die benachrichtigungflags für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getnotifyflags <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="remarks"></a>Bemerkungen

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
