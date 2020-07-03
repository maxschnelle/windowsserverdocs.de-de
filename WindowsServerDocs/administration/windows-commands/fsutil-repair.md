---
title: fsutil repair
description: Referenz Artikel für den Befehl "sasutil Repair", der Selbstreparatur Vorgänge für NTFS verwaltet und überwacht.
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: 62d77150-1d9e-4069-ab4a-299f33024912
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 700e1f713d503565321ab29f5384d74382c64f21
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931207"
---
# <a name="fsutil-repair"></a>fsutil repair

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

Verwaltet und überwacht die Selbstreparatur Vorgänge von NTFS. Die Selbstreparatur von NTFS versucht, die Beschädigungen des NTFS-Dateisystems online zu korrigieren, ohne dass **Chkdsk.exe** ausgeführt werden müssen. Weitere Informationen finden Sie unter [Selbstreparatur von NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10)).

## <a name="syntax"></a>Syntax

```
fsutil repair [enumerate] <volumepath> [<logname>]
fsutil repair [initiate] <volumepath> <filereference>
fsutil repair [query] <volumepath>
fsutil repair [set] <volumepath> <flags>
fsutil repair [wait][<waittype>] <volumepath>

```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auflisten | Listet die entids des Beschädigungs Protokolls eines Volumes auf. |
| `<logname>` | Kann sein `$corrupt` , der Satz bestätigter Beschädigungen im Volume oder `$verify` , eine Reihe potenzieller, nicht überprüfter Beschädigungen im Volume. |
| setzen | Initiiert die Selbstreparatur von NTFS. |
| `<filereference>` | Gibt die NTFS-volumespezifische Datei-ID (Datei Verweis Nummer) an. Der Datei Verweis enthält die Segment Nummer der Datei. |
| Abfrage | Fragt den selbst reparierenden Zustand des NTFS-Volumes ab. |
| set | Legt den Selbstheilungs Zustand des Volumes fest. |
| `<flags>` | Gibt die zu verwendende Reparaturmethode an, wenn der Selbstreparatur Zustand des Volumes festgelegt wird.<p>Dieser Parameter kann auf drei Werte festgelegt werden:<ul><li>**0x01** : ermöglicht die allgemeine Reparatur.</li><li>**0x09** : warnt vor einem möglichen Datenverlust ohne Reparatur.</li><li>**0x00** : deaktiviert die Reparatur Vorgänge für die Selbstreparatur von NTFS.</li></ul> |
| state | Fragt den Beschädigungs Status des Systems oder für ein bestimmtes Volume ab. |
| wait | Wartet auf den Abschluss der Reparatur (en). Wenn NTFS auf einem Volume, auf dem es repariert wird, ein Problem festgestellt hat, kann mit dieser Option gewartet werden, bis die Reparatur abgeschlossen ist, bevor ausstehende Skripts ausgeführt werden. |
| `[waittype {0|1}]` | Gibt an, ob auf den Abschluss der aktuellen Reparatur gewartet werden soll oder ob auf den Abschluss aller Reparaturen gewartet werden soll. Der *waittype* -Parameter kann auf die folgenden Werte festgelegt werden:<ul><li>**0** -wartet auf den Abschluss aller Reparaturen. (Standardwert)</li><li>**1** : wartet auf den Abschluss der aktuellen Reparatur.</li></ul> |

### <a name="examples"></a>Beispiele

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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [fsutil](fsutil.md)

- [Selbstreparatur von NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10))
