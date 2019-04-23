---
title: bitsadmin zurücksetzen
description: Windows-Befehle Thema **Bitsadmin zurücksetzen** -bricht alle Aufträge in der Übertragungswarteschlange, die der aktuelle Benutzer besitzt.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e4f9d1d-072c-493f-8d7a-f6d713c3ef29
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b7c29aac55393cd87145583814b3ffa8f0a2c3b3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874251"
---
# <a name="bitsadmin-reset"></a>bitsadmin zurücksetzen

Bricht alle Aufträge in der Übertragungswarteschlange, die der aktuelle Benutzer besitzt.

**BITSAdmin 1.5 und früher**: Wenn Sie über Administratorrechte verfügt, haben **zurücksetzen** bricht alle Aufträge in der Warteschlange ab. Die /AllUsers-Option wird nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /Reset [/AllUsers]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|AllUsers|Optional – bricht alle Aufträge in der Warteschlange ab.|

## <a name="remarks"></a>Hinweise

Sie benötigen Administratorrechte, um Sie verwenden die **AllUsers** Parameter.

> [!NOTE]
> Administratoren können nicht vom lokalen System erstellten Aufträge zurücksetzen. Verwenden Sie die aufgabenplanung, um diesen Befehl als eine Aufgabe, die mit den Anmeldeinformationen des lokalen Systems zu planen.

## <a name="BKMK_examples"></a>Beispiele für

Im folgende Beispiel bricht alle Aufträge in der Übertragungswarteschlange für den aktuellen Benutzer ab.
```
C:\>bitsadmin /Reset
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)