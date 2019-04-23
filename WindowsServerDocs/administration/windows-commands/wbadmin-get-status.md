---
title: wbadmin get status
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2911b944-7b95-46aa-8c1e-1d55a2fcc94c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 35fd640aa56bca7c5f5d6f3901fe095d0b8a73cc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863411"
---
# <a name="wbadmin-get-status"></a>wbadmin get status



Meldet den Status des Vorgangs sichern oder wiederherstellen, die derzeit ausgeführt wird.

Um dieses Unterbefehl verwenden zu können, muss Sie Mitglied der **Sicherungs-Operatoren** Gruppe oder der **Administratoren** Gruppe, oder Sie wurde die entsprechenden Berechtigungen delegiert. Darüber hinaus müssen Sie ausführen **Wbadmin** eine Eingabeaufforderung mit erhöhten Rechten. (Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.)

## <a name="syntax"></a>Syntax

```
wbadmin get status
```

## <a name="parameters"></a>Parameter

Dieses Unterbefehl hat keine Parameter.

## <a name="remarks"></a>Hinweise

-   Dieses Unterbefehl wird nicht beendet, bis die aktuelle Sicherung oder Wiederherstellung abgeschlossen ist, der Unterbefehl wird weiterhin ausgeführt, auch wenn Sie das Befehlsfenster schließen.
-   Wenn Sie die aktuelle Sicherung oder Wiederherstellung beenden möchten, verwenden Sie die **Auftrag zum Beenden des Wbadmin** Unterbefehl.

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Get-WBJob](https://technet.microsoft.com/library/jj902426.aspx) cmdlet