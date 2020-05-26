---
title: msinfo32
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a38f31d7-1766-4103-becc-9d0b87c2826d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 09767502585754bec690b40dd71fabd78540ab50
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820820"
---
# <a name="msinfo32"></a>msinfo32

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Öffnet das System Informationstool, um eine umfassende Ansicht der Hardware, der System Komponenten und der Softwareumgebung auf dem lokalen Computer anzuzeigen.
## <a name="syntax"></a>Syntax
```
msinfo32 [/pch] [/nfo <path>] [/report <path>] [/computer <computerName>] [/showcategories] [/category <CategoryID>] [/categories {+<CategoryID>(+<CategoryID>)|+all(-<CategoryID>)}]
```
#### <a name="parameters"></a>Parameter

|    Parameter    |                                                                                                                                 BESCHREIBUNG                                                                                                                                  |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     <path>      | Gibt die Datei an, die im Format *c:\folder1\file1.xxx*geöffnet werden soll, wobei *C* der Laufwerk Buchstabe, *"Ordner1"* der Ordner, *file1* der Dateiname und *xxx* die Dateinamenerweiterung ist.<p>Bei dieser Datei kann es sich um eine **nfo**-, **XML**-, **txt**-oder **. cab** -Datei handeln. |
| <computerName>  |                                                                             Gibt den Namen des Ziel Computers oder des lokalen Computers an. Dabei kann es sich um einen UNC-Namen, eine IP-Adresse oder einen vollständigen Computernamen handeln.                                                                              |
|  <CategoryID>   |                                                                                     Gibt die ID des Kategorieelements an. Die Kategoriekennung können Sie mithilfe von **/showcategories**abrufen.                                                                                      |
|      /pch       |                                                                                                       Zeigt die Ansicht System Verlauf im System Informationstool an.                                                                                                       |
|      /nfo       |                                     Speichert die exportierte Datei als **nfo** -Datei. Wenn der im *Pfad* angegebene Dateiname nicht in einer **nfo** -Erweiterung endet, wird die Erweiterung **. nfo** automatisch an den Dateinamen angehängt.                                      |
|     /Report ein     |                                               Speichert die Datei im *Pfad* als Textdatei. Der Dateiname wird genau so gespeichert, wie er im *Pfad*angezeigt wird. Die Erweiterung ". txt" wird nicht an die Datei angefügt, es sei denn, Sie wird im Pfad angegeben.                                                |
|    /computer    |                                                                startet das System Informationstool für den angegebenen Remote Computer. Sie müssen über die entsprechenden Berechtigungen für den Zugriff auf den Remote Computer verfügen.                                                                |
| /showcategories |                         startet das System Informationstool, bei dem alle verfügbaren Kategorie-IDs angezeigt werden, anstatt die anzeigen Amen oder lokalisierten Namen anzuzeigen. Beispielsweise wird die Kategorie Software Umgebung als **SWEnv** -Kategorie angezeigt.                         |
|    /category    |                                                                     startet System Informationen, bei denen die angegebene Kategorie ausgewählt ist. Verwenden Sie **/showcategories** , um eine Liste der verfügbaren kategorieids anzuzeigen.                                                                     |
|   /categories   |                          startet System Informationen, wobei nur die angegebene Kategorie oder die angegebenen Kategorien angezeigt werden. Außerdem wird die Ausgabe auf die ausgewählte Kategorie oder die ausgewählten Kategorien beschränkt. Verwenden Sie **/showcategories** , um eine Liste der verfügbaren kategorieids anzuzeigen.                          |
|       /?        |                                                                                                                     Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                     |

## <a name="remarks"></a>Hinweise
Einige System Informationskategorien enthalten große Datenmengen. Sie können den Befehl **Start/Wait** verwenden, um die Bericht Erstellungs Leistung für diese Kategorien zu optimieren. Weitere Informationen finden Sie unter [System Informationen](https://technet.microsoft.com/library/cc783305(v=ws.10).aspx).
## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um die verfügbaren Kategorie-IDs aufzulisten:
```
msinfo32 /showcategories
```
Geben Sie Folgendes ein, um das System Informationstool mit allen verfügbaren Informationen zu starten, mit Ausnahme geladener Module:
```
msinfo32 /categories +all -loadedmodules
```
Geben Sie Folgendes ein, um nur System Zusammenfassungs Informationen anzuzeigen und eine NFO-Datei namens syssum. nfo zu erstellen, die Informationen in der Kategorie System Zusammenfassung enthält:
```
msinfo32 /nfo syssum.nfo /categories +systemsummary
```
Geben Sie Folgendes ein, um Ressourcen Konflikt Informationen anzuzeigen und eine NFO-Datei namens "Konflikts. nfo" zu erstellen, die Informationen zu Ressourcenkonflikten enthält:
```
msinfo32 /nfo conflicts.nfo /categories    +componentsproblemdevices+resourcesconflicts+resourcesforcedhardware
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

