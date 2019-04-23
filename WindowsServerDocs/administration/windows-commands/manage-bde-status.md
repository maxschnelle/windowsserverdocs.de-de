---
title: Verwalten von-Bde-status
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1444a360-fabf-4dd3-b67f-188e6ea3fa5b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d81808b57b1833ca30b95dc9d4b6aa0b0a4bdbaa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836561"
---
# <a name="manage-bde-status"></a>Verwalten von-Bde: Status



Bietet die folgende Informationen über alle Laufwerke auf dem Computer an. Gibt an, ob sie BitLocker geschützt sind:
-   Größe
-   BitLocker-version
-   Konvertierungsstatus
-   Prozentsatz verschlüsselt
-   Verschlüsselungsmethode
-   Schutzstatus
-   Sperrstatus
-   ID-Feld
-   Schlüsselschutzvorrichtungen

Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
manage-bde -status [<Drive>] [-protectionaserrorlevel] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Drive>|Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar.|
|-protectionaserrorlevel|Bewirkt, dass das Befehlszeilentool "Manage-Bde" Senden Sie den Rückgabecode von 0, wenn das Volume geschützt wird und 1 ein, wenn das Volume nicht geschützt ist; am häufigsten verwendet für Batchskripts, um festzustellen, ob ein Laufwerk durch BitLocker geschützt ist. Sie können auch **-p** als eine verkürzte Version des mit diesem Befehl.|
|-computername|Gibt an, dass bde.exe verwendet wird, um die BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **- Cn** als eine verkürzte Version des mit diesem Befehl.|
|\<Name>|Stellt den Namen des Computers, auf dem BitLocker-Schutz zu ändern. Akzeptierte Werte sind die NetBIOS-Namen des Computers und die IP-Adresse des Computers.|
|-? oder /?|Zeigt eine kurze Hilfe an der Eingabeaufforderung.|
|---Help oder-h|Führen Sie zeigt Hilfe an der Eingabeaufforderung ein.|

## <a name="BKMK_Examples"></a>Beispiele für

Das folgende Beispiel veranschaulicht die Verwendung der **-Status** Befehl, um den Status des Laufwerks C. anzuzeigen.
```
manage-bde –status C:
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Verwalten von-bde](manage-bde.md)