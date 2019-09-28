---
title: assign
description: Thema Windows-Befehle für **assign** -weist dem Volume mit dem Fokus einen Laufwerk Buchstaben oder einen Einfügepunkt zu.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 57912b73-622e-489b-b053-a369021ba8e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3e07edcd4ac4ddf5eca1e57da17df441043d15f6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382679"
---
# <a name="assign"></a>assign

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

weist dem Volume mit dem Fokus einen Laufwerk Buchstaben oder einen Einfügepunkt zu.

## <a name="syntax"></a>Syntax
```
assign [{letter=<d> | mount=<path>}] [noerr]
```
## <a name="parameters"></a>Parameter

|  Parameter   |                                                                                                                                 Beschreibung                                                                                                                                 |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  Buchstabe = <d>  |                                                                                                             Der Laufwerk Buchstabe, der dem Volume zugewiesen werden soll.                                                                                                              |
| Mount = <path> | Der Pfad des einstellungspunkts, der dem Volume zugewiesen werden soll.<br /><br />Anweisungen zur Verwendung dieses Befehls finden [Sie unter Zuweisen eines Ordners für einen einstellungspunktpfad zu einem Laufwerk](https://go.microsoft.com/fwlink/?LinkId=207059) (<https://go.microsoft.com/fwlink/?LinkId=207059>). |
|    Noerr     |                                    Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.                                     |

## <a name="remarks"></a>Hinweise
- Wenn kein Laufwerk Buchstabe oder Einfügepunkt angegeben ist, wird der nächste verfügbare Laufwerk Buchstabe zugewiesen. Wenn der Laufwerk Buchstabe oder der Einfügepunkt bereits verwendet wird, wird ein Fehler generiert.
- Mit dem Befehl zuweisen können Sie den Laufwerk Buchstaben ändern, der einem Wechsel Datenträger zugeordnet ist.
- Sie können den Systemvolumes, Start Volumes oder Volumes, die die Auslagerungs Datei enthalten, keine Laufwerk Buchstaben zuweisen. Außerdem ist es nicht möglich, einem Original Gerätehersteller (OEM) oder einer anderen GPT-Partition (GUID-Partitionstabelle) einen Laufwerk Buchstaben zuzuweisen, der keine grundlegende Daten Partition ist.
- Ein Volume muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl **Volume auswählen** ein Volume aus, und verschieben Sie den Fokus auf das Volume.
  ## <a name="BKMK_examples"></a>Beispiele
  Geben Sie Folgendes ein, um den Buchstaben E dem Volume im Fokus zuzuweisen:
  ```
  assign letter=e
  ```

