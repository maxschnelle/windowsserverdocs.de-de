---
title: wbadmin start systemstatebackup
description: Referenz Artikel für den Wbadmin start systemstatebackup-Befehl, mit dem eine Systemstatus Sicherung des lokalen Computers erstellt und am angegebenen Speicherort gespeichert wird.
ms.topic: reference
ms.assetid: 998366c1-0a64-45e6-9ed3-4c3f5b8406f0
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: afdfb3f4a52ae0f5897517f8d59069bea820bc4a
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524725"
---
# <a name="wbadmin-start-systemstatebackup"></a>wbadmin start systemstatebackup

Erstellt eine Systemstatus Sicherung des lokalen Computers und speichert Sie am angegebenen Speicherort.

Wenn Sie mit diesem Befehl eine Systemstatus Sicherung ausführen möchten, müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen, indem Sie mit der rechten Maustaste auf **Eingabeaufforderung**klicken und dann **als Administrator ausführen**auswählen.

> [!NOTE]
> Windows Server-Sicherung im Rahmen der Sicherung oder Wiederherstellung des Systemstatus die registrierungsbenutzer Strukturen (HKEY_CURRENT_USER) nicht sichern oder wiederherstellen.

## <a name="syntax"></a>Syntax

```
wbadmin start systemstatebackup -backupTarget:<VolumeName> [-quiet]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| -backupTarget | Gibt den Speicherort an, an dem die Sicherung gespeichert werden soll. Der Speicherort erfordert einen Laufwerk Buchstaben oder ein GUID-basiertes Volume im folgenden Format: `\\?\Volume{*GUID*}` . Verwenden Sie den-Befehl `-backuptarget:\\servername\sharedfolder\` , um Sicherungen des Systemstatus zu speichern. |
| -quiet | Führt den Befehl ohne Aufforderungen an den Benutzer aus. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Systemstatus Sicherung zu erstellen und auf Volume f zu speichern:

```
wbadmin start systemstatebackup -backupTarget:f:
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Wbadmin-Befehl](wbadmin.md)

- [Start-wbbackup](/powershell/module/windowserverbackup/Start-WBBackup)
