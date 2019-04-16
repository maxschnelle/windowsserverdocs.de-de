---
title: "Den Datenträger einen anderen Computer verschieben"
description: "In diesem Artikel wird beschrieben, wie Sie Datenträger auf einen anderen Computer verschieben"
ms.date: 10/12/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 6b235ce8e5b936940629d5977a17bbc729efbe82
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="move-disks-to-another-computer"></a>Den Datenträger einen anderen Computer verschieben

> **Gilt für**: Windows 10, Windows 8.1, Windows Server (Semi-Annual Channel), Windows Server 10, Windows Server8.1 R2, Windows Server 2016, Windows Server2012 R2, Windows Server 2012

Dieser Abschnitt beschreibt die Schritte und Überlegungen, Datenträger auf einen anderen Computer zu verschieben. Möglicherweise möchten Sie dieses Verfahren ausdrucken oder die Schritte notieren, bevor Sie versuchen, den Datenträger von einem Computer auf einen anderen zu verschieben.

> [!NOTE]
> Sie müssen mindestens ein Mitglied der Gruppe **Sicherungsoperatoren** or **Administratoren** sein, um diese Schritte durchzuführen.

## <a name="verify-volume-health"></a>Überprüfen der Volume-Integrität

Verwenden Sie die Datenträgerverwaltung, um sicherzustellen, dass der Status des Volumes auf dem Datenträger **Fehlerfrei** ist. Wenn der Status nicht **Fehlerfrei** ist, reparieren Sie die Volumes vor dem Verschieben der Datenträger.

Um den Datenträgerstatus im Menü **Ansicht** zu überprüfen, überprüfen Sie die Spalte **Status** in der **Volumeliste**-Ansicht oder unter **Volumegröße** und Dateisystem-Informationen in der **Grafischen Ansicht**.

## <a name="uninstall-the-disks"></a>Deinstallieren Sie die Datenträger

Deinstallieren Sie mithilfe des Geräte-Managers die Datenträger, die verschoben werden sollen.

**So deinstallieren Sie die Datenträger**

1.  Öffnen Sie den Geräte-Manager in der Computerverwaltung.

2.  Doppelklicken Sie in der Liste der Geräte auf **Laufwerke**.

3.  Klicken Sie mit der rechten Maustaste auf die zu deinstallierenden Datenträger, und klicken Sie dann auf **Deinstallieren**.

4.  Klicken Sie im Dialogfeld **Entfernen des Geräts bestätigen** auf **OK**.

## <a name="remove-dynamic-disks"></a>Entfernen dynamischer Datenträger

1. Wenn die Datenträger, die Sie verschieben möchten dynamische Datenträger sind, klicken Sie in der Datenträgerverwaltung mit der rechten Maustaste auf die Datenträger, die Sie verschieben möchten, und klicken Sie dann auf **Datenträger entfernen**.

2. Nach dem Entfernen der dynamischen Datenträger, oder wenn Sie Basisfestplatten verschieben, können Sie diese jetzt physisch trennen. Wenn es sich um externe Datenträger handelt, können Sie diese jetzt vom Computer entfernen. Wenn es sich um interne Datenträger handelt, schalten Sie den Computer aus und entfernen Sie diese physisch.

## <a name="install-disks-in-the-new-computer"></a>Installieren Sie Datenträger in den neuen Computer.

1. Wenn es sich um externe Datenträger handelt, schließen sie diese an den Computer an. Wenn es sich um interne Datenträger handelt, stellen Sie sicher, dass der Computer deaktiviert ist und installieren Sie dann die Datenträger auf diesem Computer.

2. Starten Sie den Computer, der die Datenträger enthält, die verschoben werden sollen und folgen Sie den Anweisungen im Dialogfeld "Neue Hardware gefunden".

## <a name="detect-new-disks"></a>Neue Datenträger erkennen

1. Öffnen Sie die "Datenträgerverwaltung" auf dem neuen Computer. 
2. Klicken Sie auf **Aktion** und dann auf **Festplatten neu einlesen**.
3. Klicken Sie mit der rechten Maustaste auf einen Datenträger mit der Markierung **Fremd**. 
4. Klicken Sie auf **Fremde Datenträger importieren**, und befolgen Sie dann die Anweisungen auf dem Bildschirm.

## <a name="additional-considerations"></a>Weitere Überlegungen

-   Nach dem Verschieben auf einen anderen Computer erhalten Basisvolumes den nächsten verfügbaren Laufwerkbuchstaben auf dem Computer. 
-   Dynamische Volumes behalten den Laufwerkbuchstaben, den sie auf dem vorherigen Computer hatten. Wenn ein dynamisches Volume keinen Laufwerkbuchstaben auf dem vorherigen Computer hatte, erhält es keinen Laufwerkbuchstaben, wenn es auf den anderen Computer verschoben wird. Wenn der Laufwerkbuchstabe auf dem Computer bereits verwendet wird, auf denen das Volume verschoben wird, erhält das Volume den nächsten verfügbaren Laufwerkbuchstaben.

-   Wenn ein Administrator entweder die **mountvol /n** oder die **diskpart automount**-Befehle verwendet hat, um zu verhindern, dass neue Volumes dem System hinzugefügt werden, wird verhindert, dass Volumes, die von einem anderen Computer verschoben werden, bereitgestellt werden und einen Laufwerkbuchstaben erhalten. Um das Volume zu verwenden, müssen Sie manuell das Volume bereitstellen und ihm einen Laufwerkbuchstaben mit der Datenträgerverwaltung oder den Befehlen **DiskPart** und **Mountvol** zuweisen.

-   Wenn Sie einfache, übergreifende, Stripeset- oder gespiegelte Volumes oder RAID-5-Volumes verschieben, wird dringend empfohlen, alle Datenträger zusammen zu verschieben, die das Volume enthalten. Andernfalls können die Volumes auf den Datenträgern nicht online geschaltet werden und stehen nicht zur Verfügung, es sei denn, sie möchten diese löschen.

-   Sie können mehrere Datenträger von verschiedenen Computern auf einen Computer verschieben, indem Sie die Datenträger installieren, die Datenträgerverwaltung öffnen, mit der rechten Maustaste auf den neuen Datenträger klicken und dann auf **fremde Datenträger importieren** klicken. Wenn Sie mehrere Datenträger von verschiedenen Computern importieren, sollten Sie immer alle Datenträger von einem Computer in einem Schritt importieren. Wenn Sie beispielsweise Datenträger von zwei Computern verschieben möchten, importieren Sie alle Datenträger aus dem ersten Computer und importieren Sie dann alle Datenträger vom zweiten Computer.

-   Die Datenträgerverwaltung beschreibt die Bedingung der Volumes auf den Datenträgern, bevor sie importiert werden. Lesen Sie diese Informationen sorgfältig. Wenn Probleme aufgetreten sollten, lernen Sie aus diesen Informationen, was mit den einzelnen Volumes auf diesen Datenträgern passiert, nachdem die Datenträger importiert wurden.

-   Wenn Sie eine GPT-Datenträger (GUID Partition Table, GUID-Partitionstabelle) mit dem Windows-Betriebssystem auf einen x86-basierten oder x64-basierten Computer verschieben, können Sie auf die Daten zugreifen, aber Sie können nicht über dieses Betriebssystem starten.