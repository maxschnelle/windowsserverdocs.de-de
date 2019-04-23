---
title: Satz mit "auditpol"
description: 'Windows-Befehle Thema **Auditpol Set** : Legt die Überwachungsrichtlinie pro Benutzer, die Dateisystem-Überwachungsrichtlinie oder Optionen für die Überwachung.'
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4947486-87bd-48cb-ba81-7230c8e70895
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c9c0fb17620147d2de5b991c1a9a0fb95e782677
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826991"
---
# <a name="auditpol-set"></a>Satz mit "auditpol"

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Legt den pro-Benutzer-Überwachungsrichtlinie, Dateisystem-Überwachungsrichtlinie oder Optionen für die Überwachung.

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
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/ User|Der Sicherheitsprinzipal für den benutzerspezifischen Überwachungsrichtlinie angegeben werden, indem Sie die Kategorie oder Unterkategorie festgelegt ist. Entweder die Kategorie oder Unterkategorie-Option muss angegeben werden, als Sicherheits-ID (SID) oder Namen.|
|/include|Mit %% amp;quot;/User%%amp;quot; angegeben. Gibt an, dass die Richtlinie des Benutzers pro Benutzer führt eine Überwachung, auch wenn er nicht, wird der Dateisystem-Überwachungsrichtlinie angegeben wird generiert werden. Diese Einstellung ist die Standardeinstellung und wird automatisch angewendet, wenn weder der / enthalten oder/EXCLUDE-Parameter explizit angegeben werden.|
|/exclude|Mit %% amp;quot;/User%%amp;quot; angegeben. Gibt an, dass die Richtlinie des Benutzers pro Benutzer verursacht eine Überwachung, die unabhängig von der Dateisystem-Überwachungsrichtlinie unterdrückt werden. Für Benutzer, die Mitglieder der lokalen Gruppe Administratoren sind, ist diese Einstellung ignoriert.|
|/category|Eine oder mehrere Überwachungskategorien von global eindeutigen Bezeichner (GUID) oder den Namen angegeben. Wenn kein Benutzer angegeben wird, wird die Systemrichtlinie festgelegt.|
|/subcategory|Eine oder mehrere überwachungsunterkategorien anhand des GUID oder den Namen. Wenn kein Benutzer angegeben wird, wird die Systemrichtlinie festgelegt.|
|/success|Gibt die erfolgreiche Überwachung. Diese Einstellung ist die Standardeinstellung und wird automatisch angewendet, wenn weder /success noch /failure Parameter explizit angegeben werden. Diese Einstellung muss mit einem Parameter, der angibt, ob aktivieren oder deaktivieren Sie die Einstellung verwendet werden.|
|/failure|Gibt die Fehlerüberwachung. Diese Einstellung muss mit einem Parameter, der angibt, ob aktivieren oder deaktivieren Sie die Einstellung verwendet werden.|
|/option|Legt die Überwachungsrichtlinie für die CrashOnAuditFail FullprivilegeAuditing, AuditBaseObjects oder AuditBasedirectories Optionen fest.|
|/sd|Legt die Sicherheitsbeschreibung, die zum Delegieren des Zugriffs auf die Überwachungsrichtlinie fest. Die Sicherheitsbeschreibung muss angegeben werden, mit der Security Descriptor Definition Language (SDDL). Die Sicherheitsbeschreibung muss es sich um eine besitzerverwaltete Zugriffssteuerungsliste (DACL) verfügen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="remarks"></a>Hinweise
für alle Vorgänge für die pro-Benutzer und Systemrichtlinien müssen Sie schreiben müssen, oder Full Control-Berechtigung für dieses Objekt festgelegt werden, in der Sicherheitsbeschreibung. Sie können auch die Set-Vorgänge ausführen, indem besitzt die **Verwalten von überwachungs- und Sicherheitsprotokollen** Benutzerrecht (SeSecurityPrivilege). Allerdings ermöglicht dieses Recht zusätzliche Zugriffsrechte, die nicht zum Ausführen des Set-Vorgangs erforderlich ist.
## <a name="BKMK_examples"></a>Beispiele für
### <a name="examples-for-the-per-user-audit-policy"></a>Beispiele für die Überwachungsrichtlinie pro Benutzer
Zum Festlegen Überwachungsrichtlinie der benutzerspezifischen für alle Unterkategorien in der ausführlichen Überwachung Kategorie für den Benutzer Mikedan, damit alles, was die erfolgreiche Versuche des Benutzers überwacht werden sollen, geben:
```
auditpol /set /user:mikedan /category:"detailed Tracking" /include /success:enable
```
Um die Überwachungsrichtlinie pro Benutzer, für den angegebenen Namen und GUID und Unterkategorien, die anhand des GUID zum Unterdrücken der Überwachung für alle erfolgreichen oder fehlgeschlagenen Versuche Kategorien festzulegen, geben Sie Folgendes ein:
```
auditpol /set /user:mikedan /exclude /category:"Object Access","System",{6997984b-797a-11d9-bed3-505054503030} 
/subcategory:{0ccee9210-69ae-11d9-bed3-505054503030},:{0ccee9211-69ae-11d9-bed3-505054503030}, /success:enable /failure:enable
```
Um die Überwachungsrichtlinie pro Benutzer für den angegebenen Benutzer für alle Kategorien für die Unterdrückung der Überwachung von alle bis auf erfolgreiche Versuche festzulegen, geben Sie Folgendes ein:
```
auditpol /set /user:mikedan /exclude /category:* /success:enable
```
### <a name="examples-for-the-system-audit-policy"></a>Beispiele für die Dateisystem-Überwachungsrichtlinie
Um die Systemüberwachungsrichtlinie für alle Unterkategorien unter der Kategorie ausführliche Überwachung gehören die Überwachung für nur erfolgreiche Versuche festzulegen, geben Sie Folgendes ein:
```
auditpol /set /category:"detailed Tracking" /success:enable
```
> [!NOTE]
> Die Einstellung wird nicht geändert.
Geben Sie Folgendes ein, um die Systemüberwachungsrichtlinie für den Zugriff auf Objekte und System-Kategorien (die impliziert wird, da die Unterkategorien aufgeführt sind) und Unterkategorien, die anhand des GUIDs für die Unterdrückung der fehlgeschlagenen Versuche und die Überwachung der erfolgreichen Versuche festzulegen:
```
auditpol /set /subcategory:{0ccee9210-69ae-11d9-bed3-505054503030},{0ccee9211-69ae-11d9-bed3-505054503030}, /failure:disable /success:enable
```
### <a name="example-for-auditing-options"></a>Beispiel für die Optionen für die Überwachung
Um die Überwachungsoptionen zu den aktivierten Zustand für die Option CrashOnAuditFail festzulegen, geben Sie Folgendes ein:
```
auditpol /set /option:CrashOnAuditFail /value:enable
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilensyntax](command-line-syntax-key.md)
