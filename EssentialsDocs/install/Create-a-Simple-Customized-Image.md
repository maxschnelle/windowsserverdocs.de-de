---
title: Erstellen eines einfachen benutzerdefinierten Abbilds
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 29f9a09f-e4e8-476d-ada1-ab9202a670d7
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: e18ff5ded94127449072d28d00b98e17dbe63c3a
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="create-a-simple-customized-image"></a>Erstellen eines einfachen benutzerdefinierten Abbilds

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Sie können das folgende Verfahren verwenden, für das Erstellen eines einfachen benutzerdefinierten Abbilds:  
  
#### <a name="to-create-the-image"></a>Zum Erstellen des Images  
  
1.  Drücken Sie nach der Serverinstallation auf der ersten Seite der Erstkonfiguration UMSCHALT+F10, um das Befehlsfenster zu starten.  
  
2.  Erstellen Sie eine Datei "SkipIC.txt" im Stammverzeichnis des Systemlaufwerks.  
  
3.  Starten Sie den Server neu.  
  
4.  Starten Sie den Server mithilfe eines USB-Speicherstick oder DVD, das die unattend.xml-Datei enthält. Informationen zum Erstellen eines startbaren USB-Speichersticks finden Sie unter [erstellen Sie ein startbares USB-Flash-Laufwerk](Create-a-Bootable-USB-Flash-Drive.md).  
  
5.  Fügen Sie dem Dashboard ein Logo als Branding hinzu. Weitere Informationen zum Hinzufügen von Branding finden Sie unter [Add Branding to das Dashboard, Remotewebzugriff und zum Launchpad](Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md).  
  
6.  Erstellen Sie die OOBE.xml-Datei, um benutzerdefinierte Informationen wie Unternehmensname, Logo und EULA anzuzeigen. Weitere Informationen zur Datei "OOBE.xml" finden Sie unter [erstellen Sie die Oobe.xml File Including Logo und EULA](Create-the-Oobe.xml-File-Including-Logo-and-EULA.md).  
  
7.  Ändern Sie den standardmäßigen Servernamen, wenn Sie es nicht in unattend.xml definieren.  
  
8.  Standardmäßig werden der Servername einer zufälligen Zeichenfolge. Ändern Sie den Namen des Servers in eine andere Zeichenfolge (z.B. ContosoServer), und informieren Sie Ihre Kunden über den neuen Namen.  
  
9. Vorbereiten des Abbilds für die Bereitstellung unter [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Erste Schritte mit Windows Server Essentials ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)