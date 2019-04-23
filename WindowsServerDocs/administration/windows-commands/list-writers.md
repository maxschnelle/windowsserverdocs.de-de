---
title: Liste Writer
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1c30cbc4-f568-4fa7-b564-66c41d3ca82d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6fbab6644d46dbb352a5d5a51abefb293f3ffe6f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866741"
---
# <a name="list-writers"></a>Liste Writer



Listen-Writer, die im System befinden. Wenn Sie ohne Angabe von Parametern **Liste** zeigt die Ausgabe für **Liste Metadaten** standardmäßig.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
list writers [metadata | detailed | status]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|metadata|Listet die Identität und den Status des Schreibers und Metadaten, wie z. B. Details zu den Komponenten und ausgeschlossene Dateien zeigt. Dies ist der Standardparameter.|
|Ausführliche|Listet die gleiche Informationen wie **Metadaten**, aber **ausführliche** enthält die vollständige Liste der für alle Komponenten.|
|status|Listet nur die Identität und den Status der registrierten Writer auf.|

## <a name="BKMK_examples"></a>Beispiele für

Um nur die Identität und den Status des Schreibers aufzulisten, geben Sie Folgendes ein:
```
list writers status
```
Die Ausgabe, die an der folgenden ähnlich ist:
```
Listing writer status ...
* WRITER "System Writer"
        - Status: 5 (VSS_WS_WAITING_FOR_BACKUP_COMPLETE)
        - Writer Failure code: 0x00000000 (S_OK)
        - Writer ID: {e8132975-6f93-4464-a53e-1050253ae220}
        - Instance ID: {7e631031-c695-4229-9da1-a7de057e64cb}
* WRITER "Shadow Copy Optimization Writer"
        - Status: 1 (VSS_WS_STABLE)
        - Writer Failure code: 0x00000000 (S_OK)
        - Writer ID: {4dc3bdd4-ab48-4d07-adb0-3bee2926fd7f}
        - Instance ID: {9e362607-9794-4dd4-a7cd-b3d5de0aad20}
...
...
...
* WRITER "Registry Writer"
        - Status: 1 (VSS_WS_STABLE)
        - Writer Failure code: 0x00000000 (S_OK)
        - Writer ID: {afbab4a2-367d-4d15-a586-71dbb18f8485}
        - Instance ID: {e87ba7e3-f8d8-42d8-b2ee-c76ae26b98e8}
8 writers listed. 
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)