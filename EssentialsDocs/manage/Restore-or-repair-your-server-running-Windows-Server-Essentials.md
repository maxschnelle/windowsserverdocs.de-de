---
title: Wiederherstellen Sie oder reparieren Sie des Servers mit Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
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
ms.openlocfilehash: e1ebc539928d13b0d34dfe5a0ee57ce6e98088e9
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="restore-or-repair-your-server-running-windows-server-essentials"></a>Wiederherstellen Sie oder reparieren Sie des Servers mit Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials
 
 Dieses Thema bietet eine Übersicht sowie unterstützende Verfahren bezüglich des Wiederherstellens oder Reparierens eines Servers mit Windows Server Essentials und umfasst die folgenden Abschnitte:  
  
-   [Übersicht über die des Serversystems](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Overview)  
  
-   [Wiederherstellen oder Reparieren des Systemlaufwerks](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore)  
  
-   [Wiederherstellen von Dateien und Ordnern auf dem Server](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFilesAndFolders)  
  
##  <a name="BKMK_Overview"></a>Übersicht über die des Serversystems  
 Der Status des Servers beim Ausführen einer Wiederherstellung wirkt sich auf die Restore-Methode, die verfügbar ist und wie umfassend eine Wiederherstellung durchführen können.  
  
 Die häufigsten Gründe für die Wiederherstellung eines Servers sind:  
  
-   Ein Virus auf dem Server kann nicht bekämpft oder gelöscht werden.  
  
-   Konfigurationseinstellungen des Servers sind unzureichend, und Sie können den Server nicht starten.  
  
-   Sie können das Systemlaufwerk ausgetauscht.  
  
-   Werden Sie den Server abkoppeln, und Sie zu einem neuen Server wiederherstellen möchten.  
  
 Sie können entweder den Server aus einer Sicherung wiederherstellen, oder Sie können den Server wiederherstellen, um die werkseitigen Standardeinstellungen.  
  
-   [Wiederherstellen des Servers aus einer Sicherung](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFromBackup)  
  
-   [Zurücksetzen des Servers auf die werkseitigen Standardeinstellungen](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_FactoryReset)  
  
###  <a name="BKMK_RestoreFromBackup"></a>Wiederherstellen des Servers aus einer Sicherung  
 Dieser Abschnittenthält Richtlinien, auf welche Art der Sicherung auswählen.  
  
 Wenn eine Sicherung verfügbar ist, ist die beste Wahl zum Wiederherstellen des Servers mit dem Hersteller s-Installationsmedium aus einer externen Sicherung wiederherstellen. Die Wiederherstellung wird servereinstellungen und Ordner aus der Sicherung wiederherstellen, die Sie auswählen. Sie müssen nur konfigurieren, und nach der Sicherung erstellten Daten wiederherstellen.  
  
 Wenn Sie den Server wiederherstellen, indem Sie aus einer früheren Sicherung wiederherstellen möchten, wählen Sie die konkrete Sicherung, die wiederhergestellt werden sollen, und benötigen Sie eine gültige Sicherungsdatei auf einer externen Festplatte, die direkt mit dem Server verbunden ist:  
  
-   **Wenn Sie eine möglichst aktuelle erfolgreiche Sicherung des Servers haben**, und Sie wissen, dass die Sicherung enthält alle wichtigen Daten Ihrer Wahl ist recht einfach. Sie müssen nur jene Daten neu erstellen, die erstellt wurde, nachdem Ihre letzten guten Sicherung und neu konfigurieren Einstellungen nach der Sicherung geändert.  
  
-   **Wenn Sie den Server aufgrund eines Virus wiederherstellen**, wählen Sie eine Sicherung, die Sie kennen, die vor dem Auftreten des Virus aufgetreten ist. Sie müssen möglicherweise mehrere Tage zurückdatieren, um eine Sicherung auszuwählen, die einwandfrei ist.  
  
-   **Wenn Sie den Server wegen fehlerhafter Konfigurationseinstellungen wiederherstellen**, wählen Sie eine Sicherung, die Sie kennen, die vor der Konfiguration, die Einstellung ändern, die das Problem auf dem Server verursacht aufgetreten ist.  
  
 Wenn Sie aus einer Sicherung wiederherstellen, hängen das genaue Vorgehen und die erforderlichen Folgemaßnahmen die Anzahl der Festplatten auf dem Server und gibt an, ob das Systemlaufwerk ersetzt wird:  
  
