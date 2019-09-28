---
title: Online Volume
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5da073fd-578d-4691-ad0f-605ba66e0c7e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 06a3c81313180b2880c1e47c3b6c12236fda4245
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372519"
---
# <a name="online-volume"></a>Online Volume



Schaltet Volumes, die derzeit offline sind, in einen Online Status

> [!IMPORTANT]
> Dieser Befehl ist in keiner Edition von Windows Vista verfügbar.

> [!IMPORTANT]
> Dieser Befehl schlägt fehl, wenn er auf einem schreibgeschützten Volume verwendet wird.

## <a name="syntax"></a>Syntax

```
online volume [noerr]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Noerr|Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.|

## <a name="remarks"></a>Hinweise

-   Dieser Befehl funktioniert auf Volumes, bei denen Fehler aufgetreten sind, bei denen Fehler auftreten oder der Redundanz Status nicht erfüllt ist.
-   Ein Volume muss ausgewählt werden, damit dieser Befehl erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl **Volume auswählen** ein Volume aus, und verschieben Sie den Fokus auf das Volume.

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um das Volume mit dem Fokus online zu schalten:
```
online volume
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

