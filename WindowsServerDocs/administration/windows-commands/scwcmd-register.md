---
title: Scwcmd-Register
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 2e892f7c08461e88d12a072dfb171f9523558ef7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371223"
---
# <a name="scwcmd-register"></a>scwcmd: register

> Gilt für: Windows Server 2012 R2, Windows Server 2012

Erweitert oder passt die Sicherheitskonfigurations-Assistent (Security Configuration Wizard, SCW) Sicherheits Konfigurations Datenbank an, indem eine Sicherheits Konfigurations-Datenbankdatei registriert wird, die Rollen-, Task-, Dienst-oder Port Definitionen enthält

## <a name="syntax"></a>Syntax

```
scwcmd register /kbname:<MyApp> [/kbfile:<kb.xml>] [/kb:<path>] [/d]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/kbname: \<myapp >|Gibt den Namen an, unter dem die Sicherheitskonfigurations-Daten Bank Erweiterung registriert wird. Dieser Parameter muss angegeben werden.|
|/kbfile: @no__t -0KB. XML >|Gibt den Pfad und den Dateinamen der Sicherheitskonfigurations-Datenbankdatei an, die verwendet wird, um die Datenbank der Basis Sicherheitskonfiguration zu erweitern oder anzupassen. Um zu überprüfen, ob die Sicherheitskonfigurations-Datenbankdatei mit dem SCW-Schema kompatibel ist, verwenden Sie die Schema Definitionsdatei "%windir%\security\kbregistrationinfo.xsd". Diese Option muss angegeben werden, es sei denn, der **/d** -Parameter wird angegeben.|
|/KB: \<path >|Gibt den Pfad zu dem Verzeichnis an, das die zu aktualisierenden SCW-Sicherheits Konfigurations-Datenbankdateien enthält. Wenn diese Option nicht angegeben ist, wird%windir%\security\msscw\ksb verwendet.|
|/d|Hebt die Registrierung einer Sicherheitskonfigurations-Daten Bank Erweiterung aus der Sicherheitskonfigurations-Datenbank auf. Die Erweiterung, deren Registrierung aufgehoben werden soll, wird durch den/kbname-Parameter angegeben. (Der **/kbfile** -Parameter sollte nicht angegeben werden.) Die Sicherheits Konfigurations Datenbank, von der die Registrierung der Erweiterung aufgehoben werden soll, wird durch den **/KB** -Parameter angegeben.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Scwcmd. exe ist nur auf Computern verfügbar, auf denen Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 ausgeführt wird.

## <a name="BKMK_Examples"></a>Beispiele

Geben Sie Folgendes ein, um die Sicherheitskonfigurations-Datenbankdatei "scwkbformyapp. xml" unter dem Namen "MyApp" am Speicherort \\ @ no__t-1kbserver\kb zu registrieren:
```
scwcmd register /kbfile:d:\SCWKBForMyApp.xml /kbname:MyApp /kb:\\kbserver\kb
```
Geben Sie Folgendes ein, um die Registrierung der Sicherheitskonfigurations-Datenbank MyApp unter \\ @ no__t-1kbserver\kb aufzuheben:
```
scwcmd register /d /kbname:MyApp /kb:\\kbserver\kb
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)