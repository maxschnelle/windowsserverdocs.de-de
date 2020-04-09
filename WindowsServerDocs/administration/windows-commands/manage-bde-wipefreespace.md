---
title: manage-bde wipeer FreeSpace
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b8d83a2a-c5c8-4019-9041-23d1d6abf282
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6a9995c6872380af61bec5d3b200e733c034ea6b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839713"
---
# <a name="manage-bde-wipefreespace"></a>manage-bde: wipeer FreeSpace



Löscht den freien Speicherplatz auf dem Volume und entfernt alle Daten Fragmente, die möglicherweise im Speicherplatz vorhanden sind. Wenn Sie diesen Befehl auf einem Volume ausführen, das mithilfe der Verschlüsselungsmethode "nur verwendeten Speicherplatz" verschlüsselt wurde, bietet das gleiche Maß an Schutz wie die Verschlüsselungsmethode für die vollständige Volumenverschlüsselung. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
manage-bde -WipeFreeSpace|-w [<Drive>] [-Cancel] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Laufwerk >|Stellt einen Laufwerk Buchstaben, gefolgt von einem Doppelpunkt, einem Volume-GUID-Pfad oder einem bereitgestellten Volume dar.|
|-Abbrechen|Bricht eine Löschung des freien Speicherplatzes ab, der gerade verarbeitet wird.|
|-Computername|Gibt an, dass "manage-bde. exe verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden.|
|\<Name >|Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers.|
|-? oder /?|Zeigt eine kurze Hilfe an der Eingabeaufforderung an.|
|-Help oder-h|Zeigt die gesamte Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Das folgende Beispiel veranschaulicht die Verwendung des Befehls " **-w** ", um den freien Speicherplatz auf Laufwerk C zu löschen.
```
manage-bde -w C:
```
Im folgenden Beispiel wird veranschaulicht, wie der **-w-** Befehl mit dem **-Cancel-** Parameter verwendet wird, um den freien Speicherplatz auf Laufwerk C zu löschen.
```
manage-bde -w -Cancel C:
```

## <a name="additional-references"></a>Weitere Verweise

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)