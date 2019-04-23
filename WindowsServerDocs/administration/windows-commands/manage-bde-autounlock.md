---
title: Verwalten von-Bde automatisches Entsperren
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 8c17f9781dd4ff924358de490162c6388312ce03
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832271"
---
# <a name="manage-bde-autounlock"></a>Verwalten von-Bde: automatisches Entsperren



Verwaltet das automatische Entsperren von BitLocker-geschützte Laufwerke. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
manage-bde -autounlock [{-enable|-disable|-clearallkeys}] <Drive> [-computername <Name>] [{-?|/?}] [{-help|-h}]

```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-Aktivieren|Ermöglicht das automatische Entsperren für ein Laufwerk.|
|-Deaktivieren|Deaktiviert das automatische Entsperren für ein Laufwerk.|
|-clearallkeys|Entfernt alle gespeicherten externen Schlüssel für das Betriebssystemlaufwerk.|
|\<Drive>|Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar.|
|-computername|Gibt an, dass bde.exe verwendet wird, um die BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **- Cn** als eine verkürzte Version des mit diesem Befehl.|
|\<Name>|Stellt den Namen des Computers, auf dem BitLocker-Schutz zu ändern. Akzeptierte Werte sind die NetBIOS-Namen des Computers und die IP-Adresse des Computers.|
|-? oder /?|Zeigt eine kurze Hilfe an der Eingabeaufforderung.|
|---Help oder-h|Führen Sie zeigt Hilfe an der Eingabeaufforderung ein.|

## <a name="BKMK_Examples"></a>Beispiele für

Das folgende Beispiel veranschaulicht die Verwendung der **– automatisches Entsperren** Befehl zum Aktivieren der automatisches Entsperren des Datenlaufwerk e:.
```
manage-bde –autounlock -enable E:
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Verwalten von-bde](manage-bde.md)