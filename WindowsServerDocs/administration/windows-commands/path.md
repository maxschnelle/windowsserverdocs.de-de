---
title: path
description: Erfahren Sie, wie Sie der PATH-Umgebungsvariable festlegen.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1bfa1349-e79a-472b-a9e6-d7a91149ae8f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 65ccaf23b0e19319383952f3a1ca436aaf4d06fd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856461"
---
# <a name="path"></a>path



Legt den Befehlspfad in der PATH-Umgebungsvariablen (die Gruppe von Verzeichnissen zum Suchen nach ausführbaren Dateien verwendet wird) fest. Wenn Sie ohne Angabe von Parametern **Pfad** zeigt den aktuellen Befehlspfad.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
path [[<Drive>:]<Path>[;...][;%PATH%]]
path ;
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[\<Drive>:]<Path>|Gibt an, das Laufwerk und Verzeichnis, in der Befehlspfad festgelegt.|
|;|Trennt die Verzeichnisse im Befehlspfad. Ohne Angabe von anderen Parametern **;** löscht die vorhandenen Befehl Pfade von der PATH-Umgebungsvariable und leitet Cmd.exe nur im aktuellen Verzeichnis zu suchen.|
|% PATH%|Fügt den Befehlspfad der vorhandenen Satz von Verzeichnissen, die in der PATH-Umgebungsvariablen aufgelistet.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Wenn Sie einschließen **%Path%** in der Syntax Cmd.exe ersetzt sie durch die Befehls-Pfadwerte finden Sie in der PATH-Umgebungsvariablen angegeben wird, und Sie müssen diese Werte an der Eingabeaufforderung manuell eingeben.
-   Das aktuelle Verzeichnis wird immer vor in der Befehlspfad angegebenen Verzeichnisse durchsucht.
-   Sie können Dateien in einem Verzeichnis, die den gleichen Namen gemeinsam haben jedoch andere Erweiterungen aufweisen. Beispielsweise müssen Sie möglicherweise eine Datei namens Konto.com, die einem Buchhaltungsprogramm beginnt und eine andere Datei, die mit dem Namen Konto.bat Ihren Server mit der Buchhaltungsnetzwerk verbindet.

    Das Windows-Betriebssystem sucht nach einer Datei mithilfe von standardmäßigen Dateinamenerweiterungen in der folgenden Reihenfolge der Rangfolge: .exe ",".com "," bat, und. cmd ein. Um Accnt.bat auszuführen, wenn Konto.com im gleichen Verzeichnis vorhanden ist, müssen Sie die bat-Erweiterung an der Eingabeaufforderung angeben.
-   Wenn zwei oder mehr Dateien in der Befehlspfad den gleichen Namen und die Erweiterung, **Pfad** sucht zuerst nach der angegebenen Datei im aktuellen Verzeichnis zu nennen. Klicken Sie dann durchsucht er die Verzeichnisse im Befehlspfad in der Reihenfolge, die sie in der PATH-Umgebungsvariablen aufgelistet sind.
-   Setzen Sie die **Pfad** -Befehl in Ihrer Datei, die Windows-Betriebssystem fügt automatisch den angegebene MS-DOS-Subsystems Suchpfad jedes Mal, wenn Sie auf Ihrem Computer anmelden. Cmd.exe wird die Datei nicht verwendet. Wenn über eine Verknüpfung gestartet wird, erbt Cmd.exe die Umgebungsvariablen in meine Computer/Eigenschaften/erweitert/Umgebung festlegen.

## <a name="BKMK_examples"></a>Beispiele für

Um die Pfade C:\User\Taxes B:\User\Invest und B:\Bin für externe Befehle zu suchen, geben Sie Folgendes ein:

`path c:\user\taxes;b:\user\invest;b:\bin`

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)