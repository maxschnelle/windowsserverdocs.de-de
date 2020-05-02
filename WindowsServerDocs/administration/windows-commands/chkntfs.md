---
title: chkntfs
description: Referenz Thema für den Chkntfs-Befehl, der die automatische Datenträger Überprüfung beim Starten des Computers anzeigt oder ändert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 93eca810-8699-4716-8e9d-aecd54f704be
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 69b8e21a7b43538b6296666d813f2b33daa8045f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82713659"
---
# <a name="chkntfs"></a>chkntfs

Zeigt die automatische Datenträger Überprüfung an oder ändert diese, wenn der Computer gestartet wird. Bei Verwendung ohne Optionen zeigt **chkntfs** das Dateisystem des angegebenen Volumes an. Wenn die automatische Dateiüberprüfung zum Ausführen geplant ist, zeigt **chkntfs** an, ob das angegebene Volume geändert wurde oder beim nächsten Start des Computers überprüft werden soll.

> [!NOTE]
> Zum Ausführen von **chkntfs**müssen Sie ein Mitglied der Gruppe "Administratoren" sein.

## <a name="syntax"></a>Syntax

```
chkntfs <volume> [...]
chkntfs [/d]
chkntfs [/t[:<time>]]
chkntfs [/x <volume> [...]]
chkntfs [/c <volume> [...]]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<volume>` [...] | Gibt mindestens ein Volume an, das beim Starten des Computers überprüft werden soll. Zu den gültigen Volumes zählen Laufwerk Buchstaben (gefolgt von einem Doppelpunkt), Einstellungspunkte oder Volumenamen. |
| /d | Stellt alle **chkntfs** -Standardeinstellungen wieder her, außer der Countdownzeit für die automatische Dateiüberprüfung. Standardmäßig werden alle Volumes geprüft, wenn der Computer gestartet wird, und **chkdsk** wird auf dem Computer ausgeführt, der geändert wurde. |
| /t [`:<time>`] | Ändert die countdownzeitdauer von Autochk. exe auf die in Sekunden angegebene Zeitspanne. Wenn Sie keine Uhrzeit eingeben, zeigt **/t** den aktuellen countdownzeitraum an. |
| /x `<volume>` [...] | Gibt an, dass ein oder mehrere Volumes von der Überprüfung beim Start des Computers ausgeschlossen werden sollen, auch wenn das Volume als erforderliches **chkdsk**markiert ist. |
| /c `<volume>` [...] | Plant das Überprüfen eines oder mehrerer Volumes, wenn der Computer gestartet wird, und führt **chkdsk** auf den geänderten Datenträgern aus. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Typ des Dateisystems für Laufwerk C anzuzeigen:

```
chkntfs c:
```

> [!NOTE]
> Wenn die automatische Dateiüberprüfung geplant ist, wird eine zusätzliche Ausgabe angezeigt, die angibt, ob das Laufwerk geändert wurde oder manuell geplant wurde, wenn der Computer das nächste Mal gestartet wird.

Geben Sie Folgendes ein, um die Initialisierungs Zeit für Autochk. exe anzuzeigen:

```
chkntfs /t
```

Geben Sie Folgendes ein, um die countdownzeitdauer für Autochk. exe auf 30 Sekunden zu ändern:

```
chkntfs /t:30
```

> [!NOTE]
> Obwohl Sie die Countdownzeit für die Initiierung von Autochk. exe auf NULL festlegen können, wird dadurch verhindert, dass Sie eine potenziell zeitaufwändige automatische Dateiüberprüfung abbrechen.

Wenn Sie mehrere Volumes von der Überprüfung ausschließen möchten, müssen Sie diese in einem einzigen Befehl auflisten. Wenn Sie z. b. die Volumes D und E ausschließen möchten, geben Sie Folgendes ein:

```
chkntfs /x d: e:
```

> [!IMPORTANT]
> Die Befehlszeilenoption **/x** ist nicht akkumulierend. Wenn Sie ihn mehrmals eingeben, überschreibt der letzte Eintrag den vorherigen Eintrag.

Geben Sie die folgenden Befehle in der angegebenen Reihenfolge ein, um die automatische Dateiüberprüfung auf dem Laufwerk D, nicht jedoch auf den Volumes C oder E zu planen:

```
chkntfs /d
chkntfs /x c: d: e:
chkntfs /c d:
```

> [!IMPORTANT]
> Die Befehlszeilenoption **/c** ist akkumulierend. Wenn Sie **/c** mehrmals eingeben, bleibt jeder Eintrag erhalten. Um sicherzustellen, dass nur ein bestimmtes Volume überprüft wird, setzen Sie die Standardwerte zurück, um alle vorherigen Befehle zu löschen, alle Volumes von der Überprüfung ausschließen und dann die automatische Dateiüberprüfung auf dem gewünschten Volume zu planen.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
