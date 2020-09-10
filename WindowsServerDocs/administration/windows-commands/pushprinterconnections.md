---
title: pushprinterconnections
description: Referenz Artikel zum pushprconnections-Befehl, der die bereitgestellten Drucker Verbindungseinstellungen aus Gruppenrichtlinie liest und Drucker Verbindungen bei Bedarf bereitstellt bzw. entfernt.
ms.topic: reference
ms.assetid: c30afb97-b149-478f-a4b9-2cbc25361818
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ef1cfc110d446da461251b9c7e28a4595edee291
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639931"
---
# <a name="pushprinterconnections"></a>pushprinterconnections

Liest bereitgestellte Drucker Verbindungseinstellungen aus Gruppenrichtlinie und stellt Drucker Verbindungen nach Bedarf bereit/entfernt Sie.

> [!IMPORTANT]
> Dieses Hilfsprogramm dient der Verwendung beim Starten von Computern oder Benutzer Anmelde Skripts und sollte nicht über die Befehlszeile ausgeführt werden.

## <a name="syntax"></a>Syntax

```
pushprinterconnections <-log> <-?>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| < Protokoll> | Schreibt eine pro-Benutzer-Debug-Protokolldatei in *% Temp*oder schreibt ein pro-Computer-Debugprotokoll in " *%WINDIR%\Temp*". |
| <-? > | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Druckbefehlsreferenz](print-command-reference.md)

- [Bereitstellen von Druckern mithilfe von Gruppenrichtlinie](https://go.microsoft.com/fwlink/?LinkId=230627)
