---
title: Verwenden des Remotewebzugriffs in Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47ea21a0-5e05-4b4b-8fa4-338c82601276
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: ac384b545fe61b4a832debdc8aedcc81a75c669a
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="use-remote-web-access-in-windows-server-essentials"></a>Verwenden des Remotewebzugriffs in Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials
  
  Remotewebzugriff bietet Ihnen mit Ihrer Windows Server Essentials-Netzwerk verbunden bleiben, wenn Sie unterwegs sind. Wenn Sie sich mit Remote Web Access anmelden, können Sie mit den Computern in Ihrem Windows Server Essentials-Netzwerk verbinden, öffnen Sie das Dashboard zum Verwalten Ihres Windows Server Essentials-Netzwerks und Zugriff auf alle freigegebenen Ordner und Mediendateien Dateien auf dem Server.  
  
 Dieses Thema enthält die folgenden Abschnitte:  
  

-   [Verbinden Sie mit Remote Web Access](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Connect)  
  
-   [Freigeben von Dateien und Ordnern](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SharedFolders)  
  
-   [Herstellen einer Verbindung von einem mobilen Gerät](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ConnectMobile)  
  
##  <a name="BKMK_Connect"></a>Verbinden Sie mit Remote Web Access  
  
-   [Melden Sie sich bei Remotewebzugriff](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Remotezugriff auf Ihrem computer](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_1.5)  

-   [Verbinden Sie mit Remote Web Access](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Connect)  
  
-   [Freigeben von Dateien und Ordnern](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SharedFolders)  
  
-   [Herstellen einer Verbindung von einem mobilen Gerät](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ConnectMobile)  
  
##  <a name="BKMK_Connect"></a>Verbinden Sie mit Remote Web Access  
  
-   [Melden Sie sich bei Remotewebzugriff](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Remotezugriff auf Ihrem computer](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_1.5)  

  
###  <a name="BKMK_1"></a>Melden Sie sich bei Remotewebzugriff  
 Wenn Sie mit Remote Web Access aus einem lokalen Computer oder Remotecomputer anmelden, können Sie Ressourcen auf Ihrem Server unter Windows Server Essentials und Computer in Ihrem Netzwerk zugreifen.  
  
##### <a name="to-log-on-to-remote-web-access-from-a-network-computer"></a>Von einem Computer im Netzwerk mit Remote Web Access anmelden  
  
1.  Öffnen Sie einen Webbrowser, geben **https://***< YourServerName\ >***/remote** in die Adressleiste, und drücken Sie dann die EINGABETASTE.  
  
    > [!NOTE]
    >  Stellen Sie sicher, dass Sie das "s" in Https einschließen.  
  
2.  Geben Sie auf der Anmeldeseite des Remotewebzugriffs Ihren Benutzernamen und Ihr Kennwort in die Textfelder ein, und klicken Sie dann auf den Pfeil.  
  
##### <a name="to-log-on-to-remote-web-access-from-a-remote-computer"></a>Von einem Remotecomputer mit Remote Web Access anmelden  
  
1.  Öffnen Sie einen Webbrowser, geben **https://***< YourDomainName\ >***/remote** in die Adressleiste, und drücken Sie dann die EINGABETASTE.  
  
    > [!NOTE]
    >  Sie können Ihre Domänennameninformationen von Ihrem Netzwerkadministrator abrufen. Stellen Sie sicher, dass Sie das "s" in Https einschließen.  
  
2.  Geben Sie auf der Anmeldeseite des Remotewebzugriffs Ihren Benutzernamen und Ihr Kennwort in die Textfelder ein, und klicken Sie dann auf den Pfeil.  
  
