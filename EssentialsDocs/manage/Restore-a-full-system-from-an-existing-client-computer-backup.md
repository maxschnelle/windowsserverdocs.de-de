---
title: Wiederherstellen eines vollständigen Systems aus einer vorhandenen Clientcomputersicherung
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 47e498a6-1b71-47de-88f6-8c13c221d108
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 37e4d45f6bd34d77fbbf3cbabcd66a776b624c19
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852643"
---
# <a name="restore-a-full-system-from-an-existing-client-computer-backup"></a>Wiederherstellen eines vollständigen Systems aus einer vorhandenen Clientcomputersicherung

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials 
  
 Hardware- und Betriebssystemfehler sind zwar selten, können aber durchaus auftreten. Ein fehlerhafter Lüfter könnte zu einer Überhitzung der Hauptplatine des Computers führen, sodass diese nicht mehr verwendet werden kann. Das Betriebssystem könnte beschädigt werden, sodass es nicht mehr gestartet werden kann. Durch Feuer und Wasser kann die Hardware dauerhaft beschädigt werden. Bei einem Festplattenlaufwerk kann ein Fehler auftreten, oder Sie entscheiden, es gegen ein größeres Festplattenlaufwerk auszutauschen.  
  
 Dieses Dokument enthält Informationen zu den folgenden Themen:  
  
-   [Was ist die vollständige Systemwiederherstellung des Computers?](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_WhatIs)  
  
-   [Wie funktioniert die Umgebung für die Systemwiederherstellung?](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_HowDoes)  
  
-   [Erstellen eines Start baren USB-Speicherstick zum Wiederherstellen eines Client Computers](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_CreateBootable)  
  
-   [Verwenden des Assistenten für die vollständige System Wiederherstellung](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_Using)  
  
-   [Wo finde ich die Treiber für die Hardware?](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_FindDrivers)  
  
##  <a name="what-is-computer-full-system-restore"></a><a name="BKMK_WhatIs"></a>Was ist die vollständige Systemwiederherstellung des Computers?  
 Wenn Sie ein Festplattenlaufwerk austauschen oder auf dem Computer ein Fehler auftritt, der dazu führt, dass der Computer nicht mehr verwendet oder gestartet werden kann, können Sie das System aus einer früheren Sicherung des Computers wiederherstellen. Bei einer vollständigen Systemwiederherstellung wird das System wieder in den Zustand versetzt, in dem es sich zum Zeitpunkt der Sicherung befand.  
  
> [!IMPORTANT]
>  Bei Computerhardware, z. B. einer Systemplatine, die nicht der ausgetauschten Computerhardware entspricht, ist es nicht möglich, eine vollständige Systemwiederherstellung auszuführen. Ein installiertes Betriebssystem hängt stark von der zugrunde liegenden Hardware des Computers ab. Auf einer Festplatte, die mindestens genauso groß ist wie die ausgetauschte Festplatte, kann hingegen eine vollständige Systemwiederherstellung ausgeführt werden.  
  
 Bei einer vollständigen Systemwiederherstellung haben Sie die Möglichkeit, eine bestimmte Computersicherung auszuwählen, um das System mit allen dem Benutzer vor Auftreten des Fehlers, einer Katastrophe oder dem Diebstahl vertrauten Anwendungen, Konfigurationen und Einstellungen wiederherzustellen. Außerdem können Sie die Volumes auswählen, die Sie wiederherstellen möchten.  
  
 Beachten Sie beim Planen und Vorbereiten der vollständigen Systemwiederherstellung auf einem Netzwerkcomputer Folgendes:  
  
### <a name="windows-preinstallation-environment"></a>Windows Preinstallation Environment  
 Windows Preinstallation Environment (Windows PE) ist ein minimales Betriebssystem, das zum Vorbereiten eines Computers für die Installation von Windows vorgesehen ist. Bei Servern, auf denen Windows Server Essentials ausgeführt wird, wird Windows PE automatisch installiert, wenn Sie das Wiederherstellungs Medium auf einem Computer einfügen, der wieder hergestellt werden soll. Bei Servern, auf denen Windows Server Essentials ausgeführt wird, wird Windows PE automatisch installiert, wenn Sie den Computer mit dem Client Wiederherstellungs Dienst oder dem USB-Speicherstick starten.  
  
 Windows PE unterstützt keine Funkverbindungen. Daher muss der wiederherzustellende Computer physisch mit dem kleinen Firmennetzwerk verbunden sein.  
  
