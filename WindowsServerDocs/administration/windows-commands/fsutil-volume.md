---
title: fsutil volume
description: Referenz Artikel für den Befehl fsutil Volume, bei dem ein Volume getrennt wird, oder zum Abfragen des Festplatten Laufwerks, um zu bestimmen, wie viel freier Speicherplatz auf dem Festplattenlaufwerk aktuell verfügbar ist oder welche Datei einen bestimmten Cluster verwendet.
manager: dmoss
ms.author: toklima
author: toklima
ms.assetid: 0397c204-b3f8-4fd8-b71d-b7efb117766d
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: b6bcd763643eba8c82fbd1ebd82199aa46f8f0dd
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889756"
---
# <a name="fsutil-volume"></a>fsutil volume

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

Hebt die Bereitstellung eines Volumes auf oder fragt das Festplattenlaufwerk ab, um zu bestimmen, wie viel freier Speicherplatz auf dem Festplattenlaufwerk aktuell verfügbar ist oder welche Datei einen bestimmten Cluster verwendet.

## <a name="syntax"></a>Syntax

```
fsutil volume [allocationreport] <volumepath>
fsutil volume [diskfree] <volumepath>
fsutil volume [dismount] <volumepath>
fsutil volume [filelayout] <volumepath> <fileID>
fsutil volume [list]
fsutil volume [querycluster] <volumepath> <cluster> [<cluster>] … …
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Zuordnung von Berichten | Zeigt Informationen zur Verwendung von Speicher auf einem bestimmten Volume an. |
| `<volumepath>` | Gibt den Laufwerk Buchstaben (gefolgt von einem Doppelpunkt) an. |
| DiskFree | Fragt das Festplattenlaufwerk ab, um die Menge des freien Speicherplatzes zu bestimmen. |
| Aufheben der Bereitstellung | Hebt die Bereitstellung eines Volumes auf. |
| filelayout | Zeigt die NTFS-Metadaten für die angegebene Datei an. |
| `<fileID>` | Gibt die Datei-ID an. |
| list | Listet alle Volumes im System auf. |
| querycluster | Ermittelt, welche Datei einen angegebenen Cluster verwendet. Sie können mehrere Cluster mit dem **querycluster** -Parameter angeben. |
| `<cluster>` | Gibt die logische Cluster Nummer (LCN) an. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um einen zugeordneten Cluster Bericht anzuzeigen:

```
fsutil volume allocationreport C:
```

Um die Einbindung eines Volumes auf Laufwerk C aufzuheben, geben Sie Folgendes ein:

```
fsutil volume dismount c:
```

Geben Sie Folgendes ein, um die Menge des freien Speicherplatzes eines Volumes auf Laufwerk C abzufragen:

```
fsutil volume diskfree c:
```

Wenn Sie alle Informationen zu einer angegebenen Datei (en) anzeigen möchten, geben Sie Folgendes ein:

```
fsutil volume C: *
fsutil volume C:\Windows
fsutil volume C: 0x00040000000001bf
```

Geben Sie Folgendes ein, um die Volumes auf dem Datenträger aufzulisten:

```
fsutil volume list
```

Geben Sie Folgendes ein, um die Dateien zu finden, die die Cluster verwenden, die von den logischen Cluster Nummern 50 und 0x2000 angegeben werden, auf Laufwerk C:

```
fsutil volume querycluster C: 50 0x2000
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [fsutil](fsutil.md)

- [Funktionsweise von NTFS](/previous-versions/windows/it-pro/windows-server-2003/cc781134(v=ws.10))
