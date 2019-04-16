---
title: Verwalten von digitalen Medien in Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9378bffa-487c-43ca-9ec3-7e7864d2dd9a
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 6906c1dafc6d4131e07c008b9db47ebebe9b7770
ms.sourcegitcommit: 5c8d8acc59d61756377c9c4e459a47a9ab555b39
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="manage-digital-media-in-windows-server-essentials"></a>Verwalten von digitalen Medien in Windows Server Essentials

>Gilt für: Windows Server2012 R2 Essentials, Windows Server2012 Essentials

In den folgenden Themen werden die Medienstreaming-Funktionen des Servers, und führen Sie zum Einrichten und verwenden in Ihrem Netzwerk Streamen von Medien.  
  
> [!NOTE]
>  Standardmäßig ist die streaming Media-Funktionalität mit installierter Windows Server Essentials Experience-Rolle in Windows Server Essentials und Windows Server 2012 R2 nicht verfügbar. Hinzufügen von Medienstreaming-Funktionen in diesen Versionen [herunterladen und Installieren von Windows Server Essentials Media Pack](https://www.microsoft.com/download/details.aspx?id=40837) aus dem Microsoft Download Center.  
  
-   [Übersicht über digitale Medien](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Verwalten des Medienservers mithilfe des Dashboards](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Funktionsweise von Medienstreaming](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [Aktivieren von Medienstreaming aktivieren oder deaktivieren](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [Fügen Sie digitaler Mediendateien mit dem Server hinzu](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [Zulassen Sie oder beschränken Sie des Zugriffs auf eine Medienbibliothek auf dem server](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6)  
  
-   [Umbenennen der Medienbibliothek](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_8)  
  
-   [Beenden Sie die Freigabe digitaler Medien](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_9)  
  
-   [Aktivieren von Mediengeräten, die das Server Message Block (SMB)-Protokoll für den Zugriff auf freigegebene Dateien auf dem Server verwenden](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_10)  
  
-   [Allgemeine Prozessoren und die video-Profile, die diese unterstützen](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_CommonProcessors)  
  
-   [Bekannte Probleme bei Mediendateitypen](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_KnownIssues)  
  
##  <a name="BKMK_1"></a>Übersicht über digitale Medien  
 Digitale Medien sind Audio-, Video- und fotoinhalte, die (Digital komprimiert) codiert wurden. Codieren von Inhalten werden Audio- und video-Eingabe für eine digitale Mediendatei, z. B. eine Windows Media-Datei konvertieren. Nach digitale Medien codiert ist, es kann leicht bearbeitet, verteilt, und von Computern wiedergegeben und über Computernetzwerke übertragen.  
  
 Beispiele für digitale Medien sind: Windows Media Audio (WMA), Windows Media Video (WMV), MP3, JPEG und AVI. Weitere Informationen zu den digitalen Medientypen, die von Windows Media Player unterstützt werden, finden Sie unter [von Windows Media Player unterstützte Dateitypen](https://support.microsoft.com/kb/316992).  
  
### <a name="why-would-i-want-to-stream-my-digital-media"></a>Warum würde ich möchte meine digitalen Medien streamen?  
 Viele Benutzer speichern Musik, Videos und Bilder in freigegebenen Ordnern in Windows Server Essentials. Möglicherweise möchten Sie die folgenden Schritte ausführen:  
  
-   **Sehen Sie sich Videos**. Der Server kann zum Speichern und streamen umfangreiche Videosammlungen und TV-Aufzeichnungen auf Ihrem Computer oder andere Wiedergabegeräte Geräte in Ihrem Netzwerk. Sie können Videos auf einer Xbox 360 oder auf einem Computer mit Windows Media Player streamen.  
  
-   **Wiedergeben von Musik**. Wenn Sie für die Medienfreigabe aktivieren der **Musik** freigegebenen Ordner können Sie Ihre Musik zugreifen, von Geräten, die Windows Media Connect unterstützen. Sie müssen nicht aktivieren oder konfigurieren alle Benutzerkonten aus Streamen der **Musik** freigegebenen Ordner nach der Freigabe aktiviert ist.  
  
-   **Präsentieren Sie Diashows**. Sie können Ihre digitalen Fotos im Speichern der **Fotos** freigegebenen Ordner auf dem Server, und klicken Sie dann greifen sie von jedem Computer oder von einer Xbox 360, der mit einem Fernsehgerät bei Ihnen zuhause oder im Büro verbunden ist. Sie können fotodiashows ansehen und Ihr TV in einen großen Bilderrahmen verwandeln.  
  
###  <a name="BKMK_1.5"></a>Freigeben kopiergeschützter Medien  
  Windows Server Essentials unterstützt freigeben kopiergeschützter Medien nicht. Dazu gehört auch Musik, die über eine online-Music Store erworben wird.  
  
 Kopiergeschützte Medien können wiedergegeben werden, nur auf dem Computer oder Gerät, das Sie zum Kaufen verwendet. Kopierschutz verhindert, dass Sie auf mehrere Computer oder Gerät, das Wiedergeben von Medien, auch wenn Sie das Medium auf den Server kopieren und dort wiedergeben. Allerdings können das kopiergeschützte Medium auf Windows Server Essentials speichern und weiterhin auf dem Computer oder Gerät, mit dem Sie zum Kaufen die Medien wiedergeben.  
  
##  <a name="BKMK_2"></a>Verwalten des Medienservers mithilfe des Dashboards  
  Windows Server Essentials ermöglicht die allgemeine administrative Aufgaben mithilfe von Windows Server Essentials-Dashboard ausführen. Die **Media** Registerkarte des Servers **Einstellungen** -Seite des Dashboards bietet Folgendes:  
  
|Im Abschnitt|Funktionen|  
|-------------|-------------------|  
|Media-server|Die **einschalten / ausschalten** Schaltfläche aktiviert Medienstreaming aktivieren oder deaktivieren.|  
|Videostreamingqualität|Das Dropdown-Pfeil können Sie wählen die videostreamingqualität Videos, die vom Server wiedergegeben werden.|  
|Medienbibliothek|Zeigt den Namen der Medienbibliothek. Der Standardname der Bibliothek heißt **digitale Medienbibliothek**, die erstellt wird, wenn Sie das Medienstreaming aktivieren. Klicken Sie zum Ändern des Namens der Medienbibliothek finden Sie [Umbenennen der Medienbibliothek](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_8). Klicken Sie auf **anpassen** Ordner anpassen, die in der Medienbibliothek freigegeben werden.|  
  
 Weitere Informationen finden Sie unter [zulassen oder Beschränken des Zugriffs auf eine Medienbibliothek auf dem Server](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6) und [freigeben kopiergeschützter Medien](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_1.5).  
  
##  <a name="BKMK_3"></a>Funktionsweise von Medienstreaming  
 Die Medienstreaming-Funktion in Windows Server Essentials macht es möglich, dass Netzwerkcomputer und einige Geräte im Netzwerk digitale Medien auf digitale Mediendateien wiedergeben, die auf dem Server gespeichert sind.  
  
 Wenn Sie den Medienserver aktivieren, ist Inhalt, die Sie in den Medienbibliotheken freigeben für die Wiedergabe auf Geräten im Netzwerk zur Verfügung, die Streamingmedien vom Server empfangen werden. Sie können die meisten Arten von digitalen Mediendateien streamen. Das häufigeren von Dateien, die Sie streamen können unter anderem:  
  
-   Windows Media-Formate (.asf, .wma, .wmv, .wm)  
  
-   Audio Visual Interleave (AVI)  
  
-   Verschieben von Bildern Experts Group (.mpeg, .mpg,. MP3)  
  
-   Audio für Windows (.wav)  
  
-   CD-Audiospur (.cda)  
  
 Doppelklicken Sie auf eine Datei wiederzugeben, suchen Sie einfach einen Song, Video oder ein Bild in einem freigegebenen Ordner, auf die Datei, und der Inhalt wird vom Server auf Ihren Computer Streamen und wiedergeben. Informationen zum Suchen und Wiedergeben der digitalen Mediendateien, die auf dem Server gespeichert sind, finden Sie unter [Wiedergeben von Digitalmedien](../use/Play-Digital-Media-in-Windows-Server-Essentials.md).  
  
 Zum Streamen von Medien benötigen Sie die folgende Hardware:  
  
-   Ein verkabeltes oder drahtloses privates Netzwerk  
  
-   Entweder einen anderen Computer im Netzwerk oder auf einen digitalen Medienempfänger (einen digital Media-Player bezeichnet) bezeichnet. Digital Media-Receiver sind Hardwaregeräte, die mit dem verkabelten oder drahtlosen Netzwerk, die Sie steuern können, indem Sie mithilfe des Computers verbunden?, auch wenn sich der Computer in einem anderen Raum befindet.  
  
 Weitere Informationen finden Sie unter [aktivieren Medienstreaming aktivieren oder deaktivieren](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4).  
  
##  <a name="BKMK_4"></a>Aktivieren von Medienstreaming aktivieren oder deaktivieren  
 Sie können Musik, Videos und Bilder von Windows Server Essentials freigeben Streamingdateien für alle unterstützten digital Media Receiver (, DMR) wie z. B. Computer, Mobiltelefone, Fernsehgeräte, Empfänger für digitale Medien, Extender für Windows Media Center (einschließlich Xbox 360) und andere persönliche elektronische Geräte.  
  
 Eine aktuelle Liste von digitalen Medien-Geräten, die mit Windows Server Essentials kompatibel sind, finden Sie unter der [Windows-Kompatibilitätscenter](https://www.microsoft.com/windows/compatibility/CompatCenter/Home).  
  
### <a name="enabling-media-sharing"></a>Aktivieren der Medienfreigabe  
 Um in Windows Server Essentials gespeicherten Medien freizugeben, müssen Sie das Medienstreaming aktivieren. Das Medienstreaming ist standardmäßig deaktiviert.  
  
####  <a name="BKMK_2.5"></a>So aktivieren Sie Medienstreaming aktivieren oder deaktivieren  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf **Einstellungen**, klicken Sie auf **Media**, und führen Sie dann eine der folgenden Optionen:  
  
    -   Klicken Sie auf **aktivieren** damit beginnen, alle Dateien, die in der Medienbibliothek des Servers gespeichert sind.  
  
    -   Klicken Sie auf **deaktivieren** die Freigabe aller Dateien, die in der Medienbibliothek des Servers gespeichert sind.  
  
3.  Wenn Sie weitere Ordner in der Medienbibliothek freigeben möchten, klicken Sie auf **anpassen**, und wählen Sie dann **Ja** für jeden freigegebenen Ordner, die in der Medienbibliothek aufgenommen werden sollen.  
  
4.  Klicken Sie auf **OK** um Ihre Änderungen zu speichern.  
  
 Weitere Informationen zu den digitalen Medientypen, die von Windows Media Player unterstützt werden, finden Sie unter [von Windows Media Player unterstützte Dateitypen](https://support.microsoft.com/kb/316992).  
  
 Weitere Informationen finden Sie unter [zulassen oder Beschränken des Zugriffs auf eine Medienbibliothek auf dem Server](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6).  
  
##  <a name="BKMK_5"></a>Fügen Sie digitaler Mediendateien mit dem Server hinzu  
 Der Serveradministrator kann digitale Medien in der Medienbibliothek freigegebenen Ordner durch den Zugriff auf dem Server direkt oder über die Remote Web Access-Website auf dem Dashboard anmelden hinzufügen. Andere Benutzer können Mediendateien mit dem Server hinzufügen, indem Sie mit der **freigegebene Ordner** Verbindung auf dem Launchpad mithilfe der Remotewebzugriff-Website oder mithilfe der My Server-app für Windows Phone. Informationen zum Wiedergeben von Medien finden Sie unter [Wiedergeben von Digitalmedien](../use/Play-Digital-Media-in-Windows-Server-Essentials.md).  
  
> [!NOTE]
>  Sie können auch mithilfe der My Server-app für Windows Phone-Mediendateien mit dem Server hochladen. Sie können die My Server-app aus dem [Windows Phone Store](http://www.windowsphone.com/store/app/my-server/6c2f98d5-6fcf-4e1d-b8b1-cde62ea1a94a). Weitere Informationen zur My Server-app für Windows Phone finden Sie im Blogbeitrag [My Server Phone-app für Windows Server Essentials](http://blogs.technet.com/b/sbs/archive/2012/09/18/my-server-phone-app-for-windows-server-2012-essentials.aspx).  
  
#### <a name="to-add-digital-media-files-to-shared-folders-on-the-server"></a>Digitale Mediendateien freigegebenen Ordnern auf dem Server hinzu  
  
1.  Verwenden Sie eine der folgenden Methoden, um mit dem Server anmelden:  
  
    1.  Informationen zur Anmeldung beim Remotewebzugriff finden Sie unter [melden Sie sich bei Remotewebzugriff](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_1).  
  
    2.  Informationen zum Anmelden mit Launchpad finden Sie unter [Launchpad Übersicht](Overview-of-the-Launchpad-in-Windows-Server-Essentials.md).  
  
2.  Suchen Sie nach, und klicken Sie auf den Ordner für das Medium, die Sie hinzufügen möchten.  
  
3.  Kopieren und einfügen oder Drag-and-Drop hinzufügen die Mediendateien, die Sie möchten in den entsprechenden freigegebenen Ordner auf dem Server.  
  
##  <a name="BKMK_6"></a>Zulassen Sie oder beschränken Sie des Zugriffs auf eine Medienbibliothek auf dem server  
  
-   Wenn Sie die Medienfreigabe aktivieren, erstellt es vier vordefinierten Ordner: Musik, Bilder, Videos und TV-Aufzeichnungen. Wenn einer dieser Ordner Medienfreigabe auf dem Server, wird des vorhandenen Ordners als freigegebener Ordner für die Freigabe von Medien wiederverwendet. Alle vorhandenen Ordner s Medien und Berechtigungen werden beibehalten und gelten für alle Benutzer im Netzwerk.  
  
-   Bevor Sie die Medienbibliothekfreigabe für einen freigegebenen Ordner aktivieren, sollten Sie wissen, dass die Medienbibliothekfreigabe jede Art von benutzerkontenzugriff umgangen werden, die Sie für den freigegebenen Ordner festlegen. Zum Beispiel nehmen wir an, dass Sie die Medienbibliothekfreigabe für Aktivieren der **Fotos** freigegebenen Ordner, und legen Sie die **Fotos** freigegebenen Ordner **kein Zugriff** für einen Benutzer mit dem Namen Roland. Roland weiterhin digitalen Medien aus Streamen der **Videos** freigegebenen Ordner, um alle unterstützten digital Media-Player oder DMRS. Wenn Sie digitale Medien, die nicht verfügen auf diese Weise gestreamt werden sollen, speichern Sie die Dateien in einem Ordner, der keine Medienbibliothekfreigabe aktiviert haben.  
  
-   Wenn Sie auf die Medienbibliothekfreigabe für einen freigegebenen Ordner aktivieren, kann alle unterstützten digital Media-Player oder DMRS, die das Windows Server Essentials-Netzwerk zugreifen kann auch Ihre digitalen Medien in diesem freigegebenen Ordner zugreifen. Beispielsweise kann, wenn Sie über ein Drahtlosnetzwerk verfügen und Sie nicht ist gesichert haben, hat jeder im Bereich des Drahtlosnetzwerks potenziell von digitalen Medien in diesem Ordner zugreifen. Bevor Sie die Medienbibliothekfreigabe aktivieren, stellen Sie sicher, dass Sie Ihr Drahtlosnetzwerk geschützt. Weitere Informationen finden Sie in der Dokumentation zu Ihrem drahtlosen Zugriffspunkt.  
  
##  <a name="BKMK_8"></a>Umbenennen der Medienbibliothek  
 Der Standardname der Medienbibliothek ist **Digital Media-Server**. Es wird erstellt, wenn Sie in Windows Server Essentials-Medienstreaming aktivieren. Weitere Informationen zum Aktivieren auf Streamen von Medien finden Sie unter [Medienstreaming aktivieren oder deaktivieren aktivieren](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.5). Sie können Namens der Medienbibliothek jederzeit ändern, mit dem Server-Dashboard.  
  
#### <a name="to-rename-the-media-library"></a>Umbenennen die Medienbibliothek  
  
1.  Öffnen Sie das Server-Dashboard. Klicken Sie zum Öffnen des Dashboards über das Launchpad **Dashboard**, geben Sie das Serverkennwort, und klicken Sie dann auf den Pfeil, um die Anmeldung.  
  
2.  Klicken Sie auf den Server-Dashboard auf **Einstellungen**.  
  
3.  Auf der **Einstellungen** auf die **Media** Registerkarte.  
  
4.  In der **Medienbibliothek** Teil der **medieneinstellungen** auf den Namen der Medienbibliothek.  
  
5.  In der **Ändern des Namens der Medienbibliothek** Dialogfeld Geben Sie einen neuen Namen für die Medienbibliothek, und klicken Sie dann auf **OK**.  
  
##  <a name="BKMK_9"></a>Beenden Sie die Freigabe digitaler Medien  
 Der Serveradministrator kann Freigabe digitale Medien, die in freigegebenen Ordnern auf einem Server unter Windows Server Essentials gespeichert sind.  
  
#### <a name="to-stop-sharing-media-in-shared-folders"></a>Zum Beenden der Freigabe von Medien in freigegebenen Ordnern  
  
1.  Öffnen Sie das Server-Dashboard.  
  
2.  Auf dem Dashboard **Home** auf **Setup**, klicken Sie auf **Medienserver einrichten**, und klicken Sie dann auf **klicken Sie auf den Medienserver einzurichten**.  
  
3.  Auf der **Media** Seite "Einstellungen", Sie können eine der folgenden Optionen:  
  
    -   Klicken Sie auf **deaktivieren** die Freigabe aller Dateien, die auf dem Server gespeichert sind.  
  
    -   Klicken Sie auf **anpassen**, und wählen Sie dann **keine** für bestimmte Ordner, die Sie die Freigabe beenden möchten.  
  
4.  Klicken Sie auf **übernehmen** oder **OK** um Ihre Änderungen zu speichern.  
  
##  <a name="BKMK_10"></a>Aktivieren von Mediengeräten, die das Server Message Block (SMB)-Protokoll für den Zugriff auf freigegebene Dateien auf dem Server verwenden  
 Geräte, Server Message Block (SMB) für Netzwerkdateien und-Freigaben Netzwerkzugriff anstatt DLNA (für das Medienstreaming) erfordern, dass das Gastkonto aktiviert werden. Dadurch wird jedes Gerät oder Benutzer auf das Netzwerk an den Inhalt des freigegebenen Ordner ohne Authentifizierung anzuzeigen.  
  
> [!CAUTION]
>  Wenn Sie das Gastkonto aktivieren, kann jeder Benutzer standardmäßig die freigegebenen Ressourcen auf dem Server zugreifen.  
  
##  <a name="BKMK_CommonProcessors"></a>Allgemeine Prozessoren und die video-Profile, die diese unterstützen  
 Zum Streamen von Medien aus dem Windows Server Essentials-Server können Sie einen Computer mit dem Betriebssystem Windows 7 oder Windows 8 oder andere Netzwerkgeräte (z. B. digital Media-Player) oder Media Center Extender (z. B. Xbox 360) verwenden. Wenn Sie nicht Ihr Netzwerk sind, verwenden Sie Remote Web Access Media Player zum Wiedergeben, die auf dem Server gespeichert sind.  
  
 Sie benötigen eine Datenübertragungsrate zwischen 200 Kbit/s und 10 Mbit/s. Sie müssen Medienformate verwenden, die den Computer und Geräte erkannt und wiedergegeben werden können. Nicht alle Geräte unterstützen dieselben Medienformate, daher muss eine Möglichkeit für den Computer und Geräte, die Mediendateien wiederzugeben, die Sie haben.  
  
  Windows Server Essentials transcodierungsunterstützung, die die Funktion des Computers oder Geräts bestimmt und eine nicht unterstützte Videodateien dann dynamisch in unterstützte Formate konvertiert. Wenn Windows Media Player 12 Inhalte auf einem Computer wiedergegeben werden können, auf denen Windows 7 oder Windows 8 ausgeführt wird, werden die Inhalte auf dem Server im Allgemeinen auf dem Netzwerk verbundenen Gerät wiedergegeben.  
  
 Das Format und die jeweilige Bitrate für die transcodierung ausgewählt ist hoch die Leistung des Serverprozessors abhängig. Die prozessorleistung wird als Teil des Windows-Leistungsindex identifiziert. Um die leistungsbewertung Ihres Servers zu bestimmen, führen Sie eine der folgenden:  
  
-   Auf einem Netzwerkcomputer unter Windows 7 oder Windows 8, den über denselben Prozessor wie Ihr Server verfügt, wechseln Sie zu der **Systemsteuerung**, klicken Sie auf **Leistungsinformationen und-Tools**, und überprüfen Sie die Informationen auf der **bewerten und Verbessern der computerleistung Ihrer s** Seite.  
  
-   Wenden Sie sich an den Hersteller des Prozessors.  
  
 Wählen Sie für die bestmögliche benutzerfreundlichkeit Videostreaming eine auflösungsqualität, die für Ihren Serverprozessor geeignet ist. Der Server wird automatisch angepasst, die Bitrate, um eine der folgenden Einstellungen:  
  
-   **Niedrig** die prozessorbewertung ist weniger liegt unter 3,6.  
  
-   **Mittel** , wenn die prozessorbewertung höher als 3,6 und niedriger als 4,2 ist.  
  
-   **Hohe** , wenn die prozessorbewertung höher als 4,2 und niedriger als 6,0 ist.  
  
-   **Beste** ist die prozessorbewertung liegt über 6,0.  
  
 Bei Auswahl Videostreaming eine Auflösung, die als Ihr Server verfügt über mehr verarbeitungsleistung erfordert, auftreten Puffer und nicht mehr beim Streamen von Medien auf dem Server.  
  
> [!NOTE]
>  Zum Streamen von HD-Videos über den Remotewebzugriff auf Sie einen Prozessor benötigen mit einer Bewertung von mindestens 6.0.  
  
##  <a name="BKMK_KnownIssues"></a>Bekannte Probleme bei Mediendateitypen  
 Die Medienstreaming-Funktion in Remotewebzugriff verwendet den Windows Media Player 12--Netzwerkfreigabedienst. Remote Web Access Mediastreaming unterstützt die Audio-, Video- und Bilddateitypen, die von Windows Media Player 12 und Silverlight 4 unterstützt werden.  
  
 Die folgende Tabelle enthält die Dateitypen (Formate), die von Medienstreaming Remote Web Access unterstützt werden. Wenn vorhanden, dass die Medien auf Ihrem Server Dateitypen, die nicht in der Tabelle enthalten sind sind, können nicht Sie sie über Remotewebzugriff Streamen von Medien streamen.  
  
|Dateityp|Dateinamenerweiterung|  
|---------------|-------------------------|  
|3GPP-Dateien|. 3GP,. 3GPP, .3 g 2 und. 3gp2|  
|Audio Data Transport Stream (ADTS)-Audiodateien|.ADTS und .adt|  
|AU-Audiodateien|.au und .snd|  
|Audio Interchange File Format (AIFF)-Audiodateien|.AIF, .aifc und .aiff|  
|AVCHD-Dateien|. m2ts,. m2t und .mts|  
|CD-audio-Datenträger|.cda|  
|DVD-Video-Datenträger|.VOB|  
|JPEG-Bilddateien|JPG|  
|MP3-Audiodateien|MP3 und. m3u|  
|MPEG-Videodateien|.MPEG, .mpg,. m1v, .mpa, .mpe,. mp4,. MP4V,. M4V,. M4A und .mov|  
|Windows-audio und video-Dateien|.AVI und .wav|  
|Windows Media audio und video-Dateien|.ASF, .asx, .wax, WM, .wma, .wmd, .wmp, .wmv, .wmx, .wpl und .wvx|  
  
> [!NOTE]
>  Wenn Sie einen Dateityp verwenden können, der in dieser Tabelle aufgeführt ist, kann die Datei auch mit einem Codec codiert sein, die von Windows Media Player nicht unterstützt wird.  
  
 Weitere Informationen zu unterstützten Dateiformaten finden Sie unter [von Windows Media Player unterstützte Dateitypen](https://go.microsoft.com/fwlink/p/?LinkID=196118) und [Unterstützte Medienformate, Protokolle und Protokollfelder](https://go.microsoft.com/fwlink/p/?LinkId=203339) für Silverlight.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Wiedergeben von digitalen Medien](../use/Play-Digital-Media-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
