---
title: ftp user
description: Referenz Artikel für den FTP-Benutzer Befehl, der einen Benutzer für den Remote Computer angibt.
ms.topic: article
ms.assetid: 0a77bfeb-27a9-4f2f-a3c4-2fef529fb569
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bd015b7f84a6f5a4f3ee10a3cbe351a5bfa4a563
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87888823"
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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
