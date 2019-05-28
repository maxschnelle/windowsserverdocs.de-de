---
title: Prüfliste – Dateiprüfung auf ein Volume oder einen Ordner anwenden
description: Dieser Artikel beschreibt, wie Sie eine Dateiprüfung auf ein Volume oder einen Ordner anwenden.
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 03325d8a65d88c35f09985223608fc7474a0fde5
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2019
ms.locfileid: "65475850"
---
# <a name="checklist---apply-a-file-screen-to-a-volume-or-folder"></a>Prüfliste – Dateiprüfung auf ein Volume oder einen Ordner anwenden

> Gilt für: WindowsServer 2019, WindowsServer 2016, WindowsServer (Halbjährlicher Kanal), Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2

Um eine Dateiprüfung auf ein Volume oder einen Ordner anzuwenden, verwenden Sie folgende Liste:
1. Konfigurieren Sie die E-Mail-Einstellungen, wenn Sie die Prüfungsbenachrichtigungen oder Berichte per E-Mail senden möchten. Nutzen Sie dazu die Anweisungen unter [E-Mail-Benachrichtigungen konfigurieren](configure-email-notifications.md).

2. Aktivieren Sie die Aufzeichnung der Dateiprüfungsereignisse in der Überwachungsdatenbank, wenn Sie Dateiprüfungsberichte erstellen möchten.
[Dateiprüfungsberichte konfigurieren](configure-file-screen-audit.md)

3. Bewerten Sie gespeicherten Dateitypen, die als Prüfungsregeln geeignet sind. Sie können Berichte der **Speicherberichtmanagement**-Knoten verwenden, um Daten bereitzustellen. (Z. B. Führen Sie einen Dateien nach Dateigruppe oder ein Bericht große Dateien bei Bedarf, um Dateien zu identifizieren, die große Mengen an Speicherplatz belegen.) [Berichte nach Bedarf erstellen](generate-reports-on-demand.md) 

4. Überprüfen Sie die vorkonfigurierten Dateigruppen oder erstellen Sie eine neue Dateigruppe, um eine bestimmte Prüfungsrichtlinie in Ihrer Organisation zu erzwingen. [Definieren von Dateigruppen für die Prüfung](define-file-groups-for-screening.md)  

5. Überprüfen Sie die Eigenschaften der verfügbaren Dateiprüfungsvorlagen. (In **Dateiprüfungsverwaltung**, klicken Sie auf die **Datei Bildschirmvorlagen** Knoten.) [Bearbeiten der Eigenschaften der Vorlage Bildschirm](edit-file-screen-template-properties.md) 
<br />
 – Oder –
 <br /> Erstellen Sie eine neue Dateiprüfungsvorlage, um eine Speicherrichtlinie in Ihrer Organisation zu erzwingen.  [Erstellen einer Dateiprüfungsvorlage](create-file-screen-template.md) 

6. Erstellen Sie basierend auf der Vorlage eine Dateiprüfung auf einem Volume oder Ordner. 
 [Erstellen Sie einen Datei-Bildschirm](create-file-screen.md)
 
7. Konfigurieren Sie in den Unterordnern des Volumes oder Ordners Dateiprüfungsausnahmen. [Erstellen einer Dateiprüfungsausnahme](create-file-screen-exception.md) 

8. Planen Sie eine Berichtsaufgabe, die einen Dateiprüfungsüberwachungs-Bericht enthält, um die Dateiprüfungsaktivitäten in regelmäßigen Abständen zu überwachen.
  [Planen eines Satzes von Berichten](schedule-set-of-reports.md)


> [!NOTE]
> Um Speicher auf einem Volume oder einen Ordner zu beschränken, finden Sie unter [Prüfliste: Anwenden eines Kontingents auf ein Volume oder einen Ordner](checklist-apply-file-screen-to-volume-or-folder.md)