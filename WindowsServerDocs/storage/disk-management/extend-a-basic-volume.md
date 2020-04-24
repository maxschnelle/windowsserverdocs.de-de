---
title: Erweitern eines Basisvolumes
description: Du kannst einem vorhandenen Volume in Windows Speicherplatz hinzufügen, indem du es auf leeren Speicherplatz auf dem Laufwerk erweiterst. Dies ist allerdings nur möglich, wenn der leere Speicherplatz kein Volume enthält (nicht zugeordnet ist) und unmittelbar an das zu erweiternde Volume angrenzt, ohne dass sich dazwischen weitere Volumes befinden. Dieser Artikel beschreibt die Vorgehensweise.
ms.date: 12/19/2019
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: c72b242437c4c308da77a25e06f3d76e4c65f480
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "75351909"
---
# <a name="extend-a-basic-volume"></a>Erweitern eines Basisvolumes

> **Gilt für:** Windows 10, Windows 8.1, Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Du kannst einem vorhandenen Volume mithilfe der Datenträgerverwaltung Speicherplatz hinzufügen, indem du es auf leeren Speicherplatz auf dem Laufwerk erweiterst. Dies ist allerdings nur möglich, wenn der leere Speicherplatz kein Volume enthält (nicht zugeordnet ist) und unmittelbar an das zu erweiternde Volume angrenzt, ohne dass sich dazwischen weitere Volumes befinden, wie in der folgenden Abbildung dargestellt. Das zu erweiternde Volume muss außerdem mit dem NTFS- oder ReFS-Dateisystem formatiert sein.

:::image type="content" source="media/extend-volume-space-highlighted.png" alt-text="Datenträgerverwaltung mit freiem Speicherplatz, auf den ein Volume erweitert werden kann.":::

## <a name="to-extend-a-volume-by-using-disk-management"></a>So erweiterst du ein Volume mithilfe der Datenträgerverwaltung

Hier wird beschrieben, wie du ein Volume auf leeren Speicherplatz erweiterst, der unmittelbar an das Volume auf dem Laufwerk angrenzt:

1. Öffne die Datenträgerverwaltung mit Administratorberechtigungen.

   Gib dazu einfach **Computerverwaltung** in das Suchfeld auf der Taskleiste ein, halte **Computerverwaltung** gedrückt (oder klicke mit der rechten Maustaste darauf), und wähle anschließend **Als Administrator ausführen** > **Ja** aus. Nachdem die Computerverwaltung geöffnet wurde, wechsle zu **Speicher** > **Datenträgerverwaltung**.
2. Halte das Volume, das du erweitern möchtest, gedrückt (oder klicke mit der rechten Maustaste darauf), und wähle dann **Volume erweitern** aus.

   Wenn **Volume erweitern** abgeblendet ist, überprüfe Folgendes:
    - Die Datenträgerverwaltung oder Computerverwaltung wurde mit Administratorberechtigungen geöffnet.
    - Es liegt nicht zugeordneter Speicherplatz direkt im Anschluss an das (rechts vom) Volume vor, wie in der obigen Abbildung gezeigt. Wenn zwischen dem nicht zugeordneten Speicherplatz und dem Volume, das du erweitern möchtest, ein anderes Volume vorhanden ist, kannst du entweder das dazwischen liegende Volume und alle darauf befindlichen Dateien löschen (stelle sicher, dass vorher alle wichtigen Dateien gesichert oder verschoben wurden), eine Nicht-Microsoft-App zur Datenträgerpartitionierung verwenden, die das Verschieben von Volumes ohne Zerstörung von Daten ermöglicht, oder die Erweiterung des Volumes überspringen und stattdessen ein separates Volume im nicht zugeordneten Speicherplatz erstellen.
    - Das Volume wurde mit dem Dateisystem NTFS oder ReFS formatiert. Andere Dateisysteme können nicht erweitert werden. Du müsstest daher die Dateien auf dem Volume verschieben oder sichern und das Volume dann mit dem NTFS- oder ReFS-Dateisystem formatieren.
    - Wenn der Datenträger größer als 2 TB ist, stelle sicher, dass er das GPT-Partitionierungsschema verwendet. Um mehr als 2 TB auf einem Datenträger zu verwenden, muss dieser mit dem GPT-Partitionierungsschema initialisiert werden. Informationen zum Konvertieren in GPT findest du unter [Ändern eines MBR-Datenträgers in einen GPT-Datenträger](change-an-mbr-disk-into-a-gpt-disk.md).
    - Wenn du das Volume immer noch nicht erweitern kannst, durchsuche die Website [Microsoft-Community: Dateien, Ordner und Speicher](https://answers.microsoft.com/en-us/windows/forum/windows_10-files?sort=lastreplydate&dir=desc&tab=All&status=all&mod=&modAge=&advFil=&postedAfter=&postedBefore=&threadType=all&isFilterExpanded=true&tm=1514405359639). Solltest du dort keine Antwort finden, stelle selbst eine Frage, die dann von Microsoft oder von anderen Mitgliedern der Community beantwortet wird, oder [wende dich an den Microsoft-Support](https://support.microsoft.com/contactus/).

3. Wähle **Weiter** aus, und gib dann auf der Seite **Datenträger auswählen** des Assistenten (hier) an, um wie viel das Volume erweitert werden soll. Normalerweise sollte der Standardwert verwendet werden, wodurch der gesamte verfügbare freie Speicherplatz genutzt wird, aber du kannst auch einen kleineren Wert verwenden, wenn du weitere Volumes im freien Speicherplatz erstellen möchtest.

   :::image type="content" source="media/extend-volume-wizard.png" alt-text="Der Assistent zum Erweitern von Volumes zeigt ein Volume an, das auf den gesamten verfügbaren Speicher erweitert wird":::

4. Wähle **Weiter** und dann **Fertig stellen** aus, um das Volume zu erweitern.

## <a name="to-extend-a-volume-by-using-powershell"></a>So erweiterst du ein Volume mit PowerShell

1. Halte die Startschaltfläche gedrückt (oder klicke mit der rechten Maustaste darauf), und wähle dann „Windows PowerShell (Admin)“ aus.
2. Gib den folgenden Befehl ein, um die Größe des Volumes auf die maximale Größe zu ändern. Gib dabei in der Variablen *$drive_letter* den Laufwerksbuchstaben des Volumes an, das erweitert werden soll:

   ```PowerShell
   # Variable specifying the drive you want to extend
   $drive_letter = "C"

   # Script to get the partition sizes and then resize the volume
   $size = (Get-PartitionSupportedSize -DriveLetter $drive_letter)
   Resize-Partition -DriveLetter $drive_letter -Size $size.SizeMax
   ```

## <a name="see-slso"></a>Siehe auch

- [Resize-Partition](https://docs.microsoft.com/powershell/module/storage/resize-partition)
- [DiskPart – Erweitern](https://docs.microsoft.com/windows-server/administration/windows-commands/extend)
