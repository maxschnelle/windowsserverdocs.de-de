---
title: bitsadmin listfiles
description: Referenz Thema für den bizadmin-Befehl "listFiles", der die Dateien im angegebenen Auftrag auflistet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ad0d1eaa-3bd8-45e5-8f72-4da7366f0d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6826c1ec2f624a06d11fedcb8ca9f14d86b7ec27
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717418"
---
# <a name="bitsadmin-listfiles"></a>bitsadmin listfiles

Listet die Dateien im angegebenen Auftrag auf.

## <a name="syntax"></a>Syntax

```
bitsadmin /listfiles <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie die Liste der Dateien für den Auftrag mit dem Namen *mydownloadjob*ab:

```
bitsadmin /listfiles myDownloadJob
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
