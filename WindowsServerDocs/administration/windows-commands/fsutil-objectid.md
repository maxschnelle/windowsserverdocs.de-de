---
ms.assetid: 693ab895-9d0c-47c1-9f52-df5cd287842a
title: Fsutil-Objekt-ID
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 2f5887f20e2c36ec7dcfcd6f4e920b5273c6c60c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813741"
---
# <a name="fsutil-objectid"></a>Fsutil-Objekt-ID
>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, WindowsServer 2012, Windows 8, Windows Server 2008 R2, Windows 7

Verwaltet von Objektbezeichnern (OIDs), die internen Objekten, die von Distributed Link nachverfolgen (DLT)-Client-Dienst und (File Replication Service, FRS) verwendet, um andere Objekte wie Dateien, Verzeichnisse und Links zu verfolgen sind. Objekt-IDs für die meisten Programme nicht mehr sichtbar sind, und es sollten niemals geändert werden.

> [!CAUTION]
> Führen Sie nicht löschen Sie, festlegen Sie oder ändern Sie andernfalls eine Objekt-ID. Löschen oder Festlegen der Objekt-ID kann zum Verlust von Daten aus Teilen einer Datei, die bis zur und einschließlich der gesamten Mengen von Daten führen. Darüber hinaus können Sie negative Verhalten in der Distributed Link nachverfolgen (DLT)-Client-Dienst und den Dateireplikationsdienst (FRS) verursachen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
fsutil objectid [create] <FileName>
fsutil objectid [delete] <FileName>
fsutil objectid [query] <FileName>
fsutil objectid [set] <ObjectID> <BirthVolumeID> <BirthObjectID> <DomainID> <FileName>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------------|---------------|
|erstellen|Erstellt eine Objekt-ID an, wenn die angegebene Datei nicht bereits vorhanden ist. Wenn die Datei bereits eine Objekt-ID enthält, entspricht dieses Unterbefehl der **Abfrage** Unterbefehl.|
|löschen|Löscht eine Objekt-ID an.|
|query|Fragt eine Objekt-ID an.|
|set|Legt eine Objekt-ID fest.|
|\<ObjectID>|Legt eine hexadezimale 16-Byte-spezifischen-ID, die garantiert innerhalb eines Volumes eindeutig sein. Die Objekt-ID wird vom Dienst Distributed Link nachverfolgen (DLT)-Client und dem Dateireplikationsdienst (FRS) verwendet, um Dateien zu identifizieren.|
|\<BirthVolumeID>|Gibt an, das Volume auf dem sich die Datei befand, wenn sie zuerst eine Objekt-ID abgerufen. Dieser Wert ist eine hexadezimale 16-Byte-Bezeichner, der vom DLT-Client-Dienst verwendet wird.|
|\<BirthObjectID>|Gibt das ursprüngliche Objekt-ID der Datei an (die *ObjectID* möglicherweise ändern, wenn eine Datei verschoben wird). Dieser Wert ist eine hexadezimale 16-Byte-Bezeichner, der vom DLT-Client-Dienst verwendet wird.|
|\<DomainID>|hexadezimale 16-Byte-Domänenbezeichner. Dieser Wert wird derzeit nicht verwendet und muss auf lauter Nullen festgelegt werden.|
|\<FileName>|Gibt den vollständigen Pfad zur Datei einschließlich der Namen und die Erweiterung, z. B. C:\documents\filename.txt an.|

## <a name="remarks"></a>Hinweise

-   Jede Datei mit der Objekt-ID hat auch ein Geburtsdatum-Volume-ID, ein Geburtsdatum-Objekt-ID und ein Bezeichner der Anwendungsdomäne. Wenn Sie eine Datei verschieben, die Objekt-ID kann sich ändern, aber das Geburtsdatum Volume und Geburtsdatum Objektbezeichner bleiben gleich. Dieses Verhalten kann es sich um das Windows-Betriebssystem immer ermittelt eine Datei, unabhängig davon, wo es verschoben wurde.

## <a name="BKMK_examples"></a>Beispiele für
Um eine Objekt-ID zu erstellen, geben Sie Folgendes ein:

`fsutil objectid create c:\temp\sample.txt`

Um eine Objekt-ID zu löschen, geben Sie Folgendes ein:

`fsutil objectid delete c:\temp\sample.txt`

Eine Objekt-ID abgefragt werden soll, geben Sie Folgendes ein:

`fsutil objectid query c:\temp\sample.txt`

Um eine Objekt-ID festzulegen, geben Sie Folgendes ein:

`fsutil objectid set 40dff02fc9b4d4118f120090273fa9fc f86ad6865fe8d21183910008c709d19e 40dff02fc9b4d4118f120090273fa9fc 00000000000000000000000000000000 c:\temp\sample.txt`

#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilensyntax](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