###  <a name="BKMK_1.5"></a>Remotezugriff auf Ihrem computer  
 Wenn Sie nicht im Büro sind, können Sie Ihren Webbrowser, zu Remote Web Access, Remotezugriff auf Ihrem Windows Server Essentials-Dashboard, freigegebene Ordner und Computer in Ihrem Netzwerk anmelden.  
  
 Wenn Sie auf das Dashboard verbinden, können Sie Windows Server Essentials verwalten, genau wie wenn Sie sich im Büro befinden. Sie können ausgeführt werden, der üblichen Verwaltungsaufgaben, wie z. B. das Hinzufügen von Benutzerkonten, Hinzufügen von freigegebenen Ordnern Festlegen des Zugriffs auf freigegebene Ordner und so weiter. Wenn Sie auf Computern in Ihrem Netzwerk verbinden, können Sie ihre Desktops zugreifen, als säßen Sie direkt vor ihnen im Büro.  
  
 Die **Status** Spalte zeigt an, ob Sie auf einem Computer in Ihrem Netzwerk herstellen können und können die folgenden Werte enthalten:  
  
-   **Verfügbar**  
  
     Der Computer eingeschaltet ist und für eine Remoteverbindung verfügbar ist. Auch wenn dieser Status angezeigt wird, können Sie möglicherweise trotzdem nicht auf diesem Computer herstellen, wenn eine Drittanbieterfirewall die Verbindung blockiert.  
  
-   **Offline oder im Ruhezustand**  
  
     Der Computer ist ausgeschaltet oder befindet sich im Energiesparmodus oder Ruhezustand befindet. Wenn ein Computer offline oder im Ruhezustand ist, wird der Status in Echtzeit aktualisiert, damit Sie ermitteln können, wenn der Computer verfügbar ist.  
  
-   **Nicht unterstütztes Betriebssystem**  
  
     Das Betriebssystem auf dem Computer unterstützt Remotedesktop nicht. Es kann für den Status auf dem Server aktualisiert werden, wenn eine Änderung von bis zu sechs Stunden dauern.  
  
-   **Verbindung ist deaktiviert.**  
  
     Die computerverbindung wird entweder durch eine Firewall blockiert, oder der Remotedesktop auf dem Computer oder durch eine Gruppenrichtlinie deaktiviert ist. Es kann für den Status auf dem Server aktualisiert werden, wenn eine Änderung von bis zu sechs Stunden dauern.  
  
#### <a name="to-connect-to-a-computer-on-your-network"></a>Verbindung mit einem Computer in Ihrem Netzwerk  
 Auf der **Geräte** auf den Namen des Computers. Sie können auswählen, nur auf Computern mit einer **verfügbar** Status.  
  
#### <a name="to-connect-to-the-server-dashboard"></a>Verbindung mit dem Server-Dashboard  
 Auf der **Geräte** auf den Namen des Servers. Sie können auswählen, nur auf Computern mit einer **verfügbar** Status. Sie müssen ein Benutzerkonto und Kennwort auf dem Server des Dashboards bereitstellen können.  
  
##  <a name="BKMK_SharedFolders"></a>Freigeben von Dateien und Ordnern  
  

-   [Hochladen und Herunterladen von Dateien in Remote Web Access](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_UploadRWA)  
  
-   [Erstellen, umbenennen, verschieben, löschen oder Kopieren von Dateien und Ordner in Remote Web Access](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_2)  

-   [Hochladen und Herunterladen von Dateien in Remote Web Access](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_UploadRWA)  
  
-   [Erstellen, umbenennen, verschieben, löschen oder Kopieren von Dateien und Ordner in Remote Web Access](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_2)  

  
###  <a name="BKMK_UploadRWA"></a>Hochladen und Herunterladen von Dateien in Remote Web Access  
 Der Remotewebzugriff **freigegebene Ordner** Registerkarte können Sie Folgendes tun:  
  
-   Hochladen Sie (senden) Dateien von Ihrem Computer mit Windows Server Essentials.  
  
    > [!NOTE]
    >  Sie können mit Remote Web Access nur Dateien und nicht für Ordner hochladen. Wenn Sie den gleichen Datei- und Ordnerhierarchie in möchten den **freigegebene Ordner** auf dem Server auf dem Computer, Sie müssen die Ordner auf dem Server im Remotewebzugriff erstellen, und klicken Sie dann die Dateien in den von Ihnen erstellten Ordner hochladen. Informationen zum Erstellen von Serverordnern finden Sie unter [hinzufügen oder Verschieben eines Serverordners](../manage/Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_5).  
  
