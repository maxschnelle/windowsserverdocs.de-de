---
title: Ändern einer GUID-Partitionstabellen (GPT)-Festplatte in eine Master Boot Record (MBR)-Festplatte
description: Beschreibt, wie Sie den Partitionsstil einer GUID-Partitionstabellen (GPT)-Festplatte in eine Master Boot Record (MBR)-Festplatte konvertieren.
ms.date: 06/19/2018
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 5cd345230ce5c0fc556bfd8b421d866bd827507b
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812445"
---
# <a name="convert-a-gpt-disk-into-an-mbr-disk"></a>Konvertieren Sie einen GPT-Datenträger in einen MBR-Datenträger

> **Gilt für:** Windows 10, Windows 8.1, WindowsServer (Halbjährlicher Kanal), WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012

Master Boot Record (MBR)-Festplatten verwenden die Standard-BIOS-Partitionstabelle. GUID-Partitionstabelle (GPT)-Festplatten verwenden Unified Extensible Firmware Interface (UEFI). MBR-Festplatten unterstützen nicht mehr als vier Partitionen auf jeder Festplatte. Die Methode der MBR-Partition wird nicht für Festplatten mit mehr als zwei Terabyte (TB) empfohlen.

Sie können eine Festplatte von einem GPT- in einen MBR-Partitionsstil ändern, solange sie leer ist und keine Volumes enthält.

> [!NOTE]
> Bevor Sie einen Datenträger konvertieren, Sichern Sie alle Daten darauf aus, und schließen Sie alle Programme, die auf den Datenträger zugreifen.

> [!NOTE]
> Sie müssen mindestens ein Mitglied der Gruppe **Sicherungsoperatoren** or **Administratoren** sein, um diese Schritte durchzuführen.

## <a name="converting-using-the-windows-interface"></a>Konvertieren mithilfe der Windows-Benutzeroberfläche

1.  Sichern Sie oder verschieben Sie alle Volumes auf dem GPT-Basisdatenträger, die Sie in eine MBR-Festplatte konvertieren möchten.

2.  Wenn die Festplatte Partitionen oder Volumes enthält, klicken Sie mit der rechten Maustaste auf jede und klicken Sie dann auf **Volume löschen**.

3.  Klicken Sie mit der rechten Maustaste auf die GPT-Festplatte, die Sie in eine MBR-Festplatte konvertieren möchten, und klicken Sie dann auf **in MBR-Datenträger konvertieren**.

## <a name="converting-using-a-command-line"></a>Konvertieren mithilfe einer Befehlszeile

1.  Sichern Sie oder verschieben Sie alle Volumes auf dem GPT-Basisdatenträger, die Sie in eine MBR-Festplatte konvertieren möchten.

2.  Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, indem Sie mit der rechten Maustaste auf **Eingabeaufforderung** klicken und dann **Als Administrator ausführen** wählen.

3. Geben Sie `diskpart` ein. Wenn der Datenträger keine Partitionen oder Volumes enthält, fahren Sie mit Schritt 6 fort.

4.  Geben Sie an der **DISKPART**-Eingabeaufforderung `list disk` ein. Notieren Sie die Datenträgernummer, die entfernt werden soll.

5.  Geben Sie an der **DISKPART**-Eingabeaufforderung `select disk <disknumber>` ein.

6.  Geben Sie an der **DISKPART**-Eingabeaufforderung `clean` ein.

    > [!IMPORTANT]
    > Der Befehl **Bereinigen** löscht alle Partitionen oder Volumes auf dem Datenträger.

7.  Geben Sie an der **DISKPART**-Eingabeaufforderung `convert mbr` ein.

|                Wert                  |      Beschreibung   |
| ------------------------------------- | -----------------  |
|  <strong>Liste Datenträger</strong>  | Zeigt eine Liste der Festplatten und deren Informationen an wie z. B. ihre Größe, die Menge an Speicherplatz, ob es sich um eine Basis- oder einen dynamischen Datenträger handelt und ob die Festplatte den Partitionsstil Master Boot Record (MBR) oder GUID-Partitionstabelle (GPT) verwendet. Der Datenträger mit einem Sternchen gekennzeichnet (\*) den Fokus besitzt. |
| <strong>Wählen Sie Datenträger</strong> |                                                                                                          Wählt die angegebene Festplatte aus, wobei <em>disknumber</em> die Nummer der Festplatte ist, und legt den Fokus fest.                                                                                                           |
| <strong>Konvertieren von mbr</strong> |                                                                               Konvertiert einen leeren Basisdatenträger mit dem GUID-Partitionstabelle (GPT)-Partitionsstil zu einem Basisdatenträger mit Master Boot Record (MBR)-Partitionsstil.                                                                                |

## <a name="see-also"></a>Siehe auch

-   [Notation der Befehlszeilensyntax](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx)