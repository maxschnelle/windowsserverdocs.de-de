---
ms.assetid: 62d77150-1d9e-4069-ab4a-299f33024912
title: Fsutil repair
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 18c06b1f426105b098a5dc7e992b1e3becd3a4ca
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59846681"
---
# <a name="fsutil-repair"></a>Fsutil repair
>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, WindowsServer 2012, Windows 8, Windows Server 2008 R2, Windows 7

Verwaltet und überwacht die Selbstreparatur Reparaturvorgänge NTFS.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
fsutil repair [enumerate] <volumepath> [<LogName>]
fsutil repair [initiate] <VolumePath> <FileReference>
fsutil repair [query] <VolumePath>
fsutil repair [set] <VolumePath> <Flags>
fsutil repair [wait][<WaitType>] <VolumePath>

```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------------|---------------|
|Auflisten|Listet die Eingaben des Volumes Beschädigung Protokolltyp an.|
|\<volumepath>|Gibt das Volume als den Namen des Laufwerks, gefolgt von einem Doppelpunkt an.|
|\<LogName>|$Beschädigt - die Gruppe von bestätigt Beschädigungen auf dem Volume.<br />Überprüfen von $ - eine Reihe von möglichen, nicht überprüfte Beschädigungen auf dem Volume.|
|Initiieren|Initiiert die NTFS-Selbstreparaturfunktion.|
|\<FileReference >|Gibt die NTFS-Volume-spezifische Datei-ID (Datei-Verweisnummer) an. Das Projekt enthält die Segment-Anzahl der Datei.|
|query|Fragt die Selbstreparatur Zustand des NTFS-Volumes.|
|set|Legt fest, die Selbstreparatur Status des Volumes.|
|\<Flags>|Gibt die reparieren-Methode, die beim Festlegen der Selbstreparatur Status des Volumes verwendet werden.<br /><br />Die **Flags** Parameter kann auf drei Werte festgelegt werden:<br /><br />-   **0x01**: Können allgemeine reparieren.<br />-   **0x09**: Warnt vor möglicherweise Daten verloren gehen, ohne Sie zu reparieren.<br />-   **0x00**: Deaktiviert die Selbstreparatur Reparaturvorgänge NTFS.|
|Status|Fragt den Status für eine Beschädigung des Systems oder für ein bestimmtes Volume ab.|
|Warte|Wartet ab. um abzuschließen. Wenn NTFS ein Problem auf einem Volume erkannt hat, auf dem Reparaturen ausgeführt wird, können Sie diese Option das System wartet, bis die Reparatur abgeschlossen ist, bevor sie alle ausstehenden Skripts ausgeführt wird.|
|[WaitType {0&#124;1}]|Gibt an, ob warten, bis die aktuelle Reparatur abgeschlossen oder warten, bis alle Reparaturen ausführen. *Wartetyp* kann auf die folgenden Werte festgelegt werden:<br /><br />-   **0**: Wartet, bis alle Reparaturen ausführen. (Standardwert)<br />-   **1**: Wartet auf die aktuelle Reparatur abgeschlossen.|

## <a name="remarks"></a>Hinweise

-   Selbst heilen NTFS um Beschädigungen der NTFS-Dateisystem online, ohne zu beheben versucht **Chkdsk.exe** ausgeführt werden. Dieses Feature wurde in Windows Server 2008 eingeführt. Weitere Informationen finden Sie unter [Self Dienstreparatur NTFS](https://go.microsoft.com/fwlink/?LinkID=165401).

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie zum Aufzählen der bestätigten Beschädigungen eines Volumes:

```
fsutil repair enumerate C: $Corrupt 
```

Um Selbstreparatur Reparatur auf Laufwerk C zu aktivieren, geben Sie Folgendes ein:

```
fsutil repair set c: 1
```

Um die Selbstreparatur Reparatur auf Laufwerk C zu deaktivieren, geben Sie Folgendes ein:

```
fsutil repair set c: 0
```

#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilensyntax](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

[Eine Selbstreparatur NTFS](https://go.microsoft.com/fwlink/?LinkID=165401)


