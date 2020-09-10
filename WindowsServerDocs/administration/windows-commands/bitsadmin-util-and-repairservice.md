---
title: bitsadmin util and repairservice
description: Referenz Artikel für den Befehl BITSAdmin util und repaunservice, der bekannte Probleme in verschiedenen Versionen des Bits-diensdienstanweises korrigiert.
ms.topic: reference
ms.assetid: 2ac7baeb-4340-4186-bfcb-66478195378d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 0bef08a3e0db8973de9370279144be5951445cc3
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630439"
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
| /Force | (Optional) Löscht und erstellt den Dienst erneut.|

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
