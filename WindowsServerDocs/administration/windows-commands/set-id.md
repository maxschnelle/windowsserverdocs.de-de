---
title: Satz-id
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: da870c4a9676a08070e22f5391164af0bffd4df0
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441341"
---
# <a name="set-id"></a>Satz-id

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Der Befehl Diskpart-festlegen-ID ändert es sich um das Feld "Type" für die Partition mit dem Fokus.  
  
> [!IMPORTANT]  
> Dieser Befehl dient zur Verwendung durch Originalgerätehersteller \(OEMs\) nur. Partition Typfelder mit diesem Parameter ändern kann dazu führen, dass Ihr Computer ausfällt oder nicht für den Start. Es sei denn, Sie ein OEM sind oder bereits über Erfahrung mit Gpt-Datenträger, sollten Sie Partition-Feldern auf Gpt-Datenträgern durch Verwendung dieses Parameters nicht ändern. Verwenden Sie stattdessen immer die [erstellen Partition Efi](create-partition-efi.md) Befehl zum Erstellen von Partitionen für EFI-System, die [erstellen Partition Msr](create-partition-msr.md) Befehl aus, um Microsoft Reserved Partitionen zu erstellen und die [erstellen primäre Partition](create-partition-primary.md) Befehl ohne den ID-Parameter, um primäre Partitionen auf Gpt-Datenträgern zu erstellen.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
set id={ <byte> | <GUID> } [override] [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
| Parameter |                                                                                                                                                                                                                                                                                                                                                                   Beschreibung                                                                                                                                                                                                                                                                                                                                                                   |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  <byte>   |                                                                                                                                                                                                       für den master Boot Records \(MBR\) Datenträger, den neuen Wert für das Typfeld im hexadezimalen Format, für die Partition angibt. Jede Partition Typ Byte kann mit diesem Parameter mit Ausnahme von Typ 0 x 42, angegeben werden, die eine LDM-Partition angibt. Beachten Sie, dass das Präfix 0 X weggelassen wird, wenn Sie die hexadezimale Partitionstyp angeben.                                                                                                                                                                                                       |
|  <GUID>   | GUID-Partitionstabelle \(Gpt\) Datenträger, den neuen GUID-Wert für das Typfeld für die Partition angibt. Erkannte GUIDs einschließen möchten:<br /><br />-EFI Systempartition: c12a7328\-f81f\-11d 2\-ba4b\-00a0c93ec93b<br />-Einfache Datenpartition: ebd0a0a2\-b9e5\-4433\-87c 0\-68b6b72699c7<br /><br />Alle Partitionstyp GUID kann mit diesem Parameter mit Ausnahme der folgenden angegeben werden:<br /><br />– Microsoft Reserved-Partition: e3c9e316\-0b5c\-4db8\-817d\-f92df00215ae<br />-LDM Metadatenpartition auf einem dynamischen Datenträger: 5808c8aa\-7e8f\-42e0\-85d 2\-e1e90434cfb3<br />-LDM Datenpartition für einen dynamischen Datenträger: af9b60a0\-1431\-4f62\-bc68\-3311714a69ad<br />-Cluster-Metadatenpartition: db97dba9\-0840\-4bae\-97f0\-ffb9a327c7e1 |
| override  |                                                                Erzwingt, dass das Dateisystem auf dem Volume vor dem Ändern des Partitionstyps aufgehoben. Beim Ausführen der **IDs** Befehl DiskPart versucht wird, Sperren und Aufheben der Bereitstellung des Dateisystems auf dem Volume. Wenn **außer Kraft setzen** nicht angegeben ist, und der Aufruf, Sperren das Dateisystem fehlschlägt \(z. B. weil es ein geöffnetes Handle liegt\), der Vorgang schlägt fehl. Wenn **überschreiben** angegeben ist, DiskPart erzwingt die Aufheben der Bereitstellung, auch wenn der Aufruf von Sperren im Dateisystem ein Fehler auftritt, und alle geöffneten Handles zum Volume ungültig Dadurch werden.<br /><br />Dieser Befehl ist nur für Windows 7 und Windows Server 2008 R2 verfügbar.                                                                 |
|   Diskpart   |                                                                                                                                                                                                                                                                    Nur für Skripting verwendet. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.                                                                                                                                                                                                                                                                    |
  
## <a name="remarks"></a>Hinweise  
  
-   Keine Einschränkungen bereits erwähnt, DiskPart überprüft nicht die Gültigkeit der von Ihnen angegebenen Wert \(außer sicherstellen, dass es ein Byte im hexadezimalen Format oder eine GUID ist\).  
  
-   Dieser Befehl funktioniert nicht auf dynamischen Datenträgern oder auf Microsoft Reserved-Partition.  
  
## <a name="BKMK_examples"></a>Beispiele für  
Legen Sie das Typfeld auf 0 x 07, und erzwingen das Dateisystem zu entfernen, geben Sie Folgendes ein:  
  
```  
set id=0x07 override  
```  
  
Um das Typfeld werden einer Partition Basisdaten festzulegen, geben Sie Folgendes ein:  
  
```  
set id=ebd0a0a2-b9e5-4433-87c0-68b6b72699c7  
```  
  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

