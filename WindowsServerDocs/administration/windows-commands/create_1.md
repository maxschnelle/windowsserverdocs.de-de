---
title: erstellen
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 837aa449-9b60-41ae-9ef1-ef67af6e5918
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2245efb6c3bce8aecf8edf730694804ffbdc3d80
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378772"
---
# <a name="create"></a>erstellen



startet den Vorgang zum Erstellen von Schatten Kopien mithilfe der aktuellen Kontext-und Options Einstellungen. Erfordert mindestens ein Volume im Schattenkopiesatz.

## <a name="syntax"></a>Syntax

```
create
```

## <a name="remarks"></a>Hinweise

-   Sie müssen mindestens ein Volume mit dem Befehl " **Volume hinzufügen** " hinzufügen, bevor Sie den Befehl " **Create** " verwenden können.
-   Mit dem Befehl **Sicherung starten** können Sie anstelle einer Kopiesicherung eine vollständige Sicherung angeben.
-   Nachdem Sie den **Create** -Befehl ausgeführt haben, können Sie mit dem Befehl **exec** ein duplikatskript für die Sicherung aus der Schatten Kopie ausführen.

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)