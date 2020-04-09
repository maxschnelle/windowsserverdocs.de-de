---
title: BI-admin-gethelperthkensid
description: Windows-Befehls Thema für **BITSAdmin gethelpertokensid**, das die SID des Hilfsobjekts eines Bits-Übertragungs Auftrags zurückgibt, sofern ein solches festgelegt ist.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: a2e26ff459b068595529fbd24e6165c130660570
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850643"
---
# <a name="bitsadmin-gethelpertokensid"></a>BI-admin-gethelperthkensid

Gibt die sid für das [Hilfsobjekt](https://docs.microsoft.com/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)eines Bits-Übertragungs Auftrags zurück, sofern ein solches festgelegt ist.

> [!NOTE]
> Dieser Befehl wird von Bits 3,0 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /gethelpertokensid <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
