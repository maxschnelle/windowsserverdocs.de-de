---
title: Wiederherstellen eines vollständigen Systems aus einer vorhandenen Clientcomputersicherung
description: Beschreibt, wie Windows Server Essentials
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
ms.openlocfilehash: c78a2a2d950c8542bcf56005eb340ec78619acdb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433092"
---
# <a name="restore-a-full-system-from-an-existing-client-computer-backup"></a>Wiederherstellen eines vollständigen Systems aus einer vorhandenen Clientcomputersicherung

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials 
  
 Hardware- und Betriebssystemfehler sind zwar selten, können aber durchaus auftreten. Ein fehlerhafter Lüfter könnte zu einer Überhitzung der Hauptplatine des Computers führen, sodass diese nicht mehr verwendet werden kann. Das Betriebssystem könnte beschädigt werden, sodass es nicht mehr gestartet werden kann. Durch Feuer und Wasser kann die Hardware dauerhaft beschädigt werden. Bei einem Festplattenlaufwerk kann ein Fehler auftreten, oder Sie entscheiden, es gegen ein größeres Festplattenlaufwerk auszutauschen.  
  
 Dieses Dokument enthält Informationen zu den folgenden Themen:  
  
-   [Was ist die vollständige Systemwiederherstellung?](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_WhatIs)  
  
-   [Wie funktioniert die Umgebung für die Systemwiederherstellung?](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_HowDoes)  
  
-   [Erstellen Sie einen startbaren USB-Speicherstick, die Wiederherstellung eines Clientcomputers](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_CreateBootable)  
  
-   [Verwenden den vollständigen Systems Wiederherstellungs-Assistenten](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_Using)  
  
-   [Wo finde ich die Treiber für die Hardware?](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_FindDrivers)  
  
##  <a name="BKMK_WhatIs"></a> Was ist die vollständige Systemwiederherstellung?  
 Wenn Sie ein Festplattenlaufwerk austauschen oder auf dem Computer ein Fehler auftritt, der dazu führt, dass der Computer nicht mehr verwendet oder gestartet werden kann, können Sie das System aus einer früheren Sicherung des Computers wiederherstellen. Bei einer vollständigen Systemwiederherstellung wird das System wieder in den Zustand versetzt, in dem es sich zum Zeitpunkt der Sicherung befand.  
  
> [!IMPORTANT]
>  Bei Computerhardware, z. B. einer Systemplatine, die nicht der ausgetauschten Computerhardware entspricht, ist es nicht möglich, eine vollständige Systemwiederherstellung auszuführen. Ein installiertes Betriebssystem hängt stark von der zugrunde liegenden Hardware des Computers ab. Auf einer Festplatte, die mindestens genauso groß ist wie die ausgetauschte Festplatte, kann hingegen eine vollständige Systemwiederherstellung ausgeführt werden.  
  
 Bei einer vollständigen Systemwiederherstellung haben Sie die Möglichkeit, eine bestimmte Computersicherung auszuwählen, um das System mit allen dem Benutzer vor Auftreten des Fehlers, einer Katastrophe oder dem Diebstahl vertrauten Anwendungen, Konfigurationen und Einstellungen wiederherzustellen. Außerdem können Sie die Volumes auswählen, die Sie wiederherstellen möchten.  
  
 Beachten Sie beim Planen und Vorbereiten der vollständigen Systemwiederherstellung auf einem Netzwerkcomputer Folgendes:  
  
### <a name="windows-preinstallation-environment"></a>Windows Preinstallation Environment  
 Windows Preinstallation Environment (Windows PE) ist ein minimales Betriebssystem, das zum Vorbereiten eines Computers für die Installation von Windows vorgesehen ist. Für Server mit Windows Server Essentials wird Windows PE automatisch installiert, wenn Sie das Medium für die Systemwiederherstellung auf einem Computer wiederhergestellt werden einfügen. Für Server mit Windows Server Essentials wird Windows PE automatisch installiert, wenn Sie den Computer mit dem clientwiederherstellungsdienst oder USB-Speicherstick starten.  
  
 Windows PE unterstützt keine Funkverbindungen. Daher muss der wiederherzustellende Computer physisch mit dem kleinen Firmennetzwerk verbunden sein.  
  
