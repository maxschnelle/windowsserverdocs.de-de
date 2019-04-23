---
ms.assetid: 77545920-2d13-4f35-a4d1-14dbec8340dc
title: Fsutil-sparsedatei
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 76a263c82ebc42de4cc6d136f9a814c3a678666b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878391"
---
# <a name="fsutil-sparse"></a>Fsutil-sparsedatei
>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, WindowsServer 2012, Windows 8, Windows Server 2008 R2, Windows 7

Verwaltet die Dateien mit geringer Dichte.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
fsutil sparse [queryflag] <FileName>
fsutil sparse [queryrange] <FileName>
fsutil sparse [setflag] <FileName>
fsutil sparse [setrange] <FileName> <BeginningOffset> <Length>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------------|---------------|
|queryflag|Abfragen mit geringer Dichte.|
|queryrange|Durchsucht eine Datei, und sucht nach Bereichen, die möglicherweise Daten ungleich NULL enthalten.|
|SETFLAG|Markiert die angegebene Datei mit geringer Dichte.|
|SetRange|Füllt einen angegebenen Bereich von einer Datei mit Nullen aufgefüllt.|
|<FileName>|Gibt den vollständigen Pfad zur Datei einschließlich der Namen und die Erweiterung, z. B. C:\documents\filename.txt an.|
|<BeginningOffset>|Gibt den Offset in der Datei um geringen Dichte zu markieren.|
|<Length>|Gibt die Länge des Bereichs in der Datei als mit geringer Dichte (in Byte) markiert werden.|

## <a name="remarks"></a>Hinweise

-   Eine Datei mit geringer Dichte ist eine Datei mit einer oder mehreren Regionen des nicht zugeordneten Daten. Ein Programm, wird diese nicht zugewiesenen Regionen als mit Bytes, die mit dem Wert 0 (null) angezeigt, aber kein Speicherplatz wird verwendet, um diese Nullen darstellen. Alle Daten von Bedeutung sind oder ungleich NULL sind reserviert, während alle nonmeaningful Daten (large Zeichenfolgen von Daten, die aus Nullen besteht) ist nicht zugeordnet. Wenn eine Datei mit geringer Dichte gelesen wird, zugeordnete Daten werden zurückgegeben, da gespeichert, und nicht zugeordnete Daten werden zurückgegeben, in der Standardeinstellung als Nullen, gemäß der C2-Sicherheitsspezifikation. Unterstützung der Datei mit geringer Dichte kann Daten an einer beliebigen Stelle in der Datei aufgehoben werden soll.

-   In einer Datei mit geringer Dichte können große Bereiche mit Nullen nicht datenträgerzuordnung erfordern. Je nach Bedarf, wenn die Datei geschrieben wird, wird Speicherplatz für Daten ungleich NULL zugeordnet.

-   Nur Dateien komprimierte oder mit geringer Dichte können Bereiche bekannt, dass das Betriebssystem auf NULL gesetzt haben.

-   Wenn die Datei mit geringer Dichte oder komprimierten ist, kann NTFS Speicherplatz in der Datei freigeben. Hiermit wird der Bereich von Bytes auf Nullen, ohne die Dateigröße zu erweitern.

## <a name="BKMK_examples"></a>Beispiele für
Um eine Datei namens "Sample.txt" im Verzeichnis "C:\Temp" als mit geringer Dichte zu markieren, geben Sie Folgendes ein:

```
fsutil sparse setflag c:\temp\sample.txt 
```

#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilensyntax](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