-   **Wenn der Server über eine einzelne Festplatte verfügt und das Laufwerk nicht ersetzt**, die Informationen zur Laufwerkspartition beim Wiederherstellen des Servers. Das Systemvolumen wird wiederhergestellt, und die Daten auf den verbleibenden Datenträger werden beibehalten.  
  
-   **Wenn der Server über eine einzelne Festplatte verfügt und das Laufwerk ersetzt**, das Systemvolumen wird wiederhergestellt, und Sie müssen dann manuell wiederherstellen Ordner für die Datenträger. Alle nicht standardmäßigen freigegebenen Ordner müssen erstellt werden, da sie nicht erstellt werden, wenn der Serverspeicher neu erstellt wird.  
  
-   **Wenn der Server über mehrere Festplatten verfügt und Laufwerk 0 (enthält das Systemvolumen) nicht ersetzt**, die Informationen zur Laufwerkspartition beim Wiederherstellen des Servers. Das Systemvolumen wird wiederhergestellt, und die Daten auf allen verbleibenden Datenträgern werden beibehalten.  
  
-   **Wenn der Server über mehrere Festplatten verfügt und Laufwerk 0 (enthält das Systemvolumen) ersetzt**, das Systemvolumen wird wiederhergestellt und müssen dann alle freigegebenen Ordner, die zuvor auf Laufwerk 0 gespeichert waren manuell wiederherstellen.  
  
###  <a name="BKMK_FactoryReset"></a>Zurücksetzen des Servers auf die werkseitigen Standardeinstellungen  
 Wenn Sie keine Sicherung haben, die Sie wiederherstellen können, aus oder einem anderen Grund möchten oder müssen eine vollständige Systemwiederherstellung ausführen, ohne die vorherige Serverkonfiguration wiederherzustellen, können Sie eine Wiederherstellung durchführen, die den Server auf die werkseitigen Standardeinstellungen zurückgesetzt werden, indem Sie mithilfe von Installations- oder Wiederherstellungsmedien vom Hardware-Hersteller.  
  
 Wenn Sie den Server wiederherstellen, indem Sie auf die werkseitigen Standardeinstellungen zurücksetzen, werden alle vorhandenen Einstellungen und installierten Programme auf dem Server gelöscht, und müssen Sie den Server erneut konfigurieren. Nach dem Zurücksetzen einer Factory der Server neu starten.  
  
 Wenn Sie auf die Werkseinstellungen Zurücksetzen ausführen, können Sie Ihre Daten beibehalten oder gelöscht werden soll, die folgenden Auswirkungen beachten:  
  
-   Wenn Sie alle Daten, werden alle Daten beibehalten möchten das Systemvolume wird gelöscht, aber die Daten auf anderen Datenträgern werden beibehalten.  
  
    > [!CAUTION]
    >  Wenn die datenträgereinstellungen nicht die Standardeinstellungen übereinstimmen, werden alle Daten auf einem Datenträger gelöscht werden. Wenn Sie den Systemdatenträger ersetzt haben, muss der neue Datenträger größer als das ursprüngliche Datenträger s Systemvolume sein.  
    >   
    >  Wenn die Partitionsinformationen für ein Systemlaufwerk nicht lesbar ist, oder wenn Sie das Systemlaufwerk ersetzen, alle Daten auf dem Systemlaufwerk, entfernt werden auch wenn Sie alle Ihre Daten beibehalten möchten.  
  
-   Wenn Sie außer Betrieb nehmen oder des Servers wiederverwenden möchten, wählen Sie alle Ihre Daten gelöscht. Zusätzlich zur Konfiguration des Servers, andere Einstellungen und Daten auf dem Systemdatenträger werden alle anderen Daten gelöscht, und alle Festplatten auf dem Server neu formatiert.  
  
> [!NOTE]
>  Wenn Speicherplätze auf dem Server konfiguriert ist, bevor Sie auf die Werkseinstellungen Zurücksetzen ausführen, verwenden Sie die **erweitert** Teil der **Verwalten von Speicherplätzen** Konsole alle Speicherplätze manuell zu entfernen.  
  
 Nach dem Zurücksetzen auf die Werkseinstellungen müssen Sie die folgenden Aufgaben ausführen:  
  
-   **Konfigurieren Sie den Server neu.** Verwenden Sie auf dem Server den Assistenten zum Konfigurieren von Server, um die Konfigurationseinstellungen erneut einzugeben. Um einen Remote verwalteten Windows Server Essentials-Server von einem Clientcomputer zu konfigurieren, öffnen Sie einen Webbrowser, und geben Sie dann **http://***< YourServerName\ >* in die Adressleiste.  
  
