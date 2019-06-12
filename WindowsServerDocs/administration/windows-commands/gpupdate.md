---
title: gpupdate
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2fd4e567-2ce1-4637-b611-c2f0895e5708
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dba8a0fb7d9a4e95f91ed1c1e140d965f5f9e2fb
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811117"
---
# <a name="gpupdate"></a>gpupdate

Aktualisiert die Einstellungen für Gruppenrichtlinien. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#examples).

## <a name="syntax"></a>Syntax

```
gpupdate [/target:{Computer | User}] [/force] [/wait:<VALUE>] [/logoff] [/boot] [/sync] [/?]
```

### <a name="parameters"></a>Parameter

|     Parameter     |                                                                                                                                                                                                                                                                                                                             Beschreibung                                                                                                                                                                                                                                                                                                                             |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| / target: Computer { |                                                                                                                                                                                                                                                                                                                                Benutzer}                                                                                                                                                                                                                                                                                                                                |
|      /force       |                                                                                                                                                                                                                                                                                   Wendet erneut an alle Richtlinieneinstellungen. Standardmäßig gelten nur für den Richtlinieneinstellungen, die geändert wurden.                                                                                                                                                                                                                                                                                    |
|  / wait:\<Wert >   | Legt die Anzahl der Sekunden für die Richtlinie, die Verarbeitung abgeschlossen ist, bevor Sie an der Eingabeaufforderung zurückgegeben werden. Wenn das Zeitlimit überschritten wird, wird die Eingabeaufforderung angezeigt wird, aber die Verarbeitung der Gruppenrichtlinie weiterhin. Der Standardwert ist 600 Sekunden. Der Wert **0** bedeutet nicht, warten Sie. Der Wert **-1** bedeutet, dass für Warten ohne Timeout.</br>In einem Skript mithilfe dieses Befehls mit einer Frist angegeben wird, können Sie ausführen **Gpupdate** und fahren Sie mit Befehlen, die nicht nach dem Abschluss abhängen **Gpupdate**. Alternativ können Sie diesen Befehl mit kein Zeitlimit angegeben, um können **Gpupdate** Beendigung vor dem Ausführen von anderen Befehlen, die davon abhängen. |
|      /logoff      |                                                                                                                                   Bewirkt, dass sich abmelden, nachdem die gruppenrichtlinieneinstellungen aktualisiert werden. Dies ist erforderlich, für die clientseitige gruppenrichtlinienerweiterungen, die Richtlinie auf ein Updatezyklus für Hintergrund nicht verarbeiten, aber Richtlinie verarbeiten, wenn ein Benutzer anmeldet. Beispiele sind für benutzerorientierte Softwareinstallation und Ordnerumleitung. Diese Option hat keine Auswirkungen, wenn vorhanden sind, dass keine Erweiterungen aufgerufen, die eine Abmeldung erforderlich.                                                                                                                                    |
|       /boot       |                                                                                                                                       Führt einen Neustart des Computers an, nachdem die gruppenrichtlinieneinstellungen angewendet wurden. Dies ist erforderlich, für die clientseitige gruppenrichtlinienerweiterungen, die Richtlinie auf ein Updatezyklus für Hintergrund nicht verarbeiten, aber die Richtlinie beim Starten des Computers verarbeiten. Beispiele hierfür sind computerspezifische Softwareinstallation. Diese Option hat keine Auswirkungen, wenn vorhanden sind, dass keine Erweiterungen aufgerufen, die ein Neustart erforderlich ist.                                                                                                                                        |
|       /sync       |                                                                                                                                                                              Bewirkt, dass die nächste Vordergrund richtlinienanwendung synchron ausgeführt werden. Vordergrundrichtlinie wird auf dem Computer starten und bei der Anmeldung angewendet. Sie können dies angeben, für den Benutzer, Computer oder beides, mit der **/target** Parameter. Die **/force** und **/wait** Parameter werden ignoriert, wenn Sie diese angeben.                                                                                                                                                                               |
|        /?         |                                                                                                                                                                                                                                                                                                                Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                                                                                                                                                 |

## <a name="remarks"></a>Hinweise

-   Die **Gpupdate** Befehl ist in Windows Server 2008 R2, Windows Server 2008, Windows 7 Ultimate, Windows 7 Professional, Windows Vista Ultimate, Windows Vista Enterprise und Windows Vista Business verfügbar.

## <a name="examples"></a>Beispiele

Erzwingen Sie ein Hintergrund Update aller gruppenrichtlinieneinstellungen, unabhängig davon, ob sie geändert haben.

```
gpupdate /force
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Gruppenrichtlinien-TechCenter](https://go.microsoft.com/fwlink/?LinkID=145531)
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)