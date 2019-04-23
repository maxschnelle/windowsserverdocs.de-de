---
ms.assetid: b198d8ca-a5b7-430f-8911-5cbb9f50484c
title: Fsutil-Ressource
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: b55063c3c5ea41b43573e6322b5efb36d2dad90e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828331"
---
# <a name="fsutil-resource"></a>Fsutil-Ressource
>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, WindowsServer 2012, Windows 8, Windows Server 2008 R2, Windows 7, Windows 2008, Windows Vista

Erstellt einen sekundären Transaktionsressourcen-Manager., startet oder beendet eine transaktionale Ressourcen-Manager, oder zeigt Informationen über eine transaktionale Ressource-Manager und ändert das folgende Verhalten:

-   Gibt an, ob eine standardmäßige Transaktionsressourcen-Manager seine transaktionale Metadaten an die nächste Bereitstellung bereinigt

-   Der angegebene transaktionale Ressourcen-Manager Konsistenz über Verfügbarkeit bevorzugen

-   Der angegebene Transaktionsressourcen-Manager auf Verfügbarkeit als die Konsistenz bevorzugt

-   Die Merkmale eines ausgeführten transaktionale Ressourcen-Managers

Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](#BKMK_examples) .

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

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------------|---------------|
|erstellen|Erstellt einen sekundären Transaktionsressourcen-Manager.|
|<RmRootPathname>|Gibt den vollständigen Pfad zu einem Transaktionsressourcen-Manager-Stammverzeichnis.|
|info|Werden der angegebene Transaktions-Manager-Informationen angezeigt.|
|setautoreset|Gibt an, ob es sich bei der Standardwert Transaktionsressourcen-Manager die transaktionale Metadaten in der nächsten Bereitstellung bereinigt.<br /><br />– Legen Sie die **Setautoreset** Parameter **"true"** um anzugeben, dass die Transaktionsressourcen-Manager wird standardmäßig die transaktionale Metadaten in der nächsten Bereitstellung, bereinigt.<br />– Legen Sie die **Setautoreset** Parameter **"false"** um anzugeben, dass die Transaktionsressourcen-Manager die transaktionale Metadaten in der nächsten Bereitstellung, wird standardmäßig nicht bereinigt.|
|<DefaultRmRootPathname>|Gibt den Namen des Laufwerks, gefolgt von einem Doppelpunkt an.|
|setavailable|Gibt an, dass ein Transaktionsressourcen-Manager. Verfügbarkeit als die Konsistenz bevorzugt wird.|
|setconsistent|Gibt an, dass ein Transaktionsressourcen-Manager. Konsistenz über Verfügbarkeit bevorzugen.|
|setlog|Ändert die Eigenschaften eines transaktionalen Ressourcen-Managers, die bereits ausgeführt wird.|
|Wachstum|Gibt die Menge, die mit der das Transaktionsressourcen-Manager-Protokoll vergrößert werden kann.<br /><br />Der Parameter Wachstum kann wie folgt angegeben werden:<br /><br />-Anzahl der Container, die mit dem Format: *Container ***Container**<br />- Prozentsatz, mit dem Format: *Prozent *** Prozent**|
|<containers>|Gibt an, die Datenobjekte, die vom Transaktions-Manager verwendet werden.|
|maxextent|Gibt die maximale Anzahl von Containern für den angegebenen Transaktions-Manager an.|
|minextent|Gibt die minimale Anzahl von Containern für den angegebenen Transaktions-Manager an.|
|Modus {vollständige&#124;rückgängig}|Gibt an, ob alle Transaktionen protokolliert werden ( **vollständige**) oder nur ein Rollback Ereignisse werden protokolliert (**Rückgängig**).|
|rename|Ändert die GUID für den Transaktions-Manager.|
|Verkleinern|Gibt an, die mit dem das Protokoll Transaktionsressourcen-Manager automatisch verringert werden kann.|
|size|Gibt die Größe des Transaktions-Managers als eine angegebene Anzahl von *Container*.|
|start|Wird der angegebene Transaktions-Manager gestartet.|
|stop|Der angegebene Transaktions-Manager wird beendet.|

### <a name="BKMK_examples"></a>Beispiele für
Geben Sie Folgendes ein, um das Protokoll für den Transaktions-Manager festzulegen, die durch c:\test, damit eine automatische Vergrößerung von fünf Containern angegeben wird:

```
fsutil resource setlog growth 5 containers c:test
```

Geben Sie Folgendes ein, um das Protokoll für den Transaktions-Manager festzulegen, die durch c:\test, damit eine automatische Vergrößerung von beiden angegeben wird:

```
fsutil resource setlog growth 2 percent c:test
```

Um anzugeben, dass der Standard-Transaktionsressourcen-Manager, die transaktionale Metadaten in der nächsten Bereitstellung auf Laufwerk C bereinigt, geben Sie Folgendes ein:

```
fsutil resource setautoreset true c:\  
```

### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilensyntax](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

[Transaktions-NTFS](https://go.microsoft.com/fwlink/?LinkID=165402)


