---
title: bitsadmin geterrorcount
description: Windows-Befehls Thema für bizadmin GetErrorCount, das die Anzahl der Versuche abruft, mit denen der angegebene Auftrag einen vorübergehenden Fehler generiert hat.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8840ae78-52b0-4c7e-b592-0547359a237e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1711781dd416311e45874b7c611f3f8f42a06854
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850693"
---
# <a name="bitsadmin-geterrorcount"></a>bitsadmin geterrorcount

Ruft ab, wie oft der angegebene Auftrag einen vorübergehenden Fehler generiert hat.

## <a name="syntax"></a>Syntax

```
bitsadmin /geterrorcount <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel werden Fehler Anzahl Informationen für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\>bitsadmin /geterrorcount myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)