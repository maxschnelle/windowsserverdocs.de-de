---
title: ID festlegen
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5793d7ad-827e-4285-b2c6-ae60eeb0e886
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5b48cc701716412c4a79cedddb4458c57ba25ad5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384075"
---
# <a name="set-id"></a>ID festlegen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der DiskPart-Satz-ID-Befehl ändert das Feld Partitionstyp für die Partition mit dem Fokus.  
  
> [!IMPORTANT]  
> Dieser Befehl ist für die Verwendung durch die Originalgerätehersteller bestimmt \(oems @ no__t-1. Das Ändern von Partitionstyp Feldern mit diesem Parameter kann dazu führen, dass der Computer ausfällt oder nicht gestartet werden kann. Wenn Sie nicht OEM sind oder mit GPT-Datenträgern vertraut sind, sollten Sie die Partitionstyp Felder auf GPT-Datenträgern nicht mithilfe dieses Parameters ändern. Verwenden Sie stattdessen immer den Befehl [create partition efi](create-partition-efi.md) zum Erstellen von EFI-Systempartitionen, den [create partition msr](create-partition-msr.md) -Befehl zum Erstellen von reservierten Microsoft-Partitionen und den [create partition primary](create-partition-primary.md) -Befehl ohne den ID-Parameter für Erstellen Sie primäre Partitionen auf GPT-Datenträgern.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
set id={ <byte> | <GUID> } [override] [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
| Parameter |                                                                                                                                                                                                                                                                                                                                                                   Beschreibung                                                                                                                                                                                                                                                                                                                                                                   |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  <byte>   |                                                                                                                                                                                                       gibt für Master Boot Record \(mbr @ no__t-1-Datenträgern den neuen Wert für das typanfeld (in Hexadezimal Form) für die Partition an. Alle Partitionstypen Bytes können mit diesem Parameter angegeben werden, mit Ausnahme des Typs 0x42, der eine LDM-Partition angibt. Beachten Sie, dass das führende 0x beim Angeben des hexadezimalen Partitions Typs ausgelassen wird.                                                                                                                                                                                                       |
|  <GUID>   | gibt für die GUID-Partitionstabelle \(gpt @ no__t-1-Datenträger den neuen GUID-Wert für das typanfeld für die Partition an. Zu den erkannten GUIDs zählen:<br /><br />-EFI-Systempartition: c12a7328 @ no__t-0f81f @ no__t-111d2 @ no__t-2ba4b @ no__t-300a0c93ec93b<br />-Basic Data Partition: ebd0a0a2 @ no__t-0b9e5 @ no__t-14433 @ no__t-287c0 @ no__t-368b6b72699c7<br /><br />Jeder GUID des Partitions Typs kann mit diesem Parameter angegeben werden, mit Ausnahme der folgenden:<br /><br />-Microsoft Reserved Partition: e3c9e316 @ no__t-00b5c @ no__t-14db8 @ no__t-2817d @ no__t-3F 92 df00215ae<br />-LDM-Metadatenpartition auf einem dynamischen Datenträger: 5808c8aa @ no__t-07e8f @ no__t-142e0 @ no__t-285d2 @ no__t-3e1e90434cfb3<br />-LDM-Daten Partition auf einem dynamischen Datenträger: af9b60a0 @ no__t-01431 @ no__t-14f 62 @ no__t-2bc68 @ no__t-33311714a69ad<br />-Cluster Metadatenpartition: db97dba9 @ no__t-00840 @ no__t-14bae @ no__t-297f0 @ no__t-3ffb9a327c7e1 |
| Dire  |                                                                erzwingt das Aufheben der Einbindung des Dateisystems auf dem Volume, bevor der Partitionstyp geändert wird. Wenn Sie den Befehl **Set ID** ausführen, versucht Diskpart, das Dateisystem auf dem Volume zu sperren und zu entfernen. Wenn **override** nicht angegeben wird und der aufzurufende Befehl zum Sperren des Dateisystems \(Z. b., weil ein geöffnetes Handle @ no__t-2 vorhanden ist, schlägt der Vorgang fehl. Wenn **override** angegeben wird, erzwingt DiskPart die Aufhebung der Einbindung, auch wenn der aufzurufende Befehl zum Sperren des Dateisystems fehlschlägt und alle geöffneten Handles für das Volume ungültig werden.<br /><br />Dieser Befehl ist nur für Windows 7 und Windows Server 2008 R2 verfügbar.                                                                 |
|   Noerr   |                                                                                                                                                                                                                                                                    Wird nur für die Skripterstellung verwendet. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.                                                                                                                                                                                                                                                                    |
  
## <a name="remarks"></a>Hinweise  
  
-   Abgesehen von den zuvor erwähnten Einschränkungen überprüft DiskPart nicht die Gültigkeit des Werts, den Sie angeben, \(, außer um sicherzustellen, dass es sich um ein Byte in Hexadezimal Form oder um eine GUID @ no__t-1 handelt.  
  
-   Dieser Befehl funktioniert nicht auf dynamischen Datenträgern oder auf von Microsoft reservierten Partitionen.  
  
## <a name="BKMK_examples"></a>Beispiele  
Geben Sie Folgendes ein, um das typanfeld auf 0x07 festzulegen und das Aufheben der Einbindung des Dateisystems zu erzwingen:  
  
```  
set id=0x07 override  
```  
  
Geben Sie Folgendes ein, um das typanfeld als einfache Daten Partition festzulegen:  
  
```  
set id=ebd0a0a2-b9e5-4433-87c0-68b6b72699c7  
```  
  
#### <a name="additional-references"></a>Weitere Verweise  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

