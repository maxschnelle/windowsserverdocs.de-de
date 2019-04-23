---
title: Erweitern eines Basisvolume
description: In diesem Artikel wird beschrieben, wie das Hinzufügen von Speicherplatz auf primären und logischen Laufwerken ein Basisvolume erweitert
ms.date: 10/12/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 29b7b61f7edc20edda7bc18b82db17447badc0f2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834251"
---
# <a name="extend-a-basic-volume"></a>Erweitern eines Basisvolume

> **Gilt für:** Windows 10, Windows 8.1, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012

Sie können vorhandenen primären Partitionen und logischen Laufwerken mehr Platz hinzufügen, indem sie diese auf den angrenzenden, verfügbaren Speicherplatz auf dem gleichen Datenträger erweitern. Wenn ein Basisvolume zu erweitern, muss es unformatierte (nicht mit einem Dateisystem formatiert) oder mit dem NTFS-Dateisystem formatiert sein. Sie können ein logisches Laufwerk innerhalb einem fortlaufendem, freiem Speicherplatz in der erweiterten Partition erweitern, die es enthält. Wenn Sie ein logisches Laufwerk über den freien Speicherplatz in der erweiterten Partition erweitern, erhöht die erweiterte Partition die Größe, um das logische Laufwerk zu enthalten.

Für logische Laufwerke und Start- oder System-Volumes, können Sie das Volume nur in fortlaufendem Speicherplatz erweitern und auch nur dann, wenn der Datenträger auf einen dynamischen Datenträger aktualisiert werden kann. Bei anderen Volumes können Sie das Volume in einen nicht zusammenhängenden Speicherplatz erweitern, jedoch werden Sie aufgefordert, den Datenträger in einen dynamischen Datenträger zu konvertieren.

## <a name="extending-a-basic-volume"></a>Erweitern eines Basisvolumes

-   [Mithilfe der Windows-Benutzeroberfläche](#BKMK_WINUI)
-   [Über die Befehlszeile](#BKMK_CMD)

<a href="" id="BKMK_WINUI"></a>
#### <a name="to-extend-a-basic-volume-using-the-windows-interface"></a>So erweitern Sie ein Basisvolume mithilfe der Windows-Benutzeroberfläche

1.  Klicken Sie mit der rechten Maustaste in der Datenträgerverwaltung auf das Basisvolume, das Sie erweitern möchten.

2.  Klicken Sie auf **Volume erweitern**.

3.  Befolgen Sie die Anweisungen auf dem Bildschirm.

<a href="" id="BKMK_CMD"></a>
#### <a name="to-extend-a-basic-volume-using-a-command-line"></a>So erweitern Sie ein Baisisvolume mithilfe einer Befehlszeile

1.  Öffnen Sie eine Eingabeaufforderung, und geben Sie `diskpart` ein.

2.  Geben Sie an der **DISKPART**-Eingabeaufforderung `list volume` ein. Notieren Sie das Basisvolume, das Sie erweitern möchten.

3.  Geben Sie an der **DISKPART**-Eingabeaufforderung `select volume <volumenumber>` ein. Dadurch wird das Basisvolume *volumenumber* ausgewählt, das Sie in zusammenhängenden, leeren Speicherplatz auf derselben Festplatte erweitern möchten.

4.  Geben Sie an der **DISKPART**-Eingabeaufforderung `extend [size=<size>]` ein. Dies erweitert das ausgewählte Volume in der *Größe* in Megabyte (MB).

<br />

| Wert | Beschreibung |
| --- | --- |
| <p>**Liste volume**</p> | <p>Zeigt eine Liste der Basis- und dynamischen Volumes auf allen Festplatten an.</p> |
| <p>**Wählen Sie volume**</p> | <p>Wählt das angegebene Volume aus, wobei <em>volumenumber</em> die Anzahl der Volumes ist, und legt den Fokus fest. Wenn kein Volume angegeben ist, zeigt der Befehl **Auswählen** die Liste des aktuellen Volumes mit Fokus an. Das Volume kann durch die Anzahl, den Laufwerkbuchstaben oder den Bereitstellungspunkt angegeben werden. Bei einer Basisfestplatte erhält durch das Auswählen einer Festplatte auch die entsprechende Partition den Fokus.</p> |
| <p>**extend**</p> | <p><ul><li>Erweitert das Volume mit dem Fokus auf den nächsten fortlaufenden, nicht zugewiesenen Speicherplatz. Für Basisvolumes muss der nicht zugewiesene Speicherplatz auf dem gleichen Datenträger sein und der noch nicht zugeordnete Speicherbereich muss auf die Partition mit dem Fokus folgen (einen höheren Sektoren-Offsetwert haben als diese Partition). Ein einfaches dynamisches Volume oder ein übergreifendes Volume kann auf einen leeren Bereich auf den dynamischen Datenträgern erweitert werden. Mit diesem Befehl können Sie einem vorhandenen Volume in einen neu erstellten Speicherplatz erweitern.</p></li ><p><li>Wurde die Partition zuvor mit dem NTFS-Dateisystem formatiert, wird das Dateisystem automatisch so erweitert, dass es die größere Partition belegt werden. Es tritt kein Datenverlust auf. Wurde die Partition zuvor mit einem anderen Dateisystem als NTFS formatiert, schlägt der Befehl fehl, und die Partition wird nicht geändert.</p></li></ul>|
| <p>**size=** <em>size</em></p> | <p>Der Speicherplatz in Megabyte (MB), der zur aktuellen Partition hinzugefügt wird. Wenn Sie keine Größe festlegen, wird der Datenträger so erweitert, dass er den gesamten nächsten fortlaufenden Speicherplatz einnimmt, der nicht zugeordnet ist.</p> |

## <a name="additional-considerations"></a>Weitere Aspekte

-   Wenn der Datenträger keine Start- oder System-Partitionen enthält, erweitern Sie das Volume in anderen Nicht-Boot oder Nicht-System-Datenträger. Der Datenträger wird allerdings in einen dynamischen Datenträger konvertiert (wenn er aktualisiert werden kann).

## <a name="see-also"></a>Siehe auch

-   [Notation der Befehlszeilensyntax](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx)


