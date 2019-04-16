---
title: "Wichtige Informationen für die Verwendung von Windows Server Essentials ADK"
description: Beschreibt, wie Sie Windows Server Essentials
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="important-information-for-using-the-windows-server-essentials-adk"></a>Wichtige Informationen für die Verwendung von Windows Server Essentials ADK

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Zum Erstellen und Anpassen eines Images von Windows Server Essentials, verwenden Sie viele der Tools in der [Windows 8 ADK](https://go.microsoft.com/fwlink/?LinkId=248647), aber es einige wichtige Unterschiede zwischen Windows 8 ADK und dem Windows Server Essentials ADK gibt.  
  
 Sie sollten die folgenden wichtigen Unterschiede bewusst sein:  
  
-   Einige Einstellungen in geändert wurden **%windir%\setup\script\SetupComplete.cmd**. Wenn Sie diesen Befehl verwenden möchten, können weitere Befehlszeilen hinzufügen, aber entfernen Sie die vorhandenen Zeilen nicht aus.  
  
## <a name="working-with-passwords"></a>Arbeiten mit Kennwörtern  
  
-   Das Kennwort des Administrators wird festgelegt, um Admin@123 und die automatische Anmeldung in der Install.wim\unattend.xml aktiviert ist. Aus diesem Grund müssen Sie nicht das Kennwort mehrere Male während der Erstkonfiguration des Servers erneut ein. Wenn Sie eine angepasste Datei "Unattend.xml" in das Stammverzeichnis des Wechselmediums haben, diese Einstellungen überschrieben werden und Sie festlegen müssen starten das Kennwort und die Anmeldung bei der...  
  
-   Während der Erstkonfiguration wird der Benutzer aufgefordert, ein neues Konto und Kennwort zu erstellen. Dieses neue Konto wird das netzwerkadministratorkonto für das Betriebssystem. Der Administrator und die automatische Anmeldung ist deaktiviert. Sie können diesen Vorgang automatisieren, mithilfe der Datei "cfg.ini" für Qualität Assurance zu testen.  
  
-   Finden Sie in der [Windows 8 ADK](https://go.microsoft.com/fwlink/?LinkId=248694) Dokumentation weitere Informationen zum Erstellen einer Datei "Unattend.xml".  
  
## <a name="see-also"></a>Siehe auch  

 [Erste Schritte mit Windows Server Essentials ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)

 [Erste Schritte mit Windows Server Essentials ADK](../install/Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [Erstellen und Anpassen des Abbilds](../install/Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](../install/Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](../install/Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](../install/Testing-the-Customer-Experience.md)

