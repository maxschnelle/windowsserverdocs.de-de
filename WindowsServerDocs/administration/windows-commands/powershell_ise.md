---
title: PowerShell_ise
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 32c41b5b-a210-47d9-bd8c-91eb9830b4f0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b6ae96dcd40c894e0a528c06b461173f626fb2d2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837393"
---
# <a name="powershell_ise"></a>PowerShell_ise



Windows PowerShell Integrated Scripting Environment (ISE) ist eine grafische Host Anwendung, die es Ihnen ermöglicht, Skripts und Module in einer Grafik gestützten Umgebung zu lesen, zu schreiben, auszuführen, zu Debuggen und zu testen. Wichtige Funktionen wie IntelliSense, Show-Command, Ausschnitte, Vervollständigung mit der Tab-Taste, Syntax Farben, visuelles Debuggen und kontextbezogene Hilfe ermöglichen eine umfangreiche Skripterstellung.

Das Tool **PowerShell_ISE. exe** startet eine Windows PowerShell ISE Sitzung. Wenn Sie **PowerShell_ISE. exe**verwenden, können Sie die optionalen Parameter verwenden, um Dateien in Windows PowerShell ISE zu öffnen oder um eine Windows PowerShell ISE Sitzung ohne Profil oder mit einem Multithread-Apartment zu starten.

" **PowerShell_ISE. exe** " wurde in Windows PowerShell 2,0 eingeführt und in Windows PowerShell 3,0 erheblich erweitert.

## <a name="using-powershell_iseexe"></a>Verwenden von "PowerShell_ISE. exe"

Sie können **PowerShell_ISE. exe** verwenden, um eine Windows PowerShell-Sitzung wie folgt zu starten und zu beenden:
- Um eine Windows PowerShell ISE Sitzung zu starten, geben Sie in einem Eingabe Aufforderungs Fenster in Windows PowerShell oder im Startmenü Folgendes ein:  
  ```
  PowerShell_Ise
  ```  
- Zum Öffnen eines Skripts (. ps1), eines Skript Moduls (. psm1), eines Modul Manifests (. psd1), einer XML-Datei oder einer anderen unterstützten Datei in Windows PowerShell ISE verwenden Sie das folgende Befehls Format:  
  ```
  PowerShell_Ise <FilePath>
  ```  
  In Windows PowerShell 3,0 können Sie den optionalen **File** -Parameter wie folgt verwenden:  
  ```
  PowerShell_Ise -File <FilePath>
  ```  
- Verwenden Sie den **NoProfile** -Parameter, um eine Windows PowerShell ISE Sitzung ohne Ihre Windows PowerShell-Profile zu starten. (Der **NoProfile** -Parameter wird in Windows PowerShell 3,0 eingeführt.)  
  ```
  PowerShell_Ise -NoProfile
  ```  
- Verwenden Sie das folgende Befehls Format, um die Hilfedatei **PowerShell_ISE. exe** in einem Eingabe Aufforderungs Fenster anzuzeigen:  
  ```
  PowerShell_Ise -help, -?, /?
  ```  
  Eine umfassende Liste der Befehlszeilenparameter **PowerShell_ISE. exe** finden Sie unter [about_PowerShell_Ise. exe](https://go.microsoft.com/fwlink/?LinkId=256512).

## <a name="start-windows-powershell-ise-in-other-ways"></a>Windows PowerShell ISE auf andere Art und Weise starten

Weitere Informationen zu anderen Möglichkeiten zum Starten von Windows PowerShell ISE finden Sie unter [Starten von Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=135259).

## <a name="remarks"></a>Hinweise

Windows PowerShell wird auf der Server Core-Installationsoption von Windows Server-Betriebssystemen ausgeführt. Da Windows PowerShell ISE jedoch eine grafische Benutzeroberfläche erfordert, kann es nicht auf Server Core-Installationen ausgeführt werden.

## <a name="additional-references"></a>Weitere Verweise

[about_PowerShell_Ise. exe](https://go.microsoft.com/fwlink/?LinkId=256512)
[about_PowerShell. exe](https://go.microsoft.com/fwlink/?LinkID=113439)
[Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=107116)
[Skripterstellung mit Windows PowerShell](https://technet.microsoft.com/scriptcenter/dd742419) siehe auch