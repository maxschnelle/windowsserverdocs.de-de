---
title: bitsadmin util and repairservice
description: Referenz Thema für den BITSAdmin-Befehl util und repaunservice, mit dem bekannte Probleme in verschiedenen Versionen des Bits-Dienes behoben werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ac7baeb-4340-4186-bfcb-66478195378d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0104a3f2ace972821151bf5083f9b0795e427ff1
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707654"
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

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| /Force | Optional. Löscht und erstellt den Dienst erneut.|

> [!NOTE]
> Wenn BITS den Dienst erneut erstellt, kann die Dienst Beschreibungs Zeichenfolge auch in einem lokalisierten System auf Englisch festgelegt werden.

## <a name="examples"></a>Beispiele

So reparieren Sie die BITS-Dienst Konfiguration:

```
bitsadmin /util /repairservice
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "BIFS admin util"](bitsadmin-util.md)

- [Bider admin-Befehl](bitsadmin.md)
