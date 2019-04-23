---
title: Wiederherstellen
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75ad40e4-502a-401e-b11e-8b31e00424b5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5bc77b17317f602d642c7a9e025b67be10ad7256
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875111"
---
# <a name="revert"></a>Wiederherstellen



wird ein Volume an einer angegebenen Schattenkopie zurückgesetzt. Dies ist nur für Schattenkopien im Kontext CLIENTACCESSIBLE unterstützt. Diese Schattenkopien bleiben erhalten und können nur vom Systemanbieter vorgenommen werden. Wenn Sie ohne Angabe von Parametern **wiederherstellen** zeigt die Hilfe an der Eingabeaufforderung.

## <a name="syntax"></a>Syntax

```
revert <ShadowCopyID>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<ShadowCopyID>|Gibt an, der Schattenkopie-ID um das Volume wiederherzustellen.|

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)