---
title: bitsadmin zurücksetzen
description: 'Windows-Befehls Thema für die **bitadmin-zurück** Setzung: bricht alle Aufträge in der Übertragungs Warteschlange ab, die der aktuelle Benutzer besitzt.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e4f9d1d-072c-493f-8d7a-f6d713c3ef29
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: adc6b07a7b5d1414c733fe6a3ac05eba7cb3029e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380809"
---
# <a name="bitsadmin-reset"></a>bitsadmin zurücksetzen

Bricht alle Aufträge in der Übertragungs Warteschlange ab, die der aktuelle Benutzer besitzt.

**Bikadmin 1,5 und früher**: Wenn Sie über Administratorrechte verfügen, **setzen**Sie  abbrechen alle Aufträge in der Warteschlange ab. Die/ALLUSERS-Option wird nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /Reset [/AllUsers]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|ALLUSERS|Optional – bricht alle Aufträge in der Warteschlange ab.|

## <a name="remarks"></a>Hinweise

Sie müssen über Administratorrechte verfügen, um den **ALLUSERS** -Parameter zu verwenden.

> [!NOTE]
> Die vom lokalen System erstellten Aufträge können von Administratoren nicht zurückgesetzt werden. Verwenden Sie den Taskplaner, um diesen Befehl mithilfe der Anmelde Informationen für das lokale System als Task zu planen.

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel werden alle Aufträge in der Übertragungs Warteschlange des aktuellen Benutzers abgebrochen.
```
C:\>bitsadmin /Reset
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)