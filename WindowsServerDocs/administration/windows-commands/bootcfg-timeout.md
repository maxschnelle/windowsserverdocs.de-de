---
title: bootcfg timeout
description: 'Thema Windows-Befehle für **bootcfg-Timeout** : ändert den Timeout Wert des Betriebssystems.'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 94bc2de43dd179117c7a44747961213d12741a09
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379866"
---
# <a name="bootcfg-timeout"></a>bootcfg timeout

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

ändert den Timeout Wert des Betriebssystems.

## <a name="syntax"></a>Syntax
```
bootcfg /timeout <timeOutValue> [/s <computer> [/u <Domain\User>/p <Password>]]
```
## <a name="parameters"></a>Parameter

|        Parameter        |                                                                                                                                                                                  Beschreibung                                                                                                                                                                                   |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /Timeout <timeOutValue> | Gibt den Timeout Wert im Abschnitt [Boot Loader] an. Der <timeOutValue> ist die Anzahl der Sekunden, die der Benutzer auf dem Start Lade Ladebildschirm ein Betriebssystem auswählen muss, bevor NTLDR den Standardwert lädt. Gültiger Bereich für <timeOutValue> ist 0-999. Wenn der Wert 0 ist, startet NTLDR sofort das Standardbetriebssystem, ohne dass der Bildschirm des Start Lade Programms angezeigt wird. |
|      /s <computer>      |                                                                                                                               Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer.                                                                                                                               |
|    /u < Domäne \ Benutzer >     |                                                                                       Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der durch <User> oder < Domäne \ Benutzer > angegeben ist. Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird.                                                                                        |
|      /p <Password>      |                                                                                                                                            Gibt den <Password> des Benutzerkontos an, das im **/u** -Parameter angegeben ist.                                                                                                                                             |
|           /?            |                                                                                                                                                                      Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                      |

## <a name="BKMK_examples"></a>Beispiele
In den folgenden Beispielen wird gezeigt, wie Sie den Befehl **bootcfg/Timeout** verwenden können:
```
bootcfg /timeout 30
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /timeout 50
```
#### <a name="additional-references"></a>Weitere Verweise
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