-   Laden (empfangen) Dateien und Ordner von Windows Server Essentials auf Ihrem Computer.  
  
-   Erstellen Sie einen Ordner in einem freigegebenen Ordner auf Windows Server Essentials.  
  

-   Verschieben, löschen und Umbenennen von Dateien und Ordner auf Windows Server Essentials. Weitere Informationen finden Sie unter [erstellen, umbenennen, verschieben, löschen oder Kopieren von Dateien und Ordnern in Remote Web Access](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_2).  

-   Verschieben, löschen und Umbenennen von Dateien und Ordner auf Windows Server Essentials. Weitere Informationen finden Sie unter [erstellen, umbenennen, verschieben, löschen oder Kopieren von Dateien und Ordnern in Remote Web Access](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_2).  

  
#### <a name="upload-files"></a>Hochladen von Dateien  
  
###### <a name="to-upload-files"></a>Zum Hochladen von Dateien  
  
1.  Klicken Sie im Remotewebzugriff auf die **freigegebene Ordner** Registerkarte, und klicken Sie dann auf einen Link für die freigegebenen Ordner. Es wird eine Liste der Dateien und Ordner in diesem freigegebenen Ordner angezeigt.  
  
2.  Aus der Liste der freigegebenen Ordner der Dateien und Ordner, klicken Sie auf den Ordner, in dem Sie laden Sie die Datei, und klicken Sie dann auf möchten **hochladen**.  
  
3.  Wenn das standardmäßige Uploadtool nicht bereits geladen ist, klicken Sie auf **verwenden Sie die Standardmethode für Uploads Methode**.  
  
4.  Klicken Sie auf **Durchsuchen** um eine Datei auf Ihrem Computer zu suchen.  
  
5.  Navigieren Sie durch die Ordner auf Ihrem Computer nach der Datei, die Sie hochladen möchten, und klicken Sie dann auf **öffnen**.  
  
6.  Wiederholen Sie die Schritte 2 und 3 für jede Datei, die Sie hochladen möchten.  
  
7.  Wenn Sie alle Dateien, die Sie verwenden möchten, auf hinzugefügt haben **hochladen**.  
  
 Die Tool "einfacher Dateiupload" optimiert das Hochladen von Dateien auf Ihrem Server unter Windows Server Essentials. Sie können beliebig viele Dateien, wie Sie das Tool "einfacher Dateiupload", mit der Drag & Drop-Funktion soll hinzufügen, und klicken Sie dann auf die freigegebenen Ordner auf dem Server hochladen.  
  
> [!NOTE]
>  Hochladen mehrerer Dateien wird in Webbrowsern unterstützt, die mit HTML5 kompatibel sind. Dieses Tool ist nur erforderlich, wenn der Webbrowser HTML5 nicht unterstützt.  
  
###### <a name="to-upload-files-using-the-easy-file-upload-tool"></a>Zum Hochladen von Dateien mit dem Tool einfacher Dateiupload  
  
1.  Klicken Sie im Remotewebzugriff auf die **freigegebene Ordner** Registerkarte, und klicken Sie dann auf einen Link für die freigegebenen Ordner. Es wird eine Liste der Dateien und Ordner in diesem freigegebenen Ordner angezeigt.  
  
2.  Aus der Liste der freigegebenen Ordner der Dateien und Ordner, klicken Sie auf den Ordner, in dem Sie Dateien hochladen, und klicken Sie dann auf möchten **hochladen**. Wenn auf der Ordner, die Sie nicht vorhanden ist hochladen möchten, **neuen Ordner**, geben Sie den Namen des neuen Ordners im Dialogfeld ein, und klicken Sie dann auf **OK**.  
  
3.  Sie müssen möglicherweise das Add-on für Windows Server-Lösungen ausführen. Wenn dies der Fall ist, klicken Sie in den gelben Streifen oben auf dem Bildschirm, klicken Sie auf Ausführen **Add-on**, und klicken Sie dann auf **ausführen** im Dialogfeld.  
  
