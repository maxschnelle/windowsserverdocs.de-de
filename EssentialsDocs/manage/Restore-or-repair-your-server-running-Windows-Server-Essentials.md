---
title: Wiederherstellen oder Reparieren des Servers mit Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 27bf6f24-30c4-4935-9b24-069eb43e22f4
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 00c57fab4ee9689ba8bd760e5c99d87e3e18d130
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89622953"
---
# <a name="restore-or-repair-your-server-running-windows-server-essentials"></a>Wiederherstellen oder Reparieren des Servers mit Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

 Dieses Thema enthält eine Übersicht und unterstützende Verfahren zum Wiederherstellen oder Reparieren eines Servers, auf dem Windows Server Essentials ausgeführt wird, sowie die folgenden Abschnitte:

-   [Übersicht über die Wiederherstellung des Serversystems](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Overview)

-   [Wiederherstellen oder Reparieren des Systemlaufwerks](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore)

-   [Wiederherstellen von Dateien und Ordnern auf dem Server](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFilesAndFolders)

##  <a name="overview-of-server-system-restores"></a><a name="BKMK_Overview"></a> Übersicht über Server System Wiederherstellungen
 Beim Ausführen einer Wiederherstellung wirkt sich der Status des Servers auf die verfügbare Wiederherstellungsmethode aus und darauf, wie umfassend Sie eine Wiederherstellung durchführen können.

 Die häufigsten Gründe für die Wiederherstellung eines Servers sind im Folgenden aufgeführt:

- Ein Virus auf dem Server kann nicht bekämpft oder gelöscht werden.

- Die Konfigurationseinstellungen des Servers sind unzureichend, und der Server kann nicht gestartet werden.

- Sie haben das Systemlaufwerk ausgetauscht.

- Sie nehmen den Server außer Betrieb. Sie möchten eine Wiederherstellung auf einem neuen Server durchführen.

  Sie können den Server entweder mithilfe von Sicherheitskopien oder über die werkseitigen Standardeinstellungen wiederherstellen.

- [Wiederherstellen des Servers über eine Sicherung](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFromBackup)

- [Zurücksetzen des Servers auf die werkseitigen Standardeinstellungen](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_FactoryReset)

###  <a name="restoring-the-server-from-a-backup"></a><a name="BKMK_RestoreFromBackup"></a> Wiederherstellen des Servers aus einer Sicherung
 Dieser Abschnitt enthält Anleitungen in Bezug auf die Auswahl der Sicherungsart.

 Wenn eine Sicherung verfügbar ist, besteht die beste Wahl für die Wiederherstellung des Servers darin, die Installationsmedien des Herstellers für die Wiederherstellung aus einer externen Sicherung zu verwenden. Durch die Wiederherstellung werden die von Ihnen ausgewählten Servereinstellungen und -ordner aus den Sicherheitskopien erneut abgerufen und angewendet. Sie müssen lediglich die entsprechenden Einstellungen konfigurieren und die nach der Sicherung erstellten Daten wiederherstellen.

 Wenn Sie den Server über eine frühere Sicherung wiederherstellen möchten, wählen Sie die konkrete Sicherheitskopie, die für die Wiederherstellung angewendet werden soll. Sie benötigen dafür eine gültige Sicherungsdatei auf einem externen Festplattenlaufwerk, das direkt mit dem Server verbunden ist:

- **Wenn Sie erst vor Kurzem eine Sicherung des Servers erfolgreich durchgeführt haben** und Sie wissen, dass in der Sicherung sämtliche Ihrer kritischen Daten enthalten sind, verläuft Ihre Auswahl recht unkompliziert. Sie müssen nur jene Daten neu erstellen, die nach der letzten erfolgreichen Sicherung erstellt wurden. Außerdem müssen Sie die nach der Sicherung vorgenommenen Einstellungsänderungen neu konfigurieren.

- **Wenn Sie die Wiederherstellung des Servers aufgrund eines Virus durchführen**, wählen Sie Sicherheitskopien, bei denen Sie sicher sind, dass sie vor dem Auftreten des Virus erstellt wurden. Sie müssen möglicherweise mehrere Tage zurückdatieren, um eine Sicherung auszuwählen, die einwandfrei ist.

