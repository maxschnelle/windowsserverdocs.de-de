---
title: bitadmin getsecurityflags
description: Windows-Befehls Thema für **bitadmin getsecurityflags**, das die http-sicherheitsflags für die URL-Umleitung und die bei der Übertragung ausgeführten Prüfungen auf dem Serverzertifikat meldet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c2e73519-34f4-487b-af11-97d5d08ef9bb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 360f8d5514e5251dd9e4a6a6b60335dc34fe4415
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850473"
---
# <a name="bitsadmin-getsecurityflags"></a>bitadmin getsecurityflags

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Meldet die http-sicherheitsflags für die URL-Umleitung und Überprüfungen, die für das Serverzertifikat während der Übertragung ausgeführt werden.

## <a name="syntax"></a>Syntax

```
bitsadmin /getsecurityflags <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel werden die sicherheitsflags von einem Auftrag mit dem Namen *mydownloadjob*abgerufen.

```
C:\>bitsadmin /getsecurityflags myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)