### <a name="bitlocker"></a>BitLocker  
 BitLocker-Laufwerkverschlüsselung (BitLocker) ist ein Datenschutz Feature, das in einigen Versionen von Windows Vista, Windows 7 und Windows 8 verfügbar ist. BitLocker bietet Schutz vor Datendiebstahl oder der Offenlegung von Daten auf Computern, die verloren gehen oder gestohlen werden, und ermöglicht die sichere Löschung von Daten, wenn Computer außer Betrieb gesetzt werden.  
  
 **Für Windows Server Essentials:** Wenn der Computer, den Sie wiederherstellen müssen, mit BitLocker verschlüsselt wurde (unabhängig davon, ob es sich nur um das Betriebssystem Laufwerk oder das Betriebssystem Laufwerk und einzelne oder mehrere andere Festplattenlaufwerke handelte), Sie können weiterhin das vollständige System Wiederherstellungs Medium verwenden, das auf der mit Ihrem Server bereitgestellten CD und dem Assistenten für die vollständige Systemwiederherstellung enthalten ist, um das Festplatten Abbild, einschließlich des Betriebssystems, von einer Sicherung erneut zu installieren und die Daten auf dem neuen oder reparierten Computer wiederherzustellen.  
  
 **Für Windows Server Essentials:** Wenn der Computer, den Sie wiederherstellen möchten, mithilfe von BitLocker verschlüsselt wurde (unabhängig davon, ob es sich nur um das Betriebssystem Laufwerk oder das Betriebssystem Laufwerk und einzelne oder mehrere andere Festplattenlaufwerke handelte), können Sie den Assistenten für die vollständige Systemwiederherstellung weiterhin verwenden, um das Festplatten Abbild, einschließlich des Betriebssystems, über eine Sicherung erneut zu installieren.  
  
 Wenn vom Server Laufwerke, Ordner und Dateien gesichert werden, wird auf dem Server eine unverschlüsselte Version gespeichert. Diese unverschlüsselte Version wird während der vollständigen Systemwiederherstellung auf den Computer kopiert.  
  
