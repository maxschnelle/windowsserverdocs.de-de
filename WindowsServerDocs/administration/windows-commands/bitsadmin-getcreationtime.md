---
title: bitsadmin getcreationtime
description: Referenz Artikel für den bizadmin getkreationtime-Befehl, der die Erstellungszeit für den angegebenen Auftrag abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: be409cb5-ce72-41d9-aafa-edd4e230fd14
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0efc3d2a0f0f2cf3e72a4ff634733b16ef80055d
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923086"
---
# <a name="bitsadmin-getcreationtime"></a>bitsadmin getcreationtime

Ruft die Erstellungszeit für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getcreationtime <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie die Erstellungszeit für den Auftrag mit dem Namen *mydownloadjob*ab

```
bitsadmin /getcreationtime myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
