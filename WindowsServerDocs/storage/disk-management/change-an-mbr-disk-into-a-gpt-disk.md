---
title: "Ändern einer Master Boot Record (GPT)-Festplatte in eine MBR-Partitionstabellen (GUID)-Festplatte"
description: Beschreibt, wie Sie eine Master Boot Record (GPT)-Festplatte in eine MBR-Partitionstabellen (GUID)-Festplatte konvertieren
ms.date: 10/12/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: f28d151d3b1d6b19b9ca330c5ff8576a53acbfa5
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="change-a-master-boot-record-mbr-disk-into-a-guid-partition-table-gpt-disk"></a>So konvertieren Sie eine Master Boot Record (GPT)-Festplatte in eine MBR-Partitionstabellen (GUID)-Festplatte

> **Gilt für**: Windows 10, Windows 8.1, Windows Server (Semi-Annual Channel), Windows Server 10, Windows Server8.1 R2, Windows Server 2016, Windows Server2012 R2, Windows Server 2012

Master Boot Record (MBR)-Festplatten verwenden die Standard-BIOS-Partitionstabelle. GUID-Partitionstabelle (GPT)-Festplatten verwenden Unified Extensible Firmware Interface (UEFI). Ein Vorteil von GPT-Datenträgern ist, dass Sie mehr als vier Partitionen auf jedem Datenträger haben können. GPT ist auch für Datenträger mit mehr als zwei Terabyte (TB) erforderlich.

Sie können eine Festplatte von einem MBR- in einen GPT-Partitionsstil ändern, solange sie leer ist und keine Partitionen oder Volumes enthält.
Sie können den GPT-Partitionsstil nicht auf einem Wechselmedium oder auf Clusterdatenträgern verwenden, die mit freigegebenen SCSI oder Fibre Channel-Bussen verbunden sind, die vom Clusterdienst verwendet werden.

> [!NOTE]
> Beenden Sie alle Programme, die auf diesen Festplatten ausgeführt werden, bevor Sie diese konvertieren.

## <a name="changing-an-mbr-disk-into-a-gpt-disk"></a>So ändern Sie einen MBR-Datenträger in einen GPT-Datenträger

-   [Verwenden der Windows-Benutzeroberfläche](#BKMK_WINUI)
-   [Mit einer Befehlszeile](#BKMK_CMD)

> [!NOTE]
> Sie müssen mindestens ein Mitglied der Gruppe **Sicherungsoperatoren** or **Administratoren** sein, um diese Schritte durchzuführen.

<a id="BKMK_WINUI"></a>
#### <a name="to-change-an-mbr-disk-into-a-gpt-disk-using-the-windows-interface"></a>So ändern Sie mithilfe der Windows-Benutzeroberfläche einen MBR-Datenträger in einen GPT-Datenträger

1.  Sichern Sie oder verschieben Sie alle Daten auf dem MBR-Basisdatenträger, den Sie in einen GPT-Datenträger konvertieren möchten.

2.  Wenn die Festplatte Partitionen oder Volumes enthält, klicken Sie mit der rechten Maustaste auf jede und klicken Sie dann auf **Partition löschen** oder **Volume löschen**.

3.  Klicken Sie mit der rechten Maustaste auf die MBR-Festplatte, die Sie in eine GPT-Festplatte konvertieren möchten, und klicken Sie dann auf **in GPT-Datenträger konvertieren**.

<a id="BKMK_CMD"></a>
#### <a name="to-change-an-mbr-disk-into-a-gpt-disk-using-a-command-line"></a>So ändern Sie mithilfe der Befehlszeile ein MBR-Laufwerk in ein GPT-Laufwerk

1.  Sichern Sie oder verschieben Sie alle Daten auf dem MBR-Basisdatenträger, den Sie in einen GPT-Datenträger konvertieren möchten.

2.  Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, indem Sie mit der rechten Maustaste auf **Eingabeaufforderung** klicken und dann **Als Administrator ausführen** wählen.

3. Geben Sie `diskpart` ein. Wenn der Datenträger keine Partitionen oder Volumes enthält, fahren Sie mit Schritt6 fort.

4.  Geben Sie an der **DISKPART**-Eingabeaufforderung `list disk` ein. Notieren Sie die Anzahl der Festplatten, die Sie konvertieren möchten.

5.  Geben Sie an der **DISKPART**-Eingabeaufforderung `select disk <disknumber>` ein.

6.  Geben Sie an der **DISKPART**-Eingabeaufforderung `clean` ein.

> [!NOTE]
> Der Befehl **Bereinigen** löscht alle Partitionen oder Volumes auf dem Datenträger.

7.  Geben Sie an der **DISKPART**-Eingabeaufforderung `convert gpt` ein.

<br />

| Wert  | Beschreibung  |
| ----- | ----|
| <p>**list disk**</p> | <p>Zeigt eine Liste der Festplatten und deren Informationen an wie z.B. ihre Größe, die Menge an Speicherplatz, ob es sich um einen dynamischen Datenträger handelt und ob die Festplatte den Partitionsstil Master Boot Record (MBR) oder GUID-Partitionstabelle (GPT) verwendet. Die Festplatte mit einem Sternchen (*) hat den Fokus.</p> |
| <p>**select disk** <em>disknumber</em></p> | <p>Wählt die angegebene Festplatte aus, wobei <em>disknumber</em> die Nummer der Festplatte ist, und legt den Fokus fest.</p> |
| <p>**Bereinigen**</p> | <p>Entfernt alle Partitionen oder Volumes vom Datenträger mit dem Fokus.</p>  |
| <p>**convert gpt**</p>| <p>Konvertiert einen leeren Basisdatenträger mit dem Master Boot Record (MBR)-Partitionsstil zu einem Basisdatenträger mit dem GUID-Partitionstabelle-Partitionsstil.</p> |

## <a name="see-also"></a>Weitere Informationen

-   [Notation der Befehlszeilensyntax](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx)