- **Wenn Sie den Server wegen fehlerhafter Konfigurationseinstellungen wiederherstellen**, wählen Sie eine Sicherung, von der Sie wissen, dass sie vor der Konfigurationseinstellungsänderung vorgenommen wurde, welche das Problem auf dem Server verursacht hat.

  Wenn Sie eine Wiederherstellung über eine Sicherung vornehmen, hängen das genaue Vorgehen und die erforderlichen Folgemaßnahmen von der Anzahl der Festplatten auf dem Server sowie davon ab, ob das Systemlaufwerk ersetzt wird:

- **Wenn der Server über eine einzelne Festplatte verfügt und das Laufwerk nicht ersetzt wird**, bleiben die Informationen zur Laufwerkspartition beim Wiederherstellen des Servers unberührt. Das Systemvolumen wird wiederhergestellt, und die Daten auf dem verbleibenden Datenträger werden beibehalten.

- **Wenn der Server über eine einzelne Festplatte verfügt und das Laufwerk ersetzt wird**, so wird das Systemvolumen wiederhergestellt. Sie müssen dann die Ordner für die Datenträger manuell wiederherstellen. Alle nicht standardmäßig freigegebenen Ordner müssen erstellt werden, da diese nicht erstellt werden, wenn der Serverspeicher neu erstellt wird.

- **Wenn der Server über mehrere Festplatten verfügt und Laufwerk 0 (enthält das Systemvolumen) nicht ersetzt wird**, bleiben die Informationen zur Laufwerkspartition beim Wiederherstellen des Servers unberührt. Das Systemvolumen wird wiederhergestellt, und die Daten auf allen verbleibenden Datenträgern werden beibehalten.

- **Wenn der Server über mehrere Festplatten verfügt und Laufwerk 0 (enthält das Systemvolumen) ersetzt wird**, so wird das Systemvolumen wiederhergestellt. Sie müssen dann alle freigegebenen Ordner, die zuvor auf Laufwerk 0 gespeichert waren, manuell wiederherstellen.

###  <a name="resetting-the-server-to-factory-default-settings"></a><a name="BKMK_FactoryReset"></a> Zurücksetzen des Servers auf die Werkseinstellungen
 Wenn Sie über keine Sicherheitskopien verfügen, über die Sie eine Wiederherstellung vornehmen können, oder wenn Sie aus einem anderen Grund eine vollständige Systemwiederherstellung durchführen möchten oder müssen, ohne die vorherige Serverkonfiguration wiederherzustellen, können Sie eine Wiederherstellung durchführen, die den Server auf die werkseitigen Standardeinstellungen zurückgesetzt, indem Sie die Installations- oder Wiederherstellungsmedien vom Hardware-Hersteller verwenden.

 Wenn Sie den Server wiederherstellen, indem Sie ihn auf die werkseitigen Standardeinstellungen zurücksetzen, werden sämtliche vorhandenen Einstellungen und installierten Anwendungen auf dem Server gelöscht. Sie müssen den Server dann erneut konfigurieren. Nach dem Zurücksetzen auf die Werkseinstellungen muss der Server neu starten.

 Beim Zurücksetzen auf die Werkseinstellungen können Sie wählen, ob Sie Ihre Daten beibehalten oder löschen möchten. Dabei müssen Sie die folgenden Auswirkungen beachten:

-   Wenn Sie sämtliche Ihrer Daten beibehalten möchten, werden alle Daten im Systemvolumen gelöscht. Die Daten auf anderen Volumen werden jedoch beibehalten.

    > [!CAUTION]
    >  Wenn die Datenträgereinstellungen nicht den Standardeinstellungen entsprechen, werden alle Daten auf einem betreffenden Datenträger gelöscht. Wenn Sie den System Datenträger ersetzt haben, muss der neue Datenträger größer als das System Volume des ursprünglichen Datenträgers sein.
    >
    >  Falls die Partitionsinformationen für ein Systemlaufwerk nicht gelesen werden können, oder falls Sie das Systemlaufwerk ersetzen, werden alle Daten auf dem Systemlaufwerk entfernt, auch wenn Sie alle Ihre Daten beibehalten möchten.

-   Wenn Sie den Server außer Betrieb nehmen oder für einen anderen Zweck verwenden möchten, wählen Sie die Löschung all Ihrer Daten. Neben der Serverkonfiguration, weiteren Einstellungen und den Daten im Systemvolumen werden alle anderen Daten gelöscht und alle Festplatten auf dem Server neu formatiert.

