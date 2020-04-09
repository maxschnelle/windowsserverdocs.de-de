---
title: bootcfg rmsw
description: Windows-Befehls Thema für bootcfg Rmsw, das Optionen für das Laden von Betriebssystemen für einen angegebenen Betriebssystem Eintrag entfernt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fd7e4248-880e-4e2b-929e-87f8d44b9a63
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 956732f396e0fa353a8acd55953e46605a5c4200
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848443"
---
# <a name="bootcfg-rmsw"></a>bootcfg rmsw

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Entfernt Optionen für das Laden von Betriebssystemen für einen angegebenen Betriebssystem Eintrag.

## <a name="syntax"></a>Syntax
```
bootcfg /rmsw [/s <computer> [/u <Domain>\<User> [/p <Password>]]] [/mm] [/bv] [/so] [/ng] /id <OSEntryLineNum>
```
### <a name="parameters"></a>Parameter

|      Parameter       |                                                                                                      Beschreibung                                                                                                       |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>     |                                                   Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer.                                                   |
| /u <Domain>\\<User>  |          Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der durch <User> oder <Domain>\\<User>angegeben wird. Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird.          |
|    /p <Password>     |                                                                 Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist.                                                                  |
|         /mm          |           entfernt die/Maxmem-Option und den zugehörigen maximalen Speicher Wert aus dem angegebenen <OSEntryLineNum>. Die Option/MAXMEM gibt die maximale RAM-Größe an, die vom Betriebssystem verwendet werden kann.            |
|         /bv          |                     entfernt die/basevideo-Option aus dem angegebenen <OSEntryLineNum>. Die Option/basevideo weist das Betriebssystem an, den standardmäßigen VGA-Modus für den installierten Videotreiber zu verwenden.                     |
|         /so          |                         entfernt die/SOS-Option aus dem angegebenen <OSEntryLineNum>. Die Option/SOS weist das Betriebssystem an, beim Laden Gerätetreiber Namen anzuzeigen.                          |
|         /ng          |                         entfernt die/noguiboot-Option aus dem angegebenen <OSEntryLineNum>. Die Option/noguiboot deaktiviert die Statusanzeige, die vor der Eingabeaufforderung von STRG + ALT + ENTF angezeigt wird.                          |
| /ID <OSEntryLineNum> | Gibt die Betriebssystem-Eintrags Zeilennummer im Abschnitt [Betriebssysteme] der Datei Boot. ini an, aus der die Optionen für das Laden des Betriebssystems entfernt werden. Die erste Zeile nach der Abschnitts Kopfzeile [Betriebssystem] ist 1. |
|          /?          |                                                                                          Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                          |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
In den folgenden Beispielen wird gezeigt, wie Sie den Befehl **bootcfg/Rmsw**verwenden können:
```
bootcfg /rmsw /mm 64 /id 2 
bootcfg /rmsw /so /id 3 
bootcfg /rmsw /so /ng /s srvmain /u hiropln /id 2 
bootcfg /rmsw /ng /id 2 
bootcfg /rmsw /mm 96 /ng /s srvmain /u maindom\hiropln /p p@ssW23 /id 2       
```
## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
