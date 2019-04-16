---
title: Verkleinern eines Basisvolumes
description: Dieser Artikel beschreibt das Verkleinern eines Basisvolumes
ms.date: 10/12/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: e54632b78fd67a65b51147323565130881d8d81b
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="shrink-a-basic-volume"></a>Verkleinern eines Basisvolumes

> **Gilt für**: Windows 10, Windows 8.1, Windows Server (Semi-Annual Channel), Windows Server 10, Windows Server8.1 R2, Windows Server 2016, Windows Server2012 R2, Windows Server 2012

Sie können den von primären Partitionen und logischen Laufwerken verwendeten Speicherplatz reduzieren, indem Sie sie auf angrenzenden, zusammenhängenden Speicherplatz auf derselben Festplatte verkleinern. Wenn Sie beispielsweise feststellen, dass Sie eine weitere Partition benötigen, jedoch nicht über weitere Datenträger verfügen, können Sie die vorhandene Partition vom Ende des Volumes verkleinern, um neuen, verfügbaren Speicherplatz für eine neue Partition zu erstellen. Der Verkleinerungsvorgang kann durch das Vorhandensein bestimmter Dateitypen blockiert werden. Weitere Informationen finden Sie unter [Weitere Überlegungen](#addcon). 

Wenn Sie eine Partition verkleinern, werden alle normalen Dateien automatisch auf den Datenträger verschoben, um neue, verfügbare Speicherplätze zu erstellen. Es ist nicht erforderlich, die Festplatte zu verkleinern, um die Partition neu zu formatieren.

> [!CAUTION]
> Wenn die Partition eine unformatierte Partition ist (d.h. ohne Dateisystem), die Daten (z.B. eine Datenbankdatei) enthält, kann das Verkleinern der Partition die Daten löschen.

## <a name="shrinking-a-basic-volume"></a>Verkleinern eines Basisvolumes

-   [Verwenden der Windows-Benutzeroberfläche](#BKMK_WINUI)
-   [Mit einer Befehlszeile](#BKMK_CMD)

> [!NOTE]
> Sie müssen mindestens ein Mitglied der Gruppe **Sicherungsoperatoren** or **Administratoren** sein, um diese Schritte durchzuführen.

<a id="BKMK_WINUI"></a>
#### <a name="to-shrink-a-basic-volume-using-the-windows-interface"></a>So verkleinern Sie ein Basisvolume mithilfe der Windows-Benutzeroberfläche

1.  Klicken Sie mit der rechten Maustaste in der Datenträgerverwaltung auf das Basisvolume, das Sie verkleinern möchten.

2.  Klicken Sie auf **Volume verkleinern**.

3.  Befolgen Sie die Anweisungen auf dem Bildschirm.

<br />

> [!NOTE]
> Sie können nur Basisvolumes verkleinern, auf denen kein Dateisystem vorhanden ist oder die ein NTFS-Dateisystem verwenden.

<a id="BKMK_CMD"></a>
#### <a name="to-shrink-a-basic-volume-using-a-command-line"></a>So verkleinern Sie ein Baisisvolume mithilfe einer Befehlszeile

1.  Öffnen Sie eine Eingabeaufforderung, und geben Sie `diskpart` ein.

2.  Geben Sie an der **DISKPART**-Eingabeaufforderung `list volume` ein. Notieren Sie sich die Nummer des einfachen Volumes, das Sie verkleinern möchten.

3.  Geben Sie an der **DISKPART**-Eingabeaufforderung `select volume <volumenumber>` ein. Wählen Sie das einfache Volume *volumenumber*, das Sie verkleinern möchten.

4.  Geben Sie an der **DISKPART**-Eingabeaufforderung `shrink [desired=<desiredsize>] [minimum=<minimumsize>]` ein. Verkleinert das ausgewählte Volume auf *desiredsize* in Megabyte (MB), wenn möglich oder zu *Minimumsize*, wenn *desiredsize* zu groß ist.

<br />

| Wert | Beschreibung|
|---|---|
| <p>**List volume**</p> | <p>Zeigt eine Liste der Basis- und dynamischen Volumes auf allen Festplatten an.</p>|
| <p>**Volume auswählen**</p> | <p>Wählt das angegebene Volume aus, wobei <em>volumenumber</em> die Anzahl der Volumes ist, und legt den Fokus fest. Wenn kein Volume angegeben ist, zeigt der Befehl **Auswählen** die Liste des aktuellen Volumes mit Fokus an. Das Volume kann durch die Anzahl, den Laufwerkbuchstaben oder den Bereitstellungspunkt angegeben werden. Bei einer Basisfestplatte erhält durch das Auswählen einer Festplatte auch die entsprechende Partition den Fokus.</p> |
| <p>**Verkleinern**</p> | <p>Verkleinert das Volume mit dem Fokus, verfügbaren Speicherplatz zu erstellen. Es tritt kein Datenverlust auf. Wenn die Partition nicht verschiebbare Dateien enthält (z.B. die Auslagerungsdatei oder den Schattenkopiespeicherbereich), wird das Volume bis zu dem Punkt verkleinert, wo sich die Systemdateien befinden. |
| <p>**gewünscht=** <em>Desiredsize</em></p> | <p>Der Speicherplatz in Megabyte, um die aktuelle Partition wiederherzustellen.</p> |
| <p>**minimal=** <em>Minimumsize</em></p> | <p>Der minimale Speicherplatz in Megabyte, um die aktuelle Partition wiederherzustellen. Wenn Sie keine gewünschte oder minimale Größe angeben, wird der Befehl die maximale Menge an Speicherplatz freigeben.</p> 

<a id="addcon"></a>

## <a name="additional-considerations"></a>Weitere Überlegungen

-   Wenn Sie eine Partition verkleinern, können bestimmte Dateien (z.B. die Auslagerungsdatei oder der Schattenkopiespeicherbereich) nicht automatisch verschoben werden, und Sie können den zugewiesenen Speicherplatz auf den Punkt verkleinern, an dem sich die Systemdateien befinden. Wenn der Verkleinerungsvorgang fehlschlägt, überprüfen Sie das Anwendungsprotokoll für Ereignis 259, das die nicht verschiebbare Datei identifiziert. Wenn Sie die Cluster kennen, denen die Datei zugeordnet ist, die den Verkleinerungsvorgang verhindert, können Sie auch den Befehl **Fsutil** bei der Eingabeaufforderung (geben Sie **fsutil volume querycluster /?** ein) verwenden. Wenn Sie den **querycluster**-Parameter verwenden, identifiziert der Ausgabebefehl die nicht verschiebbare Datei, die den Verkleinerungsvorgang verhindert.
In einigen Fällen können Sie die Datei vorübergehend verschieben. Wenn Sie beispielsweise die Partition weiter verkleinern müssen, können Sie die Systemsteuerung verwenden, um die Auslagerungsdatei oder die gespeicherten Schattenkopien auf einen anderen Datenträger zu verschieben, oder um die gespeicherten Schattenkopien zu löschen, das Volume zu verkleinern und die Auslagerungsdatei wieder auf den Datenträger zu verschieben. Wenn die Anzahl der entdeckten beschädigten Cluster von der dynamischen erneuten Zuordnung zu hoch ist, kann die Partition nicht verkleinert werden. In diesem Fall sollten Sie die Daten verschieben und einen Austausch der Festplatte in Betracht ziehen.

-  Verwenden Sie keine Kopie auf Blockebene zum Übertragen der Daten. Dadurch wird auch die fehlerhafte Sektorentabelle kopiert, und der neue Datenträger behandelt dieselben Sektoren als fehlerhaft, obwohl sie normal sind.

-   Sie können primäre Partitionen und logische Laufwerken auf unformatierten Partitionen (d.h. ohne Dateisystem) oder Partitionen mit NTFS-Dateisystem verkleinern.

## <a name="see-also"></a>Weitere Informationen

-   [Verwalten von Basisvolumes](manage-basic-volumes.md)