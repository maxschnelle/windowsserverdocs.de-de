---
title: recover
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cc3a73d-9456-41a0-b375-2b4cc37c3992
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a83bb7502145cc09116241ea255e31b5f9981791
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384739"
---
# <a name="recover"></a>recover



Aktualisiert den Status aller Datenträger in einer Datenträger Gruppe, versucht, Datenträger in einer ungültigen Datenträger Gruppe wiederherzustellen, und synchronisiert die gespiegelten Volumes und RAID-5-Volumes mit veralteten Daten erneut.

> [!IMPORTANT]
> Dieser Diskpart-Befehl ist in keiner Edition von Windows Vista verfügbar.

## <a name="syntax"></a>Syntax

```
recover [noerr]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Noerr|Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.|

## <a name="remarks"></a>Hinweise

-   Dieser Befehl arbeitet auf einer Datenträger Gruppe.
-   Dieser Befehl gilt nur für gruppendynamischer Datenträger. Wenn dieser Befehl in einer Gruppe mit einem Basis Datenträger verwendet wird, wird kein Fehler zurückgegeben, aber es wird keine Aktion ausgeführt.
-   Dieser Befehl funktioniert auf Datenträgern, die fehlerhaft sind oder fehlschlagen. Sie funktioniert auch auf Volumes, die fehlerhaft oder fehlerhaft oder in fehlerhafter Redundanz Zustand sind.
-   Ein Datenträger, der Teil einer Datenträger Gruppe ist, muss ausgewählt werden, damit dieser Befehl erfolgreich ausgeführt werden kann. Wählen Sie mit dem Befehl Datenträger **auswählen** einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um die Datenträger Gruppe mit dem Fokus auf dem Datenträger wiederherzustellen:
```
recover
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