> [!NOTE]
>  Nach einer erfolgreichen vollständigen Systemwiederherstellung müssen Sie BitLocker auf dem Computer erneut aktivieren.  
>   
>  Anweisungen zum Aktivieren von BitLocker auf Computern, auf denen Windows 8 ausgeführt wird, finden Sie unter [BitLocker: Aktivieren von BitLocker](https://go.microsoft.com/fwlink/p/?LinkID=254918).  
>   
>  Anweisungen zum Aktivieren von BitLocker auf Computern, auf denen Windows 7 ausgeführt wird, finden Sie unter [BitLocker-Laufwerkverschlüsselung Schritt-für-Schritt-Anleitung für Windows 7](https://go.microsoft.com/fwlink/p/?LinkId=140225).  
  
 Weitere grundlegende Informationen zur BitLocker-Laufwerkverschlüsselung finden Sie unter [BitLocker: Häufig gestellte Fragen (FAQ)](https://go.microsoft.com/fwlink/p/?LinkID=254917).  
  
### <a name="encrypting-file-system-encrypted-files"></a>EFS-verschlüsselte Dateien  
 Das Feature EFS (Encrypting File System, verschlüsselndes Dateisystem) unter Windows ermöglicht eine zusätzliche benutzerbasierte Verschlüsselung auf Dateiebene, sodass unterschiedliche Sicherheitsstufen implementiert werden können, wenn mehrere Benutzer denselben Computer verwenden. Es ist wichtig zu wissen, dass EFS-verschlüsselte Ordner und Dateien im Gegensatz zu BitLocker-verschlüsselten Laufwerken in einer Computersicherung weiterhin verschlüsselt sind. EFS ist in Windows XP Home Edition, Windows Vista Starter, Windows Vista Home Basic, Windows Vista Home Premium, Windows 7 Starter, Windows 7 Home Basic, Windows 7 Home Premium oder Windows 8 nicht verfügbar. Es ist nur in Windows 8 Pro verfügbar.  
  
> [!WARNING]
>  Anders als bei BitLocker können Sie auf mit EFS geschützte Dateien nur unter dem Betriebssystem zugreifen, mit dem sie verschlüsselt wurden.  
  
### <a name="disk-partitions"></a>Datenträgerpartitionen  
 Wenn die Festplatte des neuen Computers mindestens genauso groß ist wie die ursprüngliche Festplatte, wird sie automatisch neu formatiert und partitioniert. Die Einzelheiten können Sie dem nachfolgenden Diagramm entnehmen:  
  
|Ursprünglicher Computer|Wiederhergestellter oder neuer Computer|  
|-----------------------|------------------------------|  
|Einzelner Datenträger mit mehreren Partitionen|Einzelner Datenträger mit mehreren Partitionen; zusätzlicher Speicherplatz wird der letzten Partition zugeordnet|  
|Einzelner Datenträger mit einer Partition|Einzelner Datenträger mit einer Partition; der gesamte verfügbare Speicherplatz wird für die eine Partition verwendet|  
  
> [!NOTE]
>  Wenn sich der ursprüngliche und der wiederhergestellte oder neue Computer in Datenträgergröße und Partitionslayout voneinander unterscheiden, müssen Sie mithilfe der Datenträgerverwaltung die entsprechenden Partitionen auf dem wiederhergestellten oder neuen Computer erstellen. Dazu können Sie den Assistenten für die vollständige Systemwiederherstellung verwenden.  
  
### <a name="raid-and-dynamic-disks"></a>RAID- und dynamische Datenträger  
 Das Sichern von RAID-Datenträgern (Redundant Array of Independent Disks) und dynamischen Datenträgern wird nicht unterstützt.  
  
##  <a name="how-does-the-system-restore-environment-work"></a><a name="BKMK_HowDoes"></a>Wie funktioniert die Umgebung für die Systemwiederherstellung?  
 Das mit Windows Server-&reg; 2012 Essentials bereitgestellte System Wiederherstellungs Medium wird Windows Preinstallation Environment (Windows PE) auf dem Computer installiert. Windows PE hat die MS-DOS-Umgebung abgelöst und enthält die wichtigen Programmdateien für Windows. In Windows Server Essentials gibt es zwei unterstützte Methoden zum Wiederherstellen eines Systems: mit dem Client Wiederherstellungs Dienst, der ein Netzwerk verwendet und nicht von einem Medium abhängig ist, oder über den USB-Speicherstick.  
  
> [!NOTE]
>  Windows PE unterstützt keine Funkverbindungen. Daher muss der wiederherzustellende Computer physisch mit dem kleinen Firmennetzwerk verbunden sein.  
  
 Die Umgebung für die Systemwiederherstellung enthält die Programmdateien für 32-Bit (x86) und 64-Bit (x64). Wählen Sie nach dem Einlegen des Mediums für die Systemwiederherstellung die passende Version der Dateien aus. Die Standardversion ist 32-Bit (x86). Diese wird automatisch ausgewählt, wenn Sie nicht innerhalb von 30 Sekunden eine Auswahl treffen. Wenn auf dem Server aktualisierte Programmdateien für die vollständige Systemwiederherstellung vorhanden sind, werden diese aktualisierten Dateien automatisch auf den Computer heruntergeladen.  
  
 Nachdem Windows Preinstallation Environment eingerichtet wurde, wird der Assistent für die vollständige Systemwiederherstellung gestartet. Dieser Assistent hilft Ihnen bei der Wiederherstellung des Computers aus einer früheren Sicherung. Sie können die Umgebung für die Systemwiederherstellung auch verwenden, um eine Sicherung auf einem neuen Computer mit vergleichbarer Hardware wiederherzustellen.  
  
 In den meisten Fällen reichen die in der Umgebung für die Systemwiederherstellung enthaltenen Programmdateien und Treiber aus, um den neuen oder wiederhergestellten Computer neu zu starten. Je nach der Hardware des neuen bzw. wiederhergestellten Computers enthält die Umgebung für die Systemwiederherstellung möglicherweise nicht alle Treiber für die Speicher- und Netzwerkadapter, die erforderlich sind, wenn Sie den neuen oder wiederhergestellten Computer neu starten. Der Assistent für die vollständige Systemwiederherstellung bietet Ihnen bei Bedarf die Gelegenheit zum Installieren von Treibern. Informationen dazu, wie Sie die Treiber für Ihre Hardware finden können, finden Sie unter [Wo finde ich die Treiber für die Hardware?](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_FindDrivers). Informationen zur Verwendung des Mediums für die Systemwiederherstellung finden Sie unter [Verwenden des Assistenten für die vollständige Systemwiederherstellung](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_Using).  
  
##  <a name="create-a-bootable-usb-flash-drive-to-restore-a-client-computer"></a><a name="BKMK_CreateBootable"></a>Erstellen eines Start baren USB-Speicherstick zum Wiederherstellen eines Client Computers  
 Wenn Sie einen Client Computer aus einer vorhandenen Sicherung wiederherstellen müssen, die auf dem Server (in Windows Server Essentials) vorhandene Wiederherstellungs-CD jedoch nicht finden kann, oder Sie den Client Wiederherstellungs Dienst auf dem Server (in Windows Server Essentials) nicht einrichten möchten. können Sie einen Start fähigen USB-Speicherstick erstellen. Sie können den USB-Speicherstick dann verwenden, um den Clientcomputer zu starten und das System wiederherzustellen. Der verwendetet USB-Speicherstick muss über mindestens 1 GB verfügen.  
  
#### <a name="to-create-a-bootable-usb-flash-drive"></a>So erstellen Sie einen startfähigen USB-Speicherstick  
  
1.  Öffnen Sie das **Dashboard**.  
  
2.  Klicken Sie auf die Registerkarte **Geräte**.  
  
3.  Klicken Sie im Bereich **Aufgaben** auf **Einstellungen für Computersicherung und Dateiversionsverlauf anpassen**.  
  
    > [!NOTE]
    >  Klicken Sie in Windows Server Essentials auf **Client Computer-Sicherungs Tasks**.  
  
4.  Klicken Sie auf die Registerkarte **Extras** und anschließend im Abschnitt **Computerwiederherstellung** auf **Schlüssel erstellen**. Der Assistent "Computerwiederherstellungsschlüssel erstellen" wird geöffnet.  
  
5.  Stecken Sie einen USB-Speicherstick mit 1 GB in den Server ein, und folgen Sie anschließend den Anweisungen des Assistenten.  
  
    > [!CAUTION]
    >  Alle Daten auf dem USB-Speicherstick werden gelöscht.  
  
##  <a name="using-the-full-system-restore-wizard"></a><a name="BKMK_Using"></a>Verwenden des Assistenten für die vollständige System Wiederherstellung  
 Nachdem Sie den Computer mit dem Wiederherstellungsmedium, Clientwiederherstellungsdienst oder USB-Speicherstick erfolgreich gestartet und überprüft haben, ob alle Hardwaretreiber auf dem wiederhergestellten oder neuen Clientcomputer geladen wurden, wird der Assistent für die vollständige Systemwiederherstellung angezeigt. Mithilfe dieses Assistenten können Sie auf den Server, die Computersicherung und die Quellvolumes zugreifen, die Sie auf dem Computer wiederherstellen möchten. Außerdem wird der Wiederherstellungsvorgang ausgeführt.  
  
> [!NOTE]
>   Die folgenden Wiederherstellungs Szenarien werden von Windows Server Essentials nicht unterstützt:  
> 
> - Wiederherstellen eines MBR-Datenträgers (Master Boot Record) auf einem auf einem Unified Extensible Firmware Interface (UEFI) basierenden Computer.  
>   -   Wiederherstellen einer UEFI-/GPT-Sicherung in einem BIOS-System  
> 
>   Wenn Sie Daten in einem dieser Szenarien wiederherstellen, können Sie das System nicht starten. Außerdem können Sie möglicherweise keine Festplatten verwenden, die größer als zwei Terabyte sind.  
  
 **Voraussetzung**  
  
-   Binden Sie vor dem Starten der vollständigen Systemwiederherstellung den Computer mithilfe eines Netzwerkkabels in das Netzwerk ein, in dem sich der Server befindet. Stellen Sie sicher, dass Sie Zugriff auf alle Festplatten des Clientcomputers haben.  
  
    > [!WARNING]
    >  Versuchen Sie nicht, eine vollständige Systemwiederherstellung auf einem Computer auszuführen, der über eine Funkverbindung in das Netzwerk eingebunden ist.  
  
-   Wenn Sie wissen, dass auf dem Computer wichtige Treiber für das Netzwerk oder für Speichergeräte fehlen, müssen Sie diese Treiber suchen und auf einen Speicherstick kopieren, bevor Sie die vollständige Systemwiederherstellung starten. Für Windows Server Essentials: Wenn Sie das auf CD bereitgestellte Medium für die vollständige Systemwiederherstellung verwenden, muss die CD während des Start Teils der vollständigen Systemwiederherstellung im Laufwerk bleiben. Kopieren Sie daher die fehlenden Treiber nicht auf eine CD oder DVD, es sei denn, Sie verfügen über ein zweites CD-/DVD-Laufwerk. Kopieren Sie die fehlenden Treiber stattdessen auf einen USB-Speicherstick.  
  
     Informationen dazu, wie Sie die Treiber für Ihren Computer finden können, finden Sie unter [Wo finde ich die Treiber für die Hardware?](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_FindDrivers)  
  
-   Für Windows Server Essentials: Wenn Sie die Windows Server Essentials-Wiederherstellungs-CD nicht finden können, können Sie einen Start fähigen USB-Speicherstick erstellen. Weitere Informationen finden Sie unter [Erstellen eines startbaren USB-Speichersticks für die Wiederherstellung eines Clientcomputers (möglicherweise in englischer Sprache)](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_CreateBootable).  
  
#### <a name="to-use-the-full-system-restore-wizard"></a>So verwenden Sie den Assistenten für die vollständige Systemwiederherstellung  
  
1. Führen Sie eine der folgenden Aktionen aus:  
  
   -   Windows Server Essentials: Schalten Sie den Client Computer ein, den Sie wiederherstellen möchten, legen Sie das Wiederherstellungs Medium ein, und schalten Sie den Computer dann aus.  
  
        Schalten Sie den Computer erneut ein, und drücken Sie während des Selbsttests (POST) die entsprechende Funktionstaste (F-Taste), um das Startgerätemenü aufzurufen. Wählen Sie dann das CD-/DVD-Laufwerk aus. Der Windows-Start-Manager wird gestartet.  
  
   -   Windows Server Essentials: Wenn Sie den Client Wiederherstellungs Dienst verwenden, starten Sie den Computer mit der Option **Boot from Network** neu. Andernfalls starten Sie den Computer mithilfe des USB-Sticks.  
  
        Schalten Sie den Computer erneut ein, und drücken Sie während des Selbsttests (Power On Self Test, POST), die entsprechende Funktionstaste (F-Taste), um das Gerätestartmenü aufzurufen, und wählen Sie **Boot from network** (oder die Möglichkeit, über den USB-Stick zu starten). Der Windows-Start-Manager wird gestartet.  
  
   > [!NOTE]
   >  Lesen Sie in der Dokumentation des Computerherstellers nach, welche Funktionstaste Sie drücken müssen, um das Startgerätemenü aufzurufen.  
  
2. Das Wiederherstellungsmedium für den Computer enthält die Startoptionen für 32-Bit (x86) und 64-Bit (x64). Wählen Sie im Windows-Start-Manager die Option **Vollständige Systemwiederherstellung (x86)** oder **Vollständige Systemwiederherstellung (x64)** aus. Wenn die Treiber für die Computerhardware in 32-Bit vorliegen, wählen Sie x86 aus. Liegen sie in 64-Bit vor, wählen Sie x64 aus. Die Windows-Dateien werden geladen, und der Assistent für die vollständige Systemwiederherstellung prüft, ob alle Hardwaretreiber verfügbar sind.  
  
3. Wählen Sie im Fenster **Assistent für die vollständige Systemwiederherstellung** die gewünschte Sprache aus, und klicken Sie dann auf den Pfeil.  
  
4. Wählen Sie für den Computer die gewünschten Optionen für **Zeit- und Währungsformat** und **Tastatur oder Eingabemethode** aus. Klicken Sie auf **Weiter**.  
  
5. Wenn Treiber fehlen, kann die Meldung vom Wiederherstellungsprozess nicht überprüft werden, ob die Treiber angezeigt werden. Klicken Sie auf **Schließen**, und klicken Sie dann im Dialogfeld "Willkommen" auf **Treiber laden**.  
  
   1.  Klicken Sie im Dialogfenster **Hardware ermitteln** auf **Treiber installieren**.  
  
   2.  Verbinden Sie den USB-Speicherstick, der die Hardwaretreiber enthält, mit dem Computer, und klicken Sie dann im Dialogfeld **Treiber installieren** auf **Suchen**.  
  
   3.  Wenn die Treiber gefunden wurden, klicken Sie im Dialogfeld **Treiber installieren** auf **OK**.  
  
   4.  Klicken Sie im Dialogfeld **Hardware ermitteln** auf **Weiter**.  
  
6. Wenn bei der ersten Prüfung alle Treiber gefunden wurden oder alle wichtigen Treiber installiert worden sind, klicken Sie im Dialogfeld **Vollständige Systemwiederherstellung** auf **Weiter**.  
  
7. Klicken Sie auf der Seite **Willkommen** auf **Weiter**.  
  
8. Es wird nach dem Server gesucht.  
  
   1.  Wenn der Server nicht gefunden werden kann, haben Sie die Möglichkeit, erneut zu suchen oder die IP-Adresse des Servers einzugeben.  
  
   2.  Wenn mehrere Server ermittelt wurden, werden Sie aufgefordert, einen auszuwählen.  
  
   3.  Wenn sich der-Server befindet, wird die Seite **Anmelden an < yourservername\>** angezeigt.  
  
9. Geben Sie auf der Seite **Anmelden an < yourservername\>** den Eintrag *< IhrServername\>* in das Textfeld **Benutzername** und das Kennwort des Administrator Kontos in das Textfeld **Kennwort ein** , und klicken Sie dann auf **weiter**.  
  
    > [!IMPORTANT]
    >  Sie müssen ein Administratorkonto verwenden, das in englischer Sprache erstellt wird. Wenn Sie nicht bereits über eines verfügen, müssen Sie ein neues Administratorkonto erstellen. Öffnen Sie dazu zuerst die Registerkarte **Benutzer** auf dem Serverdashboard, legen Sie dann die Tastatursprache auf Englisch fest, und führen Sie die Aufgabe**Benutzerkonto hinzufügen** aus, um das Administratorkonto zu erstellen. Verwenden Sie anschließend das neue Administratorkonto, um mit der Wiederherstellung des Clientcomputers fortzufahren.  
  
10. Wählen Sie auf der Seite **Wiederherzustellenden Computer auswählen** den Computer aus, den Sie wiederherstellen möchten, und klicken Sie auf **Weiter**. Sie können entweder **< Computername\>: (dieser Computer)** oder in der Dropdown Liste **anderer Computer** einen anderen Computer im Netzwerk auswählen.  
  
    > [!NOTE]
    >  Wenn es sich um einen Computer handelt, der dem Server nicht bekannt ist (z. B. einen neuen oder einem neuen Zweck zugeführten Computer), wird die Option **Dieser Computer** nicht angezeigt.  
  
11. Überprüfen Sie auf der Seite **Wiederherzustellende Sicherung auswählen** die Liste der verfügbaren Sicherungen, und wählen Sie die Sicherung aus, die auf dem Computer wiederhergestellt werden soll.  
  
    > [!NOTE]
    >  Es wird empfohlen, dass Sie eine erfolgreiche Sicherung (zu erkennen an dem grünen Häkchen) auswählen. So kann sichergestellt werden, dass alle System- und Datendateien erfolgreich wiederhergestellt werden.  
  
12. (*Optional*) Wählen Sie eine Sicherung aus, und klicken Sie dann auf **Details**, um die Seite **Sicherungsdetails** zu öffnen und weitere Informationen zu der Sicherung anzuzeigen. Anhand der Informationen auf der Seite **Sicherungsdetails** können Sie mehrere Sicherungen miteinander vergleichen, um die am besten geeignete Sicherung auszuwählen. Klicken Sie auf der Seite **Sicherungsdetails** auf **Schließen**, um zurück zur Seite **Wiederherzustellende Sicherung auswählen** zu gelangen.  
  
13. Wählen Sie auf der Seite **Wiederherzustellende Sicherung auswählen** eine Sicherung aus, und klicken Sie dann auf die Schaltfläche **Weiter**.  
  
14. Klicken Sie auf der Seite **Wiederherstellungsoption auswählen** auf eine der folgenden Optionen, und klicken Sie dann auf **Weiter**.  
  
    > [!NOTE]
    >  Diese Seite wird nicht angezeigt, wenn die automatische Partitionierung nicht unterstützt wird.  
  
    1.  **Assistent stellt den Computer vollständig wieder her (empfohlen)** . Mit dieser Option können Sie sicherstellen, dass der Computer in dem Zustand wiederhergestellt wird, in dem er sich unmittelbar vor dem Zeitpunkt der Erstellung der ausgewählten Sicherung befand. Fahren Sie mit Schritt 15 fort, wenn Sie diese Option auswählen.  
  
    2.  **Wiederherzustellende Volumes auswählen (erweitert)** . Mit dieser Option können Sie die Volumes auswählen, die wiederhergestellt werden sollen, und angeben, wo sie wiederhergestellt werden sollen. Sie können auch Partitionen auf der Festplatte erstellen.  
  
15. Auf der Seite **Wiederherzustellende Volumes auswählen** können Sie die wiederherzustellenden Volumes auswählen.  
  
    > [!NOTE]
    >  Diese Seite wird angezeigt, wenn der Sicherungsquellcomputer mehrere Festplatten aufweist oder auf dem Ziellaufwerk für die Wiederherstellung weniger Speicherplatz verfügbar ist als auf dem Sicherungsquelllaufwerk.  
  
    1. Der Assistent versucht, die Quellvolumes den Zielvolumes zuzuordnen. Überprüfen Sie, ob die Standardzuordnung korrekt ist.  
  
       1.  Zum Aufheben der Auswahl eines Volumes klicken Sie auf den Pfeil im Listenmenü für das betreffende Volume, und klicken Sie dann auf **Keine**.  
  
       2.  Klicken Sie auf **Weiter**, wenn Sie die Volumes ausgewählt haben.  
  
    2. Wenn das Quellvolume und das Zielvolume dieselbe Größe aufweisen oder das Quellvolume kleiner als das Zielvolume ist, wird zwischen beiden ein grüner Pfeil angezeigt. Wenn die Volumegrößen nicht übereinstimmen (das Quellvolume größer als das Zielvolume ist), wird zwischen dem Quellvolume und dem Zielvolume ein rotes X angezeigt.  
  
       > [!NOTE]
       >  Ein rotes X wird möglicherweise auch in folgenden Situationen angezeigt:  
       > 
       > - Die Datenträgersektorgröße des Quellvolumes stimmt nicht mit der Datenträgersektorgröße des Zielvolumes überein. Ein möglicher Grund hierfür ist, dass der physische Datenträger durch einen Datenträger mit einer abweichenden Sektorgröße ersetzt wurde oder der Speicherplatz konfiguriert wurde (dessen Sektorgröße möglicherweise von der Sektorgröße des physischen Datenträgers abweicht).  
       >   -   Sie haben die Beschränkung für die Clusteranzahl erreicht. Sie müssen das Zielvolume mit der gleichen Clustergröße wie das Quellvolume formatieren, um das Quellvolume im Zielvolume wiederherzustellen. Wenn das Zielvolume zu groß und die Clustergröße zu klein ist, erreichen Sie möglicherweise die Beschränkung für die Clusteranzahl.  
  
       1. Klicken Sie auf **Datenträgerverwaltung ausführen (erweitert)** , und erstellen Sie ein neues Volume, das dieselbe Größe wie das vom System reservierte Volume aufweist.  
  
          > [!NOTE]
          >  Wenn ein Client Computer Unified Extensible Firmware Interface (UEFI) basiert, müssen Sie den System Datenträger mit dem **DiskPart** -Tool initialisieren. Öffnen Sie dazu ein Befehlsfenster (drücken Sie unter Windows PE 5 Sekunden lang STRG+ALT+UMSCHALT), führen Sie **diskpart.exe** aus, und führen Sie dann die folgenden diskpart-Befehle aus:  
          > 
          > 1. **Datenträger der DISKPART-> Liste**  
          >    2. **DiskPart > Wählen Sie** Datenträger Anzahl < Datenträger *\>*  
          >    3. **DISKPART > bereinigt**  
          >    4. **DISKPART-> Konvertieren von GPT**  
          >    5. **DiskPart > Create Partition EFI size =** *100* (wobei *100* eine Beispiel Partitionsgröße in MB ist, die der ursprünglichen Partition entsprechen sollte)  
          >    6. **DiskPart > Create Partition MSR size =** *128* (wobei *128* ein Beispiel für eine Partitionsgröße in MB ist, die der ursprünglichen Partition entsprechen sollte)  
          >    7. **DISKPART > beenden**  
  
       2. *(Optional)* Wählen Sie die Option **Keinen Laufwerkbuchstaben oder -pfad zuweisen** aus.  
  
       3. Wählen Sie für das Volume das Format **NTFS** aus.  
  
       4. Klicken Sie nach Abschluss der Formatierung mit der rechten Maustaste auf das neue Systemvolume, und klicken Sie dann auf **Partition als aktiv markieren**.  
  
       5. Wenn Sie weitere Volumes benötigen, die anderen Volumes in der Sicherung entsprechen, wiederholen Sie die Schritte *ii* bis *iv*, um die Volumes zu erstellen und zu aktivieren, und schließen Sie dann **die Datenträgerverwaltung**.  
  
       6. Ordnen Sie auf der Seite **Wiederherzustellende Volumes auswählen** das vom System reservierte Volume der Sicherungsquelle dem Volume mit derselben Größe zu, das Sie in Schritt *v* erstellt haben.  
  
       7. Ordnen Sie alle anderen Quellvolumes den entsprechenden Zielvolumes zu.  
  
       8. Klicken Sie auf **Weiter**, um die Wiederherstellung fortzusetzen.  
  
16. Überprüfen Sie die Zuordnung auf der Seite **Wiederherzustellende Volumes bestätigen**, und klicken Sie dann auf **Weiter**. Klicken Sie auf **Zurück**, und wiederholen Sie Schritt 14, wenn Sie Änderungen vornehmen müssen.  
  
17. Auf der Seite **Wiederherstellen von < Computername\> von < Datum und Uhrzeit der Sicherung\>** Seite wird der Fortschritt des Wiederherstellungs Vorgangs angezeigt.  
  
18. Entfernen Sie auf der Seite **Die Wiederherstellung wurde erfolgreich beendet** das Wiederherstellungsmedium, und klicken Sie dann auf **Fertig stellen**. Der Computer wird neu gestartet.  
  
    > [!IMPORTANT]
    >  Wenn vor der Wiederherstellung auf dem Computer BitLocker-Laufwerkverschlüsselung aktiviert war, müssen Sie BitLocker nach dem Neustart des Computers manuell aktivieren.  
  
##  <a name="where-can-i-find-the-drivers-for-my-hardware"></a><a name="BKMK_FindDrivers"></a>Wo finde ich die Treiber für die Hardware?  
 Je nach der Hardware des neuen bzw. wiederhergestellten Computers enthält das Wiederherstellungsmedium möglicherweise nicht alle Treiber für die Speicher- und Netzwerkadapter, die erforderlich sind, wenn Sie den wiederhergestellten Computer neu starten. Sie müssen bestimmen, welche Treiber fehlen, diese Treiber auf vorhandenen Medien oder auf der Website des Herstellers suchen, Sie auf einen Speicherstick kopieren und dann vom Flash Laufwerk auf den neuen oder wiederhergestellten Computer kopieren, wenn Sie den Assistenten für die vollständige System Wiederherstellung ausführen.  
  
 Wenn ein Computer gesichert wird, werden die Treiber für den Computer in der Sicherung gespeichert. Wenn das Wiederherstellungsmedium nicht alle benötigten Treiber enthält, können Sie eine Sicherung für den Computer öffnen und die Treiber dann auf einen USB-Speicherstick kopieren.  
  
#### <a name="to-copy-drivers-from-a-backup-to-a-usb-flash-drive"></a>So kopieren Sie Treiber aus einer Sicherung auf einen USB-Speicherstick  
  
1. Öffnen Sie auf einem anderen Computer das Dashboard.  
  
2. Klicken Sie auf **Geräte**, und klicken Sie dann auf den Computer, für den Treiber erforderlich sind.  
  
3. Klicken Sie auf **Dateien oder Ordner für den Computer wiederherstellen**. Der Assistent zum Wiederherstellen von Dateien oder Ordnern wird geöffnet.  
  
4. Klicken Sie auf die letzte erfolgreiche Datensicherung, und klicken Sie anschließend auf **Weiter**.  
  
5. Klicken Sie auf ein Volume, um es zu öffnen, und klicken Sie anschließend auf **Weiter**. Daraufhin wird ein Fenster mit den Dateien und Ordnern in der Sicherung geöffnet.  
  
6. Verbinden Sie den USB-Speicherstick mit einem USB-Anschluss des Computers, und kopieren Sie dann den Ordner "Treiber für die vollständige Systemwiederherstellung" auf den USB-Speicherstick.  
  
   > [!NOTE]
   >  Möglicherweise müssen Sie auf **Eine Ebene nach oben** klicken, bis Sie zum Stamm des Systemvolumes gelangen.  
  
7. Entfernen Sie den Speicherstick, und verbinden Sie ihn dann mit dem Computer, der wiederhergestellt wird.  
  
   Sie können den USB-Speicherstick verwenden, um die Treiber für den Computer zu installieren, wenn Sie diesen wiederherstellen. Der Assistent für die Wiederherstellung von Dateien oder Ordnern sucht nach weiteren Treibern auf diesem USB-Speicherstick, während der Assistent für die vollständige Systemwiederherstellung ausgeführt wird. Sie werden auf jeden Fall den Treiber für den Netzwerkadapter und die Treiber für die Speichergeräte benötigen.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten von Sicherungen und Wiederherstellungen](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
