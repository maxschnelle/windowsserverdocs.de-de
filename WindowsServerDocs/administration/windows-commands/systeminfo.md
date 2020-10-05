---
title: systeminfo
description: Referenz Artikel für den System Info-Befehl, der ausführliche Konfigurationsinformationen zu einem Computer und dessen Betriebssystem anzeigt, einschließlich Betriebs Systemkonfiguration, Sicherheitsinformationen, Produkt-ID und Hardware Eigenschaften (z. b. RAM, Speicherplatz und Netzwerkkarten).
ms.topic: reference
ms.assetid: 39954968-3c2e-4d3e-9d89-c9c43347461e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9c104d3114eae6170e3fbbd60ab718fa0013ea85
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91718197"
---
# <a name="systeminfo"></a>systeminfo

Zeigt detaillierte Konfigurationsinformationen zu einem Computer und dessen Betriebssystem an, einschließlich Betriebs Systemkonfiguration, Sicherheitsinformationen, Produkt-ID und Hardware Eigenschaften (z. b. RAM, Speicherplatz und Netzwerkkarten).

## <a name="syntax"></a>Syntax

```
systeminfo [/s <computer> [/u <domain>\<username> [/p <password>]]] [/fo {TABLE | LIST | CSV}] [/nh]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /s `<computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Die Standardeinstellung ist der lokale Computer. |
| /u `<domain>\<username>` | Führt den Befehl mit den Konto Berechtigungen des angegebenen Benutzerkontos aus. Wenn **/u** nicht angegeben ist, verwendet dieser Befehl die Berechtigungen des Benutzers, der zurzeit auf dem Computer angemeldet ist, von dem der Befehl ausgegeben wird. |
| /p `<password>` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. |
| /FO `<format>` | Gibt das Ausgabeformat mit einem der folgenden Werte an:<ul><li>**Tabelle** : zeigt die Ausgabe in einer Tabelle an.</li><li>**List** : zeigt die Ausgabe in einer Liste an.</li><li>**CSV** : zeigt die Ausgabe im CSV-Format (Comma-Separated Values, Komma getrennte Werte) an.</li></ul> |
| /nh | Unterdrückt die Spaltenüberschriften in der Ausgabe. Gültig, wenn der **/FO** -Parameter auf Table oder CSV festgelegt ist. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um Konfigurationsinformationen für einen Computer namens *srvmain*anzuzeigen:

```
systeminfo /s srvmain
```

Geben Sie Folgendes ein, um Konfigurationsinformationen für einen Computer mit dem Namen *Srvmain2* , der sich in der *Maindom* -Domäne befindet, Remote anzuzeigen:

```
systeminfo /s srvmain2 /u maindom\hiropln
```

Geben Sie Folgendes ein, um die Konfigurationsinformationen (im Listenformat) für einen Computer mit dem Namen *Srvmain2* , der sich in der *Maindom* -Domäne befindet, Remote anzuzeigen:

```
systeminfo /s srvmain2 /u maindom\hiropln /p p@ssW23 /fo list
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
