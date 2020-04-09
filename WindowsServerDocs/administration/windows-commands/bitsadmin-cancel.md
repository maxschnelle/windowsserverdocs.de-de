---
title: bitsadmin cancel
description: Windows-Befehls Thema für **bitadmin Cancel**, das den Auftrag aus der Übertragungs Warteschlange entfernt und alle dem Auftrag zugeordneten temporären Dateien löscht.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7374b544-6a16-4d3e-872c-dcf4c02ad89d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5c2bdeef824bc269671cc5ae926fb77cd5726c58
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850833"
---
# <a name="bitsadmin-cancel"></a>bitsadmin cancel

Entfernt den Auftrag aus der Übertragungs Warteschlange und löscht alle temporären Dateien, die dem Auftrag zugeordnet sind.

## <a name="syntax"></a>Syntax

```
bitsadmin /cancel <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird der Auftrag *mydownloadjob* aus der Übertragungs Warteschlange entfernt.

```
C:\>bitsadmin /cancel myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)