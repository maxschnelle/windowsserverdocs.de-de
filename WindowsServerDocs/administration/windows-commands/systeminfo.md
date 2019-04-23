---
title: systeminfo
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 39954968-3c2e-4d3e-9d89-c9c43347461e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3d08d3f86bdbd176aa4de157f58a58c9ea418470
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841501"
---
# <a name="systeminfo"></a>systeminfo



Zeigt detaillierte Informationen zu einem Computer und das Betriebssystem, einschließlich der Konfiguration des Betriebssystems, die Sicherheitsinformationen, die Produkt-ID und die Hardwareeigenschaften (z. B. Arbeitsspeicher, Speicherplatz und Netzwerkkarten).

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
Systeminfo [/s <Computer> [/u <Domain>\<UserName> [/p <Password>]]] [/fo {TABLE | LIST | CSV}] [/nh]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/ s \<Computer >|Gibt den Namen oder die IP-Adresse eines Remotecomputers (umgekehrte Schrägstriche nicht verwenden). Der Standardwert ist der lokale Computer.|
|/ u \<Domäne >\<Benutzername >|Führt den Befehl mit den Kontoberechtigungen für das angegebene Benutzerkonto an. Wenn **/u** nicht angegeben ist, wird dieser Befehl verwendet die Berechtigungen des Benutzers, der derzeit auf dem Computer angemeldet ist, die den Befehl ausgegeben wird.|
|/ p \<Kennwort >|Gibt das Kennwort des Benutzerkontos ein, die im angegebenen die **/u** Parameter.|
|/ Fo \<Format >|Gibt das Ausgabeformat mit einem der folgenden Werte an:</br>TABELLE: Zeigt die Ausgabe in einer Tabelle.</br>LISTE: Zeigt die Ausgabe in einer Liste.</br>CSV: Zeigt die Ausgabe in durch Trennzeichen getrennten Format.|
|/nh|Unterdrückt die Spaltenüberschriften in der Ausgabe. Gültig, wenn die **/Fo** Parameter auf die Tabelle oder CSV-Format festgelegt ist.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_examples"></a>Beispiele für

Um die Konfigurationsinformationen für einen Computer namens Srvmain anzuzeigen, geben Sie Folgendes ein:

**systeminfo /s srvmain**

Um die Konfigurationsinformationen für einen Computer namens Srvmain2 auf dem der Domäne Maindom anzuzeigen, geben Sie Folgendes ein:

**systeminfo /s srvmain2 /u maindom\hiropln**

Zum Anzeigen von Remote Configuration-Informationen (im Listenformat) für einen Computer namens Srvmain2, die in der Domäne Maindom befindet, geben Sie Folgendes ein:

**systeminfo /s srvmain2 /u maindom\hiropln /p p@ssW23 /fo list**

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)