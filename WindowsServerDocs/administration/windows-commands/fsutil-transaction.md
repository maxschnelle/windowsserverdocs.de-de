---
title: fsutil transaction
description: Referenz Thema für den Befehl "sasutil Transaction", der NTFS-Transaktionen verwaltet.
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: f2eefaaf-2817-4ac7-abac-d2b65fa971dc
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: fc81934c5838fd81722b27a7b7e57b14709ed26a
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2020
ms.locfileid: "83437045"
---
# <a name="fsutil-transaction"></a>fsutil transaction

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

Verwaltet NTFS-Transaktionen.

## <a name="syntax"></a>Syntax

```
fsutil transaction [commit] <GUID>
fsutil transaction [fileinfo] <filename>
fsutil transaction [list]
fsutil transaction [query] [{files | all}] <GUID>
fsutil transaction [rollback] <GUID>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Commit | Markiert das Ende einer erfolgreichen impliziten oder expliziten angegebenen Transaktion. |
| `<GUID>` | Gibt den GUID-Wert an, der eine Transaktion darstellt. |
| FileInfo  | Zeigt Transaktionsinformationen für die angegebene Datei an. |
| `<filename>` | Gibt den vollständigen Pfad und den Dateinamen an. |
| list | Zeigt eine Liste der derzeit laufenden Transaktionen an. |
| Abfrage | Zeigt Informationen für die angegebene Transaktion an.<ul><li>Wenn `fsutil transaction query files` angegeben wird, werden die Dateiinformationen nur für die angegebene Transaktion angezeigt.</li><li>Wenn `fsutil transaction query all` angegeben wird, werden alle Informationen für die Transaktion angezeigt.</li></ul> |
| rollback | Führt ein Rollback für eine angegebene Transaktion zum Anfang aus. |

### <a name="examples"></a>Beispiele

Um Transaktionsinformationen für die Datei " *c:\test.txt*" anzuzeigen, geben Sie Folgendes ein:

```
fsutil transaction fileinfo c:\test.txt
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [fsutil](fsutil.md)

- [Transaktions-NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc730726(v=ws.10))
