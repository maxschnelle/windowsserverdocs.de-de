---
title: assign
description: Windows-Befehls Thema für **assign**, das dem Volume einen Laufwerk Buchstaben oder einen Einfügepunkt mit Fokus zuweist.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 57912b73-622e-489b-b053-a369021ba8e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c4745b0472e2c8ee7a4034d9a06d395d6089db6f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851303"
---
# <a name="assign"></a>assign

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Weist dem Volume mit dem Fokus einen Laufwerk Buchstaben oder einen Einfügepunkt zu.

## <a name="syntax"></a>Syntax

```
assign [{letter=<d> | mount=<path>}] [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `letter=<d>` | Der Laufwerk Buchstabe, der dem Volume zugewiesen werden soll. |
| `mount=<path>` | Der Pfad des einstellungspunkts, der dem Volume zugewiesen werden soll. Anweisungen zur Verwendung dieses Befehls finden [Sie unter Zuweisen eines Ordners für einen einstellungspunktpfad zu einem Laufwerk](https://go.microsoft.com/fwlink/?LinkId=207059). |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="remarks"></a>Hinweise

- Wenn kein Laufwerk Buchstabe oder Einfügepunkt angegeben ist, wird der nächste verfügbare Laufwerk Buchstabe zugewiesen. Wenn der Laufwerk Buchstabe oder der Einfügepunkt bereits verwendet wird, wird ein Fehler generiert.

- Mit dem Befehl zuweisen können Sie den Laufwerk Buchstaben ändern, der einem Wechsel Datenträger zugeordnet ist.

- Sie können den Systemvolumes, Start Volumes oder Volumes, die die Auslagerungs Datei enthalten, keine Laufwerk Buchstaben zuweisen. Außerdem ist es nicht möglich, einem Original Gerätehersteller (OEM) oder einer anderen GPT-Partition (GUID-Partitionstabelle) einen Laufwerk Buchstaben zuzuweisen, der keine grundlegende Daten Partition ist.

- Ein Volume muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl **Volume auswählen** ein Volume aus, und verschieben Sie den Fokus auf das Volume.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Geben Sie Folgendes ein, um den Buchstaben E dem Volume im Fokus zuzuweisen:
```
assign letter=e
```

## <a name="additional-references"></a>Weitere Verweise

- [Befehlszeilen-Syntax Schlüssel] (Command-Line-Syntax-Key.MD

