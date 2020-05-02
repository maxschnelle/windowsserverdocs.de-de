---
title: bitsadmin getnotifyflags
description: Referenz Thema für den bizadmin getnotifyflags-Befehl, der die Benachrichtigungs-Flags für den angegebenen Auftrag abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d4657e6c-8959-4db7-a4af-e73d3f80ecf8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 36e4c3584b2e3be9c9985756aeaec08b40e74b0c
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717768"
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

## <a name="remarks"></a>Bemerkungen

Der Auftrag kann eine oder mehrere der folgenden Benachrichtigungs Flags enthalten:

| Flag | BESCHREIBUNG |
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
