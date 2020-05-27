---
title: gpresult
description: Referenz Thema für den Gpresult-Befehl, der die Richtlinien Ergebnissatz-Informationen (RSoP) für einen Remote Benutzer und-Computer anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dfaa3adf-2c83-486c-86d6-23f93c5c883c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e88a75a15168baaf2e49ca08ff20d3a8ffb5620c
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83818860"
---
# <a name="gpresult"></a>gpresult

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt die Richtlinien Ergebnissatz-Informationen (RSoP) für einen Remote Benutzer und-Computer an. Um die RSoP-Berichterstellung für Remote Zielcomputer über die Firewall verwenden zu können, müssen Sie über Firewallregeln verfügen, die eingehenden Netzwerk Datenverkehr für die Ports zulassen.

## <a name="syntax"></a>Syntax

```
gpresult [/s <system> [/u <username> [/p [<password>]]]] [/user [<targetdomain>\]<targetuser>] [/scope {user | computer}] {/r | /v | /z | [/x | /h] <filename> [/f] | /?}
```

> [!NOTE]
> Außer bei Verwendung von **/?** müssen Sie eine Ausgabe Option **/r**, **/v**, **"/z**, **/x**oder **/h**einschließen.

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| /s`<system>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an. Verwenden Sie keine umgekehrten Schrägstriche. Der Standardwert ist der lokale Computer. |
| /u`<username>` | Verwendet die Anmelde Informationen des angegebenen Benutzers, um den Befehl auszuführen. Der Standardbenutzer ist der Benutzer, der auf dem Computer angemeldet ist, der den Befehl ausgibt. |
| /p`[<password>]` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben wird. Wenn **/p** ausgelassen wird, fordert **gpresult** das Kennwort an. Der **/p** -Parameter kann nicht mit **/x** oder **/h**verwendet werden. |
| /User`[<targetdomain>\]<targetuser>]` | Gibt den Remote Benutzer an, dessen RSOP-Daten angezeigt werden sollen. |
| /Scope`{user | computer}` | Zeigt die RSoP-Daten für den Benutzer oder den Computer an. Wenn **/Scope** ausgelassen wird, zeigt **gpresult** RSOP-Daten sowohl für den Benutzer als auch für den Computer an. |
| `[/x | /h] <filename>` | Speichert den Bericht im XML-Format (**/x**) oder im HTML-Format (**/h**) am Speicherort und mit dem Dateinamen, der durch den *filename* -Parameter angegeben wird. Kann nicht mit **/u**, **/p**, **/r**, **/v**oder **"/z**verwendet werden. |
| /f | Erzwingt **gpresult** , den Dateinamen zu überschreiben, der in der **/x** -Option oder der **/h** -Option angegeben ist. |
| /r | Zeigt RSoP-Zusammenfassungs Daten an. |
| /v | Zeigt ausführliche Richtlinien Informationen an. Dies schließt detaillierte Einstellungen ein, die mit einer Rangfolge von 1 angewendet wurden. |
| /z | Zeigt alle verfügbaren Informationen zu Gruppenrichtlinie an. Dies schließt detaillierte Einstellungen ein, die mit einer Rangfolge von 1 und höher angewendet wurden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Gruppenrichtlinie ist das primäre Verwaltungs Tool zum Definieren und Steuern, wie Programme, Netzwerkressourcen und das Betriebssystem für Benutzer und Computer in einer Organisation ausgeführt werden. In einer Active Directory-Umgebung wird Gruppenrichtlinie auf Benutzer oder Computer basierend auf der Mitgliedschaft in Standorten, Domänen oder Organisationseinheiten angewendet.

- Da Sie überlappende Richtlinien Einstellungen auf alle Computer oder Benutzer anwenden können, generiert das Gruppenrichtlinie Feature eine Reihe von Richtlinien Einstellungen, wenn sich der Benutzer anmeldet. Der Befehl **gpresult** zeigt den resultierenden Satz von Richtlinien Einstellungen an, die für den angegebenen Benutzer bei der Anmeldung des Benutzers auf dem Computer erzwungen wurden.

- Da **/v** und **"/z** viele Informationen liefern, ist es hilfreich, die Ausgabe in eine Textdatei umzuleiten (z. b `gpresult/z >policy.txt` .).

### <a name="examples"></a>Beispiele

Zum Abrufen von RSoP-Daten nur für den Remote Benutzer, *maindom\hiropln* mit dem Kennwort, das sich *p@ssW23* auf dem Computer *srvmain*befindet, geben Sie Folgendes ein:

```
gpresult /s srvmain /u maindom\hiropln /p p@ssW23 /user targetusername /scope user /r
```

Wenn Sie alle verfügbaren Informationen über Gruppenrichtlinie in einer *Datei mit dem* Namen " *Policy. txt*" speichern möchten, *p@ssW23* Geben Sie auf dem Computer " *srvmain*" Folgendes ein:

```
gpresult /s srvmain /u maindom\hiropln /p p@ssW23 /user targetusername /z > policy.txt
```

Zum Anzeigen von RSoP-Daten für den angemeldeten Benutzer, *maindom\hiropln* mit dem Kennwort *p@ssW23* für den Computer *srvmain*, geben Sie Folgendes ein:

```
gpresult /s srvmain /u maindom\hiropln /p p@ssW23 /r
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
