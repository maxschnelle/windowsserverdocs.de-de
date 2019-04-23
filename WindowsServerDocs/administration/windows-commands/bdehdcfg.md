---
title: bdehdcfg
description: Windows-Befehle Thema **Bdehdcfg** -bereitet eine Festplatte mit den notwendigen Partitionen für BitLocker-Laufwerkverschlüsselung.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c92cd74-188e-4fec-b7c4-fe4e8903e032
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a4fda562f4aa6b8caa885fcd70155b7150c91d12
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869701"
---
# <a name="bdehdcfg"></a>bdehdcfg



Bereitet eine Festplatte mit den notwendigen Partitionen für BitLocker-Laufwerkverschlüsselung vor. Die meisten Installationen von Windows 7 müssen nicht mit diesem Tool zu verwenden, da BitLocker-Setup bietet die Möglichkeit zum Vorbereiten und partitionieren die Laufwerke nach Bedarf.

> [!WARNING]
> Es gibt einen bekannten Konflikt mit der Gruppenrichtlinieneinstellung **Schreibzugriff auf Wechseldatenträger verweigern, die nicht durch BitLocker geschützt sind** unter **Computerkonfiguration\Administrative Vorlagen\Windows-Komponenten\BitLocker-Laufwerkverschlüsselung\Festplattenlaufwerke**.</br>> Wenn Bdehdcfg auf einem Computer ausgeführt wird, wenn diese richtlinieneinstellung aktiviert ist, können Sie die folgenden Probleme auftreten:</br>>: Wenn Sie das Laufwerk verkleinern und das Systemlaufwerk erstellen wollten die Laufwerkgröße erfolgreich reduziert und eine sogenannte raw-Partition erstellt werden. Die Raw-Partition wird nicht formatiert. Die folgende Fehlermeldung wird angezeigt: "Das neue aktive Laufwerk kann nicht formatiert werden. Sie müssen das Laufwerk möglicherweise manuell auf BitLocker vorbereiten.“</br>>-Wenn Sie Speicherplatz zum Erstellen des Systemlaufwerks verwenden wollten, wird eine sogenannte raw-Partition erstellt werden. Die Raw-Partition wird nicht formatiert. Die folgende Fehlermeldung wird angezeigt: "Das neue aktive Laufwerk kann nicht formatiert werden. Sie müssen das Laufwerk möglicherweise manuell auf BitLocker vorbereiten.“</br>>-Wenn Sie versucht haben, ein vorhandenes Laufwerk auf dem Systemlaufwerk zusammenzuführen, das Tool kann nicht auf das Ziellaufwerk zum Erstellen des Systemlaufwerks benötigte Startdatei zu kopieren. Die folgende Fehlermeldung wird angezeigt: "Fehler beim Kopieren von Startdateien. Sie müssen das Laufwerk möglicherweise manuell auf BitLocker vorbereiten.“</br>> Wenn diese richtlinieneinstellung erzwungen wird, kann kein Festplattenlaufwerk neu partitioniert werden, weil es geschützt ist. Wenn Sie ein Upgrade der Computer in ihrer Organisation von einer früheren Version von Windows durchführen und diese Computer mit einer einzelnen Partition konfiguriert waren, sollten Sie die erforderliche BitLocker-Systempartition erstellen, bevor Sie die Richtlinieneinstellung für die Computer übernehmen.

Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
bdehdcfg [–driveinfo <DriveLetter>] [-target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge}] [–newdriveletter] [–size <SizeinMB>] [-quiet]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[Bdehdcfg: driveinfo](bdehdcfg-driveinfo.md)|Zeigt den Laufwerkbuchstaben, beträgt die Gesamtgröße, der maximale freie Speicherplatz und die Partitionseigenschaften der Partitionen, auf dem angegebenen Laufwerk. Nur gültige Partitionen sind aufgeführt. Verfügbarer Speicher ist nicht aufgeführt, wenn bereits vier primäre oder erweiterte Partitionen vorhanden sind.|
|[Bdehdcfg: Ziel](bdehdcfg-target.md)|Definiert, welcher Teil eines Laufwerks als Systemlaufwerk verwendet, und aktiviert den Teil.|
|[Bdehdcfg: newdriveletter](bdehdcfg-newdriveletter.md)|Weist einen neuen Laufwerksbuchstaben, der Teil eines Laufwerks als Systemlaufwerk verwendet.|
|[Bdehdcfg: size](bdehdcfg-size.md)|Bestimmt die Größe der Systempartition, beim Erstellen ein neuen Systemlaufwerks erstellt wird.|
|[Bdehdcfg: quiet](bdehdcfg-quiet.md)|Verhindert die Anzeige von alle Aktionen und Fehler in der Befehlszeilenschnittstelle, und leitet Sie Bdehdcfg verwenden Sie die Antwort "Ja" Ja/eingabeaufforderungen, die bei der nachfolgenden Laufwerk vorbereiten.|
|[Bdehdcfg: restart](bdehdcfg-restart.md)|Weist den Computer neu starten, nachdem die laufwerksvorbereitung abgeschlossen wurde.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_Examples"></a>Beispiele für

Das folgende Beispiel zeigt die Bdehdcfg mit den standardmäßigen Datenträger verwendet wird, um eine Systempartition mit 500 MB zu erstellen. Da kein Laufwerkbuchstabe angeben ist, wird die neue Systempartition einen Laufwerkbuchstaben keine.
```
bdehdcfg -target default -size 500
```
Das folgende Beispiel zeigt Bdehdcfg mit den standardmäßigen Datenträger verwendet wird, um eine Systempartition (p) zu erstellen. die Standardgröße 300 MB verfügbaren Speicherplatz auf dem Laufwerk. Das Tool fordert den Benutzer für alle weiteren Eingabe wird nicht noch Fehlermeldungen angezeigt. Nachdem das Systemlaufwerk erstellt wurde, wird der Computer automatisch neu gestartet.
```
bdehdcfg -target unallocated –newdriveletter P: -quiet -restart
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)