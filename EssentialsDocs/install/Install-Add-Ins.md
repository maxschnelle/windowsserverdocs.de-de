---
title: Installieren von Add-Ins
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e62e4f07-c2ba-4c5e-b30c-bdc287cd654e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d00cb6886e812ee2b780ad79e1fba44442e279ad
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="install-add-ins"></a>Installieren von Add-Ins

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Sie können Add-Ins auf allen Server- oder Clientcomputer hinzufügen, indem Sie installieren, bevor Sie ein Image erstellen. Diese Add-Ins werden dann automatisch auf allen Computern, die mithilfe des Abbilds repliziert enthalten sein. Sie können entweder ein Add-In installieren, indem Sie die wssx-Datei ausführen, oder Sie können einzelne Add-in-Dateien installieren, indem Sie die Anweisungen in der [SDK-Dokumentation](https://go.microsoft.com/fwlink/?LinkID=248648)für jede Art von-Add-in. Wenn Sie mithilfe einer wssx-Datei installieren, kann das Add-in über den Add-In-Manager deinstalliert werden. Wenn Sie die einzelnen Dateien installieren, wird das Add-in nicht im Add-In-Manager verwaltet.  
  
> [!NOTE]
>  Jegliche Software, die installiert oder heruntergeladen werden, auf dem Server (einschließlich Registerkarten für das Dashboard und integritätsbenachrichtigungen) sollten eine lokalisierte Benutzeroberfläche aufweisen, die die Sprache des Betriebssystems entspricht, die auf dem Server installiert ist.  
  
#### <a name="to-install-an-add-in"></a>So installieren Sie ein Add-in  
  
1.  (Optional) Wenn Sie das Add-In installieren mithilfe einer wssx-Datei, führen Sie die folgenden Schritte aus:  
  
    1.  Speichern Sie die < AddinName\ > wssx-Datei auf dem Referenzcomputer.  
  
    2.  Doppelklicken Sie die wssx-Datei, um das Add-in-Installations-Assistenten zu öffnen.  
  
    3.  Führen Sie die Anweisungen im Assistenten, um die Installation abzuschließen.  
  
2.  (Optional) Installieren Sie die einzelnen Add-in-Dateien in den entsprechenden Speicherorten im SDK für die einzelnen Add-in-definiert.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)