---
title: Scwcmd-Register
description: Referenz Artikel für * * * *-
ms.topic: reference
ms.assetid: fe4d126a-9f27-4076-b7b1-fbefa45f378a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 644e4bff424b64b8e6a9a49b0b19320526b49a11
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89636996"
---
# <a name="scwcmd-register"></a>Scwcmd: registrieren

> Gilt für: Windows Server 2012 R2, Windows Server 2012

Erweitert oder passt die Sicherheitskonfigurations-Assistent (Security Configuration Wizard, SCW) Sicherheits Konfigurations Datenbank an, indem eine Sicherheits Konfigurations-Datenbankdatei registriert wird, die Rollen-, Task-, Dienst-oder Port Definitionen enthält

## <a name="syntax"></a>Syntax

```
scwcmd register /kbname:<MyApp> [/kbfile:<kb.xml>] [/kb:<path>] [/d]
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|/kbname:\<MyApp>|Gibt den Namen an, unter dem die Sicherheitskonfigurations-Daten Bank Erweiterung registriert wird. Dieser Parameter muss angegeben werden.|
|/kbfile:\<Kb.xml>|Gibt den Pfad und den Dateinamen der Sicherheitskonfigurations-Datenbankdatei an, die verwendet wird, um die Datenbank der Basis Sicherheitskonfiguration zu erweitern oder anzupassen. Um zu überprüfen, ob die Sicherheitskonfigurations-Datenbankdatei mit dem SCW-Schema kompatibel ist, verwenden Sie die Schema Definitionsdatei "%windir%\security\kbregistrationinfo.xsd". Diese Option muss angegeben werden, es sei denn, der **/d** -Parameter wird angegeben.|
|verarbeiten\<Path>|Gibt den Pfad zu dem Verzeichnis an, das die zu aktualisierenden SCW-Sicherheits Konfigurations-Datenbankdateien enthält. Wenn diese Option nicht angegeben ist, wird%windir%\security\msscw\ksb verwendet.|
|/d|Hebt die Registrierung einer Sicherheitskonfigurations-Daten Bank Erweiterung aus der Sicherheitskonfigurations-Datenbank auf. Die Erweiterung, deren Registrierung aufgehoben werden soll, wird durch den/kbname-Parameter angegeben. (Der **/kbfile** -Parameter sollte nicht angegeben werden.) Die Sicherheits Konfigurations Datenbank, von der die Registrierung der Erweiterung aufgehoben werden soll, wird durch den **/KB** -Parameter angegeben.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Scwcmd.exe ist nur auf Computern verfügbar, auf denen Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 ausgeführt wird.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Sicherheits Konfigurations-Datenbankdatei namens SCWKBForMyApp.xml unter dem Namen "MyApp" im Speicherort " \\ \\ kbserver\kb" zu registrieren
```
scwcmd register /kbfile:d:\SCWKBForMyApp.xml /kbname:MyApp /kb:\\kbserver\kb
```
Geben Sie Folgendes ein, um die Registrierung der Sicherheitskonfigurations-Datenbank MyApp in \\ \\ kbserver\kb aufzuheben:
```
scwcmd register /d /kbname:MyApp /kb:\\kbserver\kb
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)