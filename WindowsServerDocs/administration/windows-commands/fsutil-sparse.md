---
title: fsutil sparse
description: Referenz Artikel für den Befehl "" mit geringer Dichte, der sparsesdateien verwaltet.
manager: dmoss
ms.author: toklima
author: toklima
ms.assetid: 77545920-2d13-4f35-a4d1-14dbec8340dc
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: d79144d3894e9e181ebd889ce7bf281b827dea26
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889840"
---
# <a name="fsutil-sparse"></a>fsutil sparse

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

Verwaltet Dateien mit geringer Dichte. Eine sparsedatei ist eine Datei mit einer oder mehreren Regionen nicht zugeordneter Daten.

Die nicht zugeordneten Regionen werden von einem Programm als Bytes mit einem Wert von 0 (null) angezeigt, und es ist kein Speicherplatz vorhanden, der diese Nullen darstellt. Wenn eine sparsedatei gelesen wird, werden zugeordnete Daten als gespeichert zurückgegeben, und nicht zugeordnete Daten werden standardmäßig als Nullen in Übereinstimmung mit der C2-Sicherheits Anforderungsspezifikation zurückgegeben. Unterstützung für die Unterstützung von geringer Dichte ermöglicht die Zuordnung von Daten von jedem beliebigen Speicherort in der Datei

## <a name="syntax"></a>Syntax

```
fsutil sparse [queryflag] <filename>
fsutil sparse [queryrange] <filename>
fsutil sparse [setflag] <filename>
fsutil sparse [setrange] <filename> <beginningoffset> <length>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| queryflag | Abfragen mit geringer Dichte. |
| queryrange | Scannt eine Datei und sucht nach Bereichen, die möglicherweise Daten enthalten, die nicht NULL sind. |
| setflag | Markiert die gekennzeichnete Datei als "Sparse". |
| SetRange | Füllt einen angegebenen Bereich einer Datei mit Nullen. |
| `<filename>` | Gibt den vollständigen Pfad zur Datei einschließlich des Datei namens und der Erweiterung an, z. b. *C:\documents\filename.txt*. |
| `<beginningoffset>` | Gibt den Offset in der Datei an, der als Sparse markiert werden soll. |
| `<length>` | Gibt die Länge des Bereichs in der Datei an, der als Sparse (in Bytes) gekennzeichnet werden soll. |

#### <a name="remarks"></a>Bemerkungen

- Alle aussagekräftigen Daten oder Daten, die nicht NULL sind, werden zugeordnet, während alle nicht aussagekräftigen Daten (große Daten Zeichenfolgen aus Nullen) nicht zugeordnet werden.

- In einer sparsedatei ist für große Bereiche von Nullen möglicherweise keine Datenträger Zuordnung erforderlich. Der Speicherplatz für Daten, die nicht NULL sind, wird nach Bedarf zugeordnet, wenn die Datei geschrieben wird.

- Nur komprimierte Dateien oder Dateien mit geringer Dichte können über nulloverbereiche verfügen, die dem Betriebssystem bekannt sind.

- Wenn die Datei dünn oder komprimiert ist, kann NTFS die Zuordnung von Speicherplatz in der Datei aufheben. Dadurch wird der Byte Bereich auf Nullen festgelegt, ohne dass die Dateigröße erweitert wird.

### <a name="examples"></a>Beispiele

Um eine Datei namens *sample.txt* im Verzeichnis " *c:\temp* " als "Sparse" zu markieren, geben Sie Folgendes ein:

```
fsutil sparse setflag c:\temp\sample.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [fsutil](fsutil.md)
