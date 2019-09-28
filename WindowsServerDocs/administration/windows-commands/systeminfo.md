---
title: systeminfo
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 32a84a33c5339e9949648a4e40d71daf25c055d8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370694"
---
# <a name="systeminfo"></a>systeminfo



Zeigt detaillierte Konfigurationsinformationen zu einem Computer und dessen Betriebssystem an, einschließlich Betriebs Systemkonfiguration, Sicherheitsinformationen, Produkt-ID und Hardware Eigenschaften (z. b. RAM, Speicherplatz und Netzwerkkarten).

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
Systeminfo [/s <Computer> [/u <Domain>\<UserName> [/p <Password>]]] [/fo {TABLE | LIST | CSV}] [/nh]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/s \<computer >|Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer.|
|/u \<domäne > \<username >|Führt den Befehl mit den Konto Berechtigungen des angegebenen Benutzerkontos aus. Wenn **/u** nicht angegeben ist, verwendet dieser Befehl die Berechtigungen des Benutzers, der zurzeit auf dem Computer angemeldet ist, von dem der Befehl ausgegeben wird.|
|/p \<Password >|Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist.|
|/FO \<format >|Gibt das Ausgabeformat mit einem der folgenden Werte an:</br>GLAUB Zeigt die Ausgabe in einer Tabelle an.</br>LIST Zeigt die Ausgabe in einer Liste an.</br>CSV Zeigt die Ausgabe im Format mit Komma getrennten Werten an.|
|/nh|Unterdrückt die Spaltenüberschriften in der Ausgabe. Gültig, wenn der **/FO** -Parameter auf Table oder CSV festgelegt ist.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um Konfigurationsinformationen für einen Computer namens srvmain anzuzeigen:

**System Info/s srvmain**

Geben Sie Folgendes ein, um Konfigurationsinformationen für einen Computer mit dem Namen Srvmain2, der sich in der Maindom-Domäne befindet, Remote anzuzeigen:

**System Info/s Srvmain2/u maindom\hiropln**

Geben Sie Folgendes ein, um die Konfigurationsinformationen (im Listenformat) für einen Computer mit dem Namen Srvmain2, der sich in der Maindom-Domäne befindet, Remote anzuzeigen:

**System Info/s Srvmain2/u maindom\hiropln/p p@ssW23/FO List**

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)