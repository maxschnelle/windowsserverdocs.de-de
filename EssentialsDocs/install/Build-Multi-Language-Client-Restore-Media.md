---
title: Erstellen des mehrsprachigen Mediums zur Clientwiederherstellung
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2fdbc016-d464-43cb-bd75-8a63e61588a2
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 1ad934d297c3092050bd6adbb6bb0f50d1ec6f36
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="build-multi-language-client-restore-media"></a>Erstellen des mehrsprachigen Mediums zur Clientwiederherstellung

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

> [!NOTE]
>  Sie müssen zuerst ein mehrsprachiges Windows-Image erstellen, wie beschrieben in die [Exemplarische Vorgehensweise: mehrsprachige Windows-Imageerstellung](https://technet.microsoft.com/library/jj126995) , bevor Sie die Windows Server Essentials--Sprachpaket in install.wim hinzufügen.  
  
 Beim Erstellen der mehrsprachigen Serverinstallations-DVD werden für Server "Install.wim" Sprachpakete installiert. Die lokalisierten Ressourcen für Assistenten werden als Bestandteil des Sprachpakets installiert werden.  
  
### <a name="to-build-a-multi-language-client-restore-media"></a>Ein Client mehrsprachigen Wiederherstellungsmedium erstellen  
  
1.  Laden Sie "Install.wim" am c:\mount, rufen wir c:\mount\Program Files\Windows Server\bin\ClientRestore Ordner als Stammverzeichnis des Mediums zur clientwiederherstellung: [RestoreMediaRoot] im folgenden:  
  
    ```  
    dism /mount-wim /wimfile:install.wim /index:1 /mountdir:c:\mount  
    ```  
  
2.  Binden Sie die Clients Wiederherstellung WIM-Datei am [RestoreMediaRoot]\Sources\Boot.wim (müssen dieselben Schritte auch für "boot_x86.wim" ausgeführt werden). Die Befehlszeile lautet:  
  
    ```  
    dism /mount-wim /wimfile:boot.wim /index:1 /mountdir:c:\mountRestore  
    ```  
  
3.  Fügen Sie WinPE-Setup.cab Paket, das Wiederherstellungsmedium durch ausführen:  
  
    ```  
    dism /image:c:\mountRestore /add-package /packagepath:WinPE-Setup.cab  
    ```  
  
4.  Mit dem Editor c:\mountRestore\windows\system32\winpeshl.ini bearbeiten, fügen Sie folgenden Inhalt:  
  
    ```  
    [LaunchApp]  
    AppPath = %SYSTEMDRIVE%\sources\SelectLanguage.exe  
    ```  
  
5.  Das Wiederherstellungsmedium Sprachpakete hinzufügen. Hinzufügen von Language Packs kann durch Ausführen des folgenden Befehls erfolgen:  
  
    ```  
    dism /image:c:\mountRestore /add-package /packagepath:[language pack path]  
    ```  
  
     Folgende Sprachpakete hinzugefügt werden müssen:  
  
    1.  WinPE-Sprachpaket (lp.cab)  
  
    2.  WinPE-Setup-Sprachpaket (WinPE-Setup_ [Lang] .cab, z. B. WinPE-Setup_en-us.cab)  
  
    3.  Für asiatische Schriftarten wie Zh-Cn, Zh-Tw, Zh-Hk, Ko-Kr, ja-jp, zusätzliches Schriftartenpaket installiert werden (Winpe - Fontsupport-[Sprache] .cab, z. B. Winpe-Fontsupport-Zh-cn.cab)  
  
6.  Generieren Sie neue Datei "lang.ini", durch ausführen:  
  
    ```  
    dism /image:c:\mountRestore /Gen-LangINI /distribution:mount  
    ```  
  
7.  Übernehmen und Aufheben der Bereitstellung der Images, durch ausführen:  
  
    ```  
    dism /unmount-wim /mountdir:c:\mountRestore /commit  
    ```  
  
8.  Wiederholen Sie Schritt 2 bis 7 für [RestoreMediaroot]\Sources\Boot_x86.wim.  
  
9. Übernehmen und Aufheben der Bereitstellung der Images, durch ausführen:  
  
    ```  
    dism /unmount-wim /mountdir:c:\mount /commit  
    ```  
  
## <a name="see-also"></a>Siehe auch  

 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)

 [Erstellen und Anpassen des Abbilds](../install/Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](../install/Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](../install/Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](../install/Testing-the-Customer-Experience.md)

