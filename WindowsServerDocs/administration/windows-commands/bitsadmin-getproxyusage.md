---
title: bitsadmin getproxyusage
description: Referenz Thema für den bizadmin-Befehl getproxyusage, der die Proxy Verwendungs Einstellung für den angegebenen Auftrag abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f940a70e-3b02-497e-a47f-b37b905c299e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 13a3f216b1ed3c77dbbefee37d73a657525daa36
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717650"
---
# <a name="bitsadmin-getproxyusage"></a>bitsadmin getproxyusage

Ruft die Proxy Verwendungs Einstellung für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getproxyusage <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

#### <a name="output"></a>Output

Die zurückgegebenen Proxy Verwendungs Werte können wie folgt lauten:

- **Preconfig** : Verwenden Sie die Internet Explorer-Standardeinstellungen des Besitzers.

- **No_Proxy** : keinen Proxy Server verwenden.

- Über **Schreiben** : Verwenden Sie eine explizite Proxy Liste.

- **Autodetect** : die Proxy Einstellungen werden automatisch erkannt.

## <a name="examples"></a>Beispiele

So rufen Sie die Proxy Verwendung für den Auftrag mit dem Namen *mydownloadjob*ab

```
bitsadmin /getproxyusage myDownloadJob
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
