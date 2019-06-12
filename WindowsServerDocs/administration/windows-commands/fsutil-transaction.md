---
ms.assetid: f2eefaaf-2817-4ac7-abac-d2b65fa971dc
title: Fsutil-Transaktion
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: c225c99919a2558559b1ec7a47b61d716e199a73
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439002"
---
# <a name="fsutil-transaction"></a>Fsutil-Transaktion
>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, WindowsServer 2012, Windows 8, Windows Server 2008 R2, Windows 7, Windows 2008, Windows Vista

Die NTFS-Transaktionen verwaltet.

Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](#BKMK_examples) .

## <a name="syntax"></a>Syntax

```
fsutil transaction [commit] <GUID>
fsutil transaction [fileinfo] <Filename>
fsutil transaction [list]
fsutil transaction [query] [{Files|All}] <GUID>
fsutil transaction [rollback] <GUID>
```

### <a name="parameters"></a>Parameter

| Parameter  |                                                                                                                                                     Beschreibung                                                                                                                                                     |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   Commit   |                                                                                                                      Markiert das Ende einer erfolgreichen implizit oder explizit angegebenen Transaktion.                                                                                                                      |
|   <GUID>   |                                                                                                                               Gibt den GUID-Wert, der eine Transaktion darstellt.                                                                                                                               |
|  "FileInfo"  |                                                                                                                              Zeigt den Transaktionsinformationen für die angegebene Datei.                                                                                                                               |
| <Filename> |                                                                                                                                         Gibt an, Vollständiger Pfad und Dateinamen.                                                                                                                                          |
|    list    |                                                                                                                                 Zeigt eine Liste der aktuell ausgeführten Transaktionen.                                                                                                                                  |
|   query    | Zeigt Informationen über die angegebene Transaktion.<br /><br />-If **Fsutil Transaktion Abfragedateien** angegeben ist, werden die Informationen werden nur für die angegebene Transaktion angezeigt.<br />-If **Fsutil-Transaktion Abfragen alle** angegeben ist, werden alle Informationen für die Transaktion angezeigt werden. |
|  rollback  |                                                                                                                                Setzt eine angegebene Transaktion an den Anfang zurück.                                                                                                                                 |

### <a name="remarks"></a>Hinweise

-   Transaktions-NTFS wurde in Windows Server 2008 eingeführt.

### <a name="BKMK_examples"></a>Beispiele für
Um Transaktionsinformationen für die Datei c:\test.txt anzuzeigen, geben Sie Folgendes ein:

```
fsutil transaction fileinfo c:\test.txt  
```

### <a name="additional-references"></a>Weitere Verweise
[Erläuterung zur Befehlszeilensyntax](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

[Transaktions-NTFS](https://go.microsoft.com/fwlink/?LinkID=165402)


