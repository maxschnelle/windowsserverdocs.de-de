---
title: bitsadmin geterrorcount
description: Referenz Artikel für den Befehl bizadmin GetErrorCount, der die Anzahl der Male abruft, mit denen der angegebene Auftrag einen vorübergehenden Fehler generiert hat.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8840ae78-52b0-4c7e-b592-0547359a237e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 90eaa150f2decba4bbee693ac117cd269d5a7c97
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923056"
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

## <a name="examples"></a>Beispiele

So rufen Sie Fehler Anzahl Informationen für den Auftrag mit dem Namen *mydownloadjob*ab:

```
bitsadmin /geterrorcount myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
