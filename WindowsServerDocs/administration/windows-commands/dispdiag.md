---
title: dispdiag
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5079e1dd-b57c-44ed-970f-e6b409369e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9b640883a207648d2ef6c9a7d6e5366cd0bb384c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377757"
---
# <a name="dispdiag"></a>dispdiag



Protokolliert Anzeigeinformationen in einer Datei.

## <a name="syntax"></a>Syntax

```
dispdiag [-testacpi] [-d] [-delay <Seconds>] [-out <FilePath>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-testacpi|Führt einen Hotkey-Diagnosetest aus. Zeigt den Schlüsselnamen, den Code und den Überprüfungs Code für alle während des Tests gedrückten Schlüssel an.|
|-d|Generiert eine Dumpdatei mit Testergebnissen.|
|-Verzögerung \<sekunden >|Verzögert die Erfassung von Daten nach der angegebenen Zeit in *Sekunden*.|
|-Out \<filepath >|Gibt den Pfad und den Dateinamen zum Speichern der gesammelten Daten an. Dies muss der letzte Parameter sein.|
|-?|Zeigt verfügbare Befehlsparameter an und bietet Hilfe zur Verwendung.|