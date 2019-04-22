---
title: Entfernen von "auditpol"
description: Windows-Befehle Thema **"auditpol" entfernen** -entfernt die Überwachungsrichtlinie pro Benutzer, für ein angegebenes Konto "oder" alle Konten.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: be42ec55-235c-44f7-9abd-ed1cf3f5b1f5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 566827e93d9f8c9dc0d00f4f704513369fbb44ad
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818301"
---
# <a name="auditpol-remove"></a>Entfernen von "auditpol"

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Entfernt die Überwachungsrichtlinie pro Benutzer, für ein angegebenes Konto "oder" alle Konten.

## <a name="syntax"></a>Syntax
```
auditpol /remove [/user[:<username>|<{SID}>]]
[/allusers]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/ User|Gibt an, die Sicherheits-ID (SID) oder Benutzernamen für den Benutzer, die für die benutzerspezifischen Überwachungsrichtlinie wird gelöscht werden soll.|
|/ALLUSERS|Entfernt die Überwachungsrichtlinie pro Benutzer, für alle Benutzer.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="remarks"></a>Hinweise
für Remove-Vorgänge für die benutzerdefinierte Richtlinie müssen Sie Schreib-oder Vollzugriff auf das Objekt, das in der Sicherheitsbeschreibung festgelegt. Sie können auch Remove-Vorgänge ausführen, indem besitzt die **Verwalten von überwachungs- und Sicherheitsprotokollen** Benutzerrecht (SeSecurityPrivilege). Diese Berechtigung ermöglicht jedoch zusätzliche Zugriffsrechte, die nicht zum Ausführen des Entfernungsvorgangs erforderlich ist.
## <a name="BKMK_examples"></a>Beispiele für
Um die Überwachungsrichtlinie pro Benutzer, für die Benutzer Mikedan anhand des Namens zu entfernen, geben Sie Folgendes ein:
```
auditpol /remove /user:mikedan
```
Um die Überwachungsrichtlinie pro Benutzer, für Benutzer Mikedan SID zu entfernen, geben Sie Folgendes ein:
```
auditpol /remove /user:{S-1-5-21-397123471-12346959}
```
Um die Überwachungsrichtlinie pro Benutzer, für alle Benutzer zu entfernen, geben Sie Folgendes ein:
```
auditpol /remove /allusers
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilensyntax](command-line-syntax-key.md)
