---
title: Erstellen einer automatischen Klassifizierungsregel
description: Dieser Artikel beschreibt, wie Sie eine Klassifizierungsregel für eine Eigenschaft erstellen.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 8907c15106f4615ce26ba830e11e5f887a3f22aa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402046"
---
# <a name="create-an-automatic-classification-rule"></a>Erstellen einer automatischen Klassifizierungsregel

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Die folgende Anweisung führt Sie durch den Prozess zum Erstellen einer Klassifizierungsregel. Mit jeder Regel wird der Wert für eine einzelne Eigenschaft festgelegt. Standardmäßig wird eine Regel nur einmal ausgeführt und ignoriert Dateien, denen bereits ein Eigenschaftswert zugewiesen wurde. Allerdings können Sie eine Regel zum Bewerten der Dateien konfigurieren, unabhängig davon, ob der Eigenschaft bereits ein Wert zugewiesen wurde oder nicht.

## <a name="to-create-a-classification-rule"></a>So erstellen Sie eine Klassifizierungsregel

1.  Klicken **Sie in der Klassifizierungsverwaltung** auf den Knoten **Klassifizierungsregeln**.

2.  Klicken Sie mit der rechten Maustaste auf **Klassifizierungsregeln** und dann auf **Neue Regel erstellen** (oder klicken Sie auf **Neue Regel erstellen** im Bereich **Aktionen** aus). Daraufhin wird das Dialogfeld **Definitionen für Klassifizierungsregeln** geöffnet.

3.  Geben Sie auf der Registerkarte **Regeleinstellungen** die folgenden Informationen ein:

    -   **Regelname**. Geben Sie einen Namen für die Regel ein.
    -   **Aktiviert**. Die Regel wird nur angewendet, wenn das Kontrollkästchen „Aktiviert” aktiviert ist. Wenn Sie die Regel deaktivieren möchten, deaktivieren Sie das Kontrollkästchen.
    -   **Beschreibung** Geben Sie eine optionale Beschreibung für die Regel ein.
    -   **Umfang**. Klicken Sie auf **Hinzufügen**, um einen Speicherort auszuwählen, für den diese Regel gilt. Sie können mehrere Speicherorte hinzufügen oder einen Speicherort entfernen, indem Sie auf **Entfernen** klicken. Die Klassifizierungsregel gilt für alle Ordner und die zugehörigen Unterordner in dieser Liste.

4.  Geben Sie auf der Registerkarte **Klassifizierung** die folgenden Informationen ein:

    -   **Klassifizierungsmechanismen**. Wählen Sie eine Methode für die Zuweisung des Eigenschaftswerts aus.
    -   **Eigenschaftenname**. Wählen Sie die Eigenschaft aus, der diese Regel zugewiesen wird.
    -   **Eigenschaftenwert**. Wählen Sie den Eigenschaftswert aus, der diese Regel zugewiesen wird.

5.  Optional: Klicken Sie auf die Schaltfläche **Erweitert**, um weitere Optionen auszuwählen. Das Kontrollkästchen **Dateien erneut auswerten** auf der Registerkarte **Evaluierungstyp** ist standardmäßig deaktiviert. Hier können folgende Optionen ausgewählt werden:

    -   **Dateien** nicht überprüft: Eine Regel wird auf eine Datei angewendet, wenn, und nur dann, wenn die von der Regel angegebene Eigenschaft nicht auf einen Wert in der Datei festgelegt wurde.
    -   **Dateien erneut auswerten** aktiviert und die Option **Vorhandenen Wert überschreiben** ist ausgewählt: die Regel wird jedes Mal auf die Dateien angewendet, wenn der automatische Klassifizierungsprozess ausgeführt wird. Wenn beispielsweise eine Datei eine boolesche Eigenschaft hat, die auf **Ja** festgelegt ist, wird eine Regel, die eine Ordnerklassifizierung verwendet, die alle Dateien mit dieser festgelegten Option auf **Nein** setzt, den Eigenschaftensatz auf **Nein** lassen.
    -   Überprüfte **Dateien neu auswerten** und die Option **Werte aggregieren** ausgewählt: Die Regel wird bei jeder Ausführung des automatischen Klassifizierungs Prozesses auf die Dateien angewendet. Wenn die Regel den Wert für die Eigenschaftsdatei festgelegt hat, aggregiert sie diesen Wert mit einem bereits in der Datei vorhandenen Wert. Wenn beispielsweise eine Datei eine boolesche Eigenschaft hat, die auf **Ja** festgelegt ist, wird eine Regel, die eine Ordnerklassifizierung verwendet, die alle Dateien mit dieser festgelegten Option auf **Nein** setzt, den Eigenschaftensatz auf **Ja** lassen.

    Sie können auf der Registerkarte **Zusätzliche Klassifizierungsparameter** zusätzliche Parameter eingeben, die von der ausgewählten Klassifizierungsmethode erkannt werden, indem Sie den Namen und Wert eingeben und auf die Schaltfläche **Einfügen** klicken.

6.  Klicken Sie auf **OK** oder auf **Abbrechen**, um das Dialogfeld **Erweitert** zu schließen.

7.  Klicken Sie auf **OK**.

## <a name="see-also"></a>Siehe auch

-   [Erstellen einer Klassifizierungseigenschaft](create-classification-property.md)
-   [Klassifizierungsverwaltung](classification-management.md)