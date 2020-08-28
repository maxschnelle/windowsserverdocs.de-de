---
title: prnqctl
description: Referenz Artikel für den prnqctl-Befehl, der eine Testseite ausgibt und einen Drucker anhält oder fortsetzt.
ms.topic: reference
ms.assetid: 8df9dfa7-984c-4276-bb7d-e7675e7c399e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: fd5eb91f280df80685d07c0b809e16edeae3d893
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033858"
---
# <a name="prnqctl"></a>prnqctl

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Druckt eine Testseite, hält einen Drucker an oder setzt ihn fort und löscht eine Drucker Warteschlange. Dieser Befehl ist ein Visual Basic Skript, das sich im `%WINdir%\System32\printing_Admin_Scripts\<language>` Verzeichnis befindet. Wenn Sie diesen Befehl an einer Eingabeaufforderung verwenden möchten, geben Sie **cscript** gefolgt vom vollständigen Pfad der prnqctl-Datei ein, oder ändern Sie die Verzeichnisse in den entsprechenden Ordner. Beispiel: `cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnqctl`.

## <a name="syntax"></a>Syntax

```
cscript Prnqctl {-z | -m | -e | -x | -?} [-s <Servername>] [-p <Printername>] [-u <Username>] [-w <password>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
|--|--|
| -Z | Hält den Druck auf dem Drucker an, der durch den **-p-** Parameter angegeben wird. |
| -M | Setzt den Druckvorgang auf dem Drucker fort, der durch den **-p-** Parameter angegeben wird. |
| -E | Druckt eine Testseite auf dem Drucker, der durch den **-p-** Parameter angegeben wird. |
| -X | Bricht alle Druckaufträge auf dem Drucker ab, der durch den **-p-** Parameter angegeben wird. |
| -s `<Servername>` | Gibt den Namen des Remote Computers an, der den Drucker hostet, den Sie verwalten möchten. Wenn Sie keinen Computer angeben, wird der lokale Computer verwendet. |
| -p `<Printername>` | Erforderlich. Gibt den Namen des Druckers an, den Sie verwalten möchten. |
| -u `<Username>` -w `<password>` | Gibt ein Konto mit Berechtigungen zum Herstellen einer Verbindung mit dem Computer an, der den zu verwaltenden Drucker hostet. Alle Mitglieder der lokalen Administratoren Gruppe des Ziel Computers verfügen über diese Berechtigungen, die Berechtigungen können jedoch auch anderen Benutzern erteilt werden. Wenn Sie kein Konto angeben, müssen Sie unter einem Konto mit diesen Berechtigungen angemeldet sein, damit der Befehl funktioniert. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Wenn die Informationen, die Sie angeben, Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen (z. b. "Computer Name").

### <a name="examples"></a>Beispiele

Zum Drucken einer Testseite auf dem Laserprinter1-Drucker, der vom Server1-Computer gemeinsam verwendet \\ wird, geben Sie Folgendes ein

```
cscript prnqctl -e -s Server1 -p Laserprinter1
```

Geben Sie Folgendes ein, um das Drucken auf dem Laserprinter1-Drucker auf dem lokalen Computer anzuhalten:

```
cscript prnqctl -z -p Laserprinter1
```

Um alle Druckaufträge auf dem Laserprinter1-Drucker auf dem lokalen Computer abzubrechen, geben Sie Folgendes ein:

```
cscript prnqctl -x -p Laserprinter1
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Druckbefehlsreferenz](print-command-reference.md)
