---
title: bootcfg timeout
description: Windows-Befehls Thema für bootcfg Timeout, das den Timeout Wert des Betriebssystems ändert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: aa858eac-2bb7-4a27-a9bc-3e4a6eb8b2c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b56e609d5e3b7c92a887a98ae5d02bfbfb7a78e6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848493"
---
# <a name="bootcfg-timeout"></a>bootcfg timeout

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

ändert den Timeout Wert des Betriebssystems.

## <a name="syntax"></a>Syntax

```
bootcfg /timeout <timeOutValue> [/s <computer> [/u <Domain\User>/p <Password>]]
```

### <a name="parameters"></a>Parameter


|        Parameter        |                                                                                                                                                                                  Beschreibung                                                                                                                                                                                   |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /Timeout <timeOutValue> | Gibt den Timeout Wert im Abschnitt [Boot Loader] an. Der <timeOutValue> gibt an, wie viele Sekunden der Benutzer ein Betriebssystem auf dem Start Lade Ladebildschirm auswählen muss, bevor NTLDR den Standardwert lädt. Der gültige Bereich für <timeOutValue> ist 0-999. Wenn der Wert 0 ist, startet NTLDR sofort das Standardbetriebssystem, ohne dass der Bildschirm des Start Lade Programms angezeigt wird. |
|      /s <computer>      |                                                                                                                               Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer.                                                                                                                               |
|    /u < Domäne \ Benutzer >     |                                                                                       Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der durch <User> oder < Domäne \ Benutzer > angegeben ist. Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird.                                                                                        |
|      /p <Password>      |                                                                                                                                            Gibt den <Password> des Benutzerkontos an, das im **/u** -Parameter angegeben ist.                                                                                                                                             |
|           /?            |                                                                                                                                                                      Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                      |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
In den folgenden Beispielen wird gezeigt, wie Sie den Befehl **bootcfg/Timeout** verwenden können:
```
bootcfg /timeout 30
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /timeout 50
```
## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
