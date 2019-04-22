---
title: Set-DriverPackage / Unterbefehl
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 11804bb6-ca29-4461-8c63-5131748cd742
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0513d3de2416f93f69b1e1cc286c38b12be94d15
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818821"
---
# <a name="subcommand-set-driverpackage"></a>Subcommand: set-DriverPackage



Benennt und/oder aktiviert oder deaktiviert ein Treiberpaket auf einem Server.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Set-DriverPackage [/Server:<Server name>] {/DriverPackage:<Name> | /PackageId:<ID>} [/Name:<New Name>] [/Enabled:{Yes | No}
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[/ Server:\<Servername >]|Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollqualifizierten Domänennamen sein. Wenn ein Servername nicht angegeben ist, wird der lokale Server verwendet.|
|[/ DriverPackage /:\<Name >]|Gibt den aktuellen Namen des Treiberpakets ändern.|
|[/PackageId:\<ID>]|Gibt die Windows Deployment Services-ID des Treiberpakets an. Sie müssen diese Option angeben, wenn das Treiberpaket eindeutig anhand des Namens identifiziert werden kann. Um diese ID für ein Paket zu suchen, klicken Sie auf die Treibergruppe gewährt wird, der das Paket wird (oder die **alle Pakete** Knoten) mit der rechten Maustaste auf das Paket, und klicken Sie dann auf **Eigenschaften**. Die Paket-ID finden Sie auf die **allgemeine** Registerkarte. Zum Beispiel: {DD098D20-1850-4FC8-8E35-EA24A1BEFF5E}.|
|[/ Name:\<neuer Name >]|Gibt den neuen Namen für das Treiberpaket an.|
|[/ Aktiviert: {Yes | Keine}|Aktiviert oder deaktiviert das Paket.|

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie einen der folgenden Schritte aus, zum Ändern der Einstellungen zu einem Paket:
```
WDSUTIL /Set-DriverPackage /PackageId:{4D36E972-E325-11CE-BFC1-08002BE10318} /Name:MyDriverPackage
```
```
WDSUTIL /Set-DriverPackage /DriverPackage:MyDriverPackage /Name:NewName /Enabled:Yes
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)