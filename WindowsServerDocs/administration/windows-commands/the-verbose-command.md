---
title: Der ausführliche-Befehl
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fcf30ae7-818f-4e7e-a083-a1812682032b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6a655ccdbd95b2f3523babecaa713ccdf99f9ec7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827241"
---
# <a name="the-verbose-command"></a>Der ausführliche-Befehl



Zeigt eine ausführliche Ausgabe für einen bestimmten Befehl. Sie können **/ verbose** mit andere WDSUTIL-Befehle, die Sie ausführen. Beachten Sie, den Sie angeben, müssen **/ verbose** und **/progress** direkt nach **WDSUTIL**.

## <a name="syntax"></a>Syntax

```
WDSUTIL /verbose <commands>
```

## <a name="examples"></a>Beispiele

Zum Löschen von genehmigter Computern aus der Datenbank zum automatischen Hinzufügen und ausführlichen Ausgabe anzeigen, geben Sie Folgendes ein:
```
WDSUTIL /Verbose /progress /Delete-AutoAddDevices /Server:MyWDSServer /DeviceType:ApprovedDevices
```