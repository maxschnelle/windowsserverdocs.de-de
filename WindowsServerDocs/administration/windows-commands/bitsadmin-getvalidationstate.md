---
title: bitsadmin getvalidationstate
description: Referenz Thema für den BITSAdmin getvalidationstate-Befehl, der den Status der Inhalts Überprüfung der angegebenen Datei innerhalb des Auftrags meldet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6ada3f1f-9967-4262-9d22-ed641e23f516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ca753b20a1b7834d2e05d4ff8729a08332256f8c
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717460"
---
# <a name="bitsadmin-getvalidationstate"></a>bitsadmin getvalidationstate

Meldet den Status der Inhalts Überprüfung der angegebenen Datei innerhalb des Auftrags.

## <a name="syntax"></a>Syntax

```
bitsadmin /getvalidationstate <job> <file_index>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| file_index | Beginnt bei 0. |

## <a name="examples"></a>Beispiele

So rufen Sie den Status der Inhalts Überprüfung der Datei 2 innerhalb des Auftrags mit dem Namen *mydownloadjob*ab

```
bitsadmin /getvalidationstate myDownloadJob 1
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