4.  Wenn das Tool einfacher Dateiupload nicht bereits geladen ist, klicken Sie auf **verwenden Sie das Tool einfacher Dateiupload**.  
  
5.  Können Sie Drag & Drop-Dateien von Windows-Explorer auf das Tool einfacher Dateiupload, oder klicken Sie auf **durchsuchen, um Dateien auszuwählen**.  
  
6.  Wenn Sie die Dateien, die Sie verwenden möchten, in den ausgewählten Ordner hochladen, klicken Sie auf hinzugefügt haben **hochladen**.  
  
7.  Wenn die Dateien erfolgreich hochgeladen wurden, klicken Sie auf **schließen**.  
  
#### <a name="download-files-or-folders"></a>Herunterladen von Dateien oder Ordner  
  
###### <a name="to-download-a-single-file"></a>Eine einzelne Datei herunterladen  
  
1.  Klicken Sie im Remotewebzugriff auf die **freigegebene Ordner** Registerkarte, und klicken Sie dann auf einen Link für die freigegebenen Ordner. Es wird eine Liste der Dateien und Ordner in diesem freigegebenen Ordner angezeigt.  
  
2.  Klicken Sie in der Liste der freigegebenen Ordner auf das Kontrollkästchen neben der Datei, die Sie auf Ihrem Computer zu Hause herunterladen möchten.  
  
3.  Klicken Sie auf **herunterladen** um den Download zu starten.  
  
4.  Auf der **Dateidownload** Dialogfeld, klicken Sie auf **speichern** zum Speichern der Datei auf Ihrem Computer.  
  
5.  In der **speichern** Dialogfeld Feld, wählen Sie den Speicherort zum Speichern der Datei, und klicken Sie dann auf **speichern**. Eine einzelne Datei wird nicht komprimiert, bevor sie heruntergeladen wird.  
  
 Es gibt zwei Optionen zum Herunterladen mehrerer Dateien oder Ordner. Wählen Sie die Option, die Ihren Bedürfnissen entspricht:  
  
> [!NOTE]
>  Diese Optionen stehen nur, wenn Sie mehrere Dateien oder Ordner auf Ihren Computer herunterladen.  
  
-   **Selbstextrahierende ausführbare Datei (.exe)**  
  
    > [!NOTE]
    >   Dieser Abschnitt gilt für einen Server mit Windows Server Essentials.  
  
     Eine selbstextrahierende ausführbare Datei ist eine Datei, die Sie herunterladen können, die das Dekomprimierungsprogramm (ausführbare Datei) mit den komprimierten Dateien kombiniert. Wenn Sie das ausführbare Programm ausführen, dekomprimiert es automatisch die komprimierten Dateien (selbstextrahierend). Dies ist eine gebräuchliche Methode zum Verteilen von komprimierter Daten ohne Rücksicht auf, ob der Empfänger die nötige dekomprimierungshilfsprogramm verfügen muss.  
  
    > [!NOTE]
    >  Diese Option unterstützt Unicode-Zeichen.  
  
-   **Windows-komprimierten Ordner (ZIP)**  
  
     Komprimieren einer Datei wird eine komprimierte Version der Datei, die kleiner als die ursprüngliche Datei wird erstellt. Die komprimierte Version der Datei hat die Erweiterung ZIP-Datei. Dateitypen, die durch das Komprimieren von sind, sind textorientierte Dateitypen wie txt, -DOC-, XLS- und grafische Dateien, die nicht komprimierte Dateitypen wie .bmp. Einige Grafikdateien wie JPG- und GIF-Dateien nutzen bereits die Komprimierung und die Dateigröße durch das Komprimieren nur sehr wenig. Darüber hinaus wird ein Worddokument, das viele Grafiken enthält nicht so viel wie ein Dokument reduziert, die hauptsächlich Text.  
  
    > [!NOTE]
    >  Diese Option bietet eingeschränkte Unterstützung für internationale Dateinamen in Windows Server Essentials.  
  
 Vor Beginn des eigentlichen Downloads wird die EXE- oder Zip-Datei erstellt. Je nach Anzahl der Dateien und die Gesamtgröße der Dateien heruntergeladen werden kann dies einige Minuten dauern. Nachdem die Downloaddatei erstellt wurde, erfolgt das Herunterladen der das im Hintergrund. Dadurch können Sie weiterarbeiten, während der Downloadvorgang ausgeführt wird.  
  
