---
title: dispdiag
description: Windows-Befehls Thema für dispdiag, das Anzeigeinformationen in einer Datei protokolliert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5079e1dd-b57c-44ed-970f-e6b409369e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 498294aa6678cc4904880128bca55d7900c91db5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80845383"
---
# <a name="dispdiag"></a>dispdiag

Protokolliert Anzeigeinformationen in einer Datei.

## <a name="syntax"></a>Syntax

```
dispdiag [-testacpi] [-d] [-delay <Seconds>] [-out <FilePath>]
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-testacpi|Führt einen Hotkey-Diagnosetest aus. Zeigt den Schlüsselnamen, den Code und den Überprüfungs Code für alle während des Tests gedrückten Schlüssel an.|
|-d|Generiert eine Dumpdatei mit Testergebnissen.|
|-Verzögerung \<Sekunden >|Verzögert die Erfassung von Daten nach der angegebenen Zeit in *Sekunden*.|
|-Out \<filePath->|Gibt den Pfad und den Dateinamen zum Speichern der gesammelten Daten an. Dies muss der letzte Parameter sein.|
|-?|Zeigt verfügbare Befehlsparameter an und bietet Hilfe zur Verwendung.|