---
title: Definieren von Dateigruppen für die Prüfung
description: In diesem Artikel wird beschrieben, wie Sie Dateigruppen definieren, um einen Namespace für den Datei Bildschirm, die Datei Bildschirm Ausnahme oder Dateien nach Dateigruppen-Speicher Berichten zu erstellen.
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: cbcf96a4ab5c6516b87ebde57f6adaf1cf4df17f
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87957477"
---
# <a name="define-file-groups-for-screening"></a>Definieren von Dateigruppen für die Prüfung

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Eine *Datei Gruppe* wird verwendet, um einen Namespace für einen Datei Bildschirm, eine Datei Bildschirm Ausnahme oder einen **Dateien nach Dateigruppe** Speicher Bericht zu definieren. Sie besteht aus einem Satz von Dateinamen Mustern, die nach folgendem gruppiert werden:

-   **Einzuschließende Dateien**: Dateien, die in der Gruppe enthalten sind.
-   Auszuschließende **Dateien**: Dateien, die nicht in die Gruppe gehören.

> [!Note]
> Der Vorteil ist, dass Sie beim Bearbeiten der Eigenschaften von Datei Bildschirmen, Datei Bildschirm Ausnahmen, Datei Bildschirm Vorlagen und **Dateien nach Dateigruppe** Berichten Dateigruppen erstellen und bearbeiten können. Dateigruppen Änderungen, die Sie aus diesen Eigenschaften Blättern vornehmen, sind nicht auf das aktuelle Element beschränkt, an dem Sie arbeiten.

## <a name="to-create-a-file-group"></a>So erstellen Sie eine Datei Gruppe

1.  Klicken Sie unter **Datei-Überprüfungs Verwaltung**auf den Knoten **Dateigruppen** .

2.  Klicken Sie im **Aktions** Bereich auf **Datei Gruppe erstellen**. Dadurch wird das Dialogfeld **Dateigruppen Eigenschaften erstellen** geöffnet.

    (Alternativ können Sie, während Sie die Eigenschaften eines Datei Bildschirms, Datei Bildschirm Ausnahme, Datei Bildschirm Vorlage oder **Dateien nach Dateigruppe** Bericht bearbeiten, unter **Dateigruppen beibehalten**auf **Erstellen**klicken.)

3.  Geben Sie im Dialogfeld **Eigenschaften von Datei Gruppe erstellen** einen Namen für die Datei Gruppe ein.

4.  Fügen Sie Dateien zum Einschließen von Dateien und auszuschließende Dateien hinzu:

    -   Geben Sie für jeden Satz von Dateien, die Sie in die Datei Gruppe einschließen möchten, im Feld **einzuschließende Dateien** ein Dateinamen Muster ein, und klicken Sie dann auf **Hinzufügen**.
    -   Geben Sie für jeden Satz von Dateien, die Sie aus der Datei Gruppe ausschließen möchten, im Feld auszuschließende **Dateien** ein Dateinamen Muster ein, und klicken Sie dann auf **Hinzufügen**.
        Beachten Sie, dass standardmäßige Platzhalter Regeln angewendet werden, z ** \* . b. wählt exe** alle ausführbaren Dateien aus.

5.  Klicken Sie auf **OK**.

## <a name="additional-references"></a>Weitere Verweise

-   [Datei Prüfungsverwaltung](file-screening-management.md)
-   [Erstellen einer Dateiprüfung](create-file-screen.md)
-   [Erstellen einer Dateiprüfungsausnahme](create-file-screen-exception.md)
-   [Erstellen einer Dateiprüfungsvorlage](create-file-screen-template.md)
-   [Speicherberichtmanagement](storage-reports-management.md)


