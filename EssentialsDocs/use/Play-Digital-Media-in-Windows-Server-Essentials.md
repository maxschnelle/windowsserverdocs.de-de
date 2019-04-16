---
title: Wiedergeben von digitalen Medien in Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f570492-ee21-471b-92c1-3fd9bfb84f55
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 8228d0b17a58858ed893181ddceb465715ffdeb5
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="play-digital-media-in-windows-server-essentials"></a>Wiedergeben von digitalen Medien in Windows Server Essentials

>Gilt für: Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Digitale Medien sind Audio-, Video- und fotoinhalte, die Digital komprimiert wurden.  Windows Server Essentials ermöglicht es Computern und einigen Mediengeräten im Netzwerk digitale digitale Mediendateien wiedergeben, die auf dem Server gespeichert sind.  
  
 Die folgenden Themen enthalten Informationen zum Zugreifen auf und Wiedergeben von digitalen Mediendateien, die auf Windows Server Essentials gespeichert sind:  
  

-   [Übersicht über digitale Medien](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Wiedergeben Sie und freigeben Sie digitaler Medien](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Wiedergeben freigegebener digitaler Mediendateien von einem Remotestandort aus](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [Fügen Sie digitaler Mediendateien mit dem Server hinzu](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [Formatoptionen für Downloads](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [Einfache Dateiupload-Tool](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6)  
  
-   [Anzeigen und Durchsuchen von freigegebenen digitalen Medien](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_7)  

-   [Übersicht über digitale Medien](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Wiedergeben Sie und freigeben Sie digitaler Medien](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Wiedergeben freigegebener digitaler Mediendateien von einem Remotestandort aus](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [Fügen Sie digitaler Mediendateien mit dem Server hinzu](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [Formatoptionen für Downloads](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [Einfache Dateiupload-Tool](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6)  
  
-   [Anzeigen und Durchsuchen von freigegebenen digitalen Medien](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_7)  

  
##  <a name="BKMK_1"></a>Übersicht über digitale Medien  
 Digitale Medien sind Audio-, Video- und fotoinhalte, die (Digital komprimiert) codiert wurden. Codieren von Inhalten werden Audio- und video-Eingabe für eine digitale Mediendatei, z. B. eine Windows Media-Datei konvertieren. Nach digitale Medien codiert ist, es kann leicht bearbeitet, verteilt, und von Computern wiedergegeben und über Computernetzwerke übertragen.  
  
 Beispiele für digitale Medien sind: Windows Media Audio (WMA), Windows Media Video (WMV), MP3, JPEG und AVI. Weitere Informationen zu den digitalen Medientypen, die von Windows Media Player unterstützt werden, finden Sie unter [von Windows Media Player unterstützte Dateitypen](https://support.microsoft.com/kb/316992).  
  
### <a name="why-would-i-want-to-stream-my-digital-media"></a>Warum würde ich möchte meine digitalen Medien streamen?  
 Viele Benutzer speichern Musik, Videos und Bilder in freigegebenen Ordnern in Windows Server Essentials. Manchmal, wenn Sie möchten, vielleicht folgende:  
  
-   **Sehen Sie sich Videos**. Der Server kann zum Speichern und streamen umfangreiche Videosammlungen und TV-Aufzeichnungen auf Ihrem Computer oder andere Wiedergabegeräte Geräte in Ihrem Netzwerk. Sie können Videos auf einer Xbox 360 oder auf einem Computer mit Windows Media Player streamen.  
  
-   **Wiedergeben von Musik**. Wenn Sie für die Medienfreigabe aktivieren der **Musik** freigegebenen Ordner können Sie Ihre Musik zugreifen, von Geräten, die Windows Media Connect unterstützen. Sie müssen nicht aktivieren oder konfigurieren alle Benutzerkonten aus Streamen der **Musik** freigegebenen Ordner nach der Freigabe aktiviert ist.  
  
-   **Präsentieren Sie Diashows**. Sie können Ihre digitalen Fotos im Speichern der **Fotos** freigegebenen Ordner auf dem Server, und klicken Sie dann greifen sie von jedem Computer oder von einer Xbox 360, der mit einem Fernsehgerät bei Ihnen zuhause oder im Büro verbunden ist. Sie können fotodiashows ansehen und Ihr TV in einen großen Bilderrahmen verwandeln.  
  
### <a name="sharing-copy-protected-media"></a>Freigeben kopiergeschützter Medien  
  Windows Server Essentials unterstützt freigeben kopiergeschützter Medien nicht. Dazu gehört auch Musik, die über eine online-Music Store erworben wird.  
  
 Kopiergeschützte Medien können wiedergegeben werden, nur auf dem Computer oder Gerät, das Sie zum Kaufen verwendet. Kopierschutz verhindert, dass Sie auf mehrere Computer oder Gerät, das Wiedergeben von Medien, auch wenn Sie das Medium auf den Server kopieren und dort wiedergeben. Allerdings können das kopiergeschützte Medium auf Windows Server Essentials speichern und weiterhin auf dem Computer oder Gerät, mit dem Sie zum Kaufen die Medien wiedergeben.  
  
##  <a name="BKMK_2"></a>Wiedergeben Sie und freigeben Sie digitaler Medien  
 Nachdem Sie Ihr Netzwerk eingerichtet und Ihre Computer und Mediengeräte erfolgreich mit dem Servernetzwerk verbinden, können Sie für alle digitalen Mediendateien suchen, die Sie speichern und teilen Sie auf dem Server.  
  
> [!NOTE]
>  Eine aktuelle Liste der digital Media Player/Empfänger Geräte, die mit Windows Server Essentials kompatibel sind, finden Sie unter der [Windows-Kompatibilitätscenter](https://www.microsoft.com/windows/compatibility/CompatCenter/Home).  
  
 Sie können eine der folgenden Methoden zum Suchen und Wiedergeben von digitalen Mediendateien, die auf dem Server gespeichert sind:  
  

-   [Suchen und Wiedergeben von Mediendateien in Windows Server Essentials von einem Computer oder digital Media-Player im Netzwerk](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.1)  
  
-   [Senden von Mediendateien in Windows Server Essentials an Windows Media Player, Xbox 360, oder einen digital Media-Player im Netzwerk](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_SendToDevice)  

-   [Suchen und Wiedergeben von Mediendateien in Windows Server Essentials von einem Computer oder digital Media-Player im Netzwerk](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.1)  
  
-   [Senden von Mediendateien in Windows Server Essentials an Windows Media Player, Xbox 360, oder einen digital Media-Player im Netzwerk](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_SendToDevice)  

  
###  <a name="BKMK_2.1"></a>Suchen und Wiedergeben von Mediendateien in Windows Server Essentials von einem Computer oder digital Media-Player im Netzwerk  
 Wenn Ihr Gerät mit dem Windows Server Essentials-Netzwerk hinzugefügt wird, können Sie suchen und Wiedergeben von digitalen Mediendateien in einer der folgenden Methoden:  
  

-   [Suchen und Wiedergeben von Mediendateien auf einem Computer mit Windows Media Center](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_WMC)  
  
-   [Suchen und Wiedergeben von Mediendateien auf einem Computer, auf der Windows ausgeführt wird, mithilfe von Windows Media Player](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_MWP)  
  
-   [Suchen und Wiedergeben von Mediendateien mit der Xbox 360](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_Xbox)  
  
-   [Suchen und Wiedergeben von Mediendateien mit anderen digital Media-Player oder Empfänger, die mit Windows Server Essentials kompatibel sind](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_Other)  
  
-   [Suchen und Wiedergeben von Mediendateien mit dem Feature freigegebene Ordner über das Launchpad](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_SharedFolders)  
  
-   [Suchen Sie und wiedergeben Sie freigegebener Medien mithilfe von Remotewebzugriff](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_RWA2)  

-   [Suchen und Wiedergeben von Mediendateien auf einem Computer mit Windows Media Center](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_WMC)  
  
-   [Suchen und Wiedergeben von Mediendateien auf einem Computer, auf der Windows ausgeführt wird, mithilfe von Windows Media Player](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_MWP)  
  
-   [Suchen und Wiedergeben von Mediendateien mit der Xbox 360](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_Xbox)  
  
-   [Suchen und Wiedergeben von Mediendateien mit anderen digital Media-Player oder Empfänger, die mit Windows Server Essentials kompatibel sind](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_Other)  
  
-   [Suchen und Wiedergeben von Mediendateien mit dem Feature freigegebene Ordner über das Launchpad](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_SharedFolders)  
  
-   [Suchen Sie und wiedergeben Sie freigegebener Medien mithilfe von Remotewebzugriff](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_RWA2)  

  
####  <a name="BKMK_WMC"></a>Suchen und Wiedergeben von Mediendateien auf einem Computer mit Windows Media Center  
  
1.  Klicken Sie auf **starten**, klicken Sie auf **alle Programme**, und klicken Sie dann auf **Windows Media Center**.  
  
2.  Auf der **Windows Media Center** Seite einen Bildlauf zum gesuchten Medientyp, und klicken Sie auf die Medienbibliothek.  
  
3.  Suchen Sie manuell nach der Datei, die Sie interessiert sind, oder klicken Sie auf **Suche** und geben Sie den Namen der Datei gesucht werden soll.  
  
4.  Klicken Sie auf das Bild der Mediendatei zum Anzeigen oder die Datei wiedergegeben werden.  
  
####  <a name="BKMK_MWP"></a>Suchen und Wiedergeben von Mediendateien auf einem Computer, auf der Windows ausgeführt wird, mithilfe von Windows Media Player  
  
-   Öffnen Sie den Computer oder Mediengerät, **Windows Media Player**, und suchen Sie die Medienbibliothek.  
  
    > [!NOTE]
    >  Die Schritteder Suche variieren je nach Version von Windows Media Player, die Sie verwenden. Ausführliche Informationen finden Sie in der Hilfe für Ihre Version.  
  
####  <a name="BKMK_Xbox"></a>Suchen und Wiedergeben von Mediendateien mit der Xbox 360  
  
1.  Verbinden Sie eine kabelgebundene oder drahtlose Verbindung mit Xbox 360-Konsole mit Ihrem Heimnetzwerk.  
  
2.  Aktivieren Sie auf dem Computer, auf der Windows Server Essentials ausgeführt wird, auf die Freigabe von Medien. Weitere Informationen finden Sie im Thema [aktivieren Medienstreaming aktivieren oder deaktivieren](../manage/Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4).  
  
3.  Zum Wiedergeben von digitalen Mediendateien, die mit der Xbox 360-Konsole:  
  
    1.  Wechseln Sie zu **meine Xbox**, und wählen Sie dann **Videobibliothek**, **Musikbibliothek**, oder **Bildbibliothek**je nach Typ des Mediums, die Sie anzeigen oder wiedergeben möchten.  
  
    2.  Wählen Sie den Namen des Servers.  
  
        > [!NOTE]
        >  Wenn Sie der Namen des Servers nicht aufgeführt ist, wählen Sie **Computer**, und klicken Sie dann auf **Testverbindung**.  
  
    3.  Durchsuchen Sie die Dateiliste, und wählen Sie das Element, das Sie wiedergeben möchten.  
  
####  <a name="BKMK_Other"></a>Suchen und Wiedergeben von Mediendateien mit anderen digital Media-Player oder Empfänger, die mit Windows Server Essentials kompatibel sind  
  
1.  Wechseln Sie zu der [Windows-Kompatibilitätscenter](https://www.microsoft.com/windows/compatibility/CompatCenter/Home) und stellen Sie sicher, dass Ihr digital Media-Player oder Empfänger in der Liste der kompatiblen Geräte angezeigt wird.  
  
2.  Da Suchfeld Schrittedigital Media-Player, die Sie verwenden abhängen, finden Sie in der Hilfe des Geräts für die ausführliche Anweisungen.  
  
####  <a name="BKMK_SharedFolders"></a>Suchen und Wiedergeben von Mediendateien mit dem Feature freigegebene Ordner über das Launchpad  
  
1.  Melden Sie sich der Windows Server Essentials-Launchpad.  
  
2.  Klicken Sie auf dem Launchpad auf **freigegebene Ordner**. Windows Explorer-Fenster wird geöffnet und zeigt die freigegebenen Ordner auf dem Server.  
  
3.  In der **Suche** Geben Sie den Namen einer Mediendatei. Die Ergebnisse Ihrer Suchabfrage werden angezeigt.  
  
    > [!NOTE]
    >  Optional können Sie auch einen freigegebenen Ordner, um den Ordnerinhalt zu durchsuchen doppelklicken.  
  
####  <a name="BKMK_RWA2"></a>Suchen Sie und wiedergeben Sie freigegebener Medien mithilfe von Remotewebzugriff  
  
1.  Melden Sie sich bei Remotewebzugriff.  
  
2.  Klicken Sie auf **freigegebene Ordner**. Die **freigegebene Ordner** Abschnittder Webseite zeigt eine Liste der freigegebenen Ordner auf dem Server.  
  
3.  Doppelklicken Sie auf einen Ordner, um den Inhalt des Ordners anzuzeigen.  
  
###  <a name="BKMK_SendToDevice"></a>Senden von Mediendateien in Windows Server Essentials an Windows Media Player, Xbox 360, oder einen digital Media-Player im Netzwerk  
 Verwendung **Windows Media Player** für die Mediendatei zu suchen, die Sie möchten. Mit der rechten Maustaste der Mediendatei, und klicken Sie dann auf **wiedergeben** die Mediendatei an ein Mediengerät zu senden.  
  
##  <a name="BKMK_3"></a>Wiedergeben freigegebener digitaler Mediendateien von einem Remotestandort aus  
 Sie können Ihre Mediendateien wiedergeben, wenn Sie nicht das Windows Server Essentials-Netzwerk sind, mithilfe von Remotewebzugriff. Sie können ein Mobiltelefon, einen Remotecomputer oder einen digital Media-Player verwenden, suchen und Wiedergeben der freigegebenen Mediendateien, die auf dem Server gespeichert.  
  
#### <a name="to-play-shared-media-files-when-you-are-away-from-the-network"></a>Freigegebene Mediendateien wiedergeben, wenn Sie nicht im Netzwerk sind  
  
1.  Öffnen Sie einen Internetbrowser.  
  
2.  Wechseln Sie zu Ihrer Website für Remotewebzugriff zugreifen. Typ **https://<YourDomainName\>/remote** in die Adressleiste des Internetbrowsers ein, und drücken Sie dann die EINGABETASTE.  
  
    > [!NOTE]
    >  *< YourDomainName\ >* ist ein Platzhalter. Es werden ein Name, der an den Server eindeutig ist, damit die eingegebene Adresse aussieht **https://contoso.com/remote**. Wenn Sie den Namen Ihrer Domäne nicht kennen, bitten Sie den Administrator, die den Domänennamen ausgewählt haben, wenn der RAS-Funktionen auf dem Server festgelegt wurde. Weitere Informationen finden Sie unter [Turn on Remote Web Access](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_TurnOnRWA).  
  
3.  Klicken Sie auf die Remote Web Access-Anmeldeseite Geben Sie Ihren Benutzernamen und Kennwort, und klicken Sie dann auf den Pfeil.  
  
4.  Verwenden Sie die gewählte Methode, die Sie für die Mediendatei zu suchen, die Sie abspielen möchten gerne.  
  
    > [!NOTE]

    >  Informationen über die verschiedenen Suchmethoden finden Sie unter [suchen und Wiedergabe von Mediendateien in Windows Server Essentials von einem Computer oder digital Media-Player im Netzwerk](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.1).  

    >  Informationen über die verschiedenen Suchmethoden finden Sie unter [suchen und Wiedergabe von Mediendateien in Windows Server Essentials von einem Computer oder digital Media-Player im Netzwerk](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.1).  

  
5.  Wenn der Name der Mediendatei angezeigt wird, klicken Sie auf den Namen der Datei, um das Medium wiederzugeben.  
  
##  <a name="BKMK_4"></a>Fügen Sie digitaler Mediendateien mit dem Server hinzu  

 Der Serveradministrator kann digitale Medien in der Medienbibliothek freigegebenen Ordner durch den Zugriff auf dem Server direkt oder über die Remote Web Access-Website auf dem Dashboard anmelden hinzufügen. Andere Benutzer können Mediendateien mit dem Server hinzufügen, indem Sie mit der **freigegebene Ordner** Verbindung auf dem Launchpad mithilfe der Remotewebzugriff-Website oder mithilfe der My Server-app für Windows Phone. Informationen zum Wiedergeben von Medien finden Sie unter [wiedergeben und Freigeben digitaler Medien](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2).  

 Der Serveradministrator kann digitale Medien in der Medienbibliothek freigegebenen Ordner durch den Zugriff auf dem Server direkt oder über die Remote Web Access-Website auf dem Dashboard anmelden hinzufügen. Andere Benutzer können Mediendateien mit dem Server hinzufügen, indem Sie mit der **freigegebene Ordner** Verbindung auf dem Launchpad mithilfe der Remotewebzugriff-Website oder mithilfe der My Server-app für Windows Phone. Informationen zum Wiedergeben von Medien finden Sie unter [wiedergeben und Freigeben digitaler Medien](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2).  

  
> [!NOTE]
>  Sie können auch mithilfe der My Server-app für Windows Phone-Mediendateien mit dem Server hochladen. Sie können die My Server-app aus dem [Windows Phone Store](http://www.windowsphone.com/store/app/my-server/6c2f98d5-6fcf-4e1d-b8b1-cde62ea1a94a). Weitere Informationen zur My Server-App für Windows Phone finden Sie im Blogbeitrag [My Server Phone-App für Windows Server Essentials](http://blogs.technet.com/b/sbs/archive/2012/09/18/my-server-phone-app-for-windows-server-2012-essentials.aspx).  
  
#### <a name="to-add-digital-media-files-to-shared-folders-on-the-server"></a>Digitale Mediendateien freigegebenen Ordnern auf dem Server hinzu  
  
1.  Verwenden Sie eine der folgenden Methoden, um mit dem Server anmelden:  
  

    1.  Informationen zur Anmeldung beim Remotewebzugriff finden Sie unter [Use Remote Web Access](Use-Remote-Web-Access-in-Windows-Server-Essentials.md).  

    1.  Informationen zur Anmeldung beim Remotewebzugriff finden Sie unter [Use Remote Web Access](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md).  

  
    2.  Informationen zum Anmelden mit Launchpad finden Sie unter [Launchpad Übersicht](../manage/Overview-of-the-Launchpad-in-Windows-Server-Essentials.md).  
  
2.  Suchen Sie nach, und klicken Sie auf den Ordner für das Medium, die Sie hinzufügen möchten.  
  
3.  Kopieren und einfügen oder Drag-and-Drop Mediendateien, die Sie auf den entsprechenden hinzufügen möchten für freigegebene Ordner auf dem Server.  
  
##  <a name="BKMK_5"></a>Formatoptionen für Downloads  
 Es gibt zwei Optionen zum Herunterladen von Dateien. Diese Optionen stehen nur, wenn Sie mehrere Dateien oder einen Ordner auf einem Windows-basierten Computer herunterladen.  
  
 Wählen Sie die folgende Option, die Ihre downloadanforderungen:  
  
-   **Komprimierte ZIP-Datei (.zip)**  
  
     Komprimieren einer Datei wird eine komprimierte Version der Datei, die kleiner als die ursprüngliche Datei wird erstellt. Die komprimierte Version der Datei hat die Erweiterung ZIP-Datei. Dateitypen, die durch das Komprimieren von sind sind textorientierte Dateitypen (z.B. txt-, DOC- und xls) und grafische Dateien, die nicht komprimierte Dateitypen (z.B. bmp). Einige Grafikdateien wie JPG- und GIF-Dateien nutzen bereits die Komprimierung und die Dateigröße durch das Komprimieren nur sehr wenig. Darüber hinaus wird ein Worddokument, das viele Grafiken enthält nicht so viel wie ein Dokument reduziert, die hauptsächlich Text.  
  
    > [!NOTE]
    >  Diese Option bietet eingeschränkte Unterstützung für internationale Dateinamen.  
  
-   **Selbstextrahierende ausführbare Datei (.exe)**  
  
     Eine selbstextrahierende ausführbare Datei ist eine Datei, die Sie herunterladen können, die das Dekomprimierungsprogramm (ausführbare Datei) mit den komprimierten Dateien kombiniert. Wenn Sie das ausführbare Programm ausführen, dekomprimiert es automatisch die komprimierten Dateien. Dies ist eine gebräuchliche Methode zum Verteilen von komprimierter Daten ohne Rücksicht auf, ob der Empfänger die nötige dekomprimierungshilfsprogramm verfügen muss.  
  
    > [!NOTE]
    >  Diese Option unterstützt Unicode-Zeichen.  
  
 Vor Beginn des eigentlichen Downloads wird die .exe oder ZIP-Datei erstellt. Je nach Anzahl der Dateien und die Gesamtgröße der Dateien heruntergeladen werden kann dies einige Minuten dauern. Nachdem die Downloaddatei erstellt wurde, erfolgt das Herunterladen der das im Hintergrund. Dadurch können Sie weiterarbeiten, während der Downloadvorgang ausgeführt wird.  
  
##  <a name="BKMK_6"></a>Einfache Dateiupload-Tool  
 Die Tool "einfacher Dateiupload" optimiert das Hochladen von Dateien auf dem Windows Server Essentials-Server. Sie können beliebig viele Dateien, die das Tool "einfacher Dateiupload", und klicken Sie dann auf die freigegebenen Ordner auf dem Windows Server Essentials-Server in einem einzigen Batch hochladen hinzufügen. Weitere Informationen finden Sie im Blogbeitrag [Grundlegendes zur Remote Web Access Dateifreigabe](http://blogs.technet.com/b/sbs/archive/2012/04/19/understanding-remote-web-access-file-sharing.aspx).  
  
##  <a name="BKMK_7"></a>Anzeigen und Durchsuchen von freigegebenen digitalen Medien  
 Sie können anzeigen oder Durchsuchen Sie die Ressourcen entweder mithilfe des Dashboards, das Launchpad, die Remote Web Access-Website oder My Server-App für Windows Phone.  
  
#### <a name="to-view-and-browse-shared-media-from-the-dashboard"></a>Zum Anzeigen und Durchsuchen Sie freigegebene Medien über das Dashboard  
  
1.  Öffnen Sie das Server-Dashboard.  
  
2.  Klicken Sie auf der Hauptnavigationsleiste auf **Speicher**.  
  
3.  Klicken Sie auf die **Serverordner** Registerkarte. Eine Liste der Serverordner wird angezeigt.  
  
4.  Doppelklicken Sie auf einen Ordner, um den Inhalt des Ordners anzuzeigen.  
  
#### <a name="to-view-and-browse-shared-media-using-the-launchpad-from-a-network-computer"></a>Zum Anzeigen und durchsuchen können Sie freigegebene Medien über das Launchpad eines Netzwerkcomputers  
  
1.  Melden Sie sich das Launchpad.  
  
2.  Klicken Sie auf **freigegebene Ordner**. Windows-Explorer wird geöffnet und zeigt eine Liste der freigegebenen Ordner auf dem Server.  
  
3.  Doppelklicken Sie auf einen Ordner, um den Inhalt des Ordners anzuzeigen.  
  
#### <a name="to-view-and-browse-shared-media-using-remote-web-access"></a>Zum Anzeigen und durchsuchen können Sie freigegebene Medien über Remotewebzugriff  
  
1.  Melden Sie sich bei Remotewebzugriff.  
  
2.  Klicken Sie auf **freigegebene Ordner**. Die **freigegebene Ordner** Abschnittder Webseite zeigt eine Liste der freigegebenen Ordner auf dem Server.  
  
3.  Doppelklicken Sie auf einen Ordner, um den Inhalt des Ordners anzuzeigen.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten von digitalen Medien](../manage/Manage-Digital-Media-in-Windows-Server-Essentials.md)  
  

-   [Herstellen einer Verbindung](Get-Connected-in-Windows-Server-Essentials.md)  
  
-   [Verwenden von freigegebenen Ordnern](Use-Shared-Folders-in-Windows-Server-Essentials.md)  
  
-   [Remote-Arbeit](Work-Remotely-in-Windows-Server-Essentials.md)

-   [Herstellen einer Verbindung](../use/Get-Connected-in-Windows-Server-Essentials.md)  
  
-   [Verwenden von freigegebenen Ordnern](../use/Use-Shared-Folders-in-Windows-Server-Essentials.md)  
  
-   [Remote-Arbeit](../use/Work-Remotely-in-Windows-Server-Essentials.md)

