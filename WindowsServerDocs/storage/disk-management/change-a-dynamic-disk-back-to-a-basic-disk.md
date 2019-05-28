---
title: Zurückkonvertieren eines dynamischen Datenträgers in einen Basisdatenträger
description: Beschreibt, wie Sie einen dynamischen Datenträger in einen Basisdatenträger zurück konvertieren.
ms.date: 10/12/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: e7655ca78868d40d354b5260fa99fcfa3a21d0de
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192748"
---
# <a name="change-a-dynamic-disk-back-to-a-basic-disk"></a>Zurückkonvertieren eines dynamischen Datenträgers in einen Basisdatenträger

> **Gilt für:** Windows 10, Windows 8.1, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012

In diesem Thema wird beschrieben, wie Sie alle Daten auf einer dynamischen Festplatte löschen und diesen wieder in einen Basisdatenträger konvertieren. Dynamische Datenträger von Windows sind veraltet und nicht empfohlen, diese nicht mehr verwenden. Stattdessen empfehlen wir mithilfe von Basisdatenträger oder mithilfe der neueren [Speicherplätze](https://support.microsoft.com/help/12438/windows-10-storage-spaces) -Technologie, wenn Sie Datenträger im Speicherpool zusammen in größere Volumes möchten. Wenn Sie das Volume spiegeln möchten, von dem Windows gestartet wird, können Sie einen Hardware-RAID-Controller wie z. B. den auf Hauptplatinen verwendeten.

> [!WARNING]
> Zum Konvertieren einer dynamischen Festplatte zu einem Basisdatenträger müssen Sie alle Volumes von der Festplatte löschen und so alle Daten auf der Festplatte dauerhaft löschen. Daher sollten Sie vor der Aktion alle Dateien sichern, die Sie noch benötigen.

## <a name="changing-a-dynamic-disk-back-to-a-basic-disk"></a>Zurückkonvertieren einer dynamischen Festplatte in einen Basisdatenträger

-   [Mithilfe der Windows-Benutzeroberfläche](#to-change-a-dynamic-disk-back-to-a-basic-disk-using-the-windows-interface)
-   [Über die Befehlszeile](#to-change-a-dynamic-disk-back-to-a-basic-disk-using-a-command-line)

> [!NOTE]
> Sie müssen mindestens ein Mitglied der Gruppe **Sicherungsoperatoren** or **Administratoren** sein, um diese Schritte durchzuführen.

#### <a name="to-change-a-dynamic-disk-back-to-a-basic-disk-using-the-windows-interface"></a>So konvertieren Sie mithilfe der Windows-Benutzeroberfläche einen dynamischen Datenträger wieder in einen Basisdatenträger

1.  Sichern Sie alle Volumes auf der Festplatte, den Sie von einem dynamischen in einen Basisdatenträger konvertieren möchten.

2.  Klicken Sie mit der rechten Maustaste in der Datenträgerverwaltung auf jedes Volume der dynamischen Festplatte, die Sie in einen Basisdatenträger konvertieren möchten, und klicken Sie dann auf **Volume löschen** für jedes Volume auf der Festplatte.

3.  Wenn alle Volumes auf der Festplatte gelöscht wurden, klicken Sie mit der rechten Maustaste auf die Festplatte, und klicken Sie dann auf **Konvertieren in Basisdatenträger**.

#### <a name="to-change-a-dynamic-disk-back-to-a-basic-disk-using-a-command-line"></a>So konvertieren Sie mithilfe der Befehlszeile einen dynamischen Datenträger wieder in einen Basisdatenträger

1.  Sichern Sie alle Volumes auf der Festplatte, den Sie von einem dynamischen in einen Basisdatenträger konvertieren möchten.

2.  Öffnen Sie eine Eingabeaufforderung, und geben Sie `diskpart` ein.

3.  Geben Sie an der **DISKPART**-Eingabeaufforderung `list disk` ein. Notieren Sie die Anzahl der Festplatten, die Sie in einen Basisdatenträger konvertieren möchten.

4.  Geben Sie an der **DISKPART**-Eingabeaufforderung `select disk <disknumber>` ein.

5.  Geben Sie an der **DISKPART**-Eingabeaufforderung `detail disk <disknumber>` ein.

6.  Geben Sie für jedes Volume auf der Festplatte bei der **DISKPART**-Eingabeaufforderung `select volume= <volumenumber>` und dann `delete volume` ein.

7.  Geben Sie bei der **DISKPART**-Eingabeaufforderung `select disk <disknumber>` ein, und geben Sie die Festplattennummer der Festplatte an, die Sie in einen Basisdatenträger konvertieren möchten.

8.  Geben Sie an der **DISKPART**-Eingabeaufforderung `convert basic` ein.
 
<br /> <br />

| Wert  | Beschreibung |
| --- |---|
| <p>**Liste Datenträger**</p>                         | <p>Zeigt eine Liste der Festplatten und deren Informationen an wie z. B. ihre Größe, die Menge an Speicherplatz, ob es sich um einen dynamischen Datenträger handelt und ob die Festplatte den Partitionsstil Master Boot Record (MBR) oder GUID-Partitionstabelle (GPT) verwendet. Die Festplatte mit einem Sternchen (*) hat den Fokus.</p> |
| <p>**Wählen Sie Datenträger** <em>Disknumber</em></p>   | <p>Wählt die angegebene Festplatte aus, wobei <em>disknumber</em> die Nummer der Festplatte ist, und legt den Fokus fest.</p>  |
| <p>**Detail Datenträger** <em>Disknumber</em></p>   | <p>Zeigt die Eigenschaften des ausgewählten Datenträgers und das Volume auf der Festplatte an.</p>  |
| <p>**Wählen Sie Volume** <em>Disknumber</em></p> | <p>Wählt das angegebene Volume aus, wobei <em>disknumber</em> die Anzahl der Volumes ist, und legt den Fokus fest. Wenn kein Volume angegeben ist, zeigt der Befehl **Auswählen** die Liste des aktuellen Volumes mit Fokus an. Das Volume kann durch die Anzahl, den Laufwerkbuchstaben oder den Bereitstellungspunkt angegeben werden. Bei einer Basisfestplatte erhält durch das Auswählen einer Festplatte auch die entsprechende Partition den Fokus.</p> |
| <p>**Löschen von volume**</p>                     | <p>Hiermit wird das ausgewählte Volume gelöscht. Systemvolume, Startvolume sowie das Volume, das die aktive Auslagerungsdatei oder das Absturzabbild (Speicherabbild) enthält, können nicht gelöscht werden.</p> |
| <p>**grundlegende konvertieren**</p> | <p>Konvertieren eines Basisdatenträgers in einen dynamischen Datenträger.</p>  |

## <a name="additional-considerations"></a>Weitere Aspekte

-   Die Festplatte darf keine Volumes oder Daten enthalten, wenn Sie ihn in einen Basisdatenträger zurückkonvertieren möchten. Wenn Sie Ihre Daten beibehalten möchten, sichern Sie oder verschieben Sie diese auf ein anderes Volume, bevor Sie die Festplatte in einen Basisdatenträger konvertieren.
-   Wenn Sie einen dynamischen Datenträger wieder in einen Basisdatenträger konvertieren, können Sie nur Partitionen und logische Laufwerke auf der Festplatte erstellen.

## <a name="see-also"></a>Siehe auch

-   [Notation der Befehlszeilensyntax](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx)


