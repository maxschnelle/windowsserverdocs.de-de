---
title: manage-bde KeyPackage
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c631ef10-2a2f-4541-8578-292f2d4e9e80
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3a53edd060cb8c7a7a52e86130b2136893a42150
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840103"
---
# <a name="manage-bde-keypackage"></a>manage-bde: KeyPackage



Generiert ein Schlüssel Paket für ein Laufwerk. Das Schlüssel Paket kann zusammen mit dem Repair-Tool verwendet werden, um beschädigte Laufwerke zu reparieren. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
manage-bde -KeyPackage [<Drive>] [-ID <KeyProtectoryID>] [-path <PathToExternalKeyDirectory>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Laufwerk >|Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar.|
|-ID|Erstellen Sie ein Schlüssel Paket mithilfe der Schlüssel Schutzvorrichtung mit dem Bezeichner, der durch diesen ID-Wert angegeben wird.|
|-path|Speicherort, an dem das erstellte Schlüssel Paket gespeichert werden soll.|
|-Computername|Gibt an, dass "manage-bde. exe verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden.|
|\<Name >|Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers.|
|-? oder /?|Zeigt eine kurze Hilfe an der Eingabeaufforderung an.|
|-Help oder-h|Zeigt die gesamte Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Das folgende Beispiel veranschaulicht die Verwendung des Befehls " **-KeyPackage** " zum Erstellen eines Schlüssel Pakets für Laufwerk C, das auf der durch die GUID identifizierten Schlüssel Schutzvorrichtung basiert und das Schlüssel Paket in "f:\folder;" speichert.
```
manage-bde -KeyPackage C: -id {84E151C1...7A62067A512} -path f:\Folder
```

> [!TIP]
> Verwenden Sie **manage-bde – Protector – Get** zusammen mit dem Laufwerk Buchstaben, für den Sie ein Schlüssel Paket erstellen möchten, um eine Liste der verfügbaren GUIDs abzurufen, die als ID-Wert verwendet werden sollen.

## <a name="additional-references"></a>Weitere Verweise

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)