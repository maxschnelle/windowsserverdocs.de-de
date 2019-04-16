---
title: Festlegen der WinSAT-Bewertung auf dem Server
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 911dc494-0f8f-4723-93d6-2106f914b906
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 77866acccac13ac48da8779700c8654f2c7f3277
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="set-the-winsat-score-on-the-server"></a>Festlegen der WinSAT-Bewertung auf dem Server

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Sie sollten die WinSAT-CPU-Bewertung für einen Server festlegen, die das Betriebssystem Windows Server Essentials zum Optimieren Sie die Video-Streaming-Auflösung ausgeführt wird. Dazu erstellen und installieren Sie die XML-Datei, die die Informationen zur WinSAT-Bewertung enthält.  
  
## <a name="obtain-the-winsat-cpu-score"></a>Abrufen der WinSAT-CPU-Bewertung  
 Sie sind ein Programm bereitgestellt, mit dem OPK namens WinServerSAT.exe, die die WinSAT-CPU-Bewertung ermittelt und diese Information in der WinServerSAT.xml-Datei, die vom Betriebssystem gelesen.  
  
#### <a name="to-obtain-the-winsat-cpu-score"></a>Die WinSAT-CPU-Bewertung abrufen  
  
1.  Kopieren Sie die Resources\WinServerSAT\\ * ADK-Medium auf dem Referenzcomputer.  
  
2.  Öffnen Sie auf dem Referenzcomputer ein Eingabeaufforderungsfenster mit erhöhten Rechten aus.  
  
3.  Wenn der Ordner "%ProgramFiles%\Windows Server\Bin\OEM" nicht vorhanden ist, geben Sie folgenden Befehl ein, und drücken Sie dann die EINGABETASTE.  
  
     **Mkdir "%ProgramFiles%\Windows Server\Bin\OEM"**  
  
4.  Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE.  
  
     **WinServerSAT.exe "%ProgramFiles%\Windows Server\Bin\OEM\WinServerSAT.xml"**  
  
 Das folgende Beispiel zeigt die XML-Inhalt der Datei WinServerSAT.xml, die erstellt wird.  
  
```  
  
<?xml version="1.0" encoding="UTF-16"?>  
<WinSAT>  
   <CpuScore description="WinSAT CPU score">WinSAT_Score</CpuScore>  
</WinSAT>  
```  
  
 Wo *WinSAT_Score* ersetzt wird, mit dem Wert, der auf dem Server erkannt wird.  
  
> [!IMPORTANT]
>  Sie müssen WinServerSAT.exe "," winsat.prx "," winsat.wmv "und" WinSATEncode.wmv Dateien vom Referenzcomputer entfernen, bevor Sie das Image erfassen.
