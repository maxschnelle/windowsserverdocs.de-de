---
title: bootcfg timeout
description: Referenz Artikel für den bootcfg-Timeout-Befehl, der den Timeout Wert des Betriebssystems ändert.
ms.topic: reference
ms.assetid: aa858eac-2bb7-4a27-a9bc-3e4a6eb8b2c6
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 520889fce38eb48fe56b9b4c0a38277b5c7f8c8c
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630117"
---
# <a name="bootcfg-timeout"></a>bootcfg timeout

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den Timeout Wert des Betriebssystems.

## <a name="syntax"></a>Syntax

```
bootcfg /timeout <timeoutvalue> [/s <computer> [/u <domain>\<user> /p <password>]]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `/timeout <timeoutvalue>` | Gibt den Timeout Wert im Abschnitt [Boot Loader] an. `<timeoutvalue>`Gibt an, wie viele Sekunden der Benutzer ein Betriebssystem auf dem Start Lade Ladebildschirm auswählen muss, bevor NTLDR den Standardwert lädt. Der gültige Bereich für `<timeoutvalue>` ist 0-999. Wenn der Wert 0 ist, startet NTLDR sofort das Standardbetriebssystem, ohne dass der Bildschirm des Start Lade Programms angezeigt wird. |
| `/s <computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Die Standardeinstellung ist der lokale Computer. |
| `/u <domain>\<user>`  | Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der von oder angegeben wird `<user>` `<domain>\<user>` . Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird. |
| `/p <password>` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

So verwenden Sie den Befehl **bootcfg/Timeout** :

```
bootcfg /timeout 30
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /timeout 50
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [BOOTCFG-Befehl](bootcfg.md)
