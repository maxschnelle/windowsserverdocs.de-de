---
title: FTP-Eingabeaufforderung
description: Referenz Thema für den Befehl FTP prompt, bei dem der Eingabe Aufforderungs Modus ein-und ausgeschaltet wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 930df39b-45c4-4e0b-bfe2-1d1963be817a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 57f0e1eead36665c19845944bf22325b1aecebbb
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820380"
---
# <a name="ftp-prompt"></a>FTP-Eingabeaufforderung

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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
