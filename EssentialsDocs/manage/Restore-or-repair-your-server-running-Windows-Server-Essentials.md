---
title: Wiederherstellen oder Reparieren des Servers mit Windows Server Essentials
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 27bf6f24-30c4-4935-9b24-069eb43e22f4
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 5618eb95fb8afcff2057575191699da05612a542
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433064"
---
# <a name="restore-or-repair-your-server-running-windows-server-essentials"></a>Wiederherstellen oder Reparieren des Servers mit Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials
 
 Dieses Thema bietet eine Übersicht sowie unterstützende Verfahren bezüglich des Wiederherstellens oder Reparierens eines Servers mit Windows Server Essentials und umfasst die folgenden Abschnitte:  
  
-   [Übersicht über die des Serversystems](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Overview)  
  
-   [Wiederherstellen oder Reparieren des Systemlaufwerks](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore)  
  
-   [Wiederherstellen von Dateien und Ordner auf dem server](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFilesAndFolders)  
  
##  <a name="BKMK_Overview"></a> Übersicht über die des Serversystems  
 Beim Ausführen einer Wiederherstellung wirkt sich der Status des Servers auf die verfügbare Wiederherstellungsmethode aus und darauf, wie umfassend Sie eine Wiederherstellung durchführen können.  
  
 Die häufigsten Gründe für die Wiederherstellung eines Servers sind im Folgenden aufgeführt:  
  
- Ein Virus auf dem Server kann nicht bekämpft oder gelöscht werden.  
  
- Die Konfigurationseinstellungen des Servers sind unzureichend, und der Server kann nicht gestartet werden.  
  
- Sie haben das Systemlaufwerk ausgetauscht.  
  
- Sie nehmen den Server außer Betrieb. Sie möchten eine Wiederherstellung auf einem neuen Server durchführen.  
  
  Sie können den Server entweder mithilfe von Sicherheitskopien oder über die werkseitigen Standardeinstellungen wiederherstellen.  
  
- [Wiederherstellen des Servers aus einer Sicherung](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFromBackup)  
  
- [Zurücksetzen des Servers auf die werkseitigen Standardeinstellungen](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_FactoryReset)  
  
###  <a name="BKMK_RestoreFromBackup"></a> Wiederherstellen des Servers aus einer Sicherung  
 Dieser Abschnitt enthält Anleitungen in Bezug auf die Auswahl der Sicherungsart.  
  
 Wenn eine Sicherung verfügbar ist, werden die beste Wahl zum Wiederherstellen des Servers ab, die Installationsmedien des Herstellers s zu verwenden, um aus einer externen Sicherung wiederherzustellen. Durch die Wiederherstellung werden die von Ihnen ausgewählten Servereinstellungen und -ordner aus den Sicherheitskopien erneut abgerufen und angewendet. Sie müssen lediglich die entsprechenden Einstellungen konfigurieren und die nach der Sicherung erstellten Daten wiederherstellen.  
  
 Wenn Sie den Server über eine frühere Sicherung wiederherstellen möchten, wählen Sie die konkrete Sicherheitskopie, die für die Wiederherstellung angewendet werden soll. Sie benötigen dafür eine gültige Sicherungsdatei auf einem externen Festplattenlaufwerk, das direkt mit dem Server verbunden ist:  
  
- **Wenn Sie erst vor Kurzem eine Sicherung des Servers erfolgreich durchgeführt haben** und Sie wissen, dass in der Sicherung sämtliche Ihrer kritischen Daten enthalten sind, verläuft Ihre Auswahl recht unkompliziert. Sie müssen nur jene Daten neu erstellen, die nach der letzten erfolgreichen Sicherung erstellt wurden. Außerdem müssen Sie die nach der Sicherung vorgenommenen Einstellungsänderungen neu konfigurieren.  
  
- **Wenn Sie die Wiederherstellung des Servers aufgrund eines Virus durchführen**, wählen Sie Sicherheitskopien, bei denen Sie sicher sind, dass sie vor dem Auftreten des Virus erstellt wurden. Sie müssen möglicherweise mehrere Tage zurückdatieren, um eine Sicherung auszuwählen, die einwandfrei ist.  
  
