---
title: erstellen
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 70a8f53d9cb90fc36a76b11de2f93da71874617a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881271"
---
# <a name="create"></a>erstellen



Startet die Erstellung Schattenkopie, mit den aktuellen Kontext und die Option Einstellungen an. Erfordert mindestens ein Volume in den Schatten kopieren festgelegt.

## <a name="syntax"></a>Syntax

```
create
```

## <a name="remarks"></a>Hinweise

-   Sie müssen mindestens ein Volume mit Hinzufügen der **Volume hinzufügen** Befehl vor der Verwendung der **erstellen** Befehl.
-   Können Sie die **Sicherung beginnen** Befehl, um eine vollständige Sicherung anstelle einer kopiesicherung anzugeben.
-   Nach dem Ausführen der **erstellen** Befehl können Sie die **Exec** Befehl aus, um eine Duplizierung-Skript für die Sicherung aus der Schattenkopie ausgeführt.

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)