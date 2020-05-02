---
title: bitsadmin getcreationtime
description: Referenz Thema für den bizadmin getkreationtime-Befehl, der die Erstellungszeit für den angegebenen Auftrag abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: be409cb5-ce72-41d9-aafa-edd4e230fd14
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dc6ca5ad23730e9f57d58e069e0a2daf961930e8
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718105"
---
# <a name="bitsadmin-getcreationtime"></a>bitsadmin getcreationtime

Ruft die Erstellungszeit für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getcreationtime <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie die Erstellungszeit für den Auftrag mit dem Namen *mydownloadjob*ab

```
bitsadmin /getcreationtime myDownloadJob
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
