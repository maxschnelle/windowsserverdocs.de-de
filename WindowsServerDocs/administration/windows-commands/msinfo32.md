---
title: msinfo32
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a38f31d7-1766-4103-becc-9d0b87c2826d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a3de5088b64105e970fc38f55ecaf54382670549
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843461"
---
# <a name="msinfo32"></a>msinfo32

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Öffnet das Tool für Systeminformationen um einen umfassenden Überblick über die Hardware, Systemkomponenten und Software-Umgebung auf dem lokalen Computer anzuzeigen. 
## <a name="syntax"></a>Syntax
```
msinfo32 [/pch] [/nfo <path>] [/report <path>] [/computer <computerName>] [/showcategories] [/category <CategoryID>] [/categories {+<CategoryID>(+<CategoryID>)|+all(-<CategoryID>)}]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|<path>|Gibt die Datei im Format geöffnet werden *C:\Folder1\File1.XXX*, wobei *C* Buchstaben des Laufwerks steht, *"Ordner1"* ist der Ordner, *"file1"* ist der Name der Datei und *XXX* ist die Dateinamenerweiterung.<br /><br />Diese Datei kann sein, eine **NFO**, **XML**, **.txt**, oder **CAB** Datei.|
|<computerName>|Gibt den Namen des Ziels oder lokalen Computer. Dies kann ein UNC-Name, eine IP-Adresse oder ein vollständiger Computername sein.|
|<CategoryID>|Gibt die ID des Elements Kategorie. Sie können die Kategorie-ID abrufen, indem Sie mithilfe von **/showcategories**.|
|/pch|Zeigt die Ansicht des Systemverlaufs in das Tool für Systeminformationen an.|
|/nfo|Speichert die exportierte Datei als ein **NFO** Datei. Wenn der Dateiname wird angegeben, *Pfad* endet nicht in einer **NFO** -Erweiterung, die **NFO** Erweiterung wird automatisch an den Dateinamen angefügt.|
|/ Report ein|Speichert die Datei im *Pfad* als Textdatei. Der Dateiname wird gespeichert, genau wie im angezeigt *Pfad*. Die Erweiterung TXT wird nicht in die Datei angefügt werden, es sei denn, sie in den Pfad angegeben ist.|
|/computer|Startet das Tool für Systeminformationen für den angegebenen Remotecomputer. Sie müssen die entsprechenden Berechtigungen auf den Remotecomputer zugreifen.|
|/showcategories|Startet das Tool für Systeminformationen mit allen verfügbaren Kategorie, die IDs angezeigt, anstatt die Anzeigenamen oder lokalisierten Namen. Beispielsweise wird die Softwareumgebung Kategorie angezeigt, als die **SWEnv** Kategorie.|
|/category|Startet die Systeminformationen mit der angegebenen Kategorie ausgewählt. Verwendung **/showcategories** um eine Liste der verfügbaren Kategorie-IDs anzuzeigen.|
|/categories|Startet die Systeminformationen nur mit der angegebenen Kategorie oder Kategorien angezeigt. Außerdem wird die Ausgabe auf die Kategorien oder die ausgewählte Kategorie beschränkt. Verwendung **/showcategories** um eine Liste der verfügbaren Kategorie-IDs anzuzeigen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="remarks"></a>Hinweise
Einige Systeminformationen-Kategorien enthalten, große Mengen von Daten. Sie können die **start/wait** Befehl aus, um das reporting-Leistung für diese Kategorien zu optimieren. Weitere Informationen finden Sie unter [Systeminformationen](https://technet.microsoft.com/library/cc783305(v=ws.10).aspx).
## <a name="BKMK_Examples"></a>Beispiele für
Um die verfügbaren Kategorie-IDs aufzulisten, geben Sie Folgendes ein:
```
msinfo32 /showcategories
```
Starten Sie das Tool für Systeminformationen mit allen verfügbaren Informationen angezeigt, außer geladene Module, Typ:
```
msinfo32 /categories +all -loadedmodules
```
Um nur Systemübersicht Informationen anzeigen, und erstellen eine NFO-Datei syssum.nfo, die Informationen in der Kategorie "Systemübersicht" enthält, geben Sie Folgendes ein:
```
msinfo32 /nfo syssum.nfo /categories +systemsummary
```
Zum Anzeigen von Konfliktinformationen für die Ressource, und erstellen eine NFO-Datei Folgendes ein, das Informationen über Ressourcenkonflikte enthält, geben Sie Folgendes ein:
```
msinfo32 /nfo conflicts.nfo /categories    +componentsproblemdevices+resourcesconflicts+resourcesforcedhardware
```
## <a name="additional-references"></a>Zusätzliche Referenzen
-   [Befehlszeilensyntax](command-line-syntax-key.md)

