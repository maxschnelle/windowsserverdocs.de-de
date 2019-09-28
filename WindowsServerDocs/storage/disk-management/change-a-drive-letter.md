---
title: Ändern eines Laufwerkbuchstabens
description: Hier erfährst du, wie du unter Windows mithilfe der Datenträgerverwaltung einen Laufwerkbuchstaben änderst oder zuweist.
ms.date: 10/24/2018
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 3e18092a71e12cadb86052204738fafc8a149ff4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386020"
---
# <a name="change-a-drive-letter"></a>Ändern eines Laufwerkbuchstabens

> **Gilt für:** Windows 10, Windows 8.1, Windows 7, Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Wenn du einem Laufwerk einen anderen Laufwerkbuchstaben zuweisen möchtest oder ein Laufwerk ohne Laufwerkbuchstaben besitzt, kannst du den Laufwerkbuchstaben mithilfe der Datenträgerverwaltung ändern oder zuweisen.

> [!IMPORTANT]
> Falls du den Laufwerkbuchstaben eines Laufwerks mit Windows- oder App-Installation änderst, können Apps unter Umständen nicht richtig ausgeführt werden oder das Laufwerk möglicherweise nicht finden. Aus diesem Grund wird empfohlen, den Laufwerkbuchstaben des Laufwerks nicht zu ändern, auf dem Windows oder Apps installiert ist bzw. sind.

Nachfolgend wird erläutert, wie du den Laufwerkbuchstaben änderst. (Wenn du stattdessen das Laufwerk in einen leeren Ordner einbinden möchtest, sodass es einfach als weiterer Ordner angezeigt wird, lies die Informationen unter [Zuweisen eines Ordnerpfads mit Bereitstellungspunkt zu einem Laufwerk](assign-a-mount-point-folder-path-to-a-drive.md).)

1. Öffne die Datenträgerverwaltung mit Administratorberechtigungen. 
    Gib dazu ins Suchfeld auf der Taskleiste **Datenträgerverwaltung** ein, halte **Datenträgerverwaltung** gedrückt (oder klicke mit der rechten Maustaste darauf), und wähle anschließend **Als Administrator ausführen** > **Ja** aus. Falls das Öffnen als Administrator nicht funktioniert, gib stattdessen **Computerverwaltung** ein, und navigiere anschließend zu **Speicher** > **Datenträgerverwaltung**.
1. Klicke in der Datenträgerverwaltung mit der rechten Maustaste auf das Laufwerk, für das du den Laufwerkbuchstaben ändern oder hinzufügen möchtest, und wähle dann **Laufwerkbuchstaben und -pfade ändern...** aus.

    ![Datenträgerverwaltung mit angezeigtem Laufwerk](media/change-drive-letter.png)
    > [!TIP]
    > Wird die Option **Laufwerkbuchstaben und -pfade ändern...** nicht oder abgeblendet angezeigt, kann dem Volume möglicherweise kein Laufwerkbuchstabe zugewiesen werden. Dies ist der Fall, wenn das Laufwerk nicht zugeordnet ist und [initialisiert](initialize-new-disks.md) werden muss. Vielleicht soll der Zugriff auch gar nicht möglich sein – etwa im Fall von EFI-Systempartitionen oder Wiederherstellungspartitionen. Wenn du sichergestellt hast, dass du ein formatiertes Volume mit einem Laufwerkbuchstaben besitzt, auf das du zugreifen, dessen Laufwerkbuchstaben du aber nicht ändern kannst, findest du in diesem Thema wahrscheinlich keine hilfreichen Informationen. Wende dich in diesem Fall an [Microsoft](https://support.microsoft.com/contactus/) oder den Hersteller deines PCs, um weitere Unterstützung zu erhalten.

1. Wähle zum Ändern des Laufwerkbuchstaben die Option **Ändern** aus. Wähle **Hinzufügen** aus, um einen Laufwerkbuchstaben zuzuweisen, sofern das Laufwerk noch keinen besitzt.

    ![Dialogfeld „Laufwerkbuchstaben und -pfade ändern...“](media/change-drive-letter2.png)
1. Wähle den neuen Laufwerkbuchstaben und dann **OK** aus. Wenn die Meldung angezeigt wird, dass Programme, die den Laufwerkbuchstaben verwenden, möglicherweise nicht ordnungsgemäß ausgeführt werden, wähle **Ja** aus.

    ![Dialogfeld „Laufwerkbuchstaben und -pfade ändern...“: Ändern des Laufwerkbuchstabens](media/change-drive-letter3.png)