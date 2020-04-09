---
title: bdehdcfg
description: Windows-Befehls Thema für **bdehdcfg**, das eine Festplatte mit den für BitLocker-Laufwerkverschlüsselung erforderlichen Partitionen vorbereitet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4c92cd74-188e-4fec-b7c4-fe4e8903e032
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c9adf8bbfb655e0820fcff6385d3663fc7abbd9a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851003"
---
# <a name="bdehdcfg"></a>bdehdcfg

Bereitet eine Festplatte mit den für BitLocker-Laufwerkverschlüsselung erforderlichen Partitionen vor. Bei den meisten Installationen von Windows 7 muss dieses Tool nicht verwendet werden, da das BitLocker-Setup die Möglichkeit bietet, Laufwerke nach Bedarf vorzubereiten und neu zu partitionieren.

> [!WARNING]
> Es gibt einen bekannten Konflikt mit der Gruppenrichtlinieneinstellung **Schreibzugriff auf Wechseldatenträger verweigern, die nicht durch BitLocker geschützt sind** unter **Computerkonfiguration\Administrative Vorlagen\Windows-Komponenten\BitLocker-Laufwerkverschlüsselung\Festplattenlaufwerke**.
>
>Wenn bdehdcfg auf einem Computer ausgeführt wird, wenn diese Richtlinien Einstellung aktiviert ist, können die folgenden Probleme auftreten:
>
>- Wenn Sie das Laufwerk verkleinern und das Systemlaufwerk erstellen wollten, wird die Laufwerkgröße erfolgreich reduziert und eine sogenannte Raw-Partition erstellt. Die Raw-Partition wird nicht formatiert. Die folgende Fehlermeldung wird angezeigt: das neue aktive Laufwerk kann nicht formatiert werden. Möglicherweise müssen Sie das Laufwerk für BitLocker manuell vorbereiten.
>
>- Wenn Sie nicht zugeordneten Speicherplatz zum Erstellen des Systemlaufwerks verwenden wollten, wird eine sogenannte Raw-Partition erstellt. Die Raw-Partition wird nicht formatiert. Die folgende Fehlermeldung wird angezeigt: das neue aktive Laufwerk kann nicht formatiert werden. Möglicherweise müssen Sie das Laufwerk für BitLocker manuell vorbereiten.
>
>- Wenn Sie versuchen, ein vorhandenes Laufwerk mit dem Systemlaufwerk zusammenzuführen, kann die zum Erstellen des Systemlaufwerks benötigte Startdatei nicht auf das Ziellaufwerk kopiert werden. Es wird die folgende Fehlermeldung angezeigt: Fehler beim Kopieren von Startdateien durch das BitLocker-Setup. Möglicherweise müssen Sie das Laufwerk für BitLocker manuell vorbereiten.
>
>- Wenn diese Richtlinieneinstellung erzwungen wird, kann ein Festplattenlaufwerk nicht neu partitioniert werden, weil es geschützt ist. Wenn Sie ein Upgrade der Computer in ihrer Organisation von einer früheren Version von Windows durchführen und diese Computer mit einer einzelnen Partition konfiguriert waren, sollten Sie die erforderliche BitLocker-Systempartition erstellen, bevor Sie die Richtlinieneinstellung für die Computer übernehmen.

Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
bdehdcfg [–driveinfo <DriveLetter>] [-target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge}] [–newdriveletter] [–size <SizeinMB>] [-quiet]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- |----------- |
| [Bdehdcfg: DriveInfo](bdehdcfg-driveinfo.md) | Zeigt den Laufwerk Buchstaben, die Gesamtgröße, den maximalen freien Speicherplatz und die Partitions Merkmale der Partitionen auf dem angegebenen Laufwerk an. Nur gültige Partitionen sind aufgeführt. Verfügbarer Speicher ist nicht aufgeführt, wenn bereits vier primäre oder erweiterte Partitionen vorhanden sind. |
| [Bdehdcfg: Ziel](bdehdcfg-target.md) | Definiert, welcher Teil eines Laufwerks als Systemlaufwerk verwendet werden soll, und macht den Teil aktiv. |
| [Bdehdcfg: newdriveletter](bdehdcfg-newdriveletter.md) | Weist dem Teil eines Laufwerks, das als Systemlaufwerk verwendet wird, einen neuen Laufwerk Buchstaben zu. |
| [Bdehdcfg: Größe](bdehdcfg-size.md) | Bestimmt die Größe der Systempartition beim Erstellen eines neuen System Laufwerks. |
| [Bdehdcfg: Quiet](bdehdcfg-quiet.md) | Verhindert die Anzeige aller Aktionen und Fehler in der Befehlszeilenschnittstelle und leitet bdehdcfg zur Verwendung der ja-Antwort auf alle Ja/Nein-Eingabe Aufforderungen, die während der nachfolgenden Laufwerks Vorbereitung auftreten können. |
| [Bdehdcfg: neu starten](bdehdcfg-restart.md) | Der Computer wird nach Abschluss der Laufwerks Vorbereitung an den Neustart umgeleitet. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Das folgende Beispiel zeigt bdehdcfg, das mit dem Standard Laufwerk verwendet wird, um eine Systempartition von 500 MB zu erstellen. Da kein Laufwerk Buchstabe angegeben wird, weist die neue Systempartition keinen Laufwerk Buchstaben auf.

```
bdehdcfg -target default -size 500
```

Das folgende Beispiel zeigt, wie bdehdcfg mit dem Standard Laufwerk verwendet wird, um eine Systempartition zu erstellen (P:) der Standardgröße von 300 MB von nicht zugewiesener Speicherplatz auf dem Laufwerk. Das Tool fordert den Benutzer nicht auf, weitere Eingaben einzugeben, und es werden keine Fehler angezeigt. Nachdem das Systemlaufwerk erstellt wurde, wird der Computer automatisch neu gestartet.

```
bdehdcfg -target unallocated –newdriveletter P: -quiet -restart
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)