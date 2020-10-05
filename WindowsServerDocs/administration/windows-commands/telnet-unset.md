---
title: telnet unset
description: Referenz Artikel für den Telnet-Festlegung-Befehl, der zuvor festgelegte Optionen deaktiviert.
ms.topic: reference
ms.assetid: da9a0d99-1930-4858-93c7-0e9c3797ee09
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 51604615e989325b2e5719d02c51f70dfd84bd0c
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91717917"
---
# <a name="telnet-unset"></a>Telnet: nicht festgelegt

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Deaktiviert zuvor festgelegte Optionen.

## <a name="syntax"></a>Syntax

```
u {bsasdel | crlf | delasbs | escape | localecho | logging | ntlm} [?]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| bsasdel | Sendet **Rückraum** als **RÜCKTASTE**. |
| CRLF | Sendet die **Eingabe** Taste als CR. Wird auch als Zeilenvorschub Modus bezeichnet. |
| Delta- | Sendet **Delete** als **Delete**. |
| Escape | Entfernt die Einstellung für das Escapezeichen. |
| LOCALECHO | Deaktiviert LOCALECHO. |
| logging | Schaltet die Protokollierung aus. |
| ntlm | Deaktiviert die NTLM-Authentifizierung. |
| ? | Zeigt die Hilfe für diesen Befehl an. |

## <a name="example"></a>Beispiel

Deaktivieren Sie die Protokollierung.

```
u logging
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
