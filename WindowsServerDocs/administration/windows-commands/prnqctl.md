---
title: prnqctl
description: Drucken einer Testseite, anhalten oder Fortsetzen eines Druckers.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8df9dfa7-984c-4276-bb7d-e7675e7c399e jpjofre
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: d07d8caa0568b26f5edc16258085a59ecdafcf4e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837203"
---
# <a name="prnqctl"></a>prnqctl

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Druckt eine Testseite, hält einen Drucker an oder setzt ihn fort und löscht eine Drucker Warteschlange.  

## <a name="syntax"></a>Syntax  
```  
cscript Prnqctl {-z | -m | -e | -x | -?} [-s <ServerName>]   
[-p <printerName>] [-u <UserName>] [-w <Password>]  
```  
### <a name="parameters"></a>Parameter  

|Parameter|Beschreibung|  
|-------|--------|  
|-z|hält das Drucken auf dem Drucker an, der mit dem Parameter **-p** angegeben wird.|  
|-m|Setzt den Druckvorgang auf dem Drucker fort, der mit dem **-p-** Parameter angegeben wird.|  
|-e|druckt eine Testseite auf dem Drucker, der mit dem Parameter **-p** angegeben wird.|  
|-x|Bricht alle Druckaufträge auf dem Drucker ab, der mit dem **-p-** Parameter angegeben wird.|  
|-s \<Servername >|Gibt den Namen des Remote Computers an, der den Drucker hostet, den Sie verwalten möchten. Wenn Sie keinen Computer angeben, wird der lokale Computer verwendet.|  
|-p \<PrinterName >|Gibt den Namen des Druckers an, den Sie verwalten möchten. Erforderlich|  
|-u \<Benutzername >-w \<Kennwort ein >|Gibt ein Konto mit Berechtigungen zum Herstellen einer Verbindung mit dem Computer an, der den zu verwaltenden Drucker hostet. Alle Mitglieder der lokalen Administratoren Gruppe des Ziel Computers verfügen über diese Berechtigungen, die Berechtigungen können jedoch auch anderen Benutzern erteilt werden. Wenn Sie kein Konto angeben, müssen Sie unter einem Konto mit diesen Berechtigungen angemeldet sein, damit der Befehl funktioniert.|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  

## <a name="remarks"></a>Hinweise  
- Der **prnqctl** -Befehl ist ein Visual Basic Skript, das sich im Verzeichnis "%windir%\SYSTEM32\ printing_Admin_Scripts\\<language>" befindet. Wenn Sie diesen Befehl verwenden möchten, geben Sie an einer Eingabeaufforderung **cscript** ein, gefolgt vom vollständigen Pfad der prnqctl-Datei, oder ändern Sie die Verzeichnisse in den entsprechenden Ordner. Beispiel:  
  ```  
  cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnqctl  
  ```  
- Wenn die Informationen, die Sie angeben, Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen (z. b. `"computer Name"`).  

## <a name="examples"></a><a name="BKMK_examples"></a>Beispiele  
Geben Sie Folgendes ein, um eine Testseite auf dem Laserprinter1-Drucker zu drucken, der vom \\\server1-Computer gemeinsam genutzt wird  
```  
cscript Prnqctl -e -s Server1 -p Laserprinter1  
```  
Geben Sie Folgendes ein, um das Drucken auf dem Laserprinter1-Drucker auf dem lokalen Computer anzuhalten:  
```  
cscript Prnqctl -z -p Laserprinter1  
```  
Um alle Druckaufträge auf dem Laserprinter1-Drucker auf dem lokalen Computer abzubrechen, geben Sie Folgendes ein:  
```  
cscript Prnqctl -x -p Laserprinter1  
```  

## <a name="additional-references"></a>Weitere Verweise  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
[Befehls Verweis drucken](print-command-reference.md)  
