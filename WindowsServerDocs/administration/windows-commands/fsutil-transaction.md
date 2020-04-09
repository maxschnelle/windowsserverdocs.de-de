---
ms.assetid: f2eefaaf-2817-4ac7-abac-d2b65fa971dc
title: Ssutil-Transaktion
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: aa6692dbb8af1ec832650971c6723c060fc2cd56
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844013"
---
# <a name="fsutil-transaction"></a>Ssutil-Transaktion
>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7, Windows 2008, Windows Vista

Verwaltet NTFS-Transaktionen.

Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_examples) .

## <a name="syntax"></a>Syntax

```
fsutil transaction [commit] <GUID>
fsutil transaction [fileinfo] <Filename>
fsutil transaction [list]
fsutil transaction [query] [{Files|All}] <GUID>
fsutil transaction [rollback] <GUID>
```

#### <a name="parameters"></a>Parameter

| Parameter  |                                                                                                                                                     Beschreibung                                                                                                                                                     |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   einzusetzen   |                                                                                                                      Markiert das Ende einer erfolgreichen impliziten oder expliziten angegebenen Transaktion.                                                                                                                      |
|   <GUID>   |                                                                                                                               Gibt den GUID-Wert an, der eine Transaktion darstellt.                                                                                                                               |
|  FileInfo  |                                                                                                                              Zeigt Transaktionsinformationen für die angegebene Datei an.                                                                                                                               |
| <Filename> |                                                                                                                                         Gibt den vollständigen Pfad und den Dateinamen an.                                                                                                                                          |
|    list    |                                                                                                                                 Zeigt eine Liste der derzeit laufenden Transaktionen an.                                                                                                                                  |
|   Abfrage    | Zeigt Informationen für die angegebene Transaktion an.<p>-Wenn die file- **Transaktions Abfrage Dateien** angegeben sind, werden die Dateiinformationen nur für die angegebene Transaktion angezeigt.<br />-Wenn die vollständig ausgestellte **Transaktions Abfrage** angegeben ist, werden alle Informationen für die Transaktion angezeigt. |
|  rollback  |                                                                                                                                Führt ein Rollback für eine angegebene Transaktion zum Anfang aus.                                                                                                                                 |

### <a name="remarks"></a>Hinweise

-   Transaktionale NTFS wurde in Windows Server 2008 eingeführt.

### <a name="examples"></a><a name="BKMK_examples"></a>Beispiele
Um Transaktionsinformationen für die Datei "c:\test.txt" anzuzeigen, geben Sie Folgendes ein:

```
fsutil transaction fileinfo c:\test.txt  
```

### <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Fsutil](Fsutil.md)

[Transaktionale NTFS](https://go.microsoft.com/fwlink/?LinkID=165402)


