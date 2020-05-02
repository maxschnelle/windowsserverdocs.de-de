---
title: ipxroute
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3a30304f-655e-43d2-a4ac-7568abf8975c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5a6d0cac3f835e86d40e03141c0da51d514ef0c6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724808"
---
# <a name="ipxroute"></a>ipxroute

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu den Routing Tabellen an, die vom IPX-Protokoll verwendet werden, und ändert diese. Wird ohne Parameter verwendet, zeigt **IPXRoute** die Standardeinstellungen für Pakete an, die an unbekannte, Broadcast-und Multicast Adressen gesendet werden.   
## <a name="syntax"></a>Syntax  
```  
ipxroute servers [/type=X]  
ipxroute ripout <Network>  
ipxroute resolve {guid | name} {GUID | <AdapterName>}  
ipxroute board= N [def] [gbr] [mbr] [remove=xxxxxxxxxxxx]  
ipxroute config  
```  
#### <a name="parameters"></a>Parameter  
|Parameter|BESCHREIBUNG|  
|-------|--------|  
|Server [/Type = X]|Zeigt die Tabelle für den Dienst Zugriffspunkt (SAP) für den angegebenen Servertyp an.  **X** muss eine ganze Zahl sein. Beispielsweise werden in **/Type = 4** alle Dateiserver angezeigt. Wenn Sie **/Type**nicht angeben, werden von **IPXRoute-Servern** alle Server Typen angezeigt, die nach Servernamen aufgelistet sind.|  
|ausreißungsnetzwerk|Ermittelt, ob das *Netzwerk* erreichbar ist, indem die Routing Tabelle des IPX-Stapels und ggf. eine RIP-Anforderung gesendet wird.  *Network* ist die IPX-Netzwerksegment Nummer.|  
|{GUID&#124; Name} {GUID&#124; Adapter Name} auflösen|Löst den Namen der GUID in ihren anzeigen Amen oder den anzeigen Amen für die GUID auf.|  
|Board = *N*|Gibt den Netzwerkadapter an, für den Parameter abgefragt oder festgelegt werden sollen.|  
|def|Sendet Pakete an die Broadcast alle Routen. Wenn ein Paket an eine eindeutige MAC-Adresse (Media Access Card) übertragen wird, die sich nicht in der Quell Routing Tabelle befindet, sendet **IPXRoute** das Paket standardmäßig an die einzelnen Routen Broadcast.|  
|GbR|Sendet Pakete an die Broadcast alle Routen. Wenn ein Paket an die Broadcast Adresse (FFFFFFFFFFFF) übertragen wird, sendet **IPXRoute** das Paket standardmäßig an die einzelnen Routen Broadcast.|  
|MBR|Sendet Pakete an die Broadcast alle Routen. Wenn ein Paket an eine Multicast Adresse (C000xxxxxxxx) übertragen wird, sendet **IPXRoute** das Paket standardmäßig an die einzelnen Routen Broadcast.|  
|Remove = *xxxxxxxxxxxx*|entfernt die angegebene Knotenadresse aus der Quell Routing Tabelle.|  
|config|Zeigt Informationen zu allen Bindungen an, für die IPX konfiguriert ist.|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  
## <a name="examples"></a>Beispiele  
Geben Sie Folgendes ein, um die Netzwerksegmente anzuzeigen, an die die Arbeitsstation angefügt ist, und den verwendeten Rahmentyp:  
```  
ipxroute config  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
