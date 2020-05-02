---
ms.assetid: fb95c8ee-a418-4520-a12a-7754ae947c3c
title: "\"F\"-Analyse Punkt"
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 05c203ef610dda0443ddc845245a4072e617f7a6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725436"
---
# <a name="fsutil-reparsepoint"></a>"F"-Analyse Punkt
> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7, Windows 2008, Windows Vista

Fragt Analyse Punkte ab oder löscht sie.  Der Befehl " **bsutil-Analyse Punkt** " wird in der Regel von Supportmitarbeitern verwendet.



## <a name="syntax"></a>Syntax

```
fsutil reparsepoint [query] <FileName>
fsutil reparsepoint [delete] <FileName>
```

### <a name="parameters"></a>Parameter

| Parameter  |                                                                BESCHREIBUNG                                                                |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------|
|   Abfrage    |            Ruft die Analyse Punktdaten ab, die der Datei oder dem Verzeichnis zugeordnet sind, die durch das angegebene Handle identifiziert werden.             |
|   delete   | Löscht einen Analyse Punkt aus der durch das angegebene Handle identifizierten Datei oder dem Verzeichnis, löscht jedoch weder die Datei noch das Verzeichnis. |
| <FileName> |             Gibt den vollständigen Pfad zur Datei einschließlich des Datei namens und der Erweiterung an, z. b. "c:\documents\dateiname.txt".             |

## <a name="remarks"></a>Bemerkungen

-   Analyse Punkte sind NTFS-Dateisystem Objekte, die über ein definierbares Attribut verfügen, das benutzerdefinierte Daten enthält. Sie werden verwendet, um die Funktionalität des e/a-Subsystems (Input/Output, e/a) zu erweitern.

-   Analyse Punkte werden für Verzeichnis Verknüpfungs Punkte und volumeeinstellungspunkte verwendet. Sie werden auch von Dateisystem Filter-Treibern verwendet, um bestimmte Dateien als spezielle Dateien für diesen Treiber zu markieren.

-   Wenn von einem Programm ein Analyse Punkt festgelegt wird, werden diese Daten einschließlich eines Analyse Tags gespeichert, mit dem die Daten, die gespeichert werden, eindeutig identifiziert werden. Wenn das Dateisystem eine Datei mit einem Analyse Punkt öffnet, wird versucht, den zugeordneten Dateisystem Filter zu finden. Wenn der Dateisystem Filter gefunden wird, verarbeitet der Filter die Datei gemäß den Analysedaten. Wenn kein Dateisystem Filter gefunden wird, schlägt der Datei Öffnungsvorgang fehl.

## <a name="examples"></a><a name="BKMK_examples"></a>Beispiele
Zum Abrufen von Analyse Punktdaten, die c:\Server zugeordnet sind, geben Sie Folgendes ein:

```
fsutil reparsepoint query c:\server
```

Verwenden Sie das folgende Format, um einen Analyse Punkt aus einer angegebenen Datei oder einem angegebenen Verzeichnis zu löschen:

```
fsutil reparsepoint delete c:\server
```

## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Fsutil](Fsutil.md)


