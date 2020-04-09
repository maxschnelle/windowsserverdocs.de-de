---
title: bitsadmin getcreationtime
description: Windows-Befehls Thema für **bigsadmin getkreationtime**, das die Erstellungszeit für den angegebenen Auftrag abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: be409cb5-ce72-41d9-aafa-edd4e230fd14
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cd8f718e53cc44dc5f4c6f5ff09c9a5c201e0564
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850743"
---
# <a name="bitsadmin-getcreationtime"></a>bitsadmin getcreationtime

Ruft die Erstellungszeit für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getcreationtime <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird die Erstellungszeit für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\>bitsadmin /getcreationtime myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)