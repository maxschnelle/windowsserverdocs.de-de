---
title: Verkleinern eines Basisvolumes
description: Dieser Artikel beschreibt das Verkleinern eines Basisvolumes.
ms.date: 06/07/2019
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 9073632a656f512bdb49ebe4eeefd4cd5f4eaadf
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2019
ms.locfileid: "66812528"
---
# <a name="shrink-a-basic-volume"></a>Verkleinern eines Basisvolumes

> **Gilt für:** Windows 10, Windows 8.1, Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Du kannst den von primären Partitionen und logischen Laufwerken verwendeten Speicherplatz verringern, indem du sie auf angrenzenden, zusammenhängenden Speicherplatz auf dem gleichen Datenträger verkleinerst. Wenn du beispielsweise feststellst, dass du eine weitere Partition benötigst, jedoch nicht über weitere Datenträger verfügst, kannst du die vorhandene Partition am Ende des Volumes verkleinern, um neuen, verfügbaren Speicher für eine neue Partition zu erstellen. Der Verkleinerungsvorgang kann durch bestimmte Dateitypen blockiert werden. Weitere Informationen findest du unter [Weitere Überlegungen](#additional-considerations). 

Wenn du eine Partition verkleinerst, werden alle normalen Dateien automatisch auf dem Datenträger verschoben, um den neuen, verfügbaren Speicher zu erstellen. Es ist nicht erforderlich, den Datenträger neu zu formatieren, um die Partition zu verkleinern.

> [!CAUTION]
> Bei einer unformatierten Partition (ohne Dateisystem), die Daten enthält (etwa eine Datenbankdatei), werden die Daten durch das Verkleinern der Partition unter Umständen vernichtet.

## <a name="shrinking-a-basic-volume"></a>Verkleinern eines Basisvolumes

> [!NOTE]
> Du musst mindestens Mitglied der Gruppe **Sicherungsoperatoren** oder **Administratoren** sein, um diese Schritte ausführen zu können.

#### <a name="to-shrink-a-basic-volume-using-the-windows-interface"></a>So verkleinerst du ein Basisvolume über die Windows-Benutzeroberfläche

1.  Klicke in der Datenträgerverwaltung mit der rechten Maustaste auf das Basisvolume, das du verkleinern möchtest.

2.  Klicke auf **Volume verkleinern**.

3.  Befolgen Sie die Anweisungen auf dem Bildschirm.


> [!NOTE]
> Du kannst nur Basisvolumes verkleinern, die entweder kein Dateisystem oder das NTFS-Dateisystem besitzen.

#### <a name="to-shrink-a-basic-volume-using-a-command-line"></a>So verkleinerst du ein Basisvolume mithilfe einer Befehlszeile

1.  Öffnen Sie eine Eingabeaufforderung, und geben Sie `diskpart` ein.

2.  Gib an der Eingabeaufforderung **DISKPART** Folgendes ein: `list volume`. Notiere dir die Nummer des einfachen Volumes, das du verkleinern möchtest.

3.  Gib an der Eingabeaufforderung **DISKPART** Folgendes ein: `select volume <volumenumber>`. Wähle das einfache Volume *volumenumber* aus, das du verkleinern möchtest.

4.  Gib an der Eingabeaufforderung **DISKPART** Folgendes ein: `shrink [desired=<desiredsize>] [minimum=<minimumsize>]`. Verkleinert das ausgewählte Volume nach Möglichkeit auf *desiredsize* (in MB) oder auf *minimumsize*, falls *desiredsize* zu groß ist.

| Wert             | Beschreibung |
| ---               | ----------- |
| **list volume** | Zeigt eine Liste der Basisvolumes und dynamischen Volumes auf allen Datenträgern an. |
| **select volume** | Wählt das angegebene Volume aus und weist ihm den Fokus zu. (<em>volumenumber</em> ist die Nummer des Volumes.) Ohne Volumeangabe führt der Befehl **select** die aktuellen Volumes mit Fokus auf. Das Volume kann anhand von Nummer, Laufwerkbuchstabe oder Bereitstellungspunktpfad angegeben werden. Wenn bei einer Basisfestplatte ein Volume ausgewählt wird, erhält die entsprechende Partition den Fokus. |
| **shrink** | Verkleinert das Volume mit dem Fokus, um verfügbaren Speicher zu erstellen. Es gehen keine Daten verloren. Wenn die Partition nicht verschiebbare Dateien enthält (z. B. die Auslagerungsdatei oder den Schattenkopiespeicherbereich), wird das Volume bis zu dem Punkt verkleinert, an dem sich die Systemdateien befinden. |
| **desired=** <em>desiredsize</em> | Der Speicherplatz in Megabyte, der für die aktuelle Partition freigegeben werden soll. |
| **minimum=** <em>minimumsize</em> | Der minimale Speicherplatz in Megabyte, der für die aktuelle Partition freigegeben werden soll. Ohne Angabe einer gewünschten oder minimalen Größe gibt der Befehl die maximal mögliche Menge an Speicherplatz frei. |

## <a name="additional-considerations"></a>Weitere Aspekte

-   Beim Verkleinern einer Partition können bestimmte Dateien (z. B. die Auslagerungsdatei und der Schattenkopiespeicherbereich) nicht automatisch verschoben werden, und du kannst den zugewiesenen Speicherplatz nur bis zu dem Punkt verkleinern, an dem sich die Systemdateien befinden. Sollte der Verkleinerungsvorgang nicht erfolgreich sein, suche im Anwendungsprotokoll nach dem Ereignis 259, das die nicht verschiebbare Datei identifiziert. Falls du die Cluster kennst, die der Datei zugeordnet sind, durch die der Verkleinerungsvorgang verhindert wird, kannst du an der Eingabeaufforderung auch den Befehl **fsutil** ausführen. (Gib **fsutil volume querycluster /?** ein, um die Syntax anzuzeigen.) Bei Angabe des Parameters **querycluster** identifiziert der Ausgabebefehl die nicht verschiebbare Datei, die den Verkleinerungsvorgang verhindert.
Manchmal lässt sich die Datei vorübergehend verschieben. Wenn du beispielsweise die Partition weiter verkleinern musst, kannst du die Auslagerungsdatei oder die gespeicherten Schattenkopien über die Systemsteuerung auf einen anderen Datenträger verschieben, die gespeicherten Schattenkopien löschen, das Volume verkleinern und die Auslagerungsdatei wieder auf den Datenträger verschieben. Wenn von der dynamischen erneuten Zuordnung eine zu hohe Anzahl fehlerhafter Cluster erkannt wird, kann die Partition nicht verkleinert werden. In diesem Fall empfiehlt es sich, die Daten zu verschieben und den Datenträger auszutauschen.

-  Übertrage die Daten nicht mit einer Kopie auf Blockebene. Dadurch wird auch die Tabelle mit den beschädigten Sektoren kopiert, und der neue Datenträger behandelt die gleichen Sektoren als fehlerhaft, obwohl sie nicht fehlerhaft sind.

-   Du kannst primäre Partitionen und logische Laufwerke auf unformatierten Partitionen (ohne Dateisystem) oder auf Partitionen mit NTFS-Dateisystem verkleinern.

## <a name="see-also"></a>Weitere Informationen

-   [Verwalten von Basisvolumes](manage-basic-volumes.md)