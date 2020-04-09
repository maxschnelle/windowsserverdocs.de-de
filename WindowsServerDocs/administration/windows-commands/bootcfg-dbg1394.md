---
title: bootcfg dbg1394
description: Windows-Befehls Thema für bootcfg dbg1394, das 1394-Port-Debugging für einen angegebenen Betriebssystem Eintrag konfiguriert
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 35724697-90dd-4dbe-85b0-337fbd369dcc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d49e0a39cd021f093ca68bf97963dc35c3b53ad4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848673"
---
# <a name="bootcfg-dbg1394"></a>bootcfg dbg1394

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Konfiguriert 1394-Port Debugging für einen angegebenen Betriebssystem Eintrag.

## <a name="syntax"></a>Syntax
```
bootcfg /dbg1394 {ON | OFF}[/s <computer> [/u <Domain>\<User> /p <Password>]] [/ch <Channel>] /id <OSEntryLineNum>
```
### <a name="parameters"></a>Parameter

|      Parameter       |                                                                                                                                           Beschreibung                                                                                                                                            |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   {ON &#124; Off}    | Gibt den Wert für 1394-Port Debugging an.<p>-   **on** : aktiviert die Unterstützung für Remote Debugging durch Hinzufügen der/dbg1394-Option zum angegebenen <OSEntryLineNum>.<br />-   **Off** : deaktiviert die Unterstützung für Remote Debugging, indem die/dbg1394-Option aus dem angegebenen <OSEntryLineNum>entfernt wird. |
|    /s <computer>     |                                                                                        Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer.                                                                                        |
| /u <Domain>\\<User>  |                                               Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der durch <User> oder <Domain>\\<User>angegeben wird. Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird.                                               |
|    /p <Password>     |                                                                                                      Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist.                                                                                                       |
|     /ch-Kanal      |                                                           Gibt den für das Debugging zu verwendenden Kanal an. Gültige Werte sind ganze Zahlen zwischen 1 und 64. Verwenden Sie den Parameter **/ch** <Channel> nicht, wenn das 1394-Port-Debugging deaktiviert wird.                                                           |
| /ID <OSEntryLineNum> |                                  Gibt die Betriebssystem-Eintrags Zeilennummer im Abschnitt [Betriebssysteme] der Datei Boot. ini an, der die 1394-Port-Debugoptionen hinzugefügt werden. Die erste Zeile nach der Abschnitts Kopfzeile [Betriebssystem] ist 1.                                  |
|          /?          |                                                                                                                               Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                               |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
In den folgenden Beispielen wird gezeigt, wie Sie den Befehl **bootcfg/dbg1394**verwenden können:
```
bootcfg /dbg1394 /id 2 
bootcfg /dbg1394 on /ch 1 /id 3 
bootcfg /dbg1394 edit /ch 8 /id 2 
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /dbg1394 off /id 2
```
## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
