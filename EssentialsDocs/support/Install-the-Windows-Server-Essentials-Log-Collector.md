---
title: Installieren des Windows Server Essentials-Protokollsammlers
description: Beschreibt, wie Windows Server Essentials
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837031"
---
# <a name="install-the-windows-server-essentials-log-collector"></a>Installieren des Windows Server Essentials-Protokollsammlers

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Der Windows Server Essentials Log Collector-Installations-Assistent installiert den Log Collector als ein Launchpad-Add-in. Sie können den Log Collector auf Computern im Netzwerk oder dem Server oder beidem installieren und verwenden. Nach der Installation wird der Log Collector auf dem Dashboard angezeigt.  
  
###  <a name="BKMK_ToInstall"></a> So installieren Sie den Log Collector  
  
1.  Laden Sie das Log Collector -Installationspaket auf einen beliebigen Server oder einen Computer im Netzwerk herunter.  
  
    > [!NOTE]
    >  Von der Microsoft- Website können Sie [das Installationspaket für den Log Collector herunterladen](https://go.microsoft.com/fwlink/p/?LinkId=255470) .  
  
2.  Doppelklicken Sie auf das Log Collector-Symbol.  
  
3.  Wenn Sie die Installation von einem Computer im Netzwerk ausführen, geben Sie Ihre Server-Administratoranmeldeinformationen ein, wenn Sie aufgefordert werden.  
  
4.  Akzeptieren Sie die Microsoft-Software-Lizenzbedingungen.  
  
5.  Um den Log Collector nur auf dem Server zu installieren, aktivieren Sie das **nur auf dem Server** Kontrollkästchen. Um den Log Collector auf allen Computern im Netzwerk zu installieren, aktivieren Sie das **auf dem Server und auf allen Computern im Netzwerk** Kontrollkästchen.  
  
6.  Klicken Sie auf **Add-in installieren**.  
  
###  <a name="BKMK_Reinstall"></a> Neuinstallation des Log Collectors  
 Wenn der Log Collector neu installiert werden muss, müssen Sie den Log Collector auf dem Server und den Netzwerkcomputern im Netzwerk deinstallieren und neu installieren. Durch Deinstallieren des Log Collectors auf dem Server über das Dashboard, wird der Log Collector auf allen Netzwerk-Computern automatisch deinstalliert.  
  
##### <a name="to-uninstall-and-reinstall-the-log-collector"></a>So deinstallieren Sie den Log Collector und installieren ihn neu  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Wählen Sie auf der **Add-in** Registerkarte **Log Collector** aus der Liste aus und klicken Sie dann auf **Deinstallieren**.  
  

3.  Laden Sie den Log Collector herunter, und führen Sie die Schritte im vorherigen Verfahren, [To install the Log Collector](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_ToInstall), aus.  

3.  Laden Sie den Log Collector herunter, und führen Sie die Schritte im vorherigen Verfahren, [To install the Log Collector](../support/Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_ToInstall), aus.  

  
### <a name="manually-install-the-log-collector"></a>Den Log Collector manuell installieren  
 Wenn der Installations-Assistent den Log Collector nicht installieren konnte, können Sie den Log Collector auf einem einzelnen Computer mithilfe des folgenden Verfahrens installieren.  
  
##### <a name="to-manually-install-the-log-collector"></a>So installieren Sie den Log Collector manuell  
  
1.  Benennen Sie die Erweiterung der heruntergeladenen Installationsdatei von wssx in .cab.  
  
2.  Doppelklicken Sie auf den Dateinamen der Installationsdatei.  
  
3.  Klicken Sie auf **OK** , wenn Sie dazu aufgefordert werden.  
  
4.  Doppelklicken Sie auf den Dateinamen mit ˜.msi endet, und wählen Sie einen Ordner, in dem er extrahiert werden sollen.  
  
5.  Navigieren Sie zu dem Ordner mit der extrahierten Datei und doppelklicken Sie auf die Installationsdatei, um den Assistenten zum Abschluss der Installation zu verwenden.