### <a name="bitlocker"></a>BitLocker  
 BitLocker-Laufwerkverschlüsselung (BitLocker) ist eine Datenschutzfunktion, die in einigen Versionen von Windows Vista, Windows 7 und Windows 8 verfügbar ist. BitLocker bietet Schutz vor Datendiebstahl oder der Offenlegung von Daten auf Computern, die verloren gehen oder gestohlen werden, und ermöglicht die sichere Löschung von Daten, wenn Computer außer Betrieb gesetzt werden.  
  
 **Für Windows Server Essentials:** Wenn der Computer, der wiederhergestellt werden soll, mit BitLocker verschlüsselt war (unabhängig davon, ob nur das Betriebssystemlaufwerk oder zusätzlich auch eine oder mehrere weitere Festplattenlaufwerke verschlüsselt waren), können Sie trotzdem das Medium für die vollständige Systemwiederherstellung auf der mit dem Server gelieferten CD und den Assistenten für die vollständige Systemwiederherstellung verwenden, um das Festplattenabbild einschließlich des Betriebssystems aus einer Sicherung neu zu installieren und die Daten auf dem neuen oder reparierten Computer wiederherzustellen.  
  
 **Für Windows Server Essentials:** Wenn der Computer, der wiederhergestellt werden soll, mit BitLocker verschlüsselt war (unabhängig davon, ob nur das Betriebssystemlaufwerk oder zusätzlich auch eine oder mehrere weitere Festplattenlaufwerke verschlüsselt waren), können Sie trotzdem den Assistenten für die vollständige Systemwiederherstellung verwenden, um das Festplattenabbild einschließlich des Betriebssystems aus einer Sicherung neu zu installieren und die Daten auf dem neuen oder reparierten Computer wiederherzustellen.  
  
 Wenn vom Server Laufwerke, Ordner und Dateien gesichert werden, wird auf dem Server eine unverschlüsselte Version gespeichert. Diese unverschlüsselte Version wird während der vollständigen Systemwiederherstellung auf den Computer kopiert.  
  