> [!NOTE]
>  Wenn Speicherplätze auf dem Server konfiguriert werden, bevor Sie ein Zurücksetzen auf die Werkseinstellungen vornehmen, sollten Sie den Abschnitt **Erweitert** der Konsole **Verwalten von Speicherplätzen** anwenden, um alle Speicherplätze manuell zu entfernen.

 Nach dem Zurücksetzen auf die Werkseinstellungen müssen Sie die folgenden Aufgaben ausführen:

-   **Konfigurieren Sie den Server neu.** Verwenden Sie auf dem Server den Assistenten zum Konfigurieren von Servern, um die Konfigurationseinstellungen erneut einzugeben. Wenn Sie einen Remote verwalteten Windows Server Essentials-Server von einem Client Computer aus konfigurieren möchten, öffnen Sie einen Webbrowser, und geben Sie dann **http://** _<yourservername \> _ in der Adressleiste ein.

-   **Verbinden Sie Clientcomputer erneut mit dem Server** Wenn ein Computer zuvor mit dem Server verbunden war, müssen Sie die Windows Server Essentials-Connector-Software vom Computer deinstallieren, bevor Sie den Computer erneut mit dem Server verbinden. Weitere Informationen finden Sie unter [Deinstallieren der Connector-Software](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_13) und [Verbinden von Computern mit dem Server](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9).

##  <a name="restore-or-repair-the-system-drive"></a><a name="BKMK_Restore"></a> Wiederherstellen oder Reparieren des System Laufwerks
 Der erste Schritt bei der Serverwiederherstellung besteht darin, das Server-Systemlaufwerk wiederherzustellen oder zu reparieren. Nachdem Sie das Systemlaufwerk wiederhergestellt haben, führen Sie alle zum Wiederherstellen der Datenlaufwerke erforderlichen Maßnahmen durch. Stellen Sie außerdem sämtliche Freigabedaten wieder her, die bei der Wiederherstellung verloren gegangen sind.

 Für die Wiederherstellung stehen drei Methoden zur Verfügung:

-   [Wiederherstellen oder Reparieren des Servers mithilfe des Installationsmediums](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore_1). Verwenden Sie die Installationsmedien des Serverherstellers, um die Wiederherstellung über Sicherheitskopien durchzuführen.

-   **Verwenden Sie die Installationsmedien, um den Server auf die Werkseinstellungen zurückzusetzen**. Informationen darüber, welche Schritte Sie dafür am Server vornehmen müssen, finden Sie in der Dokumentation des Serverherstellers.

-   [Wiederherstellen oder Zurücksetzen des Servers von einem Client-Computer mit der Wiederherstellungs-DVD](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore_2). Wenn Sie einen Remote verwalteten Server wiederherstellen müssen, auf dem Windows Server Essentials ausgeführt wird, müssen Sie die Wiederherstellung von einem Client Computer durchführen, indem Sie die Wiederherstellungs-DVD des Server Herstellers verwenden.

###  <a name="restore-or-repair-your-server-using-installation-media"></a><a name="BKMK_Restore_1"></a> Wiederherstellen oder Reparieren des Servers mithilfe der Installationsmedien
 Im folgenden Verfahren wird beschrieben, wie Sie das Server-Systemlaufwerk mithilfe der Windows Server Essentials-Installationsmedien von einer Sicherung wiederherstellen. (Um herauszufinden, wie die Installationsmedien eingesetzt werden, um die werkseitigen Standardeinstellungen wiederherzustellen, lesen Sie die Dokumentation des Serverherstellers).

> [!NOTE]
>  Wenn der Server Speicherplätze verwendet und Sie die Daten auf einem neuen Server wiederherstellen, sollten Sie zunächst das Systemlaufwerk wiederherstellen und sich dann beim Windows Server Essentials-Dashboard anmelden, die Speicherplätze auf ähnliche Weise wie auf dem alten Server konfigurieren und dann die Datenvolumes wiederherstellen.

##### <a name="to-restore-the-server-system-drive-from-a-backup-using-installation-media"></a>So stellen Sie das Server-Systemlaufwerk über eine Sicherung mithilfe der Installationsmedien wieder her

