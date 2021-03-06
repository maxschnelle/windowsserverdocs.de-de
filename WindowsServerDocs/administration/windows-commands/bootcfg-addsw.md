---
title: bootcfg addsw
description: Referenz Artikel zum Befehl "bootcfg addsw", mit dem Betriebssystem-Lade Optionen für einen angegebenen Betriebssystem Eintrag hinzugefügt werden.
ms.topic: reference
ms.assetid: d8389293-ecd9-42f0-b84b-b9ead4cf52e6
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 45f8d0b567e1fa2bd9e5ddd084e7f63c5d6c6c74
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630363"
---
# <a name="bootcfg-addsw"></a>bootcfg addsw

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt Optionen für das Laden von Betriebssystemen für einen angegebenen Betriebssystem Eintrag hinzu.

## <a name="syntax"></a>Syntax

```
bootcfg /addsw [/s <computer> [/u <domain>\<user> /p <password>]] [/mm <maximumram>] [/bv] [/so] [/ng] /id <osentrylinenum>
```

### <a name="parameters"></a>Parameter

| Benennung | Definition |
| ---- | ---------- |
| `/s <computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Die Standardeinstellung ist der lokale Computer. |
| `/u <domain>\<user>`  | Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der von oder angegeben wird `<user>` `<domain>\<user>` . Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird. |
| `/p <password>` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. |
| `/mm <maximumram>` | Gibt die maximale RAM-Größe (in Megabyte) an, die vom Betriebssystem verwendet werden kann. Der Wert muss größer oder gleich 32 Megabyte sein. |
| /bv | Fügt dem angegebenen die **/basevideo** -Option hinzu `<osentrylinenum>` und leitet das Betriebssystem zur Verwendung des standardmäßigen VGA-Modus für den installierten Videotreiber um. |
| /so | Fügt dem angegebenen die **/SOS** -Option hinzu `<osentrylinenum>` und leitet das Betriebssystem so um, dass Gerätetreiber Namen angezeigt werden, während Sie geladen werden. |
| /ng | Fügt der angegebenen die **/noguiboot** -Option hinzu `<osentrylinenum>` und deaktiviert die Statusanzeige, die vor der Eingabeaufforderung von STRG + ALT + ENTF angezeigt wird. |
| `/id <osentrylinenum>` | Gibt die Betriebssystem-Eintrags Zeilennummer im Abschnitt [Betriebssysteme] der Boot.ini Datei an, der die Betriebssystem-Lade Optionen hinzugefügt werden. Die erste Zeile nach der Abschnitts Kopfzeile [Betriebssystem] ist 1. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

So verwenden Sie den Befehl **bootcfg/addsw** :

```
bootcfg /addsw /mm 64 /id 2
bootcfg /addsw /so /id 3
bootcfg /addsw /so /ng /s srvmain /u hiropln /id 2
bootcfg /addsw /ng /id 2
bootcfg /addsw /mm 96 /ng /s srvmain /u maindom\hiropln /p p@ssW23 /id 2
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [BOOTCFG-Befehl](bootcfg.md)
