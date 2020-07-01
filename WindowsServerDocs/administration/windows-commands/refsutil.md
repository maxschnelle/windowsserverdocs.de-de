---
title: Ref
description: Refsutil ist ein Tool, das in Windows und Windows Server enthalten ist und versucht, stark beschädigte Refs-Volumes zu diagnostizieren, verbleibende Dateien zu identifizieren und diese Dateien auf ein anderes Volume zu kopieren.
author: laknight5
ms.author: laknight
ms.date: 6/29/2020
ms.prod: windows-server
ms.technology: storage-file-systems
ms.topic: article
ms.openlocfilehash: 0d7c1bf79695c2ddd03943744ebf1df4827d365c
ms.sourcegitcommit: 457e88e5aa6be13a2bffdb8e434a8efc3698678f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/30/2020
ms.locfileid: "85549151"
---
# <a name="refsutil"></a>Ref

>Gilt für: Windows Server 2019, Windows 10

Refsutil ist ein Tool, das in Windows und Windows Server enthalten ist und versucht, stark beschädigte Refs-Volumes zu diagnostizieren, verbleibende Dateien zu identifizieren und diese Dateien auf ein anderes Volume zu kopieren. Dies erfolgt in Windows 10 im Ordner "%SystemRoot%\Windows\System32" oder im Ordner "% SystemRoot% System32" in Windows Server \\ .

Refs-Rettung ist derzeit die primäre Funktion von relsutil und eignet sich für die Wiederherstellung von Daten von Volumes, die in der Datenträgerverwaltung als Rohdaten angezeigt werden. Refs-Rettung besteht aus zwei Phasen: Scan Phase und Kopier Phase. Im automatischen Modus werden die Scan Phase und die Kopier Phase nacheinander ausgeführt. Im manuellen Modus kann jede Phase separat ausgeführt werden. Der Fortschritt und die Protokolle werden in einem Arbeitsverzeichnis gespeichert, sodass Phasen separat ausgeführt werden können und die Überprüfungs Phase angehalten und fortgesetzt werden kann. Refsutil muss nicht verwendet werden, es sei denn, das Volume ist RAW. Wenn Sie schreibgeschützt sind, können Sie weiterhin auf die Daten zugreifen.

## <a name="automatic-mode-command-line-usage"></a>Befehlszeilen Verwendung im automatischen Modus

### <a name="quick-automatic-mode-command-line-usage"></a>Befehlszeilen Verwendung im schnellen automatischen Modus

```dos
refsutil salvage -QA <source volume> <working directory> <target directory> <options>
```
Es wird eine schnell Scan Phase gefolgt von einer Kopier Phase ausgeführt. Dieser Modus wird schneller ausgeführt, da davon ausgegangen wird, dass einige kritische Strukturen des Volumes nicht beschädigt sind. Daher ist es nicht erforderlich, das gesamte Volume zu scannen, um Sie zu finden. Dadurch wird auch die Wiederherstellung veralteter Dateien/Verzeichnisse/Volumes reduziert.

### <a name="full-automatic-mode-command-line-usage"></a>Vollständige automatische Modus-Befehlszeilen Verwendung

```dos
refsutil salvage -FA <source volume> <working directory> <target directory> <options>
```

Sie führt eine vollständige Überprüfungsphase gefolgt von einer Kopier Phase aus. Dieser Modus kann einige Zeit in Anspruch nehmen, da er das gesamte Volume auf wiederherstellbare Dateien/Verzeichnisse/Volumes überprüfen wird.

## <a name="manual-mode-command-line-usage"></a>Befehlszeilen Verwendung im manuellen Modus

### <a name="diagnose-phase-command-line-usage"></a>Befehlszeilen Verwendung in der Diagnose Phase

```dos
refsutil salvage -D <source volume> <working directory> <options>
```

Versuchen Sie zunächst, festzustellen, ob \<source volume\> ein Refs-Volume ist, und bestimmen Sie, ob das Volume bereitgestellt werden kann. Wenn ein Volume nicht verwendet werden kann, werden die Ursache (n) ermittelt. Dabei handelt es sich um eine eigenständige Phase.

### <a name="quick-scan-phase-command-line-usage"></a>Befehlszeilen Verwendung in der schnell Scan Phase

```dos
refsutil salvage -QS <source volume> <working directory> <options>
```

