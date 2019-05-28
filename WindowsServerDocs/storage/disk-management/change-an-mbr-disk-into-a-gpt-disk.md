---
title: Ändern einer Master Boot Record (GPT)-Festplatte in eine MBR-Partitionstabellen (GUID)-Festplatte
description: Beschreibt, wie Sie eine Master Boot Record (GPT)-Festplatte in eine MBR-Partitionstabellen (GUID)-Festplatte konvertieren
ms.date: 06/19/2018
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: f6aba72c329ba380f9617f484c4cf754fbcbb363
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192727"
---
# <a name="convert-an-mbr-disk-into-a-gpt-disk"></a>Konvertieren Sie einen MBR-Datenträger in einen GPT-Datenträger

> **Gilt für:** Windows 10, Windows 8.1, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012

Master Boot Record (MBR)-Festplatten verwenden die Standard-BIOS-Partitionstabelle. GUID-Partitionstabelle (GPT)-Festplatten verwenden Unified Extensible Firmware Interface (UEFI). Ein Vorteil von GPT-Datenträgern ist, dass Sie mehr als vier Partitionen auf jedem Datenträger haben können. GPT ist auch für Datenträger mit mehr als zwei Terabyte (TB) erforderlich.

Sie können eine Festplatte von einem MBR- in einen GPT-Partitionsstil ändern, solange sie leer ist und keine Partitionen oder Volumes enthält.

> [!NOTE]
> Bevor Sie einen Datenträger konvertieren, Sichern Sie alle Daten darauf aus, und schließen Sie alle Programme, die auf den Datenträger zugreifen.

> [!NOTE]
> Sie müssen mindestens ein Mitglied der Gruppe **Sicherungsoperatoren** or **Administratoren** sein, um diese Schritte durchzuführen.

## <a name="converting-using-the-windows-interface"></a>Konvertieren mithilfe der Windows-Benutzeroberfläche

1.  Sichern Sie oder verschieben Sie alle Daten auf dem MBR-Basisdatenträger, den Sie in einen GPT-Datenträger konvertieren möchten.

2.  Wenn die Festplatte Partitionen oder Volumes enthält, klicken Sie mit der rechten Maustaste auf jede und klicken Sie dann auf **Partition löschen** oder **Volume löschen**.

3.  Klicken Sie mit der rechten Maustaste auf die MBR-Festplatte, die Sie in eine GPT-Festplatte konvertieren möchten, und klicken Sie dann auf **in GPT-Datenträger konvertieren**.

## <a name="converting-using-a-command-line"></a>Konvertieren mithilfe einer Befehlszeile

Verwenden Sie die folgenden Schritte aus, um einen leeren MBR-Datenträger auf einem GPT-Datenträger zu konvertieren. Es gibt auch eine MBR2GPT. EXE-Tool, das Sie verwenden können, aber es ist ein wenig kompliziert - finden Sie unter [konvertieren MBR-Partition zu GPT](https://docs.microsoft.com/windows/deployment/mbr-to-gpt) Weitere Details.

1.  Sichern Sie oder verschieben Sie alle Daten auf dem MBR-Basisdatenträger, den Sie in einen GPT-Datenträger konvertieren möchten.

2.  Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, indem Sie mit der rechten Maustaste auf **Eingabeaufforderung** klicken und dann **Als Administrator ausführen** wählen.

3. Geben Sie `diskpart` ein. Wenn der Datenträger keine Partitionen oder Volumes enthält, fahren Sie mit Schritt 6 fort.

4.  Geben Sie an der **DISKPART**-Eingabeaufforderung `list disk` ein. Notieren Sie die Anzahl der Festplatten, die Sie konvertieren möchten.

5.  Geben Sie an der **DISKPART**-Eingabeaufforderung `select disk <disknumber>` ein.

6.  Geben Sie an der **DISKPART**-Eingabeaufforderung `clean` ein.

    > [!NOTE]
    > Der Befehl **Bereinigen** löscht alle Partitionen oder Volumes auf dem Datenträger.

7.  Geben Sie an der **DISKPART**-Eingabeaufforderung `convert gpt` ein.

| Wert  | Beschreibung  |
| ----- | ----|
| **Liste Datenträger** | Zeigt eine Liste der Festplatten und deren Informationen an wie z. B. ihre Größe, die Menge an Speicherplatz, ob es sich um einen dynamischen Datenträger handelt und ob die Festplatte den Partitionsstil Master Boot Record (MBR) oder GUID-Partitionstabelle (GPT) verwendet. Die Festplatte mit einem Sternchen (*) hat den Fokus. |
| **Wählen Sie Datenträger** *Disknumber* | Wählt die angegebene Festplatte aus, wobei *disknumber* die Nummer der Festplatte ist, und legt den Fokus fest. |
| **clean** | Entfernt alle Partitionen oder Volumes vom Datenträger mit dem Fokus.  |
| **Konvertieren von gpt**| Konvertiert einen leeren Basisdatenträger mit dem Master Boot Record (MBR)-Partitionsstil zu einem Basisdatenträger mit dem GUID-Partitionstabelle-Partitionsstil. |

## <a name="see-also"></a>Siehe auch

-   [Notation der Befehlszeilensyntax](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx)


