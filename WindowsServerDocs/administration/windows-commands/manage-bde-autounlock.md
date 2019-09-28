---
title: manage-bde Entsperrens
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 063528bf-d235-4b44-887a-52a7d983e01a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e6927c964a3f35c70fc3b9467cc2d16bbd973b17
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374140"
---
# <a name="manage-bde-autounlock"></a>manage-bde: automatische Entsperrung



Verwaltet das automatische Entsperren von mit BitLocker geschützten Daten Laufwerken. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
manage-bde -autounlock [{-enable|-disable|-clearallkeys}] <Drive> [-computername <Name>] [{-?|/?}] [{-help|-h}]

```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-Aktivieren|Aktiviert das automatische Entsperren für ein Daten Laufwerk.|
|-Deaktivieren|Deaktiviert das automatische Entsperren für ein Daten Laufwerk.|
|-clearallkeys|Entfernt alle gespeicherten externen Schlüssel auf dem Betriebssystem Laufwerk.|
|\<laufwerk >|Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar.|
|-Computername|Gibt an, dass "manage-bde. exe verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden.|
|\<Name >|Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers.|
|-? oder /?|Zeigt eine kurze Hilfe an der Eingabeaufforderung an.|
|-Help oder-h|Zeigt die gesamte Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_Examples"></a>Beispiele

Das folgende Beispiel veranschaulicht die Verwendung des Befehls " **-autounlock** ", um das automatische Entsperren von Daten Laufwerk E zu aktivieren.
```
manage-bde –autounlock -enable E:
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)