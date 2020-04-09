---
title: ipxroute
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3a30304f-655e-43d2-a4ac-7568abf8975c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f1e011835dbdbcf7be1daca2cdfbd47c39f9355c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842063"
---
# <a name="ipxroute"></a>ipxroute

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

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
|Parameter|Beschreibung|  
|-------|--------|  
|Server [/Type = X]|Zeigt die Tabelle für den Dienst Zugriffspunkt (SAP) für den angegebenen Servertyp an.  **X** muss eine ganze Zahl sein. Beispielsweise werden in **/Type = 4** alle Dateiserver angezeigt. Wenn Sie **/Type**nicht angeben, werden von **IPXRoute-Servern** alle Server Typen angezeigt, die nach Servernamen aufgelistet sind.|  
|ausreißungsnetzwerk|Ermittelt, ob das *Netzwerk* erreichbar ist, indem die Routing Tabelle des IPX-Stapels und ggf. eine RIP-Anforderung gesendet wird.  *Network* ist die IPX-Netzwerksegment Nummer.|  
|{GUID&#124; -Name} {GUID&#124; Adapter Name} auflösen|Löst den Namen der GUID in ihren anzeigen Amen oder den anzeigen Amen für die GUID auf.|  
|Board = *N*|Gibt den Netzwerkadapter an, für den Parameter abgefragt oder festgelegt werden sollen.|  
|auflösenden|Sendet Pakete an die Broadcast alle Routen. Wenn ein Paket an eine eindeutige MAC-Adresse (Media Access Card) übertragen wird, die sich nicht in der Quell Routing Tabelle befindet, sendet **IPXRoute** das Paket standardmäßig an die einzelnen Routen Broadcast.|  
|GbR|Sendet Pakete an die Broadcast alle Routen. Wenn ein Paket an die Broadcast Adresse (FFFFFFFFFFFF) übertragen wird, sendet **IPXRoute** das Paket standardmäßig an die einzelnen Routen Broadcast.|  
|MBR|Sendet Pakete an die Broadcast alle Routen. Wenn ein Paket an eine Multicast Adresse (C000xxxxxxxx) übertragen wird, sendet **IPXRoute** das Paket standardmäßig an die einzelnen Routen Broadcast.|  
|Remove = *xxxxxxxxxxxx*|entfernt die angegebene Knotenadresse aus der Quell Routing Tabelle.|  
|config|Zeigt Informationen zu allen Bindungen an, für die IPX konfiguriert ist.|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  
## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
Geben Sie Folgendes ein, um die Netzwerksegmente anzuzeigen, an die die Arbeitsstation angefügt ist, und den verwendeten Rahmentyp:  
```  
ipxroute config  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
