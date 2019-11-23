---
title: bootcfg addsw
description: Thema Windows-Befehle für **bootcfg addsw** -fügt Optionen für das Laden von Betriebssystemen für einen angegebenen Betriebssystem Eintrag hinzu.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d8389293-ecd9-42f0-b84b-b9ead4cf52e6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2dd727c839babe1ae4f7743285844f35cf5bf76e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380180"
---
# <a name="bootcfg-addsw"></a>bootcfg addsw

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt Optionen für das Laden von Betriebssystemen für einen angegebenen Betriebssystem Eintrag hinzu.

## <a name="syntax"></a>Syntax
```
bootcfg /addsw [/s <computer> [/u <Domain>\<User> /p <Password>]] [/mm <MaximumRAM>] [/bv] [/so] [/ng] /id <OSEntryLineNum>
```
## <a name="parameters"></a>Parameter

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

## <a name="BKMK_examples"></a>Beispiele
In den folgenden Beispielen wird gezeigt, wie Sie den Befehl **bootcfg/addsw** verwenden können:
```
bootcfg /addsw /mm 64 /id 2 
bootcfg /addsw /so /id 3 
bootcfg /addsw /so /ng /s srvmain /u hiropln /id 2 
bootcfg /addsw /ng /id 2 
bootcfg /addsw /mm 96 /ng /s srvmain /u maindom\hiropln /p p@ssW23 /id 2
```
#### <a name="additional-references"></a>Weitere Verweise
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
