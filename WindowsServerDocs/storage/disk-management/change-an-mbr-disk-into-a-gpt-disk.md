---
title: Ändern eines MBR-Datenträgers (Master Boot Record) in einen GPT-Datenträger (GUID Partition Table, GUID-Partitionstabelle)
description: Hier wird beschrieben, wie du einen MBR-Datenträger (Master Boot Record) in einen GPT-Datenträger (GUID Partition Table, GUID-Partitionstabelle) änderst.
ms.date: 06/07/2019
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 902a845bbe6a7e2a4d811aac0ea2990fb3557832
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2019
ms.locfileid: "66812462"
---
# <a name="convert-an-mbr-disk-into-a-gpt-disk"></a>Konvertieren eines MBR-Datenträgers in einen GPT-Datenträger

> **Gilt für:** Windows 10, Windows 8.1, Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Für MBR-Datenträger wird die standardmäßige BIOS-Partitionstabelle verwendet. GPT-Datenträger verwenden die Unified Extensible Firmware Interface (UEFI). GPT-Datenträger haben u. a. den Vorteil, dass jeder Datenträger mehr als vier Partitionen enthalten kann. GPT ist außerdem für Datenträger mit mehr als zwei Terabyte (TB) erforderlich.

Du kannst einen MBR-Datenträger in einen GPT-Datenträger ändern, sofern der Datenträger keine Partitionen oder Volumes enthält.

> [!NOTE]
> Sichere vor dem Konvertieren eines Datenträgers die darauf gespeicherten Daten, und schließe alle Programme, die auf den Datenträger zugreifen.

> [!NOTE]
> Du musst mindestens Mitglied der Gruppe **Sicherungsoperatoren** oder **Administratoren** sein, um diese Schritte ausführen zu können.

## <a name="converting-using-the-windows-interface"></a>Konvertieren mithilfe der Windows-Benutzeroberfläche

1.  Sichere oder verschiebe die Daten auf dem MBR-Basisdatenträger, den du in einen GPT-Datenträger konvertieren möchtest.

2.  Enthält der Datenträger Partitionen oder Volumes, klicke mit der rechten Maustaste auf jede Partition bzw. auf jedes Volume, und klicke dann auf **Partition löschen** bzw. **Volume löschen**.

3.  Klicke mit der rechten Maustaste auf den MBR-Datenträger, den du in einen GPT-Datenträger konvertieren möchtest, und klicke dann auf **In GPT-Datenträger konvertieren**.

## <a name="converting-using-a-command-line"></a>Konvertieren mithilfe einer Befehlszeile

Führe die folgenden Schritte aus, um einen leeren MBR-Datenträger in einen GPT-Datenträger zu konvertieren. Du kannst auch das Tool MBR2GPT.EXE verwenden, die Verwendung ist jedoch etwas kompliziert. Weitere Einzelheiten findest du unter [Konvertieren von MBR-Partitionen zu GPT](https://docs.microsoft.com/windows/deployment/mbr-to-gpt).

1.  Sichere oder verschiebe die Daten auf dem MBR-Basisdatenträger, den du in einen GPT-Datenträger konvertieren möchtest.

2.  Öffne eine Eingabeaufforderung mit erhöhten Rechten, indem du mit der rechten Maustaste auf **Eingabeaufforderung** klickst und dann **Als Administrator ausführen** auswählst.

3. Geben Sie `diskpart` ein. Wenn der Datenträger keine Partitionen oder Volumes enthält, fahre mit Schritt 6 fort.

4.  Gib an der Eingabeaufforderung **DISKPART** Folgendes ein: `list disk`. Notiere die Nummer des Datenträgers, der konvertiert werden soll.

5.  Gib an der Eingabeaufforderung **DISKPART** Folgendes ein: `select disk <disknumber>`.

6.  Gib an der Eingabeaufforderung **DISKPART** Folgendes ein: `clean`.

    > [!NOTE]
    > Der Befehl zum **Bereinigen** löscht alle Partitionen oder Volumes auf dem Datenträger.

7.  Gib an der Eingabeaufforderung **DISKPART** Folgendes ein: `convert gpt`.

| Wert  | Beschreibung  |
| ----- | ---- |
| **list disk** | Zeigt eine Liste der Festplatten und ihre Informationen an, etwa ihre Größe, den verfügbaren freien Speicherplatz, ob es sich um eine Basisfestplatte oder einen dynamischen Datenträger handelt und ob der Datenträger den MBR- oder den GPT-Partitionsstil verwendet. Der mit einem Sternchen (*) gekennzeichnete Datenträger hat den Fokus. |
| **select disk** *disknumber* | Wählt den angegebenen Datenträger aus und weist ihm den Fokus zu. (*disknumber* ist die Nummer des Datenträgers.) |
| **clean** | Entfernt alle Partitionen oder Volumes vom Datenträger mit zugewiesenem Fokus.  |
| **convert gpt**| Konvertiert eine leere Basisfestplatte mit dem MBR-Partitionsstil in eine Basisfestplatte mit dem GPT-Partitionsstil. |

## <a name="see-also"></a>Weitere Informationen

-   [Command-line syntax notation](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx) (Notation der Befehlszeilensyntax)