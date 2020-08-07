---
title: bitsadmin reset
description: Referenz Artikel für den Befehl bizadmin Reset, der alle Aufträge in der Übertragungs Warteschlange des aktuellen Benutzers abbricht.
ms.topic: article
ms.assetid: 0e4f9d1d-072c-493f-8d7a-f6d713c3ef29
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b28ad601a40a9646ad64268aaca0320ea5165efd
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893334"
---
# <a name="bitsadmin-reset"></a>bitsadmin reset

Bricht alle Aufträge in der Übertragungs Warteschlange ab, die im Besitz des aktuellen Benutzers sind. Die vom lokalen System erstellten Aufträge können nicht zurückgesetzt werden. Stattdessen müssen Sie Administrator sein und den Taskplaner verwenden, um diesen Befehl mithilfe der Anmelde Informationen für das lokale System als Task zu planen.

> [!NOTE]
> Wenn Sie über Administratorrechte in BI-admin 1,5 und früher verfügen, werden alle Aufträge in der Warteschlange durch den Schalter/Reset abgebrochen. Darüber hinaus wird die/ALLUSERS-Option nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /reset [/allusers]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| /ALLUSERS | Optional. Bricht alle Aufträge in der Warteschlange ab, die sich im Besitz des aktuellen Benutzers befinden. Sie müssen über Administratorrechte verfügen, um diesen Parameter zu verwenden. |

## <a name="examples"></a>Beispiele

, Wenn alle Aufträge in der Übertragungs Warteschlange für den aktuellen Benutzer abgebrochen werden sollen.

```
bitsadmin /reset
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
