---
title: "Erstellen einer Serverwiederherstellungs-DVD für Remote verwaltete Server"
description: Beschreibt, wie Sie Windows Server Essentials
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
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="create-a-server-recovery-dvd-for-remotely-administered-servers"></a>Erstellen einer Serverwiederherstellungs-DVD für Remote verwaltete Server

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

##  <a name="BKMK_HeadlessRecovery"></a>Erstellen einer serverwiederherstellungs-DVD für Remote verwaltete Server  
 Es stehen zwei Modelle für die Factory und Wiederherstellung und unterscheiden sich abhängig von der Hardware, die der Kunde erhalten hat.  
  
 **Remote verwaltete Server**  
  
 Diese serverwiederherstellungsoption erfordert, dass der Prozess auf einem Clientcomputer im selben Netzwerk ausgeführt wird. Da auf die Werkseinstellungen zurücksetzen mit dem Server ein Images hardwarespezifische geliefert werden muss, muss der Partner die serverwiederherstellungs-DVD erstellen.  
  
 **Lokal verwalteter Server**  
  
 Dies ist das klassische Modell, in dem der Server über die Serverkonsole verwaltet wird. Das serverinstallationsmedium dient zum Ausführen einer Wiederherstellung. Dies erfordert, dass die Möglichkeit, Videoausgabe neben ein DVD-Lesegerät einschließlich der Server Lieferumfang. Der Kunde startet über dieses serverinstallationsmedium und wählt dann die geeignete Wiederherstellungsmethode. Sie müssen sich nicht um eine serverwiederherstellungs-DVD für Server zu erstellen, die lokal verwaltet werden.  
  
> [!NOTE]
>  Für das Modell mit lokal verwaltetem Server kann der Kunde eine Wiederherstellung der Herstellerstandards durch eine Neuinstallation durchführen. Allerdings wird der Partner Anpassungen unterbrochen.  
  
 Es gibt zwei Arten von serverwiederherstellung.  
  
 **Konsole zurücksetzen**  
  
 Mit dieser Wiederherstellung wird den Server auf den ursprünglichen Zustand, der vorhanden waren, wenn der Server vom Hersteller geliefert wurde. Nach auf die Werkseinstellungen zurücksetzen werden Sie aufgefordert, wie Sie beim ersten Einschalten waren die Erstkonfiguration des Servers ausführen, und alle Einstellungen und Anpassungen sind verloren. Dies wird auch als Tag 0 bezeichnet.? Da auf die Werkseinstellungen zurücksetzen mit dem Server ein Images hardwarespezifische geliefert werden muss, muss der Partner die serverwiederherstellungs-DVD erstellen.  
  
 **Bare-Metal-Recovery**  
  
 Bei diesem Wiederherstellungsvorgang wird davon ausgegangen, dass Sie eine Server-Sicherung konfiguriert und die Server-Sicherung mindestens ein Mal vor dem Serverausfall erfolgreich abgeschlossen wurde. Bare-Metal-Recovery (BMR) unterstützt das Wiederherstellen der System- und Startvolume Laufwerke nur von einer früheren Sicherung.  
  
 Nach einer BMR wird der Server in den Zustand zurückgegeben, die zum Zeitpunkt der Sicherung vorhanden waren, die für die Wiederherstellung verwendet wird. Dies ist in der Regel die aktuelle Sicherung, aber in einigen Fällen kann es sein, eine frühere Sicherung. Wiederherstellen von Daten erfolgt, nachdem das System mit dem Wiederherstellen von Dateien und Ordner-Assistent wiederhergestellt wird. BMR ist die bevorzugte serverwiederherstellungsmethode, da alle Einstellungen und Konfigurationen zurückgegeben werden, während auf die Werkseinstellungen Zurücksetzen des Servers in einen Zustand Tag 0 zurückgibt.  
  
