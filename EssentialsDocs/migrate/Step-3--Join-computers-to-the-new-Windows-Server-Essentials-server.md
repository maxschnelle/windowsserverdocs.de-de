---
title: "Schritt3: Hinzufügen von Computern zum neuen Windows Server Essentials-Server"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0e07d1a-8409-429b-87d7-0f4a7e14d668
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: f71ac280e2de0b7d945f2d979fe52d173f7c3323
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="step-3-join-computers-to-the-new-windows-server-essentials-server"></a>Schritt3: Hinzufügen von Computern zum neuen Windows Server Essentials-Server

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Der nächste Schrittdes Migrationsvorgangs ist auf Clientcomputern auf den neuen Server mit Windows Server Essentials zu verbinden.  
  
> [!NOTE]
>  Sie können diesen Schrittbei Computern überspringen, auf denen Windows XP oder Windows Vista-Betriebssysteme ausgeführt werden. Computer, auf denen Windows XP oder Windows Vista ausgeführt werden, werden von die Windows Server-Connector-Software nicht unterstützt.  
  
 Bevor Sie einen Clientcomputer mit dem neuen Windows Server Essentials-Server anmelden können, müssen Sie es vom Quellserver trennen, indem Sie die Windows Server-Connector-Software auf dem Clientcomputer deinstallieren.  
  
### <a name="to-uninstall-windows-server-connector-on-a-client-computer"></a>So deinstallieren Sie Windows Server-Connector auf einem Clientcomputer  
  
1.  Von einem Clientcomputer aus öffnen Sie die Systemsteuerung, und öffnen Sie dann **Programme und Funktionen**.  
  
2.  Klicken Sie in der Liste der Programme auf die Connector-Anwendung, die auf Ihrem Computer ausgeführt wird.  
  
    > [!NOTE]
    >  Die Connector-Anwendung kann **Windows Small Business Server2011 Essentials Connector**, oder **Windows Server Essentials Connector**, je nachdem, auf welche Version von Windows Server Essentials auf die Clientcomputer angeschlossen war.  
  
3.  Klicken Sie auf **Deinstallieren**.  
  
### <a name="to-reconnect-a-client-computer-to-the-server"></a>Einen Clientcomputer mit dem Server wiederherstellen  
  
1.  Melden Sie sich an den Computer, den Sie mit dem Server verbinden möchten.  
  
    > [!NOTE]
    >  Wenn auf diesem Computer mehrere Benutzerkonten vorhanden sind, melden Sie sich mit dem Benutzerkonto, das dessen Dokumente, Bilder und persönliche Einstellungen, die Sie nach dem Verbinden des Computers mit dem Server beibehalten möchten.  
  
2.  Öffnen Sie einen Internetbrowser, z. B. Internet Explorer.  
  
3.  Geben Sie in der Adressleiste **http://<servername\>/Connect**, und drücken Sie dann die EINGABETASTE.  
  
4.  Führen Sie die Anweisungen auf dem Bildschirm, um den Clientcomputer mit dem neuen Windows Server Essentials-Server hinzufügen.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Sie haben die Clientcomputer mit dem neuen Server mit Windows Server Essentials verbunden. Lesen Sie jetzt [Schritt4: Verschieben von Einstellungen und Daten auf den Zielserver für Windows Server Essentials-Migration](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  
  

Alle Schrittefinden Sie unter [Migrieren zu Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).

