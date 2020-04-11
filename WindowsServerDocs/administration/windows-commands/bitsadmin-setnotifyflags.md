---
title: bitsadmin setnotifyflags
description: Windows-Befehls Thema für **bitadmin setnotifyflags**, mit dem die ereignisbenachrichtigungsflags für den angegebenen Auftrag festgelegt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d5763d95-94a6-45ca-9e03-891c20047e06
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 73c088ce2bae8d2ad99b313417c14449ddd822b5
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122792"
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

Im folgenden Beispiel werden die Benachrichtigungs Flags so festgelegt, dass bei Auftreten eines Fehlers für einen Auftrag mit dem Namen *mydownloadjob*ein Ereignis generiert wird.

```
C:\>bitsadmin /setnotifyflags myDownloadJob 2
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)