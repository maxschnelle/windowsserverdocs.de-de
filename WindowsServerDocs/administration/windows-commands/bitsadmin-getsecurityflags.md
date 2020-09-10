---
title: bitsadmin getsecurityflags
description: Referenz Artikel für den bitadmin getsecurityflags-Befehl, der die http-sicherheitsflags für die URL-Umleitung und die bei der Übertragung ausgeführten Prüfungen auf dem Serverzertifikat meldet.
ms.topic: reference
ms.assetid: c2e73519-34f4-487b-af11-97d5d08ef9bb
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ce0637527b39ebf05546b62671ce11a87151b572
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631707"
---
# <a name="bitsadmin-getsecurityflags"></a>bitsadmin getsecurityflags

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Meldet die http-sicherheitsflags für die URL-Umleitung und Überprüfungen, die für das Serverzertifikat während der Übertragung ausgeführt werden.

## <a name="syntax"></a>Syntax

```
bitsadmin /getsecurityflags <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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
