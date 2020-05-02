---
title: netcfg
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e2daaab7-12db-4e36-b70c-db8906d084f7 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a5945da45ee01fd5bf5f89a7835c4bae0b5534c4
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723806"
---
# <a name="netcfg"></a>netcfg

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Installiert den Windows Preinstallation Environment (WinPE), eine für die Bereitstellung von Arbeitsstationen verwendete Lightweight-Version von Windows.
## <a name="syntax"></a>Syntax
```
netcfg [/v] [/e] [/winpe] [/l ] /c /i
```
#### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|/v|Ausführliches **(detaillierter** ) Modus ausführen|
|/e|Verwenden von Wartungs **Umgebungs** Variablen während der Installation und Deinstallation|
|/winpe|Installiert TCP/IP, NetBIOS und den Microsoft-Client für Windows Preinstallation Environment (WinPE).|
|/l|Gibt den **Speicherort** von INF an.|
|/C|Stellt die **Klasse** der zu installierenden Komponente bereit. Protokoll, Dienst oder Client|
|/i|Gibt die Komponenten- **ID** an.|
|/s|Stellt den Typ der **anzuzeigenden**Komponenten bereit.<p>\ta = Adapter, n = NET Components|
|/b|Zeigt die **Bindungs Pfade**an, wenn eine Zeichenfolge mit dem Namen des Pfads folgt.|
|/?|Zeigt die **Hilfe** an der Eingabeaufforderung an.|

## <a name="examples"></a>Beispiele

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
So zeigen Sie an, ob die Komponenten *MS_IPX* installiert ist:
```
netcfg /q MS_IPX
```
So deinstallieren Sie die Komponenten *MS_IPX*:
```
netcfg /u MS_IPX
```
So zeigen Sie alle installierten NET-Komponenten an:
```
netcfg /s n
```
So zeigen Sie Bindungs Pfade mit *MS_TCPIP*an:
```
netcfg /b ms_tcpip
```
## <a name="additional-references"></a>Zusätzliche Referenzen
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
