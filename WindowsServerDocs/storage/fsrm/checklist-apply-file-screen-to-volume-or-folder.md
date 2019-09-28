---
title: Prüfliste – Dateiprüfung auf ein Volume oder einen Ordner anwenden
description: Dieser Artikel beschreibt, wie Sie eine Dateiprüfung auf ein Volume oder einen Ordner anwenden.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 4d38e9a92a9c99663d81aab2a0164c5a30002f6a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401992"
---
# <a name="checklist---apply-a-file-screen-to-a-volume-or-folder"></a>Prüfliste – Dateiprüfung auf ein Volume oder einen Ordner anwenden

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Um eine Dateiprüfung auf ein Volume oder einen Ordner anzuwenden, verwenden Sie folgende Liste:
1. Konfigurieren Sie die E-Mail-Einstellungen, wenn Sie die Prüfungsbenachrichtigungen oder Berichte per E-Mail senden möchten. Nutzen Sie dazu die Anweisungen unter [E-Mail-Benachrichtigungen konfigurieren](configure-email-notifications.md).

2. Aktivieren Sie die Aufzeichnung der Dateiprüfungsereignisse in der Überwachungsdatenbank, wenn Sie Dateiprüfungsberichte erstellen möchten.
[Dateiprüfungsberichte konfigurieren](configure-file-screen-audit.md)

3. Bewerten Sie gespeicherten Dateitypen, die als Prüfungsregeln geeignet sind. Sie können Berichte der **Speicherberichtmanagement**-Knoten verwenden, um Daten bereitzustellen. (Führen Sie z. b. einen Dateien nach Dateigruppe Bericht oder einen große Dateien Bericht Bedarfs gesteuert aus, um Dateien zu identifizieren, die große Mengen an Speicherplatz belegen.) [Berichte nach Bedarf erstellen](generate-reports-on-demand.md) 

4. Überprüfen Sie die vorkonfigurierten Dateigruppen oder erstellen Sie eine neue Dateigruppe, um eine bestimmte Prüfungsrichtlinie in Ihrer Organisation zu erzwingen. [Definieren von Dateigruppen für die Prüfung](define-file-groups-for-screening.md)  

5. Überprüfen Sie die Eigenschaften der verfügbaren Dateiprüfungsvorlagen. (Klicken Sie in der **Datei Untersuchung-Verwaltung**auf den Knoten **Datei Bildschirm Vorlagen** .) [Eigenschaften der Datei Bildschirm Vorlage bearbeiten](edit-file-screen-template-properties.md) 
<br />
 – Oder –
 <br /> Erstellen Sie eine neue Dateiprüfungsvorlage, um eine Speicherrichtlinie in Ihrer Organisation zu erzwingen.  [Erstellen einer Dateiprüfungsvorlage](create-file-screen-template.md) 

6. Erstellen Sie basierend auf der Vorlage eine Dateiprüfung auf einem Volume oder Ordner. 
 [Erstellen einer Dateiprüfung](create-file-screen.md)
 
7. Konfigurieren Sie in den Unterordnern des Volumes oder Ordners Dateiprüfungsausnahmen. [Erstellen einer Dateiprüfungsausnahme](create-file-screen-exception.md) 

8. Planen Sie eine Berichtsaufgabe, die einen Dateiprüfungsüberwachungs-Bericht enthält, um die Dateiprüfungsaktivitäten in regelmäßigen Abständen zu überwachen.
  [Planen eines Satzes von Berichten](schedule-set-of-reports.md)


> [!NOTE]
> Informationen zum Einschränken des Speichers für ein Volume oder einen Ordner finden Sie unter [checkliste: Anwenden eines Kontingents auf ein Volume oder einen Ordner](checklist-apply-file-screen-to-volume-or-folder.md)