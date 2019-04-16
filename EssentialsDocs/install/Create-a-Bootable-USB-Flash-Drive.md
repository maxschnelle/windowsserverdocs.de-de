---
title: Erstellen eines startbaren USB-Speichersticks
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2fe8e35c-69f9-40b3-a270-22e2402510d8
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 9d587329e1141040b2511e1574649f1844dcec90
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-bootable-usb-flash-drive"></a>Erstellen eines startbaren USB-Speichersticks

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Sie können einen startbaren USB-Speicherstick zum Bereitstellen von Windows Server Essentials erstellen. Der erste Schrittist das USB-Flashlaufwerk mithilfe von DiskPart, dies ist ein Befehlszeilen-Hilfsprogramm vorbereiten. Weitere Informationen zu DiskPart finden Sie unter [DiskPart-Befehlszeilenoptionen ](https://go.microsoft.com/fwlink/?LinkId=207073).  
  
 Weitere Szenarien, in dem Sie möchten möglicherweise erstellen oder verwenden Sie ein startbares USB, Flash-Laufwerk, finden Sie unter den folgenden Themen:  
  
-   [Wiederherstellen eines vollständigen Systems aus einer vorhandenen clientcomputersicherung](https://technet.microsoft.com/library/jj713539.aspx#BKMK_CreateBootable)  
  
-   [Wiederherstellen Sie oder reparieren Sie des Servers mit Windows Server Essentials](https://technet.microsoft.com/library/jj593197.aspx#BKMK_Restore_2)  
  
### <a name="to-create-a-bootable-usb-flash-drive"></a>Erstellen ein startbares USB-Speichersticks  
  
1.  Legen Sie einen USB-Speicherstick an einen eingeschalteten Computer.  
  
2.  Öffnen Sie ein Eingabeaufforderungsfenster als Administrator.  
  
3.  Typ `diskpart`.  
  
4.  Geben Sie in dem neu geöffneten Befehlszeilenfenster, die geöffnet wird, um zu bestimmen, die USB-Flashlaufwerk Laufwerknummer oder des Laufwerkbuchstabens an der Eingabeaufforderung, `list disk`, und drücken Sie die EINGABETASTE. Die `list disk`Befehl zeigt alle Datenträger auf dem Computer. Beachten Sie die Laufwerknummer oder der Laufwerkbuchstabe des USB-Speichersticks.  
  
5.  Geben Sie an der Eingabeaufforderung `select disk <X>`, wobei X die Laufwerknummer ist oder der Laufwerkbuchstabe des USB-Speicherstick, und drücken Sie die EINGABETASTE.  
  
6.  Typ `clean`, und Sie dann die EINGABETASTE. Dieser Befehl löscht alle Daten vom USB-Speicherstick.  
  
7.  Um eine neue primäre Partition auf dem USB-Speicherstick zu erstellen, geben `create part pri`, und drücken Sie die EINGABETASTE.  
  
8.  Um die Partition auszuwählen, die Sie gerade erstellt haben, geben `select part 1`, und drücken Sie die EINGABETASTE.  
  
9. Um die Partition zu formatieren, geben `format fs=ntfs quick`, und drücken Sie die EINGABETASTE.  
  
    > [!IMPORTANT]
    >  Wenn Ihre Serverplattform Unified Extensible Firmware Interface (UEFI) unterstützt, sollten Sie den USB-Speicherstick als FAT32 und nicht als NTFS formatieren. Um die Partition als FAT32 zu formatieren, geben `format fs=fat32 quick`, und drücken Sie die EINGABETASTE.  
  
10. Typ `active`, und drücken Sie die EINGABETASTE.  
  
11. Typ `exit`, und drücken Sie die EINGABETASTE.  
  
12. Wenn Sie die Vorbereitung des benutzerdefinierten Abbilds abgeschlossen haben, speichern Sie sie in das Stammverzeichnis des USB-Speicherstick.  
  
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

 [Wie können wir Ihnen helfen?](https://windows.microsoft.com/windows/support)