Schnell Überprüfung \<source volume\> für alle wiederherstellbaren Dateien. Dieser Modus wird schneller ausgeführt, da davon ausgegangen wird, dass einige kritische Strukturen des Volumes nicht beschädigt sind. Daher ist es nicht erforderlich, das gesamte Volume zu scannen, um Sie zu finden. Dadurch wird auch die Wiederherstellung veralteter Dateien/Verzeichnisse/Volumes reduziert. Ermittelte Dateien werden in "FoundFiles..." protokolliert. \<volume signature\> txt "unter \<working directory\> . Wenn die Überprüfungs Phase zuvor beendet wurde, wird die Überprüfung bei erneuter Ausführung mit dem-QS-Flag fortgesetzt.

### <a name="full-scan-phase-command-line-usage"></a>Befehlszeilen Verwendung in der vollständigen Scan Phase

```dos
refsutil salvage -FS <source volume> <working directory> <options>
```

Alle wieder \<source volume\> herstellbaren Dateien überprüfen. Dieser Modus kann einige Zeit in Anspruch nehmen, da er das gesamte Volume auf wiederherstellbare Dateien überprüft.
Ermittelte Dateien werden in "FoundFiles..." protokolliert. \<volume signature\> txt "unter \<working directory\> . Wenn die Überprüfungs Phase zuvor beendet wurde, wird die Überprüfung bei der erneuten Ausführung mit dem-FS-Flag fortgesetzt.

### <a name="copy-phase-command-line-usage"></a>Befehlszeilen Verwendung in der Kopier Phase

```dos
refsutil salvage -C <source volume> <working directory> <target directory>
<options>
```

Kopieren Sie alle Dateien, die unter "Grund Dateien." beschrieben werden \<volume signature\> . txt "in \<target
directory\> . Wenn die Überprüfungs Phase zu früh beendet wird, "FoundFiles \<volume
signature\> . die txt-Datei wurde möglicherweise noch nicht geschrieben, sodass keine Datei in kopiert wird \<target directory\> .

### <a name="copy-phase-with-list-command-line-usage"></a>Kopier Phase mit Listen Befehlszeilenverwendung

```dos
refsutil salvage -SL <source volume> <working directory> <target
directory> <file list> <options>
```

Kopieren Sie alle Dateien in \<file list\> von \<source volume\> nach \<target
directory\> . Die Dateien in \<file list\> müssen zuerst von der Überprüfungs Phase identifiziert werden, obwohl die Überprüfung nicht vollständig ausgeführt werden muss. \<file list\>kann generiert werden, indem "FoundFiles. \<volume signature\> " kopiert wird. txt "in eine neue Datei, Entfernen von Zeilen, die auf Dateien verweisen, die nicht wieder hergestellt werden sollen, und beibehalten von Dateien, die wieder hergestellt werden sollen. Das PowerShell-Cmdlet Select-String ist möglicherweise hilfreich beim Filtern von grundlegenden \<volume signature\> Dateien. txt ", um nur gewünschte Pfade, Erweiterungen oder Dateinamen einzuschließen.

### <a name="copy-phase-with-interactive-console"></a>Kopier Phase mit interaktiver Konsole

```dos
refsutil salvage -IC <source volume> <working directory> <options>
```

Retten Sie Dateien in einer interaktiven Konsole für fortgeschrittene Benutzer. Dieser Modus erfordert auch Dateien, die aus einer der Scan Phasen generiert werden.

## <a name="parameters"></a>Parameter

| Parameter             | BESCHREIBUNG                                                                     |
| --------------------- | --------------------------------------------------------------------------------------- |
| \<source volume\>     | Zu verarbeitende Refs-Volume. Laufwerk Buchstabe im Format "L:" oder ein Pfad zum volumeeinstellungspunkt.           |
| \<working directory\> | Speicherort zum Speichern von temporären Informationen und Protokollen. Er darf sich **nicht** unter befinden \<source volume\> .  |
| \<target directory\>  | Der Speicherort, in den identifizierte Dateien kopiert werden. Er darf sich **nicht** unter befinden \<source volume\> . |
| \- Min.         | Stellen Sie alle möglichen Dateien einschließlich gelöschter Dateien wieder her. Diese Option wird bei Ref-Rettung v1 ignoriert. Warnung: nicht nur die Ausführung dieses Zeitraums dauert länger, es kann zu unerwartetem Ergebnis führen. |
| \-Ramelow         | Verbose-Modus                                                                                           |
| \-Stuben         | Erzwingen Sie, dass das Volume bei Bedarf zuerst entfernt wird. Alle geöffneten Handles für das Volume wären dann ungültig. Beispiel: ref-"retten-QA R: n: \\ Working N: \\ Data-x"                                  |
