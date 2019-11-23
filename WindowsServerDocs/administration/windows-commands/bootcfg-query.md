---
title: bootcfg query
description: Windows-Befehle Thema für **bootcfg query** -Queries und zeigt die Abschnitts Einträge [Boot Loader] und [Betriebssysteme] von Boot. ini an.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a4cacfd1-10a6-4a11-b0c5-f8abde72bfc8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ae82357cfe178343872448c2ebd46c49a797b5a9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379910"
---
# <a name="bootcfg-query"></a>bootcfg query

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Abfragen und Anzeigen der Abschnitts Einträge [Boot Loader] und [Betriebssysteme] aus der Datei "Boot. ini".

## <a name="syntax"></a>Syntax
```
bootcfg /query [/s <computer> [/u <Domain>\<User> /p <Password>]]
```
## <a name="parameters"></a>Parameter

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
  Friendly Name:   ""
  path:            multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
  OS Load Options: /fastdetect /debug /debugport=com1:
  ```
- Der Teil des Start Lade Programms in der **bootcfg-Abfrage** Ausgabe zeigt jeden Eintrag im Abschnitt [Boot Loader] von Boot. ini an.
- Der Teil "Start Einträge" der **bootcfg-Abfrage** Ausgabe zeigt die folgenden Details für jeden Betriebssystem Eintrag im Abschnitt [Betriebssysteme] der Datei Boot. ini: Start Eintrag-ID, Anzeige Name, Pfad und lade Optionen für das Betriebssystem an.
  ## <a name="BKMK_examples"></a>Beispiele
  In den folgenden Beispielen wird gezeigt, wie Sie den Befehl **bootcfg/query "aus** verwenden können:
  ```
  bootcfg /query
  bootcfg /query /s srvmain /u maindom\hiropln /p p@ssW23
  bootcfg /query /u hiropln /p p@ssW23
  ```
  #### <a name="additional-references"></a>Weitere Verweise
  [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
