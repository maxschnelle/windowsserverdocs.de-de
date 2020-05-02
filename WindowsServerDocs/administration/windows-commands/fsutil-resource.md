---
ms.assetid: b198d8ca-a5b7-430f-8911-5cbb9f50484c
title: Ressource "f"
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 678f3f98a96f44c146b73e9b6081884f8547373c
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725442"
---
# <a name="fsutil-resource"></a>Ressource "f"
> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7, Windows 2008, Windows Vista

Erstellt eine sekundäre Transaktions Ressourcen-Manager, startet oder beendet eine transaktionale Ressourcen-Manager oder zeigt Informationen zu einem transaktionalen Ressourcen-Manager an und ändert das folgende Verhalten:

-   Gibt an, ob eine transaktionale Standard Ressourcen-Manager beim nächsten einbinden die Transaktions Metadaten bereinigen wird.

-   Die angegebene Transaktions Ressourcen-Manager, um die Konsistenz gegenüber der Verfügbarkeit zu bevorzugen.

-   Die angegebene Transaktions Ressourcen-Manager, um die Verfügbarkeit gegenüber Konsistenz zu bevorzugen.

-   Die Merkmale einer laufenden transaktionalen Ressourcen-Manager

## <a name="syntax"></a>Syntax

```
fsutil resource [create] <RmRootPathname>
fsutil resource [info] <RmRootPathname>
fsutil resource [setautoreset] {true|false} <DefaultRmRootPathname>
fsutil resource [setavailable] <RmRootPathname>
fsutil resource [setconsistent] <RmRootPathname>
fsutil resource [setlog] [growth {<Containers> containers|<Percent> percent} <RmRootPathname>] [maxextents <Containers> <RmRootPathname>] [minextents <Containers> <RmRootPathname>] [mode {full|undo} <RmRootPathname>] [rename <RmRootPathname>] [shrink <percent> <RmRootPathname>] [size <Containers> <RmRootPathname>]
fsutil resource [start] <RmRootPathname> [<RmLogPathname> <TmLogPathname>
fsutil resource [stop] <RmRootPathname>
```

#### <a name="parameters"></a>Parameter

|        Parameter        |                                                                                                                                                                                                                                        BESCHREIBUNG                                                                                                                                                                                                                                         |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         create          |                                                                                                                                                                                                                    Erstellt eine sekundäre Transaktions Ressourcen-Manager.                                                                                                                                                                                                                     |
|    <RmRootPathname>     |                                                                                                                                                                                                        Gibt den vollständigen Pfad zu einem transaktionalen Ressourcen-Manager Stammverzeichnis an.                                                                                                                                                                                                         |
|          info           |                                                                                                                                                                                                            Zeigt die Informationen des angegebenen Transaktions Ressourcen-Manager an.                                                                                                                                                                                                            |
|      "abtautor"       | Gibt an, ob eine transaktionale Standard Ressourcen-Manager die Transaktions Metadaten bei der nächsten Auflistung bereinigt.<p>-Legen Sie den **Setautoreset** -Parameter auf " **true** " fest, um anzugeben, dass die Transaktions Ressourcen-Manager standardmäßig die transaktionalen Metadaten beim nächsten einbinden bereinigen werden.<br />-Legen Sie den **Setautoreset** -Parameter auf " **false** " fest, um anzugeben, dass die Transaktions Ressourcen-Manager die transaktionalen Metadaten beim nächsten einbinden standardmäßig nicht bereinigen werden. |
| <DefaultRmRootPathname> |                                                                                                                                                                                                                       Gibt den Namen des Laufwerks gefolgt von einem Doppelpunkt an.                                                                                                                                                                                                                        |
|      "einstellbare"       |                                                                                                                                                                                                 Gibt an, dass eine transaktionale Ressourcen-Manager die Verfügbarkeit gegenüber Konsistenz bevorzugt.                                                                                                                                                                                                 |
|      setkonsistent      |                                                                                                                                                                                                 Gibt an, dass eine transaktionale Ressourcen-Manager die Konsistenz gegenüber der Verfügbarkeit bevorzugen.                                                                                                                                                                                                 |
|         Setlog          |                                                                                                                                                                                                  Ändert die Eigenschaften eines transaktionalen Ressourcen-Manager, der bereits ausgeführt wird.                                                                                                                                                                                                  |
|         growth          |                                                                                                  Gibt den Betrag an, um den die transaktionale Ressourcen-Manager Protokoll vergrößert werden kann.<p>Der Parameter "Growth" kann wie folgt angegeben werden:<p>-Anzahl der Container mit dem folgenden Format: _Container_**Container**<br />-**Prozentsatz** mit dem Format: _Prozent_Satz                                                                                                   |
|      <containers>       |                                                                                                                                                                                                      Gibt die Datenobjekte an, die vom transaktionalen Ressourcen-Manager verwendet werden.                                                                                                                                                                                                       |
|        maxblock        |                                                                                                                                                                                                Gibt die maximale Anzahl von Containern für die angegebene Transaktions Ressourcen-Manager an.                                                                                                                                                                                                |
|        minblock        |                                                                                                                                                                                                Gibt die Mindestanzahl von Containern für die angegebene Transaktions Ressourcen-Manager an.                                                                                                                                                                                                |
|  Modus {full&#124;rückgängig}  |                                                                                                                                                                                        Gibt an, ob alle Transaktionen protokolliert ( **Full**) oder nur Rollback-Ereignisse protokolliert (**Rückgängig**) werden.                                                                                                                                                                                         |
|         rename          |                                                                                                                                                                                                                  Ändert die GUID für die transaktionale Ressourcen-Manager.                                                                                                                                                                                                                  |
|         shrink          |                                                                                                                                                                                              Gibt den Prozentsatz an, um den sich das Transaktions Ressourcen-Manager Protokoll automatisch verringern kann.                                                                                                                                                                                              |
|          size           |                                                                                                                                                                                              Gibt die Größe des transaktionalen Ressourcen-Manager als angegebene Anzahl von *Containern*an.                                                                                                                                                                                               |
|          start          |                                                                                                                                                                                                                    Startet das angegebene Transaktions Ressourcen-Manager.                                                                                                                                                                                                                    |
|          stop           |                                                                                                                                                                                                                    Beendet den angegebenen transaktionalen Ressourcen-Manager.                                                                                                                                                                                                                     |

### <a name="examples"></a><a name="BKMK_examples"></a>Beispiele
Geben Sie Folgendes ein, um das Protokoll für die durch c:\test angegebene Transaktions Ressourcen-Manager festzulegen, um eine automatische Vergrößerung von fünf Containern zu erhalten:

```
fsutil resource setlog growth 5 containers c:test
```

Geben Sie Folgendes ein, um das Protokoll für die durch c:\test angegebene Transaktions Ressourcen-Manager festzulegen, um eine automatische Vergrößerung von zwei Prozent zu haben:

```
fsutil resource setlog growth 2 percent c:test
```

Geben Sie Folgendes ein, um anzugeben, dass die Transaktions Metadaten beim nächsten einbinden auf Laufwerk C durch die standardmäßige transaktionale Ressourcen-Manager bereinigt werden:

```
fsutil resource setautoreset true c:\  
```

### <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Fsutil](Fsutil.md)

[Transaktions-NTFS](https://go.microsoft.com/fwlink/?LinkID=165402)


