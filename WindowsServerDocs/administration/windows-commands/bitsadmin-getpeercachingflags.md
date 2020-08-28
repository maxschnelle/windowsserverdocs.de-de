---
title: bitsadmin getpeercachingflags
description: Referenz Artikel für den BITSAdmin getpeercachingflags-Befehl, der Flags abruft, die bestimmen, ob die Dateien des Auftrags zwischengespeichert und für Peers bereitgestellt werden können, und ob Bits Inhalt für den Auftrag von Peers herunterladen kann.
ms.topic: reference
ms.assetid: 3c3c9f28-4c04-4c49-a23a-dee5bbcc8981
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6c6d7b53dc9c9ff99188b98d19e1418cbf9f1656
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89028718"
---
# <a name="bitsadmin-getpeercachingflags"></a>bitsadmin getpeercachingflags

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft Flags ab, die bestimmen, ob die Dateien des Auftrags zwischengespeichert und für Peers bereitgestellt werden können, und ob Bits Inhalt für den Auftrag von Peers herunterladen kann.

## <a name="syntax"></a>Syntax

```
bitsadmin /getpeercachingflags <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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
