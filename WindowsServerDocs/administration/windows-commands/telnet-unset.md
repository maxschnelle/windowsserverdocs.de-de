---
title: telnet unset
description: Referenz Artikel für die Unmenge von Telnet, die zuvor festgelegte Optionen deaktiviert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: da9a0d99-1930-4858-93c7-0e9c3797ee09
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3efbf7d4f2507d16dbe0beb704ab0c80467a56d3
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935292"
---
# <a name="telnet-unset"></a>Telnet: nicht festgelegt

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Deaktiviert zuvor festgelegte Optionen.

## <a name="syntax"></a>Syntax
```
u[nset] {bsasdel | crlf | delasbs | escape | localecho | logging | ntlm} [?]
```
#### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|bsasdel|Sendet **Rückraum** als **RÜCKTASTE**.|
|CRLF|Sendet die **Eingabe** Taste als CR. Wird auch als Zeilenvorschub Modus bezeichnet.|
|Delta-|Sendet **Delete** als **Delete**.|
|Escape|entfernt die Einstellung für das Escapezeichen.|
|LOCALECHO|Deaktiviert LOCALECHO.|
|Protokollierung|Schaltet die Protokollierung aus.|
|ntlm|Deaktiviert die NTLM-Authentifizierung.|
|?|Zeigt die Hilfe für diesen Befehl an.|
## <a name="examples"></a>Beispiele
Deaktivieren Sie die Protokollierung.
```
u logging
```
## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
