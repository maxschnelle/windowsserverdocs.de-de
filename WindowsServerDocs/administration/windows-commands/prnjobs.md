---
title: prnjobs
description: Referenz Artikel zum prnjobs-Befehl, der Druckaufträge anhält, fortsetzt, abbricht und auflistet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5ad34199-7a5a-40c1-8053-bccd5929df43
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 79ad0631a2d1c871664ecebc11c26f2e005ca772
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924199"
---
# <a name="prnjobs"></a>prnjobs

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Hält Druckaufträge an, setzt Sie fort, bricht Sie ab und listet Sie auf. Dieser Befehl ist ein Visual Basic Skript, das sich im `%WINdir%\System32\printing_Admin_Scripts\<language>` Verzeichnis befindet. Wenn Sie diesen Befehl an einer Eingabeaufforderung verwenden möchten, geben Sie **cscript** gefolgt vom vollständigen Pfad zur Datei prnjobs ein, oder ändern Sie die Verzeichnisse in den entsprechenden Ordner. Beispiel: `cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnjobs.vbs`.

## <a name="syntax"></a>Syntax

```
cscript prnjobs {-z | -m | -x | -l | -?} [-s <Servername>] [-p <Printername>] [-j <JobID>] [-u <Username>] [-w <password>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
|--|--|
| -Z | Hält den Druckauftrag an, der durch den **-j-** Parameter angegeben wird. |
| -M | Setzt den Druckauftrag fort, der durch den **-j-** Parameter angegeben wird. |
| -X | Bricht den Druckauftrag ab, der durch den **-j-** Parameter angegeben wird. |
| -l | Listet alle Druckaufträge in einer Druck Warteschlange auf. |
| -s`<Servername>` | Gibt den Namen des Remote Computers an, der den Drucker hostet, den Sie verwalten möchten. Wenn Sie keinen Computer angeben, wird der lokale Computer verwendet. |
| -p`<Printername>` | Erforderlich. Gibt den Namen des Druckers an, den Sie verwalten möchten. |
| -j`<JobID>` | Gibt (nach ID-Nummer) den Druckauftrag an, den Sie abbrechen möchten. |
| -u `<Username>` -w`<password>` | Gibt ein Konto mit Berechtigungen zum Herstellen einer Verbindung mit dem Computer an, der den zu verwaltenden Drucker hostet. Alle Mitglieder der lokalen Administratoren Gruppe des Ziel Computers verfügen über diese Berechtigungen, die Berechtigungen können jedoch auch anderen Benutzern erteilt werden. Wenn Sie kein Konto angeben, müssen Sie unter einem Konto mit diesen Berechtigungen angemeldet sein, damit der Befehl funktioniert. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Wenn die Informationen, die Sie angeben, Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen (z. b. "Computer Name").

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um einen Druckauftrag mit der Auftrags-ID 27 anzuhalten, die auf dem Remote Computer mit dem Namen HRServer zum Drucken auf dem Drucker mit dem Namen COLORPRINTER gesendet wurde:

```
cscript prnjobs.vbs -z -s HRServer -p colorprinter -j 27
```

Um alle aktuellen Druckaufträge in der Warteschlange für den lokalen Drucker namens colorprinter_2 aufzulisten, geben Sie Folgendes ein:

```
cscript prnjobs.vbs -l -p colorprinter_2
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Druckbefehlsreferenz](print-command-reference.md)
