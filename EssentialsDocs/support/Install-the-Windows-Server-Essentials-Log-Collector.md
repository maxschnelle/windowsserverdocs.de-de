---
title: Installieren Sie die Windows Server Essentials Log Collector
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d271c54f-1ffa-464e-afa5-27b8df61854e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: ade18cec590392f35e7ad6b30d9a22ccdce44dcd
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="install-the-windows-server-essentials-log-collector"></a>Installieren Sie die Windows Server Essentials Log Collector

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Der Windows Server Essentials Log Collector-Installations-Assistent installiert den Log Collector als ein Launchpad-Add-in. Sie können installieren und verwenden den Log Collector auf Computern im Netzwerk oder dem Server. Nach der Installation wird der Log Collector auf dem Dashboard angezeigt.  
  
###  <a name="BKMK_ToInstall"></a>So installieren Sie den Log Collector  
  
1.  Herunterladen des Log Collector-Installationspakets auf einen Server oder Computer im Netzwerk.  
  
    > [!NOTE]
    >  Sie können [Herunterladen des Log Collector-Installationspakets](https://go.microsoft.com/fwlink/p/?LinkId=255470) aus dem Microsoft.  
  
2.  Doppelklicken Sie auf das Log Collector-Symbol.  
  
3.  Wenn Sie die Installation von einem Computer im Netzwerk ausführen, geben Sie Ihre Server-Administratoranmeldeinformationen ein, wenn Sie aufgefordert werden.  
  
4.  Wählen Sie die Microsoft Software-Lizenzbedingungen akzeptieren.  
  
5.  Um den Log Collector nur auf dem Server zu installieren, wählen Sie die **nur auf dem Server** Kontrollkästchen. Um den Log Collector auf allen Computern im Netzwerk zu installieren, wählen Sie die **auf dem Server und auf allen Computern im Netzwerk** Kontrollkästchen.  
  
6.  Klicken Sie auf **das Add-in installieren**.  
  
###  <a name="BKMK_Reinstall"></a>Neuinstallation des Log Collectors  
 Wenn der Log Collector neu installiert werden muss, müssen Sie deinstallieren und installieren den Log Collector auf dem Server und den Netzwerkcomputern im Netzwerk. Durch deinstallieren den Log Collector auf dem Server über das Dashboard, wird allen Computern im Netzwerk den Log Collector automatisch deinstalliert.  
  
##### <a name="to-uninstall-and-reinstall-the-log-collector"></a>So deinstallieren und installieren den Log Collector  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf die **-Add-in** Registerkarte **Log Collector** aus der Liste, und klicken Sie dann auf **Deinstallieren**.  
  

3.  Herunterladen und installieren Sie den Log Collector durch Ausführen der Schritte im vorherigen Verfahren [So installieren Sie den Log Collector](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_ToInstall).  

3.  Herunterladen und installieren Sie den Log Collector durch Ausführen der Schritte im vorherigen Verfahren [So installieren Sie den Log Collector](../support/Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_ToInstall).  

  
### <a name="manually-install-the-log-collector"></a>Installieren Sie den Log Collector manuell  
 Wenn der Installations-Assistent den Log Collector installieren, können Sie den Log Collector auf einem einzelnen Computer mithilfe des folgenden Verfahrens installieren.  
  
##### <a name="to-manually-install-the-log-collector"></a>So installieren Sie den Log Collector manuell  
  
1.  Benennen Sie die Erweiterung der heruntergeladenen Installationsdatei von wssx in CAB.  
  
2.  Doppelklicken Sie auf den Dateinamen für die Installation.  
  
3.  Klicken Sie auf **OK** , wenn Sie dazu aufgefordert werden.  
  
4.  Doppelklicken Sie auf den Namen der Datei mit ˜.msi endet, und wählen Sie einen Ordner, in dem er extrahiert werden sollen.  
  
5.  Navigieren Sie zum Ordner mit der extrahierten Datei, und doppelklicken Sie auf die Installationsdatei, um den Assistenten zu verwenden, um die Installation abzuschließen.
