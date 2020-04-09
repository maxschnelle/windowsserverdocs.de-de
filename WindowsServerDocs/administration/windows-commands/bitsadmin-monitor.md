---
title: bitsadmin überwachen
description: Windows-Befehls Thema für den **bitadmin-Monitor**, mit dem Aufträge in der Übertragungs Warteschlange überwacht werden, deren Besitzer der aktuelle Benutzer ist.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2c424d27-e011-49c2-b579-a2c235467c39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bda268afd5fda24bba2afb04b32bac9cda9a05bb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850213"
---
# <a name="bitsadmin-monitor"></a>bitsadmin überwachen

Überwacht Aufträge in der Übertragungs Warteschlange, deren Besitzer der aktuelle Benutzer ist.

## <a name="syntax"></a>Syntax

```
bitsadmin /monitor [/allusers] [/refresh <seconds>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| /ALLUSERS | Optional. Überwacht Aufträge für alle Benutzer. Sie müssen über Administratorrechte verfügen, um diesen Parameter zu verwenden. |
| /Refresh | Optional. Aktualisiert die Daten in einem durch `<seconds>`angegebenen Intervall. Das Standard Aktualisierungs Intervall beträgt 5 Sekunden. Drücken Sie STRG + C, um die Aktualisierung zu verhindern. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird die Übertragungs Warteschlange für Aufträge überwacht, die im Besitz des aktuellen Benutzers sind, und die Informationen werden alle 60 Sekunden aktualisiert.

```
C:\>bitsadmin /monitor /refresh 60
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)