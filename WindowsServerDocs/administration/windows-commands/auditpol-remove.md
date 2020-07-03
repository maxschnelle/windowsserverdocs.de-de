---
title: auditpol remove
description: Referenz Artikel für den Befehl Auditpol Remove, mit dem die Überwachungsrichtlinie pro Benutzer für ein bestimmtes Konto oder für alle Konten entfernt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: be42ec55-235c-44f7-9abd-ed1cf3f5b1f5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: aada45bdc128c3122f459813d6f015f58532de18
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923727"
---
# <a name="auditpol-remove"></a>auditpol remove

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Entfernt die Überwachungsrichtlinie pro Benutzer für ein angegebenes Konto oder für alle Konten.

Um *Entfernungs* Vorgänge für die Richtlinie *pro Benutzer* auszuführen, müssen Sie über die Berechtigung **Schreiben** oder **voll** Zugriff für dieses Objekt verfügen, das in der Sicherheits Beschreibung festgelegt ist. Sie können auch *Entfernungs* Vorgänge ausführen, wenn Sie über das Benutzerrecht zum Verwalten von Überwachungs **-und Sicherheitsprotokollen** (SeSecurityPrivilege) verfügen. Dieses Recht ermöglicht jedoch zusätzlichen Zugriff, der zum Ausführen der allgemeinen *Entfernungs* Vorgänge nicht erforderlich ist.

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

## <a name="examples"></a>Beispiele

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

- [Auditpol-Befehle](auditpol.md)
