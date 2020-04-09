---
title: Erstellen eines startfähigen USB-Speichersticks
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 05/04/2018
ms.prod: windows-server
ms.topic: article
ms.assetid: 2fe8e35c-69f9-40b3-a270-22e2402510d8
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: ddcdb9576072af6b7014f6dc9b0c38e9f5bdd25d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80818363"
---
# <a name="create-a-bootable-usb-flash-drive"></a>Erstellen eines startfähigen USB-Speichersticks

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Sie können einen Start baren USB-Speicherstick erstellen, um Windows Server Essentials bereitzustellen. Der erste Schritt ist die Vorbereitung des USB-Speichersticks mithilfe von DiskPart, einem Befehlszeilenprogramm. Information zu DiskPart finden Sie auf der Seite zu [DiskPart-Befehlszeilenoptionen](https://go.microsoft.com/fwlink/?LinkId=207073).  


> [!TIP]
> Informationen zum Erstellen eines Start fähigen USB-Speicherstick für die Wiederherstellung oder Neuinstallation von Windows auf einem PC anstelle eines Servers finden Sie unter [Erstellen eines Wiederherstellungs Laufwerks](https://support.microsoft.com/help/4026852/windows-create-a-recovery-drive).
  
 Zusätzliche Szenarien, in denen Sie möglicherweise einen bootfähigen USB-Speicherstick einrichten oder verwenden möchten, finden Sie in den folgenden Themen:  
  
-   [Wiederherstellen eines vollständigen Systems aus einer vorhandenen Clientcomputersicherung](../manage/restore-a-full-system-from-an-existing-client-computer-backup.md)  
  
-   [Wiederherstellen oder Reparieren des Servers mit Windows Server Essentials](../manage/restore-or-repair-your-server-running-windows-server-essentials.md)  

  
### <a name="to-create-a-bootable-usb-flash-drive"></a>So erstellen Sie einen startfähigen USB-Speicherstick  
  
1.  Verbinden Sie einen USB-Speicherstick mit einem eingeschalteten Computer.  
  
2.  Öffnen Sie ein Eingabeaufforderungsfenster als Administrator.  
  
3.  Geben Sie `diskpart` ein.  
  
4.  Geben Sie in dem neu geöffneten Befehlszeilenfenster zum Ermitteln der Laufwerknummer oder des Laufwerkbuchstabens des USB-Speichersticks an der Eingabeaufforderung `list disk` ein, und drücken Sie dann die EINGABETASTE. Mit dem Befehl `list disk` werden alle Datenträger im Computer angezeigt. Notieren Sie sich die Laufwerknummer oder den Laufwerkbuchstaben des USB-Speichersticks.  
  
5.  Geben Sie an der Eingabeaufforderung `select disk <X>` ein, wobei X die Laufwerknummer oder der Laufwerkbuchstabe des USB-Speichersticks ist, und drücken Sie dann die EINGABETASTE.  
  
6.  Geben Sie `clean`ein, und drücken Sie dann die EINGABETASTE. Mit diesem Befehl werden alle Daten vom USB-Speicherstick gelöscht.  
  
7.  Um eine neue primäre Partition auf dem USB-Speicherstick zu erstellen, geben Sie `create partition primary` ein, und drücken Sie dann die EINGABETASTE.  
  
8.  Um die soeben erstellte Partition auszuwählen, geben Sie `select partition 1`ein, und drücken Sie dann die EINGABETASTE.  
  
9. Um die Partition zu formatieren, geben Sie `format fs=ntfs quick`ein, und drücken Sie dann die EINGABETASTE.  
  
    > [!IMPORTANT]
    >  Wenn Ihre Serverplattform Unified Extensible Firmware Interface (UEFI) unterstützt, sollten Sie den USB-Speicherstick als FAT32 und nicht als NTFS formatieren. Um die Partition als FAT32 zu formatieren, geben Sie `format fs=fat32 quick`ein, und drücken Sie dann die EINGABETASTE.  
  
10. Geben Sie `active`ein, und drücken Sie dann die EINGABETASTE.  
  
11. Geben Sie `exit`ein, und drücken Sie dann die EINGABETASTE.  
  
12. Wenn Sie die Vorbereitung des benutzerdefinierten Abbilds abgeschlossen haben, speichern Sie es im Stamm des USB-Speichersticks.  
  
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

 [Wie können wir Ihnen helfen?](https://windows.microsoft.com/windows/support)
