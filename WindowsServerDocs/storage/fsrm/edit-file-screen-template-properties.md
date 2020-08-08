---
title: Bearbeiten der Eigenschaften der Dateiprüfungsvorlage
description: In diesem Artikel wird beschrieben, wie Sie Eigenschaften von Datei Bildschirm Vorlagen bearbeiten.
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 86a6a6233c1a2092a5a54b807215c12b1f0a1bae
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942078"
---
# <a name="edit-file-screen-template-properties"></a>Bearbeiten der Eigenschaften der Dateiprüfungsvorlage

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Wenn Sie Änderungen an einer Datei Bildschirm Vorlage vornehmen, haben Sie die Möglichkeit, diese Änderungen auf Datei Bildschirme auszudehnen, die mit der ursprünglichen Datei Bildschirm Vorlage erstellt wurden. Sie können auswählen, ob Sie nur die Datei Bildschirme ändern möchten, die der ursprünglichen Vorlage oder allen Datei Bildschirmen entsprechen, die von der ursprünglichen Vorlage abgeleitet werden, unabhängig von Änderungen, die Sie seit der Erstellung an den Datei Bildschirmen vorgenommen haben. Diese Funktion vereinfacht die Aktualisierung der Eigenschaften von Datei Bildschirmen, indem Sie einen zentralen Punkt bereitstellt, an dem alle Änderungen vorgenommen werden.

> [!Note]
> Wenn Sie die Änderungen auf alle Datei Bildschirme anwenden, die von der ursprünglichen Vorlage abgeleitet werden, überschreiben Sie alle benutzerdefinierten Datei Bildschirm Eigenschaften, die Sie erstellt haben.

## <a name="to-edit-file-screen-template-properties"></a>So bearbeiten Sie die Eigenschaften der Datei Bildschirm Vorlage

1.  Wählen Sie unter **Datei Bildschirm Vorlagen**die Vorlage aus, die Sie ändern möchten.

2.  Klicken Sie mit der rechten Maustaste auf die Datei Bildschirm Vorlage, und klicken Sie auf **Vorlagen Eigenschaften bearbeiten** (oder wählen Sie im Bereich **Aktionen** unter **ausgewählte Datei Bildschirm Vorlagen**die Option **Vorlagen Eigenschaften bearbeiten**aus.) Dadurch wird das Dialogfeld **Eigenschaften der Datei Bildschirm Vorlage** geöffnet.

3.  Wenn Sie die Eigenschaften einer anderen Vorlage als Basis für die geänderte Vorlage kopieren möchten, wählen Sie eine Vorlage aus der Dropdown Liste **Eigenschaften aus Vorlage kopieren** aus. Klicken Sie dann auf **Kopieren**.

4.  Führen Sie alle erforderlichen Änderungen aus. Die Einstellungen und Benachrichtigungs Optionen sind identisch mit den Optionen, die verfügbar sind, wenn Sie eine Datei Bildschirm Vorlage erstellen.

5.  Wenn Sie mit dem Bearbeiten der Vorlagen Eigenschaften fertig sind, klicken Sie auf **OK**. Dadurch wird das Dialogfeld **aus Vorlage abgeleitete Datei Bildschirme aktualisieren** geöffnet.

6.  Wählen Sie den Typ des Updates aus, das Sie anwenden möchten:

    -   Wenn Sie über Datei Bildschirme verfügen, die geändert wurden, seit Sie mit der ursprünglichen Vorlage erstellt wurden, und Sie Sie nicht ändern möchten, klicken Sie auf **Vorlage nur auf abgeleitete Datei Bildschirme anwenden, die mit der ursprünglichen Vorlage**identisch sind. Mit dieser Option werden nur die Datei Bildschirme aktualisiert, die seit der Erstellung mit den ursprünglichen Vorlagen Eigenschaften nicht bearbeitet wurden.
    -   Wenn Sie alle vorhandenen Datei Bildschirme ändern möchten, die mit der ursprünglichen Vorlage erstellt wurden, klicken Sie **auf Vorlage auf alle abgeleiteten Datei Bildschirme anwenden**.
    -   Wenn Sie die vorhandenen Datei Bildschirme unverändert halten möchten, klicken Sie auf **Vorlage nicht auf abgeleitete Datei Bildschirme anwenden**.

7.  Klicken Sie auf **OK**.

## <a name="additional-references"></a>Weitere Verweise

-   [Datei Prüfungsverwaltung](file-screening-management.md)
-   [Erstellen einer Dateiprüfungsvorlage](create-file-screen-template.md)


