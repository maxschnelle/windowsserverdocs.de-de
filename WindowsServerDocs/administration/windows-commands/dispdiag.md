---
title: dispdiag
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 9c96c70aac1b3329e050fa8b02743e61fed44d15
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831461"
---
# <a name="dispdiag"></a>dispdiag



Protokolle werden Informationen angezeigt, in eine Datei.

## <a name="syntax"></a>Syntax

```
dispdiag [-testacpi] [-d] [-delay <Seconds>] [-out <FilePath>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-Testacpi|Hotkey-Diagnosetest ausgeführt wird. Zeigt den Schlüsselnamen, Code und -Scan-Code für eine beliebige Taste gedrückt, während des Tests.|
|-d|Generiert eine Dumpdatei mit Testergebnissen an.|
|-Delay \<Sekunden >|Das Sammeln von Daten, um die angegebene Zeit im verzögert *Sekunden*.|
|-out \<"FilePath" >|Gibt Pfad und Dateinamen zum Speichern von gesammelten Daten. Dies muss der letzte Parameter sein.|
|-?|Zeigt verfügbare Befehlsparameter an und enthält die Hilfe zu ihrer Verwendung.|