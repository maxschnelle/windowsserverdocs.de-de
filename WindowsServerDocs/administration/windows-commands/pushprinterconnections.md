---
title: pushprinterconnections
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c30afb97-b149-478f-a4b9-2cbc25361818 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c571d3adffd0e6a28f63f6d821b2524dc055aa9a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873721"
---
# <a name="pushprinterconnections"></a>pushprinterconnections



Druckerverbindung bereitgestellten Einstellungen der Gruppenrichtlinie gelesen, und klicken Sie mit der druckerverbindungen je nach Bedarf bereitgestellt oder entfernt.

## <a name="syntax"></a>Syntax

```
pushprinterconnections <-log> <-?>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|<-log>|Schreibt eine pro Benutzer Debugprotokolldatei % Temp oder schreibt eine pro Computer Debugprotokoll % windir%\temp.|
|<-?>|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Dieses Dienstprogramm ist für die Verwendung in Computer starten oder Benutzer Anmeldeskripts und sollte nicht über die Befehlszeile ausgeführt werden.

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Bereitstellen von Druckern mithilfe der Gruppenrichtlinie](https://go.microsoft.com/fwlink/?LinkId=230627)