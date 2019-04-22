---
title: Bitsadmin Cache und Informationen
description: Windows-Befehle Thema **Bitsadmin Cache und Informationen** -gibt einen bestimmten Cacheeintrag.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 15975cbf-dba6-49ca-a725-d15ce1952de5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 61ff57b33e575921f2032d4e13a2d9b74accae60
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813321"
---
# <a name="bitsadmin-cache-and-info"></a>Bitsadmin Cache und Informationen



Gibt einen bestimmten Cacheeintrag.

## <a name="syntax"></a>Syntax

```
bitsadmin /Cache /Info RecordID [/Verbose] 
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|RecordID|Die GUID des Cacheeintrags zugeordnet.|

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel gibt den Cacheeintrag mit dem Datensatz-ID von {6511FB02-E195-40A2-B595-E8E2F8F47702}.
```
C:\>bitsadmin /Cache /Info {6511FB02-E195-40A2-B595-E8E2F8F47702} 
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)