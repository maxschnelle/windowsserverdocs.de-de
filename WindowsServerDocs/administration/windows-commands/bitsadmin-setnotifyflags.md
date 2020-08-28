---
title: bitsadmin setnotifyflags
description: Referenz Artikel für den Befehl "bitadmin setnotifyflags", mit dem die ereignisbenachrichtigungsflags für den angegebenen Auftrag festgelegt werden.
ms.topic: reference
ms.assetid: d5763d95-94a6-45ca-9e03-891c20047e06
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a3b00d057659b2664098093c0a7e3b13b28cd806
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89026218"
---
# <a name="bitsadmin-setnotifyflags"></a>bitsadmin setnotifyflags

Legt die ereignisbenachrichtigungsflags für den angegebenen Auftrag fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /setnotifyflags <job> <notifyflags>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| notifyflags | Kann eine oder mehrere der folgenden Benachrichtigungs Flags enthalten, einschließlich:<ul><li>**1.** generiert ein Ereignis, wenn alle Dateien im Auftrag übertragen wurden.</li><li>**2.** generiert ein Ereignis, wenn ein Fehler auftritt.</li><li>**3.** generiert ein Ereignis, wenn alle Dateien die Übertragung abgeschlossen haben oder wenn ein Fehler auftritt.</li><li>**4.** deaktiviert Benachrichtigungen.</li></ul> |

## <a name="examples"></a>Beispiele

So legen Sie die Benachrichtigungs Flags so fest, dass bei Auftreten eines Fehlers ein Ereignis generiert wird für einen Auftrag mit dem Namen *mydownloadjob*:

```
bitsadmin /setnotifyflags myDownloadJob 2
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
