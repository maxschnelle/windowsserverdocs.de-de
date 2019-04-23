---
title: "\"auditpol\" deaktivieren"
description: Windows-Befehle Thema **"auditpol" clear** -löscht die Überwachungsrichtlinie pro Benutzer, für alle Benutzer, Zurücksetzen von Kennwörtern (deaktiviert) des Systems Überwachungsrichtlinie für alle Unterkategorien aus, und legt alle die Überwachung auf "Optionen" deaktiviert.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 05bfa218-2434-4ad1-b33c-e6fcfb2b4f67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 453579589f3fd3cc2c9fa835b50bfb59e33bc3dc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872581"
---
# <a name="auditpol-clear"></a>"auditpol" deaktivieren

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Löscht die Überwachungsrichtlinie pro Benutzer, für alle Benutzer, Zurücksetzen von Kennwörtern (deaktiviert) des Systems Überwachungsrichtlinie für alle Unterkategorien aus, und legt Optionen für alle die Überwachung deaktiviert.

## <a name="syntax"></a>Syntax
```
auditpol /clear [/y]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/y|Unterdrückt die Eingabeaufforderung zur Bestätigung, wenn alle sicherheitsüberwachungs-Richtlinieneinstellungen, die gelöscht werden sollen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="remarks"></a>Hinweise
für Vorgänge für die pro-Benutzer und Systemrichtlinien zum Löschen müssen Sie schreiben müssen, oder Full Control-Berechtigung für dieses Objekt festgelegt werden, in der Sicherheitsbeschreibung. Sie können auch den Löschvorgang ausführen, indem besitzt die **Verwalten von überwachungs- und Sicherheitsprotokollen** Benutzerrecht (SeSecurityPrivilege). Diese Berechtigung ermöglicht jedoch zusätzliche Zugriffsrechte, die nicht erforderlich, um den Löschvorgang auszuführen ist.
## <a name="BKMK_examples"></a>Beispiele für
Geben die sicherheitsüberwachungs-Richtlinieneinstellungen deaktiviert, die an einer Eingabeaufforderung zur Bestätigung, um die Überwachungsrichtlinie pro Benutzer, für alle Benutzer, zurücksetzen (deaktivieren) der Dateisystem-Überwachungsrichtlinie für alle Unterkategorien und Set zu löschen:
```
auditpol /clear
```
Um die Überwachungsrichtlinie pro Benutzer, für alle Benutzer zu löschen, Zurücksetzen der System-sicherheitsüberwachungs-Richtlinieneinstellungen für alle Unterkategorien, und Einstellungen festlegen, dass alle die Überwachung deaktiviert, ohne eine bestätigungsaufforderung, Typ:
```
auditpol /clear /y
```
> [!NOTE]
> Im vorherige Beispiel ist nützlich, wenn ein Skript verwenden, um diesen Vorgang auszuführen.
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilensyntax](command-line-syntax-key.md)