###### <a name="to-download-multiple-files-or-folders"></a>Um mehrere Dateien oder Ordner herunterzuladen.  
  
1.  Klicken Sie im Remotewebzugriff auf die **freigegebene Ordner** Registerkarte, und klicken Sie dann auf einen Link für die freigegebenen Ordner. Es wird eine Liste der Dateien und Ordner in diesem freigegebenen Ordner angezeigt.  
  
2.  Klicken Sie in der Liste der freigegebenen Ordner auf das Kontrollkästchen neben den Dateien oder Ordnern, die Sie auf Ihrem Computer zu Hause herunterladen möchten.  
  
3.  Klicken Sie auf **herunterladen** um den Download zu starten.  
  
4.  In der **Downloadformat** Dialogfeld, klicken Sie auf die Option zum Herunterladen von Format auszuwählen, die Sie bevorzugen, und klicken Sie dann auf **OK**. Die komprimierte Datei wird Formatoption vorbereitet, die Sie ausgewählt haben.  
  
5.  In der **Dateidownload** Dialogfeld, klicken Sie auf **speichern** zum Speichern der Datei auf Ihrem Computer.  
  
6.  In der **speichern** Dialogfeld Feld, wählen Sie den Speicherort zum Speichern der Datei, und klicken Sie dann auf **speichern**.  
  
#### <a name="retrieve-compressed-files-downloaded-to-your-computer"></a>Abrufen von komprimierten Dateien auf Ihren Computer heruntergeladen  
  
> [!NOTE]
>   Dieser Abschnitt gilt für einen Server mit Windows Server Essentials.  
  
 Wenn Sie mehrere Dateien oder Ordner herunterzuladen auswählen, erhalten Sie eine selbstextrahierende komprimierte ausführbare Datei (.exe) oder eine komprimierte Datei (.zip).  
  
###### <a name="to-retrieve-a-file-from-the-compressed-exe-file"></a>Zum Abrufen einer Datei aus der komprimierten (.exe)-Datei  
  
1.  Doppelklicken Sie auf dem Computer auf die komprimierte Datei, um es zu öffnen.  
  
2.  Führen Sie die Anweisungen, um die Dateien in einen Ordner auf Ihrem Computer zu extrahieren.  
  
###### <a name="to-retrieve-a-file-from-the-compressed-zip-file"></a>Zum Abrufen einer Datei aus der komprimierten ZIP-Datei  
  
1.  Doppelklicken Sie auf dem Computer auf die komprimierte Datei, um es zu öffnen.  
  
2.  Wählen Sie die Dateien, die Sie abrufen möchten, und ziehen Sie dann die Dateien in einen Ordner auf Ihrem Computer, die Sie speichern möchten.  
  
    > [!NOTE]
    >  Wenn Sie eine Drittanbieter-Komprimierungsprogramm verwenden, führen Sie die Verfahren für das Programm, um Ihre Dateien aus der komprimierten Datei zu extrahieren.  
  
###  <a name="BKMK_2"></a>Erstellen, umbenennen, verschieben, löschen oder Kopieren von Dateien und Ordner in Remote Web Access  
 Remote Web Access können Sie neue Ordner in einem vorhandenen freigegebenen Ordner umbenennen, Dateien und Ordner verschieben und Kopieren von Dateien und Ordner, und Löschen von Dateien und Ordner auf Ihrem Server erstellen.  
  
> [!NOTE]
>  Zum Hinzufügen neuer freigegebener Ordner auf einem Server, auf denen Windows Server Essentials ausgeführt wird, müssen Sie das Dashboard verwenden. Verbindung zur Serverkonsole über den Remotewebzugriff auf, auf die **Computer** Registerkarte, klicken Sie auf den Servernamen, klicken Sie auf **verbinden**, und folgen Sie dann die Anweisungen zum Anmelden beim Server. Informationen zur Vorgehensweise beim Erstellen von freigegebenen Ordnern finden Sie unter [hinzufügen oder Verschieben eines Serverordners](../manage/Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_5).  
  
