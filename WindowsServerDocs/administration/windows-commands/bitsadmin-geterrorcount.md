---
title: bitsadmin geterrorcount
description: Referenz Artikel für den Befehl bizadmin GetErrorCount, der die Anzahl der Male abruft, mit denen der angegebene Auftrag einen vorübergehenden Fehler generiert hat.
ms.topic: reference
ms.assetid: 8840ae78-52b0-4c7e-b592-0547359a237e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1b6a4d3f0e77d8ffc0d7e538affe0fb8e77a5281
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89030348"
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
