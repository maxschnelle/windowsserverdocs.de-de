---
title: manage-bde ChangeKey
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 69463db9-7e03-47ff-b233-a95d5055725f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2885723f7712ee507fb43465035513bc8c7a1b2b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840193"
---
# <a name="manage-bde-changekey"></a>manage-bde: ChangeKey



Ändert den Systemstart Schlüssel für ein Betriebssystem Laufwerk. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
manage-bde -changekey [<Drive>] [<PathToExternalKeyDirectory>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Laufwerk >|Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar.|
|\<Path>|Stellt den Verzeichnis Speicherort zum Speichern der externen Start Schlüsseldatei dar, die zum Entsperren des Laufwerks verwendet werden kann.|
|-Computername|Gibt an, dass "manage-bde. exe verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden.|
|\<Name >|Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers.|
|-? oder /?|Zeigt eine kurze Hilfe an der Eingabeaufforderung an.|
|-Help oder-h|Zeigt die gesamte Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Im folgenden Beispiel wird veranschaulicht, wie mit dem Befehl **-ChangeKey** ein neuer Systemstart Schlüssel auf Laufwerk E erstellt wird, der mit der BitLocker-Verschlüsselung auf Laufwerk C verwendet werden soll.
```
manage-bde -changekey C: E:\
```

## <a name="additional-references"></a>Weitere Verweise

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)