1.  Legen Sie die Windows Server Essentials-Installations-DVD in das DVD-Laufwerk des Servers ein, starten Sie den Server neu, und drücken Sie dann eine beliebige Taste, um die DVD zu starten

    > [!NOTE]
    >  Wenn der Wiederherstellungsvorgang nicht automatisch gestartet wird, überprüfen Sie die BIOS-Einstellungen für den Server, um sicherzustellen, dass das DVD-Laufwerk an erster Stelle im Boot-Menü steht.

     -Oder-

     Wenn der Hersteller die Installationsmedien vorab auf den Server geladen hat, drücken Sie beim Start die Taste F8, um die Installationsmedien aufzurufen und zu starten.

2.  Nachdem die Windows Server-Dateien geladen werden, wählen Sie Ihre Sprache und die weiteren Präferenzen. Klicken Sie anschließend auf **Weiter**.

3.  Klicken Sie auf der nächsten Seite des Assistenten auf **Computer reparieren**.

    > [!CAUTION]
    >  Wählen Sie nicht die Option **Jetzt installieren**. Diese Option führt Sie durch eine vollständige Systeminstallation, bei der alle Konfigurationseinstellungen und alle Daten auf dem Systemlaufwerk gelöscht werden.

4.  Klicken Sie auf der Seite **Wählen Sie eine Option** auf **Problembehandlung**.

5.  Wählen Sie auf der Seite **System Abbild-Wiederherstellung** das aktuelle System aus? entweder **Windows Server Essentials** oder **Windows Server Essentials**.

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
>  Zum Wiederherstellen und Freigeben von Ordnern auf dem Server müssen Sie eventuell zusätzliche Schritte durchführen. Weitere Informationen finden Sie unter [Wiederherstellen von Dateien und Ordnern auf dem Server](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFilesAndFolders).

###  <a name="restore-or-reset-your-server-from-a-client-computer-using-the-recovery-dvd"></a><a name="BKMK_Restore_2"></a> Wiederherstellen oder Zurücksetzen des Servers von einem Client Computer mithilfe der Wiederherstellungs-DVD
 In Windows Server Essentials können Sie den Server von einem startbaren USB-Speicherstick starten, den Sie erstellen, und dann den Server von einem Client Computer aus wiederherstellen, indem Sie die Wiederherstellungs-DVD verwenden, die Sie vom Server Hersteller erhalten haben. Der Clientcomputer muss sich im selben Netzwerk wie der Server befinden. Diese Methode ist in Windows Server Essentials nicht verfügbar.

 Das folgende Verfahren umfasst allgemeine Schritte zum Ausführen einer Server-Wiederherstellung. Die Schritte gelten gleichermaßen für das Wiederherstellen über Sicherheitskopien wie auch für das Zurücksetzen auf die werkseitigen Standardeinstellungen. Weitere ausführliche Anweisungen finden Sie in der Dokumentation des Serverherstellers.

##### <a name="to-restore-or-reset-the-server-from-a-client-computer-using-the-recovery-dvd"></a>So stellen Sie den Server von einem Clientcomputer aus mit der Wiederherstellungs-DVD wieder her oder setzen diesen zurück

1.  Legen Sie das Windows Server Essentials-Server Wiederherstellungs Medium, das Sie vom Server Hersteller erhalten haben, auf einem Client Computer ein.

     Der Assistent zum Wiederherstellen des Servers wird geöffnet.

2.  Befolgen Sie die Anweisungen im Assistenten, um einen bootfähigen USB-Speicherstick einzurichten, mit dem Sie den Server im Wiederherstellungsmodus starten können.

3.  Nachdem der Assistent zum Wiederherstellen des Servers den bootfähigen USB-Speicherstick vorbereitet hat, stecken Sie den Speicherstick am Server ein. Starten Sie dann den Server im Wiederherstellungsmodus. Lesen Sie die Dokumentation des Herstellers der Server-Hardware, um zu erfahren, wie Sie den Server im Wiederherstellungsmodus starten.

     Nachdem Sie den Server im Wiederherstellungsmodus gestartet haben, ermittelt der Assistent zur Server-Wiederherstellung den Server und stellt dann eine Verbindung her.

4.  Befolgen Sie die Anweisungen im Assistenten, um das Wiederherstellen des Servers abzuschließen.