### <a name="remotely-administered-server-recovery"></a>Remote verwaltete serverwiederherstellung  
 Dieser Abschnittbeschreibt die erforderlichen Anpassungen durch der Partner muss und die endgültigen Medien, die mit jedem Server ausgeliefert werden müssen. Sehen Sie bevor Sie mit den Detail befassen wir uns die Kundenzufriedenheit.  
  
 In diesem Szenario wird der Kunde "¢ s-Server nicht mehr funktioniert. Dies kann durch einen Virus, ein Festplattenfehler oder eine andere Ursache verursacht werden. Der Kunde legt die serverwiederherstellungs-DVD in einen Clientcomputer, der sich im selben Netzwerk wie der Server befindet. Die Anwendung führt sie durch die drei Schritteauf ihrem Server wiederherstellen:  
  
1.  Erstellt einen startbaren USB-Speicherstick, mit dem der Server im Wiederherstellungsmodus neu gestartet. Das USB-Flashlaufwerk muss 8GB groß.  
  
2.  Erkennt der Server, der jetzt im Wiederherstellungsmodus befindet.  
  
3.  Kann der Kunde auf die Werkseinstellungen zurückgesetzt oder eine bare-Metal-Wiederherstellung auswählen, und versetzt dann den Server in einen betriebsbereiten Zustand.  
  
### <a name="steps-for-creating-a-server-recovery-dvd-for-multiple-language-support"></a>Schrittezum Erstellen einer serverwiederherstellungs-DVD für mehrere Sprachen unterstützen.  
 Es gibt sechs Hauptschritte zum Erstellen einer serverwiederherstellungs-DVD  
  
