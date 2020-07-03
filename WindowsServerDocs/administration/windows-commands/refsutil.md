---
title: Ref
description: Referenz Artikel für das refsutil-Tool, das versucht, stark beschädigte Refs-Volumes zu diagnostizieren, verbleibende Dateien zu identifizieren und diese Dateien auf ein anderes Volume zu kopieren.
author: laknight5
ms.author: laknight
ms.date: 6/29/2020
ms.prod: windows-server
ms.technology: storage-file-systems
ms.topic: article
ms.openlocfilehash: c84aaed5b34c535221247dcdd6ab0a5462fd4aad
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931102"
---
# <a name="refsutil"></a>Ref

>Gilt für: Windows Server 2019, Windows 10

Refsutil ist ein Tool, das in Windows und Windows Server enthalten ist und versucht, stark beschädigte Refs-Volumes zu diagnostizieren, verbleibende Dateien zu identifizieren und diese Dateien auf ein anderes Volume zu kopieren. Dies erfolgt in Windows 10 im `%SystemRoot%\Windows\System32` Ordner oder unter Windows Server im `%SystemRoot%\\System32` Ordner.

Refs-Rettung ist die primäre Funktion von ref und eignet sich für die Wiederherstellung von Daten von Volumes, die in der Datenträgerverwaltung als Rohdaten angezeigt werden. Refs-Rettung besteht aus zwei Phasen: Scan Phase und Kopier Phase. Im automatischen Modus werden die Scan Phase und die Kopier Phase nacheinander ausgeführt. Im manuellen Modus kann jede Phase separat ausgeführt werden. Der Fortschritt und die Protokolle werden in einem Arbeitsverzeichnis gespeichert, sodass Phasen separat ausgeführt werden können und die Überprüfungs Phase angehalten und fortgesetzt werden kann. Sie sollten das Tool refsutil nicht verwenden, es sei denn, das Volume ist RAW. Wenn Sie schreibgeschützt sind, können Sie weiterhin auf die Daten zugreifen.

## <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
|--|--|
| `<source volume>` | Gibt das zu verarbeitende Refs-Volume an. Der Laufwerk Buchstabe muss als "L:" formatiert sein, oder Sie müssen einen Pfad zum volumeeinstellungspunkt angeben. |
| `<working directory>` | Gibt den Speicherort an, an dem temporäre Informationen und Protokolle gespeichert werden. Er darf sich **nicht** im befinden `<source volume>` . |
| `<target directory>` | Gibt den Speicherort an, in den identifizierte Dateien kopiert werden. Er darf sich **nicht** im befinden `<source volume>` . |
| \- Min. | Stellt alle möglichen Dateien einschließlich gelöschter Dateien wieder her.<p>**Warnung:** Dieser Parameter bewirkt nicht nur, dass die Ausführung des Prozesses länger dauert, sondern auch zu unerwarteten Ergebnissen führen kann. |
| \-Ramelow | Gibt an, dass der ausführliche Modus verwendet werden soll. |
| \-Stuben | Erzwingt, dass das Volume bei Bedarf zuerst entfernt wird. Alle geöffneten Handles für das Volume sind dann ungültig. Beispiel: `refsutil salvage -QA R: N:\\WORKING N:\\DATA -x`. |

## <a name="usage-and-available-options"></a>Verwendungs-und verfügbare Optionen

### <a name="quick-automatic-mode-command-line-usage"></a>Befehlszeilen Verwendung im schnellen automatischen Modus

Führt eine schnell Scan Phase gefolgt von einer Kopier Phase aus. Dieser Modus wird schneller ausgeführt, da davon ausgegangen wird, dass einige kritische Strukturen des Volumes nicht beschädigt sind und es daher nicht erforderlich ist, das gesamte Volume zu scannen, um Sie zu finden. Dadurch wird auch die Wiederherstellung veralteter Dateien/Verzeichnisse/Volumes reduziert.

```
refsutil salvage -QA <source volume> <working directory> <target directory> <options>
```

### <a name="full-automatic-mode-command-line-usage"></a>Vollständige automatische Modus-Befehlszeilen Verwendung

Führt eine vollständige Überprüfungsphase gefolgt von einer Kopier Phase aus. Dieser Modus kann einige Zeit in Anspruch nehmen, da er das gesamte Volume auf wiederherstellbare Dateien/Verzeichnisse/Volumes überprüfen wird.

