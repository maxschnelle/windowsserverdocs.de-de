---
title: Wbadmin Start systemstatebackup
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 998366c1-0a64-45e6-9ed3-4c3f5b8406f0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d98ba295b2a76baf98e85a01a02677d57922877d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440264"
---
# <a name="wbadmin-start-systemstatebackup"></a>Wbadmin Start systemstatebackup



Erstellt eine Sicherung des Systemstatus des lokalen Computers ein, und speichert sie in der angegebenen Position.

> [!NOTE]
> Windows Server-Sicherung nicht sichern oder Benutzer Registrierungsstrukturen (HKEY_CURRENT_USER) als Teil des Systemstatus-Sicherung oder Wiederherstellung des Systemstatus wiederherstellen.

Um eine Sicherung des Systemstatus mit diesem Unterbefehl auszuführen, müssen Sie Mitglied werden die **Sicherungs-Operatoren** Gruppe oder der **Administratoren** Gruppe, oder Sie wurde die entsprechenden Berechtigungen delegiert. Darüber hinaus müssen Sie ausführen **Wbadmin** eine Eingabeaufforderung mit erhöhten Rechten. (Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.)

Beispiele zur Verwendung dieses Unterbefehl finden Sie in [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
wbadmin start systemstatebackup
-backupTarget:<VolumeName>
[-quiet]
```

## <a name="parameters"></a>Parameter

|   Parameter   |                                                                                                                                                                                                                      Beschreibung                                                                                                                                                                                                                      |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| -backupTarget | Gibt den Speicherort zum Speichern der Sicherung werden sollen. Der Speicherort ist erforderlich, einen Laufwerkbuchstaben oder einen GUID-basierte Volume das Format: \\ \\? \Volume {*GUID*}.</br>Eine Sicherung des Systemstatus auf einem freigegebenen Netzwerkordner wird auf einem Computer unter Windows Server 2008 nicht unterstützt. Wenn es sich bei Ihrem Server Windows Server 2008 R2 ausgeführt wird, oder höher können Sie den Befehl **- Backuptarget:\\\\Servername\sharedFolder\\**  zum Speichern von Sicherungen des Systemstatus. |
|    -quiet     |                                                                                                                                                                                                   Wird keine aufforderungen den Unterbefehl für dem Benutzer ausgeführt.                                                                                                                                                                                                    |

## <a name="remarks"></a>Hinweise

Enthält Informationen zum Speichern einer Sicherung des Systemstatus auf einem Volume, das wiederum Systemstatusdateien, finden Sie in der Microsoft Knowledge Base-Artikel 944530 ([https://go.microsoft.com/fwlink/?LinkId=110439](https://go.microsoft.com/fwlink/?LinkId=110439)).

## <a name="BKMK_examples"></a>Beispiele für

Erstellen eine Sicherung des Systemstatus aus, und speichern es auf Volume f, geben Sie Folgendes ein:
```
wbadmin start systemstatebackup -backupTarget:f:
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Start-WBBackup](https://technet.microsoft.com/library/jj902459.aspx) cmdlet