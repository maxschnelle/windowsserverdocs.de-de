---
title: ver
description: Referenz Artikel für Ver, der die Versionsnummer des Betriebssystems anzeigt.
ms.topic: article
ms.assetid: 5a9c6cd4-b67d-4b30-8c56-5f9798eafd2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: de080395c2e26f03371e0b27609238b66d7317f5
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87891881"
---
# <a name="ver"></a>ver



Zeigt die Versionsnummer des Betriebssystems an.

Dieser Befehl wird in der Windows-Eingabeaufforderung (Cmd.exe), jedoch nicht in PowerShell unterstützt.



## <a name="syntax"></a>Syntax

```
ver
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Versionsnummer des Betriebssystems von der Befehlsshell (cmd.exe) abzurufen:

```
ver
```

Der Befehl "Ver" funktioniert nicht in PowerShell. Geben Sie Folgendes ein, um die Betriebssystemversion von PowerShell zu erhalten:

```powershell
$PSVersionTable.BuildVersion
````


## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
