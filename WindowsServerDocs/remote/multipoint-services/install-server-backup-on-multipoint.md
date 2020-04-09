---
title: Installieren der Server Sicherung auf dem Multipoint-Server
description: Führt Sie durch die Schritte zum Installieren der Sicherungs-und Wiederherstellungs Tools
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: e4331370-ba07-4529-92ab-db14a41bfc3b
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: f8fe5ac8b57105d421af431b12c8dc17250b622d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80820333"
---
# <a name="install-server-backup-on-your-multipoint-server"></a>Installieren der Server Sicherung auf dem Multipoint-Server
Es wird empfohlen, dass Sie einen Sicherungs-und Wiederherstellungs Plan für Ihre Multipoint-Server in Erwägung gezogen.
  
Ein guter Sicherungs-und Wiederherstellungs Plan ist für jede Größen Umgebung wichtig. Windows Server-Sicherung ist ein Feature in Windows Server 2016, das eine Reihe von Assistenten und anderen Tools bereitstellt, mit denen Sie grundlegende Sicherungs-und Wiederherstellungs Aufgaben für den Server ausführen können, auf dem es installiert ist. Sie können Windows Server-Sicherung verwenden, um einen vollständigen Server (alle Volumes), ausgewählte Volumes, den Systemstatus oder bestimmte Dateien oder Ordner zu sichern und eine Sicherung zu erstellen, die Sie zum Neuerstellen des Systems verwenden können.  
  
Sie können Volumes, Ordner, Dateien, bestimmte Apps und den Systemstatus wiederherstellen. Und bei Notfällen wie Festplattenfehlern können Sie ein System entweder von Grund auf neu oder mithilfe alternativer Hardware neu erstellen. Zu diesem Zweck müssen Sie über eine Sicherung des vollständigen Servers oder nur der Volumes verfügen, die Betriebssystemdateien und die Windows-Wiederherstellungs Umgebung enthalten. Dadurch wird das gesamte System auf dem alten System oder auf einer neuen Festplatte wieder hergestellt.  
  
Ein wichtiges Feature von Windows Server-Sicherung ist die Möglichkeit, Sicherungen für die automatische Ausführung zu planen.  
  
Verwenden Sie die folgenden Verfahren, um den erforderlichen Sicherungstyp einzurichten.  
  
## <a name="install-backup-and-recovery-tools"></a>Installieren von Sicherungs-und Wiederherstellungs Tools  
  
1.  Öffnen Sie auf dem **Start** Bildschirm **Server-Manager**.  
  
2.  Klicken Sie zum Starten des Assistenten zum Hinzufügen von Rollen auf **Rollen und Features hinzufügen** . Klicken Sie dann auf **weiter** , nachdem Sie die Anmerkungen zu **Beginn** überprüft haben.  
  
3.  Wählen Sie die Option **rollenbasierte oder featurebasierte Installation** aus, und klicken Sie dann auf **weiter**.  
  
4.  Wählen Sie den lokalen Computer aus, den Sie verwalten möchten, und klicken Sie auf **weiter**.  
  
    Daraufhin wird der Assistent zum Hinzufügen von Funktionen geöffnet.  
  
5.  Erweitern Sie auf der Seite **Features auswählen** die Option Windows Server-Sicherung Features, aktivieren Sie die Kontrollkästchen für **Windows Server-Sicherung** und **Befehlszeilen Tools**, und klicken Sie dann auf **weiter**.  
  
    > [!NOTE]  
    > Wenn Sie nur das Snap-in und das Befehlszeilen Tool Wbadmin installieren möchten, erweitern Sie **Windows Server-Sicherung Features**, und aktivieren Sie dann nur das Kontrollkästchen **Windows Server-Sicherung** – Vergewissern Sie sich, dass das Kontrollkästchen **Befehlszeilen Tools** deaktiviert ist.  
  
6.  Überprüfen Sie Ihre Auswahl auf der Seite **Installations Auswahl bestätigen** , und klicken Sie dann auf **Installieren**.  
  
    Wenn während der Installation Fehler auftreten, werden die Fehler auf der Seite **Installations Ergebnisse** angezeigt.  
  
7.  Nachdem die Installation erfolgreich abgeschlossen wurde, sollten Sie in der Lage sein, auf diese Sicherungs-und Wiederherstellungs Tools zuzugreifen:  
  
    -   Um das Windows Server-Sicherung Snap-in zu öffnen, geben Sie auf dem **Start** Bildschirm **Backup**ein, und klicken Sie dann in den Ergebnissen auf **Windows Server-Sicherung** .  
  
    -   Zum Starten des Wbadmin-Tools und Anzeigen der Syntax für die zugehörigen Befehle: Geben Sie auf dem **Start** Bildschirm **Command**ein. Klicken Sie in den Ergebnissen mit der rechten Maustaste auf **Eingabeaufforderung**, klicken Sie unten auf der Seite auf **als Administrator ausführen** , und klicken Sie dann an der Bestätigungsaufforderung auf **Ja** . Geben Sie an der Eingabeaufforderung **Wbadmin/?** ein. und drücken Sie die EINGABETASTE. Es sollten Befehlssyntax und Beschreibungen für das Tool angezeigt werden.  
  
## <a name="configure-backups-using-windows-server-backup"></a>Konfigurieren von Sicherungen mithilfe von Windows Server-Sicherung  
  
-   Befolgen Sie die Anweisungen unter [Sichern des Servers](https://technet.microsoft.com/library/cc753528.aspx). 