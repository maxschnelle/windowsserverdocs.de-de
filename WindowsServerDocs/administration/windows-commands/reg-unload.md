---
title: REG entladen
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1d07791d-ca27-454e-9797-27d7e84c5048
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: aaa7d7a9fa82db2968d988e3b7b3fb8275a72337
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834981"
---
# <a name="reg-unload"></a>REG entladen



Entfernt einen Teil der Registrierung, die geladen wurde, mithilfe der **Reg Load** Vorgang.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
reg unload <KeyName>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<KeyName>|Gibt den vollständigen Pfad des Unterschlüssels, entladen werden soll. Zum Angeben von Remotecomputern, enthalten den Namen des Computers (im Format \\ \\ComputerName\) als Teil der *KeyName*. Das auslassen \\ \\ComputerName\ bewirkt, dass den Vorgang standardmäßig auf dem lokalen Computer. Die *KeyName* muss einen gültiges Stammzertifizierungsstellen-Schlüssel enthalten. Gültiges Stammzertifizierungsstellen-Schlüssel für den lokalen Computer sind HKLM "," HKCU "," HKCR "," HKU ", und" HKCC. Wenn ein Remotecomputer angegeben wird, sind gültige Stammschlüssel HKLM und "HKU".|
|/?|Zeigt die Hilfe für **Reg entladen** an der Eingabeaufforderung.|

## <a name="remarks"></a>Hinweise

Die folgende Tabelle enthält die Rückgabewerte für die **Reg entladen** Option.

|Wert|Beschreibung|
|-----|-----------|
|0|Erfolgreich|
|1|Nicht möglich|

## <a name="BKMK_examples"></a>Beispiele für

Um die Struktur in der HKLM-Datei zu entsperren, geben Sie Folgendes ein:
```
REG UNLOAD HKLM\TempHive
```

> [!CAUTION]
> Bearbeiten Sie die Registrierung nicht direkt auf, es sei denn, es unbedingt erforderlich. Die Registrierungs-Editor umgehen Sie standardmäßige Schutzvorrichtungen, können die Einstellungen, die die Leistung beeinträchtigen, Schäden am System oder selbst müssen Sie Windows neu installieren können. Sie können die meisten registrierungseinstellungen für die sicher ändern, indem Sie die Programme in der Systemsteuerung oder Microsoft Management Console (MMC). Wenn Sie die Registrierung direkt bearbeiten müssen, Sichern sie Sie vorher.

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)