> [!NOTE]
>  Nach einer erfolgreichen vollständigen Systemwiederherstellung müssen Sie BitLocker auf dem Computer erneut aktivieren.  
>   
>  Anweisungen zum Aktivieren von BitLocker auf Computern, auf denen Windows 8 ausgeführt werden, finden Sie unter [BitLocker: Aktivieren von BitLocker](https://go.microsoft.com/fwlink/p/?LinkID=254918).  
>   
>  Anweisungen zum Aktivieren von BitLocker auf Computern, auf denen Windows 7 ausgeführt werden, finden Sie unter [BitLocker-Laufwerkverschlüsselung schrittweise Anleitung für Windows 7](https://go.microsoft.com/fwlink/p/?LinkId=140225).  
  
 Weitere grundlegende Informationen zur BitLocker-Laufwerkverschlüsselung finden Sie unter [BitLocker: Häufig gestellte Fragen (FAQ)](https://go.microsoft.com/fwlink/p/?LinkID=254917).  
  
### <a name="encrypting-file-system-encrypted-files"></a>EFS-verschlüsselte Dateien  
 Das Feature EFS (Encrypting File System, verschlüsselndes Dateisystem) unter Windows ermöglicht eine zusätzliche benutzerbasierte Verschlüsselung auf Dateiebene, sodass unterschiedliche Sicherheitsstufen implementiert werden können, wenn mehrere Benutzer denselben Computer verwenden. Es ist wichtig zu wissen, dass EFS-verschlüsselte Ordner und Dateien im Gegensatz zu BitLocker-verschlüsselten Laufwerken in einer Computersicherung weiterhin verschlüsselt sind. Microsoft ist EFS nicht verfügbar in Windows XP Home Edition, Windows Vista Starter, Windows Vista Home Basic, Windows Vista Home Premium, Windows 7 Starter, Windows 7 Home Basic, Windows 7 Home Premium oder Windows 8. Es ist nur in Windows 8 Pro verfügbar.  
  
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
  
##  <a name="BKMK_HowDoes"></a> Wie funktioniert die Umgebung für die Systemwiederherstellung?  
 Mit Windows-ServerÂ® 2012 Essentials bereitgestellten Medium für die Systemwiederherstellung wird Windows Preinstallation Environment (Windows PE) auf dem Computer installiert. Windows PE hat die MS-DOS-Umgebung abgelöst und enthält die wichtigen Programmdateien für Windows. In Windows Server Essentials, es gibt zwei unterstützte Methoden zum Wiederherstellen eines Systems: mit dem clientwiederherstellungsdienst, der ein Netzwerk verwendet und beruht nicht auf Medien, oder über einen USB-Flashlaufwerk.  
  
> [!NOTE]
>  Windows PE unterstützt keine Funkverbindungen. Daher muss der wiederherzustellende Computer physisch mit dem kleinen Firmennetzwerk verbunden sein.  
  
 Die Umgebung für die Systemwiederherstellung enthält die Programmdateien für 32-Bit (x86) und 64-Bit (x64). Wählen Sie nach dem Einlegen des Mediums für die Systemwiederherstellung die passende Version der Dateien aus. Die Standardversion ist 32-Bit (x86). Diese wird automatisch ausgewählt, wenn Sie nicht innerhalb von 30 Sekunden eine Auswahl treffen. Wenn auf dem Server aktualisierte Programmdateien für die vollständige Systemwiederherstellung vorhanden sind, werden diese aktualisierten Dateien automatisch auf den Computer heruntergeladen.  
  
 Nachdem Windows Preinstallation Environment eingerichtet wurde, wird der Assistent für die vollständige Systemwiederherstellung gestartet. Dieser Assistent hilft Ihnen bei der Wiederherstellung des Computers aus einer früheren Sicherung. Sie können die Umgebung für die Systemwiederherstellung auch verwenden, um eine Sicherung auf einem neuen Computer mit vergleichbarer Hardware wiederherzustellen.  
  
 In den meisten Fällen reichen die in der Umgebung für die Systemwiederherstellung enthaltenen Programmdateien und Treiber aus, um den neuen oder wiederhergestellten Computer neu zu starten. Je nach der Hardware des neuen bzw. wiederhergestellten Computers enthält die Umgebung für die Systemwiederherstellung möglicherweise nicht alle Treiber für die Speicher- und Netzwerkadapter, die erforderlich sind, wenn Sie den neuen oder wiederhergestellten Computer neu starten. Der Assistent für die vollständige Systemwiederherstellung bietet Ihnen bei Bedarf die Gelegenheit zum Installieren von Treibern. Informationen dazu, wie Sie die Treiber für Ihre Hardware finden können, finden Sie unter [Wo finde ich die Treiber für die Hardware?](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_FindDrivers). Informationen zur Verwendung des Mediums für die Systemwiederherstellung finden Sie unter [Verwenden des Assistenten für die vollständige Systemwiederherstellung](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_Using).  
  
##  <a name="BKMK_CreateBootable"></a> Erstellen Sie einen startbaren USB-Speicherstick, die Wiederherstellung eines Clientcomputers  
 Wenn Sie wiederherstellen müssen ein Clientcomputer aus einer vorhandenen Sicherung jedoch wurde nicht gefunden, die mit dem Server (in Windows Server Essentials) gelieferte Wiederherstellungs-CD oder Sie nicht den clientwiederherstellungsdienst auf dem Server (in Windows Server Essentials) einrichten möchten , Sie können einen startbaren USB-Speicherstick erstellen. Sie können den USB-Speicherstick dann verwenden, um den Clientcomputer zu starten und das System wiederherzustellen. Der verwendetet USB-Speicherstick muss über mindestens 1 GB verfügen.  
  
#### <a name="to-create-a-bootable-usb-flash-drive"></a>So erstellen Sie einen startfähigen USB-Speicherstick  
  
1.  Öffnen Sie das **Dashboard**.  
  
2.  Klicken Sie auf die Registerkarte **Geräte**.  
  
3.  Klicken Sie im Bereich **Aufgaben** auf **Einstellungen für Computersicherung und Dateiversionsverlauf anpassen**.  
  
    > [!NOTE]
    >  Klicken Sie in Windows Server Essentials auf **Clientcomputer-Sicherungsaufgaben**.  
  
4.  Klicken Sie auf die Registerkarte **Extras** und anschließend im Abschnitt **Computerwiederherstellung** auf **Schlüssel erstellen**. Der Assistent "Computerwiederherstellungsschlüssel erstellen" wird geöffnet.  
  
5.  Stecken Sie einen USB-Speicherstick mit 1 GB in den Server ein, und folgen Sie anschließend den Anweisungen des Assistenten.  
  
    > [!CAUTION]
    >  Alle Daten auf dem USB-Speicherstick werden gelöscht.  
  
##  <a name="BKMK_Using"></a> Verwenden den vollständigen Systems Wiederherstellungs-Assistenten  
 Nachdem Sie den Computer mit dem Wiederherstellungsmedium, Clientwiederherstellungsdienst oder USB-Speicherstick erfolgreich gestartet und überprüft haben, ob alle Hardwaretreiber auf dem wiederhergestellten oder neuen Clientcomputer geladen wurden, wird der Assistent für die vollständige Systemwiederherstellung angezeigt. Mithilfe dieses Assistenten können Sie auf den Server, die Computersicherung und die Quellvolumes zugreifen, die Sie auf dem Computer wiederherstellen möchten. Außerdem wird der Wiederherstellungsvorgang ausgeführt.  
  
> [!NOTE]
>   Windows Server Essentials unterstützt die folgenden Wiederherstellungsszenarien nicht:  
> 
> - Wiederherstellen eines Datenträgers Master Boot Record (MBR) zu einem Unified Extensible Firmware Interface-UEFI-basierten Computer.  
>   -   Wiederherstellen einer UEFI-/GPT-Sicherung in einem BIOS-System  
> 
>   Wenn Sie Daten in einem dieser Szenarien wiederherstellen, können Sie das System nicht starten. Außerdem können Sie möglicherweise keine Festplatten verwenden, die größer als zwei Terabyte sind.  
  
 **Voraussetzungen:**  
  
-   Binden Sie vor dem Starten der vollständigen Systemwiederherstellung den Computer mithilfe eines Netzwerkkabels in das Netzwerk ein, in dem sich der Server befindet. Stellen Sie sicher, dass Sie Zugriff auf alle Festplatten des Clientcomputers haben.  
  
    > [!WARNING]
    >  Versuchen Sie nicht, eine vollständige Systemwiederherstellung auf einem Computer auszuführen, der über eine Funkverbindung in das Netzwerk eingebunden ist.  
  
-   Wenn Sie wissen, dass auf dem Computer wichtige Treiber für das Netzwerk oder für Speichergeräte fehlen, müssen Sie diese Treiber suchen und auf einen Speicherstick kopieren, bevor Sie die vollständige Systemwiederherstellung starten. Für Windows Server Essentials: Wenn Sie das auf CD bereitgestellte Medium für die vollständige Systemwiederherstellung verwenden, muss die CD während des Starts der vollständigen Systemwiederherstellung im Laufwerk bleiben. Kopieren Sie daher die fehlenden Treiber nicht auf eine CD oder DVD, es sei denn, Sie verfügen über ein zweites CD-/DVD-Laufwerk. Kopieren Sie die fehlenden Treiber stattdessen auf einen USB-Speicherstick.  
  
     Informationen dazu, wie Sie die Treiber für Ihren Computer finden können, finden Sie unter [Wo finde ich die Treiber für die Hardware?](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_FindDrivers)  
  
-   Für Windows Server Essentials: Wenn Sie die Windows Server Essentials-Wiederherstellungs-CD nicht finden, können Sie einen startbaren USB-Speicherstick erstellen. Weitere Informationen finden Sie unter [Create a bootable USB flash drive to restore a client computer](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_CreateBootable).  
  
#### <a name="to-use-the-full-system-restore-wizard"></a>So verwenden Sie den Assistenten für die vollständige Systemwiederherstellung  
  
1. Führen Sie eines der folgenden Verfahren aus:  
  
   -   Windows Server Essentials: Schalten Sie den wiederherzustellenden Clientcomputer ein, legen Sie das Wiederherstellungsmedium ein, und schalten Sie den Computer wieder aus.  
  
        Schalten Sie den Computer erneut ein, und drücken Sie während des Selbsttests (POST) die entsprechende Funktionstaste (F-Taste), um das Startgerätemenü aufzurufen. Wählen Sie dann das CD-/DVD-Laufwerk aus. Der Windows-Start-Manager wird gestartet.  
  
   -   Windows Server Essentials: Wenn Sie den Clientwiederherstellungsdienst verwenden, starten Sie den Computer mit der Option **Boot from network** neu. Andernfalls starten Sie den Computer mithilfe des USB-Sticks.  
  
        Schalten Sie den Computer erneut ein, und drücken Sie während des Selbsttests (Power On Self Test, POST), die entsprechende Funktionstaste (F-Taste), um das Gerätestartmenü aufzurufen, und wählen Sie **Boot from network** (oder die Möglichkeit, über den USB-Stick zu starten). Der Windows-Start-Manager wird gestartet.  
  
   > [!NOTE]
   >  Lesen Sie in der Dokumentation des Computerherstellers nach, welche Funktionstaste Sie drücken müssen, um das Startgerätemenü aufzurufen.  
  
2. Das Wiederherstellungsmedium für den Computer enthält die Startoptionen für 32-Bit (x86) und 64-Bit (x64). Wählen Sie im Windows-Start-Manager die Option **Vollständige Systemwiederherstellung (x86)** oder **Vollständige Systemwiederherstellung (x64)** aus. Wenn die Treiber für die Computerhardware in 32-Bit vorliegen, wählen Sie x86 aus. Liegen sie in 64-Bit vor, wählen Sie x64 aus. Die Windows-Dateien werden geladen, und der Assistent für die vollständige Systemwiederherstellung prüft, ob alle Hardwaretreiber verfügbar sind.  
  
3. Wählen Sie im Fenster **Assistent für die vollständige Systemwiederherstellung** die gewünschte Sprache aus, und klicken Sie dann auf den Pfeil.  
  
4. Wählen Sie für den Computer die gewünschten Optionen für **Zeit- und Währungsformat** und **Tastatur oder Eingabemethode** aus. Klicken Sie auf **Weiter**.  
  
5. Wenn Treiber fehlen, wird die Meldung, dass der Wiederherstellungsvorgang wird die Treiber kann nicht überprüft. Klicken Sie auf **Schließen**, und klicken Sie dann im Dialogfeld "Willkommen" auf **Treiber laden**.  
  
   1.  Klicken Sie im Dialogfenster **Hardware ermitteln** auf **Treiber installieren**.  
  
   2.  Verbinden Sie den USB-Speicherstick, der die Hardwaretreiber enthält, mit dem Computer, und klicken Sie dann im Dialogfeld **Treiber installieren** auf **Suchen**.  
  
   3.  Wenn die Treiber gefunden wurden, klicken Sie im Dialogfeld **Treiber installieren** auf **OK**.  
  
   4.  Klicken Sie im Dialogfeld **Hardware ermitteln** auf **Weiter**.  
  
6. Wenn bei der ersten Prüfung alle Treiber gefunden wurden oder alle wichtigen Treiber installiert worden sind, klicken Sie im Dialogfeld **Vollständige Systemwiederherstellung** auf **Weiter**.  
  
7. Klicken Sie auf der Seite **Willkommen** auf **Weiter**.  
  
8. Es wird nach dem Server gesucht.  
  
   1.  Wenn der Server nicht gefunden werden kann, haben Sie die Möglichkeit, erneut zu suchen oder die IP-Adresse des Servers einzugeben.  
  
   2.  Wenn mehrere Server ermittelt wurden, werden Sie aufgefordert, einen auszuwählen.  
  
   3.  Wenn der Server gefunden, wird die **melden Sie sich beim < IhrServername\>**  angezeigt wird.  
  
9. Auf der **melden Sie sich beim < IhrServername\>**  geben *< AdministratorKontoName\>*  in die **Benutzernamen** Textfeld und die Kennwort für das Administratorkonto in der **Kennwort** Textfeld, und klicken Sie dann auf **Weiter**.  
  
    > [!IMPORTANT]
    >  Sie müssen ein Administratorkonto verwenden, das in englischer Sprache erstellt wird. Wenn Sie nicht bereits über eines verfügen, müssen Sie ein neues Administratorkonto erstellen. Öffnen Sie dazu zuerst die Registerkarte **Benutzer** auf dem Serverdashboard, legen Sie dann die Tastatursprache auf Englisch fest, und führen Sie die Aufgabe **Benutzerkonto hinzufügen** aus, um das Administratorkonto zu erstellen. Verwenden Sie anschließend das neue Administratorkonto, um mit der Wiederherstellung des Clientcomputers fortzufahren.  
  
10. Wählen Sie auf der Seite **Wiederherzustellenden Computer auswählen** den Computer aus, den Sie wiederherstellen möchten, und klicken Sie auf **Weiter**. Wählen Sie entweder **< ComputerName\>: (Dieser Computer)**  , oder wählen Sie einen anderen Computer im Netzwerk die **einem anderen Computer** Dropdown-Liste.  
  
    > [!NOTE]
    >  Wenn es sich um einen Computer handelt, der dem Server nicht bekannt ist (z. B. einen neuen oder einem neuen Zweck zugeführten Computer), wird die Option **Dieser Computer** nicht angezeigt.  
  
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
          >  Wenn ein Clientcomputer Unified Extensible Firmware Interface-UEFI-basiert ist, müssen Sie verwenden die **Diskpart** Tool, um den Systemdatenträger initialisieren. Öffnen Sie dazu ein Befehlsfenster (drücken Sie unter Windows PE 5 Sekunden lang STRG+ALT+UMSCHALT), führen Sie **diskpart.exe** aus, und führen Sie dann die folgenden diskpart-Befehle aus:  
          > 
          > 1. **DISKPART> list disk**  
          >    2. **DISKPART> select disk #** *<Datenträger\>*  
          >    3. **DISKPART> clean**  
          >    4. **DISKPART> convert gpt**  
          >    5. **DISKPART> create partition efi size=** *100* (wobei *100* ist eine Beispiel-Partitionsgröße in MB, muss identisch mit der ursprünglichen Partition)  
          >    6. **DISKPART> create partition msr size=** *128* (wobei *128* ist eine Beispiel-Partitionsgröße in MB, muss identisch mit der ursprünglichen Partition)  
          >    7. **DISKPART> exit**  
  
       2. *(Optional)* Wählen Sie die Option **Keinen Laufwerkbuchstaben oder -pfad zuweisen** aus.  
  
       3. Wählen Sie für das Volume das Format **NTFS**aus.  
  
       4. Klicken Sie nach Abschluss der Formatierung mit der rechten Maustaste auf das neue Systemvolume, und klicken Sie dann auf **Partition als aktiv markieren**.  
  
       5. Wenn Sie weitere Volumes benötigen, die anderen Volumes in der Sicherung entsprechen, wiederholen Sie die Schritte *ii* bis *iv* , um die Volumes zu erstellen und zu aktivieren, und schließen Sie dann **die Datenträgerverwaltung**.  
  
       6. Ordnen Sie auf der Seite **Wiederherzustellende Volumes auswählen** das vom System reservierte Volume der Sicherungsquelle dem Volume mit derselben Größe zu, das Sie in Schritt *v* erstellt haben.  
  
       7. Ordnen Sie alle anderen Quellvolumes den entsprechenden Zielvolumes zu.  
  
       8. Klicken Sie auf **Weiter**, um die Wiederherstellung fortzusetzen.  
  
16. Überprüfen Sie die Zuordnung auf der Seite **Wiederherzustellende Volumes bestätigen** , und klicken Sie dann auf **Weiter**. Klicken Sie auf **Zurück**, und wiederholen Sie Schritt 14, wenn Sie Änderungen vornehmen müssen.  
  
17. Die **Restoring < ComputerName\> von < Datum und Uhrzeit der Sicherung\>**  Seite meldet den Fortschritt des Wiederherstellungsvorgangs.  
  
18. Entfernen Sie auf der Seite **Die Wiederherstellung wurde erfolgreich beendet** das Wiederherstellungsmedium, und klicken Sie dann auf **Fertig stellen**. Der Computer wird neu gestartet.  
  
    > [!IMPORTANT]
    >  Wenn vor der Wiederherstellung auf dem Computer BitLocker-Laufwerkverschlüsselung aktiviert war, müssen Sie BitLocker nach dem Neustart des Computers manuell aktivieren.  
  
##  <a name="BKMK_FindDrivers"></a> Wo finde ich die Treiber für die Hardware?  
 Je nach der Hardware des neuen bzw. wiederhergestellten Computers enthält das Wiederherstellungsmedium möglicherweise nicht alle Treiber für die Speicher- und Netzwerkadapter, die erforderlich sind, wenn Sie den wiederhergestellten Computer neu starten. Sie müssen bestimmen, welche Treiber fehlen, suchen Sie nach auf vorhandene Medien oder auf der Website des Herstellers, kopieren Sie sie auf einen Speicherstick, und klicken Sie dann kopieren Sie sie aus der Speicherstick mit dem neuen oder wiederhergestellten Computer aus, wenn Sie den Assistenten für vollständige Systemwiederherstellung ausführen.  
  
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
  
-   [Verwalten der Sicherung und Wiederherstellung](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
