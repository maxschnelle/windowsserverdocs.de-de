---
title: bdehdcfg
description: 'Windows-Befehls Thema für **bdehdcfg** : bereitet eine Festplatte mit den für BitLocker-Laufwerkverschlüsselung erforderlichen Partitionen vor.'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: acfe2582905402f7be149148520784be6ad47453
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382192"
---
# <a name="bdehdcfg"></a>bdehdcfg



Bereitet eine Festplatte mit den für BitLocker-Laufwerkverschlüsselung erforderlichen Partitionen vor. Bei den meisten Installationen von Windows 7 muss dieses Tool nicht verwendet werden, da das BitLocker-Setup die Möglichkeit bietet, Laufwerke nach Bedarf vorzubereiten und neu zu partitionieren.

> [!WARNING]
> Es gibt einen bekannten Konflikt mit der Gruppenrichtlinieneinstellung **Schreibzugriff auf Wechseldatenträger verweigern, die nicht durch BitLocker geschützt sind** unter **Computerkonfiguration\Administrative Vorlagen\Windows-Komponenten\BitLocker-Laufwerkverschlüsselung\Festplattenlaufwerke**.</br>> Wenn bdehdcfg auf einem Computer ausgeführt wird, wenn diese Richtlinien Einstellung aktiviert ist, können die folgenden Probleme auftreten:</br>>: Wenn Sie versucht haben, das Laufwerk zu verkleinern und das Systemlaufwerk zu erstellen, wird die Laufwerk Größe erfolgreich reduziert, und es wird eine Rohpartition erstellt. Die Raw-Partition wird nicht formatiert. Die folgende Fehlermeldung wird angezeigt: "Das neue aktive Laufwerk kann nicht formatiert werden. Sie müssen das Laufwerk möglicherweise manuell auf BitLocker vorbereiten.“</br>>: Wenn Sie versucht haben, den nicht zugeordneten Speicherplatz zum Erstellen des System Laufwerks zu verwenden, wird eine Rohpartition erstellt. Die Raw-Partition wird nicht formatiert. Die folgende Fehlermeldung wird angezeigt: "Das neue aktive Laufwerk kann nicht formatiert werden. Sie müssen das Laufwerk möglicherweise manuell auf BitLocker vorbereiten.“</br>>: Wenn Sie versucht haben, ein vorhandenes Laufwerk mit dem Systemlaufwerk zusammenzuführen, kann das Tool die erforderliche Startdatei nicht auf das Ziellaufwerk kopieren, um das Systemlaufwerk zu erstellen. Die folgende Fehlermeldung wird angezeigt: "Fehler beim Kopieren von Startdateien. Sie müssen das Laufwerk möglicherweise manuell auf BitLocker vorbereiten.“</br>> Wenn diese Richtlinien Einstellung erzwungen wird, kann eine Festplatte nicht neu partitioniert werden, da das Laufwerk geschützt ist. Wenn Sie ein Upgrade der Computer in ihrer Organisation von einer früheren Version von Windows durchführen und diese Computer mit einer einzelnen Partition konfiguriert waren, sollten Sie die erforderliche BitLocker-Systempartition erstellen, bevor Sie die Richtlinieneinstellung für die Computer übernehmen.

Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
bdehdcfg [–driveinfo <DriveLetter>] [-target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge}] [–newdriveletter] [–size <SizeinMB>] [-quiet]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[Bdehdcfg: DriveInfo](bdehdcfg-driveinfo.md)|Zeigt den Laufwerk Buchstaben, die Gesamtgröße, den maximalen freien Speicherplatz und die Partitions Merkmale der Partitionen auf dem angegebenen Laufwerk an. Nur gültige Partitionen sind aufgeführt. Verfügbarer Speicher ist nicht aufgeführt, wenn bereits vier primäre oder erweiterte Partitionen vorhanden sind.|
|[Bdehdcfg: Ziel](bdehdcfg-target.md)|Definiert, welcher Teil eines Laufwerks als Systemlaufwerk verwendet werden soll, und macht den Teil aktiv.|
|[Bdehdcfg: newdriveletter](bdehdcfg-newdriveletter.md)|Weist dem Teil eines Laufwerks, das als Systemlaufwerk verwendet wird, einen neuen Laufwerk Buchstaben zu.|
|[Bdehdcfg: Größe](bdehdcfg-size.md)|Bestimmt die Größe der Systempartition beim Erstellen eines neuen System Laufwerks.|
|[Bdehdcfg: Quiet](bdehdcfg-quiet.md)|Verhindert, dass alle Aktionen und Fehler in der Befehlszeilenschnittstelle angezeigt werden, und leitet bdehdcfg zur Verwendung der "yes"-Antwort auf alle Ja/Nein-Eingabe Aufforderungen, die während der nachfolgenden Laufwerks Vorbereitung auftreten können.|
|[Bdehdcfg: neu starten](bdehdcfg-restart.md)|Der Computer wird nach Abschluss der Laufwerks Vorbereitung an den Neustart umgeleitet.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_Examples"></a>Beispiele

Das folgende Beispiel zeigt bdehdcfg, das mit dem Standard Laufwerk verwendet wird, um eine Systempartition von 500 MB zu erstellen. Da kein Laufwerk Buchstabe angegeben wird, weist die neue Systempartition keinen Laufwerk Buchstaben auf.
```
bdehdcfg -target default -size 500
```
Das folgende Beispiel zeigt, wie bdehdcfg mit dem Standard Laufwerk verwendet wird, um eine Systempartition zu erstellen (P:) der Standardgröße von 300 MB von nicht zugewiesener Speicherplatz auf dem Laufwerk. Das Tool fordert den Benutzer nicht auf, weitere Eingaben einzugeben, und es werden keine Fehler angezeigt. Nachdem das Systemlaufwerk erstellt wurde, wird der Computer automatisch neu gestartet.
```
bdehdcfg -target unallocated –newdriveletter P: -quiet -restart
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)