---
title: waitfor
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a48ef70d-4d28-4035-b6b0-7d7b46ac2157
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1c4a91dd3822cf4d8dd904f473f146a2f0ee54c0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840161"
---
# <a name="waitfor"></a>waitfor



Sendet oder wartet auf ein Signal in einem System. **WAITFOR** wird verwendet, um die Computer über ein Netzwerk zu synchronisieren.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
waitfor [/s <Computer> [/u [<Domain>\]<User> [/p [<Password>]]]] /si <SignalName>
waitfor [/t <Timeout>] <SignalName>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/ s \<Computer >|Gibt den Namen oder die IP-Adresse eines Remotecomputers (umgekehrte Schrägstriche nicht verwenden). Der Standardwert ist der lokale Computer. Dieser Parameter gilt für alle Dateien und Ordner im Befehl angegeben.|
|/u [\<Domain>\]<User>|Führt das Skript mit den Anmeldeinformationen des angegebenen Benutzerkontos. In der Standardeinstellung **Waitfor** verwendet die Anmeldeinformationen des aktuellen Benutzers.|
|/ p [\<Kennwort >]|Gibt das Kennwort des Benutzerkontos ein, die im angegebenen die **/u** Parameter.|
|/si|Das angegebene Signal über das Netzwerk gesendet.|
|/ t / \<Timeout >|Gibt die Anzahl der Sekunden für ein Signal. In der Standardeinstellung **Waitfor** wartet unbegrenzt.|
|\<SignalName>|Gibt an, das Signal, **Waitfor** wartet oder sendet. *SignalName* wird nicht beachtet.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Signalnamen darf 225 Zeichen nicht überschreiten. Gültige Zeichen sind a – Z, A-Z, 0-9 sowie dem ASCII-Zeichensatz (128 – 255) erweitert.
-   Wenn Sie nicht verwenden **/s**, das Signal an alle Systeme in einer Domäne übertragen wird. Bei Verwendung von **/s**, das Signal wird nur auf dem angegebenen System gesendet.
-   Sie können mehrere Instanzen ausführen **Waitfor** auf einem einzelnen Computer, aber jede Instanz des **Waitfor** warten muss, ein anderes Signal. Nur eine Instanz des **Waitfor** kann, bis ein bestimmtes Signal auf einem bestimmten Computer.
-   Sie können ein Signal manuell aktivieren, indem die **/SI** Befehlszeilenoption.
-   **WAITFOR** ausgeführt wird, nur auf Windows XP und Server, die unter Windows Server 2003 ausgeführt wird, aber es kann an einem beliebigen Computer mit einem Windows-Betriebssystem Signale senden.
-   Computer können nur Signale empfangen, wenn sie in der gleichen Domäne wie der Computer, auf das Signal senden sind.
-   Sie können **Waitfor** beim Testen von Softwarebuilds. Beispielsweise Computer der Kompilierung kann Senden eines Signals für mehrere Computer mit **Waitfor** nach die Kompilierung erfolgreich abgeschlossen wurde. Beim Empfang des Signals, die Batchdatei, umfasst **Waitfor** können anweisen, die Computer, die Software installieren oder Ausführen von Tests auf den kompilierten Build sofort zu starten.

## <a name="BKMK_examples"></a>Beispiele für

Um zu warten, bis das Signal "espresso\build007" empfangen wird, geben Sie Folgendes ein:
```
waitfor espresso\build007
```
In der Standardeinstellung **Waitfor** wartet auf ein Signal.

Warten Sie 10 Sekunden, bis das Signal "espresso\compile007", bevor ein Timeout empfangen werden soll, geben Sie Folgendes ein:
```
waitfor /t 10 espresso\build007
```
Um das Signal "espresso\build007" manuell zu aktivieren, geben Sie Folgendes ein:
```
waitfor /si espresso\build007
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)