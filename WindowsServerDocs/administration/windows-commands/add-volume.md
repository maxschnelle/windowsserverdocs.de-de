---
title: Volume hinzufügen
description: Windows-Befehle Thema **Volume hinzufügen** -Hinzufügen von Volumes auf der Schattenkopie festgelegt ist, wird die Gruppe von Volumes Schattenkopien werden kopiert.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b7d4d35d-8bda-46d2-8df5-eb598cecaaba
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8960ffafdf49d4512e1df2dfcc046bdfbe56e224
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819471"
---
# <a name="add-volume"></a>Volume hinzufügen



Hinzufügen von Volumes der Schatten kopieren festgelegt wird, wird die Gruppe von Volumes Schattenkopien erstellt werden. Dieser Befehl ist erforderlich, um Schattenkopien zu erstellen. Wenn Sie ohne Angabe von Parametern **Volume hinzufügen** zeigt die Hilfe an der Eingabeaufforderung.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
add volume <Volume> [provider <ProviderID>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Volume >|Gibt ein Volume zum Hinzufügen der Schatten kopieren festgelegt. Mindestens ein Volume ist erforderlich, für die Erstellung von Schattenkopien.|
|[Anbieter \<ProviderID >]|Gibt an, die Anbieter-ID eines registrierten Anbieters verwenden, um die Schattenkopie zu erstellen. Wenn **Anbieter** nicht angegeben ist, wird der Standardanbieter verwendet wird.|

## <a name="remarks"></a>Hinweise

-   Volumes werden nacheinander hinzugefügt.
-   Jedes Mal, wenn ein Volume hinzugefügt wird, wird er überprüft, um sicherzustellen, dass die VSS unterstützt die Erstellung von Schattenkopien des Volumes. Diese primären Überprüfung möglicherweise ungültig gemacht werden, jedoch später mithilfe der der **Kontext festlegen** Befehl.
-   Wenn eine Schattenkopie erstellt wird, verknüpft eine Umgebungsvariable den Alias der Schattenkopie-ID an, damit der Alias, klicken Sie dann für die Skripterstellung verwendet werden kann.

## <a name="BKMK_examples"></a>Beispiele für

Können Sie die aktuelle Liste der registrierten Anbieter auf anzeigen. dem `DISKSHADOW>` dazu aufgefordert werden, geben Sie:
```
list providers
```
Die folgende Ausgabe zeigt an einen einzigen Anbieter, der standardmäßig verwendet wird:
```
* ProviderID: {b5946137-7b9f-4925-af80-51abd60b20d5}
        Type: [1] VSS_PROV_SYSTEM
        Name: Microsoft Software Shadow Copy provider 1.0
        Version: 1.0.0.7
        CLSID: {65ee1dba-8ff4-4a58-ac1c-3470ee2f376a}
1 provider registered.
```
Zum Hinzufügen von Laufwerk C die Schattenkopie kopieren festgelegt, und weisen einen alias mit dem Namen 1, geben Sie Folgendes ein:
```
add volume c: alias System1
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)