- **Wenn Sie den Server wegen fehlerhafter Konfigurationseinstellungen wiederherstellen**, wählen Sie eine Sicherung, von der Sie wissen, dass sie vor der Konfigurationseinstellungsänderung vorgenommen wurde, welche das Problem auf dem Server verursacht hat.  
  
  Wenn Sie eine Wiederherstellung über eine Sicherung vornehmen, hängen das genaue Vorgehen und die erforderlichen Folgemaßnahmen von der Anzahl der Festplatten auf dem Server sowie davon ab, ob das Systemlaufwerk ersetzt wird:  
  
- **Wenn der Server über eine einzelne Festplatte verfügt und das Laufwerk nicht ersetzt wird**, bleiben die Informationen zur Laufwerkspartition beim Wiederherstellen des Servers unberührt. Das Systemvolumen wird wiederhergestellt, und die Daten auf dem verbleibenden Datenträger werden beibehalten.  
  
- **Wenn der Server über eine einzelne Festplatte verfügt und das Laufwerk ersetzt wird**, so wird das Systemvolumen wiederhergestellt. Sie müssen dann die Ordner für die Datenträger manuell wiederherstellen. Alle nicht standardmäßig freigegebenen Ordner müssen erstellt werden, da diese nicht erstellt werden, wenn der Serverspeicher neu erstellt wird.  
  
- **Wenn der Server über mehrere Festplatten verfügt und Laufwerk 0 (enthält das Systemvolumen) nicht ersetzt wird**, bleiben die Informationen zur Laufwerkspartition beim Wiederherstellen des Servers unberührt. Das Systemvolumen wird wiederhergestellt, und die Daten auf allen verbleibenden Datenträgern werden beibehalten.  
  
- **Wenn der Server über mehrere Festplatten verfügt und Laufwerk 0 (enthält das Systemvolumen) ersetzt wird**, so wird das Systemvolumen wiederhergestellt. Sie müssen dann alle freigegebenen Ordner, die zuvor auf Laufwerk 0 gespeichert waren, manuell wiederherstellen.  
  
###  <a name="BKMK_FactoryReset"></a> Zurücksetzen des Servers auf die werkseitigen Standardeinstellungen  
 Wenn Sie über keine Sicherheitskopien verfügen, über die Sie eine Wiederherstellung vornehmen können, oder wenn Sie aus einem anderen Grund eine vollständige Systemwiederherstellung durchführen möchten oder müssen, ohne die vorherige Serverkonfiguration wiederherzustellen, können Sie eine Wiederherstellung durchführen, die den Server auf die werkseitigen Standardeinstellungen zurückgesetzt, indem Sie die Installations- oder Wiederherstellungsmedien vom Hardware-Hersteller verwenden.  
  
 Wenn Sie den Server wiederherstellen, indem Sie ihn auf die werkseitigen Standardeinstellungen zurücksetzen, werden sämtliche vorhandenen Einstellungen und installierten Anwendungen auf dem Server gelöscht. Sie müssen den Server dann erneut konfigurieren. Nach dem Zurücksetzen auf die Werkseinstellungen muss der Server neu starten.  
  
 Beim Zurücksetzen auf die Werkseinstellungen können Sie wählen, ob Sie Ihre Daten beibehalten oder löschen möchten. Dabei müssen Sie die folgenden Auswirkungen beachten:  
  
-   Wenn Sie sämtliche Ihrer Daten beibehalten möchten, werden alle Daten im Systemvolumen gelöscht. Die Daten auf anderen Volumen werden jedoch beibehalten.  
  
    > [!CAUTION]
    >  Wenn die Datenträgereinstellungen nicht den Standardeinstellungen entsprechen, werden alle Daten auf einem betreffenden Datenträger gelöscht. Wenn Sie den Systemdatenträger ersetzt haben, muss der neue Datenträger größer als der ursprüngliche Datenträger s Systemvolume sein.  
    >   
    >  Falls die Partitionsinformationen für ein Systemlaufwerk nicht gelesen werden können, oder falls Sie das Systemlaufwerk ersetzen, werden alle Daten auf dem Systemlaufwerk entfernt, auch wenn Sie alle Ihre Daten beibehalten möchten.  
  
