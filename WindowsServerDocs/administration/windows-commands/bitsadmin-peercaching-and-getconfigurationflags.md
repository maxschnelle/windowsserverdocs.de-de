---
title: bitsadmin peercaching and getconfigurationflags
description: Referenz Artikel zum Befehl BITSAdmin-Peer Caching und getconfigurationflags, der die Konfigurationsflags abruft, die bestimmen, ob der Computer Inhalt für Peers bereitstellt und Inhalt von Peers herunterladen kann.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 124ddc15-3444-4bd5-96e5-c6bfabe4f9c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1c6834e57ebccca94c6fdc7c6cff503e2d58378a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922997"
---
# <a name="bitsadmin-peercaching-and-getconfigurationflags"></a>bitsadmin peercaching and getconfigurationflags

Ruft die Konfigurationsflags ab, die bestimmen, ob der Computer Inhalt für Peers bereitstellt und Inhalt von Peers herunterladen kann.

## <a name="syntax"></a>Syntax

```
bitsadmin /peercaching /getconfigurationflags <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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