##### <a name="to-create-a-new-folder"></a>Um einen neuen Ordner zu erstellen.  
  
1.  Klicken Sie im Remotewebzugriff auf die **freigegebene Ordner** Registerkarte, und klicken Sie dann auf Verknüpfung eines freigegebenen Ordners. Es wird eine Liste der Dateien und Ordner in diesem freigegebenen Ordner angezeigt.  
  
2.  Klicken Sie auf der Taskleiste auf **neuen Ordner**.  
  
3.  Geben Sie einen Namen für den Ordner, und klicken Sie dann auf **OK**.  
  
##### <a name="to-rename-a-file-or-folder"></a>So benennen Sie eine Datei oder einen Ordner um  
  
1.  Klicken Sie im Remotewebzugriff auf die **freigegebene Ordner** Registerkarte, und klicken Sie dann auf Verknüpfung eines freigegebenen Ordners. Es wird eine Liste der Dateien und Ordner in diesem freigegebenen Ordner angezeigt.  
  
2.  Mit der rechten Maustaste die Datei oder den Ordner, den Sie umbenennen möchten, und klicken Sie dann auf **umbenennen**.  
  
3.  Geben Sie einen neuen Namen in das Textfeld ein, und klicken Sie dann auf **OK**.  
  
##### <a name="to-move-files-or-folders"></a>So verschieben Sie Dateien oder Ordner  
  
1.  Klicken Sie im Remotewebzugriff auf die **freigegebene Ordner** Registerkarte, und klicken Sie dann auf Verknüpfung eines freigegebenen Ordners. Es wird eine Liste der Dateien und Ordner in diesem freigegebenen Ordner angezeigt.  
  
2.  Aktivieren Sie das Kontrollkästchen neben den Dateien oder Ordnern, die Sie verwenden möchten, verschieben, mit der rechten Maustaste eine der ausgewählten Dateien bzw. Ordner, und klicken Sie dann auf **Ausschneiden**.  
  
3.  Mit der rechten Maustaste in des Ordners, die Sie verwenden möchten, verschieben Sie die Dateien oder Ordner, und klicken Sie dann auf **einfügen**.  
  
##### <a name="to-delete-a-file-or-folder"></a>So löschen Sie eine Datei oder einen Ordner  
  
1.  Klicken Sie im Remotewebzugriff auf die **freigegebene Ordner** Registerkarte, und klicken Sie dann auf Verknüpfung eines freigegebenen Ordners. Es wird eine Liste der Dateien und Ordner in diesem freigegebenen Ordner angezeigt.  
  
2.  Aktivieren Sie das Kontrollkästchen neben den Dateien oder Ordnern, die Sie verwenden möchten, löschen, mit der rechten Maustaste eine der ausgewählten Dateien bzw. Ordner, und klicken Sie dann auf **löschen**.  
  
3.  Um zu bestätigen, dass Sie die ausgewählten Dateien und Ordner löschen möchten, klicken Sie auf **Ja**.  
  
##### <a name="to-copy-files-or-folders"></a>Kopieren von Dateien oder Ordner  
  
1.  Klicken Sie im Remotewebzugriff auf die **freigegebene Ordner** Registerkarte, und klicken Sie dann auf Verknüpfung eines freigegebenen Ordners. Es wird eine Liste der Dateien und Ordner in diesem freigegebenen Ordner angezeigt.  
  
2.  Aktivieren Sie das Kontrollkästchen neben den Dateien oder Ordnern, die Sie verwenden möchten, kopieren, mit der rechten Maustaste eine der ausgewählten Dateien bzw. Ordner, und klicken Sie dann auf **Kopie**.  
  
3.  Mit der rechten Maustaste in des Ordners, die Sie verwenden möchten, kopieren Sie die Dateien oder Ordner, und klicken Sie dann auf **einfügen**.  
  
##  <a name="BKMK_ConnectMobile"></a>Herstellen einer Verbindung von einem mobilen Gerät  
  

