---
title: bitsadmin getpeercachingflags
description: Referenz Artikel für den BITSAdmin getpeercachingflags-Befehl, der Flags abruft, die bestimmen, ob die Dateien des Auftrags zwischengespeichert und für Peers bereitgestellt werden können, und ob Bits Inhalt für den Auftrag von Peers herunterladen kann.
ms.topic: reference
ms.assetid: 3c3c9f28-4c04-4c49-a23a-dee5bbcc8981
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 6ec765183543bf42152d198c10ebc5debfa81edb
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631845"
---
# <a name="bitsadmin-getpeercachingflags"></a>bitsadmin getpeercachingflags

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft Flags ab, die bestimmen, ob die Dateien des Auftrags zwischengespeichert und für Peers bereitgestellt werden können, und ob Bits Inhalt für den Auftrag von Peers herunterladen kann.

## <a name="syntax"></a>Syntax

```
bitsadmin /getpeercachingflags <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie die Flags für den Auftrag mit dem Namen *mydownloadjob*ab:

```
bitsadmin /getpeercachingflags myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
