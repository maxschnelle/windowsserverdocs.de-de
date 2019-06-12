---
ms.assetid: fb95c8ee-a418-4520-a12a-7754ae947c3c
title: Fsutil reparsepoint
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: f66f09fa608fec10d7126e516f9cf2dd8a19bbfb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438997"
---
# <a name="fsutil-reparsepoint"></a>Fsutil reparsepoint
>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, WindowsServer 2012, Windows 8, Windows Server 2008 R2, Windows 7, Windows 2008, Windows Vista

Abfragen oder Löschvorgänge Analysepunkte.  Die **Fsutil Reparsepoint** Befehl wird in der Regel von Supportmitarbeitern verwendet.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
fsutil reparsepoint [query] <FileName>
fsutil reparsepoint [delete] <FileName>
```

## <a name="parameters"></a>Parameter

| Parameter  |                                                                Beschreibung                                                                |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------|
|   query    |            Ruft ab, die Punkt-Analysedaten, die Datei oder des Verzeichnisses identifiziert, die durch das angegebene Handle zugeordnet ist.             |
|   löschen   | Löscht einen Analysepunkt aus der Datei bzw. das Verzeichnis, das wird durch das angegebene Handle identifiziert, jedoch werden nicht gelöscht werden, die Datei oder das Verzeichnis an. |
| <FileName> |             Gibt den vollständigen Pfad zur Datei einschließlich der Namen und die Erweiterung, z. B. C:\documents\filename.txt an.             |

## <a name="remarks"></a>Hinweise

-   Analysepunkte sind NTFS-Systemobjekte, die ein angegebener Anzahl-Attribut aufweisen, die den benutzerdefinierten Daten enthält, und sie werden verwendet, um Funktionalität in der Eingabe/Ausgabe (e/a)-Subsystem zu erweitern.

-   Analysepunkt für Directory Verknüpfungspunkte und Volumebereitstellungspunkten verwendet. Sie werden auch von Dateisystemfilter-Treiber verwendet, um bestimmte Dateien als Sonderzeichen auf diesen Treiber zu markieren.

-   Wenn ein Programm einen Analysepunkt festlegt, speichert sie diese Daten, sowie einer analysenkennung, die die Daten eindeutig identifiziert wird, die sie gespeichert sind. Wenn das Dateisystem eine Datei einen Analysepunkt geöffnet wird, versucht, den zugeordneten Dateisystemfilter zu finden. Wenn der Dateisystemfilter gefunden wird, verarbeitet der Filter die Datei an, wie durch die Analysedaten. Wenn keine Dateisystemfilter gefunden wird, kann die Datei öffnen.

## <a name="BKMK_examples"></a>Beispiele für
Um Analysepunktdaten C:\Server zugeordneten abzurufen, geben Sie Folgendes ein:

```
fsutil reparsepoint query c:\server
```

Um einen Analysepunkt aus einer Datei oder das Verzeichnis zu löschen, verwenden Sie das folgende Format:

```
fsutil reparsepoint delete c:\server
```

#### <a name="additional-references"></a>Weitere Verweise
[Erläuterung zur Befehlszeilensyntax](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


