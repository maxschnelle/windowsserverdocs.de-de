---
title: bitsadmin getproxyusage
description: Windows-Befehls Thema für **biungadmin getproxyusage**, das die Proxy Verwendungs Einstellung für den angegebenen Auftrag abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f940a70e-3b02-497e-a47f-b37b905c299e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 01c9bb9a1d413fa847482f652e18eed30ad76109
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850513"
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

## <a name="remarks"></a>Hinweise

Die Proxy Verwendungs Werte umfassen Folgendes:

- **Preconfig** : Verwenden Sie die Internet Explorer-Standardeinstellungen des Besitzers.

- **No_Proxy** : keinen Proxy Server verwenden.

- Über **Schreiben** : Verwenden Sie eine explizite Proxy Liste.

- **Autodetect** : die Proxy Einstellungen werden automatisch erkannt.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird die Proxy Verwendung für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\>bitsadmin /getproxyusage myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)