-   Wenn Sie den Server außer Betrieb nehmen oder für einen anderen Zweck verwenden möchten, wählen Sie die Löschung all Ihrer Daten. Neben der Serverkonfiguration, weiteren Einstellungen und den Daten im Systemvolumen werden alle anderen Daten gelöscht und alle Festplatten auf dem Server neu formatiert.  
  
> [!NOTE]
>  Wenn Speicherplätze auf dem Server konfiguriert werden, bevor Sie ein Zurücksetzen auf die Werkseinstellungen vornehmen, sollten Sie den Abschnitt **Erweitert** der Konsole **Verwalten von Speicherplätzen** anwenden, um alle Speicherplätze manuell zu entfernen.  
  
 Nach dem Zurücksetzen auf die Werkseinstellungen müssen Sie die folgenden Aufgaben ausführen:  
  
-   **Konfigurieren Sie den Server neu.** Verwenden Sie auf dem Server den Assistenten zum Konfigurieren von Servern, um die Konfigurationseinstellungen erneut einzugeben. Um einen per Fernzugriff verwalteten Windows Server Essentials-Server auf einem Clientcomputer zu konfigurieren, öffnen Sie einen Webbrowser, und geben Sie dann **http://***<YourServerName\>*  in der Adressleiste.  
  
-   **Verbinden Sie Clientcomputer erneut mit dem Server** Wenn ein Computer zuvor mit dem Server verbunden war, müssen Sie die Windows Server Essentials Connector-Software vom Computer deinstallieren, bevor Sie den Computer erneut mit dem Server verbinden. Weitere Informationen finden Sie unter [Uninstall the Connector software](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_13) und [Connect computers to the server](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9).  
  
##  <a name="BKMK_Restore"></a> Wiederherstellen oder Reparieren des Systemlaufwerks  
 Der erste Schritt bei der Serverwiederherstellung besteht darin, das Server-Systemlaufwerk wiederherzustellen oder zu reparieren. Nachdem Sie das Systemlaufwerk wiederhergestellt haben, führen Sie alle zum Wiederherstellen der Datenlaufwerke erforderlichen Maßnahmen durch. Stellen Sie außerdem sämtliche Freigabedaten wieder her, die bei der Wiederherstellung verloren gegangen sind.  
  
 Für die Wiederherstellung stehen drei Methoden zur Verfügung:  
  
-   [Wiederherstellen oder Reparieren des Servers mithilfe des Installationsmediums](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore_1). Verwenden Sie die Installationsmedien des Server-Herstellers, um die Wiederherstellung über Sicherheitskopien durchzuführen.  
  
-   **Verwenden Sie die Installationsmedien, um den Server auf die Werkseinstellungen zurückzusetzen**. Informationen darüber, welche Schritte Sie dafür am Server vornehmen müssen, finden Sie in der Dokumentation des Serverherstellers.  
  
-   [Wiederherstellen oder Zurücksetzen des Servers von einem Client-Computer mit der Wiederherstellungs-DVD](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore_2). Wenn Sie müssen einen per Fernzugriff verwalteten Server wiederherstellen, auf der Windows Server Essentials ausgeführt wird, müssen Sie die Wiederherstellung von einem Clientcomputer durchführen, mit der Wiederherstellungs-DVD des serverherstellers.  
  
###  <a name="BKMK_Restore_1"></a> Wiederherstellen Sie oder reparieren Sie des Servers mithilfe der Installationsmedien  
 Das folgende Verfahren beschreibt das Systemlaufwerk des Servers aus einer Sicherung wiederherstellen, indem Sie mithilfe des Installationsmediums für Windows Server Essentials. (Um herauszufinden, wie die Installationsmedien eingesetzt werden, um die werkseitigen Standardeinstellungen wiederherzustellen, lesen Sie die Dokumentation des Serverherstellers).  
  
