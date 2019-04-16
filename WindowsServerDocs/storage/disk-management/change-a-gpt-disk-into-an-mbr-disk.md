---
title: "Ändern einer GUID-Partitionstabellen (GPT)-Festplatte in eine Master Boot Record (MBR)-Festplatte"
description: Beschreibt, wie Sie den Partitionsstil einer GUID-Partitionstabellen (GPT)-Festplatte in eine Master Boot Record (MBR)-Festplatte konvertieren.
ms.date: 10/12/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 8efe6617c46267f7e165550de82b18421ab563ca
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="change-a-guid-partition-table-gpt-disk-into-a-master-boot-record-mbr-disk"></a>Ändern einer GUID-Partitionstabellen (GPT)-Festplatte in eine Master Boot Record (MBR)-Festplatte

> **Gilt für**: Windows 10, Windows 8.1, Windows Server (Semi-Annual Channel), Windows Server 10, Windows Server8.1 R2, Windows Server 2016, Windows Server2012 R2, Windows Server 2012

Master Boot Record (MBR)-Festplatten verwenden die Standard-BIOS-Partitionstabelle. GUID-Partitionstabelle (GPT)-Festplatten verwenden Unified Extensible Firmware Interface (UEFI). MBR-Festplatten unterstützen nicht mehr als vier Partitionen auf jeder Festplatte. Die Methode der MBR-Partition wird nicht für Festplatten mit mehr als zwei Terabyte (TB) empfohlen.

Sie können eine Festplatte von einem GPT- in einen MBR-Partitionsstil ändern, solange sie leer ist und keine Volumes enthält.

> [!NOTE]
> Beenden Sie alle Programme, die auf diesen Festplatten ausgeführt werden, bevor Sie diese konvertieren.

<a name="changing-a-gpt-disk-into-an-mbr-disk"></a>So ändern einen GPT-Datenträger in einen MBR-Datenträger
-------------------------------------------------------

-   [Verwenden der Windows-Benutzeroberfläche](#BKMK_WINUI)
-   [Mit einer Befehlszeile](#BKMK_CMD)

> [!NOTE]
> Sie müssen mindestens ein Mitglied der Gruppe **Sicherungsoperatoren** or **Administratoren** sein, um diese Schritte durchzuführen.

 <a id="BKMK_WINUI"></a>
#### <a name="to-change-a-gpt-disk-into-an-mbr-disk-using-the-windows-interface"></a>So ändern Sie mithilfe der Windows-Benutzeroberfläche einen GPT-Datenträger in einen MBR-Datenträger

1.  Sichern Sie oder verschieben Sie alle Volumes auf dem GPT-Basisdatenträger, die Sie in eine MBR-Festplatte konvertieren möchten.

2.  Wenn die Festplatte Partitionen oder Volumes enthält, klicken Sie mit der rechten Maustaste auf jede und klicken Sie dann auf **Volume löschen**.

3.  Klicken Sie mit der rechten Maustaste auf die GPT-Festplatte, die Sie in eine MBR-Festplatte konvertieren möchten, und klicken Sie dann auf **in MBR-Datenträger konvertieren**.

 <a id="BKMK_CMD"></a>
#### <a name="to-change-a-gpt-disk-into-an-mbr-disk-using-a-command-line"></a>So ändern Sie mithilfe der Befehlszeile einen GPT-Datenträger in einen MBR-Datenträger

1.  Sichern Sie oder verschieben Sie alle Volumes auf dem GPT-Basisdatenträger, den Sie in einen MBR-Datenträger konvertieren möchten.

2.  Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, indem Sie mit der rechten Maustaste auf **Eingabeaufforderung** klicken und dann **Als Administrator ausführen** wählen.

3. Geben Sie `diskpart` ein. Wenn der Datenträger keine Partitionen oder Volumes enthält, fahren Sie mit Schritt6 fort.

4.  Geben Sie an der **DISKPART**-Eingabeaufforderung `list disk` ein. Notieren Sie die Datenträgernummer, die entfernt werden soll.

5.  Geben Sie an der **DISKPART**-Eingabeaufforderung `select disk <disknumber>` ein.

6.  Geben Sie an der **DISKPART**-Eingabeaufforderung `clean` ein.

> [!IMPORTANT]
> Der Befehl **Bereinigen** löscht alle Partitionen oder Volumes auf dem Datenträger.

7.  Geben Sie an der **DISKPART**-Eingabeaufforderung `convert mbr` ein.

<br />

| Wert | Beschreibung |
| --- | --- |
| <p>**list disk**</p> | <p>Zeigt eine Liste der Festplatten und deren Informationen an wie z.B. ihre Größe, die Menge an Speicherplatz, ob es sich um eine Basis- oder einen dynamischen Datenträger handelt und ob die Festplatte den Partitionsstil Master Boot Record (MBR) oder GUID-Partitionstabelle (GPT) verwendet. Die Festplatte mit einem Sternchen (*) hat den Fokus.</p> |
| <p>**Festplatte auswählen**</p> | <p>Wählt die angegebene Festplatte aus, wobei <em>disknumber</em> die Nummer der Festplatte ist, und legt den Fokus fest.</p> | <p>**Bereinigen**</p> | <p>Entfernt alle Partitionen oder Volumes vom Datenträger mit dem Fokus.</p> |
| <p>**MBR konvertieren**</p> | <p>Konvertiert einen leeren Basisdatenträger mit dem GUID-Partitionstabelle (GPT)-Partitionsstil zu einem Basisdatenträger mit Master Boot Record (MBR)-Partitionsstil.</p>

## <a name="see-also"></a>Weitere Informationen

-   [Notation der Befehlszeilensyntax](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx)


