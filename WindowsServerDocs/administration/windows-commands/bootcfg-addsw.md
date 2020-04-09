---
title: bootcfg addsw
description: Windows-Befehls Thema für bootcfg addsw, das Optionen für das Laden von Betriebssystemen für einen angegebenen Betriebssystem Eintrag hinzufügt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d8389293-ecd9-42f0-b84b-b9ead4cf52e6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a9ae5175dfc3b068276f6ab95d6823699c96b2b5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848713"
---
# <a name="bootcfg-addsw"></a>bootcfg addsw

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt Optionen für das Laden von Betriebssystemen für einen angegebenen Betriebssystem Eintrag hinzu.

## <a name="syntax"></a>Syntax
```
bootcfg /addsw [/s <computer> [/u <Domain>\<User> /p <Password>]] [/mm <MaximumRAM>] [/bv] [/so] [/ng] /id <OSEntryLineNum>
```
### <a name="parameters"></a>Parameter

|         Begriff         |                                                                                                            Definition                                                                                                            |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>     |                                                        Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer.                                                        |
| /u <Domain>\\<User>  |               Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der durch <User> oder <Domain>\\<User>angegeben wird. Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird.               |
|    /p <Password>     |                                                                      Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist.                                                                       |
|   /mm <MaximumRAM>   |                                          Gibt die maximale RAM-Größe (in Megabyte) an, die vom Betriebssystem verwendet werden kann. Der Wert muss größer oder gleich 32 Megabyte sein.                                          |
|         /bv          |                                    Fügt dem angegebenen <OSEntryLineNum>die Option **/basevideo** hinzu und leitet das Betriebssystem zur Verwendung des standardmäßigen VGA-Modus für den installierten Videotreiber um.                                     |
|         /so          |                                      Fügt dem angegebenen *osentrylinenum*die **/SOS** -Option hinzu und leitet das Betriebssystem so um, dass Gerätetreiber Namen angezeigt werden, während Sie geladen werden.                                      |
|         /ng          |                                         Fügt dem angegebenen <OSEntryLineNum>die Option **/noguiboot** hinzu und deaktiviert die Statusanzeige, die vor der Eingabeaufforderung von STRG + ALT + ENTF angezeigt wird.                                          |
| /ID <OSEntryLineNum> | Gibt die Betriebssystem-Eintrags Zeilennummer im Abschnitt [Betriebssysteme] der Datei Boot. ini an, der die Betriebssystem-Lade Optionen hinzugefügt werden. Die erste Zeile nach der Abschnitts Kopfzeile [Betriebssystem] ist 1. |
|          /?          |                                                                                               Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                               |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
In den folgenden Beispielen wird gezeigt, wie Sie den Befehl **bootcfg/addsw** verwenden können:
```
bootcfg /addsw /mm 64 /id 2 
bootcfg /addsw /so /id 3 
bootcfg /addsw /so /ng /s srvmain /u hiropln /id 2 
bootcfg /addsw /ng /id 2 
bootcfg /addsw /mm 96 /ng /s srvmain /u maindom\hiropln /p p@ssW23 /id 2
```
## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
