---
title: msinfo32
description: Referenz Artikel zum msinfo32-Befehl, der das System Informationstool öffnet, um eine umfassende Ansicht der Hardware, der System Komponenten und der Softwareumgebung auf dem lokalen Computer anzuzeigen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a38f31d7-1766-4103-becc-9d0b87c2826d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e43ed2680c099ca97a0074d5f460f504b3edb298
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86956812"
---
# <a name="msinfo32"></a>msinfo32

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Öffnet das System Informationstool, um eine umfassende Ansicht der Hardware, der System Komponenten und der Softwareumgebung auf dem lokalen Computer anzuzeigen.

Einige System Informationskategorien enthalten große Datenmengen. Sie können den Befehl **Start/Wait** verwenden, um die Bericht Erstellungs Leistung für diese Kategorien zu optimieren. Weitere Informationen finden Sie unter [System Informationen](/previous-versions/windows/it-pro/windows-server-2003/cc783305(v=ws.10)).

## <a name="syntax"></a>Syntax

```
msinfo32 [/pch] [/nfo <path>] [/report <path>] [/computer <computername>] [/showcategories] [/category <categoryID>] [/categories {+<categoryID>(+<categoryID>)|+all(-<categoryID>)}]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<path>` | Gibt die Datei an, die im Format *c:\folder1\file1.xxx*geöffnet werden soll, wobei *C* der Laufwerk Buchstabe, *"Ordner1"* der Ordner, *file1* der Dateiname und *xxx* die Dateinamenerweiterung ist.<p>Bei dieser Datei kann es sich um eine **nfo**-, **XML**-, **txt**-oder **. cab** -Datei handeln. |
| `<computername>` | Gibt den Namen des Ziel Computers oder des lokalen Computers an. Dabei kann es sich um einen UNC-Namen, eine IP-Adresse oder einen vollständigen Computernamen handeln. |
| `<categoryID>` | Gibt die ID des Kategorieelements an. Die Kategoriekennung können Sie mithilfe von **/showcategories**abrufen. |
| /pch | Zeigt die Ansicht System Verlauf im System Informationstool an. |
| /nfo | Speichert die exportierte Datei als **nfo** -Datei. Wenn der im *Pfad* angegebene Dateiname nicht in einer **nfo** -Erweiterung endet, wird die Erweiterung **. nfo** automatisch an den Dateinamen angehängt. |
| /Report ein | Speichert die Datei im *Pfad* als Textdatei. Der Dateiname wird genau so gespeichert, wie er im *Pfad*angezeigt wird. Die Erweiterung ". txt" wird nicht an die Datei angefügt, es sei denn, Sie wird im Pfad angegeben. |
| /computer | Startet das System Informationstool für den angegebenen Remote Computer. Sie müssen über die entsprechenden Berechtigungen für den Zugriff auf den Remote Computer verfügen. |
| /showcategories | Startet das System Informationstool, bei dem alle verfügbaren Kategorie-IDs angezeigt werden, anstatt die anzeigen Amen oder lokalisierten Namen anzuzeigen. Beispielsweise wird die Kategorie Software Umgebung als **SWEnv** -Kategorie angezeigt. |
| /category | Startet System Informationen, bei denen die angegebene Kategorie ausgewählt ist. Verwenden Sie **/showcategories** , um eine Liste der verfügbaren kategorieids anzuzeigen. |
| /categories | Startet System Informationen, wobei nur die angegebene Kategorie oder die angegebenen Kategorien angezeigt werden. Außerdem wird die Ausgabe auf die ausgewählte Kategorie oder die ausgewählten Kategorien beschränkt. Verwenden Sie **/showcategories** , um eine Liste der verfügbaren kategorieids anzuzeigen. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die verfügbaren Kategorie-IDs aufzulisten:

```
msinfo32 /showcategories
```

Geben Sie Folgendes ein, um das System Informationstool mit allen verfügbaren Informationen zu starten, mit Ausnahme geladener Module:

```
msinfo32 /categories +all -loadedmodules
```

Geben Sie Folgendes ein, um **System Zusammenfassungs** Informationen anzuzeigen und eine NFO-Datei namens *syssum. nfo*zu erstellen, die Informationen in der Kategorie **System Zusammenfassung** enthält:

```
msinfo32 /nfo syssum.nfo /categories +systemsummary
```

Geben Sie Folgendes ein, um Ressourcen Konflikt Informationen anzuzeigen und eine NFO-Datei namens "Konflikts *. nfo*" zu erstellen, die Informationen zu Ressourcenkonflikten enthält:

```
msinfo32 /nfo conflicts.nfo /categories +componentsproblemdevices+resourcesconflicts+resourcesforcedhardware
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
