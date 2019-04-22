---
title: Ändern Sie einen bestimmten Laufwerkbuchstaben
description: So ändern, oder weisen einen Laufwerkbuchstaben in Windows, indem Sie mit der Datenträgerverwaltung.
ms.date: 10/24/2018
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 5f25d49ac399633c048b0c8581551d862145ca76
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812161"
---
# <a name="change-a-drive-letter"></a>Ändern Sie einen bestimmten Laufwerkbuchstaben

> **Gilt für:** Windows 10, Windows 8.1, Windows 7, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012

Wenn Ihnen nicht den Laufwerkbuchstaben, der auf einem Laufwerk gefällt, oder wenn Sie ein Laufwerk haben, die noch keinen Laufwerkbuchstaben, können Sie Datenträgerverwaltung, um ihn zu ändern.

> [!IMPORTANT]
> Wenn Sie den Laufwerkbuchstaben des Laufwerks ändern, auf dem Windows oder apps installiert sind, können apps ausgeführt, oder suchen das Laufwerk schwierigkeiten. Aus diesem Grund wird empfohlen, dass Sie nicht den Laufwerkbuchstaben des Laufwerks ändern, auf denen Windows oder apps installiert sind.

So ändern Sie den Buchstaben des Laufwerks (stattdessen auf das Laufwerk in eine leere Ordner, damit es als nur einen anderen Ordner angezeigt wird finden Sie unter [weisen Sie einen Pfad des Volumebereitstellungspunkts Ordner auf einem Laufwerk](assign-a-mount-point-folder-path-to-a-drive.md)).

1. Öffnen Sie Datenträgerverwaltung mit Administratorberechtigungen aus. <br>Geben Sie dazu in das Suchfeld auf der Taskleiste **Datenträgerverwaltung**, wählen Sie aus, und halten (oder mit der rechten Maustaste) **Datenträgerverwaltung**, und wählen Sie dann **als Administrator ausführen**  >  **Ja**. Wenn Sie sie als Administrator öffnen können, geben Sie **Computerverwaltung** stattdessen, und navigieren Sie zu **Storage** > **Datenträgerverwaltung**.
1. In der Datenträgerverwaltung mit der Maustaste des Laufwerks für die Sie ändern oder Hinzufügen eines Laufwerksbuchstabens und wählen Sie dann **Ändern von Laufwerkbuchstaben und-Pfade**.<br>
![Datenträgerverwaltung mit der ein Laufwerk](media/change-drive-letter.png)
    > [!TIP]
    > Wenn Sie nicht sehen die **Ändern von Laufwerkbuchstaben und-Pfade** Option oder abgeblendet ist, es ist möglich, das Volume einen Laufwerkbuchstaben zu empfangen, das der Fall sein kann, wenn das Laufwerk nicht zugeordnet ist und muss nicht [Initialisiert](initialize-new-disks.md). Oder vielleicht es ist nicht vorgesehen, zugegriffen werden, dies ist der Fall von EFI-System-Partitionen und Wiederherstellungspartitionen. Wenn Sie bestätigt haben, dass Sie eine formatierte Volumes mit einem Laufwerkbuchstaben, die Sie zugreifen können und immer noch nicht geändert werden, leider in diesem Thema wahrscheinlich Ihnen nicht helfen kann, daher wird empfohlen [Kontaktaufnahme mit Microsoft](https://support.microsoft.com/contactus/) oder den Hersteller Ihrer PC, um weitere Hilfe zu erhalten.

1. Wählen Sie zum Ändern der Buchstabe des Laufwerks **ändern**. Zum Hinzufügen von ein Laufwerkbuchstaben auswählen, wenn das Laufwerk, noch nicht **hinzufügen**.<br>![Das Dialogfeld "Änderung Laufwerkbuchstaben und-Pfade"](media/change-drive-letter2.png)
3. Wählen Sie den neuen Laufwerkbuchstaben, **OK**, und wählen Sie dann **Ja** Wenn Sie gefragt, wie Programme, die abhängig von den Laufwerkbuchstaben möglicherweise nicht richtig ausgeführt.<br>![Das Ändern von Laufwerkbuchstaben oder-Pfad-Dialogfeld anzeigen, Ändern von Laufwerkbuchstaben](media/change-drive-letter3.png)