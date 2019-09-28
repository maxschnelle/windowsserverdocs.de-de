---
title: Definieren von Dateigruppen für die Prüfung
description: In diesem Artikel wird das Definieren von Dateigruppen beschrieben, um einen Namespace für die Dateiprüfung, Dateiprüfungsausnahme oder Speicherberichte für Dateien nach Dateigruppen festzulegen
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: b56d7b0439e3dc6f1a2e0a1c96f761dbb77cb0a0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394389"
---
# <a name="define-file-groups-for-screening"></a>Definieren von Dateigruppen für die Prüfung

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Eine *Dateigruppe* wird verwendet, um einen Namespace für die Dateiprüfung, Dateiprüfungsausnahme oder Speicherbericht für **Dateien nach Dateigruppen** festzulegen. Sie besteht aus einer Reihe von Dateinamenmustern, die folgendermaßen gruppiert werden:

-   **Einzuschließende Dateien**: Dateien, die der Gruppe angehören
-   **Auszuschließende Dateien**: Dateien, die nicht der Gruppe angehören

> [!Note]
> Sie können der Einfachheit halber Dateigruppen erstellen und bearbeiten, während Sie die Eigenschaften der Dateiprüfung, Dateiprüfungsausnahmen, Dateiprüfungsvorlagen und **Dateien nach Dateigruppe**-Berichte ändern. Jegliche Dateigruppenänderungen, die Sie von den Eigenschaftenseiten vornehmen, sind nicht auf das aktuelle Element beschränkt, das Sie bearbeiten.

## <a name="to-create-a-file-group"></a>So erstellen Sie eine Dateigruppe

1.  Klicken Sie unter **Dateiprüfungsverwaltung** auf den Knoten **Dateigruppen**.

2.  Klicken Sie im Bereich **Aktionen** auf **Dateigruppe erstellen**. Daraufhin wird das Dialogfeld **Dateigruppeneigenschaften erstellen** geöffnet.

    (Alternative können Sie während Sie unter **Dateigruppen beibehalten** auf **Erstellen** klicken, um die Eigenschaften der Dateiprüfung, Dateiprüfungsausnahmen, Dateiprüfungsvorlagen und **Dateien nach Dateigruppe**-Berichte zu ändern.)

3.  Geben Sie im Dialogfeld **Dateigruppeneigenschaften erstellen** einen Namen für die neue Dateigruppe ein.

4.  Bestimmen Sie die einzuschließenden und die auszuschließenden Dateien:

    -   Geben Sie für jede Gruppe von Dateien, die Sie in die Dateigruppe einfügen möchten, ein Dateinamenmuster in das Feld **Einzuschließende Dateien** ein und klicken Sie dann auf **Hinzufügen**.
    -   Geben Sie für jede Gruppe von Dateien, die Sie nicht in die Dateigruppe einfügen möchten, ein Dateinamenmuster in das Feld **Auszuschließende Dateien** ein und klicken Sie dann auf **Hinzufügen**.
        Beachten Sie, dass standardmäßige Platzhalter Regeln angewendet werden, z. b. **@no__t -1. exe** alle ausführbaren Dateien auswählt.

5.  Klicken Sie auf **OK**.

## <a name="see-also"></a>Siehe auch

-   [Datei Prüfungsverwaltung](file-screening-management.md)
-   [Erstellen einer Dateiprüfung](create-file-screen.md)
-   [Erstellen einer Dateiprüfungsausnahme](create-file-screen-exception.md)
-   [Erstellen einer Dateiprüfungsvorlage](create-file-screen-template.md)
-   [Speicherberichtmanagement](storage-reports-management.md)


