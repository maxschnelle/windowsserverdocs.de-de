---
title: scwcmd rollback
description: Referenz Artikel für den scwcmd-rollback-Befehl, der die letzte verfügbare Rollback-Richtlinie anwendet und diese Rollback-Richtlinie löscht.
ms.topic: reference
ms.assetid: 4fd9f89b-0420-420a-ad20-4a328636b1e7
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e8f50995131ca01ea2bb58ee9371b12d9ec9a917
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388910"
---
# <a name="scwcmd-rollback"></a>scwcmd rollback

> Gilt für: Windows Server 2012 R2 und Windows Server 2012

Wendet die neueste Rollback-Richtlinie an und löscht dann diese Rollback-Richtlinie.

## <a name="syntax"></a>Syntax

```
scwcmd rollback /m:<computername> [/u:<username>] [/pw:<password>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /m`<computername>` | Gibt den NetBIOS-Namen, den DNS-Namen oder die IP-Adresse eines Computers an, auf dem der Rollback-Vorgang ausgeführt werden soll. |
| /u`<username>` | Gibt ein alternatives Benutzerkonto an, das beim Ausführen eines Remote Rollbacks verwendet werden soll. Der Standardwert ist der angemeldete Benutzer. |
| /PW`<password>` | Gibt alternative Benutzer Anmelde Informationen an, die beim Ausführen eines Remote Rollbacks verwendet werden sollen. Der Standardwert ist der angemeldete Benutzer. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um ein Rollback der Sicherheitsrichtlinie auf einem Computer unter IP-Adresse *172.16.0.0*auszuführen:

```
scwcmd rollback /m:172.16.0.0
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [scwcmd-Analyse Befehl](scwcmd-analyze.md)

- [scwcmd-Befehl "configure"](scwcmd-configure.md)

- [scwcmd-register Befehl](scwcmd-register.md)

- [Befehl "Scwcmd Transform"](scwcmd-transform.md)

- [scwcmd-Ansichts Befehl](scwcmd-view.md)