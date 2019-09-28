---
title: Zuweisen eines Ordnerpfads mit Bereitstellungspunkt zu einem Laufwerk
description: In diesem Artikel wird beschrieben, wie du einem Laufwerk einen Ordnerpfad mit Bereitstellungspunkt (anstelle eines Laufwerkbuchstaben) zuweist.
keywords: Virtualisierung, Sicherheit, Schadsoftware
ms.date: 06/07/2019
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 1255eadd50adb0eaaf44774e150d69f6dad8adae
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386049"
---
# <a name="assign-a-mount-point-folder-path-to-a-drive"></a>Zuweisen eines Ordnerpfads mit Bereitstellungspunkt zu einem Laufwerk

> **Gilt für:** Windows 10, Windows 8.1, Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Du kannst die Datenträgerverwaltung verwenden, um dem Laufwerk einen Ordnerpfad mit Bereitstellungspunkt (anstelle eines Laufwerkbuchstabens) zuzuweisen. Ordnerpfade mit Bereitstellungspunkt sind nur für leere Ordner mit NTFS-Basisvolumes oder dynamischen NTFS-Volumes verfügbar.

## <a name="assigning-a-mount-point-folder-path-to-a-drive"></a>Zuweisen eines Ordnerpfads mit Bereitstellungspunkt zu einem Laufwerk

> [!NOTE]
> Du musst mindestens Mitglied der Gruppe **Sicherungsoperatoren** oder **Administratoren** sein, um diese Schritte ausführen zu können.

#### <a name="to-assign-a-mount-point-folder-path-to-a-drive-by-using-the-windows-interface"></a>So weist du mithilfe der Windows-Benutzeroberfläche einem Laufwerk einen Ordnerpfad mit Bereitstellungspunkt zu

1.  Klicke in der Datenträgerverwaltung mit der rechten Maustaste auf die Partition oder das Volume, in der bzw. auf dem du den Ordnerpfad mit Bereitstellungspunkt zuweisen möchtest. 
2. Klicke auf **Laufwerkbuchstaben und -pfade ändern...** und dann auf **Hinzufügen**. 
3. Klicke auf **In folgendem leeren NTFS-Ordner bereitstellen**.
4. Gib den Pfad zu einem leeren Ordner auf einem NTFS-Volume an, oder klicke auf **Durchsuchen**, um ihn zu suchen.

#### <a name="to-assign-a-mount-point-folder-path-to-a-drive-using-a-command-line"></a>So weist du mithilfe einer Befehlszeile einem Laufwerk einen Ordnerpfad mit Bereitstellungspunkt zu

1.  Öffnen Sie eine Eingabeaufforderung, und geben Sie `diskpart` ein.

2.  Gib an der **DISKPART**-Eingabeaufforderung `list volume` ein, und notiere die Volumenummer, der du den Pfad zuweisen möchtest.

3.  Gib an der Eingabeaufforderung **DISKPART** Folgendes ein: `select volume <volumenumber>`. 

4. Wähle *volumenumber* des einfachen Volumes aus, dem du den Pfad zuweisen möchtest.

5.  Gib an der Eingabeaufforderung **DISKPART** Folgendes ein: `assign [mount=<path>]`.

#### <a name="to-remove-a-mount-point-folder-path-to-a-drive"></a>So entfernst du den Ordnerpfad mit Bereitstellungspunkt eines Laufwerks

-   Klicke zum Entfernen des Ordnerpfads mit Bereitstellungspunkt auf den Pfad und dann auf **Entfernen**.

| Wert | Beschreibung |
| --- | --- |
| **list volume** | Zeigt eine Liste der Basisvolumes und dynamischen Volumes auf allen Datenträgern an. |
| **select volume**        | Wählt das angegebene Volume aus und weist ihm den Fokus zu. (<em>volumenumber</em> ist die Nummer des Volumes.) Ohne Volumeangabe führt der Befehl **select** die aktuellen Volumes mit Fokus auf. Das Volume kann anhand der Nummer, des Laufwerkbuchstabens oder des Ordnerpfads mit Bereitstellungspunkt angegeben werden. Wenn bei einer Basisfestplatte ein Volume ausgewählt wird, erhält die entsprechende Partition den Fokus.|
| **assign** | <ul><li> Weist dem Volume mit Fokus einen Laufwerkbuchstaben oder einen Ordnerpfad mit Bereitstellungspunkt zu. Ist kein Laufwerkbuchstaben oder Ordnerpfad mit Bereitstellungspunkt angegeben, wird der nächste verfügbare Laufwerkbuchstabe zugewiesen. Wird der Laufwerkbuchstabe oder Ordnerpfad mit Bereitstellungspunkt bereits verwendet, wird ein Fehler ausgegeben.</li>  <li>Mit dem Befehl **assign** kannst du den einem Wechseldatenträger zugeordneten Laufwerkbuchstaben ändern.</li> <li> Startvolumes oder Volumes mit der Auslagerungsdatei können keine Laufwerkbuchstaben zugewiesen werden. Darüber hinaus kannst du einer OEM-Partition (Original Equipment Manufacturer, Originalgerätehersteller), einer EFI-Systempartition oder einer GPT-Partition, die keine einfache Datenpartition ist, keinen Laufwerkbuchstaben zuweisen.</li></ul> |
| **mount=** <em>path</em> | Gibt einen leeren, vorhandenen NTFS-Ordner für das bereitgestellte Laufwerk an.  |

## <a name="additional-considerations"></a>Weitere Aspekte

-   Wenn du einen lokalen Computer oder einen Remotecomputer verwaltest, kannst du die NTFS-Ordner auf diesem Computer durchsuchen.
-   Ordnerpfade mit Bereitstellungspunkt sind nur für leere Ordner mit NTFS-Basisvolumes oder dynamischen NTFS-Volumes verfügbar.
-   Wenn du einen Ordnerpfad mit Bereitstellungspunkt ändern möchtest, entferne ihn, und erstelle einen neuen Ordnerpfad mit dem neuen Speicherort. Der Ordnerpfad mit Bereitstellungspunkt kann nicht direkt geändert werden.
-   Verwende beim Zuweisen eines Ordnerpfads mit Bereitstellungspunkt zu einem Laufwerk die **Ereignisanzeige**, um das Systemprotokoll auf Clusterdienstfehler oder -warnungen zu überprüfen, die auf Fehler beim Ordnerpfad mit Bereitstellungspunkt hinweisen. Diese Fehler werden in der Spalte **Quelle** als **ClusSvc** und in der Spalte **Kategorie** als **Physische Datenträgerressource** aufgeführt.
-   Du kannst ein bereitgestelltes Laufwerk auch mit dem Befehl [mountvol](https://go.microsoft.com/fwlink/?linkid=64111) erstellen.

## <a name="see-also"></a>Weitere Informationen
-   [Command-line syntax notation](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx) (Notation der Befehlszeilensyntax)


