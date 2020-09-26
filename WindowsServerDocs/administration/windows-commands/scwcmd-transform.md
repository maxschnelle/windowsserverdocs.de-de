---
title: scwcmd transform
description: Referenz Artikel zum Befehl "Scwcmd Transform", der eine mit dem Sicherheitskonfigurations-Assistenten (Security Configuration Wizard, SCW) generierte Sicherheitsrichtlinien Datei in ein neues Gruppenrichtlinie Objekt (GPO) in Active Directory Domain Services umwandelt.
ms.topic: reference
ms.assetid: 640dd892-0bb9-416d-8318-60a26605bcf4
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: bef3d9800d19ac0e3e574b4ef2e1195dcdc3baed
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91389253"
---
# <a name="scwcmd-transform"></a>scwcmd transform

> Gilt für: Windows Server 2012 R2 und Windows Server 2012

Transformiert eine mit dem Sicherheitskonfigurations-Assistenten (Security Configuration Wizard, SCW) generierte Sicherheitsrichtlinien Datei in ein neues Gruppenrichtlinie Objekt (GPO) in Active Directory Domain Services. Der Transformations Vorgang ändert keine Einstellungen auf dem Server, auf dem er ausgeführt wird. Nachdem der Transformations Vorgang abgeschlossen ist, muss ein Administrator das Gruppenrichtlinien Objekt mit den gewünschten Organisationseinheiten verknüpfen, um die Richtlinie auf den Servern bereitzustellen.

> [!IMPORTANT]
> Die Anmelde Informationen des Domänen Administrators sind erforderlich, um den Transformations Vorgang abzuschließen.
>
> Internetinformationsdienste (IIS)-Sicherheitsrichtlinien Einstellungen können nicht mithilfe von Gruppenrichtlinie bereitgestellt werden.
>
> Firewallrichtlinien, die genehmigte apps auflisten, sollten nur dann auf Servern bereitgestellt werden, wenn der Windows-Firewalldienst beim letzten Start des Servers automatisch gestartet wurde.

## <a name="syntax"></a>Syntax

```
scwcmd transform /p:<policyfile.xml> /g:<GPOdisplayname>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /p`<policyfile.xml>` | Gibt den Pfad und den Dateinamen der XML-Richtlinien Datei an, die angewendet werden soll. Dieser Parameter muss angegeben werden. |
| /g`<GPOdisplayname>` | Gibt den anzeigen amen des Gruppenrichtlinien Objekts an. Dieser Parameter muss angegeben werden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um ein Gruppenrichtlinien Objekt namens *fileserversecurity* aus einer Datei namens *FileServerPolicy.xml*zu erstellen:

```
scwcmd transform /p:FileServerPolicy.xml /g:FileServerSecurity
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [scwcmd-Analyse Befehl](scwcmd-analyze.md)

- [scwcmd-Befehl "configure"](scwcmd-configure.md)

- [scwcmd-register Befehl](scwcmd-register.md)

- [scwcmd-rollback-Befehl](scwcmd-rollback.md)

- [scwcmd-Ansichts Befehl](scwcmd-view.md)