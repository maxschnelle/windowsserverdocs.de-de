---
title: Bearbeiten der Eigenschaften des automatisch zugewiesenen Kontingents
description: In diesem Artikel wird beschrieben, wie Sie die Eigenschaften des automatischen Anwendungs Kontingents
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 558f6b094e97a6196177e728c238f5bb7a38e7a1
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87957447"
---
# <a name="edit-auto-apply-quota-properties"></a>Bearbeiten der Eigenschaften des automatisch zugewiesenen Kontingents

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Wenn Sie Änderungen an einem automatischen Apply-Kontingent vornehmen, haben Sie die Möglichkeit, diese Änderungen im Pfad zum automatischen Anwenden von Kontingenten auf vorhandene Kontingente auszuweiten. Sie können auswählen, ob Sie nur die Kontingente ändern möchten, die weiterhin mit dem ursprünglichen Kontingent für automatische Anwendungs Kontingente oder mit allen Kontingenten für das automatische Anwenden des Kontingents identisch sind, unabhängig von Änderungen, die seit der Erstellung an den Kontingenten vorgenommen wurden. Diese Funktion vereinfacht das Aktualisieren der Eigenschaften von Kontingenten, die von einem automatischen Apply-Kontingent abgeleitet wurden, indem ein zentraler Punkt bereitgestellt wird, an dem Sie alle Änderungen vornehmen können.

> [!Note]
> Wenn Sie die Änderungen auf alle Kontingente im Pfad zum automatischen Anwenden des Kontingents anwenden, überschreiben Sie alle benutzerdefinierten Kontingent Eigenschaften, die Sie erstellt haben.

## <a name="to-edit-an-auto-apply-quota"></a>So bearbeiten Sie ein automatisches Apply-Kontingent

1.  Wählen Sie in **Kontingente**das automatisch anzuwendende Kontingent aus, das Sie ändern möchten. Sie können die Kontingente filtern, um nur automatische Apply-Kontingente anzuzeigen.

2.  Klicken Sie mit der rechten Maustaste auf den Kontingent Eintrag, und klicken Sie dann auf **Kontingent Eigenschaften bearbeiten** (oder klicken Sie im **Aktions** Bereich unter **Ausgewählte Kontingente** auf **Kontingent Eigenschaften bearbeiten**). Dadurch wird das Dialogfeld " **Kontingent automatisch anwenden** " geöffnet.

3.  Wählen Sie unter **Eigenschaften von dieser Kontingent Vorlage ableiten**die Kontingent Vorlage aus, die Sie anwenden möchten. Sie können die Eigenschaften jeder Kontingent Vorlage im Listenfeld Zusammenfassung überprüfen.

4.  Klicken Sie auf **OK**. Dadurch wird das Dialogfeld **Kontingente aktualisieren, das von der Quote automatisch anwenden abgeleitet** wird geöffnet.

5.  Wählen Sie den Typ des Updates aus, das Sie anwenden möchten:

    -   Wenn Sie über Kontingente verfügen, die seit der automatischen Generierung geändert wurden, und Sie diese nicht ändern möchten, wählen Sie **die Option Automatisches Anwenden von Kontingenten nur auf abgeleitete Kontingente anwenden, die dem ursprünglichen automatischen Anwendungs Kontingent entsprechen**. Mit dieser Option werden nur die Kontingente im Pfad zum automatischen Anwenden von Kontingenten aktualisiert, die seit der automatischen Generierung nicht bearbeitet wurden.
    -   Wenn Sie alle vorhandenen Kontingente im Pfad Kontingent automatisch anwenden ändern möchten, wählen Sie die Option **Automatisches Anwenden von Kontingenten auf alle abgeleiteten Kontingente anwenden**aus.
    -   Wenn Sie die vorhandenen Kontingente unverändert halten möchten, aber das geänderte automatisch geltende Kontingent für neue Unterordner im Pfad Kontingent automatisch anwenden aktivieren möchten, wählen Sie **nicht automatisch auf abgeleitete Kontingente anwenden**aus.

6.  Klicken Sie auf **OK**.

## <a name="additional-references"></a>Weitere Verweise

-   [Kontingentverwaltung](quota-management.md)
-   [Erstellen eines automatisch zugewiesenen Kontingents](create-auto-apply-quota.md)


