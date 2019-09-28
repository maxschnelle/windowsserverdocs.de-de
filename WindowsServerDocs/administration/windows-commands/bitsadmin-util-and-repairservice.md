---
title: bizadmin util und repaunservice
description: Windows-Befehls Thema für **BITSAdmin util und repaunservice** -Command, das verwendet wird, um bekannte Probleme mit verschiedenen Versionen des Bits-dienstanweises zu beheben.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2ac7baeb-4340-4186-bfcb-66478195378d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0ab06ac9c784cfa438eb285c28f0e661cf4b8302
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380281"
---
# <a name="bitsadmin-util-and-repairservice"></a>bizadmin util und repaunservice

Wenn Bits nicht gestartet werden kann, verwenden Sie diesen Schalter, um bekannte Probleme mit verschiedenen Versionen von Bits zu beheben.

**Biout admin 1,5 und früher:**  Nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /Util /RepairService [/Force]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Force|Optional – löscht den Dienst und erstellt ihn neu.|

## <a name="remarks"></a>Hinweise

Dieser Switch löst Fehler im Zusammenhang mit falscher Dienst Konfiguration und Abhängigkeiten von Windows-Diensten (z. b. LanmanWorkstation) und dem Netzwerk Verzeichnis auf. Dieser Schalter generiert eine Ausgabe, die angibt, ob die Probleme behoben wurden.

> [!NOTE]
> Wenn BITS den Dienst neu erstellt, kann die Zeichenfolge für die Dienst Beschreibung in einem lokalisierten System auf Englisch festgelegt werden.

> [!IMPORTANT]
> Dieser Befehl wird in Windows Vista nicht unterstützt.

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird die BITS-Dienst Konfiguration repariert.
```
C:\>bitsadmin /Util /RepairService
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)