---
title: bitsadmin getproxyusage
description: Referenz Artikel für den Befehl bizadmin getproxyusage, der die Einstellung für die Proxy Verwendung für den angegebenen Auftrag abruft.
ms.topic: reference
ms.assetid: f940a70e-3b02-497e-a47f-b37b905c299e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 423168d72a88ecad90fd8de43eab3cb4486a750b
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024404"
---
# <a name="bitsadmin-getproxyusage"></a>bitsadmin getproxyusage

Ruft die Proxy Verwendungs Einstellung für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getproxyusage <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
