---
title: pushprinterconnections
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c30afb97-b149-478f-a4b9-2cbc25361818
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1ed83b51da5ad7ad0a6b4dc0afd1d6bc30803a98
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222050"
---
# <a name="pushprinterconnections"></a>pushprinterconnections



Liest bereitgestellte Drucker Verbindungseinstellungen aus Gruppenrichtlinie und stellt Drucker Verbindungen nach Bedarf bereit/entfernt Sie.

## <a name="syntax"></a>Syntax

```
pushprinterconnections <-log> <-?>
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|< Protokoll>|Schreibt eine pro-Benutzer-Debug-Protokolldatei in% Temp oder schreibt ein pro-Computer-Debugprotokoll in%windir%\temp.|
|<-? >|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Dieses Hilfsprogramm ist für das Starten von Computern oder Benutzer Anmelde Skripts vorgesehen und sollte nicht über die Befehlszeile ausgeführt werden.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Bereitstellen von Druckern mithilfe von Gruppenrichtlinie](https://go.microsoft.com/fwlink/?LinkId=230627)