-   **Verbinden Sie Clientcomputer mit dem Server erneut.** Wenn ein Computer zuvor mit dem Server verbunden wurde, müssen Sie die Windows Server Essentials Connector-Software vom Computer deinstallieren, bevor Sie den Computer erneut mit dem Server verbinden. Weitere Informationen finden Sie unter [deinstallieren die Connector-Software](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_13) und [Verbinden von Computern mit dem Server](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9).  
  
##  <a name="BKMK_Restore"></a>Wiederherstellen oder Reparieren des Systemlaufwerks  
 Der erste Schrittbeim Wiederherstellen der Server ist zum Wiederherstellen oder Reparieren des Systemlaufwerks des Servers. Nachdem Sie das Systemlaufwerk wiederhergestellt haben, werden Sie tun, was zum Wiederherstellen der Datenlaufwerke auf dem Server und wieder her, die Freigabe, die bei der Wiederherstellung verloren gegangen erforderlich ist.  
  
 Für die Wiederherstellung stehen drei Methoden zur Auswahl:  
  
-   [Wiederherstellen oder Reparieren des Servers mithilfe eines Installationsmediums](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore_1). Verwenden Sie die Installationsmedien des serverherstellers aus einer Sicherung wiederherstellen.  
  
-   **Verwenden Sie die Installationsmedien zum Wiederherstellen des Servers auf die werkseitigen Standardeinstellungen**. Um herauszufinden, wie Sie hierzu auf dem Server, finden Sie in der Dokumentation des serverherstellers.  
  
-   [Wiederherstellen oder Zurücksetzen des Servers von einem Clientcomputer mit dem Wiederherstellungs-DVD](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore_2). Wenn Sie müssen einen Remote verwalteten Server wiederherstellen, auf der Windows Server Essentials ausgeführt wird, müssen Sie die Wiederherstellung von einem Clientcomputer ausführen, mithilfe der Wiederherstellungs-DVD des serverherstellers.  
  
###  <a name="BKMK_Restore_1"></a>Wiederherstellen Sie oder reparieren Sie des Servers mithilfe eines Installationsmediums  
 Im folgenden wird beschrieben, wie Sie das Systemlaufwerk des Servers aus einer Sicherung wiederherstellen, indem Sie mithilfe des Windows Server Essentials-Installationsmediums. (Um herauszufinden, wie Sie das Installationsmedium zu verwenden, um die werkseitigen Standardeinstellungen wiederherstellen, finden Sie in der Dokumentation des serverherstellers.)  
  
> [!NOTE]
>  Wenn der Server Speicherplätze verwendet und Sie die Daten auf einem neuen Server wiederherstellen, sollten Sie das Systemlaufwerk zunächst wiederherstellen und melden Sie sich bei Windows Server Essentials-Dashboard, Speicherplätze auf ähnliche Weise wie beim alten Server konfigurieren und dann die Datenvolumen wiederherstellen.  
  
##### <a name="to-restore-the-server-system-drive-from-a-backup-using-installation-media"></a>Das Server-Systemlaufwerk über eine Sicherung mithilfe eines Installationsmediums wiederherstellen  
  
1.  Legen Sie die Windows Server Essentials-Installations-DVD in das DVD-Laufwerk des Servers, starten Sie den Server neu, und drücken Sie dann eine beliebige Taste, um von der DVD zu starten.  
  
    > [!NOTE]
    >  Wenn der Wiederherstellungsvorgang nicht automatisch gestartet wird, überprüfen Sie die BIOS-Einstellungen für den Server, um sicherzustellen, dass das DVD-Laufwerk zuerst im Menü "Start" angezeigt wird.  
  
     – Oder –  
  
     Wenn der Hersteller die Installationsmedien auf dem Server geladen, drücken Sie F8 beim Systemstart, um von den Installationsmedien starten.  
  
2.  Nachdem die Windows Server Dateien laden, wählen Sie die Sprache und andere Einstellungen, und klicken Sie dann auf **Weiter**.  
  
3.  Klicken Sie auf der nächsten Seite des Assistenten auf **Computer reparieren**.  
  
    > [!CAUTION]
    >  Wählen Sie nicht die **jetzt installieren** Option. Diese Option führt Sie durch eine vollständige Installation, die alle Konfigurationseinstellungen und alle Daten auf dem Systemlaufwerk gelöscht.  
  
