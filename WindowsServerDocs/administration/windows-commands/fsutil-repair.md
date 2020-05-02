---
ms.assetid: 62d77150-1d9e-4069-ab4a-299f33024912
title: Nicht reparieren
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 1a7931314f7064a62e45d2319e48d58162ab0e11
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725467"
---
# <a name="fsutil-repair"></a>Nicht reparieren
> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

Verwaltet und überwacht die Selbstreparatur Vorgänge von NTFS.



## <a name="syntax"></a>Syntax

```
fsutil repair [enumerate] <volumepath> [<LogName>]
fsutil repair [initiate] <VolumePath> <FileReference>
fsutil repair [query] <VolumePath>
fsutil repair [set] <VolumePath> <Flags>
fsutil repair [wait][<WaitType>] <VolumePath>

```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|-------------|---------------|
|Auflisten|Listet die entids des Beschädigungs Protokolls eines Volumes auf.|
|\<volumepath->|Gibt das Volume als den Namen des Laufwerks gefolgt von einem Doppelpunkt an.|
|\<LogName>|$Corrupt: der Satz bestätigter Beschädigungen auf dem Volume.<br />$Verify: ein Satz potenzieller, nicht überprüfter Beschädigungen auf dem Volume.|
|setzen|Initiiert die Selbstreparatur von NTFS.|
|\<> "filereferenzierung"|Gibt die NTFS-volumespezifische Datei-ID (Datei Verweis Nummer) an. Der Datei Verweis enthält die Segment Nummer der Datei.|
|Abfrage|Fragt den selbst reparierenden Zustand des NTFS-Volumes ab.|
|set|Legt den Selbstheilungs Zustand des Volumes fest.|
|\<Flags>|Gibt die zu verwendende Reparaturmethode an, wenn der Selbstreparatur Zustand des Volumes festgelegt wird.<p>Der **Flags** -Parameter kann auf drei Werte festgelegt werden:<p>-   **0x01**: ermöglicht die allgemeine Reparatur.<br />-   **0x09**: warnt vor einem möglichen Datenverlust ohne Reparatur.<br />-   **0x00**: deaktiviert die Reparatur Vorgänge für die Selbstreparatur von NTFS.|
|state|Fragt den Beschädigungs Status des Systems oder für ein bestimmtes Volume ab.|
|wait|Wartet auf den Abschluss der Reparatur (en). Wenn NTFS auf einem Volume, auf dem es repariert wird, ein Problem festgestellt hat, kann mit dieser Option gewartet werden, bis die Reparatur abgeschlossen ist, bevor ausstehende Skripts ausgeführt werden.|
|[Waittype {0&#124;1}]|Gibt an, ob auf den Abschluss der aktuellen Reparatur gewartet werden soll oder ob auf den Abschluss aller Reparaturen gewartet werden soll. " *Waittype* " kann auf die folgenden Werte festgelegt werden:<p>-   **0**: wartet auf den Abschluss aller Reparaturen.  (Standardwert)<br />-   **1**: wartet auf den Abschluss der aktuellen Reparatur.|

## <a name="remarks"></a>Bemerkungen

-   Die Selbstreparatur von NTFS versucht, die Beschädigungen des NTFS-Dateisystems online zu korrigieren, ohne dass " **Chkdsk. exe** " ausgeführt werden muss. Diese Funktion wurde in Windows Server 2008 eingeführt. Weitere Informationen finden Sie unter [Self-Healing-NTFS](https://go.microsoft.com/fwlink/?LinkID=165401).

## <a name="examples"></a><a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um die bestätigten Beschädigungen eines Volumes aufzuzählen:

```
fsutil repair enumerate C: $Corrupt 
```

Geben Sie Folgendes ein, um die Selbstreparatur auf Laufwerk C zu aktivieren:

```
fsutil repair set c: 1
```

Geben Sie Folgendes ein, um die Reparatur der Selbstreparatur auf Laufwerk C zu deaktivieren:

```
fsutil repair set c: 0
```

## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Fsutil](Fsutil.md)

[Selbstreparatur von NTFS](https://go.microsoft.com/fwlink/?LinkID=165401)


