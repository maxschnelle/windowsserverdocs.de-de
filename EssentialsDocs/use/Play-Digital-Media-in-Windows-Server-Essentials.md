---
title: Wiedergeben von digitalen Medien in Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f570492-ee21-471b-92c1-3fd9bfb84f55
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 168569fc6ce7937090a45bf9e7c68353f8b62714
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80310974"
---
# <a name="play-digital-media-in-windows-server-essentials"></a>Wiedergeben von digitalen Medien in Windows Server Essentials

>Gilt für: Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Digitale Medien sind Audio-, Video- und Fotoinhalte, die digital komprimiert wurden.  Windows Server Essentials ermöglicht Netzwerkcomputern und einigen digitalen Mediengeräten im Netzwerk die Wiedergabe digitaler Mediendateien, die auf dem Server gespeichert sind.  
  
 Die folgenden Themen enthalten Informationen zum Zugreifen auf und Wiedergeben digitaler Mediendateien, die in Windows Server Essentials gespeichert sind:  
  

-   [Übersicht über digitale Medien](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Wiedergeben und Freigeben digitaler Medien](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Wiedergeben frei gegebener digitaler Mediendateien von einem Remote Standort aus](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [Hinzufügen digitaler Mediendateien zum Server](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [Download Formatoptionen](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [Einfaches Tool zum Hochladen von Dateien](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6)  
  
-   [Anzeigen und Durchsuchen von freigegebenen digitalen Medien](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_7)  

-   [Übersicht über digitale Medien](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Wiedergeben und Freigeben digitaler Medien](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Wiedergeben frei gegebener digitaler Mediendateien von einem Remote Standort aus](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [Hinzufügen digitaler Mediendateien zum Server](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [Download Formatoptionen](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [Einfaches Tool zum Hochladen von Dateien](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6)  
  
-   [Anzeigen und Durchsuchen von freigegebenen digitalen Medien](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_7)  

  
##  <a name="digital-media-overview"></a><a name="BKMK_1"></a>Übersicht über digitale Medien  
 Digitale Medien sind Audio-, Video- und Fotoinhalte, die codiert (digital komprimiert) wurden. Beim Codieren von Inhalten werden Audio- und Videoeingaben in eine digitale Mediendatei, z. B. eine Windows Media-Datei, konvertiert. Nach der Codierung können digitale Medien einfach bearbeitet, verteilt, von Computern wiedergegeben und über Computernetzwerke übertragen werden.  
  
 Beispiele für digitale Medien sind: Windows Media Audio (WMA), Windows Media Video (WMV), MP3, JPEG und AVI. Informationen zu den digitalen Medientypen, die von Windows Media Player unterstützt werden, finden Sie unter [Von Windows Media Player unterstützte Dateitypen](https://support.microsoft.com/kb/316992).  
  
### <a name="why-would-i-want-to-stream-my-digital-media"></a>Warum sollte ich meine digitalen Medien streamen?  
 Viele Benutzer speichern Musik, Videos und Bilder in freigegebenen Ordnern in Windows Server Essentials. Sie haben verschiedene Möglichkeiten, Medien zu nutzen:  
  
-   **Videos ansehen**. Der Server kann zum Speichern und Streamen umfangreicher Videosammlungen und TV-Aufzeichnungen auf Ihre Computer oder andere Wiedergabegeräte im Netzwerk genutzt werden. Mithilfe von Windows Media Player können Sie Videos auf eine Xbox 360 oder auf einen Computer streamen.  
  
-   **Musik wiedergeben**. Wenn Sie die Medienfreigabe für den freigegebenen Ordner **Musik** aktivieren, können Sie über Geräte, die Windows Media Connect unterstützen, auf Ihre Musik zugreifen. Nachdem die Freigabe aktiviert wurde, müssen Sie keine Benutzerkonten aktivieren oder konfigurieren, um Musik aus dem freigegebenen Ordner **Musik** zu streamen.  
  
-   **Fotodiashow präsentieren**. Sie können Ihre digitalen Fotos im freigegebenen Ordner **Fotos** auf dem Server speichern und anschließend von jedem Computer oder von einer Xbox 360 darauf zugreifen, die mit einem Fernsehgerät bei Ihnen zuhause oder im Büro verbunden ist. Sie können Fotodiashows ansehen und Ihr Fernsehgerät praktisch in einen großen Bilderrahmen verwandeln.  
  
### <a name="sharing-copy-protected-media"></a>Freigeben kopiergeschützter Medien  
  Windows Server Essentials unterstützt das Freigeben von kopiergeschützten Medien nicht. Dazu gehört auch Musik, die über einen Online-Music Store gekauft wurde.  
  
 Kopiergeschützte Medien können nur auf dem Computer oder Gerät wiedergegeben werden, über den bzw. das sie erworben wurden. Der Kopierschutz verhindert, dass Sie Medien auf mehr als einem Computer oder Gerät abspielen, auch wenn Sie das Medium auf den Server kopieren und dort wiedergeben. Sie können das kopiergeschützte Medium jedoch in Windows Server Essentials speichern und die Medien weiterhin auf dem Computer oder Gerät wiedergeben, den bzw. das Sie für den Erwerb verwendet haben.  
  
##  <a name="play-and-share-digital-media"></a><a name="BKMK_2"></a>Wiedergeben und Freigeben digitaler Medien  
 Nachdem Sie Ihr Netzwerk eingerichtet und die Computer und Mediengeräte erfolgreich mit dem Servernetzwerk verbunden haben, können Sie digitale Mediendateien suchen, die Sie auf dem Server speichern und freigeben.  
  
> [!NOTE]
>  Eine aktuelle Liste der mit Windows Server Essentials kompatiblen Digital Media-Player/Receive-Geräte finden Sie im [Windows-Kompatibilitäts Center](https://www.microsoft.com/windows/compatibility/CompatCenter/Home).  
  
 Sie können auf dem Server gespeicherte digitale Mediendateien auf folgende Weisen suchen und wiedergeben:  
  

-   [Suchen und Wiedergeben von Mediendateien in Windows Server Essentials auf einem Computer oder Digital Media-Player im Netzwerk](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.1)  
  
-   [Senden von Mediendateien in Windows Server Essentials an Windows Media Player, Xbox 360 oder an einen vernetzten Digital Media-Player im Netzwerk](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_SendToDevice)  

-   [Suchen und Wiedergeben von Mediendateien in Windows Server Essentials auf einem Computer oder Digital Media-Player im Netzwerk](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.1)  
  
-   [Senden von Mediendateien in Windows Server Essentials an Windows Media Player, Xbox 360 oder an einen vernetzten Digital Media-Player im Netzwerk](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_SendToDevice)  

  
###  <a name="search-for-and-play-media-files-on-windows-server-essentials-from-a-computer-or-digital-media-player-on-the-network"></a><a name="BKMK_2.1"></a>Suchen und Wiedergeben von Mediendateien in Windows Server Essentials auf einem Computer oder Digital Media-Player im Netzwerk  
 Wenn Ihr Gerät mit dem Windows Server Essentials-Netzwerk verbunden ist, können Sie digitale Mediendateien auf folgende Weise suchen und wiedergeben:  
  

-   [Suchen und Wiedergeben von Mediendateien auf einem Computer, auf dem Windows Media Center ausgeführt wird](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_WMC)  
  
-   [Suchen und Wiedergeben von Mediendateien auf einem Computer unter Windows mithilfe von Windows Media Player](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_MWP)  
  
-   [Suchen und Wiedergeben von Mediendateien mithilfe von Xbox 360](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_Xbox)  
  
-   [Suchen und Wiedergeben von Mediendateien mit anderen Digital Media-Playern oder Empfängern, die mit Windows Server Essentials kompatibel sind](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_Other)  
  
-   [Suchen und Wiedergeben von Mediendateien mit der Funktion "freigegebene Ordner" des Launchpad](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_SharedFolders)  
  
-   [Suchen und wiedergeben frei gegebener Medien mithilfe von Remote Webzugriff](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_RWA2)  

-   [Suchen und Wiedergeben von Mediendateien auf einem Computer, auf dem Windows Media Center ausgeführt wird](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_WMC)  
  
-   [Suchen und Wiedergeben von Mediendateien auf einem Computer unter Windows mithilfe von Windows Media Player](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_MWP)  
  
-   [Suchen und Wiedergeben von Mediendateien mithilfe von Xbox 360](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_Xbox)  
  
-   [Suchen und Wiedergeben von Mediendateien mit anderen Digital Media-Playern oder Empfängern, die mit Windows Server Essentials kompatibel sind](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_Other)  
  
-   [Suchen und Wiedergeben von Mediendateien mit der Funktion "freigegebene Ordner" des Launchpad](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_SharedFolders)  
  
-   [Suchen und wiedergeben frei gegebener Medien mithilfe von Remote Webzugriff](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_RWA2)  

  
####  <a name="search-for-and-play-media-files-from-a-computer-that-is-running-windows-media-center"></a><a name="BKMK_WMC"></a>Suchen und Wiedergeben von Mediendateien auf einem Computer, auf dem Windows Media Center ausgeführt wird  
  
1.  Klicken Sie auf **Start**, **Alle Programme** und dann auf **Windows Media Center**.  
  
2.  Führen Sie auf der Seite **Windows Media Center** einen Bildlauf zum gesuchten Medientyp durch, und klicken Sie auf die Medienbibliothek.  
  
3.  Suchen Sie manuell nach der gewünschten Datei, oder klicken Sie auf **Suchen**, und geben Sie den Namen der gesuchten Datei ein.  
  
4.  Klicken Sie auf das Bild der Mediendatei, um sie anzuzeigen oder wiederzugeben.  
  
####  <a name="search-for-and-play-media-files-from-a-computer-that-is-running-windows-by-using-windows-media-player"></a><a name="BKMK_MWP"></a>Suchen und Wiedergeben von Mediendateien auf einem Computer unter Windows mithilfe von Windows Media Player  
  
-   Öffnen Sie auf dem Computer oder Mediengerät **Windows Media Player**, und suchen Sie die Medienbibliothek.  
  
    > [!NOTE]
    >  Die Schritte der Suche variieren je nach der verwendeten Version von Windows Media Player. Ausführliche Informationen finden Sie in der Hilfe zu Ihrer Version.  
  
####  <a name="search-for-and-play-media-files-by-using-xbox-360"></a><a name="BKMK_Xbox"></a>Suchen und Wiedergeben von Mediendateien mithilfe von Xbox 360  
  
1.  Verbinden Sie die Xbox 360-Konsole über eine kabelgebundene oder kabellose Verbindung mit Ihrem Heimnetzwerk.  
  
2.  Aktivieren Sie auf dem Computer, auf dem Windows Server Essentials ausgeführt wird, die Medien Freigabe. Weitere Informationen finden Sie im Thema zum Aktivieren [oder Deaktivieren des Medien Streamings](../manage/Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4).  
  
3.  So geben Sie digitale Mediendateien mit der Xbox 360-Konsole wieder:  
  
    1.  Wechseln Sie zu **Meine Xbox**, und wählen Sie dann abhängig vom Medientyp, den Sie anzeigen oder wiedergeben möchten, **Videobibliothek**, **Musikbibliothek** oder **Bildbibliothek** aus.  
  
    2.  Wählen Sie den Namen des Servers aus.  
  
        > [!NOTE]
        >  Wenn der Servername nicht aufgeführt ist, wählen Sie **Computer**, und klicken Sie dann auf **Verbindung testen**.  
  
    3.  Durchsuchen Sie die Dateiliste, und wählen Sie das Element aus, das Sie wiedergeben möchten.  
  
####  <a name="search-for-and-play-media-files-by-using-other-digital-media-players-or-receivers-that-are-compatible-with-windows-server-essentials"></a><a name="BKMK_Other"></a>Suchen und Wiedergeben von Mediendateien mit anderen Digital Media-Playern oder Empfängern, die mit Windows Server Essentials kompatibel sind  
  
1.  Wechseln Sie zum [Windows-Kompatibilitätscenter](https://www.microsoft.com/windows/compatibility/CompatCenter/Home) , und stellen Sie sicher, dass Ihr Digital Media-Player oder Empfänger für digitale Medien in der Liste kompatibler Geräte aufgeführt wird.  
  
2.  Die Suchschritte variieren abhängig vom verwendeten Digital Media-Player. Ausführliche Anweisungen finden Sie in der Hilfe zu Ihrem Gerät.  
  
####  <a name="search-for-and-play-media-files-by-using-the-shared-folders-feature-of-the-launchpad"></a><a name="BKMK_SharedFolders"></a>Suchen und Wiedergeben von Mediendateien mit der Funktion "freigegebene Ordner" des Launchpad  
  
1.  Melden Sie sich beim Windows Server Essentials-Launchpad an.  
  
2.  Klicken Sie im Launchpad auf **Freigegebene Ordner**. Ein Windows-Explorer-Fenster wird geöffnet und zeigt die freigegebenen Ordner auf dem Server an.  
  
3.  Geben Sie im Feld **Suchen** den Namen einer Mediendatei ein. Die Ergebnisse Ihrer Suchabfrage werden angezeigt.  
  
    > [!NOTE]
    >  Optional können Sie auch auf einen freigegebenen Ordner doppelklicken, um den Ordnerinhalt zu durchsuchen.  
  
####  <a name="search-for-and-play-shared-media-by-using-remote-web-access"></a><a name="BKMK_RWA2"></a>Suchen und wiedergeben frei gegebener Medien mithilfe von Remote Webzugriff  
  
1.  Melden Sie sich bei Remotewebzugriff an.  
  
2.  Klicken Sie auf **Freigegebene Ordner**. Im Abschnitt **Freigegebene Ordner** der Webseite wird eine Liste freigegebener Ordner auf dem Server angezeigt.  
  
3.  Doppelklicken Sie auf einen Ordner, um dessen Inhalt anzuzeigen.  
  
###  <a name="send-media-files-on-windows-server-essentials-to-windows-media-player-xbox-360-or-to-a-networked-digital-media-player-in-the-network"></a><a name="BKMK_SendToDevice"></a>Senden von Mediendateien in Windows Server Essentials an Windows Media Player, Xbox 360 oder an einen vernetzten Digital Media-Player im Netzwerk  
 Verwenden Sie **Windows Media Player**, um die gewünschte Mediendatei zu suchen. Klicken Sie mit der rechten Maustaste auf die Mediendatei, und klicken Sie dann auf **Wiedergeben auf**, um die Mediendatei an ein Mediengerät im Netzwerk zu senden.  
  
##  <a name="play-shared-digital-media-files-from-a-remote-location"></a><a name="BKMK_3"></a>Wiedergeben frei gegebener digitaler Mediendateien von einem Remote Standort aus  
 Sie können Ihre Mediendateien wiedergeben, wenn Sie das Windows Server Essentials-Netzwerk mithilfe von Remote Webzugriff nicht mehr verwenden. Zum Suchen und Wiedergeben der auf Ihrem Server gespeicherten freigegebenen Mediendateien können Sie ein Mobiltelefon, einen Remotecomputer oder einen Digital Media-Player verwenden.  
  
#### <a name="to-play-shared-media-files-when-you-are-away-from-the-network"></a>So geben Sie freigegebene Mediendateien wieder, wenn Sie keinen Zugriff auf Ihr Netzwerk haben  
  
1. Öffnen Sie einen Internetbrowser.  
  
2. Wechseln Sie zur Website für Remotewebzugriff. Geben Sie in der Adressleiste des Internet Browsers **https://< yourDomainName\>/Remote** ein, und drücken Sie dann die EINGABETASTE.  
  
   > [!NOTE]
   >  *< yourDomainName\>* ist ein Platzhalter. Dabei handelt es sich um einen eindeutigen Namen für Ihren Server, sodass die von Ihnen Typisierungs Adresse wie **https://contoso.com/remote** aussehen wird. Wenn Sie den Namen der Domäne nicht kennen, erkundigen Sie sich beim Administrator, der den Domänennamen bei der Einrichtung der Remotezugriffsfunktion auf dem Server ausgewählt hat. Weitere Informationen finden Sie unter [Aktivieren von Remotewebzugriff](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_TurnOnRWA).  
  
3. Geben Sie auf der Anmeldeseite für den Remotewebzugriff Ihren Benutzernamen und Ihr Kennwort ein, und klicken Sie dann auf den Pfeil.  
  
4. Suchen Sie die wiederzugebende Mediendatei auf die für Sie geeignete Weise.  
  
   > [!NOTE]
   > 
   >  Informationen zu den verschiedenen Suchmethoden finden Sie unter [Suchen und Wiedergeben von Mediendateien in Windows Server Essentials auf einem Computer oder Digital Media-Player im Netzwerk](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.1).  
   > 
   >  Informationen zu den verschiedenen Suchmethoden finden Sie unter [Suchen und Wiedergeben von Mediendateien in Windows Server Essentials auf einem Computer oder Digital Media-Player im Netzwerk](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.1).  

  
5. Sobald der Name der Mediendatei angezeigt wird, klicken Sie auf den Dateinamen, um das Medium wiederzugeben.  
  
##  <a name="add-digital-media-files-to-the-server"></a><a name="BKMK_4"></a>Hinzufügen digitaler Mediendateien zum Server  

 Der Server Administrator kann freigegebenen Ordnern in der Medienbibliothek digitale Medien hinzufügen, indem er direkt auf den Server zugreift oder sich über den Remote Webzugriff-Standort bei dem Dashboard anmeldet. Andere Benutzer können dem Server Mediendateien mithilfe der Verbindung frei **gegebene Ordner** auf dem Launchpad, mithilfe der Remote Webzugriff-Website oder mithilfe der My Server-App für Windows Phone hinzufügen. Informationen zum Wiedergeben von Medien finden Sie unter [Wiedergeben und Freigeben digitaler Medien](Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2).  

 Der Server Administrator kann freigegebenen Ordnern in der Medienbibliothek digitale Medien hinzufügen, indem er direkt auf den Server zugreift oder sich über den Remote Webzugriff-Standort bei dem Dashboard anmeldet. Andere Benutzer können dem Server Mediendateien mithilfe der Verbindung frei **gegebene Ordner** auf dem Launchpad, mithilfe der Remote Webzugriff-Website oder mithilfe der My Server-App für Windows Phone hinzufügen. Informationen zum Wiedergeben von Medien finden Sie unter [Wiedergeben und Freigeben digitaler Medien](../use/Play-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2).  

  
> [!NOTE]
>  Sie können Mediendateien auch mit der My Server-App für Windows Phone auf den Server hochladen. Sie können die My Server-Apps aus dem [Windows Phone Store](http://www.windowsphone.com/store/app/my-server/6c2f98d5-6fcf-4e1d-b8b1-cde62ea1a94a)herunterladen. Weitere Informationen zur My Server-App für Windows Phone finden Sie im Blogbeitrag [My Server Phone App for Windows Server Essentials](https://blogs.technet.com/b/sbs/archive/2012/09/18/my-server-phone-app-for-windows-server-2012-essentials.aspx).  
  
#### <a name="to-add-digital-media-files-to-shared-folders-on-the-server"></a>So fügen Sie digitale Mediendateien freigegebenen Ordnern auf dem Server hinzu  
  
1.  Verwenden Sie eine der folgenden Methoden für die Anmeldung beim Server:  
  

    1.  Informationen zum Anmelden bei Remote Webzugriff finden Sie unter [use Remote Webzugriff](Use-Remote-Web-Access-in-Windows-Server-Essentials.md).  

    1.  Informationen zum Anmelden bei Remote Webzugriff finden Sie unter [use Remote Webzugriff](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md).  

  
    2.  Weitere Informationen zum Anmelden mit Launchpad finden Sie unter [Launchpad Overview (Übersicht über Launchpad](../manage/Overview-of-the-Launchpad-in-Windows-Server-Essentials.md)).  
  
2.  Suchen Sie den Ordner für das Medium, das Sie hinzufügen, und klicken Sie darauf.  
  
3.  Kopieren Sie die gewünschten Mediendateien, und fügen Sie sie in den entsprechenden freigegebenen Ordner auf dem Server ein. Sie können sie auch mit Drag & Drop verschieben.  
  
##  <a name="download-format-options"></a><a name="BKMK_5"></a>Download Formatoptionen  
 Es gibt zwei Optionen zum Herunterladen von Dateien. Diese Optionen sind nur verfügbar, wenn Sie mehrere Dateien oder einen Ordner auf einen Windows-basierten Computer herunterladen.  
  
 Wählen Sie im Folgenden die Option, die Ihre Downloadanforderungen erfüllt:  
  
- **Komprimierte ZIP-Datei (. zip)**  
  
   Durch das Zippen einer Datei wird eine komprimierte Dateiversion erstellt, die kleiner als die Originaldatei ist. Die komprimierte Dateiversion verfügt über die Dateierweiterung ".zip". Dateitypen, die am meisten von der Komprimierung profitieren, sind textorientierte Dateitypen (z. B. TXT-, DOC- und XLS-Dateien) und Grafiken, die nicht komprimierte Dateitypen verwenden (z. B. ".bmp"). Einige Grafikdateien wie JPG- und GIF-Dateien nutzen bereits die Komprimierung, sodass sich die Dateigröße durch das Komprimieren nur geringfügig verkleinert. Darüber hinaus reduziert sich die Dateigröße eines Word-Dokuments mit vielen Grafiken nicht in dem Maße wie ein Dokument, das hauptsächlich Text enthält.  
  
  > [!NOTE]
  >  Diese Option bietet eingeschränkte Unterstützung für internationale Dateinamen.  
  
- **Selbst extrahierende ausführbare Datei (. exe)**  
  
   Eine selbstextrahierende ausführbare Datei ist eine herunterladbare Datei, die das Dekomprimierungsprogramm (ausführbare Datei) mit den komprimierten Dateien kombiniert. Beim Ausführen des Programms werden die komprimierten Dateien automatisch dekomprimiert. Mit diesem gängigen Verfahren können komprimierte Daten verteilt werden, ohne dass der Empfänger über das nötige Dekomprimierungshilfsprogramm verfügen muss.  
  
  > [!NOTE]
  >  Diese Option unterstützt Unicode-Zeichen.  
  
  Vor Beginn des eigentlichen Downloads wird die EXE- oder ZIP-Datei erstellt. Abhängig von der Anzahl der Dateien und der Gesamtgröße der Downloaddateien kann dies einige Minuten dauern. Nachdem die Downloaddatei erstellt wurde, erfolgt das Herunterladen der Datei im Hintergrund. Dadurch können Sie weiterarbeiten, während der Downloadvorgang ausgeführt wird.  
  
##  <a name="easy-file-upload-tool"></a><a name="BKMK_6"></a>Einfaches Tool zum Hochladen von Dateien  
 Das Tool "einfacher Datei Upload" optimiert das Hochladen von Dateien auf Ihren Windows Server Essentials-Server. Sie können dem Tool "einfacher Datei Upload" beliebig viele Dateien hinzufügen und Sie dann in einem einzigen Batch in die freigegebenen Ordner auf dem Windows Server Essentials-Server hochladen. Weitere Informationen finden Sie im Blogbeitrag [Grundlegendes zur Dateifreigabe mit Remotewebzugriff](https://blogs.technet.com/b/sbs/archive/2012/04/19/understanding-remote-web-access-file-sharing.aspx).  
  
##  <a name="view-and-browse-shared-digital-media"></a><a name="BKMK_7"></a>Anzeigen und Durchsuchen von freigegebenen digitalen Medien  
 Sie können Ressourcen entweder über das Dashboard, das Launchpad, die Website für Remotewebzugriff oder die My Server-App für Windows Phone anzeigen oder durchsuchen.  
  
#### <a name="to-view-and-browse-shared-media-from-the-dashboard"></a>So können Sie freigegebene Medien über das Dashboard anzeigen und durchsuchen  
  
1.  Öffnen Sie das Server-Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **SPEICHER**.  
  
3.  Klicken Sie auf die Registerkarte **Server Ordner** . Eine Liste der Server Ordner wird angezeigt.  
  
4.  Doppelklicken Sie auf einen Ordner, um dessen Inhalt anzuzeigen.  
  
#### <a name="to-view-and-browse-shared-media-using-the-launchpad-from-a-network-computer"></a>So können Sie freigegebene Medien über das Launchpad eines Netzwerkcomputers anzeigen und durchsuchen  
  
1.  Melden Sie sich beim Launchpad an.  
  
2.  Klicken Sie auf **Freigegebene Ordner**. Windows-Explorer wird geöffnet und zeigt eine Liste der freigegebenen Ordner auf dem Server an.  
  
3.  Doppelklicken Sie auf einen Ordner, um dessen Inhalt anzuzeigen.  
  
#### <a name="to-view-and-browse-shared-media-using-remote-web-access"></a>So können Sie freigegebene Medien über Remotewebzugriff anzeigen und durchsuchen  
  
1.  Melden Sie sich bei Remotewebzugriff an.  
  
2.  Klicken Sie auf **Freigegebene Ordner**. Im Abschnitt **Freigegebene Ordner** der Webseite wird eine Liste freigegebener Ordner auf dem Server angezeigt.  
  
3.  Doppelklicken Sie auf einen Ordner, um dessen Inhalt anzuzeigen.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten von digitalen Medien](../manage/Manage-Digital-Media-in-Windows-Server-Essentials.md)  
  

-   [Verbindung herstellen](Get-Connected-in-Windows-Server-Essentials.md)  
  
-   [Verwenden von freigegebenen Ordnern](Use-Shared-Folders-in-Windows-Server-Essentials.md)  
  
-   [Remote arbeiten](Work-Remotely-in-Windows-Server-Essentials.md)

-   [Verbindung herstellen](../use/Get-Connected-in-Windows-Server-Essentials.md)  
  
-   [Verwenden von freigegebenen Ordnern](../use/Use-Shared-Folders-in-Windows-Server-Essentials.md)  
  
-   [Remote arbeiten](../use/Work-Remotely-in-Windows-Server-Essentials.md)

