---
title: Erweitern eines Basisvolumes
description: In diesem Artikel erfährst du, wie du Speicherplatz auf primären und logischen Laufwerken hinzufügst, um ein Basisvolume zu erweitern.
ms.date: 06/07/2019
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 4cad773746ae64a2244178be83e4d59c7c44b6a7
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2019
ms.locfileid: "66812435"
---
# <a name="extend-a-basic-volume"></a>Erweitern eines Basisvolumes

> **Gilt für:** Windows 10, Windows 8.1, Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Du kannst vorhandenen primären Partitionen und logischen Laufwerken mehr Speicherplatz hinzufügen, indem du sie auf angrenzenden, verfügbaren Speicherplatz auf dem gleichen Datenträger erweiterst. Um ein Basisvolume erweitern zu können, muss es entweder unformatiert (nicht mit einem Dateisystem formatiert) oder mit dem NTFS-Dateisystem formatiert sein. Ein logisches Laufwerk kann innerhalb des zusammenhängenden freien Speicherplatzes in der erweiterten Partition erweitert werden, die es enthält. Wenn du ein logisches Laufwerk über den freien Speicherplatz hinaus erweiterst, der in der erweiterten Partition verfügbar ist, wird die erweiterte Partition vergrößert, um das logische Laufwerk aufnehmen zu können.

Bei logischen Laufwerken sowie bei Start- oder Systemvolumes kann das Volume nur in zusammenhängenden Speicherplatz erweitert werden, und das auch nur, wenn für den Datenträger ein Upgrade auf einen dynamischen Datenträger durchgeführt werden kann. Bei anderen Volumes kannst du das Volume in nicht zusammenhängenden Speicherplatz erweitern. Dabei wirst du allerdings aufgefordert, den Datenträger in einen dynamischen Datenträger zu konvertieren.

## <a name="extending-a-basic-volume"></a>Erweitern eines Basisvolumes

#### <a name="to-extend-a-basic-volume-using-the-windows-interface"></a>So erweiterst du ein Basisvolume über die Windows-Benutzeroberfläche

1. Klicke in der Datenträgerverwaltung mit der rechten Maustaste auf das Basisvolume, das du erweitern möchtest.

2. Klicke auf **Volume erweitern**.

3. Befolgen Sie die Anweisungen auf dem Bildschirm.

#### <a name="to-extend-a-basic-volume-using-a-command-line"></a>So erweiterst du ein Basisvolume mithilfe einer Befehlszeile

1. Öffnen Sie eine Eingabeaufforderung, und geben Sie `diskpart` ein.

2. Gib an der Eingabeaufforderung **DISKPART** Folgendes ein: `list volume`. Notiere dir das Basisvolume, das du erweitern möchtest.

3. Gib an der Eingabeaufforderung **DISKPART** Folgendes ein: `select volume <volumenumber>`. Dadurch wird das Basisvolume *volumenumber* ausgewählt, das du in zusammenhängenden leeren Speicherplatz auf dem gleichen Datenträger erweitern möchtest.

4. Gib an der Eingabeaufforderung **DISKPART** Folgendes ein: `extend [size=<size>]`. Dadurch wird das ausgewählte Volume um *size* Megabyte (MB) erweitert.

| Wert | Beschreibung |
| --- | --- |
| **list volume** | Zeigt eine Liste der Basisvolumes und dynamischen Volumes auf allen Datenträgern an. |
| **select volume** | Wählt das angegebene Volume aus und weist ihm den Fokus zu. (<em>volumenumber</em> ist die Nummer des Volumes.) Ohne Volumeangabe führt der Befehl **select** die aktuellen Volumes mit Fokus auf. Das Volume kann anhand von Nummer, Laufwerkbuchstabe oder Bereitstellungspunktpfad angegeben werden. Wenn bei einer Basisfestplatte ein Volume ausgewählt wird, erhält die entsprechende Partition den Fokus. |
| **extend** | <ul><li>Erweitert das Volume, das den Fokus hat, auf den nächsten zusammenhängenden verfügbaren Speicher. Bei Basisvolumes muss sich der verfügbare Speicher auf dem gleichen Datenträger befinden wie die Partition mit dem Fokus, und er muss auf die Partition mit dem Fokus folgen (also einen höheren Sektor-Offset besitzen). Ein einfaches dynamisches Volume oder ein übergreifendes Volume kann auf einen leeren Bereich auf einem beliebigen dynamischen Datenträger erweitert werden. Mit diesem Befehl kannst du ein vorhandenes Volume auf neu erstellten Speicherplatz erweitern.</li ><li>Wenn die Partition zuvor mit dem NTFS-Dateisystem formatiert wurde, wird das Dateisystem automatisch erweitert, um die größere Partition zu belegen. Es gehen keine Daten verloren. Wurde die Partition zuvor mit einem NTFS-fremden Dateisystem formatiert, ist der Befehl nicht erfolgreich, und die Partition wird nicht geändert.</li></ul> |
| **size=** <em>size</em> | Der Speicherplatz in Megabyte (MB), der der aktuellen Partition hinzugefügt werden soll. Ohne Größenangabe wird der Datenträger so erweitert, dass er den gesamten zusammenhängenden verfügbaren Speicher einnimmt. |

## <a name="additional-considerations"></a>Weitere Aspekte

-   Wenn der Datenträger keine Start- oder Systempartitionen enthält, kannst du das Volume auf andere Datenträger erweitern, bei denen es sich nicht um Start- oder Systemdatenträger handelt. Der Datenträger wird dann allerdings in einen dynamischen Datenträger konvertiert (sofern ein entsprechendes Upgrade möglich ist).

## <a name="see-also"></a>Weitere Informationen

-   [Command-line syntax notation](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx) (Notation der Befehlszeilensyntax)
