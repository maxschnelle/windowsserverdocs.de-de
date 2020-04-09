---
title: Auditpol Clear
description: Thema für Windows-Befehle für **Auditpol Clear**, das die Überwachungsrichtlinie pro Benutzer für alle Benutzer löscht, setzt die System Überwachungsrichtlinie für alle Unterkategorien zurück (deaktiviert Sie) und legt alle Überwachungs Optionen auf deaktiviert fest.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 05bfa218-2434-4ad1-b33c-e6fcfb2b4f67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 971f4ba54d787be29cb9e7d710f556c50c69a8dc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851203"
---
# <a name="auditpol-clear"></a>Auditpol Clear

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löscht die Überwachungsrichtlinie pro Benutzer für alle Benutzer, setzt die System Überwachungsrichtlinie für alle Unterkategorien zurück (deaktiviert Sie) und legt alle Überwachungs Optionen auf deaktiviert fest.

## <a name="syntax"></a>Syntax

```
auditpol /clear [/y]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ----------- | --------------- |
| /y | Unterdrückt die Eingabeaufforderung, um zu bestätigen, dass alle Überwachungs Richtlinien Einstellungen gelöscht werden sollen. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="remarks"></a>Hinweise

Für Löschvorgänge für die Richtlinie und die System Richtlinie pro Benutzer müssen Sie über die Berechtigung Schreiben oder Vollzugriff für dieses Objekt verfügen, das in der Sicherheits Beschreibung festgelegt ist. Sie können den Löschvorgang auch durchführen, indem Sie das Benutzerrecht zum Verwalten von Überwachungs **-und Sicherheitsprotokollen** (SeSecurityPrivilege) besitzen. Dieses Recht ermöglicht jedoch zusätzlichen Zugriff, der nicht erforderlich ist, um den Löschvorgang auszuführen.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Wenn Sie die Überwachungsrichtlinie pro Benutzer für alle Benutzer löschen möchten, setzen Sie die System Überwachungsrichtlinie für alle Unterkategorien zurück (deaktivieren Sie Sie), und legen Sie alle Überwachungs Richtlinien Einstellungen in einer Bestätigungsaufforderung auf deaktiviert fest. Geben Sie Folgendes ein:

```
auditpol /clear
```

Wenn Sie die Überwachungsrichtlinie für alle Benutzer pro Benutzer löschen möchten, setzen Sie die System Überwachungs Richtlinien Einstellungen für alle Unterkategorien zurück, und legen Sie alle Überwachungs Richtlinien Einstellungen ohne Bestätigungsaufforderung auf deaktiviert fest. Geben Sie Folgendes ein:

```
auditpol /clear /y
```

> [!NOTE]
> Das vorangehende Beispiel ist nützlich, wenn ein Skript verwendet wird, um diesen Vorgang auszuführen.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
