---
title: bitsadmin setdisplayname
description: Referenz Thema für den Befehl "bitadmin setdisplayname", mit dem der Anzeige Name des angegebenen Auftrags festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 13706c53-fb5f-4879-b5ca-82531361d6e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 382cb2f20f0374c2d2787c4c3d88670b4f7260cd
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719388"
---
# <a name="bitsadmin-setdisplayname"></a>bitsadmin setdisplayname

Legt den anzeigen Amen für den angegebenen Auftrag fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /setdisplayname <job> <display_name>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| display_name | Text, der als angezeigter Name für den jeweiligen Auftrag verwendet wird. |

## <a name="examples"></a>Beispiele

So legen Sie den anzeigen Amen für den Auftrag auf *mydownloadjob*fest

```
bitsadmin /setdisplayname myDownloadJob
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
