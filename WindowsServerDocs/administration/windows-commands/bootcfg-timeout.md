---
title: bootcfg timeout
description: Windows-Befehle Thema **Bootcfg Timeout** -ändert sich der Betriebssystem-Timeout-Wert.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aa858eac-2bb7-4a27-a9bc-3e4a6eb8b2c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1fc33d2d20d6d2532c5ed1f33e27a768935d1e85
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434640"
---
# <a name="bootcfg-timeout"></a>bootcfg timeout

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ändert den Betriebssystem-Timeout-Wert.

## <a name="syntax"></a>Syntax
```
bootcfg /timeout <timeOutValue> [/s <computer> [/u <Domain\User>/p <Password>]]
```
## <a name="parameters"></a>Parameter

|        Parameter        |                                                                                                                                                                                  Beschreibung                                                                                                                                                                                   |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| / Timeout <timeOutValue> | Gibt den Timeoutwert in den Abschnitt [Bootloader] an. Die <timeOutValue> ist die Anzahl der Sekunden, die der Benutzer muss ein Betriebssystem aus dem Bildschirm des Startladeprogramms auswählen, bevor NTLDR standardmäßig lädt. Gültige Bereich für <timeOutValue> 0 bis 999. Wenn der Wert 0 ist, startet NTLDR sofort das Standardbetriebssystem, ohne den Bildschirm des Startladeprogramms anzuzeigen. |
|      /s <computer>      |                                                                                                                               Gibt den Namen oder die IP-Adresse eines Remotecomputers (umgekehrte Schrägstriche nicht verwenden). Der Standardwert ist der lokale Computer.                                                                                                                               |
|    /u <Domain\User>     |                                                                                       Führt den Befehl mit den Berechtigungen des Benutzers gemäß <User> oder < Domäne\Benutzername >. Der Standardwert ist die Berechtigungen von der aktuell angemeldete Benutzer auf dem Computer, die der Befehl ausgegeben wird.                                                                                        |
|      /p <Password>      |                                                                                                                                            Gibt an, die <Password> des Benutzerkontos ein, die im angegebenen die **/u** Parameter.                                                                                                                                             |
|           /?            |                                                                                                                                                                      Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                      |

## <a name="BKMK_examples"></a>Beispiele für
Die folgenden Beispiele zeigen Informationen zur Verwendung der **Bootcfg/timeout** Befehl:
```
bootcfg /timeout 30
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /timeout 50
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
