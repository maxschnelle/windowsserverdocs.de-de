---
title: bitsadmin cancel
description: 'Windows-Befehle Thema **Bitsadmin Abbrechen** : entfernt den Auftrag aus der Übertragungswarteschlange und löscht alle temporären Dateien, die dem Auftrag zugeordnet.'
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7374b544-6a16-4d3e-872c-dcf4c02ad89d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0a4d1e2d6e4fd66cb525316f236d070fcd72d73f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814071"
---
# <a name="bitsadmin-cancel"></a>bitsadmin cancel

Entfernt den Auftrag aus der Übertragungswarteschlange, und löscht alle temporären Dateien, die dem Auftrag zugeordnet.

## <a name="syntax"></a>Syntax

```
bitsadmin /cancel <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="BKMK_examples"></a>Beispiele für

Im folgenden Beispiel wird die *MyDownloadJob* Auftrags, aus der Übertragungswarteschlange.
```
C:\>bitsadmin /cancel myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)