4.  Auf der **wählen Sie eine Option** auf **Problembehandlung**.  
  
5.  Auf der **Systemabbild-Wiederherstellung** Seite, wählen Sie das aktuelle System? entweder **Windows Server Essentials** oder **Windows Server Essentials**.  
  
     Der Assistent zum neues Abbild des Computers wird geöffnet.  
  
6.  Auf der **wählen Sie eine systemabbildsicherung** Seite, Sie können auch die neueste Sicherung verwenden, oder Sie können eine frühere Sicherung auswählen. Das System wird in den Zustand wiederhergestellt werden, in dem zum Zeitpunkt der Sicherung, die Sie auswählen, zum Wiederherstellen oder Reparieren des Server heranziehen. Hinzugefügte Daten oder Änderungen an den Einstellungen, die vorgenommen wurden, nachdem die Sicherung gespeichert wurde neu erstellt werden müssen.  
  
     Wählen Sie eine der folgenden Optionen aus, und klicken Sie dann auf **Weiter**:  
  
    -   **Verwenden Sie das neueste verfügbare Systemabbild (empfohlen)**  
  
    -   **Wählen Sie ein Systemabbild**  
  
    > [!NOTE]
    >  Wenn Sie eine möglichst aktuelle erfolgreiche Sicherung des Servers, und Sie wissen, dass die Sicherung alle wichtigen Daten enthält, ist Ihre Auswahl recht einfach. Sie müssen nur jene Daten neu erstellen, die erstellt wurde, nachdem Ihre letzten guten Sicherung und neu konfigurieren Einstellungen nach der Sicherung geändert.  
    >   
    >  Wenn Sie Ihre Server aufgrund eines Virus wiederherstellen möchten, wählen Sie eine Sicherung, die Sie kennen, vor dem Auftreten des Virus aufgetreten ist. Sie müssen möglicherweise mehrere Tage zurückdatieren, um eine Sicherung auszuwählen, die einwandfrei ist.  
    >   
    >  Wenn Sie den Server wegen fehlerhafter Konfigurationseinstellungen wiederherstellen möchten, wählen Sie eine Sicherung, die Sie kennen vor der konfigurationseinstellungsänderung ist aufgetreten, der das Problem auf dem Server verursacht.  
  
7.  Führen Sie die Anweisungen im Assistenten, um die Systemwiederherstellung abzuschließen.  
  
8.  Nachdem der Server erfolgreich wiederhergestellt wird, entfernen Sie die Installations-DVD zu, wenn Sie eine verwendet, und klicken Sie dann starten Sie den Server neu.  
  
> [!NOTE]
>  Zum Wiederherstellen und Freigeben von Ordnern auf dem Server, müssen Sie möglicherweise zusätzliche Schritteerforderlich. Weitere Informationen finden Sie unter [Wiederherstellen von Dateien und Ordnern auf dem Server](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFilesAndFolders).  
  
###  <a name="BKMK_Restore_2"></a>Wiederherstellen Sie oder Zurücksetzen Sie des Servers von einem Clientcomputer mit dem Wiederherstellungs-DVD  
 In Windows Server Essentials Sie können den Server von starten einen startbaren USB-Speicherstick, die Sie erstellen, und klicken Sie den Server Wiederherstellen von einem Clientcomputer mithilfe der Wiederherstellungs-DVD, die Sie vom Hersteller Servers erhalten haben. Der Clientcomputer muss sich im selben Netzwerk wie der Server. Diese Methode ist nicht verfügbar in Windows Server Essentials.  
  
 Das folgende Verfahren umfasst allgemeine Schrittezum Ausführen einer Wiederherstellung des Servers. Die Schrittegelten gleichermaßen für aus einer Sicherungskopie wiederherstellen oder auf die werkseitigen Standardeinstellungen wiederherstellen. Weitere ausführliche Anweisungen finden Sie in der Dokumentation des serverherstellers.  
  
##### <a name="to-restore-or-reset-the-server-from-a-client-computer-using-the-recovery-dvd"></a>Zum Wiederherstellen oder Zurücksetzen des Servers von einem Clientcomputer mit dem Wiederherstellungs-DVD  
  
1.  Legen Sie die Windows Server Essentials-Server Recovery-Medien, die Sie von den Hersteller des Servers in einen Clientcomputer empfangen.  
  
     Der Assistent zum Wiederherstellen des Servers wird geöffnet.  
  
