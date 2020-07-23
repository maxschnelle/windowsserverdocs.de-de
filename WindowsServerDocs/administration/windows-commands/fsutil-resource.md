---
title: fsutil resource
description: Referenz Artikel für den Ressourcen Befehl "f", der eine transaktionale Ressourcen-Manager und das zugehörige Verhalten verwaltet.
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: b198d8ca-a5b7-430f-8911-5cbb9f50484c
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: c0be84f00df2e0010f6c2a318f605532a3bc4d23
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86958182"
---
# <a name="fsutil-resource"></a>fsutil resource

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

Erstellt eine sekundäre Transaktions Ressourcen-Manager, startet oder beendet eine transaktionale Ressourcen-Manager oder zeigt Informationen zu einem transaktionalen Ressourcen-Manager an und ändert das folgende Verhalten:

- Gibt an, ob eine transaktionale Standard Ressourcen-Manager beim nächsten einbinden die transaktionalen Metadaten bereinigt.

- Die angegebene Transaktions Ressourcen-Manager, um die Konsistenz gegenüber der Verfügbarkeit zu bevorzugen.

- Die angegebene Transaktions Ressourcen-Manager, um die Verfügbarkeit gegenüber Konsistenz zu bevorzugen.

- Die Merkmale eines laufenden transaktionalen Ressourcen-Manager.

## <a name="syntax"></a>Syntax

```
fsutil resource [create] <rmrootpathname>
fsutil resource [info] <rmrootpathname>
fsutil resource [setautoreset] {true|false} <Defaultrmrootpathname>
fsutil resource [setavailable] <rmrootpathname>
fsutil resource [setconsistent] <rmrootpathname>
fsutil resource [setlog] [growth {<containers> containers|<percent> percent} <rmrootpathname>] [maxextents <containers> <rmrootpathname>] [minextents <containers> <rmrootpathname>] [mode {full|undo} <rmrootpathname>] [rename <rmrootpathname>] [shrink <percent> <rmrootpathname>] [size <containers> <rmrootpathname>]
fsutil resource [start] <rmrootpathname> [<rmlogpathname> <tmlogpathname>
fsutil resource [stop] <rmrootpathname>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| create | Erstellt eine sekundäre Transaktions Ressourcen-Manager. |
| `<rmrootpathname>` | Gibt den vollständigen Pfad zu einem transaktionalen Ressourcen-Manager Stammverzeichnis an. |
| info | Zeigt die Informationen des angegebenen Transaktions Ressourcen-Manager an. |
| "abtautor" | Gibt an, ob eine transaktionale Standard Ressourcen-Manager die Transaktions Metadaten bei der nächsten Auflistung bereinigt.<ul><li>**true** : gibt an, dass die Transaktions Ressourcen-Manager standardmäßig die Transaktions Metadaten beim nächsten einbinden bereinigen werden.</li><li>**false** : gibt an, dass der Transaktions Ressourcen-Manager die transaktionalen Metadaten beim nächsten einbinden standardmäßig nicht bereinigt. |
| `<defaultrmrootpathname>` | Gibt den Namen des Laufwerks gefolgt von einem Doppelpunkt an. |
| "einstellbare" | Gibt an, dass eine transaktionale Ressourcen-Manager die Verfügbarkeit gegenüber Konsistenz bevorzugt. |
| setkonsistent | Gibt an, dass eine transaktionale Ressourcen-Manager die Konsistenz gegenüber der Verfügbarkeit bevorzugen. |
| Setlog | Ändert die Eigenschaften eines transaktionalen Ressourcen-Manager, der bereits ausgeführt wird. |
| growth | Gibt den Betrag an, um den die transaktionale Ressourcen-Manager Protokoll vergrößert werden kann.<p>Der Parameter "Growth" kann wie folgt angegeben werden:<ul><li>Anzahl von Containern unter Verwendung des folgenden Formats:`<containers> containers`</li><li>Prozentsatz mit dem folgenden Format:`<percent> percent`</li></ul> |
| `<containers>` | Gibt die Datenobjekte an, die vom transaktionalen Ressourcen-Manager verwendet werden. |
| maxblock | Gibt die maximale Anzahl von Containern für die angegebene Transaktions Ressourcen-Manager an. |
| minblock | Gibt die Mindestanzahl von Containern für die angegebene Transaktions Ressourcen-Manager an. |
| Spar`{full|undo}` | Gibt an, ob alle Transaktionen protokolliert ( **Full**) oder nur Rollback-Ereignisse protokolliert (**Rückgängig**) werden. |
| rename | Ändert die GUID für die transaktionale Ressourcen-Manager. |
| shrink | Gibt den Prozentsatz an, um den sich das Transaktions Ressourcen-Manager Protokoll automatisch verringern kann. |
| size | Gibt die Größe des transaktionalen Ressourcen-Manager als angegebene Anzahl von *Containern*an. |
| start | Startet das angegebene Transaktions Ressourcen-Manager. |
| stop | Beendet den angegebenen transaktionalen Ressourcen-Manager. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um das Protokoll für die durch *c:\test*angegebene Transaktions Ressourcen-Manager festzulegen, um eine automatische Vergrößerung von fünf Containern zu erhalten:

```
fsutil resource setlog growth 5 containers c:test
```

Geben Sie Folgendes ein, um das Protokoll für die durch *c:\test*angegebene Transaktions Ressourcen-Manager festzulegen, um eine automatische Vergrößerung von zwei Prozent zu haben:

```
fsutil resource setlog growth 2 percent c:test
```

Geben Sie Folgendes ein, um anzugeben, dass die Transaktions Metadaten beim nächsten einbinden auf Laufwerk C durch die standardmäßige transaktionale Ressourcen-Manager bereinigt werden:

```
fsutil resource setautoreset true c:\
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [fsutil](fsutil.md)

- [Transaktions-NTFS](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc730726(v=ws.10))
