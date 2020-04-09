---
title: biout admin Cache und DeleteUrl
description: Windows-Befehls Thema für den **BI-admin-Cache und DeleteUrl**, die alle Cache Einträge für die angegebene URL löscht.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e108b76b-fae9-4c16-bf4c-d74c9f025953
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 70099e795d0f05d0fcf75fbf6b82f5466d1c0c55
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850933"
---
# <a name="bitsadmin-cache-and-deleteurl"></a>biout admin Cache und DeleteUrl

Löscht alle Cache Einträge für die angegebene URL.

## <a name="syntax"></a>Syntax

```
bitsadmin /deleteURL url
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| url | Der Uniform Resource Locator, der eine Remote Datei identifiziert. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel werden alle Cache Einträge für `https://www.contoso.com/en/us/default.aspx` gelöscht.

```
C:\>bitsadmin /deleteURL https://www.contoso.com/en/us/default.aspx 
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)