-   [Verwenden von Remotewebzugriff von einem mobilen Gerät](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_8)  
  
-   [Unterstützte Webbrowser für Mobilgeräte](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_9)  

-   [Verwenden von Remotewebzugriff von einem mobilen Gerät](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_8)  
  
-   [Unterstützte Webbrowser für Mobilgeräte](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_9)  

  
###  <a name="BKMK_8"></a>Verwenden von Remotewebzugriff von einem mobilen Gerät  
 Sie können mit Remote Web Access auf Ihrem Smartphone zum Anzeigen von Dateien und Ordner in den freigegebenen Ordnern auf dem Server anmelden.  
  
> [!NOTE]
>  Sie können auch herunterladen und verwenden Sie die My Server-app für Windows Server Essentials aus der [Windows Phone Marketplace](http://www.windowsphone.com/apps/6c2f98d5-6fcf-4e1d-b8b1-cde62ea1a94a) auf Ihre freigegebenen Ordner und Mediendateien zuzugreifen, die auf dem Server gespeichert sind.  
  
##### <a name="to-log-on-to-remote-web-access-from-a-mobile-device"></a>Von einem mobilen Gerät mit Remote Web Access anmelden  
  
1.  Öffnen Sie einen Webbrowser und geben **https://***< YourDomainName\ >***/remote** in die Adressleiste.  Stellen Sie sicher, dass Sie das "s" in Https einschließen.  
  
2.  Geben Sie auf der Anmeldeseite des Remotewebzugriffs Ihren Benutzernamen und Ihr Kennwort in die Textfelder ein, und klicken Sie dann auf den Pfeil. Sie sind in der mobilen Version des Remotewebzugriffs angemeldet.  
  
##### <a name="to-switch-to-the-desktop-version-of-remote-web-access"></a>So wechseln Sie in der Desktopversion des Remotewebzugriffs  
  
1.  Öffnen Sie einen Webbrowser und geben **https://***< YourDomainName\ >***/remote** in die Adressleiste.  Stellen Sie sicher, dass Sie das "s" in Https einschließen.  
  
2.  Geben Sie auf der Anmeldeseite des Remotewebzugriffs, Ihren Benutzernamen und Ihr Kennwort in die Textfelder ein, klicken Sie auf **Desktopversion anzeigen**, und klicken Sie dann auf den Pfeil. Sie sind in der Desktopversion des Remotewebzugriffs angemeldet.  
  
##### <a name="to-return-to-the-mobile-version-of-remote-web-access"></a>Zurückkehren zu der mobilen Version des Remotewebzugriffs  
  
1.  Melden Sie sich ab.  
  
2.  Öffnen Sie einen Webbrowser und geben **https://***< YourDomainName\ >***/Remote/m** in die Adressleiste. Stellen Sie sicher, dass Sie das "s" in Https einschließen.  
  
3.  Die mobile Version des Remotewebzugriffs wird angezeigt. Geben Sie auf der Anmeldeseite des Remotewebzugriffs Ihren Benutzernamen und Ihr Kennwort in die Textfelder ein, und klicken Sie dann auf den Pfeil. Sie sind in der mobilen Version des Remotewebzugriffs angemeldet.  
  
 Sie können für Dateien und Ordner in den freigegebenen Ordnern auf dem Server suchen.  
  
###  <a name="BKMK_9"></a>Unterstützte Webbrowser für Mobilgeräte  
 Unterstützte Webbrowser für Mobilgeräte umfassen:  
  
-   Internet Explorer Mobile 6.0 oder höher  
  
-   Safari  
  
-   BlackBerry  
  
-   Symbian 6.0 oder höher  
  
-   Android  
  
-   Google Chrome  
  
-   Firefox  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten des Remotewebzugriffs](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  

-   [Remote-Arbeit](Work-Remotely-in-Windows-Server-Essentials.md)  
  
-   [Verwenden von Windows Server Essentials](Use-Windows-Server-Essentials.md)

-   [Remote-Arbeit](../use/Work-Remotely-in-Windows-Server-Essentials.md)  
  
-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)

