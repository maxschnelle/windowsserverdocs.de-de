---
title: Anwenden eines Kontingents auf ein Volume oder einen Ordner
description: Dieser Artikel beschreibt, wie Sie ein Speicherkontingent auf ein Volume oder einen Ordner anwenden.
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: e937464ca3af1292de5fd63303ba4a430f831dcd
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2019
ms.locfileid: "65475862"
---
# <a name="checklist-apply-a-quota-to-a-volume-or-folder"></a>Prüfliste: Anwenden eines Kontingents auf einem Volume oder einen Ordner

> Gilt für: WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2, WindowsServer (Halbjährlicher Kanal)

1. Konfigurieren Sie die E-Mail-Einstellungen, wenn Sie Schwellenwertbenachrichtigungen oder Speicherberichte per E-Mail senden möchten. [Konfigurieren von e-Mail-Benachrichtigungen](configure-email-notifications.md)

2. Bewerten Sie die Speicherkapazität auf dem Volume oder Ordner. Sie können dazu die Berichte des **Speicherberichteverwaltungs**knotens verwenden, um Daten bereitzustellen. (Z. B. Führen Sie einen Dateien nach Besitzer Bericht bei Bedarf zur Identifizierung von Benutzern, die große Mengen an Speicherplatz auf dem Datenträger zu verwenden.) [Berichte nach Bedarf erstellen](generate-reports-on-demand.md)

3. Überprüfen Sie die verfügbaren vorkonfigurierten Kontingentvorlagen. (In **Kontingentverwaltung**, klicken Sie auf die **Kontingentvorlagen** Knoten.) [Kontingentvorlageneigenschaften bearbeiten](edit-quota-template-properties.md) 
<br />– Oder – <br /> Erstellen Sie eine neue Kontingentvorlage, um eine Speicherrichtlinie in Ihrer Organisation zu erzwingen. [Erstellen Sie eine Kontingentvorlage](create-quota-template.md)

4. Erstellen Sie basierend auf der Vorlage ein Kontingent auf einem Volume oder Ordner.  
 [Erstellen eines Kontingents](create-quota.md) <br /> – Oder – <br /> Erstellen Sie ein automatisch zugewiesenes Kontingent, um automatisch Kontingente für Unterordner auf dem Volume oder einen Ordner zu erstellen. [Erstellen eines automatisch zugewiesenen Kontingents](create-auto-apply-quota.md)

6. Planen Sie eine Berichtsaufgabe, die einen Kontingentbedarfsbericht enthält, um um den Kontingentbedarf in regelmäßigen Abständen zu überwachen. [Planen eines Satzes von Berichten](schedule-set-of-reports.md)

> [!Note]
> Zum Prüfen von Dateien auf einem Volume oder einen Ordner, finden Sie unter [Prüfliste: Wenden Sie einen Bildschirm für die Datei auf ein Volume oder einen Ordner](checklist-apply-file-screen-to-volume-or-folder.md).











