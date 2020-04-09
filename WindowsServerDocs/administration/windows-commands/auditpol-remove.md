---
title: Auditpol entfernen
description: Windows-Befehls Thema für " **Auditpol Remove**", mit dem die Überwachungsrichtlinie pro Benutzer für ein angegebenes Konto oder für alle Konten entfernt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: be42ec55-235c-44f7-9abd-ed1cf3f5b1f5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1eda43d6708a31b2966022d2ae2c162bbfc888cb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851173"
---
# <a name="auditpol-remove"></a>Auditpol entfernen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Entfernt die Überwachungsrichtlinie pro Benutzer für ein angegebenes Konto oder für alle Konten.

## <a name="syntax"></a>Syntax

```
auditpol /remove [/user[:<username>|<{SID}>]]
[/allusers]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ------- | -------- |
| /User | Gibt die Sicherheits-ID (SID) oder den Benutzernamen für den Benutzer an, für den die Überwachungsrichtlinie pro Benutzer gelöscht werden soll. |
| /ALLUSERS | Entfernt die Überwachungsrichtlinie pro Benutzer für alle Benutzer. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="remarks"></a>Hinweise

Bei Entfernungs Vorgängen für die Richtlinie pro Benutzer müssen Sie über die Berechtigung Schreiben oder Vollzugriff für dieses Objekt verfügen, das in der Sicherheits Beschreibung festgelegt ist. Sie können auch Remove-Vorgänge durchführen, indem Sie das Benutzerrecht zum Verwalten von Überwachungs **-und Sicherheitsprotokollen** (SeSecurityPrivilege) besitzen. Dieses Recht ermöglicht jedoch zusätzlichen Zugriff, der zum Ausführen des Entfernungs Vorgangs nicht erforderlich ist.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
