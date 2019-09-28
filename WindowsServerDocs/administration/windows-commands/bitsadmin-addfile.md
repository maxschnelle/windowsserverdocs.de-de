---
title: bitsadmin addfile
description: Thema Windows-Befehle für **bigsadmin AddFile** -fügt dem angegebenen Auftrag eine Datei hinzu.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b31aa93-0364-465b-af36-754968825989
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8dfddda92e506dbfca2a47394a310edf16fe78aa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382041"
---
# <a name="bitsadmin-addfile"></a>bitsadmin addfile

Fügt dem angegebenen Auftrag eine Datei hinzu.

## <a name="syntax"></a>Syntax

```
bitsadmin /AddFile <Job> <RemoteURL> <LocalName>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|RemoteURL|Die URL der Datei auf dem Server.|
|LocalName|Der Name der Datei auf dem lokalen Computer. " *Localname* " muss einen absoluten Pfad zur Datei enthalten.|

## <a name="BKMK_examples"></a>Beispiele

Fügen Sie dem Auftrag eine Datei hinzu. Wiederholen Sie diesen Befehl für jede Datei, die Sie hinzufügen möchten. Wenn für mehrere Aufträge *mydownloadjob* als Name verwendet wird, müssen Sie *mydownloadjob* durch die GUID des Auftrags ersetzen, um den Auftrag eindeutig zu identifizieren.
```
C:\>bitsadmin /addfile myDownloadJob http://downloadsrv/10mb.zip c:\10mb.zip
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)