> [!NOTE]
>  Bei dieser Methode der Server-Wiederherstellung werden externe Speichergeräte, die während der Wiederherstellung mit dem Server verbunden sind, nicht beachtet. Wenn Sie die Daten auf einem externen Speichergerät löschen möchten, müssen Sie dies manuell tun.

> [!NOTE]
>  Wenn Sie nach dem Wiederherstellen der Daten über eine Sicherung zusätzliche freigegebene Ordner auf dem Server erstellt haben, werden diese zusätzlichen freigegebenen Ordner unter Umständen nicht vom Server erkannt. Sie müssen diese Ordner erneut freigeben. Weitere Informationen finden Sie unter [Wiederherstellen von Dateien und Ordnern auf dem Server](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFilesAndFolders).

##  <a name="restore-files-and-folders-on-the-server"></a><a name="BKMK_RestoreFilesAndFolders"></a> Wiederherstellen von Dateien und Ordnern auf dem Server
 Je nach der Methode, die Sie zur Wiederherstellung oder Reparatur des Servers verwenden, und je nach dem vom Server verwendeten Speichertyp müssen Sie die Datenvolumen eventuell wiederherstellen, nachdem Sie das Systemlaufwerk wiederhergestellt haben. In einigen Fällen müssen Sie vorhandene Ordner eventuell erneut freigeben, damit der Server sie erkennt.

 Im Folgenden sind einige Beispiele von Fällen aufgeführt, in denen Sie Dateien und Ordner unter Umständen wiederherstellen müssen:

-   [Wiederherstellen von Dateien und Ordnern über eine Server-Sicherung](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFilesFromBackup). Wenn Sie den Systemdatenträger ersetzt haben oder die Partitionsinformationen auf dem Systemdatenträger nicht lesbar sind, können Sie das System wiederherstellen. Sie können allerdings keine Daten von anderen Volumen auf diesem Datenträger wiederherstellen. Zum Wiederherstellen von Dateien und Ordnern aus anderen Datenvolumen müssen Sie den Assistenten zum Wiederherstellen von Dateien und Ordnern verwenden.

-   [Wiederherstellen von freigegebenen Ordnern auf dem Server](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_ConfigreSharedFolders). Wenn Sie nach dem Wiederherstellen des Systemlaufwerks über die Sicherung weitere freigegebene Ordner auf dem Server erstellen, befinden sich die freigegebenen Ordner weiterhin auf der Datenpartition oder werden in der Datenpartition wiederhergestellt. Sie werden aber möglicherweise vom Server nicht erkannt. Sie müssen diese Ordner erneut freigeben.

###  <a name="restore-files-and-folders-from-a-server-backup"></a><a name="BKMK_RestoreFilesFromBackup"></a> Wiederherstellen von Dateien und Ordnern aus einer Server Sicherung
 Der Assistent zum Wiederherstellen von Dateien und Ordnern unterstützt Sie beim Schützen Ihrer Daten, wenn die Festplatte nicht mehr funktioniert oder Dateien versehentlich gelöscht werden. Mit der Windows Server Essentials-Sicherung können Sie eine Kopie aller Daten auf der Festplatte erstellen und die Daten auf einem externen Speichergerät speichern. Wenn die ursprünglichen Daten auf der Festplatte versehentlich gelöscht, überschrieben oder aufgrund einer Fehlfunktion unbrauchbar werden, können Sie die Daten über die Sicherung wiederherstellen. Der Assistent zum Wiederherstellen von Dateien oder Ordnern unterstützt Sie über vorhandene Sicherheitskopien bei der Wiederherstellung einer einzelnen Datei oder eines einzelnen Ordners, mehrerer Dateien oder Ordner oder einer kompletten Festplatte.

 Nach einer Systemwiederherstellung müssen Sie möglicherweise den Assistenten zum Wiederherstellen von Dateien und Ordnern verwenden, um Dateien und Ordner wiederherzustellen, die während der Wiederherstellung nicht erfasst wurden. Wenn Sie beispielsweise den Systemdatenträger ersetzt haben oder die Partitionsinformationen auf dem Systemdatenträger unlesbar sind, können Sie Daten von anderen Volumen auf dem Systemdatenträger nicht wiederherstellen.

