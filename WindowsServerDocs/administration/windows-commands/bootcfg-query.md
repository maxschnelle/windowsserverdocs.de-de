---
title: bootcfg query
description: Windows-Befehls Artikel für die bootcfg-Abfrage, die die Einträge für das Start Lade Paket und den Betriebssystem Abschnitt von "Boot. ini" abfragt und anzeigt
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a4cacfd1-10a6-4a11-b0c5-f8abde72bfc8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1ac80c802b1d30dcf7221f94f761233c6b6fc6b6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848523"
---
# <a name="bootcfg-query"></a>bootcfg query

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Abfragen und Anzeigen der Abschnitts Einträge [Boot Loader] und [Betriebssysteme] aus der Datei "Boot. ini".

## <a name="syntax"></a>Syntax
```
bootcfg /query [/s <computer> [/u <Domain>\<User> /p <Password>]]
```
### <a name="parameters"></a>Parameter

|        Begriff         |                                                                                             Definition                                                                                              |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>    |                                         Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer.                                          |
| /u <Domain>\\<User> | Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der durch <User>oder <Domain>\\<User>angegeben wird. Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird. |
|    /p <Password>    |                                                        Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist.                                                        |
|         /?          |                                                                                Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                 |

##### <a name="remarks"></a>Hinweise
- Im folgenden finden Sie ein Beispiel für die Ausgabe von **bootcfg/query "aus** :
  ```
  Boot Loader Settings
  ----------
  timeout: 30
  default: multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
  Boot Entries
  ------
  Boot entry ID:   1
  Friendly Name:   
  path:            multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
  OS Load Options: /fastdetect /debug /debugport=com1:
  ```
- Der Teil des Start Lade Programms in der **bootcfg-Abfrage** Ausgabe zeigt jeden Eintrag im Abschnitt [Boot Loader] von Boot. ini an.
- Der Teil "Start Einträge" der **bootcfg-Abfrage** Ausgabe zeigt die folgenden Details für jeden Betriebssystem Eintrag im Abschnitt [Betriebssysteme] der Datei Boot. ini: Start Eintrag-ID, Anzeige Name, Pfad und lade Optionen für das Betriebssystem an.
  ## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
  In den folgenden Beispielen wird gezeigt, wie Sie den Befehl **bootcfg/query "aus** verwenden können:
  ```
  bootcfg /query
  bootcfg /query /s srvmain /u maindom\hiropln /p p@ssW23
  bootcfg /query /u hiropln /p p@ssW23
  ```
  ## <a name="additional-references"></a>Weitere Verweise
  - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
