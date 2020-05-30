---
title: Telnet nicht festgelegt
description: Referenz Thema für die Unmenge von Telnet, die zuvor festgelegte Optionen deaktiviert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: da9a0d99-1930-4858-93c7-0e9c3797ee09
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1d2ae8c3e96e0416a8b9f5f477778e5e89339842
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222658"
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
|logging|Schaltet die Protokollierung aus.|
|ntlm|Deaktiviert die NTLM-Authentifizierung.|
|?|Zeigt die Hilfe für diesen Befehl an.|
## <a name="examples"></a>Beispiele
Deaktivieren Sie die Protokollierung.
```
u logging
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
