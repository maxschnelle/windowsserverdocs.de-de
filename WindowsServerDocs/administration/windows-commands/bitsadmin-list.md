---
title: bitsadmin Liste
description: Windows-Befehls Thema für die **bitadmin-Liste**, die die Übertragungs Aufträge auflistet, die sich im Besitz des aktuellen Benutzers befinden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1416965e-e0e6-49cf-b1d4-b286d3cf8716
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1883da7bfa71a41952f6f67e25eca4dbbdd3353c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850323"
---
# <a name="bitsadmin-list"></a>bitsadmin Liste

Listet die Übertragungs Aufträge auf, die sich im Besitz des aktuellen Benutzers befinden.

## <a name="syntax"></a>Syntax

```
bitsadmin /list [/allusers][/verbose]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| /ALLUSERS | Optional. Listet die Aufträge für alle Benutzer auf. Sie müssen über Administratorrechte verfügen, um diesen Parameter zu verwenden. |
| /verbose | Optional. Stellt ausführliche Informationen zu jedem Auftrag bereit. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel werden Informationen zu Aufträgen abgerufen, die sich im Besitz des aktuellen Benutzers befinden.

```
C:\>bitsadmin /list
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)