---
title: bitsadmin addfile
description: Windows-Befehls Thema für **bigsadmin AddFile**, mit dem dem angegebenen Auftrag eine Datei hinzugefügt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1b31aa93-0364-465b-af36-754968825989
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 330e79eb2ba5a824cea54094f64ceb6f9cfd66b9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850963"
---
# <a name="bitsadmin-addfile"></a>bitsadmin addfile

Fügt dem angegebenen Auftrag eine Datei hinzu.

## <a name="syntax"></a>Syntax

```
bitsadmin /AddFile <Job> <RemoteURL> <LocalName>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| RemoteURL | Die URL der Datei auf dem Server. |
| LocalName | Der Name der Datei auf dem lokalen Computer. " *Localname* " muss einen absoluten Pfad zur Datei enthalten. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Fügen Sie dem Auftrag eine Datei hinzu. Wiederholen Sie diesen Befehl für jede Datei, die Sie hinzufügen möchten. Wenn für mehrere Aufträge *mydownloadjob* als Name verwendet wird, müssen Sie *mydownloadjob* durch die GUID des Auftrags ersetzen, um den Auftrag eindeutig zu identifizieren.

```
C:\>bitsadmin /addfile myDownloadJob http://downloadsrv/10mb.zip c:\10mb.zip
```

## <a name="additional-references"></a>Weitere Verweise

- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)&copy;