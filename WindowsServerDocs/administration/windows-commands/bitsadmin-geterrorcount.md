---
title: bitsadmin geterrorcount
description: Windows-Befehls Thema für **bizadmin GetErrorCount**, das die Anzahl der Versuche abruft, mit denen der angegebene Auftrag einen vorübergehenden Fehler generiert hat.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8840ae78-52b0-4c7e-b592-0547359a237e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ef0bf043517d4edfa8d72888746ca5d9c92ecc21
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123136"
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