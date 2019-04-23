---
title: uniqueid
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 64235a4a-b91c-46da-b9b0-68ee90571c2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4cad6607e13d2657433e4e78ce8e65beff73aa9d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857511"
---
# <a name="uniqueid"></a>uniqueid



Zeigt an, oder legt die GUID Partition Table (GPT) Bezeichner oder Master Boot Record (MBR)-Signatur für den Datenträger mit dem Fokus.

> [!IMPORTANT]
> Dieser DiskPart-Befehl ist nicht in jeder Edition von Windows Vista verfügbar.

## <a name="syntax"></a>Syntax

```
uniqueid disk [id={<dword> | <GUID>}] [noerr]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|id={\<dword> | <GUID>}|Gibt an für MBR-Datenträger eine vier-Byte-DWORD-Wert im hexadezimalen Format für die Signatur.</br>Gibt Sie für GPT-Datenträger eine GUID für den Bezeichner ein.|
|Diskpart|nur für Skripts. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.|

## <a name="remarks"></a>Hinweise

-   Dieser Befehl funktioniert auf Basisdatenträger und dynamische Datenträger.
-   Ein Datenträger muss ausgewählt werden, damit dieser Befehl erfolgreich ausgeführt werden. Verwenden der **select Disk** Befehl aus, wählen Sie einen Datenträger und verschiebt den Fokus auf sie.

## <a name="BKMK_examples"></a>Beispiele für

Wenn die Signatur der MBR-Datenträgers mit dem Fokus anzeigen möchten, geben Sie Folgendes ein:
```
uniqueid disk
```
Um die Signatur der MBR-Datenträgers mit dem Fokus 5f1b2c36 festzulegen, geben Sie Folgendes ein:
```
uniqueid disk id=5f1b2c36
```
Um den Bezeichner der dem GPT-Datenträger mit dem Fokus baf784e7-6bbd-4cfb-Aaac-e86c96e166ee festzulegen, geben Sie Folgendes ein:
```
uniqueid disk id=baf784e7-6bbd-4cfb-aaac-e86c96e166ee
```

#### <a name="additional-references"></a>Weitere Verweise

