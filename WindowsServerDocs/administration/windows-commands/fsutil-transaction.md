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
ms.openlocfilehash: 18088bcedd077d5c8052bca91c648e2719304a78
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720091"
---
# <a name="fsutil-transaction"></a>Ssutil-Transaktion
> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7, Windows 2008, Windows Vista

Verwaltet NTFS-Transaktionen.



## <a name="syntax"></a>Syntax

```
fsutil transaction [commit] <GUID>
fsutil transaction [fileinfo] <Filename>
fsutil transaction [list]
fsutil transaction [query] [{Files|All}] <GUID>
fsutil transaction [rollback] <GUID>
```

#### <a name="parameters"></a>Parameter

| Parameter  |                                                                                                                                                     BESCHREIBUNG                                                                                                                                                     |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   Commit   |                                                                                                                      Markiert das Ende einer erfolgreichen impliziten oder expliziten angegebenen Transaktion.                                                                                                                      |
|   <GUID>   |                                                                                                                               Gibt den GUID-Wert an, der eine Transaktion darstellt.                                                                                                                               |
|  FileInfo  |                                                                                                                              Zeigt Transaktionsinformationen für die angegebene Datei an.                                                                                                                               |
| <Filename> |                                                                                                                                         Gibt den vollständigen Pfad und den Dateinamen an.                                                                                                                                          |
|    list    |                                                                                                                                 Zeigt eine Liste der derzeit laufenden Transaktionen an.                                                                                                                                  |
|   Abfrage    | Zeigt Informationen für die angegebene Transaktion an.<p>-Wenn die file- **Transaktions Abfrage Dateien** angegeben sind, werden die Dateiinformationen nur für die angegebene Transaktion angezeigt.<br />-Wenn die vollständig ausgestellte **Transaktions Abfrage** angegeben ist, werden alle Informationen für die Transaktion angezeigt. |
|  rollback  |                                                                                                                                Führt ein Rollback für eine angegebene Transaktion zum Anfang aus.                                                                                                                                 |

### <a name="remarks"></a>Bemerkungen

-   Transaktionale NTFS wurde in Windows Server 2008 eingeführt.

### <a name="examples"></a><a name="BKMK_examples"></a>Beispiele
Um Transaktionsinformationen für die Datei "c:\test.txt" anzuzeigen, geben Sie Folgendes ein:

```
fsutil transaction fileinfo c:\test.txt  
```

### <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Fsutil](Fsutil.md)

[Transaktions-NTFS](https://go.microsoft.com/fwlink/?LinkID=165402)


