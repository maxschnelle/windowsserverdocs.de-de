---
title: bootcfg rmsw
description: Referenz Artikel zum Befehl "bootcfg Rmsw", bei dem die Lade Optionen für das Betriebssystem für einen angegebenen Betriebssystem Eintrag entfernt werden.
ms.topic: article
ms.assetid: fd7e4248-880e-4e2b-929e-87f8d44b9a63
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2ffe80c6a95421a66a1aebd119664c9e4f68952d
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880541"
---
# <a name="bootcfg-rmsw"></a>bootcfg rmsw

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Entfernt Optionen für das Laden von Betriebssystemen für einen angegebenen Betriebssystem Eintrag.

## <a name="syntax"></a>Syntax

```
bootcfg /rmsw [/s <computer> [/u <domain>\<user> /p <password>]] [/mm] [/bv] [/so] [/ng] /id <osentrylinenum>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `/s <computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Die Standardeinstellung ist der lokale Computer. |
| `/u <domain>\<user>`  | Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der von oder angegeben wird `<user>` `<domain>\<user>` . Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird. |
| `/p <password>` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. |
| /mm | Entfernt die/Maxmem-Option und den zugehörigen maximalen Speicher Wert aus dem angegebenen `<osentrylinenum>` . Die Option/MAXMEM gibt die maximale RAM-Größe an, die vom Betriebssystem verwendet werden kann. |
| /bv | Entfernt die/basevideo-Option aus dem angegebenen `<osentrylinenum>` . Die Option/basevideo weist das Betriebssystem an, den standardmäßigen VGA-Modus für den installierten Videotreiber zu verwenden. |
| /so | Entfernt die/SOS-Option aus dem angegebenen `<osentrylinenum>` . Die Option/SOS weist das Betriebssystem an, beim Laden Gerätetreiber Namen anzuzeigen. |
| /ng | Entfernt die/noguiboot-Option aus dem angegebenen `<osentrylinenum>` . Die Option/noguiboot deaktiviert die Statusanzeige, die vor der Eingabeaufforderung von STRG + ALT + ENTF angezeigt wird. |
| `/id <osentrylinenum>` | Gibt die Betriebssystem-Eintrags Zeilennummer im Abschnitt [Betriebssysteme] der Boot.ini Datei an, der die Betriebssystem-Lade Optionen hinzugefügt werden. Die erste Zeile nach der Abschnitts Kopfzeile [Betriebssystem] ist 1. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

So verwenden Sie den Befehl **bootcfg/Rmsw** :

```
bootcfg /rmsw /mm 64 /id 2
bootcfg /rmsw /so /id 3
bootcfg /rmsw /so /ng /s srvmain /u hiropln /id 2
bootcfg /rmsw /ng /id 2
bootcfg /rmsw /mm 96 /ng /s srvmain /u maindom\hiropln /p p@ssW23 /id 2
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [BOOTCFG-Befehl](bootcfg.md)
