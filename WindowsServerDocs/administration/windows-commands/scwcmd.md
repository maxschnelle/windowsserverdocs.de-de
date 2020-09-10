---
title: Scwcmd
description: Referenz Artikel für * * * *-
ms.topic: reference
ms.assetid: 188ae881-c7d4-4a7a-b967-8fdc79f5f345
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4095d022a9bd84033eebf63b63420dc400f2c594
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89636870"
---
# <a name="scwcmd"></a>Scwcmd

> Gilt für: Windows Server 2012 R2, Windows Server 2012

Mit dem Befehlszeilen Tool Scwcmd.exe, das im Sicherheitskonfigurations-Assistenten (Security Configuration Wizard, SCW) enthalten ist, können folgende Aufgaben ausgeführt werden:
-   Konfigurieren Sie einen oder mehrere Server mit einer vom SCW generierten Richtlinie.
-   Analysieren Sie einen oder mehrere Server mit einer vom SCW generierten Richtlinie.
-   Anzeigen der Analyseergebnisse im HTML-Format.
-   Zurücksetzen von SCW-Richtlinien
-   Transformieren Sie eine SCW-generierte Richtlinie in systemeigene Dateien, die von Gruppenrichtlinie unterstützt werden.
-   Registrieren Sie eine Sicherheitskonfigurations-Daten Bank Erweiterung mit SCW.

Wenn Sie **scwcmd** verwenden, um eine Richtlinie auf einem Remote Server zu konfigurieren, zu analysieren oder zurückzusetzen, muss SCW auf dem Remote Server installiert sein.

## <a name="syntax"></a>Syntax

```
scwcmd <command> [<subcommand>]
```

### <a name="parameters"></a>Parameter

|Unterbefehl|Beschreibung|
|----------|-----------|
|/analyze|Bestimmt, ob ein Computer mit einer Richtlinie konform ist.</br>Weitere Informationen finden Sie unter [scwcmd: analysieren](scwcmd-analyze.md) für Syntax und Optionen.|
|/configure|Wendet eine vom SCW generierte Sicherheitsrichtlinie auf einen Computer an.</br>Weitere Informationen finden Sie unter [scwcmd: Configure](scwcmd-configure.md) for Syntax and options.|
|/Register|Erweitert oder passt die Sicherheits Konfigurations Datenbank von SCW an, indem eine Sicherheits Konfigurations-Datenbankdatei registriert wird, die Rollen-, Task-, Dienst-oder Port Definitionen enthält.</br>Weitere Informationen finden Sie unter [scwcmd: Register](scwcmd-register.md) für Syntax und Optionen.|
|/rollback|Wendet die neueste Rollback-Richtlinie an und löscht dann diese Rollback-Richtlinie.</br>Weitere Informationen finden Sie unter [scwcmd: Rollback](scwcmd-rollback.md) für Syntax und Optionen.|
|/Transform|Transformiert eine mit SCW generierte Sicherheitsrichtlinien Datei in ein neues Gruppenrichtlinie Objekt (GPO) in Active Directory Domain Services.</br>Weitere Informationen finden Sie unter [scwcmd: Transformieren](scwcmd-transform.md) von Syntax und Optionen.|
|/view|Rendert eine XML-Datei mithilfe einer angegebenen XSL-Transformation.</br>Informationen zur Syntax und zu Optionen finden Sie unter [scwcmd: View](scwcmd-view.md) .|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
