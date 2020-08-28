---
title: bdehdcfg
description: Referenz Artikel für den Befehl "bdehdcfg", der eine Festplatte mit den für BitLocker-Laufwerkverschlüsselung erforderlichen Partitionen vorbereitet.
ms.topic: reference
ms.assetid: 4c92cd74-188e-4fec-b7c4-fe4e8903e032
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ea7806fc75d01e3b261296ff6fd462473ca5683b
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89031458"
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

## <a name="syntax"></a>Syntax

```
bdehdcfg [–driveinfo <drive_letter>] [-target {default|unallocated|<drive_letter> shrink|<drive_letter> merge}] [–newdriveletter] [–size <size_in_mb>] [-quiet]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- |----------- |
| [bdehdcfg: DriveInfo](bdehdcfg-driveinfo.md) | Zeigt den Laufwerk Buchstaben, die Gesamtgröße, den maximalen freien Speicherplatz und die Partitions Merkmale der Partitionen auf dem angegebenen Laufwerk an. Nur gültige Partitionen sind aufgeführt. Verfügbarer Speicher ist nicht aufgeführt, wenn bereits vier primäre oder erweiterte Partitionen vorhanden sind. |
| [bdehdcfg: Ziel](bdehdcfg-target.md) | Definiert, welcher Teil eines Laufwerks als Systemlaufwerk verwendet werden soll, und macht den Teil aktiv. |
| [bdehdcfg: newdriveletter](bdehdcfg-newdriveletter.md) | Weist dem Teil eines Laufwerks, das als Systemlaufwerk verwendet wird, einen neuen Laufwerk Buchstaben zu. |
| [bdehdcfg: Größe](bdehdcfg-size.md) | Bestimmt die Größe der Systempartition beim Erstellen eines neuen System Laufwerks. |
| [bdehdcfg: Quiet](bdehdcfg-quiet.md) | Verhindert die Anzeige aller Aktionen und Fehler in der Befehlszeilenschnittstelle und leitet bdehdcfg zur Verwendung der ja-Antwort auf alle Ja/Nein-Eingabe Aufforderungen, die während der nachfolgenden Laufwerks Vorbereitung auftreten können. |
| [bdehdcfg: neu starten](bdehdcfg-restart.md) | Der Computer wird nach Abschluss der Laufwerks Vorbereitung an den Neustart umgeleitet. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
