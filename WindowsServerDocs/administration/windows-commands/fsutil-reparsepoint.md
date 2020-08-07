---
title: fsutil reparsepoint
description: Referenz Artikel für den Befehl "bsutil-Analyse Punkt", der Analyse Punkte abfragt oder löscht.
manager: dmoss
ms.author: toklima
author: toklima
ms.assetid: fb95c8ee-a418-4520-a12a-7754ae947c3c
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: b7742b7bb970394f0ef8602ae5c862c2ff9a1a41
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889881"
---
# <a name="fsutil-reparsepoint"></a>fsutil reparsepoint

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

Fragt Analyse Punkte ab oder löscht sie.  Der Befehl " **bsutil-Analyse Punkt** " wird in der Regel von Supportmitarbeitern verwendet.

Analyse Punkte sind NTFS-Dateisystem Objekte, die über ein definierbares Attribut verfügen, das benutzerdefinierte Daten enthält. Sie werden für Folgendes verwendet:

- Erweitern Sie die Funktionalität im e/a-Subsystem (Input/Output).

- Als Verzeichnis Verknüpfungs Punkte und volumeeinstellungspunkte fungieren.

- Markieren Sie bestimmte Dateien als spezielle Dateien für einen Dateisystem Filter-Treiber.

## <a name="syntax"></a>Syntax

```
fsutil reparsepoint [query] <filename>
fsutil reparsepoint [delete] <filename>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Abfrage | Ruft die Analyse Punktdaten ab, die der Datei oder dem Verzeichnis zugeordnet sind, die durch das angegebene Handle identifiziert werden. |
| delete | Löscht einen Analyse Punkt aus der durch das angegebene Handle identifizierten Datei oder dem Verzeichnis, löscht jedoch weder die Datei noch das Verzeichnis. |
| `<filename>` | Gibt den vollständigen Pfad zur Datei einschließlich des Datei namens und der Erweiterung an, z. b. *C:\documents\filename.txt*. |

#### <a name="remarks"></a>Bemerkungen

- Wenn von einem Programm ein Analyse Punkt festgelegt wird, werden diese Daten einschließlich eines Analyse Tags gespeichert, mit dem die Daten, die gespeichert werden, eindeutig identifiziert werden. Wenn das Dateisystem eine Datei mit einem Analyse Punkt öffnet, wird versucht, den zugeordneten Dateisystem Filter zu finden. Wenn der Dateisystem Filter gefunden wird, verarbeitet der Filter die Datei gemäß den Analysedaten. Wenn kein Dateisystem Filter gefunden wird, schlägt der **Datei Öffnungs** Vorgang fehl.

### <a name="examples"></a>Beispiele

Zum Abrufen von Analyse Punktdaten, die *c:\Server*zugeordnet sind, geben Sie Folgendes ein:

```
fsutil reparsepoint query c:\server
```

Verwenden Sie das folgende Format, um einen Analyse Punkt aus einer angegebenen Datei oder einem angegebenen Verzeichnis zu löschen:

```
fsutil reparsepoint delete c:\server
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [fsutil](fsutil.md)
