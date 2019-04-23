---
title: Bearbeiten der Eigenschaften der Dateiprüfungsvorlagen
description: In diesem Artikel wird beschrieben, wie Sie die Eigenschaften der Dateiprüfungsvorlage bearbeiten
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 31ca46707a32d23a5dd9606c57bcaec5d6e53a80
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59846891"
---
# <a name="edit-file-screen-template-properties"></a>Bearbeiten der Eigenschaften der Dateiprüfungsvorlagen

> Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2

Wenn Sie eine Dateiprüfungsvorlage ändern, haben Sie die Möglichkeit, diese Änderungen auf Dateiprüfungen anzuwenden, die mit der ursprünglichen Dateiprüfungsvorlage erstellt wurden. Sie haben die Möglichkeit, nur die Dateiprüfungen zu ändern, die der ursprünglichen Vorlage entsprechen oder alle Dateiprüfungen zu ändern, die von der ursprünglichen Vorlage abgeleitet sind, unabhängig von den Änderungen, die Sie an den Dateiprüfungen vorgenommen haben, seit sie erstellt wurden. Dieses Feature vereinfacht die Aktualisierung der Eigenschaften der Dateiprüfungen, da alle Änderungen an einem zentralen Ort ausgeführt werden können.

> [!Note]
> Wenn Sie die Änderungen auf alle Dateiprüfungen anwenden, die von der ursprünglichen Vorlage abgeleitet wurden, überschreiben Sie alle benutzerdefinierten Dateiprüfungseigenschaften, die Sie erstellt haben.

## <a name="to-edit-file-screen-template-properties"></a>So bearbeiten Sie die Eigenschaften der Dateiprüfungsvorlagen

1.  Wählen Sie im Dialogfeld **Dateiprüfungsvorlagen** die zu ändernde Vorlage aus.

2.  Mit der rechten Maustaste in der Vorlage der Bildschirm, und klicken Sie auf **Bearbeiten der Vorlageneigenschaften** (oder in der **Aktionen** Bereich unter **Datei Bildschirmvorlagen ausgewählt**Option  **Eigenschaften der Vorlage**.) Daraufhin wird die **Dateiprüfungseigenschaften Vorlage** Dialogfeld.

3.  Wenn Sie die Eigenschaften einer anderen Vorlage als Grundlage für eine geänderte Vorlage kopieren und verwenden möchten, wählen Sie in der Dropdownliste **Eigenschaften aus Kontingentvorlage kopieren** eine Vorlage aus, und klicken Sie anschließend auf Kopieren. Klicken Sie anschließend auf **Kopieren**.

4.  Führen Sie alle notwendigen Änderungen aus. Die Einstellungs- und Benachrichtigungsoptionen sind mit denen identisch, die verfügbar sind, wenn Sie eine Dateiprüfungsvorlage erstellen.

5.  Wenn Sie mit der Bearbeitung der Vorlageneigenschaften fertig sind, klicken Sie auf **OK**. Das Dialogfeld **Aus Vorlage abgeleitete Dateiprüfungen aktualisieren** wird geöffnet.

6.  Wählen Sie den Aktualisierungstyp aus, den Sie anwenden möchten:

    -   Wenn Sie Dateiprüfungen haben, die seit der Erstellung mit der ursprünglichen Vorlage geändert wurden und Sie diese nicht ändern möchten, klicken Sie auf **Vorlage nur auf abgeleitete Dateiprüfungen anwenden, die mit der Originalvorlage übereinstimmen**. Diese Option aktualisiert nur die Dateiprüfungen, die seit der Erstellung mit den ursprünglichen Vorlageneigenschaften nicht bearbeitet wurden.
    -   Wenn Sie alle vorhandenen Dateiprüfungen ändern möchten, die mit der ursprünglichen Vorlage erstellt wurden, klicken Sie auf **Vorlage auf alle abgeleiteten Dateiprüfungen anwenden**.
    -   Wenn Sie die vorhandene Dateiprüfungen unverändert beibehalten möchten, klicken Sie auf **Vorlage nicht auf abgeleitete Dateiprüfungen anwenden**.

7.  Klicken Sie auf **OK**.

## <a name="see-also"></a>Siehe auch

-   [Dateiprüfungsverwaltung](file-screening-management.md)
-   [Erstellen Sie eine Bildschirmvorlage Datei](create-file-screen-template.md)


