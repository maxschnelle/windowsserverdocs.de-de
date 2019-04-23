---
title: 'Schritt 3: Hinzufügen von Computern zum neuen Windows Server Essentials-Server'
description: Beschreibt, wie Windows Server Essentials
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861871"
---
# <a name="step-3-join-computers-to-the-new-windows-server-essentials-server"></a>Schritt 3: Hinzufügen von Computern zum neuen Windows Server Essentials-Server

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Der nächste Schritt im Migrationsprozess werden Clientcomputer mit dem neuen Server mit Windows Server Essentials verbinden.  
  
> [!NOTE]
>  Sie können diesen Schritt bei Computern überspringen, auf denen die Betriebssysteme Windows XP oder Windows Vista ausgeführt werden. Computer, auf denen Windows XP oder Windows Vista ausgeführt werden, werden von der Windows Server-Connector-Software nicht unterstützt.  
  
 Bevor Sie einen Clientcomputer mit dem neuen Windows Server Essentials-Server anmelden können, müssen Sie es vom Quellserver trennen, durch die Windows Server-Connector-Software auf dem Clientcomputer deinstallieren.  
  
### <a name="to-uninstall-windows-server-connector-on-a-client-computer"></a>So deinstallieren Sie Windows Server-Connector auf einem Clientcomputer  
  
1.  Öffnen Sie auf einem Clientcomputer die Systemsteuerung und dann **Programme und Funktionen**.  
  
2.  Klicken Sie in der Liste der Programme mit der rechten Maustaste auf die Connector-Anwendung, die auf dem Computer ausgeführt wird.  
  
    > [!NOTE]
    >  Die Connector-Anwendung möglich **Windows Small Business Server 2011 Essentials Connector**, oder **Windows Server Essentials Connector**, je nachdem, welche Version von Windows Server Essentials die Clientcomputer angeschlossen war auf.  
  
3.  Klicken Sie auf **Deinstallieren**.  
  
### <a name="to-reconnect-a-client-computer-to-the-server"></a>So verbinden Sie einen Clientcomputer erneut mit dem Server  
  
1.  Melden Sie sich an dem Computer an, den Sie mit dem Server verbinden möchten.  
  
    > [!NOTE]
    >  Wenn auf diesem Computer mehrere Benutzerkonten vorhanden sind, melden Sie sich mit dem Benutzerkonto an, dessen Dokumente, Bilder und persönliche Einstellungen Sie nach dem Verbinden mit dem Server beibehalten möchten.  
  
2.  Öffnen Sie einen Internetbrowser, z. B. Internet Explorer.  
  
3.  Geben Sie in der Adressleiste **http://<servername\>/Connect**, und drücken Sie dann die EINGABETASTE.  
  
4.  Führen Sie die Anweisungen auf dem Bildschirm, auf den Clientcomputer mit dem neuen Windows Server Essentials-Server hinzufügen.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Sie haben die Clientcomputer auf den neuen Server mit Windows Server Essentials verbunden. Wechseln Sie nun zur [Schritt 4: Verschieben von Einstellungen und Daten auf den Zielserver für Windows Server Essentials-Migration](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  
  

Alle Schritte finden Sie unter [Migrieren zu Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).