1.  [(Optional) Aktualisieren von WinPE](Create-a-Server-Recovery-DVD-for-Remotely-Administered-Servers.md#BKMK_Updating)  
  
2.  [Sammeln die Wiederherstellung der Herstellerstandards Abbildern und XML-Dateien](Create-a-Server-Recovery-DVD-for-Remotely-Administered-Servers.md#BKMK_Collecting)  
  
3.  [Erstellen der serverwiederherstellungs-DVD](Create-a-Server-Recovery-DVD-for-Remotely-Administered-Servers.md#BKMK_Creating)  
  
4.  [Anpassen des Assistenten](Create-a-Server-Recovery-DVD-for-Remotely-Administered-Servers.md#BKMK_Customizing)  
  
5.  [Erstellen Sie die ISO-Datei](Create-a-Server-Recovery-DVD-for-Remotely-Administered-Servers.md#BKMK_CreatingISO)  
  
6.  [Testen der Wiederherstellungs-DVD](Create-a-Server-Recovery-DVD-for-Remotely-Administered-Servers.md#BKMK_Testing)  
  
####  <a name="BKMK_Updating"></a>Schritt1: (Optional) aktualisieren von WinPE  
 Das ADK umfasst eine Kopie von Windows PE, das angepasst wird. Wenn dieses Image gestartet wird, wird automatisch für die clientwiederherstellung, die von dem die Anwendung verwendet wird, eine Verbindung zu einem Server im Wiederherstellungsmodus gestartet.  
  
 Windows PE muss weiter angepasst werden, indem hardwarespezifische Treiber wie Netzwerk oder für Festplattencontroller-Treiber hinzugefügt. Nach dem Start von WinPE, müssen die Festplatten auf dem System erkannt werden, und das Netzwerk muss funktionieren.  
  
####  <a name="BKMK_Collecting"></a>Schritt2: Sammeln die Wiederherstellung der Herstellerstandards Abbildern und XML-Dateien  
 Um einen Server auf die werkseitigen Standardeinstellungen zurückzusetzen, müssen die folgenden beiden Abbilder erfasst werden:  
  
-   Das Abbild des Systemlaufwerks  
  
-   Das System reservierte Partition  
  
 Zur Aufzeichnung dieser Abbilder wird das Tool GenDiskXML.exe bereitgestellt. GenDiskXML.exe sammelt auch eine Datei namens disk.xml, die von den Wiederherstellungsvorgang verwendet wird, um die Datenträgerkonfiguration neu erstellt.  
  
1.  Starten Sie nach Sysprep das System mit einer 64-Bit-Version von Windows PE neu.  
  
2.  Um die XML- und WIM-Dateien in einer externen Quelle auszugeben, führen Sie `GenDiskXML /outputdir:<path>`um die XML- und WIM-Dateien in eine externe Quelle auszugeben. Die Dateien werden von der DVD im nächsten Schritthinzugefügt.  
  
    > [!NOTE]
    >  Die WIM-Datei des Systems wird zum Erfüllen der FAT32-Anforderung, dass Dateien höchstens 4GB aufgeteilt werden. Während des Vorgangs muss die erforderliche Kapazität des Ziels, mit dem die WIM-Dateien erfassen, größer als 8GB betragen, damit die Teilung sein.  
  
####  <a name="BKMK_Creating"></a>Schritt3: Erstellen der serverwiederherstellungs-DVD  
 Jeder vom Hersteller ausgelieferten Server muss eine serverwiederherstellungs-DVD beizufügen. Die ADK-Tools-DVD enthält die Dateien, die zum Erstellen der DVD.  
  
###### <a name="to-create-the-server-recovery-dvd"></a>Zum Erstellen der serverwiederherstellungs-DVD  
  
1.  Erstellen Sie einen Ordner als Speicherort verwenden, für die endgültige ISO-Datei zu speichern.  
  
2.  Kopieren Sie den Inhalt der von der Partner-CD, die **Serverwiederherstellungs** Ordner, die Sie in Schritt1 erstellten Arbeitsordner.  
  
3.  Kopieren Sie die disk.xml-Datei, die erstellt wurde, bei der Ausführung GenDiskXML.exe auf die **zurücksetzen** Ordner.  
  
4.  Kopieren Sie die Bilddateien, die erstellt wurden, bei der Ausführung **GenDiskXML.exe** auf die **zurücksetzen** Ordner. Die Dateien sind die WIM- und SWM-Dateien, und die Anzahl der Dateien kann variieren.  
  
5.  Entfernen Sie GenDiskXML.exe aus dem Ordner. Es wird nur für werkseitige verwendet und sollte nicht auf der DVD, die an den Kunden ausgeliefert wird aufgenommen werden.  
  
####  <a name="BKMK_Customizing"></a>Schritt4: Anpassen des Assistenten  
 Mit einem Bild des Geräts und der Text, der beschreibt, wie Sie das Gerät in den Wiederherstellungsmodus zu starten, muss die Anwendung angepasst werden. Da diese Seite des Wiederherstellen von Dateien und Ordnern Assistenten hardwarespezifisch ist, variieren die Schritte, um den Server in den Wiederherstellungsmodus zu starten.  
  
> [!NOTE]
>  Die aufgeführten Dateinamen müssen genau übereinstimmen.  
  
1.  Die Seite ist ein Link für zusätzliche Hilfe. Wenn diese CHM-Datei vorhanden ist, wird der FWLink für die Webhilfe überschrieben. Die Hilfedatei befindet sich unter:  
  
     < DVD Root\ > \\$OEM$\Customization\\ < Kultur Tokentypen > \RestartHelp.chm  
  
2.  Diese Datei enthält den Text, den der Kunde auf der Seite des Assistenten angezeigt wird. Der Text sollte der Server im Wiederherstellungsmodus gestartet erläutert. Das Steuerelement sind Bildläufe die stellt eine praktische Beschränkung an, auf die Menge an Text, der hinzugefügt werden kann.  
  
     Die folgende Datei wird verwendet, um das Beispielbild im Assistenten ersetzt, und sie dient vorwiegend dem Branding. Es muss eine PNG-Datei sein. Die Dateigröße muss 256 Pixel X 256 Pixel sein, oder es werden abgeschnitten, wenn sie im Assistenten angezeigt wird.  
  
     < DVD Root\ > \\$OEM$\Customization\\ < Kultur Tokentypen > \RestartInstructions.rtf  
  
3.  < DVD Root\ > \\$OEM$\Customization\\ < Kultur Tokentypen > \ServerImage.png  
  
 Wenn Sie Ihre serverwiederherstellungs-DVD zur Unterstützung mehrerer Sprachen konvertieren, stellen Sie sicher, dass Sie die folgenden Schritteaus:  
  
1.  Benötigen Sie immer die En-us Ordner. Falls die Anwendung die kulturspezifischen Dateien nicht findet, die den Clientcomputer entsprechen, Computer, es fragt En-us.  
  
2.  Fügen Sie in jedem Kulturordner, den Sie erstellen, die drei Anpassungsdateien (.png, chm und RTF).  
  
3.  Kopieren Sie beide Kulturordner aus Sprache Packs\\ < CultureName\ > \Server Recovery, mit dem Stamm der serverwiederherstellungs-DVD. Beispiel: die Ordner ES und ES-ES in das Stammverzeichnis der DVD zur Unterstützung von Spanisch kopiert werden.  
  
4.  Abschließen der ISO-Datei.  
  
 Unterstützte Kulturnamen:  

|-|-|  
|-Cs-CZ<br /><br /> -de-DE<br /><br /> -en-US<br /><br /> -es-ES<br /><br /> -fr-FR<br /><br /> -Hu-HU<br /><br /> -it-IT<br /><br /> -Ja-JP<br /><br /> -Ko-KR<br /><br /> -Nl-NL |-pl-PL<br /><br /> -Pt-BR<br /><br /> -Pt-PT<br /><br /> -Ru-RU<br /><br /> -Sv-SE<br /><br /> -Tr-TR<br /><br /> -Zh-CN<br /><br /> -Zh-HK<br /><br /> -zh-TW
  
####  <a name="BKMK_CreatingISO"></a>Schritt5: Erstellen der ISO-Datei  
 Der Ordner, der erstellt wurde und der Inhalt können auf eine DVD gebrannt werden. Dies ist die DVD, die für Kunden mit einem neuen Server bereitgestellt werden.  
  
####  <a name="BKMK_Testing"></a>Schritt6: Testen der Wiederherstellungs-DVD  
 Konfigurieren Sie nach Abschluss der Serverinstallation die Server-Sicherung, führen Sie eine Server-Sicherung aus und Testen Sie die Wiederherstellungs-DVD.  
  
###### <a name="to-configure-and-run-a-server-backup"></a>Zum Konfigurieren und Ausführen einer Sicherung  
  
1.  Öffnen Sie das Dashboard, klicken Sie auf die **Geräte** Registerkarte, und klicken Sie dann auf **Sicherung für den Server einrichten** in der **Aufgaben** Bereich.  
  
2.  Führen Sie die Anweisungen im Assistenten, um eine serversicherung zu konfigurieren. Sie benötigen eine externe Festplatte für die Sicherung.  
  
3.  Klicken Sie auf **starten Sie eine Sicherung für den Server** in der **Aufgaben** Bereich, und folgen Sie dann die Anweisungen im Assistenten.  
  
4.  Wenn die Sicherung abgeschlossen ist, stellen Sie sicher, dass der Vorgang erfolgreich war.  
  
###### <a name="to-restore-a-server"></a>Zum Wiederherstellen eines Servers  
  
1.  Legen Sie die Wiederherstellungs-DVD, die Sie erstellt haben, in einen Clientcomputer, der mit dem gleichen Netzwerk wie der Server über einen Hub oder Switch verbunden ist.  
  
2.  Doppelklicken Sie auf **setup.exe**. Der Assistent für die Serverwiederherstellung durch den gleichen Prozess, den der Kunde, aufgefordert.  
  
3.  Klicken Sie auf **den Server aus einer Sicherung wiederherstellen**, und folgen Sie dann die Anweisungen im Assistenten.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)