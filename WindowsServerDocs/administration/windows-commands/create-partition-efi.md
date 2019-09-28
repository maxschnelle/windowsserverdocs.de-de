---
title: Erstellen von EFI-Partitionen
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3cfc1fca-6515-4a4d-bfae-615fa8045ea9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 76d97129fd67345f23eee2fc7b300493a1632cc6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379009"
---
# <a name="create-partition-efi"></a>Erstellen von EFI-Partitionen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt auf Itanium @ no__t-0based Computers eine Extensible Firmware Interface \(efi @ no__t-2-Systempartition in einer GUID-Partitionstabelle \(gpt @ no__t-4-Datenträger.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
create partition efi [size=<n>] [offset=<n>] [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
|  Parameter  |                                                                                             Beschreibung                                                                                              |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  Size @ no__t-0 @ no__t-1  |                         Die Größe der Partition in Megabyte \(MB @ no__t-1. Wenn keine Größe angegeben wird, wird die Partition so lange fortgesetzt, bis in der aktuellen Region kein freier Speicherplatz mehr verfügbar ist.                         |
| Offset @ no__t-0 @ no__t-1 |             Der Offset in Kilobyte \(KB @ no__t-1, bei dem die Partition erstellt wird. Wenn kein Offset angegeben wird, wird die Partition in den ersten Datenträger Block eingefügt, der groß genug ist, um Sie zu speichern.              |
|    Noerr    | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |
  
## <a name="remarks"></a>Hinweise  
  
-   Nachdem die Partition erstellt wurde, wird der Fokus auf die neue Partition festgestellt.  
  
-   Ein GPT-Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl Datenträger **auswählen** einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.  
  
## <a name="BKMK_examples"></a>Beispiele  
Geben Sie Folgendes ein, um eine EFI-Partition von 1000 Megabyte auf dem ausgewählten Datenträger zu erstellen:  
  
```  
create partition efi size=1000  
```  
  
#### <a name="additional-references"></a>Weitere Verweise  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

