---
title: manage-bde-Status
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1444a360-fabf-4dd3-b67f-188e6ea3fa5b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 494fb294e7eb0da1b8a0165182d33e799fe56371
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820600"
---
# <a name="manage-bde-status"></a>manage-bde: Status



Enthält die folgenden Informationen zu allen Laufwerken auf dem Computer. unabhängig davon, ob Sie durch BitLocker geschützt sind:
-   Size
-   BitLocker-Version
-   Konvertierungs Status
-   Verschlüsselter Prozentsatz
-   Verschlüsselungsmethode
-   Schutzstatus
-   Sperr Status
-   Identifikations Feld
-   Schlüssel Schutzvorrichtungen



## <a name="syntax"></a>Syntax

```
manage-bde -status [<Drive>] [-protectionaserrorlevel] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<Laufwerk>|Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar.|
|-schutzaserrorlevel|Bewirkt, dass das Befehlszeilen Tool "Manage-BDE" den Rückgabecode von 0 (null) sendet, wenn das Volume geschützt ist, und 1, wenn das Volume nicht geschützt ist. wird am häufigsten für Batch Skripts verwendet, um zu bestimmen, ob ein Laufwerk durch BitLocker geschützt ist. Sie können auch **-p** als abgekürzte Version dieses Befehls verwenden.|
|-Computername|Gibt an, dass "manage-bde. exe verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden.|
|\<Name>|Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers.|
|-? oder /?|Zeigt eine kurze Hilfe an der Eingabeaufforderung an.|
|-Help oder-h|Zeigt die gesamte Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a>Beispiele

Veranschaulicht die Verwendung des Befehls " **-Status** ", um den Status von Laufwerk C anzuzeigen.
```
manage-bde –status C:
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)