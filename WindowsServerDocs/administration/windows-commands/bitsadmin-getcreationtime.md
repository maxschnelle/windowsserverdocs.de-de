---
title: bitsadmin getcreationtime
description: Referenz Artikel für den bizadmin getkreationtime-Befehl, der die Erstellungszeit für den angegebenen Auftrag abruft.
ms.topic: reference
ms.assetid: be409cb5-ce72-41d9-aafa-edd4e230fd14
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 780f7124248bd38f0c3d7cc9e7cb14b1a9decc03
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632238"
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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
