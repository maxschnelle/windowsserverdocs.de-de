---
title: Installieren von Server-Sicherung auf dem MultiPoint-server
description: Führt Sie durch die Schritte zum Installieren der Tools für Sicherung und Wiederherstellung
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e4331370-ba07-4529-92ab-db14a41bfc3b
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 51932c5f0796cfd757d3322e10c17de2a3081f4c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832491"
---
# <a name="install-server-backup-on-your-multipoint-server"></a>Installieren von Server-Sicherung auf dem MultiPoint-server
Es wird empfohlen, dass Sie einen Plan für Sicherung und Wiederherstellung für Ihre MultiPoint-Server in Betracht ziehen.
  
Ein geeigneter Plan für Sicherung und Wiederherstellung ist wichtig für eine beliebige Größe-Umgebung. Windows Server-Sicherung ist ein Feature in Windows Server 2016, die bietet eine Reihe von Assistenten und anderen Tools für grundlegende Aufgaben für Sicherung und Wiederherstellung für den Server ausführen, auf dem er installiert ist. Sie können Windows Server-Sicherung verwenden, um einen vollständigen Server (alle Volumes), ausgewählte Volumes, die den Systemstatus oder bestimmte Dateien oder Ordner zu sichern, und klicken Sie zum Erstellen einer Sicherung, die Sie verwenden können, um Ihr System neu zu erstellen.  
  
Sie können Volumes, Ordner, Dateien, bestimmte Apps und den Systemstatus wiederherstellen. Und für Notfälle wie Festplattenausfall, können Sie ein System von Grund auf neu oder mithilfe der alternativen Hardware neu erstellen. Zu diesem Zweck benötigen Sie eine Sicherung des vollständigen Servers oder nur der Volumes, die Dateien des Betriebssystems und der Windows-Wiederherstellungsumgebung enthalten. Dadurch wird das gesamte System wird auf dem alten System oder auf einer neuen Festplatte wiederhergestellt.  
  
Ein wichtiges Feature von Windows Server-Sicherung ist die Möglichkeit zum Planen von Sicherungen, die automatisch ausgeführt.  
  
Verwenden Sie die folgenden Verfahren, um den Typ der Sicherung einrichten, die Sie benötigen.  
  
## <a name="install-backup-and-recovery-tools"></a>Installieren Sie die sicherungs-und Wiederherstellungstools  
  
1.  Von der **starten** öffnen **Server-Manager**.  
  
2.  Klicken Sie auf **Hinzufügen von Rollen und Features** um den Assistenten zum Hinzufügen von Rollen zu starten. Klicken Sie dann auf **Weiter** nach der Überprüfung der **vor dem Beginn** Anmerkungen zu dieser Version.  
  
3.  Wählen Sie die **rollenbasierten oder ein Feature-basierte Installation** aus, und klicken Sie dann auf **Weiter**.  
  
4.  Wählen Sie den lokalen Computer, die Sie verwalten möchten, und klicken Sie auf **Weiter**.  
  
    Daraufhin wird der Assistent zum Hinzufügen von Funktionen geöffnet.  
  
5.  Auf der **Features auswählen** Seite, erweitern Sie die Windows Server-Sicherungsfeatures, wählen Sie die Kontrollkästchen für **Windows Server-Sicherung** und **Befehlszeilentools**, und klicken Sie dann auf  **Nächste**.  
  
    > [!NOTE]  
    > Oder, wenn Sie das Snap-in und das Befehlszeilentool "Wbadmin" installieren möchten, erweitern Sie **Windows Server-Sicherungsfeatures**, und wählen Sie dann die **Windows Server-Sicherung** nur das Kontrollkästchen, stellen Sie sicher, dass die **Befehlszeilentools** ist das Kontrollkästchen deaktivieren.  
  
6.  Auf der **Installationsauswahl bestätigen** Seite überprüfen Sie Ihre Auswahl, und klicken Sie dann auf **installieren**.  
  
    Auftreten von Fehlern bei der Installation der **Installationsergebnisse** Seite werden die Fehler feststellen.  
  
7.  Nach erfolgreichem die Installation Abschluss sollten Sie auf diese Sicherung und Wiederherstellung-Tools zugreifen können:  
  
    -   Die Windows Server-Sicherung-Snap-in zum Öffnen der **starten** geben **backup**, und klicken Sie dann auf **Windows Server-Sicherung** in den Ergebnissen.  
  
    -   So starten Sie das Wbadmin-Tool, und zeigen die Syntax für die Befehle aus: Auf der **starten** geben **Befehl**. In den Ergebnissen mit der Maustaste **Eingabeaufforderung**, klicken Sie auf **als Administrator ausführen** am unteren Rand der Seite, und klicken Sie dann auf **Ja** zur Bestätigung aufgefordert. Geben Sie an der Eingabeaufforderung den Befehl **Wbadmin /?** ein, und drücken Sie die EINGABETASTE. Befehlssyntax und eine Beschreibung für das Tool sollte angezeigt werden.  
  
## <a name="configure-backups-using-windows-server-backup"></a>Konfigurieren von Sicherungen mit Windows Server-Sicherung  
  
-   Führen Sie die Anleitung im [Sichern des Servers](https://technet.microsoft.com/library/cc753528.aspx). 