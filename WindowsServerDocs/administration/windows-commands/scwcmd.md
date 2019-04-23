---
title: scwcmd
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 188ae881-c7d4-4a7a-b967-8fdc79f5f345
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 19d631f97c194a78819491f32955e391d3be5a70
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883881"
---
# <a name="scwcmd"></a>scwcmd

> Gilt für: Windows Server 2012 R2, Windows Server 2012

Das Scwcmd.exe Befehlszeilenprogramm mit den (Security Configuration Wizard, SCW) kann verwendet werden, um die folgenden Aufgaben ausführen:
-   Konfigurieren Sie einen oder mehrere Server mit einer Richtlinie für den Sicherheitskonfigurations-Assistenten generierte.
-   Analysieren Sie einen oder mehrere Server mit einer Richtlinie für den Sicherheitskonfigurations-Assistenten generierte.
-   Anzeigen von Analyseergebnissen im HTML-Format.
-   Führt einen Rollback für SCW-Richtlinien aus.
-   Wandeln Sie eine Richtlinie für den Sicherheitskonfigurations-Assistenten generierte in systemeigenen Dateien, die von der Gruppenrichtlinie unterstützt werden.
-   Registrieren Sie eine Erweiterung der Sicherheitskonfigurationsdatenbank, mit dem Sicherheitskonfigurations-Assistenten.

Bei Verwendung von **Scwcmd** zu konfigurieren, zu analysieren oder Rollback für eine Richtlinie auf einem Remoteserver, SCW auf dem Remoteserver muss installiert sein.

## <a name="syntax"></a>Syntax

```
scwcmd <command> [<subcommand>]
```

## <a name="parameters"></a>Parameter

|Unterbefehl|Beschreibung|
|----------|-----------|
|/ analyze|Bestimmt, ob ein Computer mit der eine Richtlinie konform ist.</br>Finden Sie unter [Scwcmd: Analysieren von](scwcmd-analyze.md) für die Syntax und Optionen.|
|/configure|Wendet eine Sicherheitskonfigurations-Assistenten generierte Sicherheitsrichtlinie auf einem Computer an.</br>Finden Sie unter [Scwcmd: Konfigurieren von](scwcmd-configure.md) für die Syntax und Optionen.|
|/ Register|Erweitert oder passt die SCW-Sicherheitskonfigurationsdatenbank durch Registrieren einer Sicherheitskonfigurationsdatenbank-Datei, die Rolle, Tasks, Dienst oder Portieren von Definitionen enthält.</br>Finden Sie unter [Scwcmd: registrieren](scwcmd-register.md) für die Syntax und Optionen.|
|/rollback|Die neueste verfügbare Rollbackrichtlinie gilt, und löscht dann die Rollbackrichtlinie.</br>Finden Sie unter [Scwcmd: Rollback](scwcmd-rollback.md) für die Syntax und Optionen.|
|/transform|Transformiert eine Sicherheitsrichtliniendatei mithilfe des Sicherheitskonfigurations-Assistenten in ein neues Gruppenrichtlinienobjekt (GPO) in Active Directory Domain Services generiert.</br>Finden Sie unter [Scwcmd: Transformieren](scwcmd-transform.md) Syntax und Optionen.|
|/ View|Rendert eine XML-Datei mit einer angegebenen XSL-Transformation.</br>Finden Sie unter [Scwcmd: Ansicht](scwcmd-view.md) für die Syntax und Optionen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
