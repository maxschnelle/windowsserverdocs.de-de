---
title: 'BI-admin getproxylist: Ruft die Proxy Liste für den angegebenen Auftrag ab.'
description: Windows-Befehls Thema für **bigsadmin getproxylist**, das die Proxy Liste für den angegebenen Auftrag abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: eebfa727-d8f1-4ae3-9382-6d8ffe8c3df3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0c0d26fb074bd1b792caa7fe2ce8fd31b64365e2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850523"
---
# <a name="bitsadmin-getproxylist"></a>bitsadmin getproxylist

Ruft die durch Trennzeichen getrennte Liste der Proxy Server ab, die für den angegebenen Auftrag verwendet werden sollen.

## <a name="syntax"></a>Syntax

```
bitsadmin /getproxylist <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird die Proxy Liste für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\>bitsadmin /getproxylist myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)