> [!NOTE]
>  Wenn der Server Speicherplätze verwendet und Sie die Daten auf einem neuen Server wiederherstellen, sollten Sie das Systemlaufwerk zuerst wiederhergestellt und melden Sie sich bei Windows Server Essentials-Dashboard, Speicherplätze auf ähnliche Weise wie auf dem alten Server konfigurieren und anschließend wiederherstellen, das Datenzugriffstool ein Datenträger.  
  
##### <a name="to-restore-the-server-system-drive-from-a-backup-using-installation-media"></a>So stellen Sie das Server-Systemlaufwerk über eine Sicherung mithilfe der Installationsmedien wieder her  
  
1.  Fügen Sie der Windows Server Essentials-Installations-DVD in das DVD-Laufwerk des Servers, starten Sie den Server neu, und drücken Sie dann auf eine beliebige Taste, um von der DVD zu starten.  
  
    > [!NOTE]
    >  Wenn der Wiederherstellungsvorgang nicht automatisch gestartet wird, überprüfen Sie die BIOS-Einstellungen für den Server, um sicherzustellen, dass das DVD-Laufwerk an erster Stelle im Boot-Menü steht.  
  
     – Oder –  
  
     Wenn der Hersteller die Installationsmedien vorab auf den Server geladen hat, drücken Sie beim Start die Taste F8, um die Installationsmedien aufzurufen und zu starten.  
  
2.  Nachdem die Windows Server-Dateien geladen werden, wählen Sie Ihre Sprache und die weiteren Präferenzen. Klicken Sie anschließend auf **Weiter**.  
  
3.  Klicken Sie auf der nächsten Seite des Assistenten auf **Computer reparieren**.  
  
    > [!CAUTION]
    >  Wählen Sie nicht die Option **Jetzt installieren** . Diese Option führt Sie durch eine vollständige Systeminstallation, bei der alle Konfigurationseinstellungen und alle Daten auf dem Systemlaufwerk gelöscht werden.  
  
4.  Klicken Sie auf der Seite **Wählen Sie eine Option** auf **Problembehandlung**.  
  
5.  Auf der **Systemabbild-Wiederherstellung** Seite, wählen Sie das aktuelle System? entweder **Windows Server Essentials** oder **Windows Server Essentials**.  
  
     Der Assistent zum erneuten Abbilden des Computers wird geöffnet.  
  
6.  Sie können auf der Seite **Auswählen einer Systemabbildsicherung** wählen, ob Sie die neueste Sicherung oder eine frühere Sicherung verwenden möchten. Das System wird in jenen Zustand zurückversetzt, der zum Zeitpunkt jener Sicherung aktuell war, die Sie zum Wiederherstellen oder Reparieren des Server heranziehen. Hinzugefügte Daten oder Änderungen an den Einstellungen, die nach dem Speichern der Sicherheitskopien vorgenommen wurden, müssen neu erstellt bzw. neu erfasst werden.  
  
     Wählen Sie eine der folgenden Optionen aus, und klicken Sie dann auf **Weiter**:  
  
    -   **Verwenden Sie das neueste verfügbare Systemabbild (empfohlen)**  
  
    -   **Wählen Sie ein Systemabbild**  
  
    > [!NOTE]
    >  Wenn Sie erst vor Kurzem eine Sicherung des Servers erfolgreich durchgeführt haben, und Sie wissen, dass in der Sicherung sämtliche Ihrer kritischen Daten enthalten sind, verläuft Ihre Auswahl recht unkompliziert. Sie müssen nur jene Daten neu erstellen, die nach der letzten erfolgreichen Sicherung erstellt wurden. Außerdem müssen Sie die nach der Sicherung vorgenommenen Einstellungsänderungen neu konfigurieren.  
    >   
    >  Wenn Sie die Wiederherstellung des Servers aufgrund eines Virus durchführen, wählen Sie Sicherheitskopien, bei denen Sie sicher sind, dass sie vor dem Auftreten des Virus erstellt wurden. Sie müssen möglicherweise mehrere Tage zurückdatieren, um eine Sicherung auszuwählen, die einwandfrei ist.  
    >   
    >  Wenn Sie den Server wegen fehlerhafter Konfigurationseinstellungen wiederherstellen, wählen Sie eine Sicherung, von der Sie wissen, dass sie vor der Konfigurationseinstellungsänderung vorgenommen wurde, welche das Problem auf dem Server verursacht hat.  
  
