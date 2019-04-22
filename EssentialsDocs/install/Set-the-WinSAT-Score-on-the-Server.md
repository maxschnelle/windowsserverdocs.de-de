---
title: Festlegen der WinSAT-Bewertung auf dem Server
description: Beschreibt, wie Windows Server Essentials
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819951"
---
# <a name="set-the-winsat-score-on-the-server"></a>Festlegen der WinSAT-Bewertung auf dem Server

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Sie sollten die WinSAT-CPU-Bewertung für einen Server festlegen, die die Windows Server Essentials-Betriebssystems zur Optimierung der video-streaming-Lösung ausgeführt wird. Dazu erstellen und installieren Sie die XML-Datei, die die Informationen zur WinSAT-Bewertung enthält.  
  
## <a name="obtain-the-winsat-cpu-score"></a>Abrufen der WinSAT-CPU-Bewertung  
 Mit dem OPK wird Ihnen ein Programm namens "WinServerSAT.exe" zur Verfügung gestellt, das die WinSAT-CPU-Bewertung ermittelt und diese Information in die Datei "WinServerSAT.xml" einfügt, die vom Betriebssystem gelesen wird.  
  
#### <a name="to-obtain-the-winsat-cpu-score"></a>So rufen Sie die WinSAT-CPU-Bewertung ab  
  
1.  Kopieren Sie die Resources\WinServerSAT\\* ADK-Medium, auf dem Referenzcomputer.  
  
2.  Öffnen Sie auf dem Referenzcomputer ein Eingabeaufforderungsfenster mit erhöhten Rechten.  
  
3.  Wenn der Ordner "%ProgramFiles%\Windows Server\Bin\OEM" nicht vorhanden ist, geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE.  
  
     **mkdir "%ProgramFiles%\Windows Server\Bin\OEM"**  
  
4.  Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE.  
  
     **WinServerSAT.exe "%ProgramFiles%\Windows Server\Bin\OEM\WinServerSAT.xml"**  
  
 Das folgende Beispiel zeigt den XML-Inhalt der neu erstellten Datei "WinServerSAT.xml".  
  
```  
  
<?xml version="1.0" encoding="UTF-16"?>  
<WinSAT>  
   <CpuScore description="WinSAT CPU score">WinSAT_Score</CpuScore>  
</WinSAT>  
```  
  
 Wobei *WinSAT_Score* durch den auf dem Server gefundenen Wert ersetzt wird.  
  
> [!IMPORTANT]
>  Sie müssen die Dateien "WinServerSAT.exe", "winsat.prx", "winsat.wmv" und "WinSATEncode.wmv" vom Referenzcomputer entfernen, bevor Sie das Abbild aufzeichnen.
