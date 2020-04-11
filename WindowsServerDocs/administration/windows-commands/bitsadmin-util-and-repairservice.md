---
title: bizadmin util und repaunservice
description: Windows-Befehls Thema für **BITSAdmin util und repaunservice**, das bekannte Probleme in verschiedenen Versionen des Bits-diensdienstanweises korrigiert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ac7baeb-4340-4186-bfcb-66478195378d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 164a402e7cbfc0a9223a97f4246eac84f0797aed
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122518"
---
# <a name="bitsadmin-util-and-repairservice"></a>bizadmin util und repaunservice

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
| /Force | Optional. Löscht und erstellt den Dienst erneut.|

> [!NOTE]
> Wenn BITS den Dienst erneut erstellt, kann die Dienst Beschreibungs Zeichenfolge auch in einem lokalisierten System auf Englisch festgelegt werden.

## <a name="examples"></a>Beispiele

Im folgenden Beispiel wird die BITS-Dienst Konfiguration repariert.

```
C:\>bitsadmin /util /repairservice
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)