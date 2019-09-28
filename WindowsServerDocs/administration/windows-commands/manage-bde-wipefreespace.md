---
title: manage-bde wipeer FreeSpace
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b8d83a2a-c5c8-4019-9041-23d1d6abf282
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 35d5f5fe079485d35fa412502bec745a136fbce9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373777"
---
# <a name="manage-bde-wipefreespace"></a>"manage-bde Wipeer FreeSpace



Löscht den freien Speicherplatz auf dem Volume und entfernt alle Daten Fragmente, die möglicherweise im Speicherplatz vorhanden sind. Das Ausführen dieses Befehls auf einem Volume, das mithilfe der Verschlüsselungsmethode "nur verwendeter Speicherplatz" verschlüsselt wurde, bietet die gleiche Schutz Ebene wie die Verschlüsselungsmethode "Full Volume Encryption". Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
manage-bde -WipeFreeSpace|-w [<Drive>] [-Cancel] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<laufwerk >|Stellt einen Laufwerk Buchstaben, gefolgt von einem Doppelpunkt, einem Volume-GUID-Pfad oder einem bereitgestellten Volume dar.|
|-Abbrechen|Bricht eine Löschung des freien Speicherplatzes ab, der gerade verarbeitet wird.|
|-Computername|Gibt an, dass "manage-bde. exe verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden.|
|\<Name >|Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers.|
|-? oder /?|Zeigt eine kurze Hilfe an der Eingabeaufforderung an.|
|-Help oder-h|Zeigt die gesamte Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_Examples"></a>Beispiele

Das folgende Beispiel veranschaulicht die Verwendung des Befehls " **-w** ", um den freien Speicherplatz auf Laufwerk C zu löschen.
```
manage-bde -w C:
```
Im folgenden Beispiel wird veranschaulicht, wie der **-w-** Befehl mit dem **-Cancel-** Parameter verwendet wird, um den freien Speicherplatz auf Laufwerk C zu löschen.
```
manage-bde -w -Cancel C:
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)