```
refsutil salvage -FA <source volume> <working directory> <target directory> <options>
```

### <a name="diagnose-phase-command-line-usage-manual-mode"></a>Diagnose Phase Befehlszeilen Verwendung (manueller Modus)

Versuchen Sie zunächst, festzustellen, ob `<source volume>` ein Refs-Volume ist, und bestimmen Sie, ob das Volume bereitgestellt werden kann. Wenn ein Volume nicht verfügbar ist, werden die Gründe bereitgestellt. Dabei handelt es sich um eine eigenständige Phase.

```
refsutil salvage -D <source volume> <working directory> <options>
```

### <a name="quick-scan-phase-command-line-usage"></a>Befehlszeilen Verwendung in der schnell Scan Phase

Führt eine schnell Überprüfung der `<source volume>` für alle wiederherstellbaren Dateien durch. Dieser Modus wird schneller ausgeführt, da davon ausgegangen wird, dass einige kritische Strukturen des Volumes nicht beschädigt sind und es daher nicht erforderlich ist, das gesamte Volume zu scannen, um Sie zu finden. Dadurch wird auch die Wiederherstellung veralteter Dateien/Verzeichnisse/Volumes reduziert. Ermittelte Dateien werden in der `foundfiles.<volume signature>.txt` Datei protokolliert, die sich in Ihrem befindet `<working directory>` . Wenn die Überprüfungs Phase zuvor beendet wurde, wird die Überprüfung von an der Stelle fortgesetzt, **an der Sie** aufgehört hat.

```
refsutil salvage -QS <source volume> <working directory> <options>
```

### <a name="full-scan-phase-command-line-usage"></a>Befehlszeilen Verwendung in der vollständigen Scan Phase

Scannt den gesamten `<source volume>` auf wiederherstellbare Dateien. Dieser Modus kann einige Zeit in Anspruch nehmen, da er das gesamte Volume auf wiederherstellbare Dateien überprüft. Ermittelte Dateien werden `foundfiles.<volume signature>.txt` in der Datei protokolliert, die sich in Ihrem befindet `<working directory>` . Wenn die Überprüfungs Phase zuvor beendet wurde, wird die Überprüfung von an der Stelle fortgesetzt, **an der Sie** aufgehört hat.

```
refsutil salvage -FS <source volume> <working directory> <options>
```

### <a name="copy-phase-command-line-usage"></a>Befehlszeilen Verwendung in der Kopier Phase

Kopiert alle Dateien, die in der-Datei beschrieben werden `foundfiles.<volume signature>.txt` , in Ihre `<target directory>` . Wenn Sie die Überprüfungs Phase zu frühzeitig abbrechen, ist es möglich, dass die `foundfiles.<volume signature>.txt` Datei noch nicht vorhanden ist, sodass keine Datei in die kopiert wird `<target directory>` .

```
refsutil salvage -C <source volume> <working directory> <target directory> <options>
```

### <a name="copy-phase-with-list-command-line-usage"></a>Kopier Phase mit Listen Befehlszeilenverwendung

Kopiert alle Dateien in der `<file list>` aus der `<source volume>` in die `<target directory>` . Die Dateien in der `<file list>` müssen zuerst von der Überprüfungs Phase identifiziert werden, obwohl die Überprüfung nicht bis zum Abschluss ausgeführt werden muss. `<file list>`Kann generiert werden `foundfiles.<volume signature>.txt` , indem in eine neue Datei kopiert wird, Zeilen, die auf Dateien verweisen, die nicht wieder hergestellt werden sollen, entfernt werden und Dateien beibehalten werden, die wieder hergestellt werden sollen. Das PowerShell-Cmdlet **Select-String** kann bei der Filterung hilfreich sein, `foundfiles.<volume signature>.txt` um nur gewünschte Pfade, Erweiterungen oder Dateinamen einzuschließen.

```
refsutil salvage -SL <source volume> <working directory> <target directory> <file list> <options>
```

### <a name="copy-phase-with-interactive-console"></a>Kopier Phase mit interaktiver Konsole

Fortgeschrittene Benutzer können Dateien mithilfe einer interaktiven Konsole retten. Dieser Modus erfordert auch Dateien, die aus einer der Scan Phasen generiert werden.

```
refsutil salvage -IC <source volume> <working directory> <options>
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
