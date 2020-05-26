---
title: Wbadmin start systemstatebackup
description: Referenz Thema für Wbadmin start systemstatebackup, mit dem eine Systemstatus Sicherung des lokalen Computers erstellt und am angegebenen Speicherort gespeichert wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 998366c1-0a64-45e6-9ed3-4c3f5b8406f0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5de3531f19312b9d0d7969a63639db6388487bc2
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83821180"
---
# <a name="wbadmin-start-systemstatebackup"></a>Wbadmin start systemstatebackup



Erstellt eine Systemstatus Sicherung des lokalen Computers und speichert Sie am angegebenen Speicherort.

> [!NOTE]
> Windows Server-Sicherung dient nicht zum Sichern oder Wiederherstellen von registrierungsbenutzer Strukturen (HKEY_CURRENT_USER) im Rahmen der Sicherung oder Wiederherstellung des Systemstatus.

Wenn Sie mit diesem Unterbefehl eine Systemstatus Sicherung ausführen möchten, müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen. (Klicken Sie zum Öffnen einer Eingabeaufforderung mit erhöhten Rechten mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.)

## <a name="syntax"></a>Syntax

```
wbadmin start systemstatebackup
-backupTarget:<VolumeName>
[-quiet]
```

### <a name="parameters"></a>Parameter

|   Parameter   |                                                                                                                                                                                                                      BESCHREIBUNG                                                                                                                                                                                                                      |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| -backupTarget | Gibt den Speicherort an, an dem die Sicherung gespeichert werden soll. Der Speicherort erfordert einen Laufwerk Buchstaben oder ein GUID-basiertes Volume mit dem folgenden Format: \\ \\ ? \Volume{*GUID*}.</br>Eine Systemstatus Sicherung in einem freigegebenen Netzwerkordner wird auf Computern, auf denen Windows Server 2008 ausgeführt wird, nicht unterstützt. Wenn auf Ihrem Server Windows Server 2008 R2 oder höher ausgeführt wird, können Sie den Befehl " **backupTarget: \\ \\ servername\sharedfolder \\ ** " verwenden, um Systemstatus Sicherungen zu speichern. |
|    -quiet     |                                                                                                                                                                                                   Führt den Unterbefehl ohne Aufforderungen an den Benutzer aus.                                                                                                                                                                                                    |

## <a name="remarks"></a>Hinweise

Informationen zum Speichern einer Systemstatus Sicherung auf einem Volume, das wiederum Systemstatus Dateien enthält, finden Sie im Artikel 944530 in der Microsoft Knowledge Base ( [https://go.microsoft.com/fwlink/?LinkId=110439](https://go.microsoft.com/fwlink/?LinkId=110439) ).

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Systemstatus Sicherung zu erstellen und auf Volume f zu speichern:
```
wbadmin start systemstatebackup -backupTarget:f:
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Start-wbbackup-](https://technet.microsoft.com/library/jj902459.aspx) Cmdlet