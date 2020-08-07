---
title: bitsadmin util and repairservice
description: Referenz Artikel für den Befehl BITSAdmin util und repaunservice, der bekannte Probleme in verschiedenen Versionen des Bits-diensdienstanweises korrigiert.
ms.topic: article
ms.assetid: 2ac7baeb-4340-4186-bfcb-66478195378d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4d90e6328376f52e60b598d8c2324b59877415db
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880852"
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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "BIFS admin util"](bitsadmin-util.md)

- [Bider admin-Befehl](bitsadmin.md)
