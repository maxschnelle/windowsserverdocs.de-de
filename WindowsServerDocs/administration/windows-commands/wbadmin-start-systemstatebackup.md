---
title: Wbadmin start systemstatebackup
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 0244f984d29c8a802475d2dc08f1cdfe4495f0b9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362228"
---
# <a name="wbadmin-start-systemstatebackup"></a>Wbadmin start systemstatebackup



Erstellt eine Systemstatus Sicherung des lokalen Computers und speichert Sie am angegebenen Speicherort.

> [!NOTE]
> Windows Server-Sicherung dient nicht zum Sichern oder Wiederherstellen von registrierungsbenutzer Strukturen (HKEY_CURRENT_USER) im Rahmen der Sicherung oder Wiederherstellung des Systemstatus.

Wenn Sie mit diesem Unterbefehl eine Systemstatus Sicherung ausführen möchten, müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen. (Klicken Sie zum Öffnen einer Eingabeaufforderung mit erhöhten Rechten mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.)

Beispiele für die Verwendung dieses Unterbefehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
wbadmin start systemstatebackup
-backupTarget:<VolumeName>
[-quiet]
```

## <a name="parameters"></a>Parameter

|   Parameter   |                                                                                                                                                                                                                      Beschreibung                                                                                                                                                                                                                      |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| -backupTarget | Gibt den Speicherort an, an dem die Sicherung gespeichert werden soll. Der Speicherort erfordert einen Laufwerk Buchstaben oder ein GUID-basiertes Volume im Format: \\ @ no__t-1? \Volume{*GUID*}.</br>Eine Systemstatus Sicherung in einem freigegebenen Netzwerkordner wird auf Computern, auf denen Windows Server 2008 ausgeführt wird, nicht unterstützt. Wenn auf Ihrem Server Windows Server 2008 R2 oder höher ausgeführt wird, können Sie den Befehl **-backupTarget: \\ @ no__t-2servername\sharedFolder @ no__t-3** verwenden, um Systemstatus Sicherungen zu speichern. |
|    -quiet     |                                                                                                                                                                                                   Führt den Unterbefehl ohne Aufforderungen an den Benutzer aus.                                                                                                                                                                                                    |

## <a name="remarks"></a>Hinweise

Informationen zum Speichern einer Systemstatus Sicherung auf einem Volume, das wiederum Systemstatus Dateien enthält, finden Sie im Artikel 944530 in der Microsoft Knowledge Base ([https://go.microsoft.com/fwlink/?LinkId=110439](https://go.microsoft.com/fwlink/?LinkId=110439)).

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Systemstatus Sicherung zu erstellen und auf Volume f zu speichern:
```
wbadmin start systemstatebackup -backupTarget:f:
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Start-wbbackup-](https://technet.microsoft.com/library/jj902459.aspx) Cmdlet