7.  Befolgen Sie die Anweisungen im Assistenten, um die Systemwiederherstellung abzuschließen.  
  
8.  Nachdem der Server erfolgreich wiederhergestellt ist, entfernen Sie die Installations-DVD, wenn Sie eine solche verwendet haben. Starten Sie danach den Server neu.  
  
> [!NOTE]
>  Zum Wiederherstellen und Freigeben von Ordnern auf dem Server müssen Sie eventuell zusätzliche Schritte durchführen. Weitere Informationen finden Sie unter [Restore files and folders on the server](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFilesAndFolders).  
  
###  <a name="BKMK_Restore_2"></a> Wiederherstellen Sie oder Zurücksetzen Sie des Servers von einem Clientcomputer mit der Wiederherstellungs-DVD  
 In Windows Server Essentials können Sie den Server von starten einen startbaren USB-Speicherstick, die Sie erstellen, und klicken Sie dann Sie den Server wiederherstellen auf einem Clientcomputer mithilfe der Wiederherstellungs-DVD, die Sie vom Hersteller Servers erhalten haben. Der Clientcomputer muss sich im selben Netzwerk wie der Server befinden. Diese Methode ist nicht in Windows Server Essentials verfügbar.  
  
 Das folgende Verfahren umfasst allgemeine Schritte zum Ausführen einer Server-Wiederherstellung. Die Schritte gelten gleichermaßen für das Wiederherstellen über Sicherheitskopien wie auch für das Zurücksetzen auf die werkseitigen Standardeinstellungen. Weitere ausführliche Anweisungen finden Sie in der Dokumentation des Serverherstellers.  
  
##### <a name="to-restore-or-reset-the-server-from-a-client-computer-using-the-recovery-dvd"></a>So stellen Sie den Server von einem Clientcomputer aus mit der Wiederherstellungs-DVD wieder her oder setzen diesen zurück  
  
1.  Fügen Sie die Windows Server Essentials-Server-Wiederherstellungsmedien, die Sie vom Server-Hersteller auf einem Clientcomputer zu erhalten.  
  
     Der Assistent zum Wiederherstellen des Servers wird geöffnet.  
  
2.  Befolgen Sie die Anweisungen im Assistenten, um einen bootfähigen USB-Speicherstick einzurichten, mit dem Sie den Server im Wiederherstellungsmodus starten können.  
  
3.  Nachdem der Assistent zum Wiederherstellen des Servers den bootfähigen USB-Speicherstick vorbereitet hat, stecken Sie den Speicherstick am Server ein. Starten Sie dann den Server im Wiederherstellungsmodus. Lesen Sie die Dokumentation des Herstellers der Server-Hardware, um zu erfahren, wie Sie den Server im Wiederherstellungsmodus starten.  
  
     Nachdem Sie den Server im Wiederherstellungsmodus gestartet haben, ermittelt der Assistent zur Server-Wiederherstellung den Server und stellt dann eine Verbindung her.  
  
4.  Befolgen Sie die Anweisungen im Assistenten, um das Wiederherstellen des Servers abzuschließen.  
  
> [!NOTE]
>  Bei dieser Methode der Server-Wiederherstellung werden externe Speichergeräte, die während der Wiederherstellung mit dem Server verbunden sind, nicht beachtet. Wenn Sie die Daten auf einem externen Speichergerät löschen möchten, müssen Sie dies manuell tun.  
  
