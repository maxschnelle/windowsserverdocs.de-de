---
title: netcfg
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 8f8368aaff16592a55cc9def84d593cf323f28ee
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373293"
---
# <a name="netcfg"></a>netcfg

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Installiert den Windows Preinstallation Environment (WinPE), eine für die Bereitstellung von Arbeitsstationen verwendete Lightweight-Version von Windows.   
## <a name="syntax"></a>Syntax  
```  
netcfg [/v] [/e] [/winpe] [/l ] /c /i  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|/v|Ausführliches (detaillierter) Modus ausführen|  
|/e|Verwenden von Wartungs Umgebungsvariablen während der Installation und Deinstallation|  
|/winpe|Installiert TCP/IP, NetBIOS und den Microsoft-Client für die Vorinstallation von Windows.|  
|/l|Gibt den Speicherort von INF an.|  
|/c|Stellt die Klasse der zu installierenden Komponente bereit. Protokoll, Dienst oder Client|  
|/i|Gibt die Komponenten-ID an.|  
|/s|Stellt den Typ der anzuzeigenden Komponenten bereit.<br /><br />\ta = Adapter, n = NET Components|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  
## <a name="BKMK_Examples"></a>Beispiele  
So installieren Sie das Protokoll *Beispiel* mithilfe von "c:\oemdir\example.inf":  
```  
netcfg /l c:\oemdir\example.inf /c p /i example  
```  
So installieren Sie den *MS_Server* -Dienst:  
```  
netcfg /c s /i MS_Server  
```  
So installieren Sie TCP/IP, NetBIOS und Microsoft Client für Windows Preinstallation Environment  
```  
netcfg /v /winpe  
```  
So zeigen Sie an, ob Component *MS_IPX* installiert ist:  
```  
netcfg /q MS_IPX  
```  
So deinstallieren Sie Component *MS_IPX*:  
```  
netcfg /u MS_IPX  
```  
So zeigen Sie alle installierten NET-Komponenten an:  
```  
netcfg /s n  
```  
Zeigt Bindungs Pfade mit *MS_TCPIP*an:  
```  
netcfg /b ms_tcpip  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
