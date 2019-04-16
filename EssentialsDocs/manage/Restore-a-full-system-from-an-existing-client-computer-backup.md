---
title: "Wiederherstellen eines vollständigen Systems aus einer vorhandenen clientcomputersicherung"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47e498a6-1b71-47de-88f6-8c13c221d108
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: cfc4d1ce461e1e1cbb9b99970355c4dc7241911b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="restore-a-full-system-from-an-existing-client-computer-backup"></a>Wiederherstellen eines vollständigen Systems aus einer vorhandenen clientcomputersicherung

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials 
  
 Hardware und Betriebssysteme sind zwar selten können, aber durchaus auftreten. Ein fehlerhafter Lüfter könnte Überhitzung der Hauptplatine und nutzlos zu rendern. Das Betriebssystem könnte beschädigt werden und nicht starten. Feuer und Wasser ergeben sich Hardware dauerhaft beschädigt werden. Ein Festplattenlaufwerk kann ein Fehler auftreten oder Sie es mit einer größeren Festplatte ersetzen möchten.  
  
 Dieses Dokument enthält Informationen zu den folgenden Themen:  
  
-   [Was ist die vollständige Systemwiederherstellung?](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_WhatIs)  
  
-   [Wie funktioniert die Umgebung für die Systemwiederherstellung?](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_HowDoes)  
  
-   [Erstellen Sie einen startbaren USB-Speichersticks zur Wiederherstellung eines Clientcomputers](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_CreateBootable)  
  
-   [Mithilfe des Assistenten für vollständige Wiederherstellung](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_Using)  
  
-   [Wo finde ich die Treiber für die Hardware?](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_FindDrivers)  
  
##  <a name="BKMK_WhatIs"></a>Was ist die vollständige Systemwiederherstellung?  
 Die Sie Ersetzen der Festplatte oder der Computer ein Fehler auftritt, zu dem Punkt, in denen es nicht mehr verwendet oder gestartet werden, können Sie das System aus einer früheren Sicherung des Computers wiederherstellen. Eine vollständige Systemwiederherstellung versetzt das System in den Zustand, in dem zum Zeitpunkt der Sicherung.  
  
> [!IMPORTANT]
>  Eine vollständige Systemwiederherstellung auf Computerhardware, z.B. einer Systemplatine, nicht möglich, die nicht an die Computerhardware ähnelt, die ersetzt wird. Ein Betriebssystem installiert ist, hängt stark von der zugrunde liegenden Hardware des Computers. Allerdings können Sie eine vollständige Systemwiederherstellung auf einer Festplatte ausführen, die gleich groß oder größer als die, die ersetzt wird.  
  
 Wenn Sie eine vollständige Systemwiederherstellung durchführen möchten, können Sie eine bestimmten Computer-Sicherung zum Wiederherstellen des Systems, mit allen Anwendungen, Konfigurationen und Einstellungen, die dem Benutzer vor dem Fehler, einer Katastrophe oder Diebstahl vertrauten auswählen. Sie können auch die Volumes auswählen, die Sie wiederherstellen möchten.  
  
 Bei der Planung oder Vorbereiten der Migration auf einem Computer im Netzwerk, das komplette System wiederherstellen Folgendes berücksichtigen:  
  
### <a name="windows-preinstallation-environment"></a>Windows Preinstallation Environment  
 Windows Preinstallation Environment (Windows PE) ist ein minimales Betriebssystem zur Vorbereitung eines Computers für Windows-Installation. Für Server mit Windows Server Essentials wird Windows PE automatisch installiert, wenn Sie das Wiederherstellungsmedium auf einem Computer wiederhergestellt werden einfügen. Für Server mit Windows Server Essentials wird Windows PE automatisch installiert, wenn Sie den Computer mit dem clientwiederherstellungsdienst oder das USB-Flashlaufwerk starten.  
  
 Windows PE unterstützt keine Funkverbindungen. Aus diesem Grund muss der wiederherzustellende Computer physisch mit dem kleinen Firmennetzwerk verbunden werden.  
  
