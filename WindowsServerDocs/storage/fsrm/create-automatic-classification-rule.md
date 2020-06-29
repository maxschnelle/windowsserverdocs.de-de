---
title: Erstellen einer automatischen Klassifizierungsregel
description: In diesem Artikel wird beschrieben, wie eine Klassifizierungs Regel für eine Eigenschaft erstellt wird.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 9fc2034905408975f82f9348f151d99df17f9d3a
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475397"
---
# <a name="create-an-automatic-classification-rule"></a>Erstellen einer automatischen Klassifizierungsregel

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Das folgende Verfahren führt Sie durch den Prozess der Erstellung einer Klassifizierungs Regel. Mit jeder Regel wird der Wert für eine einzelne Eigenschaft festgelegt. Standardmäßig wird eine Regel nur einmal ausgeführt, und es werden Dateien ignoriert, denen bereits ein Eigenschafts Wert zugewiesen wurde. Sie können jedoch eine Regel so konfigurieren, dass Dateien ausgewertet werden, unabhängig davon, ob der Eigenschaft bereits ein Wert zugewiesen wurde.

## <a name="to-create-a-classification-rule"></a>So erstellen Sie eine Klassifizierungs Regel

1.  Klicken Sie in der Klassifizierungsverwaltung **** auf den Knoten **Klassifizierungsregeln**.

2.  Klicken Sie mit der rechten Maustaste auf **Klassifizierungsregeln**, und klicken Sie dann auf **neue Regel erstellen** (oder klicken Sie im **Aktions** Bereich auf **neue Regel erstellen** ). Daraufhin wird das Dialogfeld **Definitionen für Klassifizierungsregeln** geöffnet.

3.  Geben Sie auf der Registerkarte **Regel Einstellungen** die folgenden Informationen ein:

    -   **Regelname**. Geben Sie einen Namen für die Regel ein.
    -   **Aktiviert**. Diese Regel wird nur angewendet, wenn das Kontrollkästchen aktiviert aktiviert ist. Wenn Sie die Regel deaktivieren möchten, deaktivieren Sie das Kontrollkästchen.
    -   **Beschreibung**. Geben Sie eine optionale Beschreibung für die Regel ein.
    -   **Umfang**. Klicken Sie auf **Hinzufügen** , um einen Speicherort für die Regel auszuwählen. Sie können mehrere Speicherorte hinzufügen oder einen Speicherort entfernen, indem Sie auf **Entfernen**klicken. Die Klassifizierungs Regel gilt für alle Ordner und deren Unterordner in dieser Liste.

4.  Geben Sie auf der Registerkarte **Klassifizierung** die folgenden Informationen ein:

    -   **Klassifizierungs Mechanismus**. Wählen Sie eine Methode aus, um den Eigenschafts Wert zuzuweisen.
    -   **Eigenschaftsname**. Wählen Sie die Eigenschaft aus, die von dieser Regel zugewiesen wird.
    -   **Eigenschafts Wert**. Wählen Sie den Eigenschafts Wert aus, der von dieser Regel zugewiesen wird.

5.  Klicken Sie optional auf die Schaltfläche **erweitert** , um weitere Optionen auszuwählen. Auf der Registerkarte **Auswertungs Typen** ist das Kontrollkästchen zum **erneuten Auswerten von Dateien** standardmäßig deaktiviert. Die folgenden Optionen können ausgewählt werden:

    -   **Dateien** nicht überprüft: eine Regel wird auf eine Datei angewendet, wenn, und nur dann, wenn die von der Regel angegebene Eigenschaft nicht auf einen Wert in der Datei festgelegt wurde.
    -   Überprüfte **Dateien neu auswerten** und die Option **vorhandenen Wert überschreiben** ausgewählt: die Regel wird bei jeder Ausführung des automatischen Klassifizierungs Prozesses auf die Dateien angewendet. Wenn eine Datei z. b. eine boolesche Eigenschaft aufweist, die auf **Ja**festgelegt ist, wird für eine Regel, bei der die Ordner Klassifizierung verwendet wird, um alle Dateien mit diesem Options Satz auf **Nein** festzulegen, die-Eigenschaft auf **Nein**festgelegt.
    -   Überprüfte **Dateien neu auswerten** und die Option **Werte aggregieren** ausgewählt: die Regel wird bei jeder Ausführung des automatischen Klassifizierungs Prozesses auf die Dateien angewendet. Wenn die Regel jedoch festgelegt hat, auf welchen Wert die Eigenschaften Datei festgelegt werden soll, wird dieser Wert mit dem bereits in der Datei vorhandenen Wert aggregiert. Wenn eine Datei z. b. eine boolesche Eigenschaft aufweist, die auf **Ja**festgelegt ist, wird für eine Regel, bei der der Ordner Klassifizierung verwendet wird, um alle Dateien mit diesem Options Satz auf **Nein** festzulegen, die-Eigenschaft auf **Yes**festgelegt.

    Auf der Registerkarte **zusätzliche Klassifizierungs Parameter** können Sie zusätzliche Parameter angeben, die von der ausgewählten Klassifizierungsmethode erkannt werden, indem Sie den Namen und den Wert eingeben und auf die Schaltfläche **Einfügen** klicken.

6.  Klicken Sie auf **OK** oder auf **Abbrechen**, um das Dialogfeld **Erweitert** zu schließen.

7.  Klicken Sie auf **OK**.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Erstellen einer Klassifizierungseigenschaft](create-classification-property.md)
-   [Klassifizierungsverwaltung](classification-management.md)