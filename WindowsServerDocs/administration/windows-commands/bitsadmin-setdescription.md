---
title: bitsadmin setdescription
description: Referenz Thema für den bitadmin setDescription-Befehl, mit dem die Beschreibung des angegebenen Auftrags festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1e46a5dd-4637-4a2e-b88f-d3f85b177db8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dc76da7cbe348461a79984b8061767711e090da7
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719308"
---
# <a name="bitsadmin-setdescription"></a>bitsadmin setdescription

Legt die Beschreibung für den angegebenen Auftrag fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /setdescription <job> <description>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| description | Der Text, der zur Beschreibung des Auftrags verwendet wird. |

## <a name="examples"></a>Beispiele

So rufen Sie die Beschreibung für den Auftrag mit dem Namen *mydownloadjob*ab

```
bitsadmin /setdescription myDownloadJob music_downloads
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
