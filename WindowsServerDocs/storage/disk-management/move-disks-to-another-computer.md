---
title: Verschieben von Datenträgern auf einen anderen Computer
description: In diesem Artikel wird beschrieben, wie du Datenträger auf einen anderen Computer verschiebst.
ms.date: 10/12/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 1527dbd567eb72e407023ecdcfade04856a3127a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971187"
---
# <a name="move-disks-to-another-computer"></a>Verschieben von Datenträgern auf einen anderen Computer

> **Gilt für:** Windows 10, Windows 8.1, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieser Abschnitt beschreibt die erforderlichen Schritte und Überlegungen im Zusammenhang mit dem Verschieben von Datenträgern auf einen anderen Computer. Es wird empfohlen, diese Vorgehensweise auszudrucken oder sich die Schritte zu notieren, bevor du Datenträger von einem Computer auf einen anderen verschiebst.

> [!NOTE]
> Du musst mindestens Mitglied der Gruppe **Sicherungsoperatoren** oder **Administratoren** sein, um diese Schritte ausführen zu können.

## <a name="verify-volume-health"></a>Überprüfen der Volume-Integrität

Stelle mithilfe der Datenträgerverwaltung sicher, dass der Status der Volumes auf den Datenträgern **Fehlerfrei** lautet. Lautet der Status nicht **Fehlerfrei**, repariere die Volumes vor dem Verschieben der Datenträger.

Den Volumestatus kannst du über das Menü **Ansicht** in der Spalte **Status** der Ansicht **Volumeliste** oder in der **grafischen Ansicht** in den Informationen zu **Volumegröße** und Dateisystem überprüfen.

## <a name="uninstall-the-disks"></a>Deinstallieren der Datenträger

Deinstalliere mithilfe des Geräte-Managers die Datenträger, die verschoben werden sollen.

**So deinstallierst du Datenträger**

1.  Öffne den Geräte-Manager in der Computerverwaltung.

2.  Doppelklicke in der Geräteliste auf **Laufwerke**.

3.  Klicken Sie mit der rechten Maustaste auf die zu deinstallierenden Datenträger, und klicken Sie dann auf **Deinstallieren**.

4.  Klicken Sie im Dialogfeld **Entfernen des Geräts bestätigen** auf **OK**.

## <a name="remove-dynamic-disks"></a>Entfernen dynamischer Datenträger

1. Möchtest du dynamische Datenträger verschieben, klicke in der Datenträgerverwaltung mit der rechten Maustaste auf die zu verschiebenden Datenträger, und klicke dann auf **Datenträger entfernen**.

2. Wenn du dynamische Datenträger entfernt hast oder Basisfestplatten verschiebst, kannst du sie jetzt physisch trennen. Wenn es sich um externe Datenträger handelt, kannst du diese jetzt vom Computer entfernen. Schalte bei internen Datenträger den Computer aus, und entferne sie dann physisch.

## <a name="install-disks-in-the-new-computer"></a>Einbauen von Datenträgern in den neuen Computer

1. Wenn es sich um externe Datenträger handelt, schließe sie an den Computer an. Stelle bei internen Datenträger sicher, dass der Computer ausgeschaltet ist, und baue die Datenträger dann in den Computer ein.

2. Starte den Computer mit den verschobenen Datenträgern, und befolge die Anweisungen im Dialogfeld „Neue Hardware gefunden“.

## <a name="detect-new-disks"></a>Erkennen neuer Datenträger

1. Öffne die Datenträgerverwaltung auf dem neuen Computer.
2. Klicke auf **Aktion** und anschließend auf **Datenträger neu einlesen**.
3. Klicke mit der rechten Maustaste auf einen Datenträger mit der Kennzeichnung **Fremd**.
4. Klicke auf **Fremde Datenträger importieren**, und befolge die Bildschirmanweisungen.

## <a name="additional-considerations"></a>Weitere Überlegungen

-   Beim Verschieben auf einen anderen Computer erhalten Basisvolumes den nächsten verfügbaren Laufwerkbuchstaben auf dem Computer.
-   Dynamische Volumes behalten den Laufwerkbuchstaben, den sie auf dem vorherigen Computer hatten. War einem dynamischen Volume auf dem vorherigen Computer kein Laufwerkbuchstabe zugewiesen, erhält es beim Verschieben auf einen anderen Computer keinen Laufwerkbuchstaben. Wird der Laufwerkbuchstabe auf dem Computer bereits verwendet, auf den das Volume verschoben wird, erhält das Volume den nächsten verfügbaren Laufwerkbuchstaben.

-   Wenn ein Administrator den Befehl **mountvol /n** oder **diskpart automount** ausgeführt hat, um zu verhindern, dass dem System neue Volumes hinzugefügt werden, können von einem anderen Computer verschobene Volumes nicht eingebunden werden, und sie erhalten auch keinen Laufwerkbuchstaben. Wenn du das Volume verwenden möchtest, musst du es mit der Datenträgerverwaltung oder den Befehlen **DiskPart** und **mountvol** manuell einbinden und ihm einen Laufwerkbuchstaben zuweisen.

-   Wenn du übergreifende oder gespiegelte Volumes oder Stripeset- oder RAID-5-Volumes verschiebst, wird dringend empfohlen, alle Datenträger zusammen zu verschieben, die das Volume enthalten. Andernfalls können die Volumes auf den Datenträgern nicht online geschaltet werden und stehen (außer zum Löschen) nicht zur Verfügung.

-   Du kannst mehrere Datenträger von verschiedenen Computern auf einen Computer verschieben. Baue dazu die Datenträger ein, öffne die Datenträgerverwaltung, und klicke mit der rechten Maustaste auf einen der neuen Datenträger. Klicke dann auf **Fremde Datenträger importieren**. Wenn du mehrere Datenträger von verschiedenen Computern importierst, importiere immer jeweils alle Datenträger von einem Computer. Beispiel: Wenn du Datenträger von zwei Computern verschieben möchtest, importiere alle Datenträger vom ersten Computer und dann alle Datenträger vom zweiten Computer.

-   Die Datenträgerverwaltung beschreibt den Zustand der Volumes auf den Datenträgern vor dem Import. Lies diese Informationen sorgfältig. Sollten Probleme auftreten, kannst du anhand dieser Informationen ermitteln, was mit den einzelnen Volumes auf diesen Datenträgern nach ihrem Import geschieht.

-   Wenn du einen GPT-Datenträger (GUID Partition Table, GUID-Partitionstabelle) mit dem Windows-Betriebssystem auf einen x86-basierten oder x64-basierten Computer verschiebst, kannst du auf die Daten zugreifen, aber nicht über dieses Betriebssystem starten.