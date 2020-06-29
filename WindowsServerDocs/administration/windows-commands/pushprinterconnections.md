---
title: pushprinterconnections
description: Referenz Thema für den Befehl pushprconnections, bei dem die Einstellungen der bereitgestellten Druckerverbindung aus Gruppenrichtlinie gelesen und Drucker Verbindungen bei Bedarf bereitgestellt bzw. entfernt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c30afb97-b149-478f-a4b9-2cbc25361818
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 701089f2597b1d4e7bc05f7949dbc80dee3535bb
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472125"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Druckbefehlsreferenz](print-command-reference.md)

- [Bereitstellen von Druckern mithilfe von Gruppenrichtlinie](https://go.microsoft.com/fwlink/?LinkId=230627)
