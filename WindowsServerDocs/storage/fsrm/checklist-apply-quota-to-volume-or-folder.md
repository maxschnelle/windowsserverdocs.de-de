---
title: Anwenden eines Kontingents auf ein Volume oder einen Ordner
description: Dieser Artikel beschreibt, wie Sie ein Speicherkontingent auf ein Volume oder einen Ordner anwenden.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 44eea3c3802e261239db9bf8350777e1b83fb9c4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394331"
---
# <a name="checklist-apply-a-quota-to-a-volume-or-folder"></a>Prüfliste: Anwenden eines Kontingents auf ein Volume oder einen Ordner

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server (halbjährlicher Kanal)

1. Konfigurieren Sie die E-Mail-Einstellungen, wenn Sie Schwellenwertbenachrichtigungen oder Speicherberichte per E-Mail senden möchten. [E-Mail-Benachrichtigungen](configure-email-notifications.md)

2. Bewerten Sie die Speicherkapazität auf dem Volume oder Ordner. Sie können dazu die Berichte des **Speicherberichteverwaltungs**knotens verwenden, um Daten bereitzustellen. (Führen Sie beispielsweise einen Dateien nach Besitzer-Bericht auf Abruf aus, um Benutzer zu identifizieren, die eine erhebliche Menge Speicherplatz beanspruchen.) [Berichte nach Bedarf erstellen](generate-reports-on-demand.md)

3. Überprüfen Sie die verfügbaren vorkonfigurierten Kontingentvorlagen. (Klicken Sie in **Kontingent Verwaltung**auf den Knoten **Kontingent Vorlagen** .) [Eigenschaften der Kontingent Vorlage bearbeiten](edit-quota-template-properties.md) 
<br />– Oder – <br /> Erstellen Sie eine neue Kontingentvorlage, um eine Speicherrichtlinie in Ihrer Organisation zu erzwingen. [Erstellen einer Kontingent Vorlage](create-quota-template.md)

4. Erstellen Sie basierend auf der Vorlage ein Kontingent auf einem Volume oder Ordner.  
 [Erstellen eines Kontingents](create-quota.md) <br /> – Oder – <br /> Erstellen Sie ein automatisch zugewiesenes Kontingent, um automatisch Kontingente für Unterordner auf dem Volume oder einen Ordner zu erstellen. [Erstellen eines automatisch zugewiesenen Kontingents](create-auto-apply-quota.md)

6. Planen Sie eine Berichtsaufgabe, die einen Kontingentbedarfsbericht enthält, um um den Kontingentbedarf in regelmäßigen Abständen zu überwachen. [Planen eines Satzes von Berichten](schedule-set-of-reports.md)

> [!Note]
> Informationen zum Prüfen von Dateien auf einem Volume oder Ordner erhalten Sie unter [Prüfliste: Dateiprüfung auf ein Volume oder einen Ordner anwenden](checklist-apply-file-screen-to-volume-or-folder.md).