> [!NOTE]
>  Sie können den Assistenten zum Wiederherstellen von Dateien und Ordnern nicht verwenden, um das komplette Systemlaufwerk wiederherzustellen. Informationen darüber, wie Sie das komplette System wiederherstellen können, finden Sie unter [Wiederherstellen oder Reparieren des Servers mithilfe der Installationsmedien](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore_1) oder [Wiederherstellen oder Zurücksetzen des Servers von einem Client-Computer mit der Wiederherstellungs-DVD](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore_2).

##### <a name="to-restore-files-and-folders-from-a-server-backup"></a>So stellen Sie Dateien und Ordner über eine Server-Sicherung wieder her

1.  Öffnen Sie das Windows Server Essentials-Dashboard, und klicken Sie dann auf die Registerkarte **Geräte** .

2.  Klicken Sie auf den Namen des Servers und anschließend auf **Wiederherstellen von Dateien oder Ordnern für den Server** im Bereich **Aufgaben**.

     Der Assistent zum Wiederherstellen von Dateien und Ordnern wird geöffnet.

3.  Befolgen Sie die Anweisungen im Assistenten, um die Dateien oder Ordner wiederherzustellen.

> [!WARNING]
>  Weitere Informationen zum Sichern und Wiederherstellen von Dateien und Ordnern finden Sie unter [Verwalten von Sicherungen und Wiederherstellungen](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md).

###  <a name="restore-shared-folders-on-the-server"></a><a name="BKMK_ConfigreSharedFolders"></a> Wiederherstellen von freigegebenen Ordnern auf dem Server
 Wenn sich nach dem Wiederherstellen des System Laufwerks des Servers die freigegebenen Ordner weiterhin in der Daten Partition befinden oder in der Daten Partition wieder hergestellt wurden, müssen Sie die freigegebenen Ordner möglicherweise erneut konfigurieren, damit der Server die Ordner erkennen kann. Im folgenden Verfahren wird beschrieben, wie freigegebene Ordner hinzuzufügen sind, die bereits zuvor einmal freigegeben waren.

##### <a name="to-add-an-existing-folder-to-the-server-shared-folders"></a>So fügen Sie einen vorhandenen Ordner zu den freigegebenen Ordnern des Servers hinzu

1.  Suchen Sie im Datei-Explorer den freigegebenen Ordner auf dem Festplattenlaufwerk.

2.  Klicken Sie mit der rechten Maustaste auf den freigegebenen Ordner. Klicken Sie dann auf **Eigenschaften** und auf die Registerkarte **Freigabe**. Notieren Sie sich anschließend die Ordnerberechtigungen.

3.  Melden Sie sich beim Windows Server Essentials-Dashboard an, klicken Sie auf die Registerkarte **Speicher** , und klicken Sie dann im Bereich **Tasks für Server Ordner** auf **Ordner hinzufügen** .

     Der Assistent zum Hinzufügen eines Ordners wird geöffnet.

4.  Geben Sie einen Namen für die Freigabe im Feld **Name** ein.

5.  Klicken Sie auf **Durchsuchen**, navigieren Sie zu *<Laufwerk \> \\<\> Servername*\serverfolders (z. b. *d:\conteso\serverfolders*), wählen Sie den Ordner aus, den Sie freigeben möchten, und klicken Sie dann auf **OK**.

6.  Klicken Sie auf **Weiter**.

7.  Geben Sie die Berechtigungen an, die Sie in Schritt 2 notiert haben. Klicken Sie dann auf **Ordner hinzufügen**.

    > [!IMPORTANT]
    >  Diese Berechtigungen ersetzen alle vorhandenen Berechtigungen, die dem Ordner nicht mithilfe des Windows Server Essentials-Dashboards hinzugefügt wurden.

> [!IMPORTANT]
>  Nachdem Sie das Hinzufügen von Ordnern zur Liste der freigegebenen Ordner abgeschlossen haben, müssen Sie sicherstellen, dass die Ordner in der Server-Sicherung enthalten sind. Informationen zum Hinzufügen von Ordnern in die Server-Sicherung finden Sie unter [Einrichten oder Anpassen der Server-Sicherung](Set-up-or-customize-server-backup.md).

## <a name="additional-references"></a>Weitere Verweise

-   [Verwalten der Sicherung und Wiederherstellung](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)

-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)

-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)
