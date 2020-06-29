---
title: Dateiprüfungsberichte konfigurieren
description: In diesem Artikel wird beschrieben, wie Sie die Datei Bildschirm Überwachung konfigurieren, um den Dateiprüfungsüberwachung Bericht zu generieren
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: cf1824e514c34ee89870daa6d15190bffd822a8b
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475317"
---
# <a name="configure-file-screen-audit"></a>Dateiprüfungsberichte konfigurieren

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Mithilfe der Datei Server Ressourcen-Manager können Sie die Aktivität "Dateiüberprüfung" in einer Überwachungs Datenbank aufzeichnen. Die in dieser Datenbank gespeicherten Informationen werden verwendet, um den Dateiprüfungsüberwachung Bericht zu generieren.

> [!Important]
> Wenn die Aktivität zum Überprüfen der Daten **Satz Datei im** Kontrollkästchen Überwachungs Datenbank deaktiviert ist, enthalten die Dateiprüfungsüberwachung Berichte keine Informationen.

## <a name="to-configure-file-screen-audit"></a>So konfigurieren Sie die Datei Bildschirm Überwachung

1.  Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf **Datei Server Ressourcen-Manager**, und klicken Sie dann auf **Optionen konfigurieren**. Das Dialogfeld **Optionen für den Ressourcen-Manager für Dateiserver** wird geöffnet.

2.  Aktivieren Sie auf der Registerkarte **Datei Bildschirm** Überwachung die **Aktivität Dateiüberprüfung aufzeichnen im** Kontrollkästchen Datenbank überwachen.

3.  Klicken Sie auf **OK**. Alle Datei Überprüfungs Aktivitäten werden nun in der Überwachungs Datenbank gespeichert und können angezeigt werden, indem ein Dateiprüfungsüberwachung Bericht ausgeführt wird.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)
-   [Speicherberichtmanagement](storage-reports-management.md)