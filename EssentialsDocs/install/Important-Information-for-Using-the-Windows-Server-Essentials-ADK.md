---
title: Wichtige Informationen zur Verwendung von Windows Server Essentials ADK
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 26cb2992-1250-4672-98ee-8b870baa45d5
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 4dec1fdf01538ca119b991675f932d2d8ec1e097
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838641"
---
# <a name="important-information-for-using-the-windows-server-essentials-adk"></a>Wichtige Informationen zur Verwendung von Windows Server Essentials ADK

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Zum Erstellen und Anpassen eines Abbilds von Windows Server Essentials, verwenden Sie viele der Tools in der [Windows 8 ADK](https://go.microsoft.com/fwlink/?LinkId=248647), aber es einige wichtige Unterschiede zwischen dem Windows 8 ADK und dem Windows Server Essentials ADK gibt.  
  
 Sie sollten sich der folgenden wichtigen Unterschiede bewusst sein:  
  
-   In **%windir%\setup\script\SetupComplete.cmd** wurden bestimmte Einstellungen geändert. Wenn Sie diesen Befehl verwenden möchten, können Sie weitere Befehlszeilen hinzufügen, jedoch keine vorhandenen Zeilen löschen.  
  
## <a name="working-with-passwords"></a>Arbeiten mit Kennwörtern  
  
-   Das Kennwort des Administrators wird festgelegt, um Admin@123 und die automatische Anmeldung in der Install.wim\unattend.xml aktiviert ist. Daher ist es nicht erforderlich, das Kennwort während der Erstkonfiguration des Servers mehrere Male einzugeben. Wenn im Stammverzeichnis des Wechselmediums eine benutzerdefinierte Datei "unattend.xml" vorhanden ist, werden diese Einstellungen überschrieben, und Sie müssen das Kennwort und die Anmeldung während des Starts festlegen.  
  
-   Während der Erstkonfiguration wird der Endbenutzer aufgefordert, ein neues Konto und ein Kennwort zu erstellen. Dieses neue Konto wird das Netzwerkadministratorkonto für das Betriebssystem. Das Administratorkonto und die automatische Anmeldung werden anschließend deaktiviert. Sie können diesen Vorgang mithilfe der Datei "Cfg.ini" für Tests zur Qualitätssicherung automatisieren.  
  
-   Ausführliche Informationen zum Erstellen einer Datei „unattend.xml“ finden Sie in der Dokumentation zum [Windows 8 ADK](https://go.microsoft.com/fwlink/?LinkId=248694) .  
  
## <a name="see-also"></a>Siehe auch  

 [Erste Schritte mit Windows Server Essentials ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Zusätzliche Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)

 [Erste Schritte mit Windows Server Essentials ADK](../install/Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [Erstellen und Anpassen des Abbilds](../install/Creating-and-Customizing-the-Image.md)   
 [Zusätzliche Anpassungen](../install/Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](../install/Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](../install/Testing-the-Customer-Experience.md)

