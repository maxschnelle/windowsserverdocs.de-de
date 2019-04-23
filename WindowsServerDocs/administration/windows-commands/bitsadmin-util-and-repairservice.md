---
title: Bitsadmin Util und repairservice
description: Windows-Befehle Thema **Bitsadmin Util und Repairservice** -Befehl verwendet, um die bekannten Probleme mit verschiedenen Versionen des BITS-Dienst zu beheben.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: bc5101378a389c865f5753146b711be0d15c6785
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852091"
---
# <a name="bitsadmin-util-and-repairservice"></a>Bitsadmin Util und repairservice

Wenn BITS nicht gestartet werden, verwenden Sie diese Option, um bekannte Probleme mit verschiedenen Versionen von BITS zu beheben.

**BITSAdmin 1.5 und früher:** nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /Util /RepairService [/Force]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Force|Optional – löscht und den Dienst erstellt.|

## <a name="remarks"></a>Hinweise

Dieser Schalter wird Fehler im Zusammenhang mit falschen Dienstkonfiguration und Abhängigkeiten von Windows-Dienste (z. B. "LanmanWorkstation") und das Netzwerkverzeichnis aufgelöst. Diese Option generiert eine Ausgabe, der angibt, wenn die Probleme behoben wurden.

> [!NOTE]
> Wenn BITS erstellt den Dienst neu, kann die Beschreibungszeichenfolge für den Dienst in einem lokalisierten System auf Englisch festgelegt werden.

> [!IMPORTANT]
> Mit diesem Befehl wird unter Windows Vista nicht unterstützt.

## <a name="BKMK_examples"></a>Beispiele für

Im folgende Beispiel wird die BITS-Dienst-Konfiguration repariert.
```
C:\>bitsadmin /Util /RepairService
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)