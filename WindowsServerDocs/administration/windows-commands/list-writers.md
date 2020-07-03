---
title: list writers
description: Referenz Artikel für den Befehl auflisten von Writer, in dem die Writer aufgelistet sind, die sich auf dem System befinden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1c30cbc4-f568-4fa7-b564-66c41d3ca82d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a3b4334d9f1f1a76b390a29a1b9cfd877da91185
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931776"
---
# <a name="list-writers"></a>list writers

Listet Writer auf, die sich auf dem System befinden. Bei Verwendung ohne Parameter zeigt **List** standardmäßig die Ausgabe für **Listen Metadaten** an.

## <a name="syntax"></a>Syntax

```
list writers [metadata | detailed | status]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| metadata | Listet die Identität und den Status von Writern auf und zeigt Metadaten wie z. b. Komponenten Details und ausgeschlossene Dateien an. Dies ist der Standardparameter. |
| Details | Listet die gleichen Informationen wie **Metadaten**auf, enthält jedoch auch die vollständige Datei Liste für alle Komponenten. |
| status | Listet nur die Identität und den Status registrierter Writer auf. |

### <a name="examples"></a>Beispiele

Um nur die Identität und den Status von Writern aufzulisten, geben Sie Folgendes ein:

```
list writers status
```

Ausgabe, die den folgenden anzeigen ähnelt:

```
Listing writer status ...
* WRITER System Writer
        - Status: 5 (VSS_WS_WAITING_FOR_BACKUP_COMPLETE)
        - Writer Failure code: 0x00000000 (S_OK)
        - Writer ID: {e8132975-6f93-4464-a53e-1050253ae220}
        - Instance ID: {7e631031-c695-4229-9da1-a7de057e64cb}
* WRITER Shadow Copy Optimization Writer
        - Status: 1 (VSS_WS_STABLE)
        - Writer Failure code: 0x00000000 (S_OK)
        - Writer ID: {4dc3bdd4-ab48-4d07-adb0-3bee2926fd7f}
        - Instance ID: {9e362607-9794-4dd4-a7cd-b3d5de0aad20}
* WRITER Registry Writer
        - Status: 1 (VSS_WS_STABLE)
        - Writer Failure code: 0x00000000 (S_OK)
        - Writer ID: {afbab4a2-367d-4d15-a586-71dbb18f8485}
        - Instance ID: {e87ba7e3-f8d8-42d8-b2ee-c76ae26b98e8}
8 writers listed.
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)