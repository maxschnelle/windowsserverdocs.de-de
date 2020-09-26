---
title: scwcmd
description: Referenz Artikel für das scwcmd.exe Befehlszeilen Tool, das im Sicherheitskonfigurations-Assistenten (Security Configuration Wizard, SCW) enthalten ist.
ms.topic: reference
ms.assetid: 188ae881-c7d4-4a7a-b967-8fdc79f5f345
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 87bd2c718bec18810026c5701b955d5ef655b53e
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388920"
---
# <a name="scwcmd"></a>scwcmd

> Gilt für: Windows Server 2012 R2 und Windows Server 2012

Mit dem Befehlszeilen Tool Scwcmd.exe, das im Sicherheitskonfigurations-Assistenten (Security Configuration Wizard, SCW) enthalten ist, können folgende Aufgaben ausgeführt werden:

- Analysieren Sie einen oder mehrere Server mit einer vom SCW generierten Richtlinie.

- Konfigurieren Sie einen oder mehrere Server mit einer vom SCW generierten Richtlinie.

- Registrieren Sie eine Sicherheitskonfigurations-Daten Bank Erweiterung mit SCW.

- Zurücksetzen von SCW-Richtlinien

- Transformieren Sie eine SCW-generierte Richtlinie in systemeigene Dateien, die von Gruppenrichtlinie unterstützt werden.

- Anzeigen der Analyseergebnisse im HTML-Format.

> [!NOTE]
> Wenn Sie **scwcmd** verwenden, um eine Richtlinie auf einem Remote Server zu konfigurieren, zu analysieren oder zurückzusetzen, muss SCW auf dem Remote Server installiert sein.

## <a name="syntax"></a>Syntax

```
scwcmd analyze
scwcmd configure
scwcmd register
scwcmd rollback
scwcmd transform
scwcmd view
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| [scwcmd analyze](scwcmd-analyze.md) | Bestimmt, ob ein Computer mit einer Richtlinie konform ist. |
| [scwcmd configure](scwcmd-configure.md) | Wendet eine vom SCW generierte Sicherheitsrichtlinie auf einen Computer an.|
| [scwcmd register](scwcmd-register.md) | Erweitert oder passt die Sicherheits Konfigurations Datenbank von SCW an, indem eine Sicherheits Konfigurations-Datenbankdatei registriert wird, die Rollen-, Task-, Dienst-oder Port Definitionen enthält. |
| [scwcmd rollback](scwcmd-rollback.md) | Wendet die neueste Rollback-Richtlinie an und löscht dann diese Rollback-Richtlinie. |
| [scwcmd transform](scwcmd-transform.md) | Transformiert eine mit SCW generierte Sicherheitsrichtlinien Datei in ein neues Gruppenrichtlinie Objekt (GPO) in Active Directory Domain Services. |
| [scwcmd view](scwcmd-view.md) | Rendert eine XML-Datei mithilfe einer angegebenen XSL-Transformation. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
