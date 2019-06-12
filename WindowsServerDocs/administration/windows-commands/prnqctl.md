---
title: prnqctl
description: Drucken einer Testseite, Anhalten oder Fortsetzen eines Druckers.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8df9dfa7-984c-4276-bb7d-e7675e7c399e jpjofre
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 1ba58970e76497f6e91c53c73a429eb65a275b2f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442104"
---
# <a name="prnqctl"></a>prnqctl

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Druckt eine Testseite, angehalten oder fortgesetzt wird einen Drucker und löscht eine Druckerwarteschlange.  

## <a name="syntax"></a>Syntax  
```  
cscript Prnqctl {-z | -m | -e | -x | -?} [-s <ServerName>]   
[-p <printerName>] [-u <UserName>] [-w <Password>]  
```  
## <a name="parameters"></a>Parameter  

|Parameter|Beschreibung|  
|-------|--------|  
|-z|Hält den Druckvorgang auf dem mit angegebenen Drucker der **-p** Parameter.|  
|-m|Drucken auf dem mit angegebenen Drucker setzt die **-p** Parameter.|  
|-e|Druckt eine Testseite auf dem mit angegebenen Drucker der **-p** Parameter.|  
|-x|Bricht alle Druckaufträge auf dem mit angegebenen Drucker der **-p** Parameter.|  
|-s \<ServerName >|Gibt den Namen des Remotecomputers, der den Drucker hostet, den Sie verwalten möchten. Wenn Sie einen Computer nicht angeben, wird der lokale Computer verwendet.|  
|-p \<Druckername >|Gibt den Namen des Druckers, den Sie verwalten möchten. Erforderlich.|  
|-u \<UserName > -w \<Kennwort >|Gibt ein Konto mit Berechtigungen zum Verbinden mit dem Computer, der den Drucker hostet, den Sie verwalten möchten. Alle Mitglieder der lokalen Gruppe Administratoren des Zielcomputers über diese Berechtigungen verfügen, aber die Berechtigungen können auch für andere Benutzer erteilt werden. Wenn Sie ein Konto nicht angeben, müssen Sie über ein Konto mit Berechtigungen für der Befehl funktioniert angemeldet sein.|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  

## <a name="remarks"></a>Hinweise  
- Die **Prnqctl** Befehl ist eine Visual Basic-Skript befindet sich in der %WINdir%\System32\printing_Admin_Scripts\\ <language> Verzeichnis. Um diesen Befehl an einer Eingabeaufforderung verwenden möchten, geben **Cscript** gefolgt von den vollständigen Pfad und die Prnqctl-Datei, oder wechseln in den entsprechenden Ordner. Zum Beispiel:  
  ```  
  cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnqctl  
  ```  
- Wenn die Informationen, die Sie angeben, die Leerzeichen enthält, verwenden Sie den Text in Anführungszeichen (z. B. `"computer Name"`).  

## <a name="BKMK_examples"></a>Beispiele für  
So drucken Sie eine Testseite Laserprinter1 Drucker freigegeben, indem die \\\Server1-Computer, Typ:  
```  
cscript Prnqctl -e -s Server1 -p Laserprinter1  
```  
Um Druckvorgänge auf dem Laserprinter1 Drucker auf dem lokalen Computer anzuhalten, geben Sie Folgendes ein:  
```  
cscript Prnqctl -z -p Laserprinter1  
```  
Geben Sie zum Abbrechen aller Druckaufträge Laserprinter1 Drucker auf dem lokalen Computer:  
```  
cscript Prnqctl -x -p Laserprinter1  
```  

#### <a name="additional-references"></a>Zusätzliche Referenzen  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
[Druckbefehlsreferenz](print-command-reference.md)  
