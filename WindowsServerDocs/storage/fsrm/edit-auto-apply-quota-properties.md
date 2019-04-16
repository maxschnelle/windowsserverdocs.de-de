---
title: Bearbeiten der Eigenschaften des automatisch zugewiesenen Kontingents
description: Dieser Artikel beschreibt, wie automatisch zugewiesenes Kontingenteigenschaften bearbeitet werden
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: aa2155268d42293ade925d53da5e29142d13aae4
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="edit-auto-apply-quota-properties"></a>Bearbeiten der Eigenschaften des automatisch zugewiesenen Kontingents

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Wenn Sie Änderungen an einem automatisch zugewiesenen Kontingent vornehmen, haben Sie die Möglichkeit, diese Änderungen auf vorhandene Kontingente des automatisch zugewiesenen Kontingentpfads anzuwenden. Sie haben die Möglichkeit, nur die Kontingente zu ändern, die mit dem ursprünglichen automatisch zugewiesenen Kontingent übereinstimmen oder alle Kontingente des automatisch zugewiesenen Kontingentpfads zu ändern, unabhängig von den Änderungen, die an den Kontingenten vorgenommen wurden, seit sie erstellt wurden. Dieses Feature vereinfacht das Aktualisieren der Eigenschaften von Kontingenten, die von einem automatisch zugewiesenen Kontingent abgeleitet wurden, da alle Updates an einem zentralen Ort ausgeführt werden können.

> [!Note]
> Wenn Sie die Änderungen an allen Kontingente des automatisch zugewiesenen Kontingentpfads vornehmen möchten, überschreiben Sie alle benutzerdefinierten Kontingenteigenschaften, die Sie erstellt haben.

## <a name="to-edit-an-auto-apply-quota"></a>So bearbeiten Sie ein automatisch zugewiesenes Kontingent

1.  Wählen Sie unter **Kontingente** die automatisch zugewiesenen Kontingent aus, die Sie ändern möchten. Sie können die Kontingente filtern, um nur die automatisch zugewiesenen Kontingente anzuzeigen.

2.  Klicken Sie mit der rechten Maustaste auf den Kontingenteintrag und klicken Sie dann auf **Kontingenteigenschaften bearbeiten** (oder wählen Sie im Bereich **Aktionen** unter **Ausgewählte Kontingente** die Option **Kontingenteigenschaften bearbeiten** aus). Das Dialogfeld **Automatisch zugewiesene Kontingente bearbeiten** wird geöffnet.

3.  Wählen Sie unter **Eigenschaften aus dieser Kontingentvorlage ableiten**die Kontingentvorlage aus, die Sie anwenden möchten. Sie können die Eigenschaften jeder Kontingentvorlage im Übersichtslistenfeld überprüfen.

4.  Klicken Sie auf **OK**. Das Dialogfeld **Aus dem automatisch zugewiesenen Kontingent abgeleitete Kontingente aktualisieren** wird geöffnet.

5.  Wählen Sie den Aktualisierungstyp aus, den Sie anwenden möchten:

    -   Wenn Sie Kontingente haben, die seit der automatischen Erstellung geändert wurden und Sie diese nicht ändern möchten, wählen Sie **Zugewiesenes Kontingent nur auf Kontingente anwenden, die mit dem urspr. übereinstimmen** aus. Diese Option aktualisiert nur die Kontingente in den automatisch zugewiesenen Kontingenten, die seit der automatischen Erstellung nicht bearbeitet wurden.
    -   Wenn Sie alle vorhandenen Kontingente im automatisch zugewiesenen Kontingentpfad ändern möchten, wählen Sie **Zugewiesenes Kontingent auf alle abgeleiteten Kontingente anwenden** aus.
    -   Wenn Sie die vorhandenen Kontingente unverändert lassen möchten, jedoch die geänderten automatisch zugewiesenen Kontingente für neue Unterordner des automatisch zugewiesenen Kontingentpfads wirksam machen möchten, wählen Sie **Zugewiesenes Kontingent nicht auf abgeleitete Kontingente anwenden** aus.

6.  Klicken Sie auf **OK**.

## <a name="see-also"></a>Weitere Informationen:

-   [Kontingentverwaltung](quota-management.md)
-   [Erstellen eines automatisch zugewiesenen Kontingents](create-auto-apply-quota.md)


