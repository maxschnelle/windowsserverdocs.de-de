---
title: bitsadmin getsecurityflags
description: Referenz Artikel für den bitadmin getsecurityflags-Befehl, der die http-sicherheitsflags für die URL-Umleitung und die bei der Übertragung ausgeführten Prüfungen auf dem Serverzertifikat meldet.
ms.topic: reference
ms.assetid: c2e73519-34f4-487b-af11-97d5d08ef9bb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 39e5df028d687de22e8e6bf54731bf0067cd5319
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89034858"
---
# <a name="bitsadmin-getsecurityflags"></a>bitsadmin getsecurityflags

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Meldet die http-sicherheitsflags für die URL-Umleitung und Überprüfungen, die für das Serverzertifikat während der Übertragung ausgeführt werden.

## <a name="syntax"></a>Syntax

```
bitsadmin /getsecurityflags <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie die sicherheitsflags von einem Auftrag mit dem Namen *mydownloadjob*ab

```
bitsadmin /getsecurityflags myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
