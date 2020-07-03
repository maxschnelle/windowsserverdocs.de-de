---
title: wbadmin get disks
description: Referenz Artikel für Wbadmin Get Disks, der die internen und externen Datenträger auflistet, die derzeit für den lokalen Computer online sind.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 320edef1-df11-446b-a183-9f81811ef938
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e9a479b3509939c17ab986ce68c9a057ac3e773c
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932132"
---
# <a name="wbadmin-get-disks"></a>wbadmin get disks



Listet die internen und externen Datenträger auf, die derzeit für den lokalen Computer online sind.

Zum Auflisten der Datenträger, die mit diesem Unterbefehl online sind, müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder der Gruppe " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen. (Klicken Sie zum Öffnen einer Eingabeaufforderung mit erhöhten Rechten mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.)

## <a name="syntax"></a>Syntax

```
wbadmin get disks
```

### <a name="parameters"></a>Parameter

Dieser Unterbefehl weist keine Parameter auf.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   Cmdlet " [Get-wbdisk](https://technet.microsoft.com/library/jj902446.aspx) "