---
title: Ändern eines GPT-Datenträgers (GUID Partition Table, GUID-Partitionstabelle) in einen MBR-Datenträger (Master Boot Record)
description: Hier wird beschrieben, wie du einen GPT-Datenträger (GUID Partition Table, GUID-Partitionstabelle) in einen MBR-Datenträger (Master Boot Record) änderst.
ms.date: 06/19/2018
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 5a387f7672fd04917e8c3e76543cba73f7195b42
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966072"
---
# <a name="convert-a-gpt-disk-into-an-mbr-disk"></a>Konvertieren eines GPT-Datenträgers in einen MBR-Datenträger

> **Gilt für:** Windows 10, Windows 8.1, Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Für MBR-Datenträger wird die standardmäßige BIOS-Partitionstabelle verwendet. GPT-Datenträger verwenden die Unified Extensible Firmware Interface (UEFI). MBR-Datenträger unterstützen maximal vier Partitionen auf jedem Datenträger. Die MBR-Partitionsmethode wird für Datenträger mit mehr als zwei Terabyte (TB) nicht empfohlen.

Du kannst einen GPT-Datenträger in einen MBR-Datenträger ändern, sofern der Datenträger leer ist und keine Volumes enthält.

> [!NOTE]
> Sichere vor dem Konvertieren eines Datenträgers die darauf gespeicherten Daten, und schließe alle Programme, die auf den Datenträger zugreifen.

> [!NOTE]
> Du musst mindestens Mitglied der Gruppe **Sicherungsoperatoren** oder **Administratoren** sein, um diese Schritte ausführen zu können.

## <a name="converting-using-the-windows-interface"></a>Konvertieren mithilfe der Windows-Benutzeroberfläche

1.  Sichere oder verschiebe alle Volumes auf dem GPT-Basisdatenträger, den du in einen MBR-Datenträger konvertieren möchtest.

2.  Enthält der Datenträger Partitionen oder Volumes, klicke mit der rechten Maustaste auf jede Partition bzw. auf jedes Volume, und klicke dann auf **Volume löschen**.

3.  Klicke mit der rechten Maustaste auf den GPT-Datenträger, den du in einen MBR-Datenträger konvertieren möchtest, und klicke dann auf **In MBR-Datenträger konvertieren**.

## <a name="converting-using-a-command-line"></a>Konvertieren mithilfe einer Befehlszeile

1.  Sichere oder verschiebe alle Volumes auf dem GPT-Basisdatenträger, den du in einen MBR-Datenträger konvertieren möchtest.

2.  Öffne eine Eingabeaufforderung mit erhöhten Rechten, indem du mit der rechten Maustaste auf **Eingabeaufforderung** klickst und dann **Als Administrator ausführen** auswählst.

3. Geben Sie `diskpart`ein. Wenn der Datenträger keine Partitionen oder Volumes enthält, fahre mit Schritt 6 fort.

4.  Gib an der Eingabeaufforderung **DISKPART** Folgendes ein: `list disk`. Notiere die Nummer des Datenträgers, der gelöscht werden soll.

5.  Gib an der Eingabeaufforderung **DISKPART** Folgendes ein: `select disk <disknumber>`.

6.  Gib an der Eingabeaufforderung **DISKPART** Folgendes ein: `clean`.

    > [!IMPORTANT]
    > Der Befehl zum **Bereinigen** löscht alle Partitionen oder Volumes auf dem Datenträger.

7.  Gib an der Eingabeaufforderung **DISKPART** Folgendes ein: `convert mbr`.

|                Value                  |      Beschreibung   |
| ------------------------------------- | -----------------  |
|  <strong>list disk</strong>  | Zeigt eine Liste der Festplatten und ihre Informationen an, etwa ihre Größe, den verfügbaren freien Speicherplatz, ob es sich um eine Basisfestplatte oder einen dynamischen Datenträger handelt und ob der Datenträger den MBR- oder den GPT-Partitionsstil verwendet. Der mit einem Sternchen (\*) gekennzeichnete Datenträger hat den Fokus. |
| <strong>select disk</strong> |                                                                                                          Wählt den angegebenen Datenträger aus und weist ihm den Fokus zu. (<em>disknumber</em> ist die Nummer des Datenträgers.)                                                                                                           |
| <strong>convert mbr</strong> |                                                                               Konvertiert eine leere Basisfestplatte mit dem GPT-Partitionsstil in eine Basisfestplatte mit dem MBR-Partitionsstil.                                                                                |

## <a name="see-also"></a>Weitere Informationen

-   [Command-line syntax notation](/previous-versions/orphan-topics/ws.11/cc742449(v=ws.11)) (Notation der Befehlszeilensyntax)
