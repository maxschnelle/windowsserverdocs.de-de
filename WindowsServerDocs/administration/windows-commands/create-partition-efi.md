---
title: Erstellen von EFI-Partitionen
description: Windows-Befehls Artikel zu create partition efi, mit dem eine Extensible Firmware Interface (EFI)-Systempartition auf einem GPT-Datenträger (GUID-Partitionstabelle) auf Itanium-basierten Computern erstellt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3cfc1fca-6515-4a4d-bfae-615fa8045ea9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a1c61f103fc719c8144e942f64172e3be554a414
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847043"
---
# <a name="create-partition-efi"></a>Erstellen von EFI-Partitionen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Auf Itanium-basierten Computern wird von eine Extensible Firmware Interface (EFI)-Systempartition auf einem GPT-Datenträger (GUID-Partitionstabelle) erstellt.

## <a name="syntax"></a>Syntax  
  
```  
create partition efi [size=<n>] [offset=<n>] [noerr]  
```  
  
### <a name="parameters"></a>Parameter  
  
|  Parameter  |                                                                                             Beschreibung                                                                                              |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  Größe\=<n>  |                         Die Größe der Partition in Megabyte \(MB\). Wenn keine Größe angegeben wird, wird die Partition so lange fortgesetzt, bis in der aktuellen Region kein freier Speicherplatz mehr verfügbar ist.                         |
| Offset\=<n> |             Der Offset in Kilobyte \(KB\), bei dem die Partition erstellt wird. Wenn kein Offset angegeben wird, wird die Partition in den ersten Datenträger Block eingefügt, der groß genug ist, um Sie zu speichern.              |
|    Noerr    | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |
  
## <a name="remarks"></a>Hinweise  
  
-   Nachdem die Partition erstellt wurde, wird der Fokus auf die neue Partition festgestellt.  
  
-   Ein GPT-Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl Datenträger **auswählen** einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.  
  
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele  
Geben Sie Folgendes ein, um eine EFI-Partition von 1000 Megabyte auf dem ausgewählten Datenträger zu erstellen:  
  
```  
create partition efi size=1000  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