2.  Führen Sie die Anweisungen im Assistenten, um einen startbaren USB-Speicherstick zu erstellen, den Sie verwenden, um den Server im Wiederherstellungsmodus starten.  
  
3.  Nachdem der Assistent zum Wiederherstellen des Servers den bootfähigen USB-Speicherstick vorbereitet hat, legen Sie das Flash-Laufwerk auf dem Server, und starten Sie den Server im Wiederherstellungsmodus. So erfahren Sie, wie Sie den Server im Wiederherstellungsmodus starten, finden Sie in der Dokumentation des Herstellers der Server-Hardware.  
  
     Nachdem Sie den Server im Wiederherstellungsmodus starten, wird der Assistent zum Wiederherstellen des Servers ermittelt den Server und stellt dann eine Verbindung her.  
  
4.  Folgen Sie den Anweisungen im Assistenten zum Wiederherstellen des Servers abzuschließen.  
  
> [!NOTE]
>  Diese Methode der Server-Wiederherstellung ignoriert externe Speichergeräte, die während der Wiederherstellung mit dem Server verbunden sind. Wenn Sie die Daten auf einem externen Speichergerät löschen möchten, müssen Sie dies manuell tun.  
  
> [!NOTE]
>  Wenn Sie zusätzliche freigegebene Ordner auf dem Server erstellt, nachdem Sie die Daten aus der Sicherung wiederherstellen, möglicherweise zusätzlichen freigegebenen Ordner vom Server nicht erkannt werden. Sie müssen diese Ordner erneut freigeben. Weitere Informationen finden Sie unter [Wiederherstellen von Dateien und Ordnern auf dem Server](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFilesAndFolders).  
  
##  <a name="BKMK_RestoreFilesAndFolders"></a>Wiederherstellen von Dateien und Ordnern auf dem Server  
 Je nach der Methode, die Sie zum Wiederherstellen oder Reparieren des Servers und der Typ des Speichers des Servers verwendet müssen Sie möglicherweise die Datenvolumen wiederherstellen, nachdem Sie das Systemlaufwerk wiederhergestellt haben. In einigen Fällen müssen Sie vorhandene Ordner erneut freigeben, damit der Server sie erkennt.  
  
 Es folgen einige Beispiele für müssen Sie u. u. auf Dateien und Ordner wiederherstellen:  
  
-   [Wiederherstellen von Dateien und Ordnern aus einer Sicherung](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFilesFromBackup). Wenn Sie den Systemdatenträger ersetzt, oder die Partitionsinformationen auf dem Systemdatenträger nicht lesbar ist, können Sie das System wiederherstellen, jedoch Daten von anderen Volumen auf diesem Datenträger können nicht wiederhergestellt werden können. Zum Wiederherstellen von Dateien und Ordnern aus anderen Datenvolumen müssen Sie das Wiederherstellen von Dateien und Ordner-Assistenten verwenden.  
  
-   [Wiederherstellen von freigegebenen Ordnern auf dem Server](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_ConfigreSharedFolders). Wenn Sie zusätzliche freigegebene Ordner auf dem Server erstellt, nachdem Sie das Systemlaufwerk aus der Sicherung wiederherstellen, die freigegebenen Ordner sind weiterhin auf der Datenpartition oder in der Datenpartition wiederhergestellt wurden, aber möglicherweise nicht vom Server erkannt werden. Sie müssen diese Ordner erneut freigeben.  
  
###  <a name="BKMK_RestoreFilesFromBackup"></a>Wiederherstellen von Dateien und Ordnern aus einer Sicherung  
 Wiederherstellen von Dateien und Ordner-Assistenten können Sie Ihre Daten schützen, wenn die Festplatte nicht mehr funktioniert oder Dateien versehentlich gelöscht. Mit Windows Server Essentials-Sicherung können Sie eine Kopie aller Daten auf der Festplatte erstellen und die Daten auf einem externen Speichergerät ablegen. Wenn die ursprünglichen Daten auf der Festplatte versehentlich gelöscht, überschrieben oder aufgrund einer Fehlfunktion nicht zugegriffen werden, können Sie die Daten aus der Sicherung wiederherstellen. Das Wiederherstellen von Dateien oder Ordner-Assistenten können Sie eine einzelne Datei oder Ordner, mehrere Dateien oder Ordner oder eine ganze Festplatte aus einer vorhandenen Sicherung wiederherstellen.  
  
 Nach einer Systemwiederherstellung müssen Sie verwenden das Wiederherstellen von Dateien und Ordner-Assistent zum Wiederherstellen von Dateien und Ordnern, die während der Wiederherstellung nicht beibehalten wurden. Beispielsweise können nicht, wenn Sie den Systemdatenträger ersetzt, oder die Partitionsinformationen auf dem Systemdatenträger nicht lesbar ist, Sie Daten von anderen Volumen auf dem Systemdatenträger wiederherstellen.  
  
