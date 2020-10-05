---
title: telnet set
description: Referenz Artikel für den Telnet-SET-Befehl, mit dem Optionen festgelegt werden.
ms.topic: reference
ms.assetid: 67316b5f-9c6f-43e3-86d5-dcff9ae2ac3e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 05678eaa3c4308f72ef4a754cc3e352826fa473a
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91717977"
---
# <a name="telnet-set"></a>Telnet: Set

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt Optionen fest. Sie können den [Befehl Telnet Festlegung](telnet-unset.md) verwenden, um eine Option zu deaktivieren, die zuvor festgelegt wurde.

## <a name="syntax"></a>Syntax

```
set [bsasdel] [crlf] [delasbs] [escape <char>] [localecho] [logfile <filename>] [logging] [mode {console | stream}] [ntlm] [term {ansi | vt100 | vt52 | vtnt}] [?]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| bsasdel | Sendet **Rückraum** als **Lösch**Vorgang. |
| CRLF | Sendet CR & LF (0x0D, 0x 0A), wenn die **Eingabe** Taste gedrückt wird. Wird als **neuer Zeilen Modus**bezeichnet. |
| Delta- | Sendet **Delete** als **RÜCKTASTE**. |
| Weg `<character>` | Legt das Escapezeichen fest, mit dem die Telnet-Client Eingabeaufforderung eingegeben wird. Das Escapezeichen kann ein einzelnes Zeichen oder eine Kombination aus der **STRG** -Taste und einem Zeichen sein. Halten Sie zum Festlegen einer Tastenkombination die **STRG** -Taste gedrückt, während Sie das Zeichen eingeben, das Sie zuweisen möchten. |
| LOCALECHO | Schaltet das lokale Echo ein. |
| Protokolldatei `<filename>` | Protokolliert die aktuelle Telnet-Sitzung in der lokalen Datei. Die Protokollierung beginnt automatisch, wenn Sie diese Option festlegen. |
| logging | Schaltet die Protokollierung ein. Wenn keine Protokolldatei festgelegt ist, wird eine Fehlermeldung angezeigt. |
| Spar `{console | stream}` | Legt den Betriebsmodus fest. |
| ntlm | Schaltet die NTLM-Authentifizierung ein. |
| zeitig `{ansi | vt100 | vt52 | vtnt}` | Legt den Terminaltyp fest. |
| ? | Zeigt die Hilfe für diesen Befehl an. |

#### <a name="remarks"></a>Bemerkungen

- In nicht englischsprachigen Versionen von Telnet ist das **Codeset** `<option>` verfügbar. **Codesatz** `<option>` Legt den aktuellen Code fest, der auf eine Option festgelegt ist. dabei kann es sich um einen der folgenden handeln: **Shift JIS**, **Japanese EUC**, **JIS Kanji**, **JIS Kanji (78)**, **Dec**Kanji, **NEC Kanji**. Sie sollten den gleichen Code festlegen, der auf dem Remote Computer festgelegt ist.

## <a name="example"></a>Beispiel

Geben Sie Folgendes ein, um die Protokolldatei festzulegen und die Protokollierung für die lokale Datei *tnlog.txt*zu starten:

```
set logfile tnlog.txt
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
