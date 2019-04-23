---
title: ipxroute
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3a30304f-655e-43d2-a4ac-7568abf8975c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d995204eea0af776a2084a82411fa95542d1d77a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889091"
---
# <a name="ipxroute"></a>ipxroute

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt an, und ändert Informationen über die Routingtabellen, die von der IPX-Protokoll verwendet wird. Ohne Parameter verwendet **Ipxroute** zeigt die Standardeinstellungen für Pakete, die an unbekannte, multicast und broadcast-Adressen gesendet werden.   
## <a name="syntax"></a>Syntax  
```  
ipxroute servers [/type=X]  
ipxroute ripout <Network>  
ipxroute resolve {guid | name} {GUID | <AdapterName>}  
ipxroute board= N [def] [gbr] [mbr] [remove=xxxxxxxxxxxx]  
ipxroute config  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|servers[ /type=X]|Zeigt die Tabelle (Service Access Point, SAPs) für den angegebenen Servertyp.  **X** muss eine ganze Zahl sein. Z. B. **/type = 4** zeigt alle Dateiserver. Wenn Sie keinen angeben **/type**, **Ipxroute Server** alle Arten von Servern, aufgelistet nach dem Servernamen angezeigt.|  
|Ripout Netzwerk|Ermittelt, ob *Netzwerk* erreichbar ist, von der Routingtabelle die IPX-Stapels, und bei Bedarf eine Rip-Anforderung gesendet.  *Netzwerk* IPX-Netzwerknummer Segment ist.|  
|Beheben {GUID&#124; Name} {GUID&#124; AdapterName}|Löst den Namen der GUID, seinen Anzeigenamen oder den Anzeigenamen ein, um die GUID an.|  
|Board = *N*|Gibt den Netzwerkadapter für die Abfragen oder Festlegen von Parametern an.|  
|DEF|Pakete, die alle ROUTEN Übertragung gesendet. Wenn ein Paket an eine eindeutige Adresse für die Karte MAC (Media Access) übertragen wird, die nicht in der Quellroutingtabelle, **Ipxroute** sendet das Paket an die einzelnen ROUTEN, die standardmäßig übertragen.|  
|gbr|Pakete, die alle ROUTEN Übertragung gesendet. Wenn ein Paket übertragen wird, an die Broadcastadresse (FFFFFFFFFFFF), **Ipxroute** sendet das Paket an die einzelnen ROUTEN, die standardmäßig übertragen.|  
|mbr|Pakete, die alle ROUTEN Übertragung gesendet. Wenn ein Paket übertragen wird, um eine Multicastadresse (C000xxxxxxxx), **Ipxroute** sendet das Paket an die einzelnen ROUTEN, die standardmäßig übertragen.|  
|remove= *xxxxxxxxxxxx*|Entfernt die angegebene Knotenadresse aus der Routingtabelle der Quelle an.|  
|config|Zeigt Informationen über alle Bindungen für die IPX konfiguriert ist.|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  
## <a name="BKMK_Examples"></a>Beispiele für  
Um anzuzeigen, die Netzwerksegmente, denen die Arbeitsstation verbunden ist, Knotenadresse für Arbeitsstation und Frametyp verwendet wird, geben Sie Folgendes ein:  
```  
ipxroute config  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
