---
title: auditpol set
description: Referenz Artikel für den Befehl Auditpol Set, mit dem die Überwachungsrichtlinie pro Benutzer, die System Überwachungsrichtlinie oder die Überwachungs Optionen festgelegt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f4947486-87bd-48cb-ba81-7230c8e70895
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bc42168d65116261d57053e0812cbb49e17021d5
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923694"
---
# <a name="auditpol-set"></a>auditpol set

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt die Überwachungsrichtlinie pro Benutzer, die System Überwachungsrichtlinie oder die Überwachungs Optionen fest.

Zum Ausführen von *Set* -Vorgängen für die *Benutzer-* und *System* Richtlinien müssen Sie über die Berechtigung **Schreiben** oder **voll** Zugriff für dieses Objekt verfügen, das in der Sicherheits Beschreibung festgelegt ist. Sie können *Set* -Vorgänge auch ausführen, wenn Sie über das Benutzerrecht zum Verwalten von Überwachungs **-und Sicherheitsprotokollen** (SeSecurityPrivilege) verfügen. Dieses Recht ermöglicht jedoch zusätzlichen Zugriff, der nicht erforderlich ist, um die Gesamt *Menge* der Vorgänge auszuführen.

## <a name="syntax"></a>Syntax

```
auditpol /set
[/user[:<username>|<{sid}>][/include][/exclude]]
[/category:<name>|<{guid}>[,:<name|<{guid}> ]]
[/success:<enable>|<disable>][/failure:<enable>|<disable>]
[/subcategory:<name>|<{guid}>[,:<name|<{guid}> ]]
[/success:<enable>|<disable>][/failure:<enable>|<disable>]
[/option:<option name> /value: <enable>|<disable>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| /User | Der Sicherheits Prinzipal, für den die von der Kategorie oder Unterkategorie angegebene Überwachungsrichtlinie pro Benutzer festgelegt ist. Die Option Category oder SubCategory muss als Sicherheits-ID (SID) oder Name angegeben werden. |
| /include | Angegeben mit/User; Gibt an, dass die Richtlinie pro Benutzer des Benutzers bewirkt, dass eine Überwachung generiert wird, auch wenn Sie nicht von der System Überwachungsrichtlinie angegeben wird. Diese Einstellung ist die Standardeinstellung und wird automatisch angewendet, wenn weder der/include-noch der/Exclude-Parameter explizit angegeben wird. |
| /Exclude | Angegeben mit/User; Gibt an, dass die Richtlinie pro Benutzer des Benutzers bewirkt, dass eine Überwachung unabhängig von der System Überwachungsrichtlinie unterdrückt wird. Diese Einstellung wird für Benutzer ignoriert, die Mitglieder der lokalen Administrator Gruppe sind. |
| /category | Eine oder mehrere Überwachungs Kategorien, die durch Globally Unique Identifier (GUID) oder den Namen angegeben werden. Wenn kein Benutzer angegeben ist, wird die System Richtlinie festgelegt. |
| /SubCategory | Eine oder mehrere Überwachungs Unterkategorien, die durch GUID oder Name angegeben werden. Wenn kein Benutzer angegeben ist, wird die System Richtlinie festgelegt. |
| /Success | Gibt die erfolgreiche Überwachung an. Diese Einstellung ist die Standardeinstellung und wird automatisch angewendet, wenn weder der/Success-noch der/Failure-Parameter explizit angegeben wird. Diese Einstellung muss mit einem Parameter verwendet werden, der angibt, ob die Einstellung aktiviert oder deaktiviert werden soll. |
| /Failure | Gibt die Fehlerüberwachung an. Diese Einstellung muss mit einem Parameter verwendet werden, der angibt, ob die Einstellung aktiviert oder deaktiviert werden soll. |
| /Option | Legt die Überwachungsrichtlinie für die Optionen CrashOnAuditFail, FullPrivilegeAuditing, auditbaseobjects oder auditbasedirectories fest. |
| /sd | Legt die Sicherheits Beschreibung fest, die zum Delegieren des Zugriffs auf die Überwachungsrichtlinie verwendet wird. Die Sicherheits Beschreibung muss mithilfe der Security Deskriptor Definition Language (SDDL) angegeben werden. Die Sicherheits Beschreibung muss über eine freigegebene Zugriffs Steuerungs Liste (DACL) verfügen. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Überwachungsrichtlinie pro Benutzer für alle Unterkategorien in der Kategorie detaillierte Nachverfolgung für den Benutzer Mikedan festzulegen, damit alle erfolgreichen Versuche des Benutzers überwacht werden:

```
auditpol /set /user:mikedan /category:detailed Tracking /include /success:enable
```

Geben Sie Folgendes ein, um die Überwachungsrichtlinie pro Benutzer für durch Name und GUID angegebene Kategorien und Unterkategorien festzulegen, die durch GUID angegeben werden, um die Überwachung für erfolgreiche oder fehlgeschlagene Versuche zu unterdrücken:

```
auditpol /set /user:mikedan /exclude /category:Object Access,System,{6997984b-797a-11d9-bed3-505054503030}
/subcategory:{0ccee9210-69ae-11d9-bed3-505054503030},:{0ccee9211-69ae-11d9-bed3-505054503030}, /success:enable /failure:enable
```

Geben Sie Folgendes ein, um die Überwachungsrichtlinie pro Benutzer für den angegebenen Benutzer für alle Kategorien festzulegen, um die Überwachung aller bis auf erfolgreiche Versuche zu unterdrücken:
```
auditpol /set /user:mikedan /exclude /category:* /success:enable
```

Geben Sie Folgendes ein, um die System Überwachungsrichtlinie für alle Unterkategorien in der Kategorie "detaillierte Nachverfolgung" so festzulegen, dass nur erfolgreiche Versuche überwacht werden:

```
auditpol /set /category:detailed Tracking /success:enable
```

> [!NOTE]
> Die Fehler Einstellung wird nicht geändert.

Geben Sie Folgendes ein, um die System Überwachungsrichtlinie für die Objekt Zugriffs-und System Kategorien festzulegen (was impliziert ist, weil Unterkategorien aufgeführt sind) und Unterkategorien, die von GUIDs für die Unterdrückung fehlgeschlagener Versuche und die Überwachung erfolgreicher Versuche angegeben werden:

```
auditpol /set /subcategory:{0ccee9210-69ae-11d9-bed3-505054503030},{0ccee9211-69ae-11d9-bed3-505054503030}, /failure:disable /success:enable
```

Geben Sie Folgendes ein, um die Überwachungs Optionen auf den aktivierten Status für die CrashOnAuditFail-Option festzulegen:

```
auditpol /set /option:CrashOnAuditFail /value:enable
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Auditpol-Befehle](auditpol.md)
