---
title: Erstellen einer Serverwiederherstellungs-DVD für remote verwaltete Server
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6141fa69-5952-4e3c-a868-40ef3f4badd2
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 7bfe1686ac84962cdb4ab1cde8d6ca5226cb9d44
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844351"
---
# <a name="create-a-server-recovery-dvd-for-remotely-administered-servers"></a>Erstellen einer Serverwiederherstellungs-DVD für remote verwaltete Server

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_HeadlessRecovery"></a> Erstellen einer serverwiederherstellungs-DVD für Remote verwaltete Server  
 Es gibt zwei Modelle für die Wiederherstellung der Herstellerstandards und die Serverwiederherstellung. Sie sind von der Hardware abhängig, die der Kunde erhalten hat.  
  
 **Remote verwalteter server**  
  
 Diese Serverwiederherstellungsoption erfordert, dass der Prozess auf einem Clientcomputer im selben Netzwerk ausgeführt wird. Da für die Wiederherstellung der Herstellerstandards ein mit dem Server bereitgestelltes hardwarespezifisches Abbild erforderlich ist, muss der Partner die Serverwiederherstellungs-DVD erstellen.  
  
 **Lokal verwalteter server**  
  
 Dies ist das klassische Modell, bei dem der Server über die Serverkonsole verwaltet wird. Das Serverinstallationsmedium dient zum Ausführen einer Wiederherstellung. Dafür muss der Server über die Möglichkeit zur Anzeige von Videoausgaben und ein DVD-Lesegerät verfügen. Der Kunde startet über dieses Serverinstallationsmedium und wählt dann die geeignete Wiederherstellungsmethode aus. Es ist nicht erforderlich, eine Serverwiederherstellungs-DVD für Server zu erstellen, die lokal verwaltet werden.  
  
> [!NOTE]
>  Beim Modell mit lokal verwaltetem Server kann der Kunde eine Wiederherstellung der Herstellerstandards durch eine Neuinstallation vornehmen. Allerdings gehen dabei die durch den Partner vorgenommenen Anpassungen verloren.  
  
 Es gibt zwei Arten von Serverwiederherstellung.  
  
 **Zurücksetzung auf werkseinstellungen**  
  
 Mit dieser Wiederherstellung wird der Server wieder in den Ursprungszustand versetzt, der bei der Auslieferung vom Werk vorlag. Nach der Wiederherstellung der Herstellerstandards müssen Sie die Erstkonfiguration des Servers wie beim ersten Einschalten des Servers erneut vornehmen. Alle Einstellungen und Anpassungen sind verloren. Dies wird auch als Tag 0 bezeichnet.? Da für die Wiederherstellung der Herstellerstandards ein mit dem Server bereitgestelltes hardwarespezifisches Abbild erforderlich ist, muss der Partner die Serverwiederherstellungs-DVD erstellen.  
  
 **Bare-Metal-Wiederherstellung**  
  
 Diese Wiederherstellung setzt voraus, dass Sie eine Serversicherung konfiguriert haben und dass die Serversicherung beim letzten Mal vor dem Serverausfall erfolgreich abgeschlossen wurde. Die Bare-Metal-Recovery (BMR) unterstützt nur die Wiederherstellung des Systems und der Startlaufwerke aus einer früheren Serversicherung.  
  
 Nach einer BMR wird der Server wieder in den Zustand versetzt, der zum Zeitpunkt der Sicherung bestand, die für die Wiederherstellung verwendet wird. Dies ist in der Regel die aktuelle Sicherung, in einigen Fällen kann es aber auch eine frühere Sicherung sein. Die Datenwiederherstellung erfolgt nach der Systemwiederherstellung mithilfe des Assistenten für die Dateien- und Ordnerwiederherstellung. BMR ist die bevorzugte Serverwiederherstellungsmethode, da alle Einstellungen und Konfigurationen anschließend wieder vorhanden sind. Bei der Wiederherstellung der Herstellerstandards wird der Server jedoch in den Zustand "Tag 0" versetzt.  
  
