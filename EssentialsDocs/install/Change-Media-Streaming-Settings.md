---
title: "Ändern der Einstellungen für Medienstreaming"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dec690d2-f80c-4b09-99d6-3bba41331972
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d34d60e792fcda4d71a4509fe3d1b95fc6e74d0e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="change-media-streaming-settings"></a>Ändern der Einstellungen für Medienstreaming

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Mehrere Optionen sind zum Ändern der Einstellungen für Medienstreaming verfügbar. Die folgenden Optionen sind verfügbar:  
  
-   [Blenden Sie remote-Medienstreaming-add-in aus](Change-Media-Streaming-Settings.md#BKMK_DisableRemote)  
  
-   [Festlegen des Namens der Medienbibliothek](Change-Media-Streaming-Settings.md#BKMK_LibraryName)  
  
-   [Festlegen der videostreamingqualität](Change-Media-Streaming-Settings.md#BKMK_StreamingQuality)  
  
-   [Programmgesteuert aktivieren oder Deaktivieren von Medienstreaming](Change-Media-Streaming-Settings.md#BKMK_Program)  
  
##  <a name="BKMK_DisableRemote"></a>Blenden Sie remote-Medienstreaming-add-in aus  
 Sie können die remote-Medienstreaming-add-in durch Hinzufügen eines Eintrags in der Registrierung ausblenden.  
  
#### <a name="to-hide-the-remote-media-streaming-add-in"></a>So blenden Sie die remote-Medienstreaming-add-in aus  
  
1.  Auf dem Server, bewegen Sie den Mauszeiger in die obere rechte Ecke des Bildschirms, und klicken Sie auf **Suche**.  
  
2.  In der **Suche** geben **Regedit**, und klicken Sie dann auf die **Regedit** Anwendung.  
  
3.  Erweitern Sie im linken Bereich auf den folgenden Registrierungseintrag:  
  
     **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\RemoteAccess\DisabledAddIns**  
  
4.  Mit der rechten Maustaste **DisabledAddIns**, zeigen Sie auf **neu**, und klicken Sie dann auf **DWORD-Wert**.  
  
5.  Geben Sie für den neuen Wert **497796c6-9cc7-43be-aa26-4e6b5695370d**, d. h. den Bezeichner für die remote-Medienstreaming-add-in, und drücken Sie dann die **EINGABETASTE**.  
  
6.  Klicken Sie mit der rechten Maustaste auf den Wert, und klicken Sie dann auf **ändern**.  
  
7.  Typ **1** für die Wertdaten ein, und klicken Sie dann auf **OK**.  
  
##  <a name="BKMK_LibraryName"></a>Festlegen des Namens der Medienbibliothek  
 Eine Klasse können im SDK für Windows Server Solutions Sie den Namen der Medienbibliothek festzulegen. Um den Namen der Medienbibliothek festzulegen, können Sie die **SetMediaLibraryName** Methode der **MediaStreamingManager** -Klasse in der **Microsoft.WindowsServerSolutions.MediaStreaming** Namespace. Das folgende Beispiel zeigt, wie Sie den Namen der Medienbibliothek festgelegt:  
  
```c#  
  
MediaStreamingManager mediaStreamingManager = new MediaStreamingManager();  
string mediaLibraryName = Guid.NewGuid().ToString("B");   
mediaStreamingManager.SetMediaLibraryName(mediaLibraryName);  
  
```  
  
 Weitere Informationen finden Sie unter [SDK für Windows Server-Lösungen](https://go.microsoft.com/fwlink/?LinkID=248648).  
  
##  <a name="BKMK_StreamingQuality"></a>Festlegen der videostreamingqualität  
 Sie legen die videostreamingqualität, indem Sie die WinSAT-CPU-Bewertung abrufen und erstellen und installieren die XML-Datei, die die Informationen zur WinSAT-Bewertung enthält. Wenn die XML-Datei mit den Informationen zur WinSAT-Bewertung vor der Erstkonfiguration die Benutzeroberfläche zum Festlegen der Videoqualität werden nicht an den Kunden angezeigt installiert ist. Weitere Informationen finden Sie unter [Festlegen der WinSAT-Bewertung auf dem Server](Set-the-WinSAT-Score-on-the-Server.md).  
  
##  <a name="BKMK_Program"></a>Programmgesteuert aktivieren oder Deaktivieren von Medienstreaming  
 Sie können eine Klasse im SDK für Windows Server Solutions programmgesteuert aktivieren oder Deaktivieren von Medienstreaming. Zum Aktivieren oder Deaktivieren von Medienstreaming, können Sie die **SetMediaStreamingEnabled** Methode der **MediaStreamingManager** -Klasse in der **Microsoft.WindowsServerSolutions.MediaStreaming** Namespace. Im folgenden Codebeispiel wird veranschaulicht, wie Medienstreaming aktiviert:  
  
```c#  
  
MediaStreamingManager mediaStreamingManager = new MediaStreamingManager();  
mediaStreamingManager.SetMediaStreamingEnabled(true);  
  
```  
  
 Im folgenden Codebeispiel wird veranschaulicht, wie Medienstreaming deaktiviert:  
  
```c#  
  
MediaStreamingManager mediaStreamingManager = new MediaStreamingManager();  
mediaStreamingManager.SetMediaStreamingEnabled(false);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)