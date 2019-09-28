---
title: chkntfs
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 93eca810-8699-4716-8e9d-aecd54f704be
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f940fe81f0e7e01495e071931059b2375b78bb22
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379340"
---
# <a name="chkntfs"></a>chkntfs



Zeigt die automatische Datenträger Überprüfung an oder ändert diese, wenn der Computer gestartet wird. Bei Verwendung ohne Optionen zeigt **chkntfs** das Dateisystem des angegebenen Volumes an. Wenn die automatische Dateiüberprüfung zum Ausführen geplant ist, zeigt **chkntfs** an, ob das angegebene Volume geändert wurde oder beim nächsten Start des Computers überprüft werden soll.

> [!NOTE]
> Zum Ausführen von **chkntfs**müssen Sie ein Mitglied der Gruppe "Administratoren" sein.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
chkntfs <Volume> [...]
chkntfs [/d]
chkntfs [/t[:<Time>]]
chkntfs [/x <Volume> [...]]
chkntfs [/c <Volume> [...]]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<volume > [...]|Gibt mindestens ein Volume an, das beim Starten des Computers überprüft werden soll. Zu den gültigen Volumes zählen Laufwerk Buchstaben (gefolgt von einem Doppelpunkt), Einstellungspunkte oder Volumenamen.|
|/d|Stellt alle **chkntfs** -Standardeinstellungen wieder her, außer der Countdownzeit für die automatische Dateiüberprüfung. Standardmäßig werden alle Volumes geprüft, wenn der Computer gestartet wird, und **chkdsk** wird auf dem Computer ausgeführt, der geändert wurde.|
|/t [: \<time >]|Ändert die countdownzeitdauer von Autochk. exe auf die in Sekunden angegebene Zeitspanne. Wenn Sie keine Uhrzeit eingeben, zeigt **/t** den aktuellen countdownzeitraum an.|
|/x \<volume > [...]|Gibt an, dass ein oder mehrere Volumes von der Überprüfung beim Start des Computers ausgeschlossen werden sollen, auch wenn das Volume als erforderliches **chkdsk**markiert ist.|
|/c \<volume > [...]|Plant das Überprüfen eines oder mehrerer Volumes, wenn der Computer gestartet wird, und führt **chkdsk** auf den geänderten Datenträgern aus.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um den Typ des Dateisystems für Laufwerk C anzuzeigen:
```
chkntfs c:
```
Die folgende Ausgabe zeigt ein NTFS-Dateisystem an:
```
The type of the file system is NTFS.
```

> [!NOTE]
> Wenn die automatische Dateiüberprüfung geplant ist, wird eine zusätzliche Ausgabe angezeigt, die angibt, ob das Laufwerk geändert wurde oder manuell geplant wurde, wenn der Computer das nächste Mal gestartet wird.

Geben Sie Folgendes ein, um die Initialisierungs Zeit für Autochk. exe anzuzeigen:
```
chkntfs /t
```
Wenn beispielsweise die Countdownzeit auf 10 Sekunden festgelegt ist, wird die folgende Ausgabe angezeigt:
```
The AUTOCHK initiation countdown time is set to 10 second(s).
```
Geben Sie Folgendes ein, um die countdownzeitdauer für Autochk. exe auf 30 Sekunden zu ändern:
```
chkntfs /t:30
```

> [!NOTE]
> Obwohl Sie die Countdownzeit für die Initiierung von Autochk. exe auf NULL festlegen können, wird dadurch verhindert, dass Sie eine potenziell zeitaufwändige automatische Dateiüberprüfung abbrechen.

Die Befehlszeilenoption **/x** ist nicht akkumulativ. Wenn Sie ihn mehrmals eingeben, überschreibt der letzte Eintrag den vorherigen Eintrag. Wenn Sie mehrere Volumes von der Überprüfung ausschließen möchten, müssen Sie diese in einem einzigen Befehl auflisten. Wenn Sie z. b. die Volumes D und E ausschließen möchten, geben Sie Folgendes ein:
```
chkntfs /x d: e:
```
Die Befehlszeilenoption **/c** ist akkumulierend. Wenn Sie **/c** mehrmals eingeben, bleibt jeder Eintrag erhalten. Um sicherzustellen, dass nur ein bestimmtes Volume überprüft wird, setzen Sie die Standardwerte zurück, um alle vorherigen Befehle zu löschen, alle Volumes von der Überprüfung ausschließen und dann die automatische Dateiüberprüfung auf dem gewünschten Volume zu planen.

Geben Sie die folgenden Befehle in der angegebenen Reihenfolge ein, um die automatische Dateiüberprüfung auf dem Laufwerk D, jedoch nicht auf den Volumes C oder E zu planen:
```
chkntfs /d
chkntfs /x c: d: e:
chkntfs /c d:
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)