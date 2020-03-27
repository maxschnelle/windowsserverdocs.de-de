---
title: Wichtige Informationen zur Verwendung von Windows Server Essentials ADK
description: Beschreibt die Verwendung von Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 26cb2992-1250-4672-98ee-8b870baa45d5
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 9a06f3b6431ae6079869e1d7fe9bc3f0ef5e597b
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80311746"
---
# <a name="important-information-for-using-the-windows-server-essentials-adk"></a>Wichtige Informationen zur Verwendung von Windows Server Essentials ADK

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Zum Erstellen und Anpassen eines Images von Windows Server Essentials verwenden Sie viele der Tools im [Windows 8 ADK](https://go.microsoft.com/fwlink/?LinkId=248647). es gibt jedoch einige wichtige Unterschiede zwischen dem Windows 8 ADK und dem Windows Server Essentials ADK.  
  
 Sie sollten sich der folgenden wichtigen Unterschiede bewusst sein:  
  
-   In **%windir%\setup\script\SetupComplete.cmd** wurden bestimmte Einstellungen geändert. Wenn Sie diesen Befehl verwenden möchten, können Sie weitere Befehlszeilen hinzufügen, jedoch keine vorhandenen Zeilen löschen.  
  
## <a name="working-with-passwords"></a>Arbeiten mit Kennwörtern  
  
-   Das Kennwort des Administrators ist auf Admin@123 festgelegt, und die automatische Anmeldung wird in der Datei "install. wim\unattend.xml" aktiviert. Daher ist es nicht erforderlich, das Kennwort während der Erstkonfiguration des Servers mehrere Male einzugeben. Wenn im Stammverzeichnis des Wechselmediums eine benutzerdefinierte Datei "unattend.xml" vorhanden ist, werden diese Einstellungen überschrieben, und Sie müssen das Kennwort und die Anmeldung während des Starts festlegen.  
  
-   Während der Erstkonfiguration wird der Endbenutzer aufgefordert, ein neues Konto und ein Kennwort zu erstellen. Dieses neue Konto wird das Netzwerkadministratorkonto für das Betriebssystem. Das Administratorkonto und die automatische Anmeldung werden anschließend deaktiviert. Sie können diesen Vorgang mithilfe der Datei "Cfg.ini" für Tests zur Qualitätssicherung automatisieren.  
  
-   Ausführliche Informationen zum Erstellen einer Datei „unattend.xml“ finden Sie in der Dokumentation zum [Windows 8 ADK](https://go.microsoft.com/fwlink/?LinkId=248694) .  
  
## <a name="see-also"></a>Weitere Informationen  

 [Die ersten Schritte mit dem Windows Server Essentials ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md) -   
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)

 [Die ersten Schritte mit dem Windows Server Essentials ADK](../install/Getting-Started-with-the-Windows-Server-Essentials-ADK.md) -   
 [Erstellen und Anpassen des Abbilds](../install/Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](../install/Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](../install/Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](../install/Testing-the-Customer-Experience.md)

