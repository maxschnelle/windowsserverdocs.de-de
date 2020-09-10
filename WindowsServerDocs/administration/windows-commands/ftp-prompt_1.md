---
title: ftp prompt
description: Referenz Artikel für den Befehl FTP prompt, bei dem der Eingabe Aufforderungs Modus ein-und ausgeschaltet wird.
ms.topic: reference
ms.assetid: 930df39b-45c4-4e0b-bfe2-1d1963be817a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d045e72ace4364b1ab8832efa35728dc3af2b123
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89624765"
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

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
