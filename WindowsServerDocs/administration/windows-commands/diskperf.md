---
title: diskperf
description: Referenz Thema für diskperf, das verwendet werden kann, um Leistungsindikatoren für physische oder logische Datenträger auf Computern, auf denen Windows 2000 ausgeführt wird, Remote zu aktivieren oder zu deaktivieren.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f06916e8-069b-4ec8-a6eb-59f1d9f77111
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c8f505d924ee1de311f2f2736ff65be844c3f2ea
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719447"
---
# <a name="diskperf"></a>diskperf

In Windows 2000 sind Leistungsindikatoren für physische und logische Datenträger standardmäßig nicht aktiviert.

**Diskperf** ist in Windows XP, Windows Server 2003, Windows Server 2008, Windows Vista, Windows Server 2008 R2 und Windows 7 enthalten, sodass es für die Remote Aktivierung oder Deaktivierung von Leistungsindikatoren für physische oder logische Datenträger auf Computern mit Windows 2000 verwendet werden kann.

## <a name="syntax"></a>Syntax

```
diskperf [-Y[D|V] | -N[D|V]] [\\computername]
```

## <a name="options"></a>Optionen

|Option|BESCHREIBUNG|
|------|-----------|
|-?|Zeigt kontextabhängige Hilfe an.|
|-y|Starten Sie alle Datenträger-Leistungsindikatoren, wenn der Computer neu gestartet wird.|
|-Yd|Aktivieren Sie Datenträger-Leistungsindikatoren für physische Laufwerke, wenn der Computer neu gestartet wird.|
|-YV|Aktivieren Sie Datenträger-Leistungsindikatoren für logische Laufwerke oder Speichervolumes, wenn der Computer neu gestartet wird.|
|-N|Deaktivieren Sie alle Datenträger Leistungsindikatoren, wenn der Computer neu gestartet wird.|
|-ND|Deaktivieren Sie die Datenträger Leistungsindikatoren für physische Laufwerke, wenn der Computer neu gestartet wird.|
|-NV|Deaktivieren Sie die Datenträger Leistungsindikatoren für logische Laufwerke oder Speichervolumes, wenn der Computer neu gestartet wird.|
|\\\\*\<Computername>*|Geben Sie den Namen des Computers an, auf dem Sie die Datenträger-Leistungsindikatoren aktivieren bzw. deaktivieren möchten.|