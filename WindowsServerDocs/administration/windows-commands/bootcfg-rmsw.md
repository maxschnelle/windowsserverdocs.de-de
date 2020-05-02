---
title: bootcfg rmsw
description: Referenz Thema für den Befehl "bootcfg Rmsw", mit dem die Optionen für das Laden von Betriebssystemen für einen angegebenen Betriebssystem Eintrag entfernt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fd7e4248-880e-4e2b-929e-87f8d44b9a63
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 41c9819fb3d669b24a5918077bef960869625a15
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82708913"
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
| `/s <computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer. |
| `/u <domain>\<user>`  | Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der `<user>` von `<domain>\<user>`oder angegeben wird. Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird. |
| `/p <password>` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. |
| /mm | Entfernt die/Maxmem-Option und den zugehörigen maximalen Speicher Wert aus dem `<osentrylinenum>`angegebenen. Die Option/MAXMEM gibt die maximale RAM-Größe an, die vom Betriebssystem verwendet werden kann. |
| /bv | Entfernt die/basevideo-Option aus dem `<osentrylinenum>`angegebenen. Die Option/basevideo weist das Betriebssystem an, den standardmäßigen VGA-Modus für den installierten Videotreiber zu verwenden. |
| /so | Entfernt die/SOS-Option aus dem `<osentrylinenum>`angegebenen. Die Option/SOS weist das Betriebssystem an, beim Laden Gerätetreiber Namen anzuzeigen. |
| /ng | Entfernt die/noguiboot-Option aus dem `<osentrylinenum>`angegebenen. Die Option/noguiboot deaktiviert die Statusanzeige, die vor der Eingabeaufforderung von STRG + ALT + ENTF angezeigt wird. |
| `/id <osentrylinenum>` | Gibt die Betriebssystem-Eintrags Zeilennummer im Abschnitt [Betriebssysteme] der Datei Boot. ini an, der die Betriebssystem-Lade Optionen hinzugefügt werden. Die erste Zeile nach der Abschnitts Kopfzeile [Betriebssystem] ist 1. |
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [BOOTCFG-Befehl](bootcfg.md)
