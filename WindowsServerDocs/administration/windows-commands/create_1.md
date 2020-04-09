---
title: erstellen
description: Windows-Befehls Artikel zum Erstellen, der den Vorgang zum Erstellen von Schatten Kopien mithilfe der aktuellen Kontext-und Options Einstellungen startet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 837aa449-9b60-41ae-9ef1-ef67af6e5918
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4d29285517ca678a15828079c95663fc4d501eaf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846833"
---
# <a name="create"></a>erstellen

Startet den Vorgang zum Erstellen von Schatten Kopien mithilfe der aktuellen Kontext-und Options Einstellungen. Erfordert mindestens ein Volume im Schattenkopiesatz.

## <a name="syntax"></a>Syntax

```
create
```

## <a name="remarks"></a>Hinweise

-   Sie müssen mindestens ein Volume mit dem Befehl " **Volume hinzufügen** " hinzufügen, bevor Sie den Befehl " **Create** " verwenden können.
-   Mit dem Befehl **Sicherung starten** können Sie anstelle einer Kopiesicherung eine vollständige Sicherung angeben.
-   Nachdem Sie den **Create** -Befehl ausgeführt haben, können Sie mit dem Befehl **exec** ein duplikatskript für die Sicherung aus der Schatten Kopie ausführen.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)