---
title: bitsadmin listfiles
description: Windows-Befehle Thema **Bitsadmin Listfiles** -Listet die Dateien in den angegebenen Auftrag.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ad0d1eaa-3bd8-45e5-8f72-4da7366f0d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4f0f86a7e176c601c51dbdf403baf51f70e53dc4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852971"
---
# <a name="bitsadmin-listfiles"></a>bitsadmin listfiles



Listet die Dateien in den angegebenen Auftrag.

## <a name="syntax"></a>Syntax

```
bitsadmin /ListFiles <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel ruft die Liste der Dateien für den Auftrag mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin /GetNotifyFlags myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)