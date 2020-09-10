---
title: bitsadmin peercaching and getconfigurationflags
description: Referenz Artikel zum Befehl BITSAdmin-Peer Caching und getconfigurationflags, der die Konfigurationsflags abruft, die bestimmen, ob der Computer Inhalt für Peers bereitstellt und Inhalt von Peers herunterladen kann.
ms.topic: reference
ms.assetid: 124ddc15-3444-4bd5-96e5-c6bfabe4f9c2
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3fe1adfb44ab845ecdb73222131191782f83c075
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631372"
---
# <a name="bitsadmin-peercaching-and-getconfigurationflags"></a>bitsadmin peercaching and getconfigurationflags

Ruft die Konfigurationsflags ab, die bestimmen, ob der Computer Inhalt für Peers bereitstellt und Inhalt von Peers herunterladen kann.

## <a name="syntax"></a>Syntax

```
bitsadmin /peercaching /getconfigurationflags <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So erhalten Sie die Konfigurationsflags für den Auftrag mit dem Namen *mydownloadjob*:

```
bitsadmin /peercaching /getconfigurationflags myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)

- [bipadmin-Befehl "Peer Caching"](bitsadmin-peercaching.md)
