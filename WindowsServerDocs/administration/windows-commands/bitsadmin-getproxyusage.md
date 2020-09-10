---
title: bitsadmin getproxyusage
description: Referenz Artikel für den Befehl bizadmin getproxyusage, der die Einstellung für die Proxy Verwendung für den angegebenen Auftrag abruft.
ms.topic: reference
ms.assetid: f940a70e-3b02-497e-a47f-b37b905c299e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: bdfcfa92a5886857920d56a0028a450ee9a3e521
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631735"
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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
