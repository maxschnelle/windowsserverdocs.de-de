---
title: Scwcmd-register
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe4d126a-9f27-4076-b7b1-fbefa45f378a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cc8b4a06af519b0da01dfcab8de0139b12cc68f2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834971"
---
# <a name="scwcmd-register"></a>scwcmd: register

> Gilt für: Windows Server 2012 R2, Windows Server 2012

Erweitert oder passt die Sicherheitskonfigurationsdatenbank (Security Configuration Wizard, SCW) durch Registrieren einer Sicherheitskonfigurationsdatenbank-Datei, die Rolle, Tasks, Dienst oder Portieren von Definitionen enthält.

## <a name="syntax"></a>Syntax

```
scwcmd register /kbname:<MyApp> [/kbfile:<kb.xml>] [/kb:<path>] [/d]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/kbname:\<MyApp>|Gibt den Namen, unter dem die Sicherheitskonfigurationsdatenbank Erweiterung registriert werden. Dieser Parameter muss angegeben werden.|
|/kbfile:\<Kb.xml>|Gibt an, der Pfad und Dateiname der Sicherheitskonfigurationsdatenbank-Datei, die zum Erweitern oder Anpassen der Basis Sicherheitskonfigurationsdatenbank verwendet werden. Um zu überprüfen, dass die Sicherheitskonfigurationsdatenbank-Datei mit dem Sicherheitskonfigurations-Assistent-Schema konform ist, verwenden Sie die %windir%\security\KBRegistrationInfo.xsd Schemadefinitionsdatei. Diese Option muss angegeben werden, es sei denn, die **/d** Parameter angegeben ist.|
|/kb:\<Path>|Gibt den Pfad zu dem Verzeichnis, das die SCW-Sicherheitskonfigurationsdatenbank aktualisiert werden, enthält. Wenn diese Option nicht angegeben ist, wird die %windir%\security\msscw\kbs verwendet.|
|/d|Hebt die Registrierung einer Erweiterungs Sicherheitskonfigurationsdatenbank, aus der Konfigurationsdatenbank für die Sicherheit. Die Erweiterung zum Aufheben der Registrierung wird von der kbname-Parameter angegeben. (Die **/kbfile** Parameter nicht angegeben werden darf.) Die Sicherheitskonfigurationsdatenbank beim Aufheben der Registrierung der Erweiterungs wird angegeben, durch die **Sicherheitskonfigurations** Parameter.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Scwcmd.exe ist nur auf Computern unter Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 verfügbar.

## <a name="BKMK_Examples"></a>Beispiele für

Zum Registrieren der Sicherheitskonfigurationsdatenbank-Datei mit dem Namen SCWKBForMyApp.xml unter dem Namen "MyApp" am Standort \\ \\Kbserver\kb, Typ:
```
scwcmd register /kbfile:d:\SCWKBForMyApp.xml /kbname:MyApp /kb:\\kbserver\kb
```
Beim Aufheben der Registrierung der Security Configuration Database "MyApp" am \\ \\Kbserver\kb, Typ:
```
scwcmd register /d /kbname:MyApp /kb:\\kbserver\kb
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)