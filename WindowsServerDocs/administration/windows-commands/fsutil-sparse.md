---
ms.assetid: 77545920-2d13-4f35-a4d1-14dbec8340dc
title: Geringe Dichte
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 3d0df4e8e8dc16818273393062989ef7c0455c51
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725449"
---
# <a name="fsutil-sparse"></a>Geringe Dichte
> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

Verwaltet Dateien mit geringer Dichte.



## <a name="syntax"></a>Syntax

```
fsutil sparse [queryflag] <FileName>
fsutil sparse [queryrange] <FileName>
fsutil sparse [setflag] <FileName>
fsutil sparse [setrange] <FileName> <BeginningOffset> <Length>
```

### <a name="parameters"></a>Parameter

|     Parameter     |                                                    BESCHREIBUNG                                                    |
|-------------------|-------------------------------------------------------------------------------------------------------------------|
|     queryflag     |                                                  Abfragen mit geringer Dichte.                                                  |
|    queryrange     |                        Scannt eine Datei und sucht nach Bereichen, die möglicherweise Daten enthalten, die nicht NULL sind.                        |
|      setflag      |                                        Markiert die gekennzeichnete Datei als "Sparse".                                        |
|     SetRange      |                                   Füllt einen angegebenen Bereich einer Datei mit Nullen.                                   |
|    <FileName>     | Gibt den vollständigen Pfad zur Datei einschließlich des Datei namens und der Erweiterung an, z. b. "c:\documents\dateiname.txt". |
| <BeginningOffset> |                              Gibt den Offset in der Datei an, der als Sparse markiert werden soll.                              |
|     <Length>      |                 Gibt die Länge des Bereichs in der Datei an, der als Sparse (in Bytes) gekennzeichnet werden soll.                 |

## <a name="remarks"></a>Bemerkungen

-   Eine sparsedatei ist eine Datei mit einer oder mehreren Regionen nicht zugeordneter Daten. Die nicht zugeordneten Regionen werden von einem Programm als Bytes mit dem Wert 0 (null) angezeigt, es wird jedoch kein Speicherplatz zur Darstellung dieser Nullen verwendet. Alle aussagekräftigen Daten oder Daten, die nicht NULL sind, werden zugeordnet, während alle nicht aussagekräftigen Daten (große Daten Zeichenfolgen aus Nullen) nicht zugeordnet werden. Wenn eine sparsedatei gelesen wird, werden zugeordnete Daten als gespeichert zurückgegeben, und nicht zugeordnete Daten werden standardmäßig als Nullen in Übereinstimmung mit der C2-Sicherheits Anforderungsspezifikation zurückgegeben. Unterstützung für die Unterstützung von geringer Dichte ermöglicht die Zuordnung von Daten von jedem beliebigen Speicherort in der Datei

-   In einer sparsedatei ist für große Bereiche von Nullen möglicherweise keine Datenträger Zuordnung erforderlich. Der Speicherplatz für Daten, die nicht NULL sind, wird nach Bedarf zugeordnet, wenn die Datei geschrieben wird.

-   Nur komprimierte Dateien oder Dateien mit geringer Dichte können über nulloverbereiche verfügen, die dem Betriebssystem bekannt sind.

-   Wenn die Datei dünn oder komprimiert ist, kann der Speicherplatz in der Datei von NTFS aufgehoben werden. Dadurch wird der Byte Bereich auf Nullen festgelegt, ohne dass die Dateigröße erweitert wird.

## <a name="examples"></a><a name="BKMK_examples"></a>Beispiele
Geben Sie Folgendes ein, um eine Datei mit dem Namen Sample. txt im Verzeichnis c:\temp als Sparse zu markieren:

```
fsutil sparse setflag c:\temp\sample.txt 
```

## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Fsutil](Fsutil.md)


