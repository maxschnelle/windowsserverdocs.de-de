---
title: Erstellen einer Dateiprüfungsausnahme
description: In diesem Artikel wird beschrieben, wie Sie eine Dateiprüfungsausnahme erstellen
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 6a0fa660db6b03104b585c8ee78a4f20aafe5c88
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403144"
---
# <a name="create-a-file-screen-exception"></a>Erstellen einer Dateiprüfungsausnahme

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Gelegentlich sind Ausnahmen bei der Dateiprüfung notwendig. Wenn Sie beispielsweise Videodateien von einem Dateiserver sperren möchten, jedoch Ihrer Schulungsgruppe das Speichern der Video-Dateien für ihre Lernprogramm erlauben müssen. Um Dateien zuzulassen, die von anderen Dateiprüfungen blockiert werden, erstellen Sie eine *Dateiprüfungsausnahme*.

Eine Dateiprüfungsausnahme ist eine besondere Art von Dateiprüfung, die jede Dateiprüfung außer Kraft setzt, die andernfalls auf den Ordner angewandt werden möchten und alle Unterordner in einem Ausnahmepfad angegebenen außer Kraft setzt. Das heißt, es wird eine Ausnahme für alle Regeln erstellt, die von einem übergeordneten Ordner abgeleitet werden.

> [!Note]
> Sie können keine Dateiprüfungsausnahme für einen übergeordneten Ordner erstellen, in denen diese bereits definiert ist. Sie müssen die Ausnahme einem Unterordner zuordnen oder Änderungen an der vorhandene Dateiprüfung vornehmen.

<br />
Um Dateigruppen zuzuweisen, die bestimmen, welche Dateitypen für die Dateiprüfungsausnahme zugelassen werden sollen.

## <a name="to-create-a-file-screen-exception"></a>So erstellen Sie eine Dateiprüfungsausnahme

1.  Klicken Sie unter **Dateiprüfungsverwaltung** auf den Knoten **Dateiprüfungen**.

2.  Klicken Sie mit der rechten Maustaste auf **Dateiprüfungsausnahme,** und dann auf **Dateiprüfungsausnahme erstellen** (oder wählen Sie **Dateiprüfungsausnahme erstellen** im Bereich **Aktionen** aus). Daraufhin wird das Dialogfeld **Dateiprüfungsausnahme erstellen** geöffnet.

3.  Geben Sie in das Textfeld **Ausnahmepfad** den Pfad ein oder wählen Sie den Pfad aus, auf den die Ausnahme angewendet wird. Die Ausnahme gilt für den ausgewählten Ordner und alle Unterordner.

4.  So geben Sie die Dateien an, die von der Dateiprüfung ausgeschlossen werden sollen:

    -   Wählen Sie unter **Dateigruppen** jede Dateigruppe aus, die von Ihrer Dateiprüfung ausgeschlossen werden sollen. (Um das Kontrollkästchen für die Dateigruppe zu aktivieren, doppelklicken Sie auf die Bezeichnung der Dateigruppe.)
    -   Wenn Sie die Dateitypen anzeigen möchten, die eine Datei Gruppe einschließt und ausschließt, klicken Sie auf die Dateigruppen Bezeichnung, und klicken Sie auf **Bearbeiten**.
    -   Klicken Sie zum Erstellen einer neuen Dateigruppe auf **Erstellen**.

5.  Klicken Sie auf **OK**.

## <a name="see-also"></a>Siehe auch

-   [Datei Prüfungsverwaltung](file-screening-management.md)
-   [Definieren von Dateigruppen für die Prüfung](define-file-groups-for-screening.md)


