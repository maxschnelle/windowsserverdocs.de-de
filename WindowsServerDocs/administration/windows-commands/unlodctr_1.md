---
title: unlodctr
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fc8aa6f0-c1d9-47ea-937a-28152148e774
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e1a662da10acc65b4ad2fd0d055cf9d46de603be
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886651"
---
# <a name="unlodctr"></a>unlodctr

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Entfernt den Namen Leistungsindikatoren und erläuternden Text eines Diensts oder Gerätetreibers aus der Registrierung des Systems an.   

## <a name="syntax"></a>Syntax  
```  
Unlodctr <DriverName>   
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|\<DriverName>|Entfernt die Leistung Leistungsindikator Einstellungen und Erklärungstext für die Treiber oder Dienst <DriverName> aus der Registrierung von Windows Server 2003.|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  

## <a name="remarks"></a>Hinweise  
> [!WARNING]  
> Durch eine fehlerhafte Bearbeitung der Registrierung können schwerwiegende Schäden am System verursacht werden. Bevor Sie Änderungen an der Registrierung vornehmen, sollten Sie alle wichtigen Computerdaten sichern.  

Wenn die Informationen, die Sie angeben, die Leerzeichen enthält, verwenden Sie den Text in Anführungszeichen (z. B. "<DriverName>").  

## <a name="BKMK_Examples"></a>Beispiele für  
So entfernen die aktuellen registrierungseinstellungen für die Leistung und Leistungsindikator erläuternden Texts für den Dienst Simple Mail Transfer Protocol (SMTP):  
```  
unlodctr SMTPSVC  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
  
