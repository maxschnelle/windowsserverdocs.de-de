---
title: Ändern der Einstellungen für Medienstreaming
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: dec690d2-f80c-4b09-99d6-3bba41331972
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: bbe3a934f402be91ea9bfaca7bbbbdae1922186a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80817323"
---
# <a name="change-media-streaming-settings"></a>Ändern der Einstellungen für Medienstreaming

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Für das Ändern der Einstellungen für Medienstreaming sind mehrere Optionen möglich. Die folgenden Optionen sind verfügbar:  
  
-   [Remote-Medien Streaming-Add-in ausblenden](Change-Media-Streaming-Settings.md#BKMK_DisableRemote)  
  
-   [Festlegen des Namens der Medienbibliothek](Change-Media-Streaming-Settings.md#BKMK_LibraryName)  
  
-   [Festlegen der videostreamingqualität](Change-Media-Streaming-Settings.md#BKMK_StreamingQuality)  
  
-   [Programm gesteuertes aktivieren oder Deaktivieren von Medien Streaming](Change-Media-Streaming-Settings.md#BKMK_Program)  
  
##  <a name="hide-remote-media-streaming-add-in"></a><a name="BKMK_DisableRemote"></a>Remote-Medien Streaming-Add-in ausblenden  
 Sie können das Remote-Medienstreaming-Add-In ausblenden, indem Sie der Registrierung einen Eintrag hinzufügen.  
  
#### <a name="to-hide-the-remote-media-streaming-add-in"></a>So blenden Sie das Remote-Medienstreaming-Add-In aus  
  
1.  Bewegen Sie Ihre Maus auf dem Server in die obere rechte Ecke des Bildschirms, und klicken Sie auf **Suchen**.  
  
2.  Geben Sie im Suchfeld **Suche** **regedit** ein und klicken Sie dann auf die **Regedit**-Anwendung.  
  
3.  Erweitern Sie den linken Fensterbereich bis zum folgenden Registrierungseintrag:  
  
     **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\RemoteAccess\DisabledAddIns**  
  
4.  Klicken Sie mit der rechten Maustaste auf **DisabledAddIns**, zeigen Sie auf **Neu**, und klicken Sie dann auf **DWORD-Wert**.  
  
5.  Geben Sie als neuen Wert **497796c6-9cc7-43be-aa26-4e6b5695370d**, d. h. den Bezeichner für das Remote-Medienstreaming-Add-In ein, und drücken Sie dann die **EINGABETASTE**.  
  
6.  Klicken Sie mit der rechten Maustaste auf den Wert, und klicken Sie dann auf **Ändern**.  
  
7.  Geben Sie **1** für die Wertdaten ein, und klicken Sie anschließend auf **OK**.  
  
##  <a name="set-the-media-library-name"></a><a name="BKMK_LibraryName"></a>Festlegen des Namens der Medienbibliothek  
 Sie können den Namen der Medienbibliothek mithilfe einer Klasse im SDK für Windows Server-Lösungen festlegen. Zum Festlegen des Namens können Sie die **SetMediaLibraryName**-Methode der Klasse **MediaStreamingManager** im Namespace **Microsoft.WindowsServerSolutions.MediaStreaming** verwenden. Im folgenden Beispiel wird der Name der Medienbibliothek festgelegt:  
  
```c#  
  
MediaStreamingManager mediaStreamingManager = new MediaStreamingManager();  
string mediaLibraryName = Guid.NewGuid().ToString("B");   
mediaStreamingManager.SetMediaLibraryName(mediaLibraryName);  
  
```  
  
 Weitere Informationen finden Sie unter [SDK für Windows Server-Lösungen](https://go.microsoft.com/fwlink/?LinkID=248648).  
  
##  <a name="set-video-streaming-quality"></a><a name="BKMK_StreamingQuality"></a>Festlegen der videostreamingqualität  
 Sie legen die Videostreamingqualität fest, indem Sie die WinSAT-CPU-Bewertung abrufen und dann die XML-Datei, die Informationen zur WinSAT-Bewertung enthält, erstellen und installieren. Wenn die XML-Datei, die die Informationen zur WinSAT-Bewertung enthält, vor dem Ausführen der Erstkonfiguration installiert wird, wird dem Kunden die Benutzeroberfläche für das Festlegen der Videoqualität nicht angezeigt. Weitere Informationen finden Sie unter [Festlegen der WinSAT-Bewertung auf dem Server](Set-the-WinSAT-Score-on-the-Server.md).  
  
##  <a name="programmatically-enable-or-disable-media-streaming"></a><a name="BKMK_Program"></a>Programm gesteuertes aktivieren oder Deaktivieren von Medien Streaming  
 Sie können Medienstreaming mithilfe einer Klasse im SDK für Windows Server-Lösungen programmgesteuert aktivieren oder deaktivieren. Zum Aktivieren oder Deaktivieren von Medienstreaming können Sie die **SetMediaStreamingEnabled**-Methode der Klasse **MediaStreamingManager** im Namespace **Microsoft.WindowsServerSolutions.MediaStreaming** verwenden. Im folgenden Codebeispiel wird Medienstreaming aktiviert:  
  
```c#  
  
MediaStreamingManager mediaStreamingManager = new MediaStreamingManager();  
mediaStreamingManager.SetMediaStreamingEnabled(true);  
  
```  
  
 Im folgenden Codebeispiel wird Medienstreaming deaktiviert:  
  
```c#  
  
MediaStreamingManager mediaStreamingManager = new MediaStreamingManager();  
mediaStreamingManager.SetMediaStreamingEnabled(false);  
```  
  
## <a name="see-also"></a>Weitere Informationen  
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)