---
title: Verwalten von-Bde WipeFreeSpace
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 7cf99a9124f78189de223018608d9864e51d7897
ms.sourcegitcommit: 08eba714d3ceb5f2dfb5486d6b990da1aa4dcbdd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2019
ms.locfileid: "65564689"
---
# <a name="manage-bde-wipefreespace"></a>Verwalten von-Bde: WipeFreeSpace



Zurücksetzen den freien Speicherplatz auf dem Volume Datenfragmente, die im Adressraum vorhanden sind, möglicherweise entfernt. Ausführen dieses Befehls auf einem Volume, das mit die Verschlüsselungsmethode für "Nur verwendeten Speicherplatz" verschlüsselt wurde, bietet das gleiche Maß an Schutz wie die Verschlüsselungsmethode "Full Volume Encryption". Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
manage-bde -WipeFreeSpace|-w [<Drive>] [-Cancel] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Drive>|Stellt einen Laufwerkbuchstaben an, gefolgt von einem Doppelpunkt, ein Volume-GUID-Pfad oder einem bereitgestellten Volume dar.|
|-"Abbrechen"|Bricht eine Zurücksetzung des freien Speicherplatzes, der ausgeführt wird.|
|-computername|Gibt an, dass bde.exe verwendet wird, um die BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **- Cn** als eine verkürzte Version des mit diesem Befehl.|
|\<Name>|Stellt den Namen des Computers, auf dem BitLocker-Schutz zu ändern. Akzeptierte Werte sind die NetBIOS-Namen des Computers und die IP-Adresse des Computers.|
|-? oder /?|Zeigt eine kurze Hilfe an der Eingabeaufforderung.|
|---Help oder-h|Führen Sie zeigt Hilfe an der Eingabeaufforderung ein.|

## <a name="BKMK_Examples"></a>Beispiele für

Das folgende Beispiel veranschaulicht die Verwendung der **-w** Befehl zum Erstellen, Zurücksetzen den freien Speicherplatz auf Laufwerk C.
```
manage-bde -w C:
```
Das folgende Beispiel veranschaulicht die Verwendung der **-w** -Befehl mit der **-Abbrechen** Parameter, um die Bereinigung der freie Speicherplatz auf Laufwerk C. Abbrechen
```
manage-bde -w -Cancel C:
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Verwalten von-bde](manage-bde.md)