---
title: bitsadmin util and repairservice
description: Referenz Artikel für den Befehl BITSAdmin util und repaunservice, der bekannte Probleme in verschiedenen Versionen des Bits-diensdienstanweises korrigiert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ac7baeb-4340-4186-bfcb-66478195378d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cf62a9410765914187b6a60ff5376e8ff5aabe03
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927340"
---
# <a name="bitsadmin-util-and-repairservice"></a>bitsadmin util and repairservice

Wenn Bits nicht gestartet werden kann, versucht dieser Switch, Fehler im Zusammenhang mit falscher Dienst Konfiguration und Abhängigkeiten von Windows-Diensten (z. b. LanmanWorkstation) und dem Netzwerk Verzeichnis zu beheben. Dieser Switch generiert auch eine Ausgabe, die angibt, ob die Probleme behoben wurden.

> [!NOTE]
> Dieser Befehl wird von Bits 1,5 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /util /repairservice [/force]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| /Force | Dies ist optional. Löscht und erstellt den Dienst erneut.|

> [!NOTE]
> Wenn BITS den Dienst erneut erstellt, kann die Dienst Beschreibungs Zeichenfolge auch in einem lokalisierten System auf Englisch festgelegt werden.

## <a name="examples"></a>Beispiele

So reparieren Sie die BITS-Dienst Konfiguration:

```
bitsadmin /util /repairservice
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "BIFS admin util"](bitsadmin-util.md)

- [Bider admin-Befehl](bitsadmin.md)
