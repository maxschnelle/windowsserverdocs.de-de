---
title: Zuweisen eines Ordnerpfads mit Bereitstellungspunkt zu einem Laufwerk
description: In diesem Artikel wird beschrieben, wie du einem Laufwerk einen Ordnerpfad mit Bereitstellungspunkt (anstelle eines Laufwerkbuchstaben) zuweist.
ms.date: 06/07/2020
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 9757f5f5f68eea0fc1d468a8d8e6fd341e2ecc6a
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475437"
---
# <a name="mount-a-drive-in-a-folder"></a>Bereitstellen eines Laufwerks in einem Ordner

> **Gilt für:** Windows 10, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sie können die Datenträgerverwaltung verwenden, um ein Laufwerk in einem Ordner statt einem Laufwerksbuchstaben bereitzustellen (zugänglich zu machen), wenn Sie dies wünschen. Dadurch wird das Laufwerk nur als ein weiterer Ordner angezeigt. Sie können Laufwerke nur in leeren Ordnern auf Basis- oder dynamischen NTFS-Volumes bereitstellen.

## <a name="mounting-a-drive-in-an-empty-folder"></a>Bereitstellen eines Laufwerks in einem leeren Ordner

> [!NOTE]
> Du musst mindestens Mitglied der Gruppe **Sicherungsoperatoren** oder **Administratoren** sein, um diese Schritte ausführen zu können.

### <a name="to-mount-a-drive-in-an-empty-folder-by-using-the-windows-interface"></a>So stellen Sie ein Laufwerk mithilfe der Windows-Benutzeroberfläche in einem leeren Ordner bereit

1.  Klicken Sie in der Datenträgerverwaltung mit der rechten Maustaste auf die Partition oder das Volume, in der bzw. auf dem sich der Ordner befindet, in dem Sie das Laufwerk bereitstellen möchten.
2. Klicke auf **Laufwerkbuchstaben und -pfade ändern...** und dann auf **Hinzufügen**.
3. Klicke auf **In folgendem leeren NTFS-Ordner bereitstellen**.
4. Gib den Pfad zu einem leeren Ordner auf einem NTFS-Volume an, oder klicke auf **Durchsuchen**, um ihn zu suchen.

### <a name="to-mount-a-drive-in-an-empty-folder-using-a-command-line"></a>So stellen Sie ein Laufwerk mithilfe einer Befehlszeile in einem leeren Ordner bereit

1.  Öffnen Sie eine Eingabeaufforderung, und geben Sie `diskpart` ein.

2.  Gib an der **DISKPART**-Eingabeaufforderung `list volume` ein, und notiere die Volumenummer, der du den Pfad zuweisen möchtest.

3.  Geben Sie an der **DISKPART**-Eingabeaufforderung `select volume <volumenumber>` und die Volumenummer ein, der Sie den Pfad zuweisen möchten.

5.  Gib an der Eingabeaufforderung **DISKPART** Folgendes ein: `assign [mount=<path>]`.

### <a name="to-remove-a-mount-point"></a>So entfernen Sie einen Bereitstellungspunkt

So entfernen Sie den Bereitstellungspunkt, damit der Zugriff auf das Laufwerk über den Ordner nicht mehr möglich ist:

1. Halten Sie das in einem Ordner bereitgestellte Laufwerk gedrückt (oder klicken Sie mit der rechten Maustaste darauf), und wählen Sie dann **Laufwerkbuchstaben und Pfade ändern** aus.
2. Wählen Sie den Ordner aus der Liste und dann **Entfernen** aus.

| Value | Beschreibung |
| --- | --- |
| **list volume** | Zeigt eine Liste der Basisvolumes und dynamischen Volumes auf allen Datenträgern an. |
| **select volume**        | Wählt das angegebene Volume aus und weist ihm den Fokus zu. (<em>volumenumber</em> ist die Nummer des Volumes.) Ohne Volumeangabe führt der Befehl **select** die aktuellen Volumes mit Fokus auf. Das Volume kann anhand der Nummer, des Laufwerkbuchstabens oder des Ordnerpfads mit Bereitstellungspunkt angegeben werden. Wenn bei einer Basisfestplatte ein Volume ausgewählt wird, erhält die entsprechende Partition den Fokus.|
| **assign** | <ul><li> Weist dem Volume mit Fokus einen Laufwerkbuchstaben oder einen Ordnerpfad mit Bereitstellungspunkt zu. Ist kein Laufwerkbuchstaben oder Ordnerpfad mit Bereitstellungspunkt angegeben, wird der nächste verfügbare Laufwerkbuchstabe zugewiesen. Wird der Laufwerkbuchstabe oder Ordnerpfad mit Bereitstellungspunkt bereits verwendet, wird ein Fehler ausgegeben.</li>  <li>Mit dem Befehl **assign** kannst du den einem Wechseldatenträger zugeordneten Laufwerkbuchstaben ändern.</li> <li> Startvolumes oder Volumes mit der Auslagerungsdatei können keine Laufwerkbuchstaben zugewiesen werden. Darüber hinaus kannst du einer OEM-Partition (Original Equipment Manufacturer, Originalgerätehersteller), einer EFI-Systempartition oder einer GPT-Partition, die keine einfache Datenpartition ist, keinen Laufwerkbuchstaben zuweisen.</li></ul> |
| **mount=** <em>path</em> | Gibt einen leeren, vorhandenen NTFS-Ordner für das bereitgestellte Laufwerk an.  |

## <a name="additional-considerations"></a>Weitere Überlegungen

-   Wenn du einen lokalen Computer oder einen Remotecomputer verwaltest, kannst du die NTFS-Ordner auf diesem Computer durchsuchen.
-   Ordnerpfade mit Bereitstellungspunkt sind nur für leere Ordner mit NTFS-Basisvolumes oder dynamischen NTFS-Volumes verfügbar.
-   Wenn du einen Ordnerpfad mit Bereitstellungspunkt ändern möchtest, entferne ihn, und erstelle einen neuen Ordnerpfad mit dem neuen Speicherort. Der Ordnerpfad mit Bereitstellungspunkt kann nicht direkt geändert werden.
-   Verwende beim Zuweisen eines Ordnerpfads mit Bereitstellungspunkt zu einem Laufwerk die **Ereignisanzeige**, um das Systemprotokoll auf Clusterdienstfehler oder -warnungen zu überprüfen, die auf Fehler beim Ordnerpfad mit Bereitstellungspunkt hinweisen. Diese Fehler werden in der Spalte **Quelle** als **ClusSvc** und in der Spalte **Kategorie** als **Physische Datenträgerressource** aufgeführt.
-   Du kannst ein bereitgestelltes Laufwerk auch mit dem Befehl [mountvol](https://go.microsoft.com/fwlink/?linkid=64111) erstellen.

## <a name="additional-references"></a>Weitere Verweise
-   [Command-line syntax notation](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx) (Notation der Befehlszeilensyntax)
