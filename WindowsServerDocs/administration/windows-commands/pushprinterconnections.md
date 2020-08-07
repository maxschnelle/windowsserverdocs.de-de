---
title: pushprinterconnections
description: Referenz Artikel zum pushprconnections-Befehl, der die bereitgestellten Drucker Verbindungseinstellungen aus Gruppenrichtlinie liest und Drucker Verbindungen bei Bedarf bereitstellt bzw. entfernt.
ms.topic: article
ms.assetid: c30afb97-b149-478f-a4b9-2cbc25361818
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 07d792b31b6ff8ead9e027c711fb91d87ba54ebd
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87884569"
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
