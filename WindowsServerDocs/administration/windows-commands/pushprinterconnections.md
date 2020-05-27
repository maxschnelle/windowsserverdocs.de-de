---
title: pushprinterconnections
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c30afb97-b149-478f-a4b9-2cbc25361818 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 55294b27ec51edb7083debf15e332117b9b4e1df
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83821230"
---
# <a name="pushprinterconnections"></a>pushprinterconnections



Liest bereitgestellte Drucker Verbindungseinstellungen aus Gruppenrichtlinie und stellt Drucker Verbindungen nach Bedarf bereit/entfernt Sie.

## <a name="syntax"></a>Syntax

```
pushprinterconnections <-log> <-?>
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|< Protokoll>|Schreibt eine pro-Benutzer-Debug-Protokolldatei in% Temp oder schreibt ein pro-Computer-Debugprotokoll in%windir%\temp.|
|<-? >|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Dieses Hilfsprogramm ist für das Starten von Computern oder Benutzer Anmelde Skripts vorgesehen und sollte nicht über die Befehlszeile ausgeführt werden.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Bereitstellen von Druckern mithilfe von Gruppenrichtlinie](https://go.microsoft.com/fwlink/?LinkId=230627)