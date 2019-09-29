---
title: Auditpol entfernen
description: Thema Windows-Befehle für **Auditpol Remove** -entfernt die Überwachungsrichtlinie pro Benutzer für ein angegebenes Konto oder alle Konten.
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 2d652cb3bf7156bc1b1198616c9f6e57f588acd8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382478"
---
# <a name="auditpol-remove"></a>Auditpol entfernen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

entfernt die Überwachungsrichtlinie pro Benutzer für ein angegebenes Konto oder für alle Konten.

## <a name="syntax"></a>Syntax
```
auditpol /remove [/user[:<username>|<{SID}>]]
[/allusers]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/User|Gibt die Sicherheits-ID (SID) oder den Benutzernamen für den Benutzer an, für den die Überwachungsrichtlinie pro Benutzer gelöscht werden soll.|
|/ALLUSERS|entfernt die Überwachungsrichtlinie pro Benutzer für alle Benutzer.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="remarks"></a>Hinweise
bei Entfernungs Vorgängen für die Richtlinie pro Benutzer müssen Sie über die Berechtigung Schreiben oder Vollzugriff für dieses Objekt verfügen, das in der Sicherheits Beschreibung festgelegt ist. Sie können auch Remove-Vorgänge durchführen, indem Sie das Benutzerrecht zum Verwalten von Überwachungs **-und Sicherheitsprotokollen** (SeSecurityPrivilege) besitzen. Dieses Recht ermöglicht jedoch zusätzlichen Zugriff, der zum Ausführen des Entfernungs Vorgangs nicht erforderlich ist.
## <a name="BKMK_examples"></a>Beispiele
Geben Sie Folgendes ein, um die Überwachungsrichtlinie für den Benutzer Mikedan nach Name zu entfernen:
```
auditpol /remove /user:mikedan
```
Geben Sie Folgendes ein, um die Überwachungsrichtlinie pro Benutzer für den Benutzer Mikedan by sid zu entfernen:
```
auditpol /remove /user:{S-1-5-21-397123471-12346959}
```
Um die Überwachungsrichtlinie pro Benutzer für alle Benutzer zu entfernen, geben Sie Folgendes ein:
```
auditpol /remove /allusers
```
#### <a name="additional-references"></a>Weitere Verweise
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
