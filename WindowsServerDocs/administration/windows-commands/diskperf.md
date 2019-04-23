---
title: diskperf
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f06916e8-069b-4ec8-a6eb-59f1d9f77111
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a99f18b56c9295e902a3c89e2e89b36c9c1b6c89
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852581"
---
# <a name="diskperf"></a>diskperf



In Windows 2000 werden die Leistungsindikatoren für physische und logische Datenträger nicht standardmäßig aktiviert.

**"Diskperf"** ist in Windows XP, Windows Server 2003, Windows Server 2008, Windows Vista, Windows Server 2008 R2 und Windows 7 enthalten, sodass sie verwendet werden kann, um Remote aktivieren oder deaktivieren die Leistungsindikatoren für das physische oder logische Datenträger auf Computern mit Windows 2000.

## <a name="syntax"></a>Syntax

```
diskperf [-Y[D|V] | -N[D|V]] [\\computername]
```

## <a name="options"></a>Optionen

|Option|Beschreibung|
|------|-----------|
|-?|Zeigt, die kontextbezogene Hilfe an.|
|-Y|Starten Sie alle Leistungsindikatoren aus, wenn der Computer neu gestartet wird.|
|-YD|Aktivieren Sie Leistungsindikatoren für physische Laufwerke aus, wenn der Computer neu gestartet wird.|
|-YV|Aktivieren Sie die Leistungsindikatoren für logische Laufwerke oder Volumes, beim Neustart des Computers.|
|-N|Deaktivieren Sie alle Leistungsindikatoren aus, wenn der Computer neu gestartet wird.|
|-ND|Deaktivieren Sie Leistungsindikatoren für physische Laufwerke aus, wenn der Computer neu gestartet wird.|
|-NV|Deaktivieren Sie die Leistungsindikatoren für logische Laufwerke oder Volumes, beim Neustart des Computers.|
|\\\\*\<computername>*|Geben Sie den Namen des Computers aktivieren oder deaktivieren die Datenträger-Leistungsindikatoren werden sollen.|