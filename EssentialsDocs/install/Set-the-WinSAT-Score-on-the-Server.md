---
title: Festlegen der WinSAT-Bewertung auf dem Server
description: Beschreibt die Verwendung von Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 911dc494-0f8f-4723-93d6-2106f914b906
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 20aafa957bd49f6522bfef98a2f8626dc5aab9df
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80311503"
---
# <a name="set-the-winsat-score-on-the-server"></a>Festlegen der WinSAT-Bewertung auf dem Server

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Sie sollten die WinSAT-CPU-Bewertung für einen Server festlegen, auf dem das Betriebssystem Windows Server Essentials ausgeführt wird, um die Video Streaming-Auflösung zu optimieren. Dazu erstellen und installieren Sie die XML-Datei, die die Informationen zur WinSAT-Bewertung enthält.  
  
## <a name="obtain-the-winsat-cpu-score"></a>Abrufen der WinSAT-CPU-Bewertung  
 Mit dem OPK wird Ihnen ein Programm namens "WinServerSAT.exe" zur Verfügung gestellt, das die WinSAT-CPU-Bewertung ermittelt und diese Information in die Datei "WinServerSAT.xml" einfügt, die vom Betriebssystem gelesen wird.  
  
#### <a name="to-obtain-the-winsat-cpu-score"></a>So rufen Sie die WinSAT-CPU-Bewertung ab  
  
1. Kopieren Sie resources\winserversat\\* auf dem Referenz Computer.  
  
2. Öffnen Sie auf dem Referenzcomputer ein Eingabeaufforderungsfenster mit erhöhten Rechten.  
  
3. Wenn der Ordner "%ProgramFiles%\Windows Server\Bin\OEM" nicht vorhanden ist, geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE.  
  
    **mkdir "%ProgramFiles%\Windows server\bin\oem"**  
  
4. Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE.  
  
    **Winserversat. exe "%ProgramFiles%\Windows server\bin\oem\winserversat.xml"**  
  
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
