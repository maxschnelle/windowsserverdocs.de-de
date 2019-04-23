---
title: Liste mit "auditpol"
description: 'Windows-Befehle Thema **"auditpol" Liste** : Listen Richtlinienkategorien und/oder Unterkategorien zu überwachen, oder Listen-Benutzer, die für die eine benutzerdefinierte Überwachungsrichtlinie definiert ist.'
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45502abe-3d6e-4e13-94f0-8e6fcb6db860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 08f524ef0aacd731f709ce7a2e17b3d831da1e5b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858581"
---
# <a name="auditpol-list"></a>Liste mit "auditpol"

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Listen überwachen Richtlinienkategorien und/oder Unterkategorien oder Listen-Benutzer, die für die eine benutzerdefinierte Überwachungsrichtlinie definiert ist.

## <a name="syntax"></a>Syntax
```
auditpol /list
[/user|/category|subcategory[:<categoryname>|<{guid}>|*]]
[/v] [/r]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/ User|Ruft alle Benutzer, die für die die Überwachungsrichtlinie pro Benutzer definiert wurde. Wenn Sie mit dem/v-Parameter verwendet wird, wird die Sicherheits-ID (SID) des Benutzers ebenfalls angezeigt.|
|/category|Zeigt die Namen der Kategorien, die vom System verstanden. Wenn Sie mit dem/v-Parameter verwendet wird, wird die Kategorie globally unique Identifier (GUID) wird ebenfalls angezeigt.|
|/subcategory|Zeigt die Namen von Unterkategorien und Ihnen jeweils zugeordnete GUID.|
|/v|Zeigt die GUID der Kategorie oder Unterkategorie oder bei Verwendung mit/User die SID eines einzelnen Benutzers.|
|/r|Zeigt die Ausgabe als ein Bericht im Format mit kommagetrennten Werten (CSV).|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="remarks"></a>Hinweise
für alle List-Vorgänge für die benutzerdefinierte Richtlinie müssen Sie für dieses Objekt festgelegt werden, in der Sicherheitsbeschreibung Leseberechtigung. Sie können auch die List-Vorgänge ausführen, indem besitzt die **Verwalten von überwachungs- und Sicherheitsprotokollen** Benutzerrecht (SeSecurityPrivilege). Allerdings ermöglicht dieses Recht zusätzliche Zugriffsrechte, die nicht zum Ausführen des List-Vorgangs erforderlich ist.
## <a name="BKMK_examples"></a>Beispiele für
Um alle Benutzer aufzulisten, die eine definierten Überwachungsrichtlinie haben, geben Sie Folgendes ein:
```
auditpol /list /user
```
Um alle Benutzer aufzulisten, die einer definierten Überwachungsrichtlinie und deren zugeordnete SID haben, geben Sie Folgendes ein:
```
auditpol /list /user /v
```
Um alle Kategorien und Unterkategorien im Berichtsformat aufzulisten, geben Sie Folgendes ein:
```
auditpol /list /subcategory:* /r
```
Um die Unterkategorien der detaillierten nachverfolgung und DS-Zugriff Kategorien aufzulisten, geben Sie Folgendes ein:
```
auditpol /list /subcategory:"detailed Tracking","DS Access"
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilensyntax](command-line-syntax-key.md)