> [!NOTE]
>  Wenn Sie nach dem Wiederherstellen der Daten über eine Sicherung zusätzliche freigegebene Ordner auf dem Server erstellt haben, werden diese zusätzlichen freigegebenen Ordner unter Umständen nicht vom Server erkannt. Sie müssen diese Ordner erneut freigeben. Weitere Informationen finden Sie unter [Restore files and folders on the server](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFilesAndFolders).  
  
##  <a name="BKMK_RestoreFilesAndFolders"></a> Wiederherstellen von Dateien und Ordner auf dem server  
 Je nach der Methode, die Sie zur Wiederherstellung oder Reparatur des Servers verwenden, und je nach dem vom Server verwendeten Speichertyp müssen Sie die Datenvolumen eventuell wiederherstellen, nachdem Sie das Systemlaufwerk wiederhergestellt haben. In einigen Fällen müssen Sie vorhandene Ordner eventuell erneut freigeben, damit der Server sie erkennt.  
  
 Im Folgenden sind einige Beispiele von Fällen aufgeführt, in denen Sie Dateien und Ordner unter Umständen wiederherstellen müssen:  
  
-   [Wiederherstellen von Dateien und Ordnern über eine Server-Sicherung](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFilesFromBackup). Wenn Sie den Systemdatenträger ersetzt haben oder die Partitionsinformationen auf dem Systemdatenträger nicht lesbar sind, können Sie das System wiederherstellen. Sie können allerdings keine Daten von anderen Volumen auf diesem Datenträger wiederherstellen. Zum Wiederherstellen von Dateien und Ordnern aus anderen Datenvolumen müssen Sie den Assistenten zum Wiederherstellen von Dateien und Ordnern verwenden.  
  
-   [Restore shared folders on the server](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_ConfigreSharedFolders). Wenn Sie nach dem Wiederherstellen des Systemlaufwerks über die Sicherung weitere freigegebene Ordner auf dem Server erstellen, befinden sich die freigegebenen Ordner weiterhin auf der Datenpartition oder werden in der Datenpartition wiederhergestellt. Sie werden aber möglicherweise vom Server nicht erkannt. Sie müssen diese Ordner erneut freigeben.  
  
###  <a name="BKMK_RestoreFilesFromBackup"></a> Wiederherstellen von Dateien und Ordnern aus einer Sicherung  
 Der Assistent zum Wiederherstellen von Dateien und Ordnern unterstützt Sie beim Schützen Ihrer Daten, wenn die Festplatte nicht mehr funktioniert oder Dateien versehentlich gelöscht werden. Mit Windows Server Essentials-Sicherung können Sie eine Kopie aller Daten auf der Festplatte erstellen und die Daten auf einem externen Speichergerät ablegen. Wenn die ursprünglichen Daten auf der Festplatte versehentlich gelöscht, überschrieben oder aufgrund einer Fehlfunktion unbrauchbar werden, können Sie die Daten über die Sicherung wiederherstellen. Der Assistent zum Wiederherstellen von Dateien oder Ordnern unterstützt Sie über vorhandene Sicherheitskopien bei der Wiederherstellung einer einzelnen Datei oder eines einzelnen Ordners, mehrerer Dateien oder Ordner oder einer kompletten Festplatte.  
  
 Nach einer Systemwiederherstellung müssen Sie möglicherweise den Assistenten zum Wiederherstellen von Dateien und Ordnern verwenden, um Dateien und Ordner wiederherzustellen, die während der Wiederherstellung nicht erfasst wurden. Wenn Sie beispielsweise den Systemdatenträger ersetzt haben oder die Partitionsinformationen auf dem Systemdatenträger unlesbar sind, können Sie Daten von anderen Volumen auf dem Systemdatenträger nicht wiederherstellen.  
  
> [!NOTE]
>  Sie können den Assistenten zum Wiederherstellen von Dateien und Ordnern nicht verwenden, um das komplette Systemlaufwerk wiederherzustellen. Informationen darüber, wie Sie das komplette System wiederherstellen können, finden Sie unter [Restore or repair your server using installation media](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore_1) oder [Restore or reset your server from a client computer using the recovery DVD](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore_2).  
  
