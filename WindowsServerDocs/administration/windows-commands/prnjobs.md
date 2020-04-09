---
title: prnjobs
description: Erfahren Sie, wie Druckaufträge über die Befehlszeile verwaltet werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5ad34199-7a5a-40c1-8053-bccd5929df43
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 231b8a7a9f4f8623b3d84cc789064d256883a733
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837293"
---
# <a name="prnjobs"></a>prnjobs

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

hält Druckaufträge an, setzt Sie fort, bricht Sie ab und listet Sie auf.

## <a name="syntax"></a>Syntax
```
cscript Prnjobs {-z | -m | -x | -l | -?} [-s <ServerName>] 
[-p <printerName>] [-j <JobID>] [-u <UserName>] [-w <Password>]
```

### <a name="parameters"></a>Parameter

|          Parameter           |                                                                                                                                                                                        Beschreibung                                                                                                                                                                                        |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              -z              |                                                                                                                                                                 hält den Druckauftrag an, der mit dem **-j-** Parameter angegeben wird.                                                                                                                                                                 |
|              -m              |                                                                                                                                                                Setzt den mit dem **-j-** Parameter angegebenen Druckauftrag fort.                                                                                                                                                                 |
|              -x              |                                                                                                                                                                Bricht den mit dem **-j-** Parameter angegebenen Druckauftrag ab.                                                                                                                                                                 |
|              -l              |                                                                                                                                                                        Listet alle Druckaufträge in einer Druck Warteschlange auf.                                                                                                                                                                         |
|       -s \<Servername >       |                                                                                                                  Gibt den Namen des Remote Computers an, der den Drucker hostet, den Sie verwalten möchten. Wenn Sie keinen Computer angeben, wird der lokale Computer verwendet.                                                                                                                  |
|      -p \<PrinterName >       |                                                                                                                                                           Gibt den Namen des Druckers an, den Sie verwalten möchten. Erforderlich                                                                                                                                                            |
|         -j \<JobID >          |                                                                                                                                                                Gibt (nach ID-Nummer) den Druckauftrag an, den Sie abbrechen möchten.                                                                                                                                                                 |
| -u \<Benutzername >-w <Password> | Gibt ein Konto mit Berechtigungen zum Herstellen einer Verbindung mit dem Computer an, der den zu verwaltenden Drucker hostet. Alle Mitglieder der lokalen Administratoren Gruppe des Ziel Computers verfügen über diese Berechtigungen, die Berechtigungen können jedoch auch anderen Benutzern erteilt werden. Wenn Sie kein Konto angeben, müssen Sie unter einem Konto mit diesen Berechtigungen angemeldet sein, damit der Befehl funktioniert. |
|              /?              |                                                                                                                                                                           Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                            |

## <a name="remarks"></a>Hinweise
-   Der **prnjobs** -Befehl ist ein Visual Basic Skript, das sich im Verzeichnis "%windir%\SYSTEM32\ printing_Admin_Scripts\\<language>" befindet. Wenn Sie diesen Befehl verwenden möchten, geben Sie an einer Eingabeaufforderung **cscript** gefolgt vom vollständigen Pfad zur Datei prnjobs ein, oder ändern Sie die Verzeichnisse in den entsprechenden Ordner. Beispiel:
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnjobs.vbs
    ```
-   Wenn die Informationen, die Sie angeben, Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen (z. b. `"computer Name"`).

## <a name="examples"></a><a name="BKMK_examples"></a>Beispiele
Geben Sie Folgendes ein, um einen Druckauftrag mit der Auftrags-ID 27 anzuhalten, die auf dem Remote Computer mit dem Namen HRServer zum Drucken auf dem Drucker mit dem Namen COLORPRINTER gesendet wurde:
```
cscript prnjobs.vbs -z -s HRServer -p colorprinter -j 27
```
Um alle aktuellen Druckaufträge in der Warteschlange für den lokalen Drucker namens colorprinter_2 aufzulisten, geben Sie Folgendes ein:
```
cscript prnjobs.vbs -l -p colorprinter_2
```

## <a name="additional-references"></a>Weitere Verweise

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Druckbefehlsreferenz](print-command-reference.md)
