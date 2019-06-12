---
title: Einem Laufwerk einen Ordnerpfad mit Bereitstellungspunkt zuweisen
description: In diesem Artikel wird beschrieben, wie Sie einem Laufwerk einen Ordnerpfad mit Bereitstellungspunkt zuweisen.
keywords: Virtualisierung, Sicherheit, Schadsoftware
ms.date: 06/07/2019
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: d09024b3c7f7a1e55c9e9c2ece56e037fe7e16f2
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812494"
---
# <a name="assign-a-mount-point-folder-path-to-a-drive"></a>Einem Laufwerk einen Ordnerpfad mit Bereitstellungspunkt zuweisen

> **Gilt für:** Windows 10, Windows 8.1, WindowsServer (Halbjährlicher Kanal), WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012

Verwenden Sie die Datenträgerverwaltung, um einem Laufwerk einen Ordnerpfad mit Bereitstellungspunkt zuzuweisen. Ein Ordnerpfad mit Bereitstellungspunkt ist nur bei leeren Ordnern mit Basis- oder dynamischem NTFS-Volume verfügbar.

## <a name="assigning-a-mount-point-folder-path-to-a-drive"></a>So weisen Sie einem Laufwerk einen Ordnerpfad mit Bereitstellungspunkt zu

> [!NOTE]
> Sie müssen mindestens ein Mitglied der Gruppe **Sicherungsoperatoren** or **Administratoren** sein, um diese Schritte durchzuführen.

#### <a name="to-assign-a-mount-point-folder-path-to-a-drive-by-using-the-windows-interface"></a>Einen Pfad des Volumebereitstellungspunkts Ordner auf einem Laufwerk zugewiesen werden, mithilfe der Windows-Benutzeroberfläche

1.  Klicken Sie mit der rechten Maustaste in der Datenträgerverwaltung die Partition oder das Volume, in denen der Ordnerpfad mit Bereitstellungspunkt erstellt werden soll. 
2. Klicken Sie auf **Laufwerkbuchstaben und -pfade ändern...** und dann auf **Hinzufügen**. 
3. Klicken Sie auf **In folgendem leeren NTFS-Ordner bereitstellen**.
4. Geben Sie den Pfad zu einem leeren Ordner auf einem NTFS-Volume an, oder klicken Sie auf **Durchsuchen**, um ihn zu suchen.

#### <a name="to-assign-a-mount-point-folder-path-to-a-drive-using-a-command-line"></a>So weisen Sie einen Ordnerpfad mit Bereitstellungspunkt mithilfe einer Befehlszeile zu

1.  Öffnen Sie eine Eingabeaufforderung, und geben Sie `diskpart` ein.

2.  Geben Sie an der **DISKPART**-Eingabeaufforderung `list volume` ein und notieren Sie sich die Volumenummer, die Sie dem Pfad zuweisen möchten.

3.  Geben Sie an der **DISKPART**-Eingabeaufforderung `select volume <volumenumber>` ein. 

4. Wählen Sie das einfache Volume *volumenumber*, dem Sie den Pfad zuweisen möchten.

5.  Geben Sie an der **DISKPART**-Eingabeaufforderung `assign [mount=<path>]` ein.

#### <a name="to-remove-a-mount-point-folder-path-to-a-drive"></a>So entfernen Sie einem Laufwerk einen Ordnerpfad mit Bereitstellungspunkt

-   Um einen Ordnerpfad mit Bereitstellungspunkt zu entfernen, klicken Sie darauf und dann auf **Entfernen**.

| Wert | Beschreibung |
| --- | --- |
| **Liste volume** | Zeigt eine Liste der Basis- und dynamischen Volumes auf allen Festplatten an. |
| **Wählen Sie volume**        | Wählt das angegebene Volume aus, wobei <em>volumenumber</em> die Anzahl der Volumes ist, und legt den Fokus fest. Wenn kein Volume angegeben ist, zeigt der Befehl **Auswählen** die Liste des aktuellen Volumes mit Fokus an. Das Volume kann durch die Anzahl, den Laufwerkbuchstaben oder den Bereitstellungspunkt angegeben werden. Bei einer Basisfestplatte erhält durch das Auswählen einer Festplatte auch die entsprechende Partition den Fokus.|
| **assign** | <ul><li> Weist dem Volume mit Fokus einen Laufwerkbuchstaben oder einen Ordnerpfad mit Bereitstellungspunkt zu. Wenn kein Laufwerkbuchstaben oder einen Ordnerpfad mit Bereitstellungspunkt angegeben ist, wird der Nächste verfügbare Laufwerkbuchstabe zugewiesen. Wenn der Laufwerksbuchstaben oder Ordnerpfad mit Bereitstellungspunkt bereits verwendet wird, wird ein Fehler generiert.</li>  <li>Der Befehl **Zuweisen** kann dazu verwendet werden, den Laufwerkbuchstaben zu ändern, der einem austauschbaren Laufwerk zugeordnet ist.</li> <li> Sie können Startvolumes oder Volumes, die die Auslagerungsdatei enthalten, keine Laufwerkbuchstaben zuweisen. Darüber hinaus können Sie einer Originalgerätehersteller (OEM)-Partition, EFI-Systempartition oder einer GPT-Partition sowie einer einfachen Datenpartition keinen Laufwerkbuchstaben zuweisen.</li></ul> |
| **mount=** <em>path</em> | Gibt einen leeren, vorhandenen NTFS-Ordner an, in dem das bereitgestellte Laufwerk gespeichert werden soll.  |

## <a name="additional-considerations"></a>Weitere Aspekte

-   Wenn Sie einen lokalen Computer oder einen Remotecomputer verwalten, können Sie die NTFS-Ordner auf diesem Computer durchsuchen.
-   Ein Ordnerpfad mit Bereitstellungspunkt ist nur bei leeren Ordnern mit Basis- oder dynamischem NTFS-Volume verfügbar.
-   Um einen Ordnerpfad mit Bereitstellungspunkt zu ändern, entfernen Sie diesen und erstellen Sie einen neuen Ordnerpfad mit einem neuen Speicherort. Der Ordnerpfad mit Bereitstellungspunkt kann nicht direkt geändert werden.
-   Wenn Sie einem Laufwerkt einen Ordnerpfad mit Bereitstellungspunkt zuordnen möchten, verwenden Sie **Ereignisanzeige** zum Überprüfen des Systemprotokolls nach einem Cluster Service-Fehler oder Warnungen, die einen „Ordnerpfad mit Bereitstellungspunkt”-Fehler anzeigen. Diese Fehler sind: **ClusSvc** in der Spalte **Quelle** und **physische Datenträgerressourcen** in der Spalte **Kategorie**.
-   Sie können auch ein bereitgestelltes Laufwerk mit dem Befehl [mountvol](https://go.microsoft.com/fwlink/?linkid=64111) erstellen.

## <a name="see-also"></a>Siehe auch
-   [Notation der Befehlszeilensyntax](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx)