### <a name="remotely-administered-server-recovery"></a>Remote verwaltete Serverwiederherstellung  
 In diesem Abschnitt werden die erforderlichen Anpassungen durch den Partner und die endgültigen Medien beschrieben, die mit jedem Server ausgeliefert werden müssen. Bevor wir uns mit den Details befassen, sehen wir uns zuerst die Situation beim Kunden an.  
  
 In diesem Szenario wird der Kunde "des s-Server funktioniert nicht mehr. Der Grund kann ein Virus, ein Festplattenfehler oder eine andere Ursache sein. Der Kunde legt die Serverwiederherstellungs-DVD in einen Clientcomputer ein, der sich im selben Netzwerk wie der Server befindet. Mit der Anwendung für die Serverwiederherstellung wird der Kunde durch die drei Schritte zur Wiederherstellung des Servers geführt:  
  
1.  Die Anwendung erstellt einen startfähigen USB-Speicherstick, über den der Server im Wiederherstellungsmodus neu gestartet wird. Der USB-Speicherstick muss mindestens 8 GB groß sein.  
  
2.  Die Anwendung ermittelt den Server, der sich jetzt im Wiederherstellungsmodus befindet.  
  
3.  Die Anwendung lässt den Kunden festlegen, ob die Herstellerstandards wiederherstellt oder eine Bare-Metal-Recovery ausgeführt wird, und versetzt dann den Server wieder in einen betriebsbereiten Zustand.  
  
### <a name="steps-for-creating-a-server-recovery-dvd-for-multiple-language-support"></a>Schritte zum Erstellen einer Serverwiederherstellungs-DVD für die Unterstützung mehrerer Sprachen  
 Zum Erstellen einer Serverwiederherstellungs-DVD sind sechs Hauptschritte auszuführen:  
  
