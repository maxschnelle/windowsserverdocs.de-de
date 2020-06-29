---
title: Erstellen einer Dateiprüfungsausnahme
description: In diesem Artikel wird beschrieben, wie Sie eine Datei Bildschirm Ausnahme erstellen.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: c496151ed1f38cd1f2c604bd227627a586e582c6
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473697"
---
# <a name="create-a-file-screen-exception"></a>Erstellen einer Dateiprüfungsausnahme

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Gelegentlich müssen Sie Ausnahmen für das Überprüfen von Dateien zulassen. Beispielsweise möchten Sie möglicherweise Videodateien von einem Dateiserver blockieren, aber Sie müssen der Trainingsgruppe gestatten, die Videodateien für Ihre computerbasierten Schulungen zu speichern. Wenn Sie zulassen möchten, dass Dateien von anderen Datei Bildschirmen blockiert werden, erstellen Sie eine *Datei Bildschirm Ausnahme*.

Eine Datei Bildschirm Ausnahme ist eine besondere Art von Datei Bildschirm, die alle Datei Prüfungen überschreibt, die andernfalls auf einen Ordner und alle zugehörigen Unterordner in einem bestimmten Ausnahme Pfad angewendet werden. Das heißt, es wird eine Ausnahme für alle Regeln erstellt, die von einem übergeordneten Ordner abgeleitet werden.

> [!Note]
> Es ist nicht möglich, eine Datei Bildschirm Ausnahme für einen übergeordneten Ordner zu erstellen, in dem bereits ein Datei Bildschirm definiert ist. Sie müssen die Ausnahme einem Unterordner zuweisen oder Änderungen am vorhandenen Datei Bildschirm vornehmen.

<br />
Sie weisen Dateigruppen zu, um zu bestimmen, welche Dateitypen in der Datei Bildschirm Ausnahme zulässig sind.

## <a name="to-create-a-file-screen-exception"></a>So erstellen Sie eine Ausnahme für den Datei Bildschirm

1.  Klicken Sie unter **Datei-Überprüfungs Verwaltung**auf den Knoten **Datei Bildschirme** .

2.  Klicken Sie mit der rechten Maustaste auf **Datei Bildschirme**, und klicken Sie auf **Datei Bildschirm Ausnahme erstellen** (oder wählen Sie im Bereich **Aktionen** die Option **Datei Bildschirm Ausnahme erstellen** ) aus. Dadurch wird das Dialogfeld **Datei Bildschirm Ausnahme erstellen** geöffnet.

3.  Geben Sie im Textfeld **Ausnahme Pfad** den Pfad ein, auf den die Ausnahme angewendet werden soll, oder wählen Sie ihn aus. Die Ausnahme gilt für den ausgewählten Ordner und alle zugehörigen Unterordner.

4.  So geben Sie an, welche Dateien aus der Dateiüberprüfung ausgeschlossen werden sollen:

    -   Wählen Sie unter **Dateigruppen**die einzelnen Dateigruppen aus, die Sie aus der Dateiüberprüfung ausschließen möchten. (Doppelklicken Sie auf die Dateigruppen Bezeichnung, um das Kontrollkästchen für die Datei Gruppe auszuwählen.)
    -   Wenn Sie die Dateitypen anzeigen möchten, die eine Datei Gruppe einschließt und ausschließt, klicken Sie auf die Dateigruppen Bezeichnung, und klicken Sie auf **Bearbeiten**.
    -   Klicken Sie zum Erstellen einer neuen Dateigruppe auf **Erstellen**.

5.  Klicken Sie auf **OK**.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Datei Prüfungsverwaltung](file-screening-management.md)
-   [Definieren von Dateigruppen für die Prüfung](define-file-groups-for-screening.md)


