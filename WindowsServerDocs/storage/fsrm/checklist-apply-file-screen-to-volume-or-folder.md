---
title: 'Prüfliste: Anwenden eines Datei Bildschirms auf ein Volume oder einen Ordner'
description: In diesem Artikel wird beschrieben, wie Sie einen Datei Bildschirm auf ein Volume oder einen Ordner anwenden.
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: e7318d2e67cb5dd39aaa4fb95ad6cbca7eff9512
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87957598"
---
# <a name="checklist---apply-a-file-screen-to-a-volume-or-folder"></a>Prüfliste: Anwenden eines Datei Bildschirms auf ein Volume oder einen Ordner

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Verwenden Sie die folgende Liste, um einen Datei Bildschirm auf ein Volume oder einen Ordner anzuwenden:
1. Konfigurieren von e-Mail-Einstellungen, wenn Sie Datei Überprüfungs Benachrichtigungen oder Speicher Berichte per e-Mail senden möchten, indem Sie die Anweisungen unter [Konfigurieren von e-Mail-Benachrichtigungen](configure-email-notifications.md)befolgen

2. Aktivieren Sie die Aufzeichnung von Datei Überprüfungs Ereignissen in der Überwachungs Datenbank, wenn Sie beabsichtigen, Dateiprüfungsüberwachung Berichte zu generieren.
[Dateiprüfungsberichte konfigurieren](configure-file-screen-audit.md)

3. Bewertet gespeicherte Dateitypen, die Kandidaten für Überprüfungs Regeln sind. Sie können Berichte im Knoten **Speicher Berichte-Verwaltung** verwenden, um Daten bereitzustellen. (Führen Sie z. b. einen Dateien nach Dateigruppe Bericht oder einen große Dateien Bericht Bedarfs gesteuert aus, um Dateien zu identifizieren, die große Mengen an Speicherplatz belegen.) [Bedarfs gesteuertes Generieren von Berichten](generate-reports-on-demand.md)

4. Überprüfen Sie die vorkonfigurierten Dateigruppen, oder erstellen Sie eine neue Datei Gruppe, um eine bestimmte Überprüfungs Richtlinie in Ihrer Organisation zu erzwingen. [Definieren von Dateigruppen für die Prüfung](define-file-groups-for-screening.md)

5. Überprüfen Sie die Eigenschaften der verfügbaren Datei Bildschirm Vorlagen. (Klicken Sie in der **Datei Untersuchung-Verwaltung**auf den Knoten **Datei Bildschirm Vorlagen** .) [Eigenschaften der Datei Bildschirm Vorlage bearbeiten](edit-file-screen-template-properties.md)
<br />
 -Oder-
 <br /> Erstellen Sie eine neue Datei Bildschirm Vorlage, um eine Speicher Richtlinie in Ihrer Organisation zu erzwingen.  [Erstellen einer Dateiprüfungsvorlage](create-file-screen-template.md)

6. Erstellen Sie einen Datei Bildschirm auf der Grundlage der Vorlage auf einem Volume oder Ordner.
 [Erstellen einer Dateiprüfung](create-file-screen.md)

7. Konfigurieren Sie Datei Bildschirm Ausnahmen in Unterordnern des Volumes oder Ordners. [Erstellen einer Dateiprüfungsausnahme](create-file-screen-exception.md)

8. Planen Sie eine Berichts Aufgabe mit einem Dateiprüfungsüberwachung Bericht, um die Prüfungs Aktivität regelmäßig zu überwachen.
  [Planen eines Satzes von Berichten](schedule-set-of-reports.md)


> [!NOTE]
> Informationen zum Einschränken des Speichers für ein Volume oder einen Ordner finden Sie unter Prüfliste [: Anwenden eines Kontingents auf ein Volume oder einen Ordner](checklist-apply-file-screen-to-volume-or-folder.md)