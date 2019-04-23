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
ms.openlocfilehash: 62910af666fb16db5c2e7a30b49eedfa8c12cacb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860851"
---
# <a name="checklist-apply-a-quota-to-a-volume-or-folder"></a>Prüfliste: Anwenden eines Kontingents auf einem Volume oder einen Ordner

> Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2

1. Konfigurieren Sie die E-Mail-Einstellungen, wenn Sie Schwellenwertbenachrichtigungen oder Speicherberichte per E-Mail senden möchten. [Konfigurieren von e-Mail-Benachrichtigungen](configure-email-notifications.md)

2. Bewerten Sie die Speicherkapazität auf dem Volume oder Ordner. Sie können dazu die Berichte des **Speicherberichteverwaltungs**knotens verwenden, um Daten bereitzustellen. (Z. B. Führen Sie einen Dateien nach Besitzer Bericht bei Bedarf zur Identifizierung von Benutzern, die große Mengen an Speicherplatz auf dem Datenträger zu verwenden.) [Generieren von Berichten bei Bedarf](generate-reports-on-demand.md)

3. Überprüfen Sie die verfügbaren vorkonfigurierten Kontingentvorlagen. (In **Kontingentverwaltung**, klicken Sie auf die **Kontingentvorlagen** Knoten.) [Kontingentvorlageneigenschaften bearbeiten](edit-quota-template-properties.md) 
<br />– Oder – <br /> Erstellen Sie eine neue Kontingentvorlage, um eine Speicherrichtlinie in Ihrer Organisation zu erzwingen. [Erstellen Sie eine Kontingentvorlage](create-quota-template.md)

4. Erstellen Sie basierend auf der Vorlage ein Kontingent auf einem Volume oder Ordner.  
 [Erstellen Sie ein Kontingent](create-quota.md) <br /> – Oder – <br /> Erstellen Sie ein automatisch zugewiesenes Kontingent, um automatisch Kontingente für Unterordner auf dem Volume oder einen Ordner zu erstellen. [Erstellen eines automatisch zugewiesenen Kontingents](create-auto-apply-quota.md)

6. Planen Sie eine Berichtsaufgabe, die einen Kontingentbedarfsbericht enthält, um um den Kontingentbedarf in regelmäßigen Abständen zu überwachen. [Planen Sie eine Reihe von Berichten](schedule-set-of-reports.md)

> [!Note]
> Zum Prüfen von Dateien auf einem Volume oder einen Ordner, finden Sie unter [Prüfliste: Wenden Sie einen Bildschirm für die Datei auf ein Volume oder einen Ordner](checklist-apply-file-screen-to-volume-or-folder.md).











