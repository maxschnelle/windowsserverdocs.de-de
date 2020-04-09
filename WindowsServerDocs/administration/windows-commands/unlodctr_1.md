---
title: unlodctr
description: Windows-Befehls Thema für unlodctr, mit dem Namen von Leistungs Zählern und der Erläuterung von Text für einen Dienst oder einen Gerätetreiber aus der Systemregistrierung entfernt werden
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fc8aa6f0-c1d9-47ea-937a-28152148e774
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fe7fc3c9eafefd59a5daab625e3af06b6addd292
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832257"
---
# <a name="unlodctr"></a>unlodctr

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Entfernt die Namen von **Leistungs Zählern** und **erläutert** den Text für einen Dienst oder einen Gerätetreiber aus der Systemregistrierung.   

## <a name="syntax"></a>Syntax  
```  
Unlodctr <DriverName>   
```  
#### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|\<DriverName >|entfernt die Namen Einstellungen des Leistungs Zählers und den erläuternden Text für Treiber-oder Dienst <DriverName> aus der Windows Server 2003-Registrierung.|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  

## <a name="remarks"></a>Hinweise  
> [!WARNING]  
> Eine fehlerhafte Bearbeitung der Registrierung kann Ihr System schwer beschädigen. Bevor Sie Änderungen an der Registrierung vornehmen, sollten Sie alle wichtigen Computerdaten sichern.  

Wenn die Informationen, die Sie angeben, Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen (z. b. <DriverName>).  

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
So entfernen Sie die aktuellen Registrierungs Einstellungen für die Leistung und den leistungsstarken Text für den Simple Mail Transfer Protocol (SMTP)-Dienst:  
```  
unlodctr SMTPSVC  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  
