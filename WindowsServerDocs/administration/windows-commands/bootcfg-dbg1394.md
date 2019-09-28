---
title: bootcfg dbg1394
description: 'Thema "Windows-Befehle" für **bootcfg dbg1394** : Konfigurieren des 1394-Port Debuggens für einen angegebenen Betriebssystem Eintrag'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35724697-90dd-4dbe-85b0-337fbd369dcc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8550871c60343fdc6d797f3f81729c24270400b4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380087"
---
# <a name="bootcfg-dbg1394"></a>bootcfg dbg1394

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Konfiguriert 1394-Port Debugging für einen angegebenen Betriebssystem Eintrag.

## <a name="syntax"></a>Syntax
```
bootcfg /dbg1394 {ON | OFF}[/s <computer> [/u <Domain>\<User> /p <Password>]] [/ch <Channel>] /id <OSEntryLineNum>
```
## <a name="parameters"></a>Parameter

|      Parameter       |                                                                                                                                           Beschreibung                                                                                                                                            |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   {ON &#124; OFF}    | Gibt den Wert für 1394-Port Debugging an.<br /><br />-   **auf** : aktiviert die Unterstützung für Remote Debugging durch Hinzufügen der/dbg1394-Option zum angegebenen <OSEntryLineNum>.<br />@no__t **-0 deaktiviert** : deaktiviert die Unterstützung für Remote Debugging, indem die/dbg1394-Option aus dem angegebenen <OSEntryLineNum> entfernt wird. |
|    /s <computer>     |                                                                                        Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer.                                                                                        |
| /u <Domain> @ no__t-1 @ no__t-2  |                                               Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der durch <User> oder <Domain> @ no__t-2 @ no__t-3 angegeben wird. Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird.                                               |
|    /p <Password>     |                                                                                                      Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist.                                                                                                       |
|     /ch-Kanal      |                                                           Gibt den für das Debugging zu verwendenden Kanal an. Gültige Werte sind ganze Zahlen zwischen 1 und 64. Verwenden Sie den Parameter " **/ch** <Channel>" nicht, wenn 1394-Port-Debugging deaktiviert wird.                                                           |
| /ID <OSEntryLineNum> |                                  Gibt die Betriebssystem-Eintrags Zeilennummer im Abschnitt [Betriebssysteme] der Datei Boot. ini an, der die 1394-Port-Debugoptionen hinzugefügt werden. Die erste Zeile nach der Abschnitts Kopfzeile [Betriebssystem] ist 1.                                  |
|          /?          |                                                                                                                               Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                               |

## <a name="BKMK_examples"></a>Beispiele
In den folgenden Beispielen wird gezeigt, wie Sie den Befehl **bootcfg/dbg1394**verwenden können:
```
bootcfg /dbg1394 /id 2 
bootcfg /dbg1394 on /ch 1 /id 3 
bootcfg /dbg1394 edit /ch 8 /id 2 
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /dbg1394 off /id 2
```
#### <a name="additional-references"></a>Weitere Verweise
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
