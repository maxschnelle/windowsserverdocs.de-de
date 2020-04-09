---
title: manage-bde-Spezifizierer
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7092d18f-4ac9-4c73-a20f-1246ca60e75e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e24719e120430cbfd5192e1800f59f0676aef5cb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839873"
---
# <a name="manage-bde-setidentifier"></a>manage-bde:-Objekt-tifier



Legt das Feld Laufwerks-ID auf dem Laufwerk auf den Wert fest, der in der Einstellung **Geben Sie die eindeutigen Bezeichner für Ihre Organisation** Gruppenrichtlinie festgelegt ist. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
manage-bde –setidentifier <Drive> [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Laufwerk >|Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar.|
|-Computername|Gibt an, dass "manage-bde. exe verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden.|
|\<Name >|Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers.|
|-? oder /?|Zeigt eine kurze Hilfe an der Eingabeaufforderung an.|
|-Help oder-h|Zeigt die gesamte Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Das folgende Beispiel veranschaulicht die Verwendung des Befehls " **-setidentifier** " zum Festlegen des BitLocker-Laufwerks Bezeichnerfelds für C.
```
manage-bde –setidentifier C:
```

## <a name="additional-references"></a>Weitere Verweise

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)
-   [Verwenden von Datenwiederherstellungs-Agents mit BitLocker](https://technet.microsoft.com/library/dd875560(WS.10).aspx)