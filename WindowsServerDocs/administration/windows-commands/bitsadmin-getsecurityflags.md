---
title: bitsadmin getsecurityflags
description: Referenz Artikel für den bitadmin getsecurityflags-Befehl, der die http-sicherheitsflags für die URL-Umleitung und die bei der Übertragung ausgeführten Prüfungen auf dem Serverzertifikat meldet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c2e73519-34f4-487b-af11-97d5d08ef9bb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8613f2bd293bdbf7680aa730ec6fc222ffcfe158
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926687"
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
