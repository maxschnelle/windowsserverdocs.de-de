---
title: Verwalten von digitalen Medien in Windows Server Essentials
description: Beschreibt, wie Windows Server Essentials
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
ms.openlocfilehash: 87ec5218455672cbfd2bc1d77244fd263b91362c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433298"
---
# <a name="manage-digital-media-in-windows-server-essentials"></a>Verwalten von digitalen Medien in Windows Server Essentials

>Gilt für: Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

In den folgenden Themen werden die Medienstreaming-Funktionen des Servers und das Einrichten und Verwenden des Medienstreamings im Netzwerk erläutert.  
  
> [!NOTE]
>  Standardmäßig ist die streaming Media-Funktionalität mit installierter Windows Server Essentials Experience-Rolle in Windows Server Essentials und Windows Server 2012 R2 nicht verfügbar. Zum Hinzufügen von Medienstreamingfunktionen in diesen Versionen müssen Sie das [Windows Server Essentials Media Pack herunterladen und installieren](https://www.microsoft.com/download/details.aspx?id=40837) , das im Microsoft Download Center verfügbar ist.  
  
-   [Übersicht über digitale Medien](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Verwalten des Medienservers mithilfe des Dashboards](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Funktionsweise von Medienstreaming](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [Deaktivieren von Medienstreaming aktivieren oder deaktivieren](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [Fügen Sie digitaler Mediendateien zum Server hinzu](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [Zulassen Sie oder Beschränken des Zugriffs auf eine Medienbibliothek auf dem server](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6)  
  
-   [Umbenennen der Medienbibliothek](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_8)  
  
-   [Aufheben Sie Freigabe digitaler Medien](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_9)  
  
-   [Aktivieren von Mediengeräten, die die Server Message Block (SMB)-Protokoll verwenden, um Zugriff auf freigegebene Dateien auf dem server](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_10)  
  
-   [Allgemeine Prozessoren und die unterstützten Videoprofile](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_CommonProcessors)  
  
-   [Bekannte Probleme bei Mediendateitypen](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_KnownIssues)  
  
##  <a name="BKMK_1"></a> Übersicht über digitale Medien  
 Digitale Medien sind Audio-, Video- und Fotoinhalte, die codiert (digital komprimiert) wurden. Beim Codieren von Inhalten werden Audio- und Videoeingaben in eine digitale Mediendatei, z. B. eine Windows Media-Datei, konvertiert. Nach der Codierung können digitale Medien einfach bearbeitet, verteilt, von Computern wiedergegeben und über Computernetzwerke übertragen werden.  
  
 Beispiele für digitale Medien sind: Windows Media Audio (WMA), Windows Media Video (WMV), MP3, JPEG und AVI. Informationen zu den digitalen Medientypen, die von Windows Media Player unterstützt werden, finden Sie unter [Von Windows Media Player unterstützte Dateitypen](https://support.microsoft.com/kb/316992).  
  
### <a name="why-would-i-want-to-stream-my-digital-media"></a>Warum sollte ich meine digitalen Medien streamen?  
 Viele Benutzer speichern Musik, Videos und Bilder in freigegebenen Ordnern in Windows Server Essentials. Sie haben verschiedene Möglichkeiten, Medien zu nutzen:  
  
-   **Videos ansehen**. Der Server kann zum Speichern und Streamen umfangreicher Videosammlungen und TV-Aufzeichnungen auf Ihre Computer oder andere Wiedergabegeräte im Netzwerk genutzt werden. Mithilfe von Windows Media Player können Sie Videos auf eine Xbox 360 oder auf einen Computer streamen.  
  
-   **Musik wiedergeben**. Wenn Sie die Medienfreigabe für den freigegebenen Ordner **Musik** aktivieren, können Sie über Geräte, die Windows Media Connect unterstützen, auf Ihre Musik zugreifen. Nachdem die Freigabe aktiviert wurde, müssen Sie keine Benutzerkonten aktivieren oder konfigurieren, um Musik aus dem freigegebenen Ordner **Musik** zu streamen.  
  
-   **Fotodiashow präsentieren**. Sie können Ihre digitalen Fotos im freigegebenen Ordner **Fotos** auf dem Server speichern und anschließend von jedem Computer oder von einer Xbox 360 darauf zugreifen, die mit einem Fernsehgerät bei Ihnen zuhause oder im Büro verbunden ist. Sie können Fotodiashows ansehen und Ihr Fernsehgerät praktisch in einen großen Bilderrahmen verwandeln.  
  
###  <a name="BKMK_1.5"></a> Freigeben kopiergeschützter Medien  
  Windows Server Essentials unterstützt freigeben kopiergeschützter Medien nicht. Dazu gehört auch Musik, die über einen Online-Music Store gekauft wurde.  
  
 Kopiergeschützte Medien können nur auf dem Computer oder Gerät wiedergegeben werden, über den bzw. das sie erworben wurden. Der Kopierschutz verhindert, dass Sie Medien auf mehr als einem Computer oder Gerät abspielen, auch wenn Sie das Medium auf den Server kopieren und dort wiedergeben. Allerdings können Sie die kopiergeschützter Medien in Windows Server Essentials zu speichern und weiterhin wiedergeben des Mediums, auf dem Computer oder Gerät, das Sie verwendet haben, sie zu erwerben.  
  
##  <a name="BKMK_2"></a> Verwalten des Medienservers mithilfe des Dashboards  
  Windows Server Essentials ermöglicht es, die Ausführung allgemeiner administrativer Aufgaben mithilfe von Windows Server Essentials-Dashboard. Die Registerkarte **Medien** der Seite **Einstellungen** des Serverdashboards bietet folgende Optionen:  
  
|Abschnitt|Funktionalität|  
|-------------|-------------------|  
|Medienserver|Mit der Schaltfläche **Einschalten/Ausschalten** können Sie das Medienstreaming aktivieren oder deaktivieren.|  
|Videostreamingqualität|Der Dropdownpfeil ermöglicht die Auswahl der Videostreamingqualität für die Videos, die vom Server wiedergegeben werden.|  
|Medienbibliothek|Zeigt den Namen der Medienbibliothek an. Der Standardname der Bibliothek lautet **Digitale Medienbibliothek**. Er wird beim Aktivieren des Medienstreamings erstellt. Informationen dazu, wie Sie den Namen der Medienbibliothek ändern, finden Sie unter [Umbenennen der Medienbibliothek](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_8). Klicken Sie auf **Anpassen**, um die in der Medienbibliothek freigegebenen Ordner anzupassen.|  
  
 Weitere Informationen finden Sie unter [Allow or restrict access to a media library on the server](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6) und [Sharing copy-protected media](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_1.5).  
  
##  <a name="BKMK_3"></a> Funktionsweise von Medienstreaming  
 Die medienstreamingfunktion in Windows Server Essentials ermöglicht es Computern und einigen digitalen Mediengeräten, die auf dem Server gespeicherte, digitale Mediendateien wiederzugeben.  
  
 Wenn Sie den Medienserver aktivieren, können Inhalte, die Sie in den Medienbibliotheken freigeben, auf Geräten im Netzwerk wiedergegeben werden, die in der Lage sind, Streamingmedien vom Server zu empfangen. Sie können die meisten Arten von digitalen Mediendateien streamen. Zu den häufiger verwendeten streamingfähigen Dateitypen gehören:  
  
- Windows Media-Formate (.asf, .wma, .wmv, .wm)  
  
- Audio Visual Interleave (.avi)  
  
- Moving Pictures Experts Group (.mpeg, .mpg, .mp3)  
  
- Audio für Windows (.wav)  
  
- CD Audio Track (.cda)  
  
  Um eine Datei wiederzugeben, suchen Sie einfach einen Songtitel, ein Video oder ein Bild in einem freigegebenen Ordner und doppelklicken auf die Datei. Der Inhalt wird vom Server auf den Computer gestreamt und wiedergegeben. Weitere Informationen zum Suchen und Wiedergeben der digitalen Mediendateien, die auf dem Server gespeichert sind, finden Sie unter [wiedergeben Digitalmedien](../use/Play-Digital-Media-in-Windows-Server-Essentials.md).  
  
  Zum Streamen von Medien benötigen Sie die folgende Hardware:  
  
- Ein privates Kabel- oder Drahtlosnetzwerk  
  
- Entweder einen anderen Computer in Ihrem Netzwerk oder ein so genanntes Empfangsgerät für digitale Medien (auch als vernetzter Digital Media-Player bezeichnet). Empfänger für digitale Medien sind Hardwaregeräte, die mit Ihrem verkabelten oder drahtlosen Netzwerk, die Sie steuern können, über den Computer verbunden?, selbst wenn der Computer in einem anderen Raum befindet.  
  
  Weitere Informationen finden Sie unter [aktiviert oder deaktiviert das Medienstreaming aktivieren](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_4).  
  
##  <a name="BKMK_4"></a> Deaktivieren von Medienstreaming aktivieren oder deaktivieren  
 Sie können Musik, Videos und Bilder von Windows Server Essentials freigeben durch Streamen von Dateien auf alle unterstützten digital Media Receiver (DMR), z. B. Computer, Mobiltelefone, Fernsehgeräte, Empfänger für digitale Medien, Extender für Windows Media Center (einschließlich Xbox 360), und andere persönliche elektronische Geräte.  
  
 Eine aktuelle Liste von digitalen Geräten, die mit Windows Server Essentials kompatibel sind, finden Sie unter den [Windows Compatibility Center](https://www.microsoft.com/windows/compatibility/CompatCenter/Home).  
  
### <a name="enabling-media-sharing"></a>Aktivieren der Medienfreigabe  
 Um die Medien freizugeben, die in Windows Server Essentials gespeichert ist, müssen Sie turn on Mediastreaming. Das Medienstreaming ist standardmäßig deaktiviert.  
  
####  <a name="BKMK_2.5"></a> Das Medienstreaming aktivieren oder deaktivieren aktivieren  
  
1. Öffnen Sie Windows Server Essentials-Dashboard.  
  
2. Klicken Sie auf **Einstellungen**, klicken Sie auf **Medien**, und führen Sie einen der folgenden Schritte aus:  
  
   -   Klicken Sie auf **Einschalten**, um alle Dateien freizugeben, die in der Medienbibliothek des Servers gespeichert sind.  
  
   -   Klicken Sie auf **Ausschalten** , um die Freigabe aller Dateien aufzuheben, die in der Medienbibliothek des Servers gespeichert sind.  
  
3. Wenn Sie weitere Ordner in der Medienbibliothek freigeben möchten, klicken Sie auf **Anpassen** und wählen dann **Ja** für jeden freigegebenen Ordner aus, der in die Medienbibliothek aufgenommen werden soll.  
  
4. Klicken Sie auf **OK**, um die Änderungen zu speichern.  
  
   Informationen zu den digitalen Medientypen, die von Windows Media Player unterstützt werden, finden Sie unter [Von Windows Media Player unterstützte Dateitypen](https://support.microsoft.com/kb/316992).  
  
   Weitere Informationen finden Sie unter [Zulassen oder Beschränken des Zugriffs auf eine Medienbibliothek auf dem Server](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_6).  
  
##  <a name="BKMK_5"></a> Fügen Sie digitaler Mediendateien zum Server hinzu  
 Der Server-Administrator kann digitale Medien an freigegebene Ordner in der Medienbibliothek durch Zugriff auf den Server direkt oder mithilfe der Remotewebzugriff-Website für die Anmeldung auf dem Dashboard hinzufügen. Andere Benutzer können mit dem Server Mediendateien hinzufügen, indem Sie mit der **gemeinsam genutzten Ordnern** Verbindung auf dem Launchpad mithilfe der Remotewebzugriff-Website oder mithilfe der My Server-app für Windows Phone. Informationen zum Wiedergeben von Medien finden Sie unter [wiedergeben Digitalmedien](../use/Play-Digital-Media-in-Windows-Server-Essentials.md).  
  
> [!NOTE]
>  Sie können Mediendateien auch mit der My Server-App für Windows Phone auf den Server hochladen. Sie können die My Server-Apps aus dem [Windows Phone Store](http://www.windowsphone.com/store/app/my-server/6c2f98d5-6fcf-4e1d-b8b1-cde62ea1a94a)herunterladen. Weitere Informationen zur My Server-app für Windows Phone finden Sie im Blogbeitrag [My Server Phone-app für Windows Server Essentials](http://blogs.technet.com/b/sbs/archive/2012/09/18/my-server-phone-app-for-windows-server-2012-essentials.aspx).  
  
#### <a name="to-add-digital-media-files-to-shared-folders-on-the-server"></a>So fügen Sie digitale Mediendateien freigegebenen Ordnern auf dem Server hinzu  
  
1.  Verwenden Sie eine der folgenden Methoden für die Anmeldung beim Server:  
  
    1.  Informationen zur Anmeldung beim Remotewebzugriff finden Sie unter [Anmelden beim Remotewebzugriff](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_1).  
  
    2.  Informationen zum Anmelden mit Launchpad finden Sie unter [Launchpad-Übersicht](Overview-of-the-Launchpad-in-Windows-Server-Essentials.md).  
  
2.  Suchen Sie den Ordner für das Medium, das Sie hinzufügen, und klicken Sie darauf.  
  
3.  Kopieren Sie die gewünschten Mediendateien, und fügen Sie sie in den entsprechenden freigegebenen Ordner auf dem Server ein. Sie können sie auch mit Drag & Drop verschieben.  
  
##  <a name="BKMK_6"></a> Zulassen Sie oder Beschränken des Zugriffs auf eine Medienbibliothek auf dem server  
  
-   Wenn Sie die Medienfreigabe aktivieren, werden die vier vordefinierten Ordner für Musik, Bilder, Videos und TV-Aufzeichnungen erstellt. Wenn einer dieser Ordner bereits auf dem Server vorhanden ist, wird der bestehende Ordner für die Medienfreigabe als freigegebener Ordner wiederverwendet. Medien und Benutzerberechtigungen alle des vorhandenen Ordners werden beibehalten, und sie werden für alle Benutzer im Netzwerk freigegeben.  
  
-   Bevor Sie die Medienbibliothekfreigabe für einen freigegebenen Ordner aktivieren, sollten Sie wissen, dass bei der Medienbibliothekfreigabe jede Art von Benutzerkontenzugriff umgangen wird, den Sie für den freigegebenen Ordner festlegen. Angenommen, Sie aktivieren die Medienbibliothekfreigabe für den freigegebenen Ordner **Fotos** und legen für den freigegebenen Ordner **Fotos** für ein Benutzerkonto mit dem Namen Roland die Option **Kein Zugriff** fest. In diesem Fall kann Roland weiterhin digitale Medien aus dem freigegebenen Ordner **Videos** auf alle unterstützten Digital Media-Player oder DMRs streamen. Wenn Sie über digitale Medien verfügen, die nicht auf diese Weise gestreamt werden sollen, speichern Sie die Dateien in einem Ordner, für den keine Medienbibliothekfreigabe aktiviert ist.  
  
-   Wenn Sie auf die Medienbibliothekfreigabe für einen freigegebenen Ordner aktivieren, kann alle unterstützten digital Media-Player oder DMRS, die auf Ihrem Windows Server Essentials-Netzwerk zugreifen kann auch Ihre digitalen Medien in diesem freigegebenen Ordner zugreifen. Wenn Sie beispielsweise über ein Drahtlosnetzwerk verfügen, das nicht gesichert ist, hat jeder im Bereich des Drahtlosnetzwerks die Möglichkeit, auf die digitalen Medien in diesem Ordner zuzugreifen. Bevor Sie die Medienbibliothekfreigabe aktivieren, stellen Sie sicher, dass Ihr Drahtlosnetzwerk geschützt ist. Weitere Informationen finden Sie in der Dokumentation zu Ihrem Funkzugriffspunkt.  
  
##  <a name="BKMK_8"></a> Umbenennen der Medienbibliothek  
 Der Standardname der Medienbibliothek ist **Digital Media-Server**. Er wird erstellt, wenn Sie in Windows Server Essentials das Medienstreaming aktivieren. Weitere Informationen zum Aktivieren auf Medien-streaming finden Sie unter [das Medienstreaming aktivieren oder deaktivieren aktivieren](Manage-Digital-Media-in-Windows-Server-Essentials.md#BKMK_2.5). Mithilfe des Serverdashboards können Sie den Namen der Medienbibliothek jederzeit ändern.  
  
#### <a name="to-rename-the-media-library"></a>So benennen Sie die Medienbibliothek um  
  
1.  Öffnen Sie das Server-Dashboard. Klicken Sie zum Öffnen des Dashboards über das Launchpad auf **Dashboard**, geben Sie das Serverkennwort ein, und klicken Sie dann auf den Pfeil, um sich anzumelden.  
  
2.  Klicken Sie im Serverdashboard auf **Einstellungen**.  
  
3.  Klicken Sie auf der Seite **Einstellungen** auf die Registerkarte **Medien** .  
  
4.  Klicken Sie im Abschnitt **Medienbibliothek** der Seite **Medieneinstellungen** auf den Namen der Medienbibliothek.  
  
5.  Geben Sie im Dialogfeld **Namen der Medienbibliothek ändern** einen neuen Namen für die Medienbibliothek ein, und klicken Sie dann auf **OK**.  
  
##  <a name="BKMK_9"></a> Aufheben Sie Freigabe digitaler Medien  
 Der Serveradministrator kann aufheben Freigabe digitaler Medien, die in freigegebenen Ordnern auf einem Server mit Windows Server Essentials gespeichert sind.  
  
#### <a name="to-stop-sharing-media-in-shared-folders"></a>So heben Sie die Freigabe von Medien in freigegebenen Ordnern auf  
  
1.  Öffnen Sie das Server-Dashboard.  
  
2.  Klicken Sie im Dashboard auf der Seite **Home** auf **Setup**, klicken Sie auf **Medienserver einrichten**, und klicken Sie dann auf **Klicken Sie hier, um den Medienserver einzurichten**.  
  
3.  Auf der Einstellungsseite für **Medien** können Sie unter folgenden Optionen wählen:  
  
    -   Klicken Sie auf **Ausschalten**, um die Freigabe aller Dateien aufzuheben, die auf dem Server gespeichert sind.  
  
    -   Klicken Sie auf **Anpassen**, und wählen Sie dann für bestimmte Ordner, deren Freigabe aufgehoben werden soll, **Nein** .  
  
4.  Klicken Sie auf **Übernehmen** oder **OK** , um die Änderungen zu speichern.  
  
##  <a name="BKMK_10"></a> Aktivieren von Mediengeräten, die die Server Message Block (SMB)-Protokoll verwenden, um Zugriff auf freigegebene Dateien auf dem server  
 Für Geräte, die anstatt DLNA (für das Medienstreaming) SMB (Server Message Block) für den Zugriff auf Netzwerkdateien und -freigaben verwenden, muss das Gastkonto aktiviert werden. Dadurch kann jedes Gerät oder jeder Benutzer im Netzwerk ohne Authentifizierung den Inhalt freigegebener Ordner anzeigen.  
  
> [!CAUTION]
>  Wenn Sie das Gastkonto aktivieren, kann standardmäßig jeder auf die freigegebenen Ressourcen auf dem Server zugreifen.  
  
##  <a name="BKMK_CommonProcessors"></a> Allgemeine Prozessoren und die unterstützten Videoprofile  
 Zum Streamen von Medien aus dem Windows Server Essentials-Server können Sie einen Computer, auf denen das Betriebssystem Windows 7 oder Windows 8 oder andere Netzwerkgeräte (z. B. digital Media-Player) oder Media Center Extender (z. B. Xbox 360) ausgeführt wird. Wenn Sie sich nicht in Reichweite Ihres Netzwerks befinden, verwenden Sie einen Media Player für den Remotewebzugriff zum Wiedergeben von Dateien, die auf dem Server gespeichert sind.  
  
 Sie benötigen eine Datenübertragungsrate zwischen 200 Kbit/s und 10 Mbit/s. Sie müssen Medienformate verwenden, die vom Computer und den Geräten erkannt und wiedergegeben werden können. Da nicht alle Geräte dieselben Medienformate unterstützen, müssen Sie sicherstellen, dass Ihre Mediendateien vom Computer und den Geräten wiedergegeben werden können.  
  
  Windows Server Essentials transcodierungsunterstützung, die die wiedergabefähigkeit des Computers oder Geräts bestimmt und konvertiert dann eine nicht unterstützte Videodateien dynamisch in unterstützte Formate. Wenn Inhalte von Windows Media Player 12 auf einem Computer wiedergegeben werden können, auf dem Windows 7 oder Windows 8 ausgeführt wird, werden die Inhalte auf dem Server im Allgemeinen auch vom jeweiligen Netzwerkgerät wiedergegeben.  
  
 Das für die Transcodierung gewählte Format und die jeweilige Bitrate sind in hohem Maß von der Leistung des Serverprozessors abhängig. Die Prozessorleistung wird anhand des Windows-Leistungsindexes identifiziert. Führen Sie eine der folgenden Aktionen aus, um die Leistungsbewertung Ihres Servers zu ermitteln:  
  
- Wechseln Sie auf einem Netzwerkcomputer unter Windows 7 oder Windows 8, den über denselben Prozessor wie Ihr Server verfügt, zu der **Systemsteuerung**, klicken Sie auf **Leistungsinformationen und-Tools**, und überprüfen Sie dann die Informationen auf der **Rate und Verbessern der Leistung Ihres Computers** Seite.  
  
- Wenden Sie sich an den Hersteller des Prozessors.  
  
  Um eine optimale Benutzererfahrung zu gewährleisten, wählen Sie für das Videostreaming eine Auflösungsqualität, die für Ihren Serverprozessor geeignet ist. Der Server legt die Bitrate automatisch auf eine der folgenden Einstellungen fest:  
  
- **Niedrig** : Die Prozessorbewertung liegt unter 3,6.  
  
- **Mittel** : Die Prozessorbewertung ist höher als 3,6 und niedriger als 4,2.  
  
- **Hoch** : Die Prozessorbewertung ist höher als 4,2 und niedriger als 6,0.  
  
- **Beste** : Die Prozessorbewertung liegt über 6,0.  
  
  Wenn Sie für das Videostreaming eine Auflösung wählen, die mehr Verarbeitungsleistung erfordert, als der Server leisten kann, kann es vorkommen, dass der Mediendatenstrom beim Streamen gepuffert bzw. unterbrochen wird.  
  
> [!NOTE]
>  Zum Streamen von High Definition-Videos über den Remotewebzugriff benötigen Sie einen Prozessor, der mindestens mit 6,0 bewertet wurde.  
  
##  <a name="BKMK_KnownIssues"></a> Bekannte Probleme bei Mediendateitypen  
 Die Medienstreaming-Funktion in Remotewebzugriff verwendet den Windows Media Player 12-Netzwerkfreigabedienst. Das Medienstreaming mit Remotewebzugriff unterstützt die Audio-, Video- und Bilddateitypen, die von Windows Media Player 12 und Silverlight 4 unterstützt werden.  
  
 In der folgende Tabelle sind die Dateitypen (Formate) aufgeführt, die beim Medienstreaming mit Remotewebzugriff unterstützt werden. Wenn auf Ihrem Server Mediendateitypen enthalten sind, die nicht in der Tabelle aufgelistet sind, ist es nicht möglich, sie über das Medienstreaming mit Remotewebzugriff zu streamen.  
  
|Dateityp|Dateierweiterung|  
|---------------|-------------------------|  
|3GPP-Dateien|.3gp, .3gpp, .3g2 und .3gp2|  
|ADTS (Audio Data Transport Stream)-Audiodateien|.adts und .adt|  
|AU-Audiodateien|.au und .snd|  
|AIFF (Audio Interchange File Format)-Audiodateien|.aif, .aifc und .aiff|  
|AVCHD-Dateien|.m2ts, .m2t und .mts|  
|Audio-CD|.cda|  
|Video-DVD|.vob|  
|JPEG-Bilddateien|.jpg|  
|MP3-Audiodateien|.mp3 und .m3u|  
|MPEG-Videodateien|.mpeg, .mpg, .m1v, .mpa, .mpe, .mp4, .mp4v, .m4v, .m4a und .mov|  
|Windows-Audio- und -Videodateien|.avi und .wav|  
|Windows Media-Audio- und -Videodateien|.asf, .asx, .wax, .wm, .wma, .wmd, .wmp, .wmv, .wmx, .wpl und .wvx|  
  
> [!NOTE]
>  Wenn Sie einen in dieser Tabelle aufgeführten Dateityp nicht verwenden können, wurde die Datei möglicherweise mit einem Codec codiert, der von Windows Media Player nicht unterstützt wird.  
  
 Zusätzliche Informationen zu unterstützten Dateiformaten finden Sie unter [Von Windows Media Player unterstützte Dateitypen](https://go.microsoft.com/fwlink/p/?LinkID=196118) und für Silverlight unter [Unterstützte Medienformate, Protokolle und Protokollfelder](https://go.microsoft.com/fwlink/p/?LinkId=203339) .  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Wiedergeben von digitalen Medien](../use/Play-Digital-Media-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
