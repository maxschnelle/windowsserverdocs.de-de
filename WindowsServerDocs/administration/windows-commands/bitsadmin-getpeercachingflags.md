---
title: bitsadmin getpeercachingflags
description: Referenz Thema für den BITSAdmin getpeercachingflags-Befehl, der Flags abruft, die bestimmen, ob die Dateien des Auftrags zwischengespeichert und für Peers bereitgestellt werden können, und ob Bits Inhalt für den Auftrag von Peers herunterladen kann.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3c3c9f28-4c04-4c49-a23a-dee5bbcc8981
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f30eead56958af3cd0fb0d91f6ee2bf9f79fdc4e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717691"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
