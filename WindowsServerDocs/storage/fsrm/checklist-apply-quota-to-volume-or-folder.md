---
title: Anwenden eines Kontingents auf ein Volume oder einen Ordner
description: In diesem Artikel wird beschrieben, wie Sie ein Speicher Kontingent auf ein Volume oder einen Ordner anwenden.
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 6f35576c67b3b5837749d0f19da82b242cc6c1cd
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87957588"
---
# <a name="checklist-apply-a-quota-to-a-volume-or-folder"></a>Prüfliste: Anwenden eines Kontingents auf ein Volume oder einen Ordner

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server (halbjährlicher Kanal)

1. Konfigurieren Sie e-Mail-Einstellungen, wenn Sie Schwellenwert Benachrichtigungen oder Speicher Berichte per e-Mail senden möchten. [E-Mail-Benachrichtigungen](configure-email-notifications.md)

2. Bewerten Sie die Speicheranforderungen für das Volume oder den Ordner. Sie können Berichte auf dem Knoten **Speicher Berichte-Verwaltung** verwenden, um Daten bereitzustellen. (Führen Sie z. b. einen Dateien nach Besitzer Bericht bei Bedarf aus, um Benutzer zu identifizieren, die große Mengen an Speicherplatz verwenden.) [Bedarfs gesteuertes Generieren von Berichten](generate-reports-on-demand.md)

3. Überprüfen Sie die verfügbaren vorkonfigurierten Kontingent Vorlagen. (Klicken Sie in **Kontingent Verwaltung**auf den Knoten **Kontingent Vorlagen** .) [Eigenschaften für Kontingent Vorlage bearbeiten](edit-quota-template-properties.md)
<br />-Oder- <br /> Erstellen Sie eine neue Kontingent Vorlage, um eine Speicher Richtlinie in Ihrer Organisation zu erzwingen. [Erstellen einer Kontingent Vorlage](create-quota-template.md)

4. Erstellen Sie ein Kontingent auf der Grundlage der Vorlage auf dem Volume oder Ordner.
 [Erstellen eines Kontingents](create-quota.md) <br /> -Oder- <br /> Erstellen Sie ein automatisches Apply-Kontingent, um automatisch Kontingente für Unterordner auf dem Volume oder Ordner zu generieren. [Erstellen eines automatisch zugewiesenen Kontingents](create-auto-apply-quota.md)

6. Planen Sie einen Berichts Task, der einen Bericht zur Kontingent Verwendung enthält, um die Kontingent Auslastung regelmäßig zu überwachen [Planen eines Satzes von Berichten](schedule-set-of-reports.md)

> [!Note]
> Wenn Sie Dateien auf einem Volume oder Ordner überprüfen möchten, finden Sie unter Prüfliste [: Anwenden eines Datei Bildschirms auf ein Volume oder einen Ordner](checklist-apply-file-screen-to-volume-or-folder.md)Weitere Informationen.











