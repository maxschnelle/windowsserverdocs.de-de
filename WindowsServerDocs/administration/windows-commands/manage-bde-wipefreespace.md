---
title: manage-bde wipeer FreeSpace
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b8d83a2a-c5c8-4019-9041-23d1d6abf282
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8f1e0f99c226edae467ecb09222b18098ac399ee
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724045"
---
# <a name="manage-bde-wipefreespace"></a>manage-bde: wipeer FreeSpace



Löscht den freien Speicherplatz auf dem Volume und entfernt alle Daten Fragmente, die möglicherweise im Speicherplatz vorhanden sind. Wenn Sie diesen Befehl auf einem Volume ausführen, das mithilfe der Verschlüsselungsmethode "nur verwendeten Speicherplatz" verschlüsselt wurde, bietet das gleiche Maß an Schutz wie die Verschlüsselungsmethode für die vollständige Volumenverschlüsselung.

## <a name="syntax"></a>Syntax

```
manage-bde -WipeFreeSpace|-w [<Drive>] [-Cancel] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<Laufwerk>|Stellt einen Laufwerk Buchstaben, gefolgt von einem Doppelpunkt, einem Volume-GUID-Pfad oder einem bereitgestellten Volume dar.|
|-Abbrechen|Bricht eine Löschung des freien Speicherplatzes ab, der gerade verarbeitet wird.|
|-Computername|Gibt an, dass "manage-bde. exe verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden.|
|\<Name>|Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers.|
|-? oder /?|Zeigt eine kurze Hilfe an der Eingabeaufforderung an.|
|-Help oder-h|Zeigt die gesamte Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a>Beispiele

Um zu veranschaulichen, dass der freie Speicherplatz auf Laufwerk C mit dem Befehl **-w** gelöscht wird.
```
manage-bde -w C:
```
Um zu veranschaulichen, wie der **-w-** Befehl mit dem Parameter **-Cancel** verwendet wird, um das Löschen des freien Speicherplatzes auf Laufwerk C aufzuheben.
```
manage-bde -w -Cancel C:
```

## <a name="additional-references"></a>Zusätzliche Referenzen

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)