##### <a name="to-restore-files-and-folders-from-a-server-backup"></a>So stellen Sie Dateien und Ordner über eine Server-Sicherung wieder her  
  
1.  Öffnen Sie Windows Server Essentials-Dashboard, und klicken Sie dann auf die **Geräte** Registerkarte.  
  
2.  Klicken Sie auf den Namen des Servers und anschließend auf **Wiederherstellen von Dateien oder Ordnern für den Server** im Bereich **Aufgaben**.  
  
     Der Assistent zum Wiederherstellen von Dateien und Ordnern wird geöffnet.  
  
3.  Befolgen Sie die Anweisungen im Assistenten, um die Dateien oder Ordner wiederherzustellen.  
  
> [!WARNING]
>  Weitere Informationen zum Sichern und Wiederherstellen von Dateien und Ordnern finden Sie unter [Manage Backup and Restore](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md).  
  
###  <a name="BKMK_ConfigreSharedFolders"></a> Wiederherstellen von freigegebenen Ordnern auf dem server  
 Nachdem Sie das Systemlaufwerk Server s wiederherstellen, wenn freigegebene Ordner befinden sich weiterhin auf der Datenpartition oder auf der Datenpartition wiederhergestellt wurden, müssen Sie konfigurieren die freigegebenen Ordner erneut, damit für den Server die Ordner erkennen. Im folgenden Verfahren wird beschrieben, wie freigegebene Ordner hinzuzufügen sind, die bereits zuvor einmal freigegeben waren.  
  
##### <a name="to-add-an-existing-folder-to-the-server-shared-folders"></a>So fügen Sie einen vorhandenen Ordner zu den freigegebenen Ordnern des Servers hinzu  
  
1.  Suchen Sie im Datei-Explorer den freigegebenen Ordner auf dem Festplattenlaufwerk.  
  
2.  Klicken Sie mit der rechten Maustaste auf den freigegebenen Ordner. Klicken Sie dann auf **Eigenschaften**und auf die Registerkarte **Freigabe** . Notieren Sie sich anschließend die Ordnerberechtigungen.  
  
3.  Melden Sie sich bei Windows Server Essentials-Dashboard, klicken Sie auf die **Storage** Registerkarte, und klicken Sie dann auf **fügen Sie einen Ordner** in die **Tasks für Serverordner** Bereich.  
  
     Der Assistent zum Hinzufügen eines Ordners wird geöffnet.  
  
4.  Geben Sie einen Namen für die Freigabe im Feld **Name** ein.  
  
5.  Klicken Sie auf **Durchsuchen**, navigieren Sie zu *< Laufwerk\>\\< ServerName\>* \ServerFolders (z. B. *d:\Contoso\ServerFolders*), wählen Sie den Ordner, die Sie freigeben möchten, und klicken Sie dann auf **OK**.  
  
6.  Klicken Sie auf **Weiter**.  
  
7.  Geben Sie die Berechtigungen an, die Sie in Schritt 2 notiert haben. Klicken Sie dann auf **Ordner hinzufügen**.  
  
    > [!IMPORTANT]
    >  Diese Berechtigungen ersetzen alle vorhandenen Berechtigungen, die nicht in den Ordner hinzugefügt wurden, mithilfe von Windows Server Essentials-Dashboard.  
  
> [!IMPORTANT]
>  Nachdem Sie das Hinzufügen von Ordnern zur Liste der freigegebenen Ordner abgeschlossen haben, müssen Sie sicherstellen, dass die Ordner in der Server-Sicherung enthalten sind. Informationen zum Hinzufügen von Ordnern in die Server-Sicherung finden Sie unter [Einrichten oder Anpassen der Server-Sicherung](Set-up-or-customize-server-backup.md).  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten der Sicherung und Wiederherstellung](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)  
  
-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)
