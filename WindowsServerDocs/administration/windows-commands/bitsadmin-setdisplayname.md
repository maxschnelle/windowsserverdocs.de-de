---
title: bitsadmin setdisplayname
description: Windows-Befehle Thema **Bitsadmin Setdisplayname** -legt den Anzeigenamen des angegebenen Auftrags fest.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 13706c53-fb5f-4879-b5ca-82531361d6e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d50cd2785e42b554cee340abc97fe4e4b53adcfc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843671"
---
# <a name="bitsadmin-setdisplayname"></a>bitsadmin setdisplayname



Legt den Anzeigenamen des angegebenen Auftrags fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetDisplayName <Job> <DisplayName>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|DisplayName|Text für den Anzeigenamen des angegebenen Auftrags verwendet.|

## <a name="BKMK_examples"></a>Beispiele für

Im folgenden Beispiel wird der Anzeigename für den Auftrag mit dem Namen *MyDownloadJob* zu *myDownloadJob2*.
```
C:\>bitsadmin /SetDisplayName myDownloadJob "Download Music Job"
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)