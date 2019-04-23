---
title: netcfg
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2daaab7-12db-4e36-b70c-db8906d084f7 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: aed535f843da6d735526ea97c07f94564dc00dc6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871321"
---
# <a name="netcfg"></a>netcfg

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Installiert die Windows Preinstallation Environment (WinPE), eine einfache Version von Windows zum Bereitstellen von Arbeitsstationen verwendet.   
## <a name="syntax"></a>Syntax  
```  
netcfg [/v] [/e] [/winpe] [/l ] /c /i  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|/v|Führen Sie im Modus für ausführliche (Details)|  
|/ e|Wartung Umgebungsvariablen verwenden, während der Installation und Deinstallation|  
|/WinPE|Wird die TCP/IP "," NetBIOS-Namen "und" Microsoft-Client für Windows preinstallation-Umgebung installiert.|  
|/l|Gibt die Position des INF|  
|/c|Stellt die Klasse der Komponente installiert werden; Protokoll, Dienst oder client|  
|/i|Stellt die Komponenten-ID|  
|/s|Stellt den Typ der Komponenten angezeigt<br /><br />\ta =-Adapter, n = net-Komponenten|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  
## <a name="BKMK_Examples"></a>Beispiele für  
So installieren Sie das Protokoll *Beispiel* c:\oemdir\example.inf verwenden:  
```  
netcfg /l c:\oemdir\example.inf /c p /i example  
```  
So installieren Sie die *MS_Server* Dienst:  
```  
netcfg /c s /i MS_Server  
```  
So installieren Sie TCP/IP "," NetBIOS-Namen "und" Microsoft-Client für Windows preinstallation environment  
```  
netcfg /v /winpe  
```  
Anzeigen, wenn die Komponente *MS_IPX* installiert ist:  
```  
netcfg /q MS_IPX  
```  
So deinstallieren Sie die Komponente *MS_IPX*:  
```  
netcfg /u MS_IPX  
```  
Um alle anzuzeigen. Sie net-Komponenten installiert:  
```  
netcfg /s n  
```  
Um Pfade, die Bindung wird *MS_TCPIP*:  
```  
netcfg /b ms_tcpip  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
