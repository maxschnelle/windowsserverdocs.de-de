---
title: "Erstellen Sie die Datei \"PostIC.cmd\" zum Ausführen von Aufgaben nach der Erstkonfiguration"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99e258bc-0695-48c9-b694-a7f3cbe2a2d0
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: f5042204cd189e3101f5e0126fd98e786a49032d
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="create-the-posticcmd-file-for-running-post-initial-configuration-tasks"></a>Erstellen Sie die Datei "PostIC.cmd" zum Ausführen von Aufgaben nach der Erstkonfiguration

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Sie können Anpassungen nach der Erstkonfiguration hinzufügen, indem Sie eigenen Code schreiben, und klicken Sie dann diesen Code über eine Skriptdatei mit dem Namen PostIC.cmd aufrufen. Wenn Sie die PostIC.cmd-Datei zu verwenden, müssen Sie die folgenden Richtlinien beachtet werden:  
  
-   Der Anpassungscode muss im Hintergrund ausgeführt werden (es kann nicht in eine Benutzeroberfläche angezeigt).  
  
-   Einen Neustart des Servers kann nicht durch den Anpassungscode initiiert werden. Die Erstkonfiguration wird den Server im letzten Task neu gestartet.  
  
-   Der Anpassungscode muss in drei Minuten oder weniger ausgeführt.  
  
 Definieren Sie die PostIC.cmd-Datei, um eine 0 zurückgegeben, wenn der Code erfolgreich ausgeführt wird. Wenn ein anderer Wert zurückgegeben wird, sucht das Betriebssystem nach einer Datei namens ["setupfailure.cmd"](Create-the-PostIC.cmd-File-for-Running-Post-Initial-Configuration-Tasks.md#BKMK_SetupFailure), enthält Code, der ausgeführt werden soll, wenn der Code in der PostIC.cmd-Datei nicht erfolgreich ausgeführt wurde. PostIC.cmd-Datei und die SetupFailure.cmd-Datei müssen sich C:\Windows\Setup\Scripts sein.  
  
#### <a name="to-define-post-initial-configuration-customizations"></a>Definieren Sie Anpassungen nach der Erstkonfiguration  
  
1.  Schreiben Sie Code, der vom Skript PostIC.cmd aufgerufen wird.  
  
2.  Mit dem Editor, erstellen Sie eine Datei namens PostIC.cmd, und fügen Sie den Aufruf an den Code, den Sie in Schritt1 erstellt haben. Stellen Sie sicher, dass Ihr Code einen Erfolgswert zurückgibt.  
  
3.  Speichern Sie PostIC.cmd in C:\Windows\Setup\Scripts.  
  
4.  (Optional) Erstellen Sie eine SetupFailure.cmd-Datei, die Code ausgeführt wird, wenn PostIC.cmd ungleich 0 zurückgibt.  
  
###  <a name="BKMK_SetupFailure"></a>SetupFailure.cmd  
 Sie können Benachrichtigungen zu Problemen bei der Erstkonfiguration mithilfe der SetupFailure.cmd bereitstellen. Die SetupFailure.cmd-Datei enthält den Code, den ausgeführt wird, wenn Probleme auftreten, werden soll. Die Datei SetupFailure.cmd in C:\Windows\Setup\Scripts und wird ausgeführt, wenn ein Problem auftritt, bei einem setuptask oder die PostIC.cmd-Datei einen Wert ungleich 0 zurückgibt.  
  
##### <a name="to-define-notifications"></a>Definieren von Benachrichtigungen  
  
1.  Schreiben Sie Code, der vom Skript SetupFailure.cmd aufgerufen wird.  
  
2.  Mit dem Editor, erstellen Sie eine Datei namens SetupFailure.cmd, und fügen Sie den Aufruf an den Code, den Sie in Schritt1 erstellt haben. Stellen Sie sicher, dass Ihr Code einen Erfolgswert zurückgibt.  
  
3.  Speichern Sie SetupFailure.cmd in C:\Windows\Setup\Scripts.  
  
## <a name="see-also"></a>Siehe auch  
 [Erste Schritte mit Windows Server Essentials ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)