---
title: Zurückkonvertieren eines dynamischen Datenträgers in eine Basisfestplatte
description: Hier erfährst du, wie du einen dynamischen Datenträger in eine Basisfestplatte zurückkonvertierst.
ms.date: 12/18/2019
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 8ad14225592d627b6ff88b9e2286b686aa549392
ms.sourcegitcommit: bfe9c5f7141f4f2343a4edf432856f07db1410aa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75351942"
---
# <a name="change-a-dynamic-disk-back-to-a-basic-disk"></a>Zurückkonvertieren eines dynamischen Datenträgers in eine Basisfestplatte

> **Gilt für:** Windows 10, Windows 8.1, Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema erfährst du, wie du alle Daten auf einem dynamischen Datenträger löschst und ihn in eine Basisfestplatte zurückkonvertierst. Dynamische Datenträger sind in Windows veraltet und sollten nicht mehr verwendet werden. Verwende stattdessen Basisfestplatten oder die neuere [Speicherplätze](https://support.microsoft.com/help/12438/windows-10-storage-spaces)-Technologie, wenn du Festplatten in größeren Volumes zusammenlegen möchtest. Wenn du das Windows-Startvolume spiegeln möchtest, empfiehlt sich ggf. die Verwendung eines Hardware-RAID-Controllers, wie er beispielsweise auf vielen Hauptplatinen zu finden ist.

> [!WARNING]
> Um einen dynamischen Datenträger wieder in eine Basisfestplatte zu konvertieren, musst du alle Volumes von dem Datenträger löschen. Dabei werden alle Daten auf dem Datenträger endgültig gelöscht. Sichere daher zuvor alle Daten, die du noch benötigst.

## <a name="to-change-a-dynamic-disk-back-to-a-basic-disk-by-using-disk-management"></a>So konvertierst du einen dynamischen Datenträger mithilfe der Datenträgerverwaltung wieder in eine Basisfestplatte

1.  Sichere alle Volumes auf dem Datenträger, den du von einem dynamischen Datenträger in eine Basisfestplatte konvertieren möchtest.

2. Öffne die Datenträgerverwaltung mit Administratorberechtigungen.

   Gib dazu einfach **Computerverwaltung** in das Suchfeld auf der Taskleiste ein, halte **Computerverwaltung** gedrückt (oder klicke mit der rechten Maustaste darauf), und wähle anschließend **Als Administrator ausführen** > **Ja** aus. Nachdem die Computerverwaltung geöffnet wurde, wechsle zu **Speicher** > **Datenträgerverwaltung**.

2.  Halte in der Datenträgerverwaltung jedes Volume des dynamischen Datenträgers, den du in eine Basisfestplatte konvertieren möchtest, gedrückt (oder klicke mit der rechten Maustaste darauf). Klicke anschließend auf **Volume löschen**.

3.  Nachdem alle Volumes auf dem Datenträger gelöscht wurden, klicke mit der rechten Maustaste auf den Datenträger, und klicke anschließend auf **In einen Basisdatenträger konvertieren**.

## <a name="to-change-a-dynamic-disk-back-to-a-basic-disk-by-using-a-command-line"></a>So konvertierst du einen dynamischen Datenträger über eine Befehlszeile wieder in eine Basisfestplatte

1.  Sichere alle Volumes auf dem Datenträger, den du von einem dynamischen Datenträger in eine Basisfestplatte konvertieren möchtest.

2.  Öffnen Sie eine Eingabeaufforderung, und geben Sie `diskpart` ein.

3.  Gib an der Eingabeaufforderung **DISKPART** Folgendes ein: `list disk`. Notiere die Nummer des Datenträgers, den du in eine Basisfestplatte konvertieren möchtest.

4.  Gib an der Eingabeaufforderung **DISKPART** Folgendes ein: `select disk <disknumber>`.

5.  Gib an der Eingabeaufforderung **DISKPART** Folgendes ein: `detail disk`.

6.  Gib für jedes Volume auf dem Datenträger an der Eingabeaufforderung **DISKPART** zuerst `select volume= <volumenumber>` und dann `delete volume` ein.

7.  Gib an der Eingabeaufforderung **DISKPART** den Befehl `select disk <disknumber>` ein, und gib dabei die Nummer des Datenträgers an, den du in eine Basisfestplatte konvertieren möchtest.

8.  Gib an der Eingabeaufforderung **DISKPART** Folgendes ein: `convert basic`.

| Value  | Beschreibung |
| --- | --- |
| **list disk**                         | Zeigt eine Liste der Festplatten und ihre Informationen an, etwa ihre Größe, den verfügbaren freien Speicherplatz, ob es sich um eine Basisfestplatte oder einen dynamischen Datenträger handelt und ob der Datenträger den MBR- oder den GPT-Partitionsstil verwendet. Der mit einem Sternchen (*) gekennzeichnete Datenträger hat den Fokus. |
| **select disk** <em>disknumber</em>   | Wählt den angegebenen Datenträger aus und weist ihm den Fokus zu. (<em>disknumber</em> ist die Nummer des Datenträgers.)  |
| **detail disk** <em>disknumber</em>   | Zeigt die Eigenschaften des ausgewählten Datenträgers und der Volumes auf dem Datenträger an.  |
| **select volume** <em>disknumber</em> | Wählt das angegebene Volume aus und weist ihm den Fokus zu. (<em>disknumber</em> ist die Nummer des Volumes.) Ohne Volumeangabe führt der Befehl **select** die aktuellen Volumes mit Fokus auf. Das Volume kann anhand von Nummer, Laufwerkbuchstabe oder Bereitstellungspunktpfad angegeben werden. Wenn bei einer Basisfestplatte ein Volume ausgewählt wird, erhält die entsprechende Partition den Fokus. |
| **delete volume**                     | Löscht das ausgewählte Volume. Systemvolume, Startvolume und Volumes, die die aktive Auslagerungsdatei oder das Absturzabbild (Speicherabbild) enthalten, können nicht gelöscht werden. |
| **convert basic** | Konvertiert einen leeren dynamischen Datenträger in eine Basisfestplatte.  |

## <a name="additional-considerations"></a>Weitere Überlegungen

-   Der Datenträger, der in eine Basisfestplatte zurückkonvertiert werden soll, darf keine Volumes oder Daten enthalten. Wenn du deine Daten behalten möchtest, musst du sie sichern oder auf ein anderes Volume verschieben, bevor du den Datenträger in eine Basisfestplatte konvertierst.
-   Nachdem du einen dynamischen Datenträger wieder in eine Basisfestplatte konvertiert hast, kannst du darauf nur Partitionen und logische Laufwerke erstellen.

## <a name="see-also"></a>Siehe auch

-   [Command-line syntax notation](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx) (Notation der Befehlszeilensyntax)