1.  [(Optional) Aktualisieren von WinPE](Create-a-Server-Recovery-DVD-for-Remotely-Administered-Servers.md#BKMK_Updating)  
  
2.  [Sammelt die Wiederherstellung der Herstellerstandards Abbildern und XML-Dateien](Create-a-Server-Recovery-DVD-for-Remotely-Administered-Servers.md#BKMK_Collecting)  
  
3.  [Erstellen der serverwiederherstellungs-DVD](Create-a-Server-Recovery-DVD-for-Remotely-Administered-Servers.md#BKMK_Creating)  
  
4.  [Anpassen des Assistenten](Create-a-Server-Recovery-DVD-for-Remotely-Administered-Servers.md#BKMK_Customizing)  
  
5.  [Erstellen Sie die ISO-Datei](Create-a-Server-Recovery-DVD-for-Remotely-Administered-Servers.md#BKMK_CreatingISO)  
  
6.  [Testen der Wiederherstellungs-DVD](Create-a-Server-Recovery-DVD-for-Remotely-Administered-Servers.md#BKMK_Testing)  
  
####  <a name="BKMK_Updating"></a> Schritt 1: (Optional) Aktualisieren von WinPE  
 Das ADK umfasst eine angepasste Kopie von Windows PE. Beim Starten des Abbilds wird automatisch das Signal gestartet, mit dem die Anwendung für die Clientwiederherstellung eine Verbindung mit einem Server im Wiederherstellungsmodus herstellt.  
  
 Windows PE muss weiter angepasst werden, indem hardwarespezifische Treiber wie Treiber für das Netzwerk oder für Festplattencontroller hinzugefügt werden. Nach dem Start über WinPE müssen die Festplatten im System erkannt werden können, und das Netzwerk muss funktionieren.  
  
####  <a name="BKMK_Collecting"></a> Schritt 2: Erfassen von Abbildern und XML-Dateien für die Wiederherstellung der Herstellerstandards  
 Die folgenden beiden Abbilder müssen aufgezeichnet werden, um einen Server auf die Herstellerstandards zurückzusetzen:  
  
-   Das Abbild des Systemlaufwerks  
  
-   Die für das System reservierte Partition  
  
 Zur Aufzeichnung dieser Abbilder wird das Tool "GenDiskXML.exe" bereitgestellt. Mit "GenDiskXML.exe" wird auch die Datei "disk.xml" erfasst, mit der während der Wiederherstellung die Datenträgerkonfiguration neu erstellt wird.  
  
1.  Starten Sie nach Sysprep das System mit einer 64-Bit-Version von Windows PE neu.  
  
2.  Führen Sie `GenDiskXML /outputdir:<path>` aus, um die XML- und WIM-Dateien in eine externe Quelle auszugeben. Die Dateien werden der DVD im nächsten Schritt hinzugefügt.  
  
    > [!NOTE]
    >  Die WIM-Datei des Systems wird geteilt, damit die FAT32-Anforderung, dass Dateien höchstens 4 GB aufweisen dürfen, erfüllt wird. Dabei muss die erforderliche Kapazität des Ziels, mit dem die WIM-Dateien aufgezeichnet werden, mehr als 8 GB betragen, damit die Teilung vorgenommen werden kann.  
  
####  <a name="BKMK_Creating"></a> Schritt 3: Erstellen der Serverwiederherstellungs-DVD  
 Zu jedem vom Hersteller ausgelieferten Server muss eine Serverwiederherstellungs-DVD gehören. Auf Ihrer DVD mit den ADK-Tools finden Sie die für die Erstellung der DVD erforderlichen Dateien.  
  
###### <a name="to-create-the-server-recovery-dvd"></a>So erstellen Sie die Serverwiederherstellungs-DVD  
  
1.  Erstellen Sie einen Arbeitsordner, in dem die endgültige ISO gespeichert wird.  
  
2.  Kopieren Sie den Inhalt des Ordners **Server Recovery** von der Partner-CD in den in Schritt 1 erstellten Arbeitsordner.  
  
3.  Kopieren Sie die Datei "disk.xml", die bei der Ausführung von "GenDiskXML.exe" erstellt wurde, in den Ordner **Reset**.  
  
4.  Kopieren Sie die Abbilddatei, die bei der Ausführung von **GenDiskXML.exe** erstellt wurde, in den Ordner **Reset**. Bei den Dateien handelt es sich um WIM- und SWM-Dateien. Deren Anzahl kann variieren.  
  
5.  Entfernen Sie "GenDiskXML.exe" aus dem Ordner. Diese Datei ist nur für werkseitige Arbeiten vorgesehen und sollte nicht auf der DVD enthalten sein, die an den Kunden geliefert wird.  
  
####  <a name="BKMK_Customizing"></a> Schritt 4: Anpassen des Assistenten  
 Die Anwendung für die Serverwiederherstellung muss mit einem Abbild des Geräts sowie mit einer Beschreibung für den Start des speziellen Geräts im Wiederherstellungsmodus angepasst werden. Da diese Seite des Assistenten für die Dateien- und Ordnerwiederherstellung hardwarespezifisch ist, variieren die Schritte für den Start des Servers im Wiederherstellungsmodus.  
  
> [!NOTE]
>  Die aufgeführten Dateinamen müssen genau übereinstimmen.  
  
1.  Auf der Seite des Assistenten ist ein Link für zusätzliche Hilfe angegeben. Wenn diese CHM-Datei vorhanden ist, wird der FWLink für die Webhilfe überschrieben. Die Hilfedatei befindet sich unter:  
  
     < DVD-Stamm\>\\$OEM$ \Customization\\< Kulturname\>\RestartHelp.chm  
  
2.  Diese Datei enthält den Text, der dem Kunden auf der Seite des Assistenten angezeigt wird. Der Text sollte erklären, wie der Server im Wiederherstellungsmodus gestartet wird. Für das Steuerelement sind Bildläufe möglich. Beim Umfang des hinzugefügten Texts bestehen also praktische Grenzen.  
  
     Mit dieser Datei wird das Beispielbild im Assistenten ersetzt, sie dient vorwiegend dem Branding. Es muss eine PNG-Datei sein. Die Dateigröße muss 256 Pixel x 256 Pixel betragen, andernfalls wird das Bild bei der Anzeige im Assistenten abgeschnitten.  
  
     < DVD-Stamm\>\\$OEM$ \Customization\\< Kulturname\>\RestartInstructions.rtf  
  
3.  < DVD-Stamm\>\\$OEM$ \Customization\\< Kulturname\>\ServerImage.png  
  
 Beachten Sie unbedingt Folgendes, wenn Sie Ihre Serverwiederherstellungs-DVD für die Unterstützung mehrerer Sprachen konvertieren:  
  
1.  Der Ordner "en-us" muss immer vorhanden sein. Wenn die Anwendung für die Serverwiederherstellung die kulturspezifischen Dateien, die zu dem Clientcomputer passen, auf dem sie ausgeführt wird, nicht findet, wird "en-us" verwendet.  
  
2.  Fügen Sie in jedem Kulturordner, den Sie erstellen, die drei Anpassungsdateien (PNG, CHM und RTF) hinzu.  
  
3.  Kopieren Sie beide Kulturordner aus Language Packs\\< CultureName\>\Server Recovery auf den Stamm der serverwiederherstellungs-DVD. Zum Beispiel: Die Ordner ES und ES-ES würden beide in das Stammverzeichnis der DVD zur Unterstützung der spanischen Sprache kopiert.  
  
4.  Schließen Sie die ISO-Datei ab.  
  
 Unterstützte Kulturnamen:  

|-|-|  
|- cs-CZ<br /><br /> - de-DE<br /><br /> -En-US<br /><br /> - es-ES<br /><br /> - fr-FR<br /><br /> - hu-HU<br /><br /> -It-IT<br /><br /> - ja-JP<br /><br /> - ko-KR<br /><br /> -nl-NL |-pl-PL<br /><br /> - pt-BR<br /><br /> - pt-PT<br /><br /> - ru-RU<br /><br /> - sv-SE<br /><br /> - tr-TR<br /><br /> - zh-CN<br /><br /> - zh-HK<br /><br /> - zh-TW
  
####  <a name="BKMK_CreatingISO"></a> Schritt 5: Erstellen der ISO-Datei  
 Der Ordner, der erstellt wurde, kann mit seinem kompletten Inhalt auf eine DVD gebrannt werden. Dies ist die DVD, die Kunden zusammen mit einem neuen Server bereitgestellt wird.  
  
####  <a name="BKMK_Testing"></a> Schritt 6: Testen der Wiederherstellungs-DVD  
 Wenn die Serverinstallation abgeschlossen ist, konfigurieren Sie die Serversicherung, führen eine Serversicherung aus und testen dann die Wiederherstellungs-DVD.  
  
###### <a name="to-configure-and-run-a-server-backup"></a>So konfigurieren Sie eine Serversicherung und führen sie aus  
  
1.  Öffnen Sie das Dashboard, klicken Sie auf die Registerkarte **Geräte** und klicken Sie dann im Bereich **Aufgaben** auf **Sicherung für den Server einrichten**.  
  
2.  Folgen Sie den Anweisungen des Assistenten, um eine Serversicherung zu konfigurieren. Für die Sicherung benötigen Sie eine externe Festplatte.  
  
3.  Klicken Sie im Bereich **Aufgaben** auf **Sicherung für den Server starten** , und folgen Sie dann den Anweisungen des Assistenten.  
  
4.  Wenn die Sicherung abgeschlossen ist, überprüfen Sie, ob sie erfolgreich war.  
  
###### <a name="to-restore-a-server"></a>So stellen Sie einen Server wieder her  
  
1.  Legen Sie die Wiederherstellungs-DVD, die Sie erstellt haben, in einen Clientcomputer ein, der über einen Hub oder Switch mit demselben Netzwerk verbunden ist wie der Server.  
  
2.  Doppelklicken Sie auf **setup.exe**. Der Assistent für die Serverwiederherstellung führt Sie durch den gleichen Prozess, durch den auch der Kunde geführt wird.  
  
3.  Klicken Sie auf **Den Server aus einer Sicherung wiederherstellen**, und folgen Sie dann den Anweisungen des Assistenten.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Zusätzliche Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)