---
title: "Hinzufügen von Integritätswarnungen"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 270e0aac-dc42-46f3-a20b-a68ffbded06d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: cf0c062b92c687f5f7b33b419eafdca2dd3bbbfc
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="add-health-alerts"></a>Hinzufügen von Integritätswarnungen

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Ein Integritäts-Add-In bietet Definitionen für Warnungen, integritätsprüfungen und Reparaturen für Netzwerkprobleme. Ein Integritäts-Add-In besteht aus XML-Dateien, die Kommentieren, Code oder Daten, die zum Bewerten der Integritätsinformationen für ein bestimmtes Feature verwendet werden. Integritäts-Add-Ins werden von Entwicklern erstellt und der Administrator auf dem Server und Clientcomputern installiert.  
  
 Weitere Informationen finden Sie in der [SDK für Windows Server-Lösungen](https://go.microsoft.com/fwlink/?LinkID=248648) ausführliche Informationen zum Erstellen eines Integritäts-add-Ins.  
  
## <a name="installing-health-add-in-files"></a>Installieren die Integrität der Add-In-Dateien  
 Nachdem der Entwickler die XML-Dateien erstellt hat, müssen Sie eine Kopie der Dateien in den entsprechenden Speicherort auf dem Server und den Clientcomputern platzieren.  
  
#### <a name="to-install-the-xml-files-on-the-server"></a>So installieren Sie die XML-Dateien auf dem Server  
  
1.  In der **%ProgramFiles%\Windows** Ordner, erstellen Sie einen neuen Ordner namens **%programfiles%\Windows server\bin\Feature Definitions**. Sie können in diesem Ordner einen beliebigen Namen geben. Es wird empfohlen, dass der Name des Ordners, der Name der Funktion identisch sein.  
  
2.  Kopieren Sie die Definition.xml und die Definition.xml-config-Dateien in den neuen Ordner.  
  
3.  Wenn Sie Binärdateien für Bedingungen oder Aktionen erstellt haben, sollten Sie diese Dateien auch kopieren **%ProgramFiles%\Windows Server\Bin**.  
  
 Clientcomputer ausführen eine geplante Aufgabe alle 6 Stunden, die die XML-Dateien an den entsprechenden Speicherort abruft. Sie können die Synchronisierung zwischen dem Clientcomputer und dem Server erzwingen, indem Sie die Aufgabe manuell ausführen.  
  
#### <a name="to-install-the-xml-files-on-the-client-computer"></a>So installieren Sie die XML-Dateien auf dem Clientcomputer  
  
1.  Öffnen Sie die Aufgabenplanung.  
  
2.  Führen Sie die **HealthDefintionUpdateTask** im Taskplaner.  
  
    > [!NOTE]
    >  Dieser Task installiert keine Binärdateien. Sie müssen die Binärdateien manuell kopieren der **%ProgramFiles%\Windows Server\Bin** Ordner auf dem Clientcomputer.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)