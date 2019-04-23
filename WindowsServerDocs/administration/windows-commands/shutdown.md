---
title: shutdown
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c432f5cf-c5aa-4665-83af-0ec52c87112e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5d03a8d35f3e56ec7829bc51c1499fddd13b86e8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837251"
---
# <a name="shutdown"></a>shutdown



Ermöglicht das Herunterfahren oder Neustarten von jeweils einem lokalen Computer oder Remotecomputer.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
shutdown [/i | /l | /s | /r | /a | /p | /h | /e] [/f] [/m \\<ComputerName>] [/t <XXX>] [/d [p|u:]<XX>:<YY> [/c "comment"]] 
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/i|Zeigt die **Remote Shutdown-Dialogfeld** Feld. Die **/i** -Option muss der erste Parameter, die nach dem Befehl sein. Wenn **/i** angegeben ist, werden alle anderen Optionen werden ignoriert.|
|/l|Meldet den aktuellen Benutzer sofort mit kein Timeout festgelegt. Sie können keine **/l** mit **/m** oder **/t /**.|
|/s|Der Computer wird heruntergefahren.|
|/r|Startet den Computer nach dem Herunterfahren neu.|
|/a|Bricht ein Herunterfahren des Systems ab. Nur innerhalb des Timeoutzeitraums ab. Verwendung von **/a**, Sie müssen außerdem verwenden die **/m** Option.|
|/p|Deaktiviert nur den lokalen Computer (keinem Remotecomputer) – ohne Timeout-Zeitraum oder die Warnung. Sie können **/p** nur mit **/d** oder **/f**. Wenn Ihr Computer ausschalten Funktionen nicht unterstützt, es wird heruntergefahren bei Verwendung von **/p**, aber die Möglichkeit, zu dem Computer verbleiben auf.|
|/h|Versetzt den lokalen Computer in den Ruhezustand, an, ob der Ruhezustand aktiviert ist. Sie können **/h** nur mit **/f**.|
|/ e|Ermöglicht Ihnen, dokumentieren Sie den Grund für das unerwartete Herunterfahren auf dem Zielcomputer.|
|/f|Erzwingt die Ausführung von Anwendungen, ohne Vorwarnung geschlossen.</br>Vorsicht: Mithilfe der **/f** Option kann zum Verlust nicht gespeicherter Daten führen.|
|/ m \\ \\ \<ComputerName >|Gibt den Zielcomputer an. Kann nicht verwendet werden, mit der **/l** Option.|
|/ t / \<XXX >|Legt fest, das Zeitlimit oder verzögert, *XXX* Sekunden, nach einem Neustart oder Herunterfahren. Dadurch wird eine Warnung, die auf die lokale Konsole angezeigt. Sie können angeben, 0 bis 600 Sekunden. Wenn Sie nicht verwenden **/t /**, der Timeoutzeitraum ist standardmäßig 30 Sekunden.|
|/d [p\|u:]\<XX>:\<YY>|Listet den Grund für das System neu gestartet oder heruntergefahren. Es folgen die Parameterwerte:</br>**p** gibt an, dass das Neustarten oder Herunterfahren geplant ist.</br>**u** gibt an, dass der Grund Benutzerdefiniert ist.</br>Hinweis: Wenn **p** oder **u** nicht angegeben wird, das Neustarten oder Herunterfahren ungeplante.</br>*XX* gibt an, die als Hauptgrund (positive ganze Zahl kleiner als 256).</br>*YY* der Nebengrundnummer (positive ganze Zahl kleiner als 65536) angibt.|
|/ c "\<Kommentar >"|Hier können Sie detaillierte Kommentare zum Grund für das Herunterfahren eingeben. Sie müssen zuerst einen Grund angeben, mit der **/d** Option. Sie müssen die Kommentare in Anführungszeichen einschließen. Sie können maximal 511 Zeichen verwenden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung ein, einschließlich einer Liste der Haupt- und Nebenversionsnummern Gründe, die auf dem lokalen Computer definiert sind.|

## <a name="remarks"></a>Hinweise

-   Benutzer zugewiesen werden müssen die **Herunterfahren des Systems** Benutzerberechtigung zum Herunterfahren einer lokalen oder remote verwaltet, Computer, der verwendet die **Herunterfahren** Befehl.
-   Benutzer müssen Mitglieder der Gruppe "Administratoren" ein unerwartetes Herunterfahren von einem lokalen oder remote verwalteten Computer mit Anmerkungen versehen werden. Wenn der Zielcomputer einer Domäne angehört, um dieses Verfahren ausführen können möglicherweise Mitglieder der Gruppe "Domänen-Admins". Weitere Informationen finden Sie in den folgenden Themen:  
    -   [Lokale Standardgruppen](https://technet.microsoft.com/library/cc785098(v=ws.10).aspx)
    -   [Standardgruppen](https://technet.microsoft.com/library/cc756898(v=ws.10).aspx)
-   Wenn Sie zu einem Zeitpunkt mehr als einen Computer herunterfahren möchten, können Sie aufrufen **Herunterfahren** für jeden Computer mithilfe eines Skripts, oder Sie verwenden kann **Herunterfahren** **/i** Remote anzeigen Dialogfeld "Herunterfahren".
-   Wenn Sie Haupt- und Nebenversionsnummern Ursachencodes angeben, müssen Sie zunächst diese Ursachencodes auf jedem Computer definieren, in der Sie die Gründe verwenden möchten. Wenn die Codes für Gründe nicht auf dem Zielcomputer definiert sind, kann Ereignisprotokollierung für Herunterfahren nicht den richtigen Grundtext protokollieren.
-   Denken Sie daran, um anzugeben, dass das Herunterfahren geplant ist, mithilfe der **p:** Parameter. Das auslassen **p:** gibt an, dass das Herunterfahren nicht geplant ist. Wenn Sie eingeben **p:** gefolgt von den Ursachencode für ungeplant heruntergefahren wurde, wird nicht der Befehl, das Herunterfahren auszuführen. Im Gegensatz dazu, wenn Sie weglassen **p:** und geben Sie den Ursachencode für ein geplantes Herunterfahren, den Befehl wird das Herunterfahren nicht auszuführen.

## <a name="BKMK_examples"></a>Beispiele für

Erzwingen von Anwendungen zu schließen, und starten Sie den lokalen Computer nach einer Verzögerung von einer Minute mit dem Grund "Anwendung: Wartung (geplant) "und der Kommentar"Reconfiguring myapp.exe"Typ:
```
shutdown /r /t 60 /c "Reconfiguring myapp.exe" /f /d p:4:1
```
Zum Neustarten des Remotecomputers \\ \\ServerName mit den gleichen Parametern eingeben:
```
shutdown /r /m \\servername /t 60 /c "Reconfiguring myapp.exe" /f /d p:4:1
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)
