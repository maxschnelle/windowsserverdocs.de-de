---
title: tftp
description: Übertragen von Dateien zu und von einem Remotecomputer befindet.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 772f19a8-dafe-45cd-878a-f5691f6568ef vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ad195409076840fda0e8d6bf5cd0c295a62cdede
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845901"
---
# <a name="tftp"></a>tftp

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Überträgt Dateien in und aus einem remote-Computer in der Regel einem Computer mit UNIX, auf dem das Trivial File Transfer Protocol (Tftp)-Dienst oder der Daemon ausgeführt wird. TFTP wird normalerweise verwendet, von embedded-Geräten oder Systemen, die Firmware, Informationen zur Konfiguration oder ein Systemabbild während des Startvorgangs von einem Tftp-Server abrufen.   

## <a name="syntax"></a>Syntax  
```  
tftp [-i] [<Host>] [{get | put}] <Source> [<Destination>]  
```  

### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|-i|Gibt an, binäres Abbild Übertragungsmodus (auch als Oktett-Modus bezeichnet). Die Datei wird im Binärmodus byteweise übertragen. Verwenden Sie diesen Modus, bei der Übertragung von Binärdateien. Wenn **-i** wird weggelassen, wird die Datei im ASCII-Modus übertragen. Dies ist der Standardmodus für die Übertragung. In diesem Modus konvertiert die End-of-Line (EOL)-Zeichen in ein geeignetes Format für den angegebenen Computer an. Verwenden Sie diesen Modus, bei der Übertragung von Textdateien. Wenn eine Dateiübertragung erfolgreich ist, wird die Datenübertragungsrate angezeigt.|  
|\<Host\>|Gibt den lokalen Computer oder Remotecomputer an.|  
|Put|Überträgt die Datei *Quelle* auf dem lokalen Computer, auf die Datei *Ziel* auf dem Remotecomputer. Da das Tftp-Protokoll nicht der Benutzerauthentifizierung unterstützt, muss der Benutzer angemeldet sein, auf dem Remotecomputer, und die Dateien müssen auf dem Remotecomputer beschreibbar sein.|  
|get|Überträgt die Datei *Ziel* auf dem Remotecomputer in die Datei *Quelle* auf dem lokalen Computer.|  
|\<Quelle\>|Gibt die Datei übertragen.|  
|\<Ziel\>|Gibt an, um die Datei übertragen.|  

## <a name="remarks"></a>Hinweise  
-   Sie können mit den Funktionen Assistenten zum Hinzufügen den Tftp-Client installieren.  
-   Der Tftp-Protokoll unterstützt keine Authentifizierung oder Verschlüsselung Mechanismus, und daher kann ein Sicherheitsrisiko darstellen einführen. Installieren den Tftp-Client sollte nicht für Systeme, die mit dem Internet verbunden.  
-   Der Tftp-Client ist eine optionale Software und als unter Windows Vista und höheren Versionen des Windows-Betriebssystems als veraltet markiert. Ein Tftp-Server-Dienst wird aus Sicherheitsgründen nicht mehr von Microsoft bereitgestellt.  

## <a name="BKMK_Examples"></a>Beispiele für  
Kopieren Sie die Datei **boot.img** vom Remotecomputer **"host1"**.  
```  
tftp  -i Host1 get boot.img  
```  

## <a name="additional-references"></a>Weitere Verweise  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
