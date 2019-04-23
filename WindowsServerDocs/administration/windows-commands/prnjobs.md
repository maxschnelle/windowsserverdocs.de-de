---
title: prnjobs
description: Erfahren Sie, wie Druckaufträge über die Befehlszeile zu verwalten.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5ad34199-7a5a-40c1-8053-bccd5929df43
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 03a7f0cf36539272140ea39903bab585b4bc5c72
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889581"
---
# <a name="prnjobs"></a>prnjobs

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Wird angehalten, fortgesetzt wird, bricht ab und listet Druckaufträge.

## <a name="syntax"></a>Syntax
```
cscript Prnjobs {-z | -m | -x | -l | -?} [-s <ServerName>] 
[-p <printerName>] [-j <JobID>] [-u <UserName>] [-w <Password>]
```

## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|-z|Hält den Auftrag angegeben wird, mit der **+ j** Parameter.|
|-m|Setzt den Auftrag angegeben wird, mit der **+ j** Parameter.|
|-x|Bricht den Druckauftrag mit angegebenen ab der **+ j** Parameter.|
|-l|Listet alle Druckaufträge in einer Druckwarteschlange an.|
|-s \<ServerName >|Gibt den Namen des Remotecomputers, der den Drucker hostet, den Sie verwalten möchten. Wenn Sie einen Computer nicht angeben, wird der lokale Computer verwendet.|
|-p \<Druckername >|Gibt den Namen des Druckers, den Sie verwalten möchten. Erforderlich.|
|+ j \<Auftrags-ID >|Gibt den Druckauftrag, die, den Sie abbrechen möchten, (den ID-Nummer) an.|
|-u \<UserName > -w <Password>|Gibt ein Konto mit Berechtigungen zum Verbinden mit dem Computer, der den Drucker hostet, den Sie verwalten möchten. Alle Mitglieder der lokalen Gruppe Administratoren des Zielcomputers über diese Berechtigungen verfügen, aber die Berechtigungen können auch für andere Benutzer erteilt werden. Wenn Sie ein Konto nicht angeben, müssen Sie über ein Konto mit Berechtigungen für der Befehl funktioniert angemeldet sein.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Die **Prnjobs** Befehl ist eine Visual Basic-Skript befindet sich in der %WINdir%\System32\printing_Admin_Scripts\\ <language> Verzeichnis. Um diesen Befehl an einer Eingabeaufforderung verwenden möchten, geben **Cscript** gefolgt von den vollständigen Pfad und die Prnjobs-Datei, oder wechseln in den entsprechenden Ordner. Zum Beispiel:
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnjobs
    ```
-   Wenn die Informationen, die Sie angeben, die Leerzeichen enthält, verwenden Sie den Text in Anführungszeichen (z. B. `"computer Name"`).

## <a name="BKMK_examples"></a>Beispiele für
Geben Sie zum Anhalten eines Druckauftrags mit eine Auftrags-ID 27, die auf den Remotecomputer mit dem Namen HRServer für den Druck auf dem Drucker mit dem Namen Colorprinter gesendet:
```
cscript prnjobs -z -s HRServer -p colorprinter -j 27
```
Um alle aktuellen Druckaufträge in der Warteschlange für den lokalen Drucker mit dem Namen Farbdrucker_2 aufzulisten, geben Sie Folgendes ein:
```
cscript prnjobs -l -p colorprinter_2
```

#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[druckbefehlsreferenz](print-command-reference.md)
