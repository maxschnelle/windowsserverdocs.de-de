---
title: gpupdate
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2fd4e567-2ce1-4637-b611-c2f0895e5708
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f159acf1415ee48fe48c5d514a866ffc9f356db4
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724931"
---
# <a name="gpupdate"></a>gpupdate

Aktualisiert Gruppenrichtlinie Einstellungen. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#examples).

## <a name="syntax"></a>Syntax

```
gpupdate [/target:{Computer | User}] [/force] [/wait:<VALUE>] [/logoff] [/boot] [/sync] [/?]
```

#### <a name="parameters"></a>Parameter

|     Parameter     |                                                                                                                                                                                                                                                                                                                             BESCHREIBUNG                                                                                                                                                                                                                                                                                                                             |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /target: {Computer\|Benutzer} | Gibt an, dass nur Benutzer-oder nur Computer Richtlinien Einstellungen aktualisiert werden. Standardmäßig werden die Benutzer-und Computer Richtlinien Einstellungen aktualisiert.                                                                                                                                                                                                                                                                                                                                |
|      /Force       |                                                                                                                                                                                                                                                                                   Wendet alle Richtlinien Einstellungen erneut an. Standardmäßig werden nur Richtlinien Einstellungen angewendet, die geändert wurden.                                                                                                                                                                                                                                                                                    |
|  /Wait:\<Wert>   | Legt die Anzahl von Sekunden fest, die auf den Abschluss der Richtlinien Verarbeitung gewartet werden soll, bevor zur Eingabeaufforderung zurückgekehrt wird. Wenn das Zeitlimit überschritten wird, wird die Eingabeaufforderung angezeigt, die Richtlinien Verarbeitung wird jedoch fortgesetzt. Der Standardwert beträgt 600 Sekunden. Der Wert **0** bedeutet, dass nicht gewartet werden soll. Der Wert **-1** bedeutet, unbegrenzt zu warten.</br>In einem Skript können Sie mithilfe dieses Befehls mit einem angegebenen Zeit Limit **gpupdate** ausführen und mit Befehlen fortfahren, die nicht vom Abschluss von **gpupdate**abhängen. Alternativ können Sie diesen Befehl ohne angegebenes Zeit Limit verwenden, damit die Ausführung von " **gpupdate** " beendet wird, bevor andere Befehle ausgeführt werden, die von ihm abhängen. |
|      /logoff      |                                                                                                                                   Bewirkt eine Abmeldung, nachdem die Gruppenrichtlinie Einstellungen aktualisiert wurden. Dies ist für die Gruppenrichtlinie Client seitigen Erweiterungen erforderlich, die keine Richtlinien für einen Hintergrund Aktualisierungs Zeitraum verarbeiten, aber die Prozess Richtlinie bei der Anmeldung eines Benutzers verarbeiten. Beispiele hierfür sind die benutzerorientierte Software Installation und Ordner Umleitung. Diese Option hat keine Auswirkungen, wenn keine Erweiterungen namens vorhanden sind, für die eine Abmeldung erforderlich ist.                                                                                                                                    |
|       /Boot       |                                                                                                                                       Verursacht einen Computer Neustart, nachdem die Gruppenrichtlinie Einstellungen angewendet wurden. Dies ist für diejenigen Gruppenrichtlinie Client seitigen Erweiterungen erforderlich, die keine Richtlinien in einem Hintergrund Update Prozess verarbeiten, aber die Prozess Richtlinie beim Starten des Computers verarbeiten. Beispiele hierfür sind die Computerorientierte Software Installation. Diese Option hat keine Auswirkung, wenn keine Erweiterungen namens vorhanden sind, für die ein Neustart erforderlich ist.                                                                                                                                        |
|       /sync       |                                                                                                                                                                              Bewirkt, dass die nächste Anwendung der Vordergrund Richtlinie synchron ausgeführt wird. Die Vordergrund Richtlinie wird beim Computer Start und bei der Benutzeranmeldung angewendet. Sie können dies für den Benutzer, den Computer oder beides angeben, indem Sie den **/target** -Parameter verwenden. Die Parameter **/Force** und **/Wait** werden ignoriert, wenn Sie Sie angeben.                                                                                                                                                                               |
|        /?         |                                                                                                                                                                                                                                                                                                                Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                                                                                                                                                 |

## <a name="remarks"></a>Bemerkungen

-   Der **gpupdate** -Befehl ist in Windows Server 2008 R2, Windows Server 2008, Windows 7 Ultimate, Windows 7 Professional, Windows Vista Ultimate, Windows Vista Enterprise und Windows Vista Business verfügbar.

## <a name="examples"></a>Beispiele

Erzwingen einer Hintergrund Aktualisierung aller Gruppenrichtlinie Einstellungen, unabhängig davon, ob Sie geändert wurden.

```
gpupdate /force
```

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [TechCenter zu Gruppenrichtlinien](https://go.microsoft.com/fwlink/?LinkID=145531)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
