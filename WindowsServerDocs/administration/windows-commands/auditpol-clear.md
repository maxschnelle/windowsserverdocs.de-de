---
title: auditpol clear
description: Der Referenz Artikel für den Befehl Auditpol Clear, der die Überwachungsrichtlinie für alle Benutzer pro Benutzer löscht, setzt die System Überwachungsrichtlinie für alle Unterkategorien zurück (deaktiviert Sie) und legt alle Überwachungs Optionen auf deaktiviert fest.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 05bfa218-2434-4ad1-b33c-e6fcfb2b4f67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 797f26ab9e191176808bbce917ca5ac0fa3d73a3
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923797"
---
# <a name="auditpol-clear"></a>auditpol clear

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löscht die Überwachungsrichtlinie pro Benutzer für alle Benutzer, setzt die System Überwachungsrichtlinie für alle Unterkategorien zurück (deaktiviert Sie) und legt alle Überwachungs Optionen auf deaktiviert fest.

Zum Ausführen *von* Lösch Vorgängen für *Benutzer-* und *System* Richtlinien müssen Sie über die Berechtigung **Schreiben** oder **voll** Zugriff für dieses Objekt verfügen, das in der Sicherheits Beschreibung festgelegt ist. Sie können auch *Clear* -Vorgänge ausführen, wenn Sie über das Benutzerrecht zum Verwalten von Überwachungs **-und Sicherheitsprotokollen** (SeSecurityPrivilege) verfügen. Dieses Recht ermöglicht jedoch zusätzlichen Zugriff, der nicht erforderlich ist, um *die allgemeinen Lösch* Vorgänge auszuführen.

## <a name="syntax"></a>Syntax

```
auditpol /clear [/y]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ----------- | --------------- |
| /y | Unterdrückt die Eingabeaufforderung, um zu bestätigen, dass alle Überwachungs Richtlinien Einstellungen gelöscht werden sollen. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

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

- [Auditpol-Befehle](auditpol.md)
