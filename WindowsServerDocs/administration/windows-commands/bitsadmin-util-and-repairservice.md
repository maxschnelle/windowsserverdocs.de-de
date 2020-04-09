---
title: bizadmin util und repaunservice
description: Windows-Befehls Thema für BITSAdmin util und repaunservice, das bekannte Probleme in verschiedenen Versionen des Bits-diensdienstanweises korrigiert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ac7baeb-4340-4186-bfcb-66478195378d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: aaaa6edab22031dc53d266984bb669634e3bb362
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848893"
---
# <a name="bitsadmin-util-and-repairservice"></a>bizadmin util und repaunservice

Wenn Bits nicht gestartet werden kann, verwenden Sie diesen Schalter, um bekannte Probleme in verschiedenen Versionen von Bits zu beheben.

**Biout admin 1,5 und früher:**  nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /Util /RepairService [/Force]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Force|Optional – löscht den Dienst und erstellt ihn neu.|

## <a name="remarks"></a>Hinweise

Dieser Switch löst Fehler im Zusammenhang mit falscher Dienst Konfiguration und Abhängigkeiten von Windows-Diensten (z. b. LanmanWorkstation) und dem Netzwerk Verzeichnis auf. Dieser Schalter generiert eine Ausgabe, die angibt, ob die Probleme behoben wurden.

> [!NOTE]
> Wenn BITS den Dienst neu erstellt, kann die Zeichenfolge für die Dienst Beschreibung in einem lokalisierten System auf Englisch festgelegt werden.

> [!IMPORTANT]
> Dieser Befehl wird in Windows Vista nicht unterstützt.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird die BITS-Dienst Konfiguration repariert.
```
C:\>bitsadmin /Util /RepairService
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)