---
title: bitsadmin setnotifyflags
description: Referenz Artikel für den Befehl "bitadmin setnotifyflags", mit dem die ereignisbenachrichtigungsflags für den angegebenen Auftrag festgelegt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d5763d95-94a6-45ca-9e03-891c20047e06
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b4054788bb8c14e4bd9be38296f5c0f933de9462
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927615"
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
