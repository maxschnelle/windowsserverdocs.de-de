---
title: chkntfs
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 876c0e0c254216ac217aea7d165d5f4e3a7da9b4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861991"
---
# <a name="chkntfs"></a>chkntfs



Zeigt oder ändert automatisch Datenträger überprüfen, wenn der Computer gestartet wird. Ohne Angabe von Optionen **Chkntfs** zeigt das Dateisystem des angegebenen Volumes. Wenn die Überprüfung der automatischen Ausführung geplant ist, **Chkntfs** angezeigt, ob das angegebene Volume fehlerhaft ist oder geplant ist, überprüft das nächste Mal den Computer wird gestartet.

> [!NOTE]
> Auszuführende **Chkntfs**, Sie müssen Mitglied der Gruppe "Administratoren" sein.

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
|\<Volume > [...]|Gibt an, ein oder mehrere Volumes, um zu überprüfen, wenn der Computer gestartet wird. Gültige Volumes einbeziehen Laufwerkbuchstaben (gefolgt von einem Doppelpunkt) bereitstellen, Punkte oder Volume-Namen.|
|/d|Stellt alle **Chkntfs** Standardeinstellungen, außer den Countdown für die Überprüfung der automatischen. Alle Volumes sind standardmäßig aktiviert, wenn der Computer gestartet wird, und **Chkdsk** ausgeführt wird, die geändert werden.|
|/ t [:\<Zeit >]|Ändert den Autochk.exe Initiierungscountdown auf die Zeitdauer in Sekunden angegeben. Wenn Sie nicht einzeln eingeben **/t /** zeigt den aktuellen Countdown.|
|/ x \<Volume > [...]|Gibt an, ein oder mehrere Volumes auszuschließende aus beim Starten des Computers, selbst wenn das Volume, erfordert gekennzeichnet ist **Chkdsk**.|
|/ c \<Volume > [...]|Plant eine oder mehrere Volumes, die überprüft werden, wenn der Computer gestartet wird und ausgeführt wird **Chkdsk** auf diejenigen, die geändert werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_examples"></a>Beispiele für

Um den Typ des Dateisystems für Laufwerk C: anzuzeigen, geben Sie Folgendes ein:
```
chkntfs c:
```
Die folgende Ausgabe zeigt ein NTFS-Dateisystem an:
```
The type of the file system is NTFS.
```

> [!NOTE]
> Wenn die Überprüfung der automatischen Ausführung geplant ist, werden zusätzliche Ausgabe wird angezeigt, gestartet wird, der angibt, ob das Laufwerk fehlerhaft ist oder wurde manuell geplante sich das nächste Mal der Computer überprüft.

Um den Autochk.exe Initiierungscountdown anzuzeigen, geben Sie Folgendes ein:
```
chkntfs /t
```
Wenn der Countdown auf 10 Sekunden festgelegt ist, wird z. B. die folgende Ausgabe angezeigt:
```
The AUTOCHK initiation countdown time is set to 10 second(s).
```
Um den Autochk.exe Initiierungscountdown auf 30 Sekunden zu ändern, geben Sie Folgendes ein:
```
chkntfs /t:30
```

> [!NOTE]
> Obwohl die Autochk.exe Initiierung Countdownzeit 0 (null) festgelegt werden können, dies also Sie verhindert, dass eine möglicherweise zeitaufwendige automatische dateiüberprüfung Abbrechen.

Die **/x** Befehlszeilenoption ist nicht kumulativ. Wenn Sie es mehr als einmal eingeben, überschreibt den letzte Eintrag des vorherigen Eintrags. Um mehrere Datenträger werden von der Überprüfung auszuschließen, müssen Sie jedes Mitglied in einem einzigen Befehl auflisten. Geben Sie z. B. zum Ausschließen von D und E-Volumes:
```
chkntfs /x d: e:
```
Die **/c** Befehlszeilenoption ist kumulativ. Wenn Sie eingeben **/c** mehr als einmal auf jeder Eintrag bleibt. Um sicherzustellen, dass nur ein bestimmtes Volume aktiviert ist, stellen Sie die Standardeinstellungen, deaktivieren Sie alle früheren Befehle ausschließen, dass alle Volumes überprüft wird, und dann die planen Sie automatische Prüfung auf das gewünschte Volume Datei.

Geben Sie z. B. um automatische Prüfung auf das Volume D, aber nicht die Volumes C oder E-Datei zu planen, die folgenden Befehle in der Reihenfolge:
```
chkntfs /d
chkntfs /x c: d: e:
chkntfs /c d:
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)