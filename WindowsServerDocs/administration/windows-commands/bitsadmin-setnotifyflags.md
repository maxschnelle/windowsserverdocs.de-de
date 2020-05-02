---
title: bitsadmin setnotifyflags
description: Referenz Thema für den bitadmin setnotifyflags-Befehl, mit dem die ereignisbenachrichtigungsflags für den angegebenen Auftrag festgelegt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d5763d95-94a6-45ca-9e03-891c20047e06
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 00b704bf0943790ef01bbfbdbcbbde4dfd1845c6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717278"
---
# <a name="bitsadmin-setnotifyflags"></a>bitsadmin setnotifyflags

Legt die ereignisbenachrichtigungsflags für den angegebenen Auftrag fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /setnotifyflags <job> <notifyflags>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| notifyflags | Kann eine oder mehrere der folgenden Benachrichtigungs Flags enthalten, einschließlich:<ul><li>**1.** generiert ein Ereignis, wenn alle Dateien im Auftrag übertragen wurden.</li><li>**2.** generiert ein Ereignis, wenn ein Fehler auftritt.</li><li>**3.** generiert ein Ereignis, wenn alle Dateien die Übertragung abgeschlossen haben oder wenn ein Fehler auftritt.</li><li>**4.** deaktiviert Benachrichtigungen.</li></ul> |

## <a name="examples"></a>Beispiele

So legen Sie die Benachrichtigungs Flags so fest, dass bei Auftreten eines Fehlers ein Ereignis generiert wird für einen Auftrag mit dem Namen *mydownloadjob*:

```
bitsadmin /setnotifyflags myDownloadJob 2
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
