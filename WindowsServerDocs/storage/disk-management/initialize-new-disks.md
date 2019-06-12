---
title: Initialisieren neuer Datenträger
description: So initialisieren Sie neue Datenträger mit der Datenträgerverwaltung diese Vorbereitung verwendet werden. Enthält auch Links zur Behandlung von Problemen.
ms.date: 06/07/2019
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 7a275c372e1486b26821f797a7663eecbc3e8784
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812429"
---
# <a name="initialize-new-disks"></a>Initialisieren neuer Datenträger

> **Gilt für:** Windows 10, Windows 8.1, Windows 7, WindowsServer (Halbjährlicher Kanal), WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012

Wenn Sie einen neuen Datenträger auf Ihren PC hinzufügen, und es nicht im Datei-Explorer angezeigt, Sie müssen möglicherweise [Hinzufügen eines Laufwerksbuchstabens](change-a-drive-letter.md), oder initialisieren Sie sie vor der Verwendung. Sie können nur einem Laufwerk initialisieren, die noch nicht formatiert ist. Initialisieren eines Datenträgers Löscht alles, was darauf, und bereitet es für die Verwendung von Windows, nach dem können Sie sie formatieren und dann speichern Dateien vor.

> [!WARNING]
> Wenn Ihr Datenträger bereits Dateien, die Sie interessiert verfügt, nicht initialisieren Sie es – verlieren Sie alle Dateien. Stattdessen es wird empfohlen, zur Problembehandlung des Datenträgers angezeigt, wenn Sie die Dateien – lesen können, finden Sie unter [der Status eines Datenträgers ist nicht initialisiert oder der Datenträger fehlt vollständig](troubleshooting-disk-management.md#a-disks-status-is-not-initialized-or-the-disk-is-missing).

## <a name="to-initialize-new-disks"></a>So initialisieren Sie neue Datenträger

So sieht wie einen neuen Datenträger mit der Datenträgerverwaltung initialisiert. Wenn Sie PowerShell lieber, verwenden Sie die [Initialize-Disk](https://docs.microsoft.com/powershell/module/storage/initialize-disk) Cmdlet stattdessen.

1. Öffnen Sie Datenträgerverwaltung mit Administratorberechtigungen aus. 
 
    Geben Sie dazu in das Suchfeld auf der Taskleiste **Datenträgerverwaltung**, wählen Sie aus, und halten (oder mit der rechten Maustaste) **Datenträgerverwaltung**, und wählen Sie dann **als Administrator ausführen**  >  **Ja**. Wenn Sie sie als Administrator öffnen können, geben Sie **Computerverwaltung** stattdessen, und navigieren Sie zu **Storage** > **Datenträgerverwaltung**.
1. In der Datenträgerverwaltung mit der Maustaste des Datenträgers zu initialisieren, und klicken Sie dann auf **Datenträgerinitialisierung** (hier gezeigt). Wenn der Datenträger als aufgeführt wird *Offline*, zuerst mit der rechten Maustaste darauf und wählen **Online**.

     Beachten Sie, dass einige USB-Laufwerke haben keine Möglichkeit, das initialisiert wird, werden sie nur die erste formatiert und ein [Laufwerkbuchstaben](change-a-drive-letter.md).

    ![Datenträgerverwaltung, die einen unformatierten Datenträger anzeigt und im Kontextmenü "Datenträger initialisieren" angezeigt](media/uninitialized-disk.PNG)
2. In der **Datenträgerinitialisierung** Dialogfeld (hier gezeigt), überprüfen, stellen Sie sicher, dass die richtige Datenträger ausgewählt ist, und klicken Sie dann auf **OK** , dem standardpartitionsstil zu akzeptieren. Wenn Sie den Partition Stil ("GPT" oder "MBR") finden Sie unter ändern müssen [zu Partitionstypen - GPT- und MBR](#about-partition-styles---gpt-and-mbr).

     Kurz ändert sich der Datenträgerstatus **Initializing** und wählen Sie dann die **Online** Status. Wenn aus irgendeinem Grund ein Fehler auftritt initialisieren möchten, finden Sie unter [der Status eines Datenträgers ist nicht initialisiert oder der Datenträger fehlt vollständig](troubleshooting-disk-management.md#a-disks-status-is-not-initialized-or-the-disk-is-missing).

    ![Das Dialogfeld "Datenträger initialisieren", mit dem GPT-Partitionsstil ausgewählt](media/initialize-disk.PNG)

## <a name="about-partition-styles---gpt-and-mbr"></a>Informationen zu Partitionstypen - GPT- und MBR

Datenträger können in mehrere Blöcke, die Partitionen aufgeteilt werden. Jede Partition - verfügt selbst wenn Sie nur eine jeweils -, haben Sie einen Partitionstyp - GPT "oder" MBR. Windows verwendet den Partitionsstil zu um verstehen, wie die Daten auf dem Datenträger zuzugreifen.

So faszinierend, wie dies wahrscheinlich nicht, ist das Fazit, dass heutzutage, Sie müssen in der Regel keine Partitionstyp kümmern – Windows automatisch den geeigneten Datenträger-Typ verwendet.

Die meisten PCs verwenden Sie den Datenträgertyp von GUID-Partitionstabelle (GPT) für Festplatten und SSDs. GPT bietet mehr Stabilität und Volumes größer als 2 TB ermöglicht. Der ältere Master Boot Record (MBR)-Datenträgertyp wird von 32-Bit-PCs, ältere PCs und Wechseldatenträger wie z. B. Speicherkarten verwendet.

Um einen Datenträger von MBR zu GPT oder umgekehrt zu konvertieren, müssen Sie zuerst das Löschen aller Volumes vom Datenträger, löschen Alles, was auf dem Datenträger. Weitere Informationen finden Sie unter [ein MBR-Datenträgers in einen GPT-Datenträger konvertieren](change-an-mbr-disk-into-a-gpt-disk.md), oder [einen GPT-Datenträger in einen MBR-Datenträger konvertieren](change-a-gpt-disk-into-an-mbr-disk.md).