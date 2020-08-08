---
title: Bearbeiten von Kontingentvorlageneigenschaften
description: In diesem Artikel wird beschrieben, wie Sie Kontingent Vorlagen Eigenschaften bearbeiten, um Änderungen an Kontingenten, die aus der ursprünglichen Kontingent Vorlage erstellt wurden
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 4e8a112f26f2b0ffdf8047063411dbb5539f4eb1
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87961414"
---
# <a name="edit-quota-template-properties"></a>Bearbeiten von Kontingentvorlageneigenschaften

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Wenn Sie Änderungen an einer Kontingent Vorlage vornehmen, haben Sie die Möglichkeit, diese Änderungen auf Kontingente auszudehnen, die aus der ursprünglichen Kontingent Vorlage erstellt wurden. Sie können auswählen, ob Sie nur die Kontingente ändern möchten, die noch mit der ursprünglichen Vorlage oder allen Kontingenten, die von der ursprünglichen Vorlage abgeleitet wurden, identisch sind, unabhängig von Änderungen, die seit der Erstellung an den Kontingenten vorgenommen wurden. Diese Funktion vereinfacht die Aktualisierung der Eigenschaften ihrer Kontingente, indem ein zentraler Punkt bereitgestellt wird, an dem alle Änderungen vorgenommen werden können.

> [!Note]
> Wenn Sie die Änderungen auf alle Kontingente anwenden, die von der ursprünglichen Vorlage abgeleitet wurden, überschreiben Sie alle benutzerdefinierten Kontingent Eigenschaften, die Sie erstellt haben.

## <a name="to-edit-quota-template-properties"></a>So bearbeiten Sie Kontingent Vorlagen Eigenschaften

1.  Wählen Sie in **Kontingent Vorlagen**die Vorlage aus, die Sie ändern möchten.

2.  Klicken Sie mit der rechten Maustaste auf die Kontingent Vorlage, und klicken Sie dann auf **Vorlagen Eigenschaften bearbeiten** (oder wählen Sie im Bereich **Aktionen** unter **ausgewählte Kontingent Vorlagen** die Option **Vorlagen Eigenschaften bearbeiten**aus). Dadurch wird das Dialogfeld **Eigenschaften der Kontingent Vorlage** geöffnet.

3.  Führen Sie alle erforderlichen Änderungen aus. Die Einstellungen und Benachrichtigungs Optionen sind identisch mit den Optionen, die Sie festlegen können, wenn Sie eine Kontingent Vorlage erstellen. Optional können Sie die Eigenschaften aus einer anderen Vorlage kopieren und für diese ändern.

4.  Wenn Sie mit dem Bearbeiten der Vorlagen Eigenschaften fertig sind, klicken Sie auf **OK**. Dadurch wird das Dialogfeld **aus Vorlage abgeleitete Kontingente aktualisieren** geöffnet.

5.  Wählen Sie den Typ des Updates aus, das Sie anwenden möchten:

    -   Wenn Sie über Kontingente verfügen, die geändert wurden, nachdem Sie mit der ursprünglichen Vorlage erstellt wurden, und Sie diese nicht ändern möchten, wählen Sie **Vorlage nur auf abgeleitete Kontingente anwenden, die mit der ursprünglichen Vorlage**identisch sind aus. Mit dieser Option werden nur die Kontingente aktualisiert, die seit der Erstellung mit der ursprünglichen Vorlage nicht bearbeitet wurden.
    -   Wenn Sie alle vorhandenen Kontingente ändern möchten, die aus der ursprünglichen Vorlage erstellt wurden, wählen Sie **Vorlage auf alle abgeleiteten Kontingente anwenden**aus.
    -   Wenn Sie die vorhandenen Kontingente unverändert halten möchten, wählen Sie **Vorlage nicht auf abgeleitete Kontingente anwenden**aus.

6.  Klicken Sie auf **OK**.

## <a name="additional-references"></a>Weitere Verweise

-   [Kontingentverwaltung](quota-management.md)
-   [Erstellen einer Kontingent Vorlage](create-quota-template.md)


