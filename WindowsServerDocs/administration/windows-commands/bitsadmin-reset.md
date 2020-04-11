---
title: bitsadmin zurücksetzen
description: Windows-Befehls Artikel zum **Zurücksetzen von bitadmin**, bei dem alle Aufträge in der Übertragungs Warteschlange des aktuellen Benutzers abgebrochen werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0e4f9d1d-072c-493f-8d7a-f6d713c3ef29
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b73bd3b9c66b24330a0f9444836b9c8bd1730722
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123083"
---
# <a name="bitsadmin-reset"></a>bitsadmin zurücksetzen

Bricht alle Aufträge in der Übertragungs Warteschlange ab, die im Besitz des aktuellen Benutzers sind. > Sie keine Aufträge zurücksetzen können, die vom lokalen System erstellt wurden. Stattdessen müssen Sie Administrator sein und den Taskplaner verwenden, um diesen Befehl mithilfe der Anmelde Informationen für das lokale System als Task zu planen.

> [!NOTE]
> Wenn Sie in BI-admin 1,5 und früher über Administratorrechte verfügen, werden die Aufträge in der Warteschlange durch den Schalter/Reset abgebrochen. Darüber hinaus wird die/ALLUSERS-Option nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /reset [/allusers]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| /ALLUSERS | Optional. Bricht alle Aufträge in der Warteschlange ab, die sich im Besitz des aktuellen Benutzers befinden. Sie müssen über Administratorrechte verfügen, um diesen Parameter zu verwenden. |

## <a name="examples"></a>Beispiele

Im folgenden Beispiel werden alle Aufträge in der Übertragungs Warteschlange des aktuellen Benutzers abgebrochen.

```
C:\>bitsadmin /reset
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)