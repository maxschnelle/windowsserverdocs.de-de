---
title: ntfrsutl
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d7721a19-5a87-4ab6-b816-65d2da2c811f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2dd245b7d85d6d5668262d3800ab72e35b852246
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836621"
---
# <a name="ntfrsutl"></a>ntfrsutl

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Sichert die interne Tabellen, Thread- und Speicherinformationen für den NT-Dateireplikationsdienst \(NTFRS\). Es wird für lokale Server und Remoteserver ausgeführt. Die Recovery-Einstellung für NTFRS im Dienststeuerungs-Manager \(SCM\) zur Suche und behalten wichtige Protokollieren von Ereignissen auf dem Computer entscheidend sein können. Dieses Tool bietet eine praktische Methode, um diese Einstellungen zu überprüfen.   
  
## <a name="syntax"></a>Syntax  
  
```  
ntfrsutl[idtable|configtable|inlog|outlog][<computer>]  
ntfrsutl[memory|threads|stage][<computer>]  
ntfrsutl ds[<computer>]  
ntfrsutl [sets][<computer>]  
ntfrsutl [version][<computer>]  
ntfrsutl poll[/quickly[=[<N>]]][/slowly[=[<N>]]][/now][<computer>]  
```  
  
### <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|IDtable|ID-Tabelle|  
|configtable|FRS-Konfigurationstabelle|  
|inlog|Eingehende Protokoll|  
|outlog|Das ausgehende Protokoll|  
|<computer>|Gibt den Computer.|  
|memory|Speicherauslastung|  
|threads||  
|Stufe||  
|ds|werden die DS-Instanz der NTFRS-Dienst angezeigt.|  
|Legt|Gibt an, die active-Replikatsätze|  
|version|Gibt die API als auch der NTFRS-Dienst-Versionen.|  
|Abruf|Gibt den aktuellen Abrufintervalle an.<br /><br />Parameter:<br /><br /><ul><li>**\/schnell** \[ **\=** \[ <N> \] \] \(fragt schnell ab.  \)<br /><br /><ul><li>**schnell** \- schnell abgefragt werden, bis stabile Konfiguration Rectrieved ist</li><li>**schnell\=**  \- fragt schnell alle standardmäßigen Minuten ab.</li><li>**schnell\=**  <N> \- schnell fragt jede *N* Minuten</li></ul></li><li>**\/langsam** \[ **\=** \[ <N> \] \] \(fragt langsam ab.\)<br /><br /><ul><li>**langsam** \- langsam abgefragt werden, bis stabile Konfiguration abgerufen werden</li><li>**langsam\=**  \- fragt langsam alle Standard-Minuten</li><li>**langsam\=**  <N> \- schnell fragt jede *N* Minuten</li></ul></li><li>**\/jetzt** \(fragt Sie ab jetzt\)</li></ul>|  
|\/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  
  
## <a name="BKMK_Examples"></a>Beispiele für  
So bestimmen Sie das Abrufintervall für die Dateireplikation  
  
```  
C:\Program Files\SupportTools>ntfrsutl poll wrkstn-1  
```  
  
Um zu bestimmen, die aktuellen NTFRS Anwendungsprogrammierschnittstelle \(API\) Version:  
  
```  
C:\Program Files\SupportTools>ntfrsutl version  
```  
  
## <a name="additional-references"></a>Zusätzliche Referenzen  
  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
  
  
  

