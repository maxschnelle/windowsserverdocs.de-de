---
title: Initialisieren neuer Datenträger
description: Hier erfährst du, wie du neue Datenträger mit der Datenträgerverwaltung initialisierst und damit für die Verwendung vorbereitest. Darüber hinaus findest du hier Links zur Problembehandlung.
ms.date: 12/20/2019
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: c2cb88d5b30be28a8ab7709e3a3908ce82ae8408
ms.sourcegitcommit: bfe9c5f7141f4f2343a4edf432856f07db1410aa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75352360"
---
# <a name="initialize-new-disks"></a>Initialisieren neuer Datenträger

> **Gilt für:** Windows 10, Windows 8.1, Windows 7, Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Wenn du einen ganz neuen Datenträger zu deinem PC hinzufügst und er nicht im Datei-Explorer angezeigt wird, musst du unter Umständen einen [Laufwerkbuchstaben hinzufügen](change-a-drive-letter.md) oder den Datenträger vor der Verwendung initialisieren. Du kannst nur ein noch nicht formatiertes Laufwerk initialisieren. Beim Initialisieren eines Datenträgers werden alle darauf gespeicherten Daten gelöscht, und der Datenträger wird für die Verwendung durch Windows vorbereitet. Anschließend kannst du ihn formatieren und Dateien darauf speichern.

> [!WARNING]
> Enthält dein Datenträger bereits wichtige Dateien, solltest du ihn nicht initialisieren. Andernfalls gehen alle Dateien verloren. Stattdessen wird die Ausführung der Problembehandlung für den Datenträger empfohlen, um zu überprüfen, ob die Dateien gelesen werden können. Informationen dazu findest du unter [Ein Datenträger hat den Status „Nicht initialisiert“, oder der Datenträger fehlt](troubleshooting-disk-management.md#disks-that-are-missing-or-not-initialized-plus-general-troubleshooting-steps).

## <a name="to-initialize-new-disks"></a>So initialisierst du neue Datenträger

Hier wird erläutert, wie du einen neuen Datenträger mit der Datenträgerverwaltung initialisierst. Wenn du PowerShell bevorzugst, verwende stattdessen das Cmdlet [initialize-disk](https://docs.microsoft.com/powershell/module/storage/initialize-disk).

1. Öffne die Datenträgerverwaltung mit Administratorberechtigungen.
 
    Gib dazu ins Suchfeld auf der Taskleiste **Datenträgerverwaltung** ein, halte **Datenträgerverwaltung** gedrückt (oder klicke mit der rechten Maustaste darauf), und wähle anschließend **Als Administrator ausführen** > **Ja** aus. Falls das Öffnen als Administrator nicht funktioniert, gib stattdessen **Computerverwaltung** ein, und navigiere anschließend zu **Speicher** > **Datenträgerverwaltung**.
1. Klicke in der Datenträgerverwaltung mit der rechten Maustaste auf den zu initialisierenden Datenträger, und klicke dann auf **Datenträgerinitialisierung** (siehe Abbildung unten). Wird der Datenträger als *Offline* angezeigt, klicke zunächst mit der rechten Maustaste darauf, und wähle dann **Online** aus.

     Beachte, dass für einige USB-Laufwerke keine Option zum Initialisieren verfügbar ist. Sie werden einfach formatiert und erhalten einen [Laufwerkbuchstaben](change-a-drive-letter.md).

    ![Datenträgerverwaltung mit einem unformatierten Datenträger und dem Kontextmenü „Datenträger initialisieren“](media/uninitialized-disk.PNG)
2. Vergewissere dich im Dialogfeld **Datenträger initialisieren** (siehe Abbildung unten), dass der richtige Datenträger ausgewählt ist, und klicke dann auf **OK**, um den Standardpartitionsstil zu übernehmen. Informationen zum Ändern des Partitionsstils (GPT oder MBR) findest du unter [Informationen zu Partitionsstilen: GPT und MBR](#about-partition-styles---gpt-and-mbr).

     Der Datenträgerstatus wird kurzzeitig in **Initialisieren** und dann in **Online** geändert. Tritt bei der Initialisierung ein Fehler auf, findest du unter [Ein Datenträger hat den Status „Nicht initialisiert“, oder der Datenträger fehlt.](troubleshooting-disk-management.md#disks-that-are-missing-or-not-initialized-plus-general-troubleshooting-steps) weitere Informationen.

    ![Das Dialogfeld „Datenträger initialisieren“ mit ausgewähltem GPT-Partitionsstil](media/initialize-disk.PNG)

3. Halte den nicht zugeordneten Speicherplatz auf dem Laufwerk gedrückt (oder klicke mit der rechten Maustaste darauf), und wähle dann **Neues einfaches Volume** aus.
4. Wähle **Weiter** aus, gib die Größe des Volumes an (normalerweise wirst du bei der Standardeinstellung bleiben, die das gesamte Laufwerk verwendet), und wähle dann **Weiter** aus.
5. Gib den Laufwerksbuchstaben an, den du dem Volume zuweisen möchtest, und wähle dann **Weiter** aus.
6. Gib das gewünschte Dateisystem an (normalerweise NTFS), wähle **Weiter** und dann **Fertig stellen** aus.

## <a name="about-partition-styles---gpt-and-mbr"></a>Informationen zu Partitionsstilen: GPT und MBR

Datenträger können in mehrere Blöcke, sogenannte Partitionen, unterteilt werden. Auch wenn nur eine Partition vorhanden ist: Für jede Partition muss ein Partitionsstil (GPT oder MBR) festgelegt werden. Windows erkennt anhand des Partitionsstils, wie auf die Daten auf dem Datenträger zugegriffen werden soll.

Letztendlich musst du dir heutzutage in der Regel aber ohnehin keine Gedanken mehr über den Partitionsstil machen, da Windows automatisch den geeigneten Datenträgertyp verwendet.

Die meisten PCs verwenden den Datenträgertyp „GPT“ (GUID Partition Table, GUID-Partitionstabelle) für Festplatten und SSDs. GPT bietet mehr Stabilität und ermöglicht die Verwendung von Volumes mit mehr als 2 TB. Der ältere MBR-Datenträgertyp (Master Boot Record) wird von 32-Bit-PCs, älteren PCs und Wechseldatenträgern wie Speicherkarten verwendet.

Zum Konvertieren eines Datenträgers von MBR in GPT oder umgekehrt musst du zuerst alle Volumes vom Datenträger und damit alle Daten vom Datenträger löschen. Weitere Informationen findest du unter [Konvertieren eines MBR-Datenträgers in einen GPT-Datenträger](change-an-mbr-disk-into-a-gpt-disk.md) bzw. [Konvertieren eines GPT-Datenträgers in einen MBR-Datenträger](change-a-gpt-disk-into-an-mbr-disk.md).