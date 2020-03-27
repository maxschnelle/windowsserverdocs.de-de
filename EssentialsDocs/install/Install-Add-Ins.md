---
title: Installieren von Add-Ins
description: Beschreibt die Verwendung von Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e62e4f07-c2ba-4c5e-b30c-bdc287cd654e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 9f3c952df01f44f29d1e7b39e1ffb8e04c931945
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80311686"
---
# <a name="install-add-ins"></a>Installieren von Add-Ins

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Wenn Sie Add-Ins vor der Erstellung eines Abbilds installieren, können diese auf allen Server- oder Clientcomputern einbezogen werden. Diese Add-Ins werden dann automatisch auf allen Computern einbezogen, die mithilfe des Abbilds repliziert werden. Sie können entweder ein Add-In installieren, indem Sie die WSSX-Datei ausführen, oder einzelne Add-In-Dateien installieren, indem Sie die Anweisungen in der [SDK-Dokumentation](https://go.microsoft.com/fwlink/?LinkID=248648)für die einzelnen Add-In-Typen ausführen. Wenn Sie Add-Ins mithilfe einer WSSX-Datei installieren, kann das Add-In über den Add-In-Manager deinstalliert werden. Wenn Sie die einzelnen Dateien installieren, wird das Add-In nicht im Add-In-Manager verwaltet.  
  
> [!NOTE]
>  Jegliche Software, die auf dem Server installiert bzw. auf diesen heruntergeladen wird (einschließlich Registerkarten für das Dashboard und Integritätsbenachrichtigungen), sollten eine lokalisierte Benutzeroberfläche aufweisen, die der Sprache des auf dem Server installierten Betriebssystems entspricht.  
  
#### <a name="to-install-an-add-in"></a>So installieren Sie ein Add-In  
  
1.  (Optional) Führen Sie die folgenden Schritte aus, wenn Sie das Add-In mithilfe einer WSSX-Datei installieren:  
  
    1.  Speichern Sie die Datei < AddInName\>. wssx auf dem Referenz Computer.  
  
    2.  Doppelklicken Sie auf die WSSX-Datei, um den Assistenten für die Add-In-Installation zu öffnen.  
  
    3.  Befolgen Sie die Anweisungen im Assistenten, um die Installation abzuschließen.  
  
2.  (Optional) Installieren Sie die einzelnen Add-In-Dateien unter den im SDK für jeden Add-In-Typ festgelegten Pfaden.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)