### <a name="bitlocker"></a>BitLocker  
 BitLocker-Laufwerkverschlüsselung (BitLocker) ist eine Funktion zum Schutz von Daten, die in einigen Versionen von Windows Vista, Windows7 und Windows8 verfügbar ist. BitLocker schützt vor Datendiebstahl oder auf Computern, die verloren geht oder gestohlen werden, und bietet sichere Löschung von Daten, wenn Computer außer Betrieb gesetzt werden.  
  
 **Für Windows Server Essentials:** Wenn der Computer, den Sie wiederherstellen müssen verschlüsselt war die Verwendung von BitLocker (gibt an, ob sie nur das Betriebssystemlaufwerk oder das Betriebssystemlaufwerk und einzelne oder mehrere weitere Festplattenlaufwerke war), können Sie weiterhin die vollständige Medium für die Systemwiederherstellung auf der CD mit dem Server und den Assistenten für vollständige Systemwiederherstellung enthaltenen verwenden, das Festplattenabbild neu installieren, einschließlich des Betriebssystems, aus einer Sicherung und die Daten auf dem neuen oder reparierten Computer wiederherzustellen.  
  
 **Für Windows Server Essentials:** Wenn der Computer, die Sie wiederherstellen müssen verschlüsselt war die Verwendung von BitLocker (gibt an, ob sie nur das Betriebssystemlaufwerk oder das Betriebssystemlaufwerk und einzelne oder mehrere weitere Festplattenlaufwerke war), Sie können weiterhin den Assistenten für vollständige Systemwiederherstellung verwenden, um das Festplattenabbild einschließlich des Betriebssystems, aus einer Sicherung neu zu installieren und die Daten auf dem neuen oder reparierten Computer wiederherzustellen.  
  
 Wenn der Server Laufwerke, Ordner und Dateien gesichert werden, ist eine unverschlüsselte Version auf dem Server gespeichert. Diese unverschlüsselte Version wird während der vollständigen Systemwiederherstellung auf den Computer kopiert.  
  
> [!NOTE]
>  Nach einer erfolgreichen vollständigen Systemwiederherstellung müssen Sie BitLocker auf dem Computer erneut aktivieren.  
>   
>  Anweisungen zum Aktivieren von BitLocker auf Computern, auf denen Windows8 ausgeführt werden, finden Sie unter [BitLocker: Aktivieren von BitLocker](https://go.microsoft.com/fwlink/p/?LinkID=254918).  
>   
>  Anweisungen zum Aktivieren von BitLocker auf Computern, auf denen Windows7 ausgeführt werden, finden Sie unter [BitLocker Drive Encryption Step-by-Step für Windows7](https://go.microsoft.com/fwlink/p/?LinkId=140225).  
  
 Weitere Informationen zu BitLocker-laufwerkverschlüsselung, finden Sie unter [BitLocker: häufig gestellte Fragen (FAQ)](https://go.microsoft.com/fwlink/p/?LinkID=254917).  
  
### <a name="encrypting-file-system-encrypted-files"></a>Verschlüsselndes Dateisystem-verschlüsselte Dateien  
 Das verschlüsselnde Dateisystem (Encrypting File System, EFS)-Feature in Windows kann zusätzliche benutzerbasierte Verschlüsselung auf Dateiebene für verschiedene Sicherheitsstufen durch mehrere Benutzer desselben Computers bereitzustellen. Es ist wichtig zu beachten, dass im Gegensatz zu BitLocker-verschlüsselten Laufwerken EFS-verschlüsselte Ordner und Dateien weiterhin in einer computersicherung verschlüsselt werden. EFS ist nicht in Windows XP Home Edition, Windows Vista Starter, Windows Vista Home Basic, Windows Vista Home Premium, Windows7 Starter, Windows7 Home Basic, Windows7 Home Premium oder Windows8 verfügbar. Es ist nur in Windows8 Pro verfügbar.  
  
> [!WARNING]
>  Anders als bei BitLocker können Sie nur EFS-geschützte Dateien aus dem Betriebssystem zugreifen, die sie verschlüsselt.  
  
### <a name="disk-partitions"></a>Festplattenpartitionen  
 Wenn die Festplatte auf dem neuen Computer die gleichen oder größer als die ursprüngliche, die Festplatte ist Laufwerk automatisch neu formatiert und partitioniert. Weitere Informationen finden Sie in der nachfolgenden Diagramm entnehmen:  
  
|Quellcomputer|Wiederhergestellter oder neuer Computer|  
|-----------------------|------------------------------|  
|Einzelner Datenträger mit mehreren Partitionen|Einzelner Datenträger mit mehreren Partitionen; zusätzlicher Speicherplatz wird mit dem letzten Partition zugeordnet.|  
|Einzelner Datenträger mit einer Partition|Einzelner Datenträger mit einer Partition und alle verfügbaren Speicherplatz wird für die einzelnen Partition verwendet.|  
  
> [!NOTE]
>  Wenn Datenträger Datenträgergröße und Partitionslayout Layout-Unterschiede zwischen der ursprünglichen und dem wiederhergestellten oder neuen Computer vorhanden sind, müssen Sie Datenträgerverwaltung verwenden, um die entsprechenden Partitionen auf dem wiederhergestellten oder neuen Computer zu erstellen. Dies ist in den Assistenten für vollständige Systemwiederherstellung möglich.  
  
### <a name="raid-and-dynamic-disks"></a>RAID- und dynamische Datenträger  
 Sichern von redundant Array of independent Datenträger (RAID) und dynamischen Datenträgern wird nicht unterstützt.  
  
##  <a name="BKMK_HowDoes"></a>Wie funktioniert die Umgebung für die Systemwiederherstellung?  
 Mit Windows ServerÂ® 2012 Essentials bereitgestellten Medium für die Systemwiederherstellung wird Windows Preinstallation Environment (Windows PE) auf dem Computer installiert. Windows PE ersetzt die MS-DOS-Umgebung und die wichtigen Programmdateien für Windows enthält. In Windows Server Essentials, es gibt zwei unterstützte Methoden zum Wiederherstellen eines Systems: mit dem clientwiederherstellungsdienst, der ein Netzwerk verwendet und keine ausschließlich auf Medien oder über einen USB-Speicherstick.  
  
> [!NOTE]
>  Windows PE unterstützt keine Funkverbindungen. Aus diesem Grund muss der wiederherzustellende Computer physisch mit dem kleinen Firmennetzwerk verbunden werden.  
  
 Die Umgebung für die Systemwiederherstellung enthält die Programmdateien mit (x86) 32-Bit- und 64-Bit-(x64). Nach dem Einfügen des Systems wiederherstellen Sie Medien, wählen Sie die entsprechende Version der Dateien. 32-Bit-(x86) ist die Standardeinstellung und wird automatisch ausgewählt, wenn Sie nicht innerhalb von 30Sekunden. Sind Updates für die vollständige Programmdateien auf dem Server wiederherstellen, werden die aktualisierten Dateien automatisch auf den Computer heruntergeladen.  
  
 Nachdem Windows preinstallation Environment eingerichtet wurde, wird der Assistent für vollständige Systemwiederherstellung gestartet. Der Assistenten können Sie den Computer von einer früheren Sicherung wiederherstellen. Sie können auch die Umgebung für die Wiederherstellung verwenden, um eine Sicherung auf einem neuen Computer mit vergleichbarer Hardware wiederherzustellen.  
  
 In den meisten Fällen sind die Programmdateien und Treiber, die auf die Umgebung für die Wiederherstellung enthalten alle, die benötigt wird, um den neuen bzw. wiederhergestellten Computer neu starten. Abhängig von der neuen bzw. wiederhergestellten Computerhardware Umgebung für die Systemwiederherstellung möglicherweise alle des Speichers und keine Netzwerkadapter-Treiber, die erforderlich sind, wenn Sie den neuen oder wiederhergestellten Computer neu starten. Der Assistent für vollständige Systemwiederherstellung bietet Ihnen Gelegenheit zum Installieren von Treibern, bei Bedarf. Informationen dazu, wie Ihre Hardwaretreiber, finden Sie unter [Wo finde ich die Treiber für die Hardware?](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_FindDrivers). Informationen dazu, wie Sie das Medium für die Wiederherstellung verwenden, finden Sie unter [mit dem Assistenten für vollständige Systemwiederherstellung](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_Using).  
  
##  <a name="BKMK_CreateBootable"></a>Erstellen Sie einen startbaren USB-Speichersticks zur Wiederherstellung eines Clientcomputers  
 Wenn Sie einen Clientcomputer aus einer vorhandenen Sicherung wiederherstellen müssen, aber nicht finden, die mit dem Server (in Windows Server Essentials) gelieferte Wiederherstellungs-CD oder Sie nicht den clientwiederherstellungsdienst auf dem Server (in Windows Server Essentials) einrichten möchten, können Sie einen startbaren USB-Speicherstick erstellen. Dann können den USB-Speicherstick an den Clientcomputer starten und das System wiederherstellen. Das USB-Flashlaufwerk, mit denen Sie muss über mindestens 1GB oder größer.  
  
#### <a name="to-create-a-bootable-usb-flash-drive"></a>Erstellen ein startbares USB-Speichersticks  
  
1.  Öffnen der **Dashboard**.  
  
2.  Klicken Sie auf die **Geräte** Registerkarte.  
  
3.  In **Aufgaben** Bereich, klicken Sie auf **Einstellungen anpassen Computersicherung und Dateiversionsverlauf**.  
  
    > [!NOTE]
    >  Klicken Sie in Windows Server Essentials auf **Clientcomputer-Sicherungsaufgaben**.  
  
4.  Klicken Sie auf die **Tools** Registerkarte, und klicken Sie dann auf **Create Key** in der **computerwiederherstellung** Abschnitt. Das Erstellen Computer Recovery Key-Assistent wird geöffnet.  
  
5.  Legen Sie eine 1GB oder größer USB Flash-Laufwerk auf dem Server, und folgen Sie dann die Anweisungen im Assistenten.  
  
    > [!CAUTION]
    >  Alle Daten auf dem USB-Speicherstick werden gelöscht.  
  
##  <a name="BKMK_Using"></a>Mithilfe des Assistenten für vollständige Wiederherstellung  
 Nachdem Sie die Wiederherstellung erfolgreich mit Speicherstick Medien, clientwiederherstellungsdienst oder USB-, starten Sie den Computer, und stellen Sie sicher, dass alle Hardware Treiber geladen werden, auf dem wiederhergestellten oder neuen Clientcomputer, den Assistenten für vollständige Systemwiederherstellung angezeigt wird. Dieser Assistent ermöglicht den Zugriff auf den Server, die computersicherung und die Quell-Volumes auf dem Computer wiederherstellen möchten, und der Wiederherstellungsvorgang ausgeführt wird.  
  
> [!NOTE]
>   Windows Server Essentials unterstützt die folgenden Wiederherstellungsszenarien nicht:  
>   
>  -   Wiederherstellen eines Master Boot Record (MBR)-Datenträgers zu einem Unified Extensible Firmware Interface (UEFI)-basierten Computer.  
> -   Wiederherstellen einer UEFI-/GPT-Sicherung auf einem BIOS-System.  
>   
>  Wenn Sie Daten in einem dieser Szenarien wiederherstellen, Sie können für den Systemstart nicht. Darüber hinaus können Sie nicht möglicherweise Festplatten verwenden, die größer als zwei Terabyte sind.  
  
 **Erforderliche Komponenten:**  
  
-   Vor dem Starten der vollständigen Systemwiederherstellung, verwenden Sie ein Netzwerkkabel (eine Kabelverbindung) um den Computer mit demselben Netzwerk wie der Server zu verbinden. Stellen Sie sicher, dass Sie Zugriff auf alle Festplatten auf dem Clientcomputer haben.  
  
    > [!WARNING]
    >  Versuchen Sie nicht, eine vollständige Systemwiederherstellung auf einem Computer ausführen, die eine drahtlose Verbindung mit dem Netzwerk verwendet.  
  
-   Wenn Sie wissen, dass der Computer wichtige Netzwerk- oder Treiber für Speichergeräte fehlen, müssen Sie zum Suchen und diese Treiber auf einen Speicherstick kopieren, bevor Sie die vollständige Systemwiederherstellung zu starten. Wenn Sie Medium für die vollständige Systemwiederherstellung, die auf CD bereitgestellte verwenden, muss die CD für Windows Server Essentials: Auf dem Laufwerk während des Starts der vollständigen Systemwiederherstellung bleiben. Aus diesem Grund sollten Sie nicht die fehlenden Treiber auf eine CD oder DVD kopieren, es sei denn, Sie ein zweites CD-/DVD-Laufwerk haben. Kopieren Sie die fehlenden Treiber stattdessen auf einem USB-Speicherstick.  
  
     Weitere Informationen dazu, wie Sie die Treiber für Ihren Computer zu finden, finden Sie unter [Wo finde ich die Treiber für die Hardware?](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_FindDrivers)  
  
-   Für Windows Server Essentials: Wenn Sie die Windows Server Essentials-Wiederherstellungs-CD nicht finden, können Sie einen startbaren USB-Speicherstick erstellen. Weitere Informationen finden Sie unter [erstellen Sie einen startbaren USB-Speichersticks zur Wiederherstellung eines Clientcomputers](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_CreateBootable).  
  
#### <a name="to-use-the-full-system-restore-wizard"></a>Verwenden Sie den Assistenten für vollständige Systemwiederherstellung  
  
1.  Führen Sie einen der folgenden:  
  
    -   Windows Server Essentials: Schalten Sie auf dem Clientcomputer, den Sie wiederherstellen möchten, legen Sie das Wiederherstellungsmedium, und deaktivieren Sie dann den Computer.  
  
         Schalten Sie den Computer erneut, und wählen Sie dann das CD-/DVD-Laufwerk während der Power On Self Test (POST), drücken Sie die entsprechende Funktionstaste (F-Taste), um das Startgerätemenü aufzurufen. Der Windows-Start-Manager wird gestartet.  
  
    -   Windows Server Essentials: Wenn Sie den clientwiederherstellungsdienst verwenden, einen Neustart der Computer die **Boot from Network** Option. Andernfalls starten Sie den Computer mit dem USB-Stick.  
  
         Schalten Sie den Computer erneut, und während der Power On Self Test (POST), drücken Sie die entsprechende Funktionstaste (F-Taste), um das Startgerätemenü aufzurufen, und wählen Sie dann **Boot from Network** (oder Sie können auch über den USB-Stick zu starten). Der Windows-Start-Manager wird gestartet.  
  
    > [!NOTE]
    >  Überprüfen Sie die Dokumentation des Computerherstellers, um zu bestimmen, welche Funktionstaste Sie Drücken der startgerätemenü.  
  
2.  Das Medium für die Systemwiederherstellung enthält (x86) 32-Bit- und 64-Bit (x 64)-Startoptionen. Wählen Sie in der Windows-Start-Manager, **Full System Restore (x86)** oder **Full System Restore (x64)**. Wenn der Treiber für die Computerhardware 32-Bit-sind, wählen Sie die x86. Wenn sie 64-Bit-sind, wählen Sie x64. Windows-Dateien werden geladen, und der Assistent für vollständige Systemwiederherstellung überprüft, um sicherzustellen, dass alle Hardwaretreiber verfügbar sind.  
  
3.  In der **Assistent vollständige Systemwiederherstellung** Fenster, wählen Sie Ihre bevorzugte Sprache, und klicken Sie dann auf den Pfeil.  
  
4.  Wählen Sie die entsprechende **Uhrzeit und Währungsformat**, und die **Tastatur oder Eingabemethode** für diesen Computer. Klicken Sie auf **weiterhin**.  
  
5.  Wenn Treiber fehlen, wird die Meldung, dass der Wiederherstellungsvorgang nicht überprüfen kann, die Treiber angezeigt. Klicken Sie auf **schließen**, und klicken Sie dann auf das Dialogfeld Willkommen auf **Treiber laden**.  
  
    1.  Auf der **Hardware ermitteln** Dialogfeld, klicken Sie auf **Installieren von Treibern**.  
  
    2.  Legen Sie den USB-Speicherstick, der die Hardwaretreiber enthält, und klicken Sie dann auf die **Treiber installieren** Dialogfeld klicken Sie auf **Scannen**.  
  
    3.  Auf der **Treiber installieren** Dialogfeld, klicken Sie auf **OK** Wenn die Treiber gefunden wurden.  
  
    4.  Auf der **Hardware ermitteln** Dialogfeld, klicken Sie auf **Weiter**.  
  
6.  Wenn bei der ersten Prüfung alle Treiber gefunden wurden oder wenn alle wichtigen Treiber installiert sind, auf die **vollständige Systemwiederherstellung** Fenster, klicken Sie auf **Weiter**.  
  
7.  Auf der **Willkommen bei den Assistenten für vollständige Systemwiederherstellung** auf **Weiter**.  
  
8.  Der Assistent sucht nach dem Server.  
  
    1.  Wenn der Assistent den Server nicht finden kann, erhalten Sie die Möglichkeit, erneut zu suchen, oder die IP-Adresse des Servers eingeben.  
  
    2.  Wenn mehrere Server ermittelt wurden, werden Sie aufgefordert, eine auswählen.  
  
    3.  Wenn der Server befindet, ist die **melden Sie sich bei < YourServerName\ >** angezeigt wird.  
  
9. Auf der **melden Sie sich bei < YourServerName\ >** geben *< AdministratorAccountName\ >* in der **Benutzernamen** Textfeld, und das Kennwort des Administratorkontos in der **Kennwort** Textfeld ein, und klicken Sie dann auf **Weiter**.  
  
    > [!IMPORTANT]
    >  Sie müssen ein Administratorkonto verwenden, die in Englisch erstellt wird. Wenn Sie eine nicht verfügen, müssen Sie ein neues Administratorkonto erstellen. Öffnen Sie hierzu zunächst die **Benutzer** Registerkarte auf dem serverdashboard, legen Sie dann die Tastatursprache auf Englisch, und führen Sie die **Hinzufügen eines Benutzerkontos** Task, um das Administratorkonto zu erstellen. Als Nächstes verwenden Sie das neue Administratorkonto, um zum Wiederherstellen des Clientcomputers fortzusetzen.  
  
10. Auf der **wählen Sie einen Computer wiederherstellen** Seite, wählen Sie den Computer, die Sie wiederherstellen möchten, und klicken Sie dann auf **Weiter**. Sie haben die Wahl **< ComputerName\ >: (dieser Computer)**, oder wählen Sie einen anderen Computer im Netzwerk aus der **einem anderen Computer** Dropdownliste.  
  
    > [!NOTE]
    >  Ist dies ein Computer, die mit dem Server (z.B. ein neues oder einem neuen Zweck zugeführten Computer), unbekannt ist die **dieses Computers** Option wird nicht angezeigt.  
  
11. Auf der **wählen Sie eine Sicherung wiederherstellen** Seite, überprüfen Sie die Liste der verfügbaren Sicherungen, und wählen Sie die App, die Sie auf dem Computer wiederherstellen möchten.  
  
    > [!NOTE]
    >  Es wird empfohlen, dass Sie eine erfolgreiche Sicherung (grünes Häkchen) auswählen. Dadurch wird sichergestellt, dass alle System- und Datendateien erfolgreich wiederhergestellt werden.  
  
12. (*optionale*) Wählen Sie eine Sicherung aus, und klicken Sie dann auf **Details** zum Öffnen der **Sicherungsdetails** Seite und Weitere Informationen zu der Sicherung anzuzeigen. Verwenden Sie die Informationen auf der **Sicherungsdetails** Seite mehrere Sicherungen miteinander vergleichen Hilfe Sie entscheiden, welche Sicherung am besten geeignet ist. Klicken Sie auf **schließen** auf die **Sicherungsdetails** Seite zurückkehren zu den **wählen Sie eine Sicherung wiederherstellen** Seite.  
  
13. Auf der **wählen Sie eine Sicherung wiederherstellen** Seite, wählen Sie eine Sicherung aus, und klicken Sie dann auf die **Weiter** Schaltfläche.  
  
14. Auf der **Wiederherstellungsoption auswählen** auf eine der folgenden, und klicken Sie dann auf **Weiter**.  
  
    > [!NOTE]
    >  Diese Seite wird nicht angezeigt, wenn die automatische Partitionierung nicht unterstützt wird.  
  
    1.  **Damit der Assistent vollständig auf den Computer (empfohlen) wiederherstellen**. Diese Option trägt dazu bei, die der Computer in den Zustand wiederhergestellt wird, die sie unmittelbar vor der Uhrzeit und Datum der Sicherung, die Sie ausgewählt haben. Wenn Sie diese Option auswählen, fahren Sie mit Schritt15 fort.  
  
    2.  **Wiederherzustellende Volumes auswählen (erweitert)**. Mit dieser Option können Sie die Volumes auswählen, die Sie wiederherstellen möchten und wo Sie wiederhergestellt werden sollen. Sie können auch Partitionen auf der Festplatte erstellen.  
  
15. Auf der **wiederherzustellende Volumes auswählen** Seite, Sie können die Volumes, die Sie wiederherstellen möchten.  
  
    > [!NOTE]
    >  Diese Seite wird angezeigt, wenn mehrere Festplatten auf dem Backup Quell-PC vorhanden sind oder das Ziellaufwerk für die Wiederherstellung weniger Speicherplatz als dem sicherungsquelllaufwerk hat.  
  
    1.  Der Assistent versucht, die Quell- und Ziel-Volumes anzupassen. Sie sollten überprüfen, ob die Standardzuordnung korrekt ist.  
  
        1.  Um ein Volume zu deaktivieren, klicken Sie auf den Pfeil im für das Volume, und klicken Sie dann auf **keine**.  
  
        2.  Wenn Sie die Volumes ausgewählt haben, klicken Sie auf **Weiter**.  
  
    2.  Wenn das Quellvolume und das Zielvolume dieselbe Größe aufweisen, oder die Größe der Datenquelle kleiner als das Zielvolume ist, wird Sie zwischen den beiden ein grüner Pfeil angezeigt. Befindet sich Volumegrößen (wobei das Quellvolume größer als das Zielvolume ist), wird ein rotes X zwischen der Quell- und Ziel angezeigt.  
  
        > [!NOTE]
        >  Ein rotes X kann auch angezeigt, wenn:  
        >   
        >  -   Die Datenträgersektorgröße des Quellvolumes stimmt nicht mit der Sektorgröße der Festplatte des Zielvolumes überein. Dies kann vorkommen, wenn Sie den physischen Datenträger mit einem Datenträger ersetzen, die eine anderen Sektorgröße hat, oder Speicherplatz konfiguriert wurde (mit einer anderen Sektorgröße als die des physischen Datenträgers kann).  
        > -   Sie erreichen die Clusteranzahl. Um das Quellvolume im Zielvolume wiederherzustellen, müssen Sie das Zielvolume mit der gleichen Clustergröße wie das Quellvolume formatieren. Wenn das Zielvolume zu groß ist und die Clustergröße zu klein ist, können Sie die Clusteranzahl erreichen.  
  
        1.  Klicken Sie auf **ausführen Disk Manager (erweitert)**, und erstellen Sie ein neues Volume, das die gleiche Größe wie das System reservierte Volume ist.  
  
            > [!NOTE]
            >  Wenn ein Clientcomputer Unified Extensible Firmware Interface (UEFI) basiert ist, können Sie mit der **Diskpart** Tool, um den Systemdatenträger initialisieren. Öffnen Sie dazu ein Befehlsfenster (drücken Sie Strg+Alt+Umschalt unter Windows PE 5Sekunden lang), führen **diskpart.exe**, und führen Sie die folgenden Diskpart-Befehle:  
            >   
            >  1.  **DISKPART > Liste Datenträger**  
            > 2.  **DISKPART > Wählen Sie den Datenträger #***< Datenträger\Durchschnittl >*  
            > 3.  **DISKPART > bereinigen**  
            > 4.  **DISKPART > Gpt konvertieren**  
            > 5.  **DISKPART > Erstellen Sie die Größe der Partition Efi =***100* (wo *100* eine Beispiel-Partitionsgröße in MB ist, sollte der ursprünglichen Partition identisch sein)  
            > 6.  **DISKPART > Erstellen Sie die Größe der Partition MSR-Partition =***128* (wo *128* eine Beispiel-Partitionsgröße in MB ist, sollte der ursprünglichen Partition identisch sein)  
            > 7.  **DISKPART > Beenden**  
  
        2.  *(Optional) *Wählen Sie die Option **weisen Sie einen Laufwerkbuchstaben oder -Pfad**.  
  
        3.  Formatieren Sie das Volume als **NTFS**.  
  
        4.  Nach Abschluss der Formatierung mit der rechten Maustaste in des neue Systemvolume, und klicken Sie dann auf **Partition als aktiv markieren**.  
  
        5.  Wenn Sie weitere Volumes mit anderen Volumes in die Sicherung benötigen, wiederholen Sie die Schritte *Ii* über *iv* erstellen und die Volumes aktivieren, und schließen Sie dann **Datenträgerverwaltung**.  
  
        6.  Auf der **wiederherzustellende Volumes auswählen** Seite, Karte, die vom System reservierte Volume der Sicherungsquelle dem Volume mit der gleichen Größe, die Sie in Schritterstellten *v*.  
  
        7.  Ordnen Sie alle anderen Quellvolumes den entsprechenden Zielvolumes zu.  
  
        8.  Klicken Sie auf **Weiter**, mit der Wiederherstellung fortzufahren.  
  
16. Auf der **wiederherzustellende Volumes bestätigen** Seite, überprüfen Sie die Zuordnung, und klicken Sie dann auf **Weiter**. Wenn Sie keine Änderungen vornehmen müssen, klicken Sie auf **wieder**, und wiederholen Sie Schritt14 fort.  
  
17. Die **wiederherstellen < ComputerName\ > in < Datum und Uhrzeit der Backup\ >** Seite wird der Fortschritt des Wiederherstellungsvorgangs.  
  
18. Auf der **die Wiederherstellung erfolgreich abgeschlossen** Seite, entfernen Sie das Wiederherstellungsmedium, und klicken Sie dann auf **Fertig stellen**. Der Computer neu gestartet.  
  
    > [!IMPORTANT]
    >  Wenn BitLocker Drive Encryption vor der Wiederherstellung auf dem Computer aktiviert wurde, müssen Sie BitLocker nach dem Neustart des Computers manuell aktivieren.  
  
##  <a name="BKMK_FindDrivers"></a>Wo finde ich die Treiber für die Hardware?  
 Abhängig von der neuen bzw. wiederhergestellten Computerhardware das Wiederherstellungsmedium möglicherweise alle des Speichers und keine Netzwerkadapter-Treiber, die erforderlich sind, wenn Sie den wiederhergestellten Computer neu starten. Sie müssen bestimmen, welche Treiber fehlt, suchen Sie nach auf dem vorliegenden Medium oder auf der Website des Herstellers s, auf einen Speicherstick kopieren und dann kopieren Sie sie vom Speicherstick auf den neuen oder wiederhergestellten Computer aus, wenn Sie den Assistenten für vollständige Systemwiederherstellung ausführen.  
  
 Wenn ein Computer gesichert wird, werden die Treiber für den Computer in die Sicherung gespeichert. Wenn das Wiederherstellungsmedium nicht alle Treiber, die Sie benötigen enthalten, können Sie eine Sicherung für diesen Computer öffnen und kopieren Sie die Treiber auf einem USB-Speicherstick.  
  
#### <a name="to-copy-drivers-from-a-backup-to-a-usb-flash-drive"></a>Treiber aus einer Sicherung auf einem USB-Speicherstick zu kopieren.  
  
1.  Öffnen Sie das Dashboard auf einem anderen Computer.  
  
2.  Klicken Sie auf **Geräte**, und klicken Sie dann auf dem Computer, die für den Treiber erforderlich.  
  
3.  Klicken Sie auf **Wiederherstellen von Dateien oder Ordner für den Computer**. Das Wiederherstellen von Dateien oder Ordner-Assistent wird geöffnet.  
  
4.  Klicken Sie auf der letzten erfolgreichen Sicherung aus, und klicken Sie dann auf **Weiter**.  
  
5.  Klicken Sie auf ein Volume, um es zu öffnen, und klicken Sie dann auf **Weiter**. Es wird ein Fenster geöffnet, die die Dateien und Ordner in die Sicherung enthält.  
  
6.  Legen Sie das USB-Flashlaufwerk in einen USB-Anschluss auf dem Computer, und kopieren Sie die Treiber für die vollständige Systemwiederherstellung Ordner auf den USB-Speicherstick.  
  
    > [!NOTE]
    >  Möglicherweise müssen Sie klicken Sie auf **eine Ebene nach oben** bis zu den Stamm des Systemvolumes.  
  
7.  Entfernen Sie den Speicherstick, und fügen sie in den Computer, den Sie wiederherstellen.  
  
 Das USB-Flashlaufwerk können Sie um die Treiber für Ihren Computer zu installieren, wenn Sie es wiederherstellen. Das Wiederherstellen von Dateien oder Ordner-Assistent sucht nach weiteren Treibern auf diesem USB-Speicherstick während des vollständigen Systemwiederherstellungs-Assistenten. Die Treiber, die Sie am wahrscheinlichsten benötigen werden die Treiber für Netzwerkadapter und Treiber für Speichergeräte.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten der Sicherung und Wiederherstellung](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
