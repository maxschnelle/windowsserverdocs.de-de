---
title: ftp prompt
description: Referenz Artikel für den Befehl FTP prompt, bei dem der Eingabe Aufforderungs Modus ein-und ausgeschaltet wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 930df39b-45c4-4e0b-bfe2-1d1963be817a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e0859d3989a054d03421f08f5df7823a690dc85c
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933108"
---
# <a name="ftp-prompt"></a>ftp prompt

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Schaltet den Eingabe Aufforderungs Modus ein und aus. Standardmäßig ist der Eingabe Aufforderungs Modus aktiviert. Wenn der Eingabe Aufforderungs Modus aktiviert ist, fordert der FTP-Befehl bei mehreren Dateiübertragungen dazu auf, Dateien selektiv abzurufen oder zu speichern.

> [!NOTE]
> Sie können die Befehle [FTP mget](ftp-mget.md) und [ftp mput](ftp-mput_1.md) verwenden, um alle Dateien zu übertragen, wenn der Eingabe Aufforderungs Modus deaktiviert ist.

## <a name="syntax"></a>Syntax

```
prompt
```

### <a name="examples"></a>Beispiele

Um den Eingabe Aufforderungs Modus ein-und auszuschalten, geben Sie Folgendes ein:

```
prompt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
