---
title: ftp user
description: Referenz Artikel für den FTP-Benutzer Befehl, der einen Benutzer für den Remote Computer angibt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0a77bfeb-27a9-4f2f-a3c4-2fef529fb569
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9b1eea449765b58461d410f0e015d4978c3ad016
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86957352"
---
# <a name="ftp-user"></a>ftp user

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Gibt einen Benutzer für den Remote Computer an.

## <a name="syntax"></a>Syntax

```
user <username> [<password>] [<account>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<username>` | Gibt einen Benutzernamen an, mit dem sich beim Remote Computer anmelden soll. |
| `[<password>]` | Gibt das Kennwort für den *Benutzernamen*an. Wenn kein Kennwort angegeben ist, aber erforderlich ist, fordert der **FTP** -Befehl das Kennwort an. |
| `[<account>]` | Gibt ein Konto an, mit dem Sie sich beim Remote Computer anmelden können. Wenn kein *Konto* angegeben ist, aber erforderlich ist, fordert der **FTP** -Befehl das Konto an. |

### <a name="examples"></a>Beispiele

Um *User1* mit dem Kennwort *Password1*anzugeben, geben Sie Folgendes ein:

```
user User1 Password1
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