> [!NOTE]
>  Wiederherstellen von Dateien und Ordner-Assistenten können Sie das komplette Systemlaufwerk wiederherzustellen. Informationen dazu, wie Sie das komplette System wiederherstellen können, finden Sie unter [wiederherstellen oder Reparieren des Servers mithilfe eines Installationsmediums](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore_1) oder [wiederherstellen oder Zurücksetzen des Servers von einem Clientcomputer mit dem Wiederherstellungs-DVD](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore_2).  
  
##### <a name="to-restore-files-and-folders-from-a-server-backup"></a>Wiederherstellen von Dateien und Ordnern aus einer Sicherung  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard, und klicken Sie dann auf die **Geräte** Registerkarte.  
  
2.  Klicken Sie auf den Namen des Servers, und klicken Sie dann auf **Wiederherstellen von Dateien oder Ordner für den Server** in der **Aufgaben** Bereich.  
  
     Das Wiederherstellen von Dateien und Ordner-Assistent wird geöffnet.  
  
3.  Führen Sie die Anweisungen im Assistenten, um die Dateien oder Ordner wiederherzustellen.  
  
> [!WARNING]
>  Weitere Informationen zum Sichern und Wiederherstellen von Dateien und Ordnern finden Sie unter [Manage Backup and Restore](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md).  
  
###  <a name="BKMK_ConfigreSharedFolders"></a>Freigegebene Ordner auf dem Server wiederherstellen  
 Nachdem Sie das Systemlaufwerk des Servers, wiederherstellen, wenn freigegebene Ordner weiterhin auf der Datenpartition sind oder in der Datenpartition wiederhergestellt wurden, müssen Sie dem Server die Ordner erkennen kann die freigegebenen Ordner erneut konfigurieren. Das folgende Verfahren beschreibt, wie freigegebene Ordner hinzuzufügen, die vor dem freigegeben wurden.  
  
##### <a name="to-add-an-existing-folder-to-the-server-shared-folders"></a>Einen vorhandenen Ordner auf dem Server Hinzufügen freigegebener Ordner  
  
1.  Suchen Sie im Datei-Explorer den freigegebenen Ordner auf der Festplatte.  
  
2.  Mit der rechten Maustaste in des freigegebenen Ordners, klicken Sie auf **Eigenschaften**, klicken Sie auf die **Freigabe** Registerkarte, und notieren Sie die Ordnerberechtigungen.  
  
3.  Melden Sie sich bei Windows Server Essentials-Dashboards, klicken Sie auf die **Speicher** Registerkarte, und klicken Sie dann auf **Hinzufügen eines Ordners** in der **Tasks für Serverordner** Bereich.  
  
     Hinzufügen, wird ein Ordner-Assistent geöffnet.  
  
4.  Geben Sie einen Namen für die Freigabe in der **Namen** Feld.  
  
5.  Klicken Sie auf **Durchsuchen**, navigieren Sie zu *< Laufwerk\ > \\ < ServerName\ >*\ServerFolders (z.B. *d:\Contoso\ServerFolders*), wählen Sie den Ordner, die Sie freigeben möchten, und klicken Sie dann auf **OK**.  
  
6.  Klicken Sie auf **Weiter**.  
  
7.  Geben Sie die Berechtigungen, die Sie in Schritt2 notiert, und klicken Sie dann auf **Ordner hinzufügen**.  
  
    > [!IMPORTANT]
    >  Diese Berechtigungen ersetzen alle vorhandenen Berechtigungen, die nicht in den Ordner mithilfe der Windows Server Essentials-Dashboard hinzugefügt wurden.  
  
> [!IMPORTANT]
>  Nachdem Sie das Hinzufügen von Ordnern zur Liste der freigegebenen Ordner abgeschlossen haben, stellen Sie sicher, dass die Ordner in der Server-Sicherung enthalten sind. Informationen zum Hinzufügen von Ordnern zur serversicherung finden Sie unter [festlegen einrichten oder Anpassen der serversicherung](Set-up-or-customize-server-backup.md).  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten der Sicherung und Wiederherstellung](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)  
  
-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)
