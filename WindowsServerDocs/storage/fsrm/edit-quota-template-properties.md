---
title: Bearbeiten von Kontingentvorlageneigenschaften
description: Dieser Artikel beschreibt, wie Kontingentvorlageneigenschaften bearbeitet werden, um die Änderungen an Kontingenten zu erweitern, die mit der ursprünglichen Kontingentvorlage erstellt wurden
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 37719656e107869b97045af98c1a63744e4f6b38
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403029"
---
# <a name="edit-quota-template-properties"></a>Bearbeiten von Kontingentvorlageneigenschaften

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Wenn Sie eine Kontingentvorlage ändern, haben Sie die Möglichkeit, diese Änderungen auf Kontingente anzuwenden, die mit der ursprünglichen Kontingentvorlage erstellt wurden. Sie haben die Möglichkeit, nur die Kontingente zu ändern, die der ursprünglichen Vorlage entsprechen oder alle Kontingente zu ändern, die von der ursprünglichen Vorlage abgeleitet sind, unabhängig von den Änderungen, die Sie an den Kontingenten vorgenommen haben, seit sie erstellt wurden. Dieses Feature vereinfacht die Aktualisierung der Eigenschaften der Kontingente, da alle Änderungen an einem zentralen Ort ausgeführt werden können.

> [!Note]
> Wenn Sie die Änderungen auf alle Kontingente anwenden möchten, die von der ursprünglichen Vorlage abgeleitet wurden, überschreiben Sie alle benutzerdefinierten Kontingente, die Sie erstellt haben.

## <a name="to-edit-quota-template-properties"></a>So bearbeiten Sie Kontingentvorlageneigenschaften

1.  Wählen Sie im Dialogfeld **Kontingentvorlagen** die zu ändernde Vorlage aus.

2.  Klicken Sie mit der rechten Maustaste auf die Kontingentvorlage und klicken Sie dann auf **Vorlageneigenschaften bearbeiten** (oder wählen Sie im Bereich **Aktionen** unter **Ausgewählte Kontingentvorlagen** die Option **Kontingentvorlagen bearbeiten** aus). Das Dialogfeld **Kontingentvorlageneigenschaften** wird geöffnet.

3.  Führen Sie alle notwendigen Änderungen aus. Die Einstellungs- und Benachrichtigungsoptionen sind mit denen identisch, die Sie einstellen können, wenn Sie eine Kontingentvorlage erstellen. Optional können Sie die Eigenschaften einer anderen Vorlage kopieren und sie für diese ändern.

4.  Wenn Sie mit der Bearbeitung der Vorlageneigenschaften fertig sind, klicken Sie auf **OK**. Das Dialogfeld **Aus Vorlage abgeleitete Kontingente aktualisieren** wird geöffnet.

5.  Wählen Sie den Aktualisierungstyp aus, den Sie anwenden möchten:

    -   Wenn Sie Kontingente haben, die seit der Erstellung mit der ursprünglichen Vorlage geändert wurden und Sie diese nicht ändern möchten, wählen Sie **Vorlage nur auf abgeleitete Kontingente anwenden, die mit der Originalvorlage übereinstimmen** aus. Diese Option aktualisiert nur die Kontingente, die seit der Erstellung mit den ursprünglichen Vorlage nicht bearbeitet wurden.
    -   Wenn Sie alle vorhandenen Kontingente ändern möchten, die mit der ursprünglichen Vorlage erstellt wurden, wählen Sie **Vorlage auf alle abgeleiteten Kontingente anwenden** aus.
    -   Wenn Sie die vorhandenen Kontingente unverändert beibehalten möchten, wählen Sie **Vorlage nicht auf abgeleitete Kontingente anwenden** aus.

6.  Klicken Sie auf **OK**.

## <a name="see-also"></a>Siehe auch

-   [Kontingentverwaltung](quota-management.md)
-   [Erstellen einer Kontingent Vorlage](create-quota-template.md)


