---
title: manage-bde Entsperrens
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 063528bf-d235-4b44-887a-52a7d983e01a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3786700a809a672c00ee77c444c133b04e71e863
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840253"
---
# <a name="manage-bde-autounlock"></a>manage-bde: automatische Entsperrung



Verwaltet das automatische Entsperren von mit BitLocker geschützten Daten Laufwerken. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
manage-bde -autounlock [{-enable|-disable|-clearallkeys}] <Drive> [-computername <Name>] [{-?|/?}] [{-help|-h}]

```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-enable|Aktiviert das automatische Entsperren für ein Daten Laufwerk.|
|-disable|Deaktiviert das automatische Entsperren für ein Daten Laufwerk.|
|-clearallkeys|Entfernt alle gespeicherten externen Schlüssel auf dem Betriebssystem Laufwerk.|
|\<Laufwerk >|Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar.|
|-Computername|Gibt an, dass "manage-bde. exe verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden.|
|\<Name >|Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers.|
|-? oder /?|Zeigt eine kurze Hilfe an der Eingabeaufforderung an.|
|-Help oder-h|Zeigt die gesamte Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Das folgende Beispiel veranschaulicht die Verwendung des Befehls " **-autounlock** ", um das automatische Entsperren von Daten Laufwerk E zu aktivieren.
```
manage-bde –autounlock -enable E:
```

## <a name="additional-references"></a>Weitere Verweise

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)