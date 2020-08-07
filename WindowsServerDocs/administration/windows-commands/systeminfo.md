---
title: systeminfo
description: Referenz Artikel zu Systeminfo, der ausführliche Konfigurationsinformationen zu einem Computer und dessen Betriebssystem anzeigt, einschließlich Betriebs Systemkonfiguration, Sicherheitsinformationen, Produkt-ID und Hardware Eigenschaften (z. b. RAM, Speicherplatz und Netzwerkkarten).
ms.topic: article
ms.assetid: 39954968-3c2e-4d3e-9d89-c9c43347461e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b34e92a5035360cb600bfe73b405f0a7033b6196
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87881900"
---
# <a name="systeminfo"></a>systeminfo

Zeigt detaillierte Konfigurationsinformationen zu einem Computer und dessen Betriebssystem an, einschließlich Betriebs Systemkonfiguration, Sicherheitsinformationen, Produkt-ID und Hardware Eigenschaften (z. b. RAM, Speicherplatz und Netzwerkkarten).



## <a name="syntax"></a>Syntax

```
Systeminfo [/s <Computer> [/u <Domain>\<UserName> [/p <Password>]]] [/fo {TABLE | LIST | CSV}] [/nh]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|/s\<Computer>|Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Die Standardeinstellung ist der lokale Computer.|
|/u\<Domain>\<UserName>|Führt den Befehl mit den Konto Berechtigungen des angegebenen Benutzerkontos aus. Wenn **/u** nicht angegeben ist, verwendet dieser Befehl die Berechtigungen des Benutzers, der zurzeit auf dem Computer angemeldet ist, von dem der Befehl ausgegeben wird.|
|/p\<Password>|Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist.|
|/FO\<Format>|Gibt das Ausgabeformat mit einem der folgenden Werte an:</br>Table: zeigt die Ausgabe in einer Tabelle an.</br>List: zeigt die Ausgabe in einer Liste an.</br>CSV: zeigt die Ausgabe im Format mit Komma getrennten Werten an.|
|/nh|Unterdrückt die Spaltenüberschriften in der Ausgabe. Gültig, wenn der **/FO** -Parameter auf Table oder CSV festgelegt ist.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um Konfigurationsinformationen für einen Computer namens srvmain anzuzeigen:

**System Info/s srvmain**

Geben Sie Folgendes ein, um Konfigurationsinformationen für einen Computer mit dem Namen Srvmain2, der sich in der Maindom-Domäne befindet, Remote anzuzeigen:

**System Info/s Srvmain2/u maindom\hiropln**

Geben Sie Folgendes ein, um die Konfigurationsinformationen (im Listenformat) für einen Computer mit dem Namen Srvmain2, der sich in der Maindom-Domäne befindet, Remote anzuzeigen:

**System Info/s Srvmain2/u maindom\hiropln/p p@ssW23 /FO List**

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)