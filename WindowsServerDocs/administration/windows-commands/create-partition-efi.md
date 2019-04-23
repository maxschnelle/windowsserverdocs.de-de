---
title: Erstellen der Partition efi
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 3714cfe52aafd4a602346139552b6712dbbc98c1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878221"
---
# <a name="create-partition-efi"></a>Erstellen der Partition efi

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Auf Itanium\--basierten Computern erstellt eine Extensible Firmware Interface \(EFI\) Systempartition auf eine GUID-Partitionstabelle \(Gpt\) Datenträger.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
create partition efi [size=<n>] [offset=<n>] [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|Größe\=<n>|Die Größe der Partition in Megabytes \(MB\). Wenn keine Größe angegeben wird, wird die Partition erst in der aktuellen Region nicht mehr Speicherplatz verfügbar ist.|  
|offset\=<n>|Der Offset in Kilobyte \(KB\), an dem die Partition erstellt wird. Wird kein Offset angegeben wird, wird die Partition in der ersten Datenträgerbereich platziert, die groß genug für die sie enthalten ist.|  
|Diskpart|nur für Skripts. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.|  
  
## <a name="remarks"></a>Hinweise  
  
-   Nachdem Sie die Partition erstellt wurde, erhält der Fokus in die neue Partition.  
  
-   Ein Gpt-Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden. Verwenden der **select Disk** Befehl aus, wählen Sie einen Datenträger und verschiebt den Fokus auf sie.  
  
## <a name="BKMK_examples"></a>Beispiele für  
Um eine EFI-Systempartition von 1000 MB auf den ausgewählten Datenträger zu erstellen, geben Sie Folgendes ein:  
  
```  
create partition